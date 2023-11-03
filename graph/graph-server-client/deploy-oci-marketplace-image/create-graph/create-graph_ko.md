# 그래프 생성

## 소개

이제 테이블이 생성되어 데이터로 채워집니다. 이에 대한 그래프 표현을 작성해 보겠습니다.

예상 시간: 5분

### 목표

관계형 데이터 소스에서 그래프를 생성하는 방법을 알아봅니다.

*   Graph Server에 접속하는 클라이언트(Python 셸) 시작
*   PGQL DDL(데이터 정의어)(예: CREATE PROPERTY GRAPH)을 사용하여 그래프 인스턴스화

### 필요 조건

*   이 실습에서는 테이블 생성 및 채우기 실습을 성공적으로 완료했다고 가정합니다.

## 작업 1: Python 클라이언트 시작

이전에 생성한 전용 키를 사용하여 SSH를 통해 **opc** 사용자로 컴퓨트 인스턴스에 접속합니다.

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

예:

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

서버에 연결하는 Python 클라이언트 셸 인스턴스를 시작합니다.

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

클라이언트 셸이 성공적으로 시작되면 다음이 표시됩니다.

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## 작업 2: 그래프 생성

기존 테이블에서 그래프를 생성하는 create property graph 문을 설정합니다.

    <copy>
    statement = '''
    CREATE PROPERTY GRAPH "customer_360"
      VERTEX TABLES (
        customer
      , account
      , merchant
      )
      EDGE TABLES (
        account
          SOURCE KEY(id) REFERENCES account (id)
          DESTINATION KEY(customer_id) REFERENCES customer (id)
          LABEL owned_by PROPERTIES (id)
      , parent_of
          SOURCE KEY(customer_id_parent) REFERENCES customer (id)
          DESTINATION KEY(customer_id_child) REFERENCES customer (id)
      , purchased
          SOURCE KEY(account_id) REFERENCES account (id)
          DESTINATION KEY(merchant_id) REFERENCES merchant (id)
      , transfer
          SOURCE KEY(account_id_from) REFERENCES account (id)
          DESTINATION KEY(account_id_to) REFERENCES account (id)
      ) 
    '''
    </copy>
    

DDL 구문에 대한 자세한 내용은 [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph)를 참조하십시오. _입력 테이블의 모든 열은 [기본적으로](https://pgql-lang.org/spec/1.4/#properties)_ 정점/에지의 속성에 매핑됩니다. **owned\_by** 에지의 경우 에지 ID 생성을 위해 **id** 등록 정보와 **PROPERTIES** 키워드만 제공되며, 다른 등록 정보는 이미 계정 정점에 의해 보류되므로 제공되지 않습니다.

이제 PGQL DDL을 실행하여 그래프를 생성합니다.

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## 작업 3: 새로 생성된 그래프 확인

그래프가 생성되었는지 확인합니다. 다음 명령문을 복사하여 붙여넣고 Python 셸에서 실행합니다.

그래프를 연결합니다.

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

그래프가 생성되었는지 확인합니다.

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

일부 PGQL 질의를 실행합니다. 예: 정점 레이블 목록:

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(v) FROM MATCH (v)
    """).print()
    </copy>
    
    +----------+
    | LABEL(v) |
    +----------+
    | ACCOUNT  |
    | CUSTOMER |
    | MERCHANT |
    +----------+
    

각 레이블의 정점 수:

    <copy>
    graph.query_pgql("""
      SELECT COUNT(v), LABEL(v) FROM MATCH (v) GROUP BY LABEL(v)
    """).print()
    </copy>
    
    +---------------------+
    | COUNT(v) | LABEL(v) |
    +---------------------+
    | 5        | MERCHANT |
    | 6        | ACCOUNT  |
    | 4        | CUSTOMER |
    +---------------------+
    

모서리 레이블 목록:

    <copy>
    graph.query_pgql("""
      SELECT DISTINCT LABEL(e) FROM MATCH ()-[e]->()
    """).print()
    </copy>
    
    +-----------+
    | LABEL(e)  |
    +-----------+
    | OWNED_BY  |
    | PARENT_OF |
    | PURCHASED |
    | TRANSFER  |
    +-----------+
    

각 레이블의 가장자리 수:

    <copy>
    graph.query_pgql("""
      SELECT COUNT(e), LABEL(e) FROM MATCH ()-[e]->() GROUP BY LABEL(e)
    """).print()
    </copy>
    
    +----------------------+
    | COUNT(e) | LABEL(e)  |
    +----------------------+
    | 4        | OWNED_BY  |
    | 8        | TRANSFER  |
    | 1        | PARENT_OF |
    | 11       | PURCHASED |
    +----------------------+
    

## 작업 4: 그래프 게시

새로 생성된 그래프는 기본적으로 "전용"이며 현재 세션에서만 액세스할 수 있습니다. 나중에 새 세션에서 그래프에 액세스하려면 그래프를 "게시"할 수 있습니다.

그런 다음 위의 절차에 따라 그래프를 다시 만든 다음 게시합니다.

    <copy>
    graph.publish()
    </copy>
    

다음에 연결할 때 로그인 사이에 그래프 서버가 종료되거나 다시 시작되지 않은 경우 메모리를 다시 로드하지 않고 메모리에 보관된 그래프에 액세스할 수 있습니다.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

사용자가 생성될 때 **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** 롤이 부여되었으므로 그래프를 게시할 수 있습니다. 그렇지 않으면 **ADMIN** 사용자가 권한을 부여하고 업데이트된 권한을 선택하려면 Python 셸에 다시 연결해야 합니다.

이제 다음 실습을 진행할 수 있습니다.

## 확인

*   **작성자** - Jayant Sharma
*   **기여자** - Arabella Yao, Jenny Tsai
*   **최종 업데이트 수행자/날짜** - Ryota Yamanaka, 2023년 3월