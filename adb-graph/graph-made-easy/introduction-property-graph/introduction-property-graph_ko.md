# Graph Studio 작업

## 이 워크샵 정보

이 워크샵에서는 Autonomous Database의 Graph Studio 기능을 사용하는 주요 그래프 데이터 모델링 및 분석 개념을 소개합니다. 그래프 쿼리를 사용하여 사기 거래를 나타내는 순환 지불을 찾는 방법과 많은 거래가 흐르는 계정을 식별하는 그래프 분석 알고리즘을 보여줍니다. (인공) 계정 및 트랜잭션 정보를 포함하는 데이터를 Query하게 됩니다. 먼저 그래프를 생성하고, 그래프를 질의하고, 분석 알고리즘을 실행하고, 결과를 시각화합니다. 선택적 섹션에서는 일반적으로 지식 그래프에 사용되는 RDF(시맨틱) 그래프 개념을 소개하고 n-3중 형식과 같은 표준 RDF 그래프 형식에서 데이터를 로드하는 방법과 RDF 그래프에 대한 쿼리 언어인 SPARQL을 사용하여 쿼리하는 방법을 보여줍니다.

예상 워크샵 시간: 75분

워크샵을 시청하려면 [여기](https://youtu.be/Ymk9TE9Q2K4)를 클릭하십시오.

### Graph Studio 정보

Oracle Autonomous Database에는 확장 가능한 그래프 데이터베이스로 작동할 수 있는 기능이 있습니다. 데이터베이스 테이블에서 그래프 모델 및 인메모리 그래프 생성을 자동화합니다. 여기에는 PGQL을 사용하여 그래프 쿼리를 실행하기 위한 노트북 및 개발자 API, SQL과 유사한 그래프 쿼리 언어, Java 또는 Python API를 사용하는 60개 이상의 내장된 그래프 알고리즘, 기본 그래프 시각화가 포함됩니다.

Graph Studio에 대한 자세한 내용은 다음 두 비디오를 시청하십시오. 첫 번째는 속성 그래프 및 해당 사용 사례에 대한 소개입니다. 두 번째는 Graph Studio 인터페이스를 둘러보는 것입니다.

[Autonomous Database로 그래프 분석 간소화](youtube:eCd-969hrak) Autonomous Database로 그래프 분석 간소화

[Autonomous Database: Graph Studio 인터페이스 투어](youtube:S6Q-IJcBkU0) Autonomous Database: Graph Studio 인터페이스 투어

### 목표

이 워크샵에서는 다음 작업을 수행합니다.

*   PGQL(그래프 질의 언어) CREATE PROPERTY GRAPH 문을 사용하여 그래프 생성
*   분석을 위해 메모리로 그래프 로드
*   노트북 생성
*   PGQL 노트북 단락을 사용하여 그래프 쿼리 및 시각화
*   그래프 알고리즘 실행 및 결과 시각화

### 필요 조건

*   Oracle Cloud 계정
*   프로비저닝된 Autonomous Database-서버리스 인스턴스

이 연습을 마칩니다. **이제 다음 실습을 진행할 수 있습니다.**

## 확인

*   **작성자** - Jayant Sharma, 제품 관리
*   **제공자** - Jayant Sharma, 제품 관리
*   **최종 업데이트 기한/일자** - Ramu Murakami Gutierrez, 2023년 8월 제품 관리자