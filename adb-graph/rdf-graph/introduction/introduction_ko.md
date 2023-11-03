# Graph Studio에서 RDF 그래프 사용

## 소개

Oracle Autonomous Database의 Graph Studio를 통해 사용자는 그래프 데이터를 모델링, 생성, 쿼리, 분석할 수 있습니다. 여기에는 노트북, PGQL을 사용하여 그래프 쿼리를 실행하기 위한 개발자 API, 60개 이상의 내장된 그래프 알고리즘이 포함되며, 기본 그래프 시각화를 포함한 수십 개의 시각화가 제공됩니다. 이제 속성 그래프 외에도 Graph Studio는 RDF(Resource Description Framework) 및 OWL(Web Ontology Language)을 기반으로 데이터 및 온톨로지에 대한 저장, 추론 및 쿼리 기능을 포함한 의미 기술에 대한 지원을 확대합니다. 이제 지원되는 다음 RDF 기능에 대해 Graph Studio를 사용할 수 있습니다.

*   RDF 그래프 생성
*   노트북 단락의 RDF 그래프에서 SPARQL 질의 실행
*   RDF 그래프 분석 및 시각화

RDF는 연결된 데이터를 나타내는 W3C 표준 데이터 모델입니다. RDF는 URI(Uniform Resource Identifier)를 리소스 및 URI에 대한 전역 고유 식별자로 사용하여 두 리소스 간의 관계 이름을 지정합니다. URI 외에도 RDF는 리터럴을 사용하여 숫자, 문자열 및 시간 기록과 같은 스칼라 값을 나타냅니다. RDF는 연결된 데이터를 레이블이 지정된 지시형 그래프로 모델링합니다. 여기서 각 모서리를 일반적으로 삼중이라고 합니다. 모서리의 소스 정점을 삼중의 주체라고 합니다. 모서리의 레이블 또는 이름을 삼중의 술어라고 하며 모서리의 대상 정점을 삼중의 객체라고 합니다. RDF 그래프는 특히 지식 그래프 및 데이터 통합 애플리케이션에 적합합니다. URI는 전역적으로 고유한 식별자를 제공하고, 간단하고 스키마 없는 3중 구조를 통해 여러 RDF 그래프의 데이터를 단일 그래프로 매우 쉽게 결합할 수 있기 때문입니다. 또한 RDFS 및 OWL은 보다 상호 운용 가능한 머신 처리 가능한 그래프 데이터를 위해 재사용 가능한 어휘(반면적으로 의미 있는 에지 레이블 및 리소스 유형 세트)를 정의하는 표준 방법을 제공합니다. W3C RDF 1.1 표준에 대한 자세한 내용은 [여기](https://www.w3.org/TR/rdf11-primer/)를 참조하십시오.

SPARQL(SPARQL Protocol and RDF Query Language)은 RDF(Resource Description Framework) 데이터를 쿼리하기 위해 W3C에 의해 표준화된 기술 중 하나입니다. W3C SPARQL 1.1 표준에 대한 자세한 내용은 [여기](https://www.w3.org/TR/sparql11-overview/)에서 확인할 수 있습니다.

SPARQL은 **일부 조건인 일부 요소 선택** 구조를 사용하여 질의를 지정합니다. SPARQL 질의의 WHERE 절에 있는 조건은 3중 패턴을 사용하여 작성됩니다. 이 패턴은 기본적으로 3중 요소를 질의 변수로 바꿀 수 있는 RDF 3중입니다(? 접두어로 표시됨). 삼중 패턴의 질의 변수는 와일드 카드 문자로 사용됩니다. 3중 패턴 **?movie ms:genre ms:genre\_Comedy**를 고려합니다. 이 삼중 패턴이 RDF 그래프에 대해 평가되면 술어 **ms:genre** 및 **object ms:genre\_Comedy**를 사용하여 삼중의 모든 **subjects**를 반환합니다. SPARQL SELECT 절은 query에서 투영할 query 변수 리스트를 지정합니다. SPARQL 구문에서 URI는 꺾쇠 괄호 안에 묶이고 리터럴은 큰따옴표 안에 묶입니다(예: "Kevin Bacon"). 리터럴 뒤에는 ^^ 및 데이터 유형 URI(예: "100"^^[http://www.w3.org/2001/XMLSchema#integer](http://www.w3.org/2001/XMLSchema#integer))가 올 수도 있고 @ 및 언어 태그(예: "Jalapeño"@es)가 올 수도 있습니다. 대부분의 XML 스키마 데이터 유형은 SPARQL에서 지원되며, 데이터 유형 URI가 없는 일반 리터럴은 [http://www.w3.org/2001/XMLSchema#string](http://www.w3.org/2001/XMLSchema#string) 데이터 유형으로 간주됩니다.

아래에 소개된 이 비디오는 이 실습에서 활용할 유사한 데이터 세트를 사용하는 데모 예입니다. 이 비디오는 RDF를 사용하는 영화 구조의 온톨로지의 구조를 강조합니다. 이 데모는 SQL Developer와 함께 스테이지 테이블을 사용하는 RDF Graph를 특징으로 하며, 이 랩의 Autonomous Database 버전과는 다른 특징입니다. 그러나 데이터를 쿼리하고 시각화하는 데 사용되는 SPARQL 언어는 컨텍스트와 매우 유사합니다.

[](youtube:e_EQjInas50)

이 실습에서는 의미형 그래프가 다양한 데이터 소스를 통합하는 표준화된 방법론인 SPARQL을 사용하여 작성됩니다. 이 절차에서는 그래프 기반 쿼리 및 시각화를 사용하여 데이터를 분석하는 방법을 설명합니다.

예상 시간: 35분

### 목표

*   환경 준비
*   RDF 그래프 시작하기
*   Graph Studio에서 RDF 그래프 사용자 생성 및 검증
*   RDF 그래프 쿼리 및 시각화

### 필요 조건

이 실습에서는 다음을 가정합니다.

*   Oracle Cloud 계정 - 이 워크숍의 LiveLabs 랜딩 페이지를 통해 지원되는 환경을 확인하십시오.

*   이 [링크](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/moviestream_rdf.nt)를 사용하여 MOVIESTREAM 파일(moviestream\_rdf.nt)을 다운로드합니다.

이 연습을 마칩니다. 이제 _다음 실습을 진행할 수 있습니다._

## 확인

*   **작성자** - Nicholas Cusato, Ethan Shmargad, Matthew McDaniel 솔루션 엔지니어, Ramu Murakami Gutierrez 제품 관리자
*   **기술 기여자** - Melliyal Annamalai Distinguished Product Manager, Joao Paiva Consulting Member of Technical Staff, Lavanya Jayapalan Principal User Assistance Developer
*   **최종 업데이트 기한/일자** - Ramu Murakami Gutierrez 제품 관리자, 2023년 6월