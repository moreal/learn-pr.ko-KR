### <a name="exercise-4-create-a-nothotdog-app"></a><span data-ttu-id="637c1-101">연습 4: NotHotDog 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="637c1-101">Exercise 4: Create a NotHotDog app</span></span>

<span data-ttu-id="637c1-102">이 연습에서는 Data Science VM에 미리 설치되는 Microsoft의 플랫폼 간 무료 소스 코드 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용하여 Python에서 NotHotDog 앱을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-102">In this exercise, you will use [Visual Studio Code](https://code.visualstudio.com/), Microsoft's free, cross-platform source-code editor which is preinstalled in the Data Science VM, to write a NotHotDog app in Python.</span></span> <span data-ttu-id="637c1-103">이 앱은 Python용 인기 GUI 프레임워크인 [Tkinter](https://wiki.python.org/moin/TkInter)를 사용하여 해당 사용자 인터페이스를 구현하고 로컬 파일 시스템에서 이미지를 선택할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-103">The app will use [Tkinter](https://wiki.python.org/moin/TkInter), which is a popular GUI framework for Python, to implement its user interface, and it will allow you to select images from your local file system.</span></span> <span data-ttu-id="637c1-104">그런 다음, 이전 연습에서 학습한 모델에 해당 이미지를 전달하고 핫도그가 포함되어 있는지 여부를 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-104">Then it will pass those images to the model you trained in the previous exercise and tell you whether they contain a hot dog.</span></span>

1. <span data-ttu-id="637c1-105">바탕 화면의 왼쪽 위에 있는 **응용 프로그램**을 클릭하고 **보조 프로그램 > Visual Studio Code**를 선택하여 Visual Studio Code를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-105">Click **Applications** in the upper-left corner of the desktop and select **Accessories > Visual Studio Code** to start Visual Studio Code.</span></span> <span data-ttu-id="637c1-106">Visual Studio Code의 **파일 > 폴더 열기...** 명령을 사용하여 모델을 학습할 때 만든 **retrained_graph_hotdog.pb** 파일이 들어 있는 “notebooks/tensorflow-for-poets-2/tf_files” 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-106">Use Visual Studio Code's **File > Open Folder...** command to open the "notebooks/tensorflow-for-poets-2/tf_files" folder containing the **retrained_graph_hotdog.pb** file created when you trained the model.</span></span>

1. <span data-ttu-id="637c1-107">현재 폴더에 **classify.py**라는 새 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-107">Create a new file named **classify.py** in the current folder.</span></span> <span data-ttu-id="637c1-108">Visual Studio Code가 Python 확장을 설치하도록 제안하는 경우 **설치**를 클릭하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-108">If Visual Studio Code offers to install the Python extension, click **Install** to install it.</span></span> <span data-ttu-id="637c1-109">아래 코드를 클립보드에 복사하고 **Shift+Ins**를 사용하여 **classify.py**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-109">Copy the code below to the clipboard and use **Shift+Ins** to paste it into **classify.py**.</span></span> <span data-ttu-id="637c1-110">그런 다음, 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-110">Then save the file:</span></span>

    ```python
    import tkinter as tk
    from tkinter import messagebox, filedialog, font
    from PIL import ImageTk, Image
    import subprocess

    def select_image_click(img_label):
        try:
            file = filedialog.askopenfilename()

            img = Image.open(file)
            img = img.resize((300, 300))
            selected_img = ImageTk.PhotoImage(img)

            img_label.configure(image=selected_img, width=240)

            output = subprocess.check_output(["python",
                "../scripts/label_image.py",
                "--graph=retrained_graph_hotdog.pb",
                "--image={0}".format(file),
                "--labels=retrained_labels_hotdog.txt"])

            highest = str(output).split("\\n")[3].split(" ")

            if len(highest) == 3:
                score = float(highest[2])
                is_hotdog = True
            else:
                score = float(highest[3])
                is_hotdog = False

            if score > 0.95:
                if is_hotdog:
                    messagebox.showinfo("Result", "That's a hot dog!")
                else:
                    messagebox.showinfo("Result", "That's not a hot dog.")
            else:
                messagebox.showinfo("Result", "Can't tell.")

        except FileNotFoundError as e:
            messagebox.showerror("File not found", "File {0} was not found.".format(e.filename))

    def run():
        window = tk.Tk()

        window.title("Hotdog or Not Hotdog")
        window.geometry('400x600')

        text_font = font.Font(size=18, family="Helvetica Neue")
        welcome_text = tk.Label(window, text="Hot Dog or Not Hot Dog", font=text_font)
        welcome_text.pack()

        instructions_text = tk.Label(window, text="\n\nUse a neural network built with Tensorflow\n"
            "to identify photos containing hot dogs")
        instructions_text.pack(fill=tk.X)

        select_btn = tk.Button(window, text="Select", bg="#0063B1", fg="white", width=5, height=1)
        select_btn.pack(pady=30)

        image_label = tk.Label(window)
        image_label.pack()

        select_btn.configure(command=lambda: select_image_click(image_label))
        window.mainloop()

    if __name__ == "__main__":
        run()
    ```

    <span data-ttu-id="637c1-111">여기서 핵심 사항은 ```subprocess.check_output``` 호출입니다. 이 호출은 “scripts” 폴더에 있는 **label_image.py**라는 Python 스크립트를 실행하고, 사용자가 선택한 이미지를 전달하여 학습된 모델을 불러옵니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-111">They key code here is the call to ```subprocess.check_output```, which invokes the trained model by executing a Python script named **label_image.py** found in the "scripts" folder, passing in the image that the user selected.</span></span> <span data-ttu-id="637c1-112">이 스크립트는 이전 연습에서 복제한 리포지토리에서 가져온 것입니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-112">This script came from the repo that you cloned in the previous exercise.</span></span>

1. <span data-ttu-id="637c1-113">즐겨 찾는 검색 엔진을 사용하여 핫도그가 포함된 이미지와 포함되지 않은 이미지를 포함하는 몇 가지 음식 이미지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-113">Use your favorite search engine to find a few food images — some containing hot dogs, and some not.</span></span> <span data-ttu-id="637c1-114">이러한 이미지를 다운로드한 후 VM 파일 시스템의 원하는 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-114">Download these images and store them in the location of your choice in the VM's file system.</span></span>

1. <span data-ttu-id="637c1-115">Visual Studio Code의 **보기 > 통합 터미널** 명령을 사용하여 통합 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-115">Use Visual Studio Code's **View > Integrated Terminal** command to open an integrated terminal.</span></span> <span data-ttu-id="637c1-116">그런 다음, 통합 터미널에서 다음 명령을 실행하여 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-116">Then execute the following command in the integrated terminal to run the app:</span></span>

     ```bash
     python classify.py
     ```

1. <span data-ttu-id="637c1-117">앱의 **선택** 단추를 클릭하고 3단계에서 다운로드한 핫도그 이미지 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-117">Click the app's **Select** button and pick one of the hot-dog images you downloaded in Step 3.</span></span> <span data-ttu-id="637c1-118">이미지에 핫도그가 포함되어 있는지 여부를 나타내는 메시지 상자가 나타날 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-118">Wait for a message box to appear, indicating whether the image contains a hot dog.</span></span> <span data-ttu-id="637c1-119">모델이 적합한가요?</span><span class="sxs-lookup"><span data-stu-id="637c1-119">Did the model get it correct?</span></span>

    > <span data-ttu-id="637c1-120">이미지를 처리할 때 터미널 창에서 누락된 커널 드라이버와 관련된 오류 메시지가 표시되면 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-120">If you see error messages regarding a missing kernel driver in the terminal window when you process an image, you can safely ignore them.</span></span> <span data-ttu-id="637c1-121">이 오류는 Data Science VM에 가상 GPU가 포함되어 있지 않기 때문에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-121">They result from the fact that the Data Science VM does not contain a virtual GPU.</span></span>

    ![이미지 선택](../images/select-image.png)

    <span data-ttu-id="637c1-123">_이미지 선택_</span><span class="sxs-lookup"><span data-stu-id="637c1-123">_Selecting an image_</span></span>

1. <span data-ttu-id="637c1-124">핫도그가 없는 이미지를 사용하여 이전 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-124">Repeat the previous step using an image that doesn't contain a hot dog.</span></span> <span data-ttu-id="637c1-125">해당 모델이 이번에는 적합한가요?</span><span class="sxs-lookup"><span data-stu-id="637c1-125">Was the model right this time?</span></span>

<span data-ttu-id="637c1-126">핫도그가 포함된 이미지를 만족스럽게 식별할 수 있을 때까지 앱에 음식 이미지를 계속 공급합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-126">Continue feeding food images into the app until you're satisfied that it can identify images containing hot dogs.</span></span> <span data-ttu-id="637c1-127">100%는 가능하지 않습니다. ‘대부분의 경우’ 이미지를 식별할 수 있으면 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="637c1-127">Don't expect it to be right 100% of the time, but do expect it to be right *most* of the time.</span></span>