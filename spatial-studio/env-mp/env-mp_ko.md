# Spatial Studio 설치

## 소개

이 실습에서는 Oracle Cloud Marketplace를 사용하여 Oracle Spatial Studio(Spatial Studio)를 프로비저닝하는 프로세스를 살펴봅니다. Oracle Cloud Marketplace는 Oracle 및 타사가 제공하는 앱과 서비스를 제공합니다. 자세한 내용은 [여기](https://docs.oracle.com/en/cloud/marketplace/marketplace-cloud/index.html)에서 확인할 수 있습니다.

예상 실험 시간: 30분

### 목표

이 실습에서는 다음을 수행합니다.

*   Oracle Cloud Marketplace에서 Spatial Studio를 설치하는 방법 알아보기
*   초기 실행 시 Spatial Studio 저장소 스키마를 설정하는 방법 알아보기

### 필요 조건

*   Oracle Free Tier, 상시 무료, 유료 또는 LiveLabs 클라우드 계정
*   저장소 스키마가 생성되었습니다(랩 3).

## 작업 1: Marketplace에서 Spatial Studio 선택

1.  왼쪽 위에 있는 **탐색 메뉴**를 누르고 **마켓플레이스**를 선택합니다.

![Oracle Cloud Marketplace](https://oracle-livelabs.github.io/common/images/console/marketplace.png "시장")

2.  Spatial Studio를 검색한 다음 Oracle Spatial Studio 앱을 누릅니다.

![Oracle Cloud Marketplace의 Oracle Spatial Studio](images/env-marketplace-2.png "Oracle Spatial Studio Marketplace 이미지")

3.  사용 지침을 검토한 다음 조항 및 조건에 동의하고 스택 실행을 누릅니다.

![스택을 실행하여 Oracle Spatial Studio 배포](images/env-marketplace-3.png "스택 실행")

## 작업 2: 스택 생성 마법사

1.  선택적으로 배치 스택에 대한 사용자정의 이름과 설명을 입력합니다. 그런 다음 배치에 사용할 구획을 선택하고 Next를 누릅니다.

![스택 마법사 생성](images/env-marketplace-4.png "마법사를 사용하여 스택 생성")

2.  컴퓨트 인스턴스의 가용성 도메인 및 구성을 선택합니다.

컴퓨트 구성에 대한 자세한 내용은 [여기](https://docs.oracle.com/en-us/iaas/Content/Compute/References/computeshapes.htm)에서 확인할 수 있습니다. 가용성 도메인에서 원하는 구성의 할당량 가용성을 확인합니다. 항상 무료 구성을 사용하는 경우 특히 중요합니다. \*OCI 콘솔에서 거버넌스 > 제한, 할당량 및 사용량으로 이동합니다. \* 서비스의 경우 컴퓨트를 선택하고 범위에 대해 가용성 도메인을 선택합니다. \*원하는 구성의 가용성 확인 \* 필요한 경우 가용성 도메인 선택을 변경하여 사용 가능한 할당량을 식별합니다.

![Oracle Cloud 리소스의 제한, 할당량 및 사용량](images/env-marketplace-4-1.png "컴퓨트 리소스 제한")

할당량을 확인한 후 스택 생성 마법사에서 선택합니다.

![스택 매개변수 설정](images/env-marketplace-5.png "컴퓨트 인스턴스 선택")

그런 다음 아래로 이동합니다.

3.  선택적으로 HTTPS 포트 및 Spatial Studio 관리자 사용자 이름을 기본값에서 변경합니다. Spatial Studio 관리자 사용자 인증의 경우 OCI Vault 암호 또는 암호를 사용할 수 있습니다. 아래 이미지는 비밀번호를 사용하는 예를 보여줍니다. 운용 중인 배치의 경우 OCI 저장소 암호를 사용하는 것이 좋습니다. 네트워크 구성 섹션까지 아래로 이동합니다.

참고: 기본적으로 Spatial Studio 관리자 사용자 이름은 **admin**입니다. 데이터베이스에 저장된 저장소 스키마에 대해 랩 3에서 생성된 데이터베이스 사용자 이름(studio\_repo)과 다른 Spatial Studio 애플리케이션 사용자입니다.

![포트 및 암호와 같은 추가 파라미터 설정](images/env-marketplace-6.png "Spatial Studio 고급 구성 - Spatial Studio 관리자 사용자 비밀번호")

4.  네트워킹의 경우 새 VCN 또는 기존 VCN을 자동으로 생성할 수 있습니다. 새 VCN을 생성하거나 기존 VCN을 검색할 구획을 선택합니다.

아래 이미지는 \[새 VCN 생성\]을 사용하는 예를 보여줍니다. 기존 VCN을 사용하려면 2단계에서 선택한 것과 동일한 가용성 도메인에 있어야 합니다. 기존 VCN이 없는 경우 나머지 기본값은 그대로 유지할 수 있습니다. 다른 기존 VCN이 있는 경우 충돌을 방지하려면 CIDR 값을 업데이트하십시오.

![네트워크 구성](images/env-marketplace-7.png "Spatial Studio 고급 구성 - 네트워크 구성")

SSH Keys 섹션을 아래로 이동합니다.

5.  SSH 공용 키를 로드하면 관리 목적으로 Spatial Studio의 파일 시스템에 액세스할 수 있습니다. 대화 상자에는 일반 SSH 연결 설명서에 대한 링크가 있습니다. 키 파일을 찾아보거나 키 문자열을 복사 붙여넣어 SSH 공개 키를 제출합니다. 파일에서 SSH 공개 키를 로드하면 아래 이미지와 같이 키 파일 이름이 표시됩니다. Next를 누릅니다.

![SSH 키 추가](images/env-marketplace-8.png "Spatial Studio 고급 구성 - 공용 SSH 키")

6.  항목 요약을 검토합니다. 수정이 필요한 경우 Back을 누릅니다. 그렇지 않은 경우 Create를 눌러 배치 프로세스를 시작합니다. 배치에 대한 \[작업 세부정보\] 페이지로 재지정됩니다.

![스택 생성](images/env-marketplace-9.png "스택 정의 검토 및 스택 생성")

## 작업 3: 배치 진행률 모니터

1.  Job Details 페이지 하단에 있는 Logs 섹션에 진행률이 표시됩니다. 배치를 설정할 때 처음에 스피너를 표시합니다.

![스택 배치 작업 모니터 - Terraform Apply](images/env-marketplace-10.png "스택 배치 진행률 모니터")

몇 분 후 로그 정보가 표시됩니다.

![배치 작업에 대한 로그 정보](images/env-marketplace-11.png "스택 배치 로그")

2.  Log 섹션 아래쪽으로 이동합니다. 완료되면 Apply Complete!와 instance 세부 정보를 차례로 확인합니다. 마지막으로 나열된 항목은 Spatial Studio 공용 URL입니다. 이 URL을 복사하여 브라우저에 붙여 넣습니다.

![배치 작업이 성공적으로 완료되었습니다.](images/env-marketplace-12.png "배치된 스택의 출력 변수")

## 작업 4: 처음 로그인

1.  Spatial Studio 공용 URL을 처음으로 열면 개인 정보 보호 및 보안과 관련된 브라우저 경고가 표시됩니다. 특정 경고는 플랫폼과 브라우저에 따라 다릅니다.

![Spatial Studio URL을 여는 중 경고가 발생했습니다.](images/env-marketplace-13.png "브라우저 연결 경고")

이 문제는 Spatial Studio 문제가 아닙니다. 서명된 HTTPS 인증서가 없는 웹 사이트에 액세스하는 것이 일반적입니다. 서명된 인증서를 로드하고 구성하면 이 경고가 제거됩니다. 그러나 Jetty에서 인증서를 로드하는 프로세스는 이 워크샵의 범위를 벗어납니다.

링크를 눌러 웹 사이트로 이동합니다.

2.  Spatial Studio 관리자 사용자 이름(기본값은 admin)과 2단계에서 입력한 암호(스택 만들기 마법사, 항목 3)를 입력합니다. 그런 다음 Sign In을 누릅니다.

![Spatial Studio에 로그인하기 위한 사용자 이름 및 비밀번호 제공](images/env-marketplace-14.png "Spatial Studio 로그인 대화상자")

3.  Spatial Studio 인스턴스에 처음 로그인하면 Spatial Studio의 메타데이터 저장소로 사용할 데이터베이스 스키마에 대한 연결 정보를 묻는 메시지가 표시됩니다. 이 스키마는 Spatial Studio의 모든 메타데이터에 사용되는 데이터베이스 스키마이며 Spatial Studio 관리자 사용자가 다른 데이터를 저장하는 데 사용할 수도 있습니다. Lab 3에서 생성된 스키마를 사용하므로 Oracle Autonomous Database를 선택하고 Next를 누릅니다.

![메타데이터 접속 유형 선택](images/env-marketplace-15.png "Spatial Studio 메타데이터 저장소 유형 선택")

4.  Lab 3에 저장된 Wallet 파일을 찾아보거나 끌어 놓습니다. 로드 후 전자 지갑 파일 이름이 선택된 전자 지갑으로 나열됩니다. OK를 누릅니다.

![전자 지갑 업로드](images/env-marketplace-16.png "접속 전자 지갑 업로드")

5.  Lab 2 및 서비스에 정의된 사용자 이름과 암호를 입력합니다. Medium 서비스 레벨은 이 워크샵에 적합합니다. OK를 누릅니다.

![메타데이터 저장소에 대한 접속 세부정보를 입력합니다.](images/env-marketplace-17.png "접속 세부정보를 입력합니다.")

6.  Spatial Studio가 스키마에 초기 연결을 설정하고 여러 메타데이터 테이블을 생성하는 동안 잠시 기다립니다. 완료되면 시작 정보로 Spatial Studio가 열립니다.

![Spatial Studio 홈페이지 - 시작하기](images/env-marketplace-18.png "Spatial Studio 랜딩 페이지")

## 작업 5: 데이터 로드 및 맵 생성

Spatial Studio가 제대로 작동하는지 확인하려면 작은 데이터 샘플을 로드, 준비 및 시각화합니다. 데이터에는 이름과 주소를 포함한 박물관 목록이 포함되어 있습니다. 대화식 맵에서 데이터를 지오코딩하고 데이터를 시각화합니다.

1.  이 확인에 Spatial Studio 저장소 연결을 사용할 수 있으므로 여기에서 연결을 생성하지 않습니다. 타일을 눌러 **데이터 집합 생성**을 수행합니다.

![데이터 업로드를 위한 마법사 시작](images/verify-1.png "데이터 집합 생성")

2.  [여기](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/sf_area_museums.xlsx)에서 데이터 샘플 파일을 다운로드하고 편리한 위치에 저장하십시오. 그런 다음 파일을 파일 업로드 타일로 끌어 놓습니다. 파일 업로드 타일을 누르고 파일로 이동할 수도 있습니다.

![데이터를 업로드하여 데이터 집합 생성](images/verify-2.png "기존 스프레드시트 데이터 업로드")

3.  데이터 미리보기에서 Connection 업로드를 SPATIAL\_STUDIO으로 설정하고 POSTAL\_CODE의 데이터 유형을 STRING으로 설정합니다. 그런 다음 **제출**을 누릅니다.

![업로드 세부정보 지정](images/verify-3.png "업로드 세부정보 지정 및 열 설정 확인")

4.  업로드가 완료되면 작업 수행을 나타내는 경고 아이콘과 함께 데이터 세트가 나열됩니다. 경고 아이콘을 누른 다음 **데이터 집합 열로 이동** 링크를 눌러 키 열을 지정합니다.

![데이터 집합의 키 열 설정](images/verify-4.png "데이터 세트 문제 해결 - 키 열 선택 또는 추가")

5.  NAME을 키로 선택한 다음 **Validate key**를 누릅니다.

![키 검증](images/verify-5.png "선택한 키 검증")

키를 검증한 후 **Apply**를 누릅니다.

6.  경고 아이콘을 다시 누른 다음 **지오코드 주소** 단추를 눌러 맵 시각화를 위해 주소를 좌표 위치로 변환합니다.

![지역 번호](images/verify-7.png "데이터 세트 문제 해결 - 지오코드 주소")

7.  ADDRESS 및 POSTAL\_CODE 열이 지오코딩에 사용하도록 자동으로 감지되었는지 확인합니다. 기본값을 적용하고 **적용**을 누릅니다.

![지역 코드 주소 매핑](images/verify-8.png "지오코딩 참조 데이터로 데이터 집합 매핑")

지오코딩이 완료되면 \[데이터 집합\] 페이지로 돌아갑니다.

8.  SF\_AREA\_MUSEUMS 데이터 집합에 대한 작업 메뉴를 누르고 **프로젝트 생성**을 선택합니다.

![프로젝트 생성 시작](images/verify-9.png "데이터 집합에 대한 새 프로젝트 생성")

9.  SF\_AREA\_MUSEUMS 데이터 집합을 눌러서 맵의 아무 곳에나 놓습니다.

![데이터 집합을 추가하고 맵 캔버스로 끌어오기](images/verify-10.png "프로젝트에 데이터 세트를 계층으로 추가")

SF\_AREA\_MUSEUMS 데이터 집합이 맵 층으로 추가되고 맵이 데이터 영역으로 이동 및 확대/축소됩니다.

10.  SF\_AREA\_MUSEUMS 계층에 대한 작업 메뉴를 누르고 **설정**을 선택합니다.

![데이터 층 설정](images/verify-11.png "데이터 층에 대한 스타일 등을 정의합니다.")

11.  선택한 색상과 불투명도를 선택하여 맵 레이어의 스타일을 지정합니다.

![스타일 설정](images/verify-12.png "데이터 레이어의 색상과 불투명도 선택")

12.  **상호 작용** 탭을 누르고 **정보 창 표시**를 사용으로 설정한 다음 모든 열을 선택합니다. 그런 다음 맵에서 항목을 누르면 선택한 항목에 대한 데이터 값이 포함된 정보 창이 표시됩니다.

![맵 상호 작용에 대한 설정](images/verify-13.png "맵과의 상호 작용에 대한 세부정보 정의")

기본 데이터 준비 및 시각화가 제대로 작동하는지 확인합니다.

13\. 왼쪽 탐색 패널 버튼을 눌러 데이터 세트 페이지로 돌아갑니다. 이 테스트를 보존할 필요가 없으므로 **변경 사항 무시** 옵션을 선택합니다.

![변경사항 무시](images/verify-14.png "현재 프로젝트에 대한 변경사항 폐기")

14.  확인이 완료되면 테스트 데이터 집합 및 데이터베이스 테이블을 삭제할 수 있습니다. SF\_AREA\_MUSEUMS의 작업 메뉴를 누르고 **삭제**를 선택합니다.

![데이터 집합 삭제](images/verify-15.png "데이터 집합 삭제")

15.  데이터베이스 테이블을 삭제하는 옵션을 선택하고 **확인**을 누릅니다.

![데이터베이스 테이블을 영구적으로 삭제하려면 선택합니다.](images/verify-16.png "데이터 집합과 관련된 데이터베이스 테이블 삭제")

이제 Oracle Spatial Studio가 프로비저닝 및 테스트되었습니다. 다음 실습에서는 더 이상 필요하지 않을 때 Spatial Studio를 해체하는 단계를 제공합니다.

## 작업 6: Spatial Studio 제거(더 이상 필요하지 않은 경우)

**Marketplace 배포를 완전히 제거하려면 다음을 진행하십시오.**

1.  왼쪽 위에 있는 **탐색 메뉴**를 누르고 **개발자 서비스**로 이동한 다음 **스택**을 선택합니다.

![배치된 모든 리소스 정리](https://oracle-livelabs.github.io/common/images/console/developer-resmgr-stacks.png "마켓플레이스 배포 제거")

2.  2단계에서 사용된 구획 및 이름을 선택합니다. 아래 예제에서는 sandbox라는 구획과 Oracle Spatial Studio라는 Stack이 사용되었습니다.

![적절한 구획을 선택하고 삭제할 스택을 선택합니다.](images/env-marketplace-20.png "스택 선택")

3.  Terraform 작업 > 삭제 선택

![Oracle Spatial Studio 스택을 통해 배포된 모든 리소스를 삭제합니다.](images/env-marketplace-21.png "배치된 리소스를 삭제합니다.")

확인 메시지가 표시됩니다. 그러면 마켓플레이스 배포에서 생성된 컴퓨트 및 네트워크 아티팩트가 제거됩니다.

4.  Spatial Studio 앱을 제거한 후 저장소 스키마가 그대로 유지됩니다. 저장소 스키마를 제거하려면 연습 3에서 수행한 대로 **admin**으로 데이터베이스에 연결하고 다음을 실행합니다.

    <copy>DROP USER studio_repo CASCADE;</copy>
    

## 자세히 알아보기

*   [Spatial Studio 제품 페이지](https://www.oracle.com/database/spatial/#rc30p2)
*   [Spatial Studio 시작하기](https://www.oracle.com/database/technologies/spatial-studio/get-started.html)

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 기한/일자** - David Lapp, 데이터베이스 제품 관리, 2023년 3월