# 그래프 쿼리 및 분석

## 소개

이 예에서는 여러 데이터 세트를 통합하고 그래프를 사용하여 추가 분석을 수행하는 방법을 보여 주며 새로운 통찰력을 얻을 수 있습니다. 설명을 위해 세 개의 작은 데이터 세트를 사용합니다. 첫 번째는 계정 및 계정 소유자를 포함합니다. 두 번째는 해당 계좌를 소유한 사람들의 구매입니다. 세번째는 이러한 계정 간의 트랜잭션입니다.

결합된 데이터 집합은 패턴 일치, 주기 감지, 중요한 노드 찾기, 커뮤니티 감지 등 일반적인 그래프 질의 및 분석을 수행하는 데 사용됩니다.

다음 ER 다이어그램은 데이터 세트 간의 관계를 보여 줍니다.

![ER 다이어그램](images/er-diagram.jpg)

예상 실험 시간: 10분

### 목표

*   그래프를 query하고 분석하는 방법 학습

### 필요 조건

*   Python 클라이언트 작동 및 실행

## 작업 1: 메모리에 대한 그래프 가져오기

**customer\_360** 그래프가 이전 랩의 메모리에 이미 로드되었다고 가정하면 이 명령을 사용하여 그래프를 연결할 수 있습니다. 그래프가 게시되면 새 세션에서 그래프에 액세스할 수도 있습니다.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

이제 이 그래프를 query하여 이에 대한 몇 가지 분석을 실행할 수 있습니다.

## 작업 2: 패턴 일치

PGQL 쿼리는 특정 패턴을 감지하는 데 편리합니다.

같은 날 인바운드 및 아웃바운드 이전이 500개가 넘는 계정을 찾습니다. 이에 대한 PGQL 질의는 다음과 같습니다.

    <copy>
    graph.query_pgql("""
        SELECT a.account_no
             , a.balance
             , t1.amount AS t1_amount
             , t2.amount AS t2_amount
             , t1.transfer_date
        FROM MATCH (a)<-[t1:transfer]-(a1)
           , MATCH (a)-[t2:transfer]->(a2)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
    """).print()
    </copy>
    
    +---------------------------------------------------------------+
    | account_no  | balance | t1_amount | t2_amount | transfer_date |
    +---------------------------------------------------------------+
    | xxx-yyy-202 | 200.0   | 900.0     | 850.0     | 2018-10-06    |
    +---------------------------------------------------------------+
    

## 작업 3: 주기 감지

다음으로 PGQL을 사용하여 동일한 계정에서 시작 및 종료되는 일련의 이전(예: A-B-A 또는 A-B-C-A)을 찾습니다.

첫번째 query는 다음과 같이 표현될 수 있습니다.

    <copy>
    graph.query_pgql("""
        SELECT a1.account_no    AS a1_account
             , t1.transfer_date AS t1_date
             , t1.amount        AS t1_amount
             , a2.account_no    AS a2_account
             , t2.transfer_date AS t2_date
             , t2.amount        AS t2_amount
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
    """).print()
    </copy>
    
    +-----------------------------------------------------------------------------+
    | a1_account  | t1_date    | t1_amount | a2_account  | t2_date    | t2_amount |
    +-----------------------------------------------------------------------------+
    | xxx-yyy-201 | 2018-10-05 | 200.0     | xxx-yyy-202 | 2018-10-10 | 300.0     |
    +-----------------------------------------------------------------------------+
    

이 결과는 다음 섹션에서 표시됩니다.

![감지](images/detection.jpg)

두번째 query는 패턴(리스트)에 전송을 하나 더 추가하고 다음과 같이 표현할 수 있습니다.

    <copy>
    graph.query_pgql("""
        SELECT a1.account_no AS a1_account
             , t1.amount     AS t1_amount
             , a2.account_no AS a2_account
             , t2.amount     AS t2_amount
             , a3.account_no AS a3_account
             , t3.amount     AS t3_amount
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
    """).print()
    </copy>
    
    +-----------------------------------------------------------------------------+
    | a1_account  | t1_amount | a2_account  | t2_amount | a3_account  | t3_amount |
    +-----------------------------------------------------------------------------+
    | xxx-yyy-201 | 500.0     | xxx-yyy-203 | 450.0     | xxx-yyy-204 | 400.0     |
    +-----------------------------------------------------------------------------+
    

이 결과는 다음 섹션에서 표시됩니다.

![detection2](images/detection2.jpg)

## 태스크 4: 영향력 있는 고객사

네트워크에서 어떤 계정이 영향을 받는지 알아보겠습니다. 정점의 중요도와 중심성에 점수를 부여하는 다양한 알고리즘이 있습니다. 기본 제공 PageRank 알고리즘을 예로 사용하겠습니다.

1.  그래프에서 고객을 필터링합니다(참조). [필터 표현식](https://docs.oracle.com/cd/E56133_01/latest/prog-guides/filter.html))
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'"));
        graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  [PageRank 알고리즘](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/pagerank.html)을 실행합니다. PageRank 알고리즘은 각 정점에 숫자 가중치를 지정하여 그래프 내에서 상대적 중요성을 측정합니다.
    
        <copy>
        analyst.pagerank(graph2);
        </copy>
        
        VertexProperty(name: pagerank, type: double, graph: sub-graph_16)
        
3.  결과를 표시합니다.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.account_no, a.pagerank
            FROM MATCH (a)
            ORDER BY a.pagerank DESC
        """).print()
        </copy>
        
        +-------------------------------------+
        | a.account_no | a.pagerank           |
        +-------------------------------------+
        | xxx-yyy-201  | 0.18012007557258927  |
        | xxx-yyy-204  | 0.1412461615467829   |
        | xxx-yyy-203  | 0.1365633635065475   |
        | xxx-yyy-202  | 0.12293884324085073  |
        | xxx-zzz-212  | 0.05987452026569676  |
        | xxx-zzz-211  | 0.025000000000000005 |
        +-------------------------------------+
        

## 작업 5: 커뮤니티 감지

커뮤니티를 형성하는 계정의 하위 세트를 찾겠습니다. 즉, 동일한 하위 세트의 계정 간에 다른 하위 세트의 계정과 계정 간에 더 많은 이체가 있습니다. 약하게/강하게 연결된 기본 제공 구성요소 알고리즘을 사용합니다.

1.  첫번째 단계는 계정과 이들 간의 이전만 포함하는 하위 그래프를 생성하는 것입니다. 이 작업은 그래프에 모서리 필터(레이블이 "전송"인 모서리의 경우)를 만들고 적용하여 수행됩니다.
    
    그래프에서 고객을 필터링합니다.
    
        <copy>
        graph2 = graph.filter(pgx.EdgeFilter("edge.label()='TRANSFER'")); graph2
        </copy>
        
        PgxGraph(name: sub-graph_16, v: 6, e: 8, directed: True, memory(Mb): 0)
        
2.  WCC([Weakly Connected Component](https://docs.oracle.com/cd/E56133_01/latest/reference/analytics/algorithms/wcc.html)) 알고리즘은 분할 영역을 하나만 감지합니다.
    
        <copy>
        analyst.wcc(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 1)
        
    
    구성 요소 값은 **wcc**라는 등록 정보에 저장됩니다.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.wcc AS component_id
                 , COUNT(*) AS count
            FROM MATCH (a)
            GROUP BY a.wcc
            ORDER BY a.wcc
        """).print()
        </copy>
        
        +----------------------+
        | component_id | count |
        +----------------------+
        | 0            | 6     |
        +----------------------+
        
    
    이 경우 6개 계정이 모두 WCC 알고리즘에 의해 하나의 구성요소를 형성합니다.
    
3.  [강하게 연결된 구성요소](https://docs.oracle.com/cd/E56133_01/latest/reference//analytics/algorithms/scc.html) 알고리즘인 SCC Kosaraju를 대신 실행합니다. 세 가지 구성 요소를 감지합니다.
    
        <copy>
        analyst.scc_kosaraju(graph2)
        </copy>
        
        PgxPartition(graph: sub-graph_16, components: 3)
        
4.  구성요소 및 각 정점 수를 나열합니다.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.scc_kosaraju AS component_id
                 , COUNT(*) AS count
            FROM MATCH (a)
            GROUP BY a.scc_kosaraju
            ORDER BY a.scc_kosaraju
        """).print()
        </copy>
        
        +----------------------+
        | component_id | count |
        +----------------------+
        | 0            | 1     |
        | 1            | 4     |
        | 2            | 1     |
        +----------------------+
        
5.  John의 계정과 동일한 연결된 구성 요소에 있는 다른 계정을 나열합니다(= **xxx-yyy-201**). 구성 요소 ID는 PGQL 질의에 사용할 **SCC\_KOSARAJ** 등록 정보로 추가됩니다.
    
        <copy>
        graph2.query_pgql("""
            SELECT a.account_no
            FROM MATCH (a)
               , MATCH (a1)
            WHERE a1.account_no = 'xxx-yyy-201'
            AND a.scc_kosaraju = a1.scc_kosaraju
            ORDER BY a.account_no
        """).print()
        </copy>
        
        +-------------+
        | account_no  |
        +-------------+
        | xxx-yyy-201 |
        | xxx-yyy-202 |
        | xxx-yyy-203 |
        | xxx-yyy-204 |
        +-------------+
        
    
    ![커뮤니티](images/community.jpg)
    
    이 경우 계정 **xxx-yyy-201**(John의 계정), **xxx-yyy-202**, **xxx-yyy-203** 및 **xxx-yyy-204**는 하나의 분할 영역을 구성하고, 계정 **xxx-zzz-211**은 분할 영역이고, 계정 **xxx-zzz-212**는 SCC Kosaraju 알고리즘에 의한 분할 영역입니다.
    

이제 다음 랩을 진행할 수 있습니다.

## 확인

*   **작성자** - Jayant Sharma
*   **기여자** - Arabella Yao, Jenny Tsai
*   **최종 업데이트 수행자/날짜** - Ryota Yamanaka, 2023년 3월