### <a name="exercise-2-upload-tagged-images"></a><span data-ttu-id="c4011-101">연습 2: 태그 지정된 이미지 업로드</span><span class="sxs-lookup"><span data-stu-id="c4011-101">Exercise 2: Upload tagged images</span></span>

<span data-ttu-id="c4011-102">이 연습에서는 Picasso, Pollock 및 Rembrandt의 유명한 그림 이미지를 Artworks 프로젝트에 추가하고 이미지 태그를 지정하여 Custom Vision Service가 학습하고 아티스트를 서로 구별할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-102">In this exercise, you will add images of famous paintings by Picasso, Pollock, and Rembrandt to the Artworks project, and tag the images so the Custom Vision Service can learn to differentiate one artist from another.</span></span>
  
1. <span data-ttu-id="c4011-103">**이미지 추가**를 클릭하여 프로젝트에 이미지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-103">Click **Add images** to add images to the project.</span></span>

    ![Artworks 프로젝트에 이미지 추가](../images/portal-click-add-images.png)

    <span data-ttu-id="c4011-105">_Artworks 프로젝트에 이미지 추가_</span><span class="sxs-lookup"><span data-stu-id="c4011-105">_Adding images to the Artworks project_</span></span> 
 
1. <span data-ttu-id="c4011-106">**로컬 파일 찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-106">Click **Browse local files**.</span></span>

    ![로컬 이미지 찾아보기](../images/portal-click-browse-local-files.png)

    <span data-ttu-id="c4011-108">_로컬 이미지 찾아보기_</span><span class="sxs-lookup"><span data-stu-id="c4011-108">_Browsing for local images_</span></span> 
 
