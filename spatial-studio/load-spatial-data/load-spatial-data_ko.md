# 공간 데이터 로드

## 소개

Spatial Studio는 Oracle Databases에 저장된 데이터에서 작동합니다. Spatial Studio에서는 데이터베이스 연결을 통해 액세스되는 데이터베이스 테이블 및 뷰인 "데이터 집합"으로 작업합니다. 데이터 집합은 데이터베이스 테이블 및 뷰에 대한 포인터이며 기본 데이터베이스 테이블 또는 뷰 이름보다 자체 설명할 수 있도록 친숙한 이름을 지정할 수 있습니다.

사용자는 종종 다양한 소스에서 획득한 데이터를 통합해야 합니다. 이를 지원하기 위해 Spatial Studio는 표준 형식에서 Oracle Database로 데이터를 로드하는 기능을 제공합니다. 여기에는 공간 데이터 교환을 위한 가장 일반적인 두 가지 형식인 Shapefiles 및 GeoJSON 파일 로드가 포함됩니다. 이 실습에서는 Spatial Studio를 사용하여 이러한 형식으로 공간 데이터를 로드하는 단계를 안내합니다.

Spatial Studio는 공간 형식을 로드하는 것 외에도 스프레드시트 로드를 지원합니다. 이 경우 주소("주소 지오코딩") 및 위도/경도 좌표("좌표 인덱싱")와 같은 공간 속성에서 지오메트리를 파생하려면 추가 준비가 필요합니다. 이러한 사례는 이 실습에서 다루지 않지만 별도의 실습에서 다루게 됩니다.

예상 실험실 시간: 15분

### 목표

*   Shapefiles 및 GeoJSON에서 공간 데이터를 로드하는 방법 알아보기
*   데이터세트에 대한 키 필드를 설정하는 방법 알아보기

### 필요 조건

*   이 실습에서는 Spatial Studio 및 Oracle Database에 액세스해야 합니다.
*   Oracle Cloud Marketplace에서 배포하려면 [여기](https://cloud.oracle.com/marketplace/application/71472162/overview) 목록으로 이동하여(Oracle Cloud 계정에 로그인하라는 메시지가 표시됨) [여기](https://blogs.oracle.com/database/post/oracle-spatial-studio-221-now-on-cloud-marketplace)에서 지침을 따르십시오.
*   Oracle Spatial에 대한 이전 경험은 필요하지 않습니다.

## 작업 1: 사고 데이터 로드

먼저 GeoJSON 파일에서 교통 사고 데이터 세트를 로드합니다. 데이터는 가상이며 남아프리카의 도로를 따라 무작위 위치에 대해 생성되었습니다.

1.  GeoJSON 파일을 편리한 위치([accidents.geojson](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/accidents.geojson))로 다운로드합니다.
    
2.  Spatial Studio의 왼쪽 패널 메뉴에서 \[데이터 집합\] 페이지로 이동하여 **데이터 집합 생성**을 누르고 accidents.geojson을 끌어 놓습니다. 업로드 영역을 누르고 해당 파일을 선택하여 이동할 수도 있습니다. ![데이터 집합 생성](images/load-data-1.png)
    
3.  GeoJSON 데이터 미리보기가 표시됩니다. 이 업로드에 대한 대상 접속을 선택합니다. 이 워크샵에서는 SPATIAL\_STUDIO 접속(Spatial Studio 메타데이터 저장소)을 사용하지만 운용 시나리오에서는 메타데이터 저장소와 별도로 해당 비즈니스 데이터에 대한 다른 접속을 사용합니다. NR\_VEHICLES 및 SEVERITY의 데이터 유형을 NUMERIC으로 설정합니다. **제출**을 눌러 업로드를 시작합니다. ![GeoJSON 데이터 미리보기 표시](images/load-data-2.png)
    
4.  업로드된 ACCIDENTS 데이터 세트는 준비 단계가 필요함을 나타내는 작은 경고 아이콘과 함께 나열됩니다. 이 경우 데이터 세트 키를 추가해야 합니다. 기본 매핑에는 필요하지 않지만 이후 워크샵 섹션의 분석에 키가 필요하므로 지금 키를 추가합니다. 경고 아이콘을 누른 다음 **데이터 집합 열로 이동** 링크를 누릅니다. ![사고 데이터 세트에 대한 경고 상자](images/load-data-3.png)
    
5.  ACCIDENTS 데이터에 고유 식별자 열이 있으면 키로 지정할 수 있습니다. 그러나 이 가상의 데이터에는 이러한 열이 없으므로 Spatial Studio에서 열을 생성합니다. **키 열 생성**을 누르고 이름을 ACCIDENT\_ID로 설정한 다음 **적용**을 누릅니다. ![열 이름을 입력하십시오.](images/load-data-4.png) 매핑 및 공간 분석을 위해 준비된 경고 없이 나열된 ACCIDENTS 데이터 집합을 확인합니다. ![경고가 없는 사고 데이터 세트](images/load-data-5.png)
    

## 작업 2: 경찰서 데이터 로드

다음으로 단일 zip 파일에 저장된 쉐이프 파일에서 남아프리카 경찰서(SAPS) 스테이션 및 스테이션 경계를 로드합니다.

1.  편리한 위치([SAPS\_police.zip](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/SAPS_police.zip))에 Shapefiles가 포함된 zip 파일을 다운로드합니다.
    
2.  \[데이터 집합\] 페이지로 이동하여 **데이터 집합 생성**을 누르고 SAPS\_police.zip을 끌어 놓습니다. Spatial Studio는 zip 파일에서 Shapefiles를 추출하여 개별적으로 처리합니다. ![데이터 집합 생성](images/load-data-6.png)
    
3.  추출 된 첫 번째 Shapefile은 경찰서 경계, 즉 역에서 순찰 한 지리적 영역이 될 것입니다. 대상 Connection을 선택하고 테이블 및 데이터 집합 이름을 POLICE\_BOUNDS로 설정합니다. ![Shapefile 데이터 미리보기 표시(파일 1)](images/load-data-7.png)
    
4.  추출된 두 번째 Shapefile은 경찰서입니다. 대상 Connection을 선택하고 테이블 및 데이터 집합 이름을 POLICE\_POINTS로 설정합니다. ![ Shapefile 데이터 미리보기 표시(파일 2)](images/load-data-8.png)
    
5.  키를 정의해야 하므로 이제 POLICE\_BOUNDS 및 POLICE\_POINTS 데이터 세트가 경고와 함께 나열됩니다. POLICE\_BOUNDS에 대한 경고 아이콘을 누른 다음 **데이터 집합 열로 이동** 링크를 누릅니다. ![ 경찰 경계 데이터 세트에 대한 경고 상자](images/load-data-9.png)
    
6.  이 경우 키로 사용할 기존 고유 열이 있습니다. COMPNT\_NAME 열에 대해 **키로 사용**을 선택하고 **키 검증**을 누른 다음 **적용**을 누릅니다. ![기존 열을 키로 사용](images/load-data-10.png)
    
    5단계와 6단계를 반복하여 데이터 세트 POLICE\_POINTS에 대한 키를 설정합니다.
    
7.  이제 모든 데이터세트를 매핑 및 공간 분석할 준비가 되었습니다. ![분석 준비가 완료된 데이터 세트](images/load-data-11.png)
    

이제 [다음 실습을 진행하십시오](#next).

## 자세히 알아보기

*   \[Spatial Studio 제품 포털\] (https://oracle.com/goto/spatialstudio)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 기한/일자** - Denise Myrick, 데이터베이스 제품 관리, 2023년 4월
*   **랩 만료** - 2024년 3월 31일