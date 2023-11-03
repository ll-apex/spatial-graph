# Spatial Studio 저장소에 대한 데이터베이스 사용자

## 소개

이 실습에서는 Spatial Studio의 메타데이터 저장소에 사용할 데이터베이스 스키마를 생성해 봅니다. 이 스키마는 데이터 집합, 분석 및 프로젝트의 정의와 같이 Spatial Studio에서 수행하는 작업을 저장할 스키마입니다.

Spatial Studio 저장소의 데이터베이스 스키마는 기술적으로 모든 이름을 가질 수 있습니다. 다른 Spatial Studio 워크샵과의 일관성을 위해 사용자 이름 **studio\_repo**을 지정합니다. 이 이름은 데이터베이스 사용자 이름이며 Spatial Studio 앱 자체를 설치할 때 생성된 기본 Spatial Studio 관리자 사용자 이름(studio\_admin)과 같은 Spatial Studio 애플리케이션 사용자 이름과 구분됩니다.

예상 실험 시간: 5분

### 목표

*   Spatial Studio 메타데이터 저장소에 대한 스키마를 생성하는 방법 알아보기
*   데이터베이스 접속용 전자 지갑 다운로드 방법 알아보기

### 필요 조건

*   Oracle Free Tier, 상시 무료, 유료 또는 LiveLabs 클라우드 계정
*   데이터베이스 SQL Developer Web에 액세스합니다.

## 작업 1: 저장소 스키마 생성

1.  SQL Developer Web에서 **admin** 사용자로 Spatial Studio 저장소에 사용할 자율운영 데이터베이스에 접속합니다.
    
2.  Spatial Studio 저장소에 대한 스키마를 생성합니다. 스키마는 이름을 가질 수 있지만 다른 실습과의 일관성을 위해 **studio\_repo**이라는 이름을 사용합니다. Oracle Autonomous Database의 비밀번호 요구 사항은 [여기](https://docs.oracle.com/en/cloud/paas/autonomous-database/adbsa/manage-users-create.html#GUID-72DFAF2A-C4C3-4FAC-A75B-846CC6EDBA3F)에서 확인할 수 있습니다. 선택한 비밀번호를 기록해 둡니다. 이후 단계에서 사용할 것입니다.
    
        <copy>CREATE USER studio_repo
        IDENTIFIED BY <password goes here>;</copy>
        

## 작업 2: 테이블스페이스 할당량 지정

1.  기본 테이블스페이스를 Spatial Studio 저장소 스키마에 지정합니다. Autonomous Database를 사용하면 테이블스페이스 이름 **data**를 사용할 수 있습니다.
    
        <copy>ALTER USER studio_repo
        DEFAULT TABLESPACE data;</copy>
        
2.  Spatial Studio 저장소 스키마에 테이블스페이스 할당량을 지정합니다. Spatial Studio의 메타데이터는 매우 적은 양의 스토리지를 차지합니다. 따라서 할당량은 주로 저장소 스키마에 저장된 업무 데이터를 수용합니다. 이 연습에서는 할당량 값 **250M**을 사용합니다. 다른 데이터 세트를 실험할 경우 값을 **unlimited**로 설정할 수도 있습니다.
    
        <copy>ALTER USER studio_repo
        QUOTA <quota value> ON data;</copy>
        

## 작업 3: 권한 부여

1.  Spatial Studio 저장소 스키마 사용자에게 다음 권한을 부여합니다.
    
        <copy>
        GRANT CONNECT,
              CREATE SESSION,
              CREATE TABLE,
              CREATE VIEW,
              CREATE SEQUENCE,
              CREATE PROCEDURE,
              CREATE SYNONYM,
              CREATE TYPE,
              CREATE TRIGGER
        TO  studio_repo
        </copy>
        

이제 studio\_repo 스키마를 Spatial Studio 저장소로 사용할 준비가 되었습니다.

## 작업 4: 전자 지갑 다운로드

생성한 Autonomous Database 저장소 스키마에 접속하려면 Spatial Studio에 전자 지갑이 필요합니다. 우리는 다음 실험실에서 지갑을 사용할 것입니다.

1.  Autonomous Database로 이동하여 View Details를 선택합니다.
    
    ![이미지 대체 텍스트](images/repo-schema-1.png "이미지 제목")
    
2.  DB 접속 탭을 선택합니다.
    
    ![이미지 대체 텍스트](images/repo-schema-2.png "이미지 제목")
    
3.  전자 지갑 다운로드를 누릅니다. ![이미지 대체 텍스트](images/repo-schema-3.png "이미지 제목")
    
    Wallet 파일의 비밀번호를 입력하라는 메시지가 표시됩니다. 전자 지갑은 단일 zip 파일입니다.
    
4.  편리한 위치에 전자 지갑 파일을 저장합니다. 다음 랩에서 이 파일이 필요합니다.
    

이제 [다음 실습을 진행하십시오](#next).

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 기한/일자** - David Lapp, 데이터베이스 제품 관리, 2023년 3월