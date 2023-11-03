# Incorporar Análise Espacial

## Introdução

Neste laboratório, você aprimora seu mapa do laboratório anterior incorporando uma análise espacial. Você configurará uma pesquisa de aeroportos localizados em uma distância definida pelo usuário de um estado selecionado.

Tempo de Laboratório Estimado: 30 minutos

### Objetivos

*   Entender uma operação básica de análise espacial
*   Compreender a integração da análise espacial na Região do Mapa do APEX

### Pré-requisitos

*   Laboratório 3: Criar um mapa do zero

## Tarefa 1: Adicionar uma Região para Filtros

1.  Clique na **Página 3: Mapa de Aeroportos e Estados** na parte superior da árvore à esquerda. Em seguida, no painel de propriedades Página à direita, em Aparência, altere o Modelo de Página para **Coluna Lateral Esquerda**.
    
    ![Atualizar Modelo de Página](images/add-spatial-analysis-01a.png)
    
    Você verá **LEFT COLUMN** no layout.
    
    ![Atualizar Modelo de Página](images/add-spatial-analysis-01b.png)
    
2.  Arraste uma região Conteúdo Estático para a coluna esquerda.
    
    ![Adicionar Região de Conteúdo Estático](images/add-spatial-analysis-01c.png)
    
3.  Renomeie para **Região Meus Filtros** ou um nome de sua escolha.
    
    ![Renomear Região](images/add-spatial-analysis-02.png)
    

## Tarefa 2: Adicionar um Item para Seleção de Estado

1.  Arraste um item Selecionar Lista para sua região de filtros e atualize o nome para **P3\_STATE**.
    
    ![Adicionar Selecionar Item da Lista](images/add-spatial-analysis-03.png)
    
2.  Nas propriedades Item da Página à direita, role até a seção Lista de Valores. Ative **Valor Obrigatório** usando a chave, defina o Tipo como **Consulta SQL** e informe a seguinte consulta:
    
        <copy>
          select name, state_code
            from EBA_SAMPLE_MAP_SIMPLE_STATES
        order by name
        </copy>
        
    
    ![SELECT consulta](images/add-spatial-analysis-04.png)
    
3.  Nas propriedades Item da Página à direita, role até a seção Padrão. Defina o Tipo como **Estático** e o valor como **'Texas'** ou outro estado de sua escolha (entre aspas simples).
    
    ![Configurar Lista de Seleção](images/add-spatial-analysis-05.png)
    

## Tarefa 3: Adicionar um Item para Entrada de Distância

1.  Arraste o Campo de Número para sua região de filtros. Atualize o nome para **P3\_DISTANCE** e o label para **Proximidade (km)**.
    
    ![Adicionar Item de Campo de Número](images/add-spatial-analysis-06.png)
    
2.  Nas propriedades do Item de Página à direita, role para baixo até a seção Validação e ative **Valor Obrigatório**.
    
    ![Definir Validação como Valor Obrigatório](images/add-spatial-analysis-07.png)
    
3.  Role para baixo até a seção Padrão. Defina o Tipo como **Estático** e o valor como **100**.
    
    ![Definir Valor Padrão](images/add-spatial-analysis-08.png)
    
    Agora você tem entradas para filtrar aeroportos por proximidade a um estado. Em seguida, você aplicará os filtros usando Ações Dinâmicas.
    

## Tarefa 4: Aplicar Filtros usando Ações Dinâmicas

Em seguida, você cria as ações que são chamadas quando os valores de estado e/ou distância são alterados pelo usuário.

1.  Clique com o botão direito do mouse no item P3\_STATE ou P3\_DISTANCE e selecione **Criar Ação Dinâmica** (a ação que criamos será aplicada a ambos os itens).
    
    ![Criar Ação Dinâmica](images/add-spatial-analysis-09.png)
    
2.  Nas propriedades Ação Dinâmica à direita, defina o Nome como **Validar e Atualizar**. Na seção Quando, defina Evento como **Alterar**, Tipo de Seleção como **Itens** e itens para a lista separada por vírgulas **P3\_DISTANCE,P3\_STATE** . Observe que o botão à direita da caixa de texto de itens permite selecionar itens de uma lista. Para evitar o envio de valores negativos para distância, na seção Condição do Cliente, defina Tipo como **Item >= Valor**, item como **P3\_DISTANCE** e Valor como **0**.
    
    ![Configurar ação dinâmica](images/add-spatial-analysis-10.png)
    
