# 소개

## 이 워크샵 정보

이 워크샵에서는 Map Region 기능 및 Oracle Spatial을 사용하여 Oracle APEX에서 매핑을 살펴봅니다. 다양한 유용한 매핑 예제가 포함된 사전 작성된 샘플 응용 프로그램을 설치하고 탐색합니다. 그런 다음 마법사를 사용하거나 처음부터 맵을 구성하여 고유한 응용 프로그램을 만듭니다.

맵 영역은 APEX 21.1에 도입된 고유 APEX 기능으로, Oracle Spatial, GeoJSON 및 좌표의 공간 데이터를 표시하는 대화식 맵을 구성할 수 있습니다. 이 워크샵에서는 원시 공간 데이터와 공간 분석 결과를 쉽게 통합할 수 있도록 Oracle Spatial을 공간 데이터 소스로 사용하는 방법에 대해 중점적으로 다룹니다.

![샘플 맵 앱](./images/intro-01.png "Oracle Application Express - 샘플 맵 애플리케이션입니다. ")

예상 워크샵 시간: 1시간 15분

### APEX(Oracle Application Express) 및 Oracle Spatial 정보

Oracle Application Express(APEX) 및 Oracle Spatial은 ADW(Autonomous Data Warehouse) 및 ATP(Autonomous Transaction Processing) 서비스를 포함한 Oracle Database의 기능입니다.

Oracle Application Express(APEX)는 어디든 배치할 수 있는 세계적 수준의 기능을 통해 안전하고 확장성을 갖춘 엔터프라이즈 앱을 구축하도록 돕는 로우코드 개발 플랫폼입니다. [Oracle APEX 제품 홈페이지](https://apex.oracle.com)에서 자세히 알아보기

Oracle Spatial은 Oracle Database 내의 지리 공간 데이터 관리, 분석 및 처리 기능 세트입니다. 기본 공간 데이터 유형 및 분석 작업을 통해 위치 기반 분석은 주류이며 다른 모든 데이터베이스 작업과 함께 배치됩니다. [Oracle Spatial 제품 홈페이지](https://www.oracle.com/database/spatial)에 대한 자세한 내용

### 목표

*   APEX Map Region 샘플 이해
*   맵 영역을 생성 및 구성하는 방법 학습
*   Oracle Spatial에 위치 분석 통합 방법 학습

### 필요 조건

*   Oracle APEX 21.1 이상이 필요합니다. 이 워크샵의 스크린샷은 APEX 21.2를 사용하여 촬영됩니다. 일반적으로 [최신 버전의 APEX](https://www.oracle.com/tools/downloads/apex-downloads/)를 사용하는 것이 좋으므로 사용자 인터페이스에 약간의 차이가 있을 수 있습니다.
*   Oracle APEX 기본 사용 경험이 권장되지만 필수는 아닙니다. 필요한 경우 LiveLabs APEX 소개 워크숍 [Oracle Autonomous Cloud Service용 기존 테이블을 기반으로 앱 생성](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=628)을 검토하십시오.
*   Oracle Spatial에 대한 기본적인 경험이 필요한 것은 아니지만 권장됩니다. 필요한 경우 다음 소개 LiveLabs 공간 워크샵을 검토하십시오. [Oracle Spatial 소개](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=736)

_참고: **무료 체험판** 계정이 있는 경우 무료 체험판 만료 시 계정이 **항상 무료** 계정으로 변환됩니다. 상시 무료 환경을 사용할 수 없으면 Free Tier 워크샵을 수행할 수 없습니다. **[Free Tier FAQ 페이지를 보려면 여기를 클릭하십시오.](https://www.oracle.com/cloud/free/faq.html)**_

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **제공자** - Jayson Hanes, APEX 제품 관리, Oracle
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 3월