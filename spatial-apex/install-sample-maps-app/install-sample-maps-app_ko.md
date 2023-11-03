# 샘플 맵 애플리케이션 설치

## 소개

Oracle APEX는 특정 기능 영역을 강조하는 샘플 애플리케이션 포트폴리오에 대한 액세스를 제공합니다. Oracle APEX의 매핑 기능을 보여주는 샘플 맵 애플리케이션입니다. 추가 사용자 정의를 위한 기능 예제 및 시작점으로 사용할 수 있도록 다양한 예가 제공됩니다. 이 실습에서는 Sample Maps 응용 프로그램을 설치하고 구성합니다.

예상 실험실 시간: 15분

### 목표

*   샘플 맵 애플리케이션 설치
*   지원 데이터 로드

### 필요 조건

*   Oracle APEX 21.1 이상이 필요합니다. 이 워크샵의 스크린샷은 APEX 21.2를 사용하여 촬영됩니다. 일반적으로 [최신 버전의 APEX](https://www.oracle.com/tools/downloads/apex-downloads/)를 사용하는 것이 좋으므로 사용자 인터페이스에 약간의 차이가 있을 수 있습니다.

## 작업 1: 응용 프로그램 설치

1.  먼저 **앱 작성기**를 누릅니다.
    
    ![APEX Application Builder입니다.](images/install-sample-maps-00.png)
    
2.  **시작 또는 샘플 앱 설치**를 누릅니다.
    
    ![시작 또는 샘플 앱 선택](images/install-sample-maps-01.png)
    
    **주:** 작업 영역에 기존 애플리케이션이 있는 경우 **생성**, **Starter 앱** 순으로 누릅니다.
    
3.  **샘플**을 눌러 사용 가능한 샘플 앱 목록이 포함된 새 브라우저 탭을 엽니다.
    
    ![샘플 선택](images/install-sample-maps-02.png)
    
4.  아래로 스크롤하여 **샘플 맵**을 찾고 **앱 다운로드**를 누릅니다.
    
    ![이미지 대체 텍스트](images/install-sample-maps-03.png)
    
    애플리케이션 번들을 로컬 폴더에 저장하라는 메시지가 표시됩니다.
    
    **주:** github로 재지정될 경우 APEX 버전의 폴더로 이동하고 **sample-maps.zip**을 다운로드하십시오.
    
5.  앱 작성기 브라우저 탭으로 돌아가서 **임포트**를 누릅니다.
    
    ![임포트 선택](images/install-sample-maps-04.png)
    
6.  이전에 다운로드한 샘플 맵 애플리케이션 zip 파일을 끌어 놓거나 찾아봅니다. File Type 선택을 Database Application으로 두고 **Next**를 누릅니다.
    
    ![샘플 맵 애플리케이션 zip 선택](images/install-sample-maps-05.png)
    
7.  파일 임포트가 확인되었습니다. **Next**를 다시 누릅니다.
    
    ![Next를 누릅니다.](images/install-sample-maps-06.png)
    
8.  기본 메뉴 선택 항목을 그대로 두고 **응용 프로그램 설치**를 누릅니다.
    
    ![Install Application을 누릅니다.](images/install-sample-maps-07.png)
    
    그러면 애플리케이션 설치 마법사로 이동합니다.
    
9.  기본 메뉴 선택 항목을 그대로 두고 **Next**를 누릅니다.
    
    ![Next를 누릅니다.](images/install-sample-maps-08.png)
    
10.  **다음**을 눌러 시스템 호환성을 검증합니다.
    

![Next를 누릅니다.](images/install-sample-maps-09.png)

11.  호환성이 확인된 경우 **설치**를 눌러 지원되는 데이터베이스 객체 및 APEX 애플리케이션 설치를 시작합니다.

![Install을 누릅니다.](images/install-sample-maps-10.png)

12.  설치가 완료되면 **응용 프로그램 실행**을 누릅니다.

![Run Application을 누릅니다.](images/install-sample-maps-11.png)

13.  APEX 작업영역 사용자 이름 및 비밀번호를 사용하여 샘플 맵 애플리케이션에 사인인합니다.

![로그인](images/install-sample-maps-12.png)

## 작업 2: 데이터 로드

1.  이제 APEX에서 다양한 맵 및 공간 작업 예를 제공하는 샘플 맵 애플리케이션에 있습니다. 초기 실행 시 데이터 로드와 관련된 경고 메시지가 표시됩니다. 해당 메시지 내에서 **데이터 로드** 링크를 누릅니다. 데모 데이터 로드를 완료한 페이지로 이동합니다.
    
    ![데이터 로드를 누릅니다.](images/install-sample-maps-13.png)
    
2.  \[데이터 로드\] 페이지에는 샘플 맵 응용 프로그램과 이 워크샵의 나머지 부분에서 사용되는 상태 및 공항 데이터 집합의 로드 상태가 표시됩니다. 샘플 맵 응용 프로그램 설치 시 이러한 데이터 세트는 부분적으로만 로드됩니다. 샘플 데이터 로드를 완료하려면 github에 저장된 파일에서 직접 로드하거나 먼저 파일을 다운로드하여 로컬 시스템에서 로드할 수 있습니다. 프록시가 github에 액세스해야 하는 네트워크에서 APEX를 실행 중인 경우 후자 옵션을 사용해야 합니다.
    
    APEX 인스턴스에 github에 액세스하는 데 프록시가 필요하지 않은 경우(예: apex.oracle.com 또는 Oracle Autonomous Database의 APEX) 단추를 눌러 **GitHub에서 직접** 로드한 후 오른쪽 상단에서 **데이터 집합 로드**를 누릅니다.
    
    ![Github에서 직접 클릭](images/install-sample-maps-14.png)
    
    APEX 인스턴스에서 github(예: 회사 방화벽 뒤에서 실행되는 APEX)에 액세스하기 위해 프록시가 필요하거나 github에서 직접 로드하는 데 다른 문제가 있는 경우 **파일 업로드** 단추를 눌러 대체 지침을 제공합니다.
    
3.  데이터 로드가 완료되면 오른쪽 상단에 통지가 표시되고 경고 메시지가 사라집니다. 이제 Sample Maps 응용 프로그램을 사용할 준비가 되었습니다.
    
    ![데이터 로드 확인](images/install-sample-maps-15.png)
    

## 작업 3: 샘플 맵 응용 프로그램 탐색

1.  타일을 누르면 애플리케이션의 연관된 페이지로 이동합니다. 예를 들어, **맵 및 보고서**를 누릅니다.
    
    ![맵 및 보고서 페이지로 이동](images/install-sample-maps-16.png)
    
2.  이 페이지에서 맵의 오른쪽 가운데에 있는 보고서의 항목을 누르면 정보 창이 열립니다. 왼쪽 상단 모서리에 있는 아이콘을 누르면 탐색 패널이 열리고 애플리케이션의 다른 페이지에 액세스할 수 있습니다.
    
    ![맵과 상호 작용](images/install-sample-maps-17.png)
    
3.  탐색 패널에서 항목을 눌러 애플리케이션의 다른 페이지에 액세스합니다.
    
    ![탐색 패널에 다른 페이지가 표시됨](images/install-sample-maps-18.png)
    
4.  탐색 패널을 닫으려면 왼쪽 위에 있는 아이콘을 누릅니다. 왼쪽 위에 있는 **샘플 맵**을 눌러 애플리케이션 홈 페이지로 이동할 수도 있습니다.
    
    ![탐색 패널 닫기](images/install-sample-maps-19.png)
    

## 작업 4: 데모 데이터 탐색

1.  APEX로 돌아가서 **SQL 워크샵**, **객체 브라우저** 순으로 누릅니다.
    
    ![SQL Workshop - 객체 브라우저](images/install-sample-maps-20.png)
    
2.  이전에 수행된 데이터 로드 단계로 생성된 테이블을 살펴봅니다. **EBA\_SAMPLE\_MAP\_AIRPORTS**을 누릅니다. 열에 SDO\_GEOMETRY 유형(Oracle의 고유 공간 데이터 유형)이 있는 GEOMETRY라는 열이 포함되어 있는지 확인합니다.
    
    ![고유 형상 열이 있는 테이블](images/install-sample-maps-21.png)
    
3.  테이블 콘텐츠를 보려면 **데이터** 탭을 누릅니다.
    
    ![테이블 내용](images/install-sample-maps-22.png)
    
    그런 다음 오른쪽으로 스크롤하여 형상 열을 확인합니다. 공항은 점으로 저장되므로 APEX는 점 형상 값의 문자열 표현을 표시합니다. 포인트는 항상 단일 좌표를 기반으로 하므로 APEX에서 이 방법으로 값을 표시하는 것이 좋습니다.
    
    ![포인트 도면](images/install-sample-maps-23.png)
    
4.  **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**을 누릅니다. 또한 열에 SDO\_GEOMETRY 유형(Oracle의 고유 공간 데이터 유형)이 있는 GEOMETRY라는 열이 포함되어 있는지 확인합니다.
    
    ![고유 형상 열이 있는 테이블](images/install-sample-maps-24.png)
    
5.  **데이터** 탭을 눌러 테이블 콘텐츠를 봅니다. 이 테이블에는 상태가 저장되므로 형상은 다각형입니다. APEX는 매우 긴 좌표 집합이 포함될 수 있으므로 이러한 값의 문자열 표현을 표시하지 않습니다.
    
    ![다각형 도면](images/install-sample-maps-25.png)
    
6.  이름이 **MDRT\_....$**인 테이블을 확인합니다. 이러한 인덱스는 다른 테이블에 대한 공간 인덱스를 지원하기 위해 데이터베이스에서 백그라운드에서 자동으로 생성 및 관리됩니다. 이러한 테이블을 수동으로 생성, 갱신 또는 삭제할 수는 없습니다. 공간 분석 작업만 지원하며 무시할 수 있습니다.
    
    ![공간 인덱스 아티팩트](images/install-sample-maps-26.png)
    
7.  마지막으로 이 데이터를 사용하여 기본 공간 질의를 실행할 수 있습니다. **SQL Workshop**, **SQL Commands** 순으로 누릅니다.
    
    ![SQL Workshop - SQL 명령](images/install-sample-maps-27.png)
    
8.  다음 질의는 텍사스의 100km 이내의 1000 에이커 이상의 육지 적용이 있는 공항 수를 반환합니다. 고유 공간 연산자 **sdo\_within\_distance**를 사용합니다. 질의를 복사하여 SQL Commands 창에 붙여넣은 후 오른쪽 상단에 있는 **Run**을 누릅니다.
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![공간 질의](images/install-sample-maps-28.png)
    
9.  sdo\_within\_distance 연산자에서 거리를 300km로 업데이트하고 다시 실행합니다. 검색 영역이 클수록 결과 변경 사항을 확인합니다.
    
    ![공간 질의](images/install-sample-maps-29.png)
    

이후 연습에서는 페이지의 메뉴에서 상태와 거리를 제어하는 이 query의 결과를 표시하는 맵을 구성합니다.

이제 Sample Maps 응용 프로그램과 데이터를 설치하고 탐색했습니다. 다음으로 이동하여 고유한 응용 프로그램 및 맵을 만듭니다.

이것은 실험실을 끝낸다. 이제 다음 실습을 진행할 수 있습니다.

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **제공자** - Carsten Czarski, APEX 개발, Oracle
*   **최종 업데이트 기한/일자** - David Lapp, 데이터베이스 제품 관리, 2023년 3월