Your team has decided to leverage the capabilities of the Azure Event Hubs to manage and process the increasing transaction volumes coming through your system.

An event hub is an Azure resource, so your first step is to create a new hub in Azure and configure it to meet the specific requirements of your applications.

## What is an Azure event hub?

Azure Event Hubs is a cloud-based, event-processing service that's capable of receiving and processing millions of events per second. Event Hubs acts as a front door for an event pipeline, where it receives incoming data and stores it until processing resources are available.

An entity that sends data to the Event Hubs is called a *publisher* and an entity that reads data from the Event Hubs is called a *consumer* or a *subscriber*. Azure Event Hubs sits between these two entities to divide the production (from publisher) and consumption (to subscriber) of an event stream. This decoupling helps to manage scenarios where the rate of event production is much higher than the consumption. The following illustration shows the role of an event hub.

![An illustration showing an Azure Event Hub placed between four publishers and two subscribers. The Event hub receives multiple events from the publishers, serializes the events into data streams, and makes the data streams available to subscribers.](../media-draft/2-event-hub-overview.png)

### Events

An **event** is a small packet that contains a notification of a change and not the details of what exactly has changed. You can't configure a consumer application to initiate some form of query to find out the details, but this isn't a requirement and Event Hubs doesn't handle this. Events can be published individually, or in batches, but a single publication (individual or batch) can't exceed 256 KB.

On the contrary, in message queuing (in Azure Service Bus), the **message** contains data and the event, and the publisher of the message expects the consumer to process the message in a particular way.

### Publishers and subscribers

Event publishers are any application or device that can send out event data using either HTTPS or Advanced Message Queuing Protocol (AQMP) 1.0. 

For publishers that send data frequently, AMQP has the better performance. However, it has a higher initial session overhead, because a persistent bidirectional socket and transport level security (TLS) or SSL/TLS has to be set up first. 

For more intermittent publishing, HTTPS is the better option. Though HTTPS requires additional SSL overhead for every request, there isn’t the session initialization overhead.

> [!NOTE] 
> Existing Kafka-based applications, using Apache Kafka 1.0 and newer client versions, can also act as Event Hubs publishers.

Event subscribers are applications that use one of two supported programmatic methods to receive and process events from an event hub.

- **EventHubReceiver** - A simple method that provides limited management options.
- **EventProcessorHost** - An efficient method that we’ll use later in this module.

### Consumer groups

An event hub **consumer group** represents a specific view of an event hub data stream. By using separate consumer groups, multiple subscriber applications can process an event stream independently, and without affecting other applications. However, the use of multiple consumer groups is not a requirement, and for many applications, the single default consumer group is sufficient.

### Pricing

There are three pricing tiers for Azure Event Hubs: Basic, Standard, and Dedicated. The tiers differ in terms of supported connections, number of available Consumer groups, and throughput. When using Azure CLI to create an Event Hubs Namespace, if you don't specify a pricing tier, the default of **Standard** (20 Consumer groups, 1000 Brokered connections) is assigned.

## Creating and configuring a new Azure Event Hubs

There are two main steps when creating and configuring a new Azure Event Hubs. The first step is to define an Event Hubs **namespace**. The second step is to create an event hub in that namespace.

### Defining an Event Hubs namespace

An Event Hubs namespace is a containing entity for managing one or more Event Hubs. 

Creating an Event Hubs namespace typically involves the following:

1. Defining namespace-level settings. Certain settings such as namespace capacity (configured using **throughput units**), pricing tier, and performance metrics are defined at the namespace level. These are applicable for all the event hubs within that namespace. If you don't define these settings, a default value is used: *1* for capacity and *Standard* for pricing tier.

    You cannot change the throughput unit once you set it. You must balance your configuration against your Azure budget expectations. You might consider configuring different event hubs for different throughput requirements. For example, if you have a sales data application and you are planning for two Event Hubs, one for high throughput collection of real-time sales data telemetry and one for infrequent event log collection, it would make sense to use a separate namespace for each hub. This way you only need to configure (and pay for) high throughput capacity on the telemetry hub.

1. Selecting a unique name for the namespace. The namespace is accessible through this url: *_namespace_.servicebus.windows.net*

1. Defining the following optional properties:

    - Enable Kafka. This option enables Kafka applications to publish events to the event hub.
    - Make this namespace zone redundant. Zone-redundancy replicates data across separate data centers with their own independent power, networking, and cooling infrastructures.
    - Enable Auto-Inflate, and Auto-Inflate Maximum Throughput Units. Auto-Inflate provides an automatic scale-up option, by increasing the number of throughput units up to a maximum value. This is useful to avoid throttling in situations when incoming or outgoing data rates exceed the currently set number of throughput units.

### Azure CLI commands for creating an Event Hubs namespace

To create a new Event Hubs namespace, you use the following commands:

1. In Azure, a resource group is a container that holds related Azure resources for ease of management. If required, create a new resource group for your event hub.

    ```azurecli
    az group create --name <resource group name> --location <location>
    ```

1. Create the Event Hubs Namespace, using the same resource group and location as in the previous step.

    ```azurecli
    az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <resource group name> -l <location>
    ```

1. All Event Hubs within the same Event Hubs namespace share common connection credentials. You will need these credentials when you configure applications to send and receive messages using the event hub. Use the following command to return the connection string for your Event Hubs namespace, using the same resource group and Event Hubs namespace name as before.

    ```azurecli
    az eventhubs namespace authorization-rule keys list --resource-group <resource group name> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```

### Configuring a new event hub

After the Event Hubs namespace has been created, you can create an event hub. When creating a new event hub, there are several mandatory parameters.

The following parameters are required to create an event hub:

- **Event hub name** - Event hub name that is unique within your subscription and:
  - Is between 1 and 50 characters long
  - Contains only letters, numbers, periods, hyphens, and underscores
  - Starts and ends with a letter or number
- **Partition Count** -  The number of partitions required in an event hub (between 2 and 32). This should be directly related to the expected number of concurrent consumers. This cannot be changed after the hub has been created. The partition separates the message stream, so that consumer or receiver applications only need to read a specific subset of the data stream. If not defined, this defaults to *4*.
- **Message Retention** - The number of days (between 1 and 7) that messages will remain available, if the data stream needs to be replayed for any reason. If not defined, this defaults to *7*.

You can also optionally configure an event hub to stream data to an Azure Blob storage or Azure Data Lake Store account.

### Azure CLI commands for creating an event hub

To create a new event hub, you use the following commands:

1. Create the event hub, using the same resource group and location as you used when creating the namespace.

    ```azurecli
    az eventhubs eventhub create --name <event hub name> --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name>
    ```

1. View the details of your event hub in the namespace, using the same resource group and event hub name and namespace name as before.

    ```azurecli
    az eventhubs eventhub show --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name> --name <event hub name>

## Summary

To deploy Azure Event Hubs, you must configure an Event Hubs namespace and then configure the event hub itself. In the next section, you will go through the detailed configuration steps to create a new namespace and event hub.