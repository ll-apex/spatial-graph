# JupyterLab 시작

## 소개

노트북은 코드, 설명 텍스트 및 시각화를 위한 대화형 문서입니다. 이 워크샵에서는 파일 업로드와 같이 사용자에게 친숙한 여러 기능을 웹 기반 노트북 환경에 제공하는 오픈 소스 JupyterLab를 사용합니다.

예상 실험 시간: 5분

실습 과정을 간단히 살펴보려면 아래 비디오를 시청하십시오. [랩 3](videohub:1_p5fff23s)

### 목표

*   JupyterLab 시작
*   JupyterLab에 대한 액세스 확인
*   나머지 실습 랩을 수행하기 위한 옵션 선택

### 필요 조건

*   실습 2 완료: Autonomous Database 생성

## 작업 1: JupyterLab 시작

1.  Cloud Shell을 확장합니다. ![Cloud Shell 확장](images/start-jupyter-01.png)
    
2.  여전히 SSH를 사용하여 컴퓨팅 인스턴스에 연결해야 합니다. 그렇지 않은 경우 다음 명령을 입력하여 컴퓨트 인스턴스에 접속합니다.
    

\`\`\`\`\`\`\`\` ssh -i ~/.ssh/my-ssh-key opc@\[IP address\] \`\`\`\`\` \`\`\` ssh -i ~/.ssh/ocw23-rsa opc@\[IP address\] \`\`\`

    ![Expand Cloud Shell](images/start-jupyter-02.png) 
    

3.  컴퓨트 인스턴스에 Python 라이브러리가 로드된 가상 환경이 있습니다. 다음 명령을 사용하여 가상 환경을 활성화합니다.
    
        <copy>
         source my-virtual-env/bin/activate
        </copy>
        
    
    ![Cloud Shell 확장](images/start-jupyter-03.png)
    
4.  다음 명령을 입력하여 JupyterLab를 시작합니다.
    
        <copy>
         jupyter-lab --ip=0.0.0.0 --port=8001 --no-browser
        </copy>
        
    
    ![JupyterLab 시작](images/start-jupyter-04.png)
    
    시작 프로세스는 "To access the server ..." 다음에 파일 경로와 URL이 표시되면 완료됩니다.
    

## 작업 2: JupyterLab에 대한 액세스 확인

1.  인증 토큰을 포함하는 JupyterLab URL을 확인합니다. 이 URL을 복사하여 텍스트 편집기에 붙여 넣습니다. ![JupyterLab 시작](images/start-jupyter-05.png)
    
2.  Cloud Shell에서 SSH 명령까지 스크롤하여 컴퓨트 IP 주소를 복사합니다. 그런 다음 텍스트 편집기의 URL에 붙여 넣고 127.0.0.1를 바꿉니다. ![JupyterLab 시작](images/start-jupyter-06.png)
    
3.  새 브라우저 탭을 엽니다. 그런 다음 텍스트 편집기에서 URL을 복사하여 새 탭에 붙여넣고 실행합니다. 다음 실습에서 Python 노트북을 만들고 실행할 JupyterLab가 열립니다. ![JupyterLab 시작](images/start-jupyter-07.png)
    

## 작업 3: Jupyter 노트북 탐색

Jupyter Notebook은 실시간 코드, 방정식, 시각화 및 텍스트가 포함된 문서를 생성하고 공유할 수 있는 대화형 웹 기반 도구입니다. 데이터 과학 커뮤니티에서 프로토타이핑 및 데이터 분석을 위해 널리 사용됩니다.

이 작업에서는 Jupyter Notebook 사용의 기본 사항을 살펴봅니다.

1.  새 노트북을 생성합니다.
    
    Jupyter 환경이 로드되면 실행 프로그램 탭이 열려 있어야 합니다.
    
    ![실행기 탭이 열려 있습니다.](./images/launcher1.png)
    
    실행 프로그램 창이 표시되지 않으면 창 왼쪽 상단에 있는 파일을 선택하고 '새 실행 프로그램'을 선택합니다.
    
    ![새 실행기 탭 열기](./images/launcher2.png)
    
    실행 프로그램 창에서 "Python 3"을 선택하여 Python 프로그래밍 언어를 사용하여 새 노트북을 만듭니다. 새 노트북이 만들어지고 코드 셀에 코드를 입력하거나 마크다운 셀에 마크다운 텍스트를 추가하여 작업을 시작할 수 있습니다.
    
    ![새 Python 노트북 만들기](./images/launcher3.png)
    
2.  몇 가지 마크다운 텍스트를 추가합니다.
    
    코드 셀을 누르고 셀 유형 드롭다운을 사용하여 '마크다운'을 선택하십시오.
    
    ![마크다운 셀 추가](./images/notebook1.png)
    
    셀에 다음을 붙여넣고 도구 모음에서 재생 버튼을 누르거나 Shift+Enter 키를 눌러 셀을 실행합니다.
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![매가인하 결과](./images/notebook2.png)
    
3.  Python 코드를 작성합니다. 다음을 다음 셀에 붙여넣고 실행합니다. 'Hello, World!'라는 문구가 셀 아래에 나타나야 합니다.
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![안녕하세요.](./images/notebook3.png)
    
4.  Jupyter Notebook을 저장하려면 도구 모음에서 "저장" 아이콘을 클릭하거나 Ctrl+S(또는 macOS의 경우 Cmd+S)을 누릅니다. 노트북은 .ipynb 파일 확장자로 저장됩니다.
    

## 작업 4: 이 실습의 나머지 부분을 수행하기 위한 옵션 선택

이 실습의 나머지 부분에서는 다음 옵션 중 하나를 사용하여 수행할 수 있습니다.

**옵션 1:** 지침에 따라 각 단계를 노트북에 복사/붙여넣기/실행합니다.

1.  Lab 4 및 후속 Lab으로 이동합니다.

**옵션 2:** 모든 단계로 사전 구축된 노트북을 로드하고 각 셀을 실행합니다.

1.  **Lab 4 - 작업 1** 수행
    
2.  **Lab 5 - Task 1**을 수행합니다.
    
3.  다음 링크를 눌러 노트북에 미리 빌드된 노트북을 다운로드합니다. \* [prebuit-notebook.ipynb](./files/prebuilt-notebook.ipynb)
    
4.  업로드 단추를 클릭하고 사전 제작 노트북을 선택합니다.
    

     ![Use prebuilt notebook](./images/prebuilt-nb-01.png)
    

5.  기본 노트북을 두 번 클릭하여 열고 각 셀을 실행합니다.

     ![Use prebuilt notebook](./images/prebuilt-nb-02.png)
    

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **제공자** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 8월