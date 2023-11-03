/\* 다음 릴리스에서 이 파일을 삭제하십시오. ADB-PROVISION-CONDITIONAL.MD 파일을 사용하여 원하는 버전을 지정하십시오. { "title": "Lab 1: Provision an ADB Instance", "description": "Provisioning an Autonomous Database Instance", "type": "livelabs", "filename": "https://oracle-livelabs.github.io/adb/shared/adb-provision/adb-provision-conditional.md" }, \*/

# Autonomous Database(ADW 및 ATP) 프로비저닝

## 소개

이 실습에서는 Oracle Cloud에서 Oracle Autonomous Database(Autonomous Data Warehouse \[ADW\] 및 Autonomous Transaction Processing \[ATP\]) 사용을 시작하는 단계를 안내합니다. 이 실습에서는 새 ADW instance를 프로비저닝(Provisioning)합니다.

> **주:** 이 연습에서는 ADW를 사용하지만 단계는 ATP 데이터베이스를 생성하는 것과 동일합니다.

예상 시간: 5분

### 목표

*   새로운 Autonomous Database를 프로비저닝하는 방법 알아보기

## 작업 1: 서비스 메뉴에서 ADW 또는 ATP 선택

1.  Oracle Cloud에 로그인합니다.
    
2.  로그인하면 사용 가능한 모든 서비스를 볼 수 있는 클라우드 서비스 대시보드로 이동합니다. 왼쪽 위에 있는 탐색 메뉴를 눌러 최상위 레벨 탐색 선택을 표시합니다.
    
    > **참고:** 대시보드의 **빠른 작업** 섹션에서 Autonomous Data Warehouse 또는 Autonomous Transaction Processing 서비스에 직접 액세스할 수도 있습니다.
    
    ![Oracle 홈 페이지](./images/Picture100-36.png " ")
    
