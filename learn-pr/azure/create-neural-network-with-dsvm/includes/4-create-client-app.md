### <a name="exercise-4-create-a-nothotdog-app"></a>연습 4: NotHotDog 앱 만들기

이 연습에서는 Data Science VM에 미리 설치되는 Microsoft의 플랫폼 간 무료 소스 코드 편집기인 [Visual Studio Code](https://code.visualstudio.com/)를 사용하여 Python에서 NotHotDog 앱을 작성합니다. 이 앱은 Python용 인기 GUI 프레임워크인 [Tkinter](https://wiki.python.org/moin/TkInter)를 사용하여 해당 사용자 인터페이스를 구현하고 로컬 파일 시스템에서 이미지를 선택할 수 있도록 합니다. 그런 다음, 이전 연습에서 학습한 모델에 해당 이미지를 전달하고 핫도그가 포함되어 있는지 여부를 알려줍니다.

1. 바탕 화면의 왼쪽 위에 있는 **응용 프로그램**을 클릭하고 **보조 프로그램 > Visual Studio Code**를 선택하여 Visual Studio Code를 시작합니다. Visual Studio Code의 **파일 > 폴더 열기...** 명령을 사용하여 모델을 학습할 때 만든 **retrained_graph_hotdog.pb** 파일이 들어 있는 “notebooks/tensorflow-for-poets-2/tf_files” 폴더를 엽니다.

1. 현재 폴더에 **classify.py**라는 새 파일을 만듭니다. Visual Studio Code가 Python 확장을 설치하도록 제안하는 경우 **설치**를 클릭하여 설치합니다. 아래 코드를 클립보드에 복사하고 **Shift+Ins**를 사용하여 **classify.py**에 붙여넣습니다. 그런 다음, 파일을 저장합니다.

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

    여기서 핵심 사항은 ```subprocess.check_output``` 호출입니다. 이 호출은 “scripts” 폴더에 있는 **label_image.py**라는 Python 스크립트를 실행하고, 사용자가 선택한 이미지를 전달하여 학습된 모델을 불러옵니다. 이 스크립트는 이전 연습에서 복제한 리포지토리에서 가져온 것입니다.

1. 즐겨 찾는 검색 엔진을 사용하여 핫도그가 포함된 이미지와 포함되지 않은 이미지를 포함하는 몇 가지 음식 이미지를 찾습니다. 이러한 이미지를 다운로드한 후 VM 파일 시스템의 원하는 위치에 저장합니다.

1. Visual Studio Code의 **보기 > 통합 터미널** 명령을 사용하여 통합 터미널을 엽니다. 그런 다음, 통합 터미널에서 다음 명령을 실행하여 앱을 실행합니다.

     ```bash
     python classify.py
     ```

1. 앱의 **선택** 단추를 클릭하고 3단계에서 다운로드한 핫도그 이미지 중 하나를 선택합니다. 이미지에 핫도그가 포함되어 있는지 여부를 나타내는 메시지 상자가 나타날 때까지 기다립니다. 모델이 적합한가요?

    > 이미지를 처리할 때 터미널 창에서 누락된 커널 드라이버와 관련된 오류 메시지가 표시되면 무시해도 됩니다. 이 오류는 Data Science VM에 가상 GPU가 포함되어 있지 않기 때문에 표시됩니다.

    ![이미지 선택](../images/select-image.png)

    _이미지 선택_

1. 핫도그가 없는 이미지를 사용하여 이전 단계를 반복합니다. 해당 모델이 이번에는 적합한가요?

핫도그가 포함된 이미지를 만족스럽게 식별할 수 있을 때까지 앱에 음식 이미지를 계속 공급합니다. 100%는 가능하지 않습니다. ‘대부분의 경우’ 이미지를 식별할 수 있으면 충분합니다.