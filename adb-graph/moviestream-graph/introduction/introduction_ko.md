# 그래프 분석을 사용하여 영화 추천

## 소개

이 워크샵에서는 Graph Studio를 사용하여 동영상 보기 동작을 기반으로 고객 커뮤니티를 감지하고 생성합니다. 커뮤니티를 만든 후에는 커뮤니티 구성원이 본 내용을 기반으로 권장 사항을 작성합니다.

예상 시간: 60분

### Graph Studio 정보

Oracle Autonomous Database에는 확장 가능한 속성 그래프 데이터베이스로 기능할 수 있는 기능이 있습니다. 데이터베이스 테이블에서 그래프 모델 및 인메모리 그래프 생성을 자동화합니다. 여기에는 PGQL을 사용하여 그래프 쿼리를 실행하기 위한 노트북 및 개발자 API, SQL과 유사한 그래프 쿼리 언어, 60개 이상의 내장된 그래프 알고리즘, 기본 그래프 시각화를 포함한 다양한 시각화가 포함됩니다.

속성 그래프 및 사용 사례를 소개하는 다음 비디오를 시청하십시오.

Autonomous Database로 그래프 분석 간소화

[](youtube:eCd-969hrak)

이 워크샵에서는 MOVIE, CUSTOMER\_PROMOTIONS 및 CUSTSALES\_PROMOTIONS 테이블에서 생성된 그래프를 사용합니다. MOVIE 및 CUSTOMER\_PROMOTIONS는 정점 테이블입니다. 이러한 테이블의 모든 행은 정점이 됩니다. CUSTSALES\_PROMOTIONS는 두 테이블을 연결하며 가장자리 테이블입니다. CUSTOMER\_PROMOTIONS의 고객이 MOVIE 테이블에서 그래프의 모서리인 동영상을 대여할 때마다 이 그래프는 이 워크샵에서 사용할 수 있도록 생성되었습니다.

그래프를 분석할 때 사전 구축된 알고리즘을 60개 이상 선택할 수 있습니다. 이 워크샵에서는 제품 권장 사항에 적합한 **Personalized SALSA** 알고리즘을 사용합니다. 고객 정점은 _허브_에 매핑되고 동영상은 _권한_에 매핑됩니다. 허브 점수가 높을수록 고객 간의 긴밀한 관계가 형성됩니다. 높은 권한 점수는 정점(또는 영화)이 해당 근접성을 설정하는 데 더 중요한 역할을 함을 나타냅니다.

### 목표

이 워크샵에서는 Autonomous Database의 Graph Studio 기능을 사용하여 다음을 수행합니다.

*   메모장 사용
*   몇 가지 PGQL 그래프 쿼리 실행
*   python을 사용하여 알고리즘 라이브러리에서 Personalized SALSA 실행
*   권장 사항 질의 및 저장

### 필요 조건

*   Oracle Cloud 계정

## 확인

*   **작성자** - Melli Annamalai, Oracle Spatial and Graph 제품 관리자
*   **제공자** - Jayant Sharma
*   **최종 업데이트 기한/일자** - Ramu Murakami Gutierrez, Oracle Spatial and Graph 제품 관리자, 2023년 2월