3.  다음 단계는 Autonomous Data Warehouse 또는 Autonomous Transaction Processing과 유사하게 적용됩니다. 이 실습에서는 Autonomous Data Warehouse 데이터베이스의 프로비저닝을 보여 주므로 **Autonomous Data Warehouse**를 클릭하십시오.
    
    ![Autonomous Data Warehouse를 누릅니다.](https://oracle-livelabs.github.io/common/images/console/database-adw.png " ")
    
4.  Autonomous Data Warehouse 인스턴스를 보려면 작업 로드 유형이 **Data Warehouse** 또는 **모두**인지 확인하십시오. **목록 범위** 드롭다운 메뉴를 사용하여 구획을 선택합니다. 구획을 빠르게 찾으려면 사용자 이름의 첫 부분(예: Search Compartments 필드에 `LL185`)을 입력합니다.
    
    ![왼쪽의 작업 로드 유형을 확인합니다.](images/livelabs-compartment.png " ")
    
5.  이 콘솔은 아직 데이터베이스가 없음을 보여줍니다. 긴 데이터베이스 목록이 있는 경우 데이터베이스의 **상태**(사용 가능, 정지됨, 종료됨 등)를 기준으로 목록을 필터링할 수 있습니다. **작업 로드 유형**별로 정렬할 수도 있습니다. 여기서 **데이터 웨어하우스** 작업 로드 유형이 선택됩니다.
    
    ![독립 데이터베이스 콘솔입니다.](./images/Compartment.png " ")
    

## 작업 2: ADB instance 생성

1.  **Autonomous Database 생성**을 눌러 인스턴스 생성 프로세스를 시작합니다.
    
    ![Create Autonomous Database를 누릅니다.](./images/Picture100-23.png " ")
    
2.  그러면 인스턴스 구성을 지정할 수 있는 **Autonomous Database 생성** 화면이 나타납니다.
    
    ![](./images/create-adb-screen-livelabs-default.png " ")
    
3.  Autonomous Database에 대한 기본 정보 제공:
    
    *   **구획 선택** - 기본 구획을 그대로 둡니다.
    *   **표시 이름** - 표시할 데이터베이스의 기억에 남는 이름을 입력합니다. 이 실습에서는 **ADW Finance Mart**를 사용합니다.
    *   **데이터베이스 이름** - 문자와 숫자만 사용하고 문자로 시작합니다. 최대 길이는 14자입니다. (처음에는 밑줄이 지원되지 않음) 이 실습의 경우 **ADWFINANCE**를 사용하고 **사용자 ID를 추가**하십시오. 예를 들어, 사용자 ID가 **LL-185**인 경우 **ADWFINANCE185를 입력합니다.**
    
    ![필수 세부정보를 입력하십시오.](./images/Picture100-26-livelabs.png " ")
    
4.  작업 로드 유형을 선택하십시오. 다음 중에서 데이터베이스의 작업 로드 유형을 선택합니다.
    
    *   **데이터 웨어하우스** - 이 실습에서는 작업 로드 유형으로 **데이터 웨어하우스**를 선택합니다.
    *   **트랜잭션 처리** - 또는 트랜잭션 처리를 작업 로드 유형으로 선택할 수 있습니다.
    
    ![작업 로드 유형 선택](./images/Picture100-26b.png " ")
    
5.  배치 유형을 선택합니다. 다음 중에서 데이터베이스의 배치 유형을 선택합니다.
    
    *   **공유 기반 구조** - 이 실습에서는 **공유 기반 구조**를 배치 유형으로 선택합니다.
    *   **전용 인프라** - 또는 전용 인프라를 배치 유형으로 선택할 수 있습니다.
    
    ![배치 유형을 선택하십시오.](./images/Picture100-26_deployment_type.png " ")
    
6.  데이터베이스를 구성합니다.
    
    *   **항상 무료** - 클라우드 계정이 항상 무료 계정인 경우 이 옵션을 선택하여 항상 무료 자율운영 데이터베이스를 생성할 수 있습니다. 항상 무료 데이터베이스는 CPU 1개와 20GB의 스토리지를 제공합니다. 이 실습에서는 항상 무료를 선택하지 않은 상태로 두는 것이 좋습니다.
    *   **Choose database version(데이터베이스 버전 선택)** - 사용 가능한 버전에서 데이터베이스 버전을 선택합니다.
    *   **OCPU 개수** - 서비스에 대한 CPU 수입니다. 이 실습에서는 **1 CPU**를 지정합니다. 상시 무료 데이터베이스를 선택하면 CPU 1개가 제공됩니다.
    *   **스토리지(TB)** - 스토리지 용량을 테라바이트 단위로 선택합니다. 이 실습에서는 스토리지를 **1TB**로 지정합니다. 또는 상시 무료 데이터베이스를 선택하면 20GB의 스토리지가 제공됩니다.
    *   **자동 스케일링** - 이 실습에서는 시스템이 자동으로 최대 3배 더 많은 CPU 및 IO 리소스를 사용하여 작업 로드 요구를 충족할 수 있도록 자동 스케일링을 사용으로 설정합니다.
    *   **새 데이터베이스 미리보기** - 새 데이터베이스 버전을 미리 볼 수 있는 체크박스가 있는 경우 선택하지 마십시오.
    
    > **주:** 항상 무료 자율운영 데이터베이스는 스케일 업/다운할 수 없습니다.
    
    ![나머지 매개변수를 선택합니다.](./images/Picture100-26c.png " ")
    
7.  관리자 인증서 생성:
    
    *   **비밀번호 및 비밀번호 확인** - 서비스 인스턴스의 ADMIN 사용자에 대한 비밀번호를 지정합니다. 비밀번호가 다음 요구사항을 충족해야 합니다.
    *   비밀번호는 12자에서 30자 사이여야 하며 대문자, 소문자 및 숫자를 하나 이상 포함해야 합니다.
    *   비밀번호에 사용자 이름을 포함할 수 없습니다.
    *   비밀번호에 대문자를 포함할 수 없습니다.
    *   비밀번호는 마지막으로 사용된 4개의 비밀번호와 달라야 합니다.
    *   비밀번호는 24시간 전에 설정된 것과 동일한 비밀번호가 아니어야 합니다.
    *   확인을 위해 비밀번호를 다시 입력합니다. 이 비밀번호를 기록해 둡니다.
    
    ![비밀번호와 확인을 입력하십시오.](./images/Picture100-26d.png " ")
    
8.  네트워크 액세스 선택:
    
    *   이 연습에서는 기본값인 "Secure access from everywhere"를 적용합니다.
    *   지정한 IP 주소 및 VCN의 트래픽만 허용하려는 경우(모든 공용 IP 또는 VCN의 데이터베이스에 대한 액세스가 차단되는 경우) Choose network(네트워크 선택) 액세스 영역에서 "Secure access from allowed IPs and VCNs only(허용되는 IP 및 VCN에서만 보안 액세스)"를 선택합니다.
    *   OCI VCN 내 전용 끝점으로 액세스를 제한하려면 네트워크 선택 액세스 영역에서 "전용 끝점 액세스만"을 선택합니다.
    *   "mTLS(상호 TLS) 인증 필요" 옵션이 선택된 경우 Autonomous Database에 대한 접속을 인증하려면 mTLS가 필요합니다. JDK8 이상의 JDBC Thin 드라이버를 사용하는 경우 TLS 접속을 통해 전자 지갑 없이 Autonomous Database에 접속할 수 있습니다. TLS를 허용하거나 mTLS(상호 TLS) 인증만 요구하는 옵션은 [documentation for network options](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/support-tls-mtls-authentication.html#GUID-3F3F1FA4-DD7D-4211-A1D3-A74ED35C0AF5)을 참조하십시오.
    
    ![네트워크 액세스를 선택합니다.](./images/Picture100-26e.png " ")
    
9.  라이센스 유형을 선택하십시오. 이 실습에서는 **BYOL(Bring Your Own License)**을 선택합니다. 두 가지 라이센스 유형은 다음과 같습니다.
    
    *   **BYOL(Bring Your Own License)** - 조직에 기존 데이터베이스 라이센스가 있는 경우 이 유형을 선택합니다.
    *   **라이센스 포함됨** - 새 데이터베이스 소프트웨어 라이센스 및 데이터베이스 클라우드 서비스를 구독하려는 경우 이 유형을 선택합니다.
    
    ![Create Autonomous Database를 누릅니다.](./images/Picture100-27-byol.png " ")
    
10.  이 실습에서는 연락처 전자 메일 주소를 제공하지 않습니다. "연락처 전자메일" 필드를 사용하면 계획되지 않은 유지보수 통지뿐만 아니라 운영 통지 및 공고를 수신할 연락처를 나열할 수 있습니다.
    
    ![담당자 전자메일 주소를 제공하지 마십시오.](images/contact-email-field.png)
    
11.  **Create Autonomous Database**를 누릅니다.
    
12.  인스턴스 프로비전이 시작됩니다. 몇 분 안에 상태가 프로비저닝에서 사용 가능으로 바뀝니다. 이제 Autonomous Data Warehouse 데이터베이스를 사용할 준비가 되었습니다! 여기서 instance의 이름, 데이터베이스 버전, OCPU 개수, 저장 영역 크기를 포함한 instance의 세부 정보를 살펴봅니다.
    

    ![Database instance homepage.](./images/Picture100-32.png " ")
    

_다음 실습을 진행하십시오_.

## 자세히 알아보겠습니까?

Autonomous Data Warehouse를 사용하는 일반적인 워크플로우에 대한 설명서를 보려면 [여기](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/autonomous-workflow.html#GUID-5780368D-6D40-475C-8DEB-DBA14BA675C3)를 클릭하십시오.

## 확인

*   **작성자** - ADB 제품 관리, Nilay Panchal
*   **클라우드 도입** - Richard Green, 데이터베이스 사용자 지원 수석 개발자
*   **제공자** - Oracle LiveLabs QA 팀(Jeffrey Malcolm Jr, Intern | Arabella Yao, Product Manager Intern)
*   **최종 업데이트 수행자/날짜** - Richard Green, 2022년 2월