# Criar Mapa do Zero

## Introdução

Neste laboratório, você cria uma nova página em seu aplicativo e, em seguida, configura uma Região de Mapa do zero.

Tempo de Laboratório Estimado: 15 minutos

### Objetivos

*   Compreender a configuração da Região do Mapa do APEX

### Pré-requisitos

*   Laboratório 2: Criar mapa com assistente

## Tarefa 1: Criar uma Nova Página

1.  Nas trilhas de navegação no canto superior esquerdo, clique no link do home do aplicativo. Em seguida, clique na guia **Layout**. ![Layout da página](images/create-map-15a.png)
    
2.  Clique em **Criar Página**. ![Assistente de criação de página](images/create-map-15b.png)
    
3.  Você pode selecionar Mapear aqui para ter o mesmo assistente que viu no assistente Criar Aplicativo. Mas este passo é criar um mapa do zero, por exemplo, se você tivesse uma página existente. Selecione **Página em Branco** e clique em **Próximo**. ![Selecionar Página em Branco](images/create-map-16.png)
    
4.  Para obter o nome, informe **Mapa de Aeroportos e Estados** e clique em **Próximo**. ![Informar Nome da página](images/create-map-16a.png)
    
5.  Selecione a opção para criar uma nova entrada no menu de navegação e informe **Mapa de Aeroportos e Estados**, ou seja, o mesmo que o nome da página. Em seguida, clique em **Próximo**. ![Criar entrada do menu de navegação](images/create-map-17.png)
    
6.  Verifique o resumo e clique em **Finalizar**. ![Verificar resumo](images/create-map-18.png)
    

## Tarefa 2: Adicionar um Mapa à Página

1.  Arraste **Mapa** da paleta Regiões na parte inferior e solte na seção Corpo do layout da página. Observe que a Região do Mapa aparece na árvore Página em Corpo com o nome padrão Novo. Clique em **Novo** na árvore Página e observe suas propriedades à direita. Observe que o Tipo de Região é Mapa. ![Adicionar Região do Mapa](images/create-map-19.png)
    
2.  No painel à direita, atualize o Título da Região de Novo para um nome de sua escolha, por exemplo, **Minha Região de Mapa**. Observe que o título é atualizado na árvore de páginas à esquerda. ![Informar título da Região](images/create-map-20.png)
    
3.  Observe que a Região do Mapa inclui um elemento filho chamado Camadas com uma Camada padrão chamada Nova. Camadas são o conteúdo orientado a dados a ser renderizado no mapa. Clique na Camada **Nova** na árvore de páginas para ver suas propriedades no painel direito. ![Exibir propriedades da Camada](images/create-map-21.png)
    
4.  Atualize o Nome da Camada para **Aeroportos** e o Tipo para **Pontos**. Observe a atualização do Nome da Camada na árvore de páginas à esquerda. ![Atualizar propriedades da Camada](images/create-map-23.png)
    
5.  Role para baixo no painel de propriedades Camada à direita. Atualize a **Origem** para usar a tabela **EBA\_SAMPLE\_MAP\_AIRPORTS**. Para limitar os aeroportos renderizados na camada, adicione a cláusula where **LAND\_AREA\_COVERED > 2500**. Ative a opção Usar Índice Espacial usando o switch. ![Atualizar propriedades da Camada](images/create-map-24.png)
    
6.  Role para baixo no painel de propriedades Camada à direita da seção **Mapeamento de Coluna**. É aqui que você configura a coluna espacial para renderização. Selecione o tipo de dados de geometria **SDO\_GEOMETRY** e a coluna de geometria **GEOMETRY**. ![Atualizar propriedades da Camada](images/create-map-25.png)
    
7.  Role para baixo no painel de propriedades Camada à direita da seção **Janela Informações**. É aqui que você pode configurar o conteúdo de uma janela de informações que aparece ao clicar em um item no mapa. Ative a **Formatação Avançada** clicando no botão de alternância e cole o seguinte na área de texto **Expressão HTML**:
    
        <copy>
        <strong>&AIRPORT_NAME.</strong><br>
        &CITY., &STATE_NAME.<br>
        Code: &IATA_CODE.
        </copy>
        
    
    ![Atualizar propriedades da Camada](images/create-map-25a.png)
    

## Tarefa 3: Adicionar uma Camada ao Mapa

1.  Na árvore Página à esquerda, clique com o botão direito do mouse em **Camadas** em sua Região de Mapa e selecione **Criar Camada**. ![Adicionar uma Camada](images/create-map-26.png)
    
2.  Clique na Camada recém-criada na árvore Página em sua Região do Mapa. Em seguida, no painel de detalhes Camada à direita, atualize o Nome para **Estados**, o tipo de Camada para **Polígonos** e a Origem para **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. ![Atualizar propriedades da Camada](images/create-map-27.png)
    
3.  As camadas serão renderizadas na ordem em que aparecem sob Camadas na árvore de páginas. Para que os Aeroportos sejam renderizados nos Estados superiores, arraste a camada **Estados** acima da camada Aeroportos em Camadas na árvore de páginas. Role para baixo no painel de detalhes Camada à direita da seção Mapeamento da Coluna. Selecione o tipo de dados de geometria **SDO\_GEOMETRY** e a coluna de geometria **GEOMETRY**. Em Aparência, selecione as cores de preenchimento e traçado (esboço) de sua escolha. Defina a opacidade de preenchimento para um valor de sua escolha, observando que um valor de 1 significa totalmente opaco para que o mapa de fundo não seja visível. ![Atualizar ordem de Camada](images/create-map-28.png)
    
4.  No canto superior direito, clique em **Salvar** e, em seguida, no botão verde **Executar**. ![Página Salvar e Executar](images/create-map-29.png)
    
5.  Observe a renderização do mapa com as camadas Estados e Aeroportos. Clique e arraste o mapa para panorâmica e use o controle de navegação no canto superior direito para ampliar e reduzir. Clique em um aeroporto para ver a janela de informações que você configurou. Passe o mouse sobre um estado para ver a dica de ferramenta configurada. Desligue as camadas com as caixas de seleção no mapa. ![Interaja com o mapa](images/create-map-30.png)
    

Parabéns por criar seu primeiro mapa do zero. No próximo Laboratório, você incorporará a análise espacial neste mapa.

Isso conclui o laboratório. Agora você pode ir para o próximo laboratório.

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, março de 2023