1. <span data-ttu-id="c4011-109">[이 랩과 함께 제공되는 리소스](https://a4r.blob.core.windows.net/public/cvs-resources.zip)에서 “Artists\Picasso” 폴더를 찾아 해당 폴더의 모든 파일을 선택하고 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-109">Browse to the "Artists\Picasso" folder in the [resources that accompany this lab](https://a4r.blob.core.windows.net/public/cvs-resources.zip), select all of the files in the folder, and click **Open**.</span></span>

    ![이미지 선택](../images/fe-browse-picasso-01.png)

    <span data-ttu-id="c4011-111">_이미지 선택_</span><span class="sxs-lookup"><span data-stu-id="c4011-111">_Selecting an image_</span></span> 
 
1. <span data-ttu-id="c4011-112">**일부 태그 추가...** 상자에 “painting”(따옴표 제외)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-112">Type "painting" (without quotation marks) into the **Add some tags...** box.</span></span> <span data-ttu-id="c4011-113">그런 다음, **+** 를 클릭하여 이미지에 태그를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-113">Then click **+** to assign the tag to the images.</span></span>

    ![이미지에 “painting” 태그 추가](../images/portal-add-tags-01.png)

    <span data-ttu-id="c4011-115">_이미지에 “painting” 태그 추가_</span><span class="sxs-lookup"><span data-stu-id="c4011-115">_Adding a "painting" tag to the images_</span></span> 

1. <span data-ttu-id="c4011-116">4단계를 반복하여 이미지에 “Picasso” 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-116">Repeat Step 4 to add a "Picasso" tag to the images.</span></span>

1. <span data-ttu-id="c4011-117">**7개 파일 업로드**를 클릭하여 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-117">Click **Upload 7 files** to upload the images.</span></span> <span data-ttu-id="c4011-118">업로드가 완료되면 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-118">Once the upload has completed, click **Done**.</span></span>

    ![태그 지정된 이미지 업로드](../images/upload-picasso-images.png)

    <span data-ttu-id="c4011-120">_태그 지정된 이미지 업로드_</span><span class="sxs-lookup"><span data-stu-id="c4011-120">_Uploading tagged images_</span></span> 

1. <span data-ttu-id="c4011-121">업로드한 이미지가 할당된 태그와 함께 포털에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-121">Confirm that the images you uploaded appear in the portal, along with the tags assigned to them.</span></span>

    ![업로드된 이미지](../images/portal-tagged-01.png)

    <span data-ttu-id="c4011-123">_업로드된 이미지_</span><span class="sxs-lookup"><span data-stu-id="c4011-123">_The uploaded images_</span></span> 

1. <span data-ttu-id="c4011-124">Custom Vision Service는 7개의 Picasso 이미지를 사용하여 Picasso 그림을 제대로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-124">With seven Picasso images, the Custom Vision Service can do a decent job of identifying paintings by Picasso.</span></span> <span data-ttu-id="c4011-125">하지만 지금 모델을 학습한 경우에는 Picasso 그림이 어떻게 보이는지만 이해하고 다른 아티스트의 그림은 식별할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-125">But if you trained the model right now, it would only understand what a Picasso looks like, and it would not be able to identify paintings by other artists.</span></span>

    <span data-ttu-id="c4011-126">다음 단계는 다른 아티스트의 그림을 일부 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-126">The next step is to upload some paintings by another artist.</span></span> <span data-ttu-id="c4011-127">**이미지 추가**를 클릭하고 랩 리소스의 “Artists\Rembrandt” 폴더에 있는 이미지를 모두 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-127">Click **Add images** and select all of the images in the "Artists\Rembrandt" folder in the lab resources.</span></span> <span data-ttu-id="c4011-128">레이블이 “painting” 및 “Rembrandt”(“Picasso”가 아님) 레이블로 태그를 지정하고 프로젝트에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-128">Tag them with the labels "painting" and "Rembrandt" (not "Picasso"), and upload them to the project.</span></span>

    > <span data-ttu-id="c4011-129">“painting” 태그를 추가하는 경우 다시 입력할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-129">When you add the tag "painting," you don't have to type it in again.</span></span> <span data-ttu-id="c4011-130">아래 표시된 것처럼 **일부 태그 추가...** 상자에 연결된 드롭다운 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-130">You can select it from the drop-down list attached to the **Add some tags...** box, as shown below.</span></span> <span data-ttu-id="c4011-131">“Rembrandt”를 입력하고 **+** 를 클릭하여 “Rembrandt” 태그를 추가해야 **합니다**.</span><span class="sxs-lookup"><span data-stu-id="c4011-131">You **will** have to type "Rembrandt" and click **+** to add a "Rembrandt" tag.</span></span>

    ![기존 태그 선택](../images/select-painting-tag.png)

    <span data-ttu-id="c4011-133">_기존 태그 선택_</span><span class="sxs-lookup"><span data-stu-id="c4011-133">_Selecting an existing tag_</span></span> 

1. <span data-ttu-id="c4011-134">프로젝트에서 Rembrandt 이미지가 Picasso 이미지와 함께 표시되는지 그리고 “Rembrandt”가 태그 목록에 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-134">Confirm that the Rembrandt images appear alongside the Picasso images in the project, and that "Rembrandt" appears in the list of tags.</span></span>

    ![Picasso 및 Rembrandt 이미지](../images/portal-tagged-02.png)

    <span data-ttu-id="c4011-136">_Picasso 및 Rembrandt 이미지_</span><span class="sxs-lookup"><span data-stu-id="c4011-136">_Picasso and Rembrandt images_</span></span> 

1. <span data-ttu-id="c4011-137">이제 수수께끼 같은 아티스트 Jackson Pollock의 그림을 추가하여 Custom Vision Service가 Pollock의 그림도 인식할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-137">Now add paintings by the enigmatic artist Jackson Pollock to enable the Custom Vision Service to recognize Pollock paintings, too.</span></span> <span data-ttu-id="c4011-138">랩 리소스의 “Artists\Pollock” 폴더에 있는 이미지를 모두 선택하고 “painting” 및 “Pollock” 용어로 태그를 지정한 후 프로젝트에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-138">Select all of the images in the "Artists\Pollock" folder in the lab resources, tag them with the terms "painting" and "Pollock", and upload them to the project.</span></span>

<span data-ttu-id="c4011-139">태그 지정된 이미지가 업로드되면 다음 단계는 Picasso, Rembrandt 및 Pollock의 그림을 서로 구별하고 그림이 이러한 유명한 아티스트 중 하나의 작품인지 확인할 수 있도록 해당 이미지가 포함된 모델을 학습하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4011-139">With the tagged images uploaded, the next step is to train the model with these images so it can distinguish between paintings by Picasso, Rembrandt, and Pollock, as well as determine whether a painting is a work by one of these famous artists.</span></span>