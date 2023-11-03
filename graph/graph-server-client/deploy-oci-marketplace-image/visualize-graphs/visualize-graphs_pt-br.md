# Visualizar o Gráfico

## Introdução

Os resultados das análises feitas nos laboratórios anteriores podem ser facilmente visualizados usando o recurso Visualização de Gráfico.

Tempo estimado: 5 minutos

O vídeo a seguir fornece uma visão geral do componente Visualização de Gráfico (= GraphViz).

[youtube](youtube:zfefKdNfAY4)

### Objetivos

*   Saiba como executar consultas de gráfico PGQL e visualizar os resultados.

### Pré-requisitos

*   O gráfico é criado e publicado
*   O Servidor de Gráficos (com GraphViz) está ativo e em execução

## Tarefa 1: Efetuar log-in em GraphViz

Abra o GraphViz em **`https://<public_ip_for_compute>:7007/ui`** usando um Web browser. Substitua **`<public_ip_for_compute>`** pelo da sua instância de computação do Servidor de Gráficos.

Como a imagem do marketplace é distribuída com um certificado SSL autoassinado, você deve alterá-la para seu próprio certificado em uso de produção. Enquanto isso, os navegadores da web devem mostrar avisos, enquanto entendemos que é seguro.

Se você usar o **Chrome**, digite **thisisunsafe** na janela de aviso para ir para a tela GraphViz.

![login-chrome](images/login-chrome.jpg)

Usando o **Firefox**, clique em **Avançado** e, em seguida, em **Aceitar o Risco e Continuar**.

![login-firefox](images/login-firefox.jpg)

Você deverá ver uma tela semelhante à captura de tela abaixo. Informe o nome de usuário (**customer\_360**) e a senha e clique em Submeter. O **Servidor de Gráficos** é o padrão nas Opções Avançadas, portanto, você não precisa alterá-lo.

![fazer log-in](images/login.jpg)

## Tarefa 2: Modificar consulta

Modifique a consulta para obter as primeiras 5 linhas, ou seja, altere **LIMIT 100** para **LIMIT 5** e clique em Run.

Você deve ver um gráfico semelhante à captura de tela abaixo.

![mostrar-5-elementos](images/show-5-elements.jpg)

## Tarefa 3: Adicionar destaques

Agora vamos adicionar alguns rótulos e outro contexto visual. Estes são conhecidos como destaques. Clique [aqui](https://objectstorage.us-ashburn-1.oraclecloud.com/p/VEKec7t0mGwBkJX92Jn0nMptuXIlEpJ5XJA-A6C9PymRgY2LhKbjWqHeB5rVBbaV/n/c4u04/b/livelabsfiles/o/data-management-library-files/highlights.json.zip) para fazer download de um arquivo zip, highlights.json.zip. Descompacte este arquivo e anote onde ele está descompactado.

Clique no botão Carregar em **Definições** (no lado direito da tela). Navegue até a pasta apropriada e escolha o arquivo e clique em Abrir para carregá-lo.

![destaques-1](images/highlights-1.png)

O gráfico agora deve parecer

![destaques-2](images/highlights-2.png)

## Tarefa 4: Correspondência de padrões com PGQL

1.  Em seguida, vamos executar algumas consultas PGQL.
    
    O site [pgql-lang.org](http://pgql-lang.org) e a [Especificação](http://pgql-lang.org/spec/1.4) são as melhores referências para detalhes e exemplos. Para os fins deste laboratório, no entanto, aqui estão noções básicas mínimas.
    
    A estrutura geral de uma consulta PGQL é:
    
        <copy>
        SELECT <select_list>
        FROM MATCH <graph_pattern> ON <graph_name>
        WHERE <condition>
        </copy>
        
    
    O PGQL fornece uma construção específica conhecida como a cláusula **MATCH** para padrões de gráfico correspondentes. Um padrão de gráfico corresponde a vértices e arestas que satisfazem as condições e restrições fornecidas.
    
    *   **(v)** indica uma variável de vértice **v**
    *   **\-** indica uma borda não direcionada, como em (origem)-(dest)
    *   **\->** uma borda de saída da origem para o destino
    *   **<-** uma borda de entrada do destino para a origem
    *   **\[e\]** indica uma variável de borda **e**
    
    Além disso, omita **graph\_name** aqui, pois ele está selecionado na IU GraphViz.
    
2.  Vamos encontrar contas que tiveram uma transferência de saída e entrada de mais de 500 no mesmo dia.
    
    A consulta PGQL para isso é:
    
        <copy>
        SELECT *
        FROM MATCH (a)-[t1:transfer]->(a1)
           , MATCH (a2)-[t2:transfer]->(a)
        WHERE t1.transfer_date = t2.transfer_date
          AND t1.amount > 500
          AND t2.amount > 500
        </copy>
        
    
    Na primeira cláusula **MATCH** acima, **(a)** indica o vértice de origem e **(a1)** o destino, enquanto **\[t1:transfer\]** é a borda que os conecta. A **:transfer** especifica que a borda **t1** tenha o label **TRANSFER**. A vírgula (,) entre os dois padrões é uma condição AND.
    
3.  Copie e cole a consulta na caixa de entrada de texto Consulta de Gráfico PGQL do aplicativo GraphViz. Clique em Run.
    
    O resultado deve ser exibido como mostrado abaixo. Nas configurações de destaque, as contas que começam com **xxx-yyy-** são mostradas em vermelho (= contas do banco), enquanto **xxx-zzz-** são mostradas em laranja (= contas de outro banco).
    
    ![mesmo dia-transferências](images/same-day-transfers.jpg)
    
4.  A próxima consulta localiza padrões de transferências de e para as mesmas duas contas, ou seja, de a1->a2 e a2->a1.
    
    A consulta PGQL para isso é:
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
        </copy>
        
5.  Copie e cole a consulta na caixa de entrada de texto Consulta de Gráfico PGQL do aplicativo GraphViz. Clique em Run.
    
    O resultado deve ser exibido como mostrado abaixo.
    
    ![ciclo-2-hops](images/cycle-2-hops.jpg)
    
6.  Vamos adicionar mais uma conta a essa consulta para encontrar um padrão de transferência circular entre 3 contas.
    
    A consulta PGQL se torna:
    
        <copy>
        SELECT *
        FROM MATCH (a1)-[t1:transfer]->(a2)-[t2:transfer]->(a3)-[t3:transfer]->(a1)
        WHERE t1.transfer_date < t2.transfer_date
          AND t2.transfer_date < t3.transfer_date
        </copy>
        
7.  Copie e cole a consulta na caixa de entrada de texto Consulta de Gráfico PGQL do aplicativo GraphViz. Clique em Run.
    
    O resultado deve ser exibido como mostrado abaixo.
    
    ![ciclo-3-hops](images/cycle-3-hops.jpg)
    

## Agradecimentos

*   **Autor** - Jayant Sharma
*   **Colaboradores** - Arabella Yao, Jenny Tsai
*   **Última Atualização em/Data** - Ryota Yamanaka, março de 2023