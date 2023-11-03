# 설정: 스택 실행

## 소개

이 실습에서는 Autonomous Database를 생성하고, Graph User를 생성하고, 사용할 데이터세트를 업로드할 스택을 실행합니다.

예상 시간: 5분

실습 과정을 간단히 살펴보려면 아래 비디오를 시청하십시오. [설정](videohub:1_8z5ze0pe)

### 목표

방법 알아보기

*   구획 생성(선택사항)
*   스택을 실행하여 Autonomous Database, Graph 사용자를 생성하고 데이터세트를 업로드합니다.
*   Graph Studio에 로그인

## 작업 1: OCI 구획 생성(OPTIONAL)

> **주:** _이미 구획이 있는 경우 이 실습은 선택사항입니다._

[](include:iam-compartment-create-body.md)

## 작업 2: 스택 실행

아래 지침은 그래프 사용자를 포함하는 Autonomous Database 및 속성 그래프 쿼리에 필요한 데이터 세트를 자동으로 생성하는 스택을 실행하는 방법을 보여줍니다.

1.  Oracle Cloud에 로그인합니다.
    
2.  로그인한 후에는 이 [링크](https://cloud.oracle.com/resourcemanager/stacks/create?zipUrl=https://github.com/oracle-quickstart/oci-arch-graph/releases/latest/download/orm-graph-stack.zip)를 사용하여 스택을 만들고 실행합니다.
    

> 참고: 링크가 새 탭 또는 창에서 열립니다.

3.  이 페이지로 이동합니다.

![스택 생성 페이지](./images/create-stack.png)

4.  "Oracle 이용약관을 검토했으며 이에 동의합니다." 상자를 선택하고 해당 구획을 선택합니다. 나머지는 기본값으로 둡니다. **다음**을 누릅니다.

![선택된 Oracle 이용약관을 검토 및 수락하는 옵션](./images/oracle-terms.png)

5.  구획을 선택하여 Autonomous Database를 생성하고 나머지는 기본값으로 둡니다. **다음**을 누릅니다. 검토 페이지로 이동한 후 **생성**을 누릅니다.

![스택 생성 페이지](./images/configure-variables.png)

6.  초기 상태가 주황색으로 표시된 Job Details 페이지로 이동합니다. 작업이 성공적으로 완료되면 아이콘이 녹색으로 표시됩니다.
    
    ![작업이 성공했습니다.](./images/successful-job.png)
    
    애플리케이션에 대한 정보를 보려면 **애플리케이션 정보**를 누릅니다. Graph Studio에 로그인하는 데 사용되므로 Graph 사용자 이름과 비밀번호를 저장합니다.
    
    ![그래프 사용자 이름과 암호를 보는 방법](./images/graph-username-password.png)
    

## 작업 3: Graph Studio에 로그인

1.  애플리케이션 정보 아래에서 **Graph Studio 열기**를 누릅니다. 새 페이지가 열립니다. 애플리케이션 정보 아래에 제공된 그래프 사용자 이름과 비밀번호를 로그인 화면에 입력합니다.

![애플리케이션 정보 아래에 그래프 스튜디오 열기](./images/login-page.png " ")

2.  그런 다음 **Sign In(사인인)** 버튼을 누릅니다. Studio 홈 페이지가 표시됩니다.

![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/gs-graphuser-home-page.png " ")

Graph Studio는 왼쪽의 메뉴에서 액세스되는 일련의 페이지로 구성됩니다.

홈 아이콘 ![홈 아이콘](images/home.svg)을 누르면 홈 페이지로 이동합니다.  
모델 아이콘 ![모델 아이콘](images/code-fork.svg)은 기존 테이블 및 뷰를 그래프로 모델링한 다음 그래프를 생성하거나 인스턴스화하는 모델 페이지로 이동합니다.  
그래프 페이지 ![그래프 아이콘](images/radar-chart.svg)에는 노트북에 사용할 기존 그래프가 나열됩니다.  
메모장 페이지 ![메모장 아이콘](images/notebook.svg)에는 기존 노트북이 나열되며 새 노트북을 생성할 수 있습니다.  
작업 페이지 ![작업 아이콘](images/server.svg)에는 백그라운드 작업의 상태가 나열되며 연관된 로그(있는 경우)를 볼 수 있습니다.

이 연습을 마칩니다. **이제 다음 실습을 진행할 수 있습니다.**

## 확인

*   **작가** - Jayant Sharma, Ramu Murakami Gutierrez, 제품 관리
*   **공헌자** - Rahul Tasker, Jayant Sharma, Ramu Murakami Gutierrez, 제품 관리
*   **최종 업데이트 기한/일자** - Ramu Murakami Gutierrez, 제품 관리, 2022년 6월