3.  As Ações Dinâmicas são configuradas com ação(ões) VERDADEIRA(s) e ação(ões) FALSA(s) que são chamadas com base nas condições que foram configuradas. Nesse caso, a condição do cliente (P3\_DISTANCE >= 0) determina se a Ação VERDADEIRA (condição atendida) ou a Ação FALSA (condição não atendida). Isso nos permitirá capturar a entrada de distância negativa.
    
    Quando a condição do cliente for TRUE, a ação deverá enviar os valores de entrada e atualizar a página. Clique na ação em Verdadeiro. Nas propriedades Ação à direita, em Ação do conjunto de Identificação para **Atualizar**. Em Elementos Afetados, defina o Tipo de Seleção como **Região** e Região como **Minha Região de Mapa** (ou o nome que você usou se for diferente). Observe na árvore de páginas à esquerda que a ação Verdadeira muda para Atualizar.
    
    ![Configurar ação dinâmica](images/add-spatial-analysis-11.png)
    
4.  Em seguida, você configurará a ação a ser chamada quando a condição do cliente não for atendida, o que significa que um valor de distância negativo foi inserido. Em Ações Dinâmicas para um dos itens, clique com o botão direito do mouse em Falso e selecione **Criar Ação FALSA**.
    
    ![Configurar ação dinâmica](images/add-spatial-analysis-12.png)
    
5.  A Ação FALSE chamada quando a distância é negativa será uma mensagem pop-up para o usuário. Clique na ação False. Nas propriedades Ação à direita, em Identificação, defina Ação como **Alerta**. Em Definições, defina o Título como **Distância inválida** (este será o banner do alerta) e a Mensagem como **Distância deve ser >= 0** (este será o corpo do alerta). Observe na árvore de páginas à esquerda que a ação Falso muda para Alerta.
    
    ![Configurar ação dinâmica](images/add-spatial-analysis-13.png)
    
6.  Sua Região do Mapa atualmente inclui uma camada Estados exibindo todos os estados. Agora você ajusta essa camada para exibir apenas o estado selecionado no menu P3\_STATE. Na árvore de páginas à esquerda, em Camadas, clique em Estados. Nas propriedades de Camada à direita, em Nome de alteração de Identificação para **Estado Selecionado**. Em Origem, defina a Cláusula Where como **state\_code = :P3\_STATE**. Observe na árvore de páginas à esquerda que o nome da camada muda para Estado Selecionado.
    
        <copy>
        state_code = :P3_STATE
        </copy>
        
    
    ![Configurar a cláusula WHERE](images/add-spatial-analysis-14.png)
    
7.  Por fim, atualize a camada Aeroportos para retornar itens filtrados pelo estado e proximidade especificados pelo usuário. Na árvore Página à esquerda, clique na camada Aeroportos. Nas propriedades de Camada à direita, em Origem, altere Tipo para **Consulta SQL**. Para Consulta SQL, informe o seguinte, que usa o operador SQL nativo "dentro da distância" do Oracle Database.
    
        <copy>
        select a.*
          from EBA_SAMPLE_MAP_AIRPORTS a,
               EBA_SAMPLE_MAP_SIMPLE_STATES b
         where b.state_code= :P3_STATE
           and a.land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance='|| :P3_DISTANCE ||' unit=KM') = 'TRUE'
        </copy>
        
    
    Para Itens de Página a Submeter, informe a lista separada por vírgulas **P3\_STATE,P3\_DISTANCE**.
    
    ![Consulta SQL espacial](images/add-spatial-analysis-15.png)
    
8.  Sua página está pronta para ser exibida. Clique em **Salvar** e, em seguida, no botão verde **Executar** no canto superior direito. Depois que a página for renderizada, para estado, selecione **Alabama**. O mapa exibe o estado e os aeroportos selecionados dentro de 100 km (a distância padrão).
    
    ![Página Salvar e Executar](images/add-spatial-analysis-16.png)
    
9.  Altere o estado selecionado para **Kansas**. Observe o mapa agora exibe o estado selecionado e aeroportos com 100 km.
    
    ![Selecionar Kansas](images/add-spatial-analysis-17.png)
    
10.  Aumente a distância para 600km e clique em Enter ou Tab para enviar. Observe o mapa agora exibe aeroportos adicionais a uma distância maior.
    
    ![Aumentar a distância para 600 km](images/add-spatial-analysis-18.png)
    
11.  Por fim, confirme se o envio de uma distância negativa resulta no pop-up Erro configurado anteriormente.
    
    ![Alerta de distância negativa](images/add-spatial-analysis-19.png)
    
    Conforme mostrado no aplicativo Mapas de Amostra que você instalou no início deste workshop, há uma enorme quantidade de funcionalidades adicionais que podem ser obtidas com as Regiões do Mapa e o Spatial. Este workshop introduziu o básico e é nossa esperança que seu interesse tenha sido despertado e que você aproveite o poder dos mapas e análises espaciais em seus aplicativos APEX.
    

## Saiba Mais

*   [Oracle Spatial](https://www.oracle.com/database/spatial/)
*   [APEX](https://apex.oracle.com/)

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, março de 2023