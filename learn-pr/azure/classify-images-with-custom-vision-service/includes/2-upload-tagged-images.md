<span data-ttu-id="64639-101">이 섹션에서는 피카소, 폴록, 렘브란트의 유명 회화 이미지를 Artists 프로젝트에 추가할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64639-101">In this unit, you'll add images of famous paintings by Picasso, Pollock, and Rembrandt to the Artworks project.</span></span> <span data-ttu-id="64639-102">Custom Vision Service가 아티스트를 구별하는 방법을 학습할 수 있도록 이미지에 태그를 지정할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64639-102">You'll tag the images so the Custom Vision Service can learn to differentiate one artist from another.</span></span>

1. <span data-ttu-id="64639-103">앞에서 만든 **Artists** 프로젝트에서, 측면 패널의 **태그** 오른쪽에서 더하기 기호(**+**)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-103">In the **Artworks** project that we created, select the plus sign (**+**) to the right of **Tags** in the side panel.</span></span>

     ![[태그 추가] 단추 선택](../media/2-add-tags.png)

1. <span data-ttu-id="64639-105">**태그 이름 지정** 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="64639-105">A dialog called **Name the tag** is displayed.</span></span> <span data-ttu-id="64639-106">태그 이름 필드에 *painting*을 입력하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-106">Type *painting* into the tag name field and select **Save**.</span></span> <span data-ttu-id="64639-107">그러면 태그 목록에 *painting*이라는 태그가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="64639-107">This operation creates the tag *painting* in the tag list.</span></span> <span data-ttu-id="64639-108">좀 더 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64639-108">Let's add some more.</span></span> 

1. <span data-ttu-id="64639-109">2단계를 반복하여 *피카소*, *폴록*, *렘브란트* 값으로 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-109">Repeat step 2 to add tags with the values *Picasso*, *Pollock*, and *Rembrandt*.</span></span> <span data-ttu-id="64639-110">모두 마치면 태그 목록이 다음과 비슷할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64639-110">The tag list will look like the following when you are finished.</span></span>

    ![[태그 추가] 단추 선택](../media/2-tag-list.png)

    <span data-ttu-id="64639-112">보시다시피, 프로젝트에서 이러한 태그가 지정된 이미지 수는 0입니다.</span><span class="sxs-lookup"><span data-stu-id="64639-112">As you can see, the number of images in our project that are tagged with each of these tags is zero.</span></span> <span data-ttu-id="64639-113">프로젝트에 이미지를 추가하고 태그를 할당해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="64639-113">Let's add some images to our project and assign tags.</span></span>

1. <span data-ttu-id="64639-114">이 모듈에 대한 이미지 리소스를 포함하는 [cvs-resources.zip](https://github.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/raw/master/cvs-resources.zip)을 다운로드하여 로컬 머신에 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="64639-114">Download [cvs-resources.zip](https://github.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/raw/master/cvs-resources.zip) which contains image resources for this module and unzip it to your local machine.</span></span> 

1. <span data-ttu-id="64639-115">포털로 돌아가서 **이미지 추가**를 선택하여 이미지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-115">Back in the portal, select **Add images** to add images to the project.</span></span>

    ![Artists 프로젝트에 이미지 추가](../media/2-portal-click-add-images.png)

1. <span data-ttu-id="64639-117">4단계에서 로컬로 다운로드한 **cvs-resources** 폴더에서 "Artists\Picasso" 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-117">In the **cvs-resources** folder that you downloaded locally in step 4, navigate to the "Artists\Picasso" folder.</span></span>

1. <span data-ttu-id="64639-118">"Artists\Picasso"에서 모든 파일을 선택한 다음, **열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-118">Select all of the files in "Artists\Picasso", and then select **Open**.</span></span>

    ![이미지 선택](../media/2-fe-browse-picasso-01.png)

1. <span data-ttu-id="64639-120">업로드 중인 모든 이미지의 미리 보기를 표시하는 **이미지 업로드** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="64639-120">The **Image upload** dialog appears and displays thumbnails of all the images we are uploading.</span></span> <span data-ttu-id="64639-121">**내 태그** 필드를 선택합니다. 그러면 이러한 이미지를 할당할 수 있는 태그 드롭다운이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="64639-121">Select the **My Tags** field, which opens a dropdown of the tags you can assign these images.</span></span> 

    ![이미지에 "painting" 태그 추가](../media/2-upload-picasso-tags.png)

1. <span data-ttu-id="64639-123">*painting* 및 *Picasso* 태그를 선택한 다음, **7개 파일 업로드**를 선택하여 업로드를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-123">Select the tags *painting* and *Picasso* and then select **Upload 7 files** to finish the upload.</span></span> 

1. <span data-ttu-id="64639-124">업로드한 이미지가 Artworks 프로젝트에 있는지, 태그 목록이 업데이트되어 7개 이미지에 *Picasso* 및 *painting* 태그가 지정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-124">Confirm that the images you uploaded are now in the Artworks project, and that the tag list has been updated to show that we've tagged seven images with *Picasso* and *painting*.</span></span>

    ![업로드된 이미지](../media/2-portal-tagged-01.png)

1. <span data-ttu-id="64639-126">Custom Vision Service는 7개의 Picasso 이미지를 사용하여 Picasso 그림을 제대로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="64639-126">With seven Picasso images, the Custom Vision Service can do a decent job of identifying paintings by Picasso.</span></span> <span data-ttu-id="64639-127">하지만 지금 모델을 학습한 경우에는 Picasso 그림이 어떻게 보이는지만 이해하고 다른 아티스트의 그림은 식별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="64639-127">But if you trained the model right now, it would only understand what a Picasso looks like, and it wouldn't be able to identify paintings by other artists.</span></span> <span data-ttu-id="64639-128">다음 단계에서는 다른 아티스트의 일부 그림을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-128">The next step is to upload some paintings by another artist.</span></span> 

1. <span data-ttu-id="64639-129">**이미지 추가**를 선택하고, 랩 리소스의 "Artists\Rembrandt" 폴더에 있는 이미지를 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-129">Select **Add images** and select all of the images in the "Artists\Rembrandt" folder in the module resources.</span></span> <span data-ttu-id="64639-130">"painting" 및 "Rembrandt"("Picasso"가 아님) 레이블을 사용하여 태그를 지정하고, **6개 파일 업로드**를 선택하여 프로젝트에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-130">Tag them with the labels "painting" and "Rembrandt" (not "Picasso"), and select **Upload 6 files** to upload them to the project.</span></span>

    ![업로드된 이미지](../media/2-upload-rembrandt.png)

1. <span data-ttu-id="64639-132">프로젝트에서 Rembrandt 이미지가 Picasso 이미지와 함께 표시되는지, "Rembrandt"가 태그 목록에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-132">Confirm that the Rembrandt images appear alongside the Picasso images in the project, and that "Rembrandt" appears in the list of tags.</span></span>

    ![Picasso 및 Rembrandt 이미지](../media/2-portal-tagged-02.png)

1. <span data-ttu-id="64639-134">이제 수수께끼 같은 아티스트 Jackson Pollock의 그림을 추가하여 Custom Vision Service가 Pollock의 그림도 인식할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-134">Now add paintings by the enigmatic artist Jackson Pollock to enable the Custom Vision Service to recognize Pollock paintings, too.</span></span> <span data-ttu-id="64639-135">랩 리소스의 "Artists\Pollock" 폴더에 있는 이미지를 모두 선택하고 "painting" 및 "Pollock" 용어로 태그를 지정하고, 프로젝트에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="64639-135">Select all of the images in the "Artists\Pollock" folder in the module resources, tag them with the terms "painting" and "Pollock", and upload them to the project.</span></span>

<span data-ttu-id="64639-136">태그 지정된 이미지가 업로드되면 다음 단계는 Picasso, Rembrandt 및 Pollock의 그림을 서로 구별하고 그림이 이러한 유명한 아티스트 중 하나의 작품인지 확인할 수 있도록 해당 이미지가 포함된 모델을 학습하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="64639-136">With the tagged images uploaded, the next step is to train the model with these images so it can distinguish between paintings by Picasso, Rembrandt, and Pollock, as well as determine whether a painting is a work by one of these famous artists.</span></span>