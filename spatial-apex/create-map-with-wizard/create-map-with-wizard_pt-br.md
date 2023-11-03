# Criar Mapa com Assistente

## Introdução

O Oracle APEX fornece um assistente para criar uma variedade de tipos de página úteis. Neste laboratório, você usará o assistente para criar um novo aplicativo e uma página com um mapa. Em seguida, inspecione a página resultante para compreender melhor a Região do Mapa.

Tempo de Laboratório Estimado: 10 minutos

### Objetivos

*   Compreender os conceitos básicos da Região do Mapa do APEX

### Pré-requisitos

*   Conclusão do Laboratório 1: Instalar aplicativo de Mapas de Amostra

## Tarefa 1: Criar um Novo Aplicativo com uma Página de Mapa usando o Assistente

O assistente fornece uma maneira rápida e fácil de criar um novo aplicativo e seu primeiro mapa.

1.  Navegue até **App Builder** e clique em **Criar**. ![Criar Assistente de Aplicativos no App Builder](images/create-map-01.png)
    
2.  Selecione **Novo Aplicativo**. ![Criar um Aplicativo - Novo Aplicativo](images/create-map-02.png)
    
3.  Informe um nome para seu aplicativo e clique em **Adicionar Página**. ![Criar um Aplicativo - Formulário](images/create-map-03.png)
    
4.  Selecione **Mapa** como o tipo de página. ![Criar um Aplicativo - Adicionar Página](images/create-map-04.png)
    
    **Observação**: Este é o mesmo assistente que usar **Criar Página** em um aplicativo existente.
    
5.  Informe **Mapa de Aeroportos** como Nome da Página. (Com este assistente, o Nome da Página também será usado como o nome da Região do Mapa criada na página.) Clique no ícone à direita da entrada da tabela para selecionar a tabela **EBA\_SAMPLE\_MAP\_AIRPORTS**. Para coluna de geometria, selecione **GEOMETRY** e, finalmente, selecione uma coluna para usar uma dica de ferramenta ao passar o mouse sobre um item no mapa. ![Criar um Aplicativo - Página Criar Mapa](images/create-map-05.png)
    
6.  Observe que sua nova página agora está listada em **Páginas**. Clique em **Criar Aplicativo**. ![Criar um Aplicativo - Finaliza a criação do aplicativo](images/create-map-06.png)
    
7.  Você navegará até a página em que gerencia seu novo aplicativo. Clique em **Executar Aplicativo**. ![Executar Aplicativo](images/create-map-07.png)
    
8.  Acesse o aplicativo usando o nome de usuário e a senha de log-in do APEX. ![Entre em seu aplicativo](images/create-map-08.png)
    
9.  O layout padrão que selecionamos para nosso aplicativo fornece uma página inicial com links para outras páginas. Na página inicial, navegue até a página que você acabou de criar. ![Home Page do Aplicativo](images/create-map-09.png)
    
10.  Observe que a página inclui um mapa interativo mostrando os locais do aeroporto com dicas de ferramenta conforme você configurou. ![Exibir o Mapa](images/create-map-10.png)
    

## Tarefa 2: Inspecionar a Página do Mapa

Agora você inspecionará a Região do Mapa criada pelo assistente.

1.  Na Barra de Ferramentas do Desenvolvedor, na parte inferior da página, clique no botão **Página 2** para editar a página. ![Editar a página](images/create-map-11.png)
    
2.  Na árvore Página à esquerda, em **Corpo**, clique em **Mapa de Aeroportos**. Este é o título da Região do Mapa criada pelo assistente de Criação de Página. É, por padrão, o mesmo que o título da Página e pode ser alterado conforme desejado. No painel de detalhes Região à direita, observe que esta Região tem um tipo de **Mapa**. ![Ver propriedades da página](images/create-map-12.png)
    
3.  As Regiões do Mapa incluem Camadas que são os pontos, linhas e polígonos (do Oracle Spatial, GeoJSON ou coordenadas) exibidos na parte superior de um mapa de plano de fundo. Ao percorrer o assistente de Criação de Página, você selecionou um Mapa usando a coluna GEOMETRY na tabela EBA\_SAMPLE\_MAP\_AIRPORTS (ou seja, dados do Oracle Spatial). Então, o assistente criou uma camada contendo esses locais de aeroporto. Por padrão, a Camada tem o mesmo nome da Página, ou seja, **Mapa de Aeroportos**. Isso pode ser alterado conforme desejado.
    
    Para inspecionar essa Camada, na árvore Página no painel esquerdo, em Camadas, clique em **Mapa de Aeroportos**. Os detalhes da configuração são exibidos no painel **Camada** à direita. Para obter informações sobre itens de configuração, clique na guia **Ajuda** no painel do meio. Quando você clica em itens de configuração, as informações de ajuda são exibidas para esse item. Por exemplo, clique no menu **Tipo de Camada** para ver a ajuda sobre suas opções. ![Inspecionar Propriedades da Camada do Mapa](images/create-map-13.png)
    
4.  Role para baixo no painel Camada para ver as outras opções de configuração que foram definidas pelo assistente, incluindo Mapeamento de Colunas, onde o tipo de dados de geometria está definido. Aqui você está usando o tipo de dados espaciais nativos da Oracle, SDO\_GEOMETRY, e o nome da coluna é GEOMETRY. ![Inspecionar Propriedades da Camada do Mapa](images/create-map-14.png)
    

Parabéns pela criação dos primeiros mapas. Há muita capacidade além do básico que você acabou de explorar. Sinta-se à vontade para experimentar ajustes nos parâmetros e, em seguida, salve e execute para ver os resultados. No próximo Laboratório, você configurará uma nova Região do Mapa do zero.

Isso conclui o laboratório. Agora você pode ir para o próximo laboratório.

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, março de 2023