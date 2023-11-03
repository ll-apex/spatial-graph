# 그래프 시각화

## 소개

이전 실습에서 수행된 분석 결과는 그래프 시각화 기능을 사용하여 쉽게 시각화할 수 있습니다.

예상 시간: 5분

다음 비디오에서는 그래프 시각화 구성요소(= GraphViz)의 개요를 제공합니다.

[유튜브](youtube:zfefKdNfAY4)

### 목표

*   PGQL 그래프 쿼리를 실행하고 결과를 시각화하는 방법을 알아봅니다.

### 필요 조건

*   그래프 생성 및 게시
*   Graph Server(GraphViz 사용)가 작동되어 실행 중입니다.

## 작업 1: GraphViz에 로그인합니다.

웹 브라우저를 사용하여 **`https://<public_ip_for_compute>:7007/ui`**에서 GraphViz를 엽니다. **`<public_ip_for_compute>`**을 Graph Server 컴퓨트 인스턴스에 대한 항목으로 바꿉니다.

마켓플레이스 이미지는 자체 서명된 SSL 인증서로 배포되므로 프로덕션에서 사용할 인증서에 맞게 변경해야 합니다. 한편, 웹 브라우저는 경고를 표시해야하지만 우리는 그것이 안전하다는 것을 이해합니다.

**Chrome**을 사용하는 경우 경고 창에 **thisisunsafe**를 입력하여 GraphViz 화면으로 이동합니다.

![로그인 크롬](images/login-chrome.jpg)

**Firefox**를 사용하여 **고급**, **위험 확보 및 계속** 순으로 누릅니다.

![로그인-firefox](images/login-firefox.jpg)

아래 스크린샷과 비슷한 화면이 나타나야 합니다. 사용자 이름(**customer\_360**)과 암호를 입력한 다음 Submit(제출)을 누릅니다. **그래프 서버**는 고급 옵션의 기본값이므로 변경할 필요가 없습니다.

![로그인](images/login.jpg)

## 작업 2: 질의 수정

처음 5개 행을 가져오도록 질의를 수정합니다. 즉, **LIMIT 100**을 **LIMIT 5**로 변경하고 Run을 누릅니다.

아래 스크린샷과 비슷한 그래프가 표시되어야 합니다.

![쇼-5 요소](images/show-5-elements.jpg)

## 작업 3: 강조 표시 추가

이제 몇 가지 레이블 및 기타 시각적 컨텍스트를 추가합니다. 이를 하이라이트라고 합니다. [여기](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip)를 눌러 zip 파일 highlights.json.zip을 다운로드합니다. 이 파일의 압축을 풀고 압축이 풀린 위치를 기록해 둡니다.

화면 오른쪽에 있는 **Settings** 아래의 Load 버튼을 누릅니다. 해당 폴더를 찾아서 파일을 선택하고 열기를 클릭하여 로드합니다.

![하이라이트-1](images/highlights-1.png)

그래프는 다음과 같아야 합니다.

![하이라이트-2](images/highlights-2.png)

## 작업 4: PGQL과 패턴 일치

1.  다음으로 몇 가지 PGQL 쿼리를 실행해 보겠습니다.
    
    [pgql-lang.org](http://pgql-lang.org) 사이트 및 [사양](http://pgql-lang.org/spec/1.4)은 세부 정보 및 예제에 대한 최상의 참조입니다. 그러나 이 연습의 목적상 최소한의 기본 사항은 다음과 같습니다.
    
    PGQL 질의의 일반적인 구조는 다음과 같습니다.
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    PGQL은 그래프 패턴 일치를 위해 **MATCH** 절로 알려진 특정 구성을 제공합니다. 그래프 패턴은 지정된 조건 및 제약 조건을 충족하는 정점과 가장자리를 일치시킵니다.
    
    *   **(v)**는 정점 변수 **v를 나타냅니다.**
    *   **\-**는 (source)-(dest)에서와 같이 방향이 지정되지 않은 가장자리를 나타냅니다.
    *   **\->** 소스 간 송신 에지
    *   **<-** 대상에서 소스로의 수신 에지
    *   **\[e\]**는 에지 변수 **e를 나타냅니다.**
    
    또한 **graph\_name**는 GraphViz UI에서 선택되므로 여기서 생략하십시오.
    
2.  같은 날 아웃바운드 및 인바운드 이전이 500개가 넘는 계정을 찾겠습니다.
    
    이에 대한 PGQL 질의는 다음과 같습니다.
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    위의 첫번째 **MATCH** 절에서 **(a)**는 소스 정점을 나타내고 **(a1)**는 대상을 나타내며 **\[t1:transfer\]**는 대상을 연결하는 모서리입니다. **:transfer**는 **t1** 가장자리에 **TRANSFER** 레이블이 포함되도록 지정합니다. 두 패턴 사이의 쉼표(,)는 AND 조건입니다.
    
3.  GraphViz 애플리케이션의 PGQL Graph Query 텍스트 입력 상자에 질의를 복사하여 붙여넣습니다. Run을 누릅니다.
    
    결과는 아래와 같아야 합니다. 강조 표시 설정에서는 **xxx-yyy-**로 시작하는 계정이 빨간색(= 은행 계정)으로 표시되고 **xxx-zzz-**는 주황색(= 다른 은행의 계정)으로 표시됩니다.
    
    ![동일 일자-이전](images/same-day-transfers.jpg)
    
4.  다음 질의는 동일한 두 계정(예: a1->a2 및 뒤로 a2->a1)으로의 이전 패턴을 찾습니다.
    
    이에 대한 PGQL 질의는 다음과 같습니다.
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  GraphViz 애플리케이션의 PGQL Graph Query 텍스트 입력 상자에 질의를 복사하여 붙여넣습니다. Run을 누릅니다.
    
    결과는 아래와 같아야 합니다.
    
    ![사이클-2-홉](images/cycle-2-hops.jpg)
    
6.  3개의 계정 간에 순환 이전 패턴을 찾기 위해 해당 질의에 계정을 하나 더 추가합니다.
    
    PGQL 질의는 다음과 같이 됩니다.
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  GraphViz 애플리케이션의 PGQL Graph Query 텍스트 입력 상자에 질의를 복사하여 붙여넣습니다. Run을 누릅니다.
    
    결과는 아래와 같아야 합니다.
    
    ![주기 3 홉](images/cycle-3-hops.jpg)
    

## 확인

*   **작성자** - Jayant Sharma
*   **기여자** - Arabella Yao, Jenny Tsai
*   **최종 업데이트 수행자/날짜** - Ryota Yamanaka, 2023년 3월