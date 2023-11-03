# Spatial Studio 액세스

## 소개

이 실습에서는 Oracle LiveLabs 예약에서 Oracle Spatial Studio(Spatial Studio)에 액세스하는 프로세스를 안내합니다. 환경에는 Spatial Studio 및 Autonomous Database가 포함됩니다. Spatial Studio에 처음 로그인하면 Autonomous Database에 대한 연결 정보가 제공됩니다.

예상 실험 시간: 10분

### 목표

이 실습에서는 다음을 수행합니다.

*   Autonomous Database용 Cloud Wallet 다운로드
*   Autonomous Database 연결 정보를 제공하는 Spatial Studio에 최초 로그인 수행

### 필요 조건

*   "Oracle Spatial Studio 소개"에 대한 LiveLabs 예약 완료

## 작업 1: Autonomous Database용 클라우드 전자 지갑 다운로드

1.  워크샵 세부 정보에서 클라우드 사용자 이름, 비밀번호, 구획 및 Spatial Studio IP 주소를 기록해 둡니다. 그런 다음 클라우드 콘솔을 실행합니다.

![이미지 대체 텍스트](images/1-1.png "이미지 제목")

2.  클라우드 사용자 이름과 초기 비밀번호를 사용하여 **Oracle Cloud Infrastructure Direct Sign-in**을 사용하여 사인인합니다. 기본 암호를 변경하라는 메시지가 표시됩니다.

![이미지 대체 텍스트](images/1-2.png "이미지 제목")

3.  **Oracle Database**, **Autonomous Database** 순으로 이동합니다.

![이미지 대체 텍스트](images/1-3.png "이미지 제목")

4.  왼쪽의 Compartment 양식에 앞에서 설명한 Compartment 이름 입력을 시작합니다. 그러면 구획 목록이 동적으로 필터링됩니다. 나열된 컴파트먼트를 선택합니다. 그러면 Autonomous Database가 나열됩니다. Autonomous Database 링크를 클릭합니다.

![이미지 대체 텍스트](images/1-4.png "이미지 제목")

5.  **데이터베이스 접속**, **전자 지갑 다운로드** 순으로 누릅니다. 전자 지갑 암호를 입력하라는 메시지가 표시됩니다. 이 비밀번호는 사용되지 않으므로 문자열을 입력하십시오. 다음 단계에서 사용할 수 있도록 전자 지갑을 랩탑의 편리한 위치에 저장합니다.

![이미지 대체 텍스트](images/1-5.png "이미지 제목")

## 작업 2: Spatial Studio 최초 로그인

1.  이제 앞에서 언급한 Spatial Studio IP 주소를 사용합니다. 브라우저에서 새 탭을 열고 **https://\[your Spatial Studio IP address\]:4040/spatialstudio**로 이동합니다. 예를 들어, Spatial Studio IP 주소가 123.123.12.123인 경우 https://123.123.12.123:4040/spatialstudio.로 이동합니다. Spatial Studio 인스턴스가 서명된 SSL 인증서로 구성되지 않았으므로 브라우저별 보안 경고가 표시됩니다. 경고를 받아들이고 사이트로 진행합니다. 운용 환경에서는 인증서가 구성되고 이 문제가 발생하지 않습니다. 사용자 **admin** 및 암호 **welcome1**로 로그인합니다.

![이미지 대체 텍스트](images/2-1.png "이미지 제목")

2.  Spatial Studio에 처음 로그인하면 Spatial Studio의 메타데이터 저장소에 대한 데이터베이스 연결 정보를 입력하라는 메시지가 표시됩니다. **Autonomous Database**, **다음** 순으로 누릅니다. 다음 화면에서 이전에 다운로드한 전자 지갑 파일을 끌어 놓고 **확인**을 누릅니다.

![이미지 대체 텍스트](images/2-2.png "이미지 제목")

3.  이제 Automomous Database 연결 정보를 묻는 메시지가 표시됩니다. 사용자 **studio\_repo**, 암호 **Welcome1Welcome1**를 입력하고 중간 서비스 레벨을 선택합니다.

![이미지 대체 텍스트](images/2-3.png "이미지 제목")

Spatial Studio는 이제 Autonomous Database에서 메타데이터 테이블을 구축하고 있습니다. 이 작업은 약 30초 정도 걸립니다.

4.  Spatial Studio가 열리면 처음 로그인이 완료되고 워크샵을 진행할 준비가 됩니다.

![이미지 대체 텍스트](images/2-4.png "이미지 제목")

이제 [다음 실습을 진행하십시오](#next).

## 자세히 알아보기

*   [Spatial Studio 제품 페이지](https://oracle.com/goto/spatialstudio)

## 확인

*   **작성자** - 데이터베이스 제품 관리, David Lapp
*   **최종 업데이트 기한/일자** - David Lapp, 데이터베이스 제품 관리, 2021년 6월