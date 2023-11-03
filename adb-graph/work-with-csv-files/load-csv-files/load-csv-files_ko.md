# Graph Studio: CSV 파일에서 테이블로 데이터 로드

## 소개

이 실습에서는 Oracle Autonomous Data Warehouse 또는 Oracle Autonomous Transaction Processing 인스턴스의 Database Actions 인터페이스를 사용하여 두 개의 CSV 파일을 해당 테이블로 로드합니다.

예상 시간: 10분

실습 과정을 빠르게 살펴보려면 아래 비디오를 시청하십시오.

[](youtube:wkKKO-RO0lA)

### 목표

방법 알아보기

*   Database Actions를 사용하여 Autonomous Database로 CSV 파일 로드

### 필요 조건

*   다음 실습에서는 Oracle Autonomous Database 계정이 필요합니다.
*   여기에서는 그래프 및 웹 액세스가 사용으로 설정된 사용자가 있다고 가정합니다. 즉, 올바른 롤과 권한을 가진 데이터베이스 유저가 존재하며 해당 유저는 Database Actions에 로그인할 수 있습니다.

## 작업 1: Autonomous Database 인스턴스의 Database Actions에 연결

1.  Oracle Cloud 콘솔에서 Autonomous Database 인스턴스에 대한 서비스 세부정보 페이지를 엽니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](images/open-database-actions.png " ")
    
2.  **데이터베이스 작업**을 눌러 엽니다.
    

## 작업 2: 그래프 사용 유저로 로그인

1.  Autonomous Database 인스턴스에 대한 그래프 사용자(예: `GRAPHUSER`)로 로그인합니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-graphuser-login.png " ")
    
    > **주:** _필요한 경우 다음을 수행하여 올바른 롤 및 권한을 가진 사용자를 생성합니다._
    
    *   Autonomous Database의 **ADMIN** 사용자로 Database Actions에 로그인합니다.
    *   탐색 메뉴에서 **관리**, **데이터베이스 사용자** 순으로 선택합니다.
    *   **Create User**를 누릅니다.
    *   **웹 액세스** 및 **그래프** 단추를 설정합니다.

## 작업 3: ObjectStore에서 샘플 데이터 세트를 다운로드합니다.

1.  브라우저에 zip 아카이브(즉,
    
        <copy>
        https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
    
    또는 `wget` 또는 `curl`를 사용하여 샘플 데이터를 컴퓨터에 다운로드합니다.  
    복사하여 붙여넣을 수 있는 `curl` 요청의 예는 다음과 같습니다.
    
        <copy>
        curl -G -o acct-txn-data.zip https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/random-acct-txn-data.zip
        </copy>
        
2.  아카이브를 ~/downloads와 같은 로컬 디렉토리에 **압축 해제**합니다.
    

## 태스크 4: 데이터베이스 작업 데이터 로드를 사용하여 업로드

1.  **DATA LOAD** 카드를 누릅니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](images/db-actions-dataload-card.png " ")
    
    그런 다음 데이터 위치를 지정합니다. 즉, **LOAD DATA** 및 **LOCAL FILE** 카드에 선택 표시가 있는지 확인합니다. **다음**을 누릅니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-dataload-location.png)
    
2.  **파일 선택**을 누릅니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](images/db-action-dataload-file-browser.png " ")
    
    올바른 폴더(예: ~/downloads/random-acct-data)로 이동하고 `bank_accounts.csv` 및 `bank_txns.csv` 파일을 선택합니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-dataload-choose-files.png " ")
    
3.  올바른 파일이 선택되었는지 확인한 다음 **Run** 아이콘을 누릅니다. ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-dataload-click-run.png " ")
    
4.  데이터 로드 작업을 원하는지 확인합니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-dataload-confirm-run.png " ")
    
5.  파일이 로드되면
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/dbactions-dataload-files-loaded.png " ")
    
    **완료**를 눌러 종료합니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](images/dbactions-click-done.png " ")
    
6.  이제 **SQL** 워크시트를 엽니다. ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-choose-sql-card.png " ")
    
7.  올바른 폴더(예: ~/downloads)로 이동하여 `fixup.sql` 파일을 선택하고 SQL Worksheet로 끌어옵니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-drag-drop-fixup-sql.png " ")
    
    그러나 copy-n-paste를 선호하는 경우 `fixup.sql`의 내용은 다음과 같습니다.
    
        <copy>
        alter table bank_accounts add primary key (acct_id);
        
        alter table bank_txns add txn_id number;
        update bank_txns set txn_id = rownum;
        commit;
        
        alter table bank_txns add primary key (txn_id);
        alter table bank_txns modify from_acct_id references bank_accounts (acct_id);
        alter table bank_txns modify to_acct_id references bank_accounts (acct_id);
        
        desc bank_txns;
        
        select * from USER_CONS_COLUMNS where table_name in ('BANK_ACCOUNTS', 'BANK_TXNS');
        </copy>      
        
    
    여기에서는 다음을 제공합니다.
    
    *   `bank_accounts` 테이블에 기본 키 제약 조건을 추가합니다.
    *   `bank_txns` 테이블에 열(`txn_id`)을 추가합니다.
    *   `txn_id`에 대한 값을 설정하고 트랜잭션을 커밋합니다.
    *   `bank_txns` 테이블에 기본 키 제약 조건을 추가합니다.
    *   `from_acct_id`가 `bank_accounts.acct_id`를 참조하도록 지정하는 외래 키 제약 조건을 `bank_txns` 테이블에 추가합니다.
    *   `to_acct_id`가 `bank_accounts.acct_id`를 참조하도록 지정하는 두번째 외래 키 제약 조건을 `bank_txns` 테이블에 추가합니다.
    *   `txn_id` 열 및 제약 조건이 추가되었는지 확인하는 데 도움이 됩니다.
8.  SQL Worksheet에서 `fixup.sql` 스크립트를 실행합니다.  
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-sql-execute-fixup.png " ")
    
9.  스크립트 출력은 다음과 같아야 합니다.
    
    ![이 이미지에는 ALT 텍스트를 사용할 수 없습니다.](./images/db-actions-sql-script-output.png " ")
    
    이러한 테이블에서 그래프를 생성하려면 **다음 실습으로 이동**하십시오.
    

## 확인

*   **작성자** - Jayant Sharma, 제품 관리
*   **제공자** - Jayant Sharma, 제품 관리
*   **최종 업데이트 기한/일자** - Jayant Sharma, 제품 관리, 2022년 2월