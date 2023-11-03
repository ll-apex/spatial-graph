# 정리

## 소개

Autonomous Database를 사전 워크샵 상태로 재설정하여 워크샵 환경을 정리할 수 있습니다.

예상 실험 시간: 2분

### 목표

*   Autonomous Database를 프리워크샵 상태로 재설정

### 필요 조건

*   활성 Autonomous Database 인스턴스

## 작업 1: Autonomous Database를 워크샵 이전 상태로 재설정

1.  다음을 실행하여 이 워크샵에서 생성된 모든 데이터베이스 아티팩트를 제거합니다.
    
        <copy>
        import oracledb
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        cursor.execute("drop table transactions")
        cursor.execute("drop table locations")
        cursor.execute("drop table transaction_labels")
        cursor.execute("drop function lonlat_to_proj_geom")
        cursor.execute("delete from user_sdo_geom_metadata")
        connection.commit()
        </copy>
        

## 확인

*   **작성자** - David Lapp, Oracle 데이터베이스 제품 관리
*   **최종 업데이트 수행자/날짜** - David Lapp, 2023년 8월