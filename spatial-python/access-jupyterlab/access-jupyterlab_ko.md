# 액세스 JupyterLab

## 소개

노트북은 코드, 설명 텍스트 및 시각화를 위한 대화형 문서입니다. 이 워크샵에서는 파일 업로드와 같이 사용자에게 친숙한 여러 기능을 웹 기반 노트북 환경에 제공하는 오픈 소스 JupyterLab를 사용합니다.

예상 실험 시간: 5분

### 목표

*   JupyterLab에 대한 액세스 확인
*   노트북 기능 탐색
*   나머지 실습 랩을 수행하기 위한 옵션 선택

## 작업 1: JupyterLab에 대한 IP 주소 검색

1.  기본 메뉴에서 Compute > Instances로 이동합니다.

![IP 주소 검색](images/compute-01.png)

2.  워크샵 지침 페이지에서 왼쪽 위에 있는 **로그인 정보 보기**를 누르고 구획 이름을 복사합니다.

![IP 주소 검색](images/compartment.png)

1.  OCI 콘솔에서 구획 이름을 붙여넣고 풀다운에서 선택합니다.

![IP 주소 검색](images/compute-02.png)

4.  컴퓨트 인스턴스의 공용 IP를 확인합니다. JupyerLab가 이 인스턴스에 설정되었습니다. 나중에 이 실습과 다른 실습에서 사용할 수 있습니다.

![IP 주소 검색](images/compute-03.png)

## 작업 2: JupyterLab에 대한 액세스 확인

1.  새 브라우저 탭을 열고 URL **http://\[IP address\]:8001/lab**을 입력합니다. 여기서 \[IP address\]는 작업 1에서 검색된 주소입니다.
    
    ![액세스 JupyterLab](images/access-jupyter-01.png)
    
2.  비밀번호 **livelabs**를 입력하고 **로그인**을 누릅니다.
    

## 작업 2: Jupyter 노트북 탐색

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
    

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **제공자** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 8월