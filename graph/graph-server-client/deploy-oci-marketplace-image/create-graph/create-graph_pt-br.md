# Criar o Gráfico

## Introdução

Agora, as tabelas são criadas e preenchidas com dados. Vamos criar uma representação gráfica deles.

Tempo estimado: 5 minutos

### Objetivos

Saiba como criar um gráfico com base em origens de dados relacionais:

*   Iniciando um cliente (shell Python) que se conecta ao Servidor de Gráficos
*   Usando DDL (Data Definition Language) PGQL (por exemplo, CREATE PROPERTY GRAPH) para instanciar um gráfico

### Pré-requisitos

*   Este laboratório pressupõe que você tenha concluído com êxito o laboratório - Criar e preencher tabelas.

## Tarefa 1: Iniciar o cliente Python

Conecte-se à instância de computação via SSH como usuário **opc**, usando a chave privada criada anteriormente.

    <copy>
    ssh -i <private_key> opc@<public_ip_for_compute>
    </copy>
    

Exemplo:

    <copy>
    ssh -i key.pem opc@203.0.113.14
    </copy>
    

Inicie uma instância do shell do cliente Python que se conecte ao servidor.

    <copy>
    opg4py -b https://localhost:7007 -u customer_360
    </copy>
    

Você verá o seguinte se o shell do cliente for iniciado com sucesso.

    <copy>
    password:
    
    Oracle Graph Client Shell 22.4.0
    >>>
    </copy>
    

## Tarefa 2: Criar um gráfico

Configure a instrução Criar gráfico de propriedades, que cria um gráfico a partir das tabelas existentes.

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
    

Para obter mais informações sobre a sintaxe DDL, consulte [pgql-lang.org](https://pgql-lang.org/spec/1.4/#create-property-graph). Observe que _todas as colunas das tabelas de entrada são mapeadas para as propriedades de vértices/bordas [por padrão](https://pgql-lang.org/spec/1.4/#properties)_. Para a borda **owned\_by**, somente a propriedade **id** é fornecida com a palavra-chave **PROPERTIES** para fins de geração de ID de borda, e as outras propriedades não são fornecidas porque já são mantidas pelos vértices da conta.

Agora execute a DDL PGQL para criar o gráfico.

    >>> <copy>session.prepare_pgql(statement).execute()</copy>
    False   # This is the expected result
    

## Tarefa 3: Verifique o gráfico recém-criado

Verifique se o gráfico foi criado. Copie, cole e execute as instruções a seguir no shell Python.

Anexe o gráfico.

    >>> <copy>graph = session.get_graph("customer_360")</copy>
    

Verifique se o gráfico foi criado.

    >>> <copy>graph</copy>
    PgxGraph(name: customer_360, v: 15, e: 24, directed: True, memory(Mb): 0)
    

Executar algumas consultas PGQL. Por exemplo, a lista de rótulos de vértice:

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
    

Quantos vértices com cada rótulo:

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
    

A lista de labels de borda:

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
    

Quantas bordas com cada rótulo:

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
    

## Tarefa 4: Publicar o gráfico

O gráfico recém-criado é "privado" por padrão e só pode ser acessado a partir da sessão atual. Para acessar o gráfico de novas sessões no futuro, você pode "publicar" o gráfico.

Em seguida, crie o gráfico novamente seguindo o procedimento acima e publique-o.

    <copy>
    graph.publish()
    </copy>
    

Na próxima vez que você se conectar, poderá acessar o gráfico mantido na memória sem recarregá-lo, se o servidor de gráficos não tiver sido encerrado ou reiniciado entre logins.

    <copy>
    graph = session.get_graph("customer_360")
    </copy>
    

Observe que você tem permissão para publicar gráficos porque a atribuição **`PGX_SESSION_ADD_PUBLISHED_GRAPH`** foi concedida quando o usuário é criado. Caso contrário, ele deverá ser concedido pelo usuário **ADMIN** e reconectado com o shell Python para selecionar as permissões atualizadas.

Agora você pode ir para o próximo laboratório.

## Agradecimentos

*   **Autor** - Jayant Sharma
*   **Colaboradores** - Arabella Yao, Jenny Tsai
*   **Última Atualização em/Data** - Ryota Yamanaka, março de 2023