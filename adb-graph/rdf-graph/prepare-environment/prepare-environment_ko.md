# 환경 준비

## 소개

Oracle Autonomous Transaction Processing(ATP)은 OCI(Oracle Cloud Infrastructure)에서 "자율 구동" 기능을 제공하는 완전 관리형 Oracle 데이터베이스 서비스입니다. Graph Studio 사용 권한이 있는 사용자를 생성하는 것이 가장 좋습니다.

다음 랩 가이드는 ATP를 프로비저닝하고 Graph Studio에 대한 권한이 있는 사용자를 생성하는 방법을 보여줍니다.

예상 시간: 15분

### 목표

*   Oracle Cloud상에서 Autonomous Database를 생성합니다.

### 필요 조건

*   웹 브라우저
*   항상 올바른 지역 및 구획에 있는지 확인하십시오.

## **작업 1:** Oracle Cloud에 로그인

1.  브라우저에서 Oracle Cloud에 로그인합니다.

## **태스크 2:** ATP 프로비저닝

아래 단계를 사용하여 Autonomous Transaction Processing 데이터베이스(ATP)를 프로비저닝합니다. 또는 ADW(Autonomous Data Warehouse)도 이와 유사하게 사용할 수 있습니다.

1.  OCI 콘솔의 오른쪽 위에서 지정된 리전을 선택합니다.
    
2.  왼쪽 상단의 햄버거 메뉴에서 Oracle Database, Autonomous Transaction Processing을 차례로 선택합니다.
    

![메뉴에서 Autonomous Transaction Processing에 액세스하도록 선택할 위치를 보여주는 이미지](./images/atp.png)

3.  Create Autonomous Database를 누릅니다.

![자율운영 데이터베이스 생성 단추를 보여주는 이미지](./images/create-adb.png)

4.  구획 선택.
    
5.  표시 및 데이터베이스 이름에 고유한 이름(이름일 수 있음)을 입력합니다. 표시 이름은 콘솔 UI에서 데이터베이스를 식별하는 데 사용됩니다.
    

![데이터베이스의 고유한 이름을 입력할 위치를 보여주는 이미지](./images/unique-name.png)

6.  트랜잭션 처리 작업 로드 유형이 선택되었는지 확인하십시오.
    
7.  비밀번호를 입력합니다. 사용자 이름은 항상 ADMIN입니다. (참고: 비밀번호를 기억하십시오.)
    

![비밀번호 선언 위치를 보여주는 이미지](./images/password.png)

8.  하단에 있는 Create Autonomous Database를 누릅니다.
    
    콘솔에 ATP가 프로비저닝 중임을 표시합니다. 이 작업을 완료하는 데 2~3분 정도 걸립니다.
    
    작업 요청에서 프로비전 상태를 확인할 수 있습니다.
    

![프로비전된 데이터베이스의 상태를 확인할 위치를 보여주는 이미지입니다.](./images/status.png)

이 연습을 마칩니다. _이제 다음 실습을 진행할 수 있습니다._

## 확인

*   **작성자** - Nicholas Cusato(Santa Monica Specialist Hub)
*   **기여자** - Nicholas Cusato(Santa Monica Specialist Hub)
*   **최종 업데이트 수행자/날짜** - Nicholas Cusato, 2022년 2월