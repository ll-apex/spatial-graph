# 소개

## 이 워크샵 정보

이 워크샵에서는 OCI Cloud Marketplace의 Oracle Cloud에 Spatial Studio를 프로비저닝하고 Spatial Studio의 메타데이터 저장소로 사용할 Autonomous Database의 스키마를 준비합니다.

예상 워크샵 시간: 60분

### Oracle Spatial Studio 정보

Oracle Spatial Studio(Spatial Studio)는 Oracle Database의 공간 기능에 대한 셀프 서비스 액세스를 제공하는 웹 애플리케이션입니다. 이러한 기능에는 과거에는 타사 도구의 코딩 및/또는 사용이 필요했지만 Spatial Studio를 사용하면 비즈니스 사용자가 셀프 서비스 GUI를 사용하여 공간 분석 및 대화식 웹 맵을 만들고 공유할 수 있습니다.

![이미지 대체 텍스트](./images/spatial-studio.png "공간 스튜디오")

Spatial Studio는 Oracle Database의 공간 데이터에서 작동하며, 이는 Oracle의 기하학 데이터 유형을 포함하는 테이블 및 뷰를 의미합니다. 이 데이터는 기존 공간 데이터이거나 Spatial Studio를 사용하여 속성을 기반으로 형상을 추가할 수 있도록 준비된 공간 데이터가 아닙니다.

Spatial Studio는 Oracle Cloud Marketplace에서 Oracle Cloud에 배포할 수 있는 Java EE 애플리케이션입니다. Spatial Studio는 Oracle WebLogic 또는 Jetty에 수동으로 배포하거나, 자체적으로 사전 배포된 테스트용 Quick Start로 배포할 수도 있습니다.

자세한 내용은 \[https://oracle.com/goto/spatialstudio\](https://oracle.com/goto/spatialstudio)을 참조하십시오.

### 목표

*   Spatial Studio의 메타데이터 저장소에 대한 데이터베이스 스키마를 생성하고 지정하는 방법 알아보기
*   Cloud Marketplace를 사용하여 Spatial Studio를 설치하는 방법 알아보기
*   더 이상 필요하지 않은 경우 Spatial Studio를 제거하는 방법 알아보기

### 필요 조건

*   이 워크샵에는 Oracle Autonomous Database가 필요합니다.
*   SQL Developer Web은 Autonomous Database와 함께 제공되며 Spatial Studio 저장소 스키마를 생성하는 데도 사용됩니다.
*   이미 액세스 권한이 있는 경우 이 소개를 따라 실습 3으로 건너뛸 수 있습니다.
*   그렇지 않으면 Lab 1을 진행해야 합니다.
*   Oracle Spatial에 대한 이전 경험은 필요하지 않습니다.
*   Oracle Cloud 계정 - 이 워크숍의 LiveLabs 랜딩 페이지를 통해 지원되는 환경을 확인하십시오.

_참고: **무료 체험판** 계정이 있는 경우 무료 체험판 만료 시 계정이 **항상 무료** 계정으로 변환됩니다. 상시 무료 환경을 사용할 수 없으면 Free Tier 워크샵을 수행할 수 없습니다. **[Free Tier FAQ 페이지를 보려면 여기를 클릭하십시오.](https://www.oracle.com/cloud/free/faq.html)**_

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 기한/일자** - David Lapp, 데이터베이스 제품 관리, 2021년 1월