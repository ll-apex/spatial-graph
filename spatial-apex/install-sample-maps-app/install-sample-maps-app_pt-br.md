# Instalar o Aplicativo de Mapas de Amostra

## Introdução

O Oracle APEX fornece acesso a um portfólio de aplicativos de amostra que destacam áreas específicas de funcionalidade. Entre eles está o aplicativo Sample Maps, que mostra os recursos de mapeamento no Oracle APEX. Uma grande variedade de exemplos são fornecidos para servir como exemplos funcionais e pontos de partida para personalização adicional. Neste laboratório, você instalará e configurará o aplicativo Mapas de Amostra.

Tempo de Laboratório Estimado: 15 minutos

### Objetivos

*   Instalar o aplicativo Mapas de Amostra
*   Carregar dados de suporte

### Pré-requisitos

*   O Oracle APEX 21.1+ é obrigatório. as capturas de tela neste workshop serão feitas usando o APEX 21.2. Como geralmente recomendamos o uso da [versão mais recente do APEX](https://www.oracle.com/tools/downloads/apex-downloads/), espere pequenas diferenças ocasionais na interface do usuário.

## Tarefa 1: Instalar o Aplicativo

1.  Comece clicando em **App Builder**.
    
    ![Application Builder do APEX](images/install-sample-maps-00.png)
    
2.  Clique em **Instalar um Aplicativo Inicial ou de Amostra**.
    
    ![Selecionar aplicativo inicial ou de amostra](images/install-sample-maps-01.png)
    
    **Observação:** Se o Espaço de Trabalho tiver aplicativos existentes, clique em **Criar** e, em seguida, em **Aplicativo Inicial**.
    
3.  Clique em **Amostras** para abrir uma nova guia do browser com uma lista de aplicativos de amostra disponíveis.
    
    ![Selecionar amostras](images/install-sample-maps-02.png)
    
4.  Role para baixo até **Mapas de Amostra** e clique em **Fazer Download do Aplicativo**.
    
    ![Texto alternativo da imagem](images/install-sample-maps-03.png)
    
    Você será solicitado a salvar o bundle do aplicativo em uma pasta local.
    
    **Observação:** Se você for redirecionado para o github, navegue até a pasta da versão do APEX e faça download da **sample-maps.zip**.
    
5.  Retorne à guia do browser do App Builder e clique em **Importar**.
    
    ![Selecionar Importação](images/install-sample-maps-04.png)
    
6.  Arraste e solte ou navegue até o arquivo zip do aplicativo Mapas de amostra baixado anteriormente. Deixe a seleção Tipo de Arquivo como Aplicativo de Banco de Dados e clique em **Próximo**.
    
    ![Selecionar zip do Aplicativo de Mapas de Amostra](images/install-sample-maps-05.png)
    
7.  Importação de arquivo confirmada. Clique em **Próximo** novamente.
    
    ![Clique em Próximo](images/install-sample-maps-06.png)
    
8.  Deixe as seleções de menu padrão e clique em **Instalar Aplicativo**.
    
    ![Clique em Install Application](images/install-sample-maps-07.png)
    
    Isso o levará ao assistente de Instalação de Aplicativos.
    
9.  Deixe as seleções de menu padrão e clique em **Próximo**.
    
    ![Clique em Próximo](images/install-sample-maps-08.png)
    
10.  Clique em **Próximo** para validar a compatibilidade do sistema.
    

![Clique em Próximo](images/install-sample-maps-09.png)

11.  Com a compatibilidade confirmada, clique em **Instalar** para iniciar a instalação de objetos de banco de dados de suporte e do aplicativo APEX.

![Clique em Install](images/install-sample-maps-10.png)

12.  Quando a instalação estiver concluída, clique em **Executar Aplicativo**.

![Clique em Run Application](images/install-sample-maps-11.png)

13.  Acesse o aplicativo Sample Maps usando o nome de usuário e a senha do espaço de trabalho do APEX.

![Acessar](images/install-sample-maps-12.png)

## Tarefa 2: Carregar Dados

1.  Agora você está no aplicativo Sample Maps, que fornece vários exemplos de mapas e operações espaciais no APEX. Na inicialização inicial, uma mensagem de aviso é exibida com relação ao carregamento de dados. Clique no link **Carregamento de Dados** dentro dessa mensagem. Você navegará até uma página na qual concluirá o carregamento dos dados de demonstração.
    
    ![Clique em Data Loading](images/install-sample-maps-13.png)
    
2.  A página Carregamento de Dados mostra o status de carregamento dos conjuntos de dados Estados e Aeroportos usados pelo aplicativo Mapas de Amostra e pelo restante deste workshop. Na instalação do aplicativo Mapas de amostra, esses conjuntos de dados são apenas parcialmente carregados. Para concluir o carregamento de dados de amostra, você pode carregar diretamente dos arquivos armazenados no github ou primeiro fazer download dos arquivos e carregar do sistema local. Se você estiver executando o APEX em uma rede que exija um proxy para acessar o github, use a última opção.
    
    Se sua instância do APEX não exigir um proxy para acessar o github (por exemplo, apex.oracle.com ou APEX com o Oracle Autonomous Database), clique no botão para carregar **Diretamente de GitHub** e, em seguida, clique em **Carregar Conjunto de Dados** no canto superior direito.
    
    ![Clique diretamente no Github](images/install-sample-maps-14.png)
    
    Se sua instância do APEX exigir um proxy para acessar o github (por exemplo, o APEX executado atrás do firewall corporativo) ou se você tiver outros problemas ao carregar diretamente do github, clique no botão **Fazer Upload de Arquivos**, que fornece instruções alternativas.
    
3.  Quando o carregamento de dados estiver concluído, você verá uma notificação no canto superior direito e a mensagem de aviso desaparecerá. O aplicativo Mapas de amostra agora está pronto para uso.
    
    ![Confirmação de Carga de Dados](images/install-sample-maps-15.png)
    

## Tarefa 3: Explorar o Aplicativo de Mapas de Amostra

1.  Clicar em qualquer um dos blocos navega até a página associada no aplicativo. Como exemplo, clique em **Mapear e Reportar**.
    
    ![Navegar até a página Mapa e Relatório](images/install-sample-maps-16.png)
    
2.  Nesta página, clicar em um item no relatório à direita centraliza o item no mapa e abre uma janela de informações. Clicar no ícone no canto superior esquerdo abre um painel de navegação para acessar outras páginas do aplicativo.
    
    ![Interaja com o mapa](images/install-sample-maps-17.png)
    
3.  Clique em itens no painel de navegação para acessar outras páginas do aplicativo.
    
    ![O painel de navegação mostra outras páginas](images/install-sample-maps-18.png)
    
4.  Para fechar o painel de navegação, clique no ícone no canto superior esquerdo. Você também pode navegar até a home page do aplicativo clicando em **Mapas de Amostra** no canto superior esquerdo.
    
    ![Fechar painel de navegação](images/install-sample-maps-19.png)
    

## Tarefa 4: Explorar os Dados de Demonstração

1.  Retorne ao APEX, clique em **SQL Workshop** e em **Object Browser**.
    
    ![SQL Workshop - Object Browser](images/install-sample-maps-20.png)
    
2.  Observe as tabelas criadas pela etapa de carregamento de dados executada anteriormente. Clique em **EBA\_SAMPLE\_MAP\_AIRPORTS**. Observe que as colunas incluem uma coluna chamada GEOMETRY que tem o tipo SDO\_GEOMETRY (tipo de dados espaciais nativos da Oracle).
    
    ![Tabela com coluna de geometria nativa](images/install-sample-maps-21.png)
    
3.  Clique na guia **Dados** para exibir o conteúdo da tabela.
    
    ![Conteúdo da tabela](images/install-sample-maps-22.png)
    
    Em seguida, role para a direita para ver a coluna de geometria. Como os aeroportos são armazenados como pontos, o APEX exibe uma representação de string do valor da geometria do ponto. Como os pontos sempre se baseiam em uma única coordenada, faz sentido que o APEX exiba o valor dessa maneira.
    
    ![Geometrias de ponto](images/install-sample-maps-23.png)
    
4.  Clique em **EBA\_SAMPLE\_MAP\_SIMPLE\_STATES**. Observe novamente que as colunas incluem uma coluna chamada GEOMETRY que tem o tipo SDO\_GEOMETRY (tipo de dados espaciais nativos da Oracle).
    
    ![Tabela com coluna de geometria nativa](images/install-sample-maps-24.png)
    
5.  Clique na guia **Dados** para exibir o conteúdo da tabela. Uma vez que esta tabela armazena estados, as geometrias são polígonos. O APEX não exibe uma representação de string desses valores porque eles podem incluir conjuntos extremamente longos de coordenadas.
    
    ![geometrias de polígono](images/install-sample-maps-25.png)
    
6.  Observe as tabelas com nomes como **MDRT\_....$**. Eles são criados e gerenciados automaticamente nos bastidores pelo banco de dados para suportar índices espaciais em outras tabelas. Você nunca cria, atualiza ou exclui manualmente essas tabelas. Eles são apenas para apoiar operações de análise espacial e podem ser ignorados.
    
    ![Artefatos de índice espacial](images/install-sample-maps-26.png)
    
7.  Por fim, você pode executar uma consulta espacial básica com esses dados. Clique em **SQL Workshop** e em **SQL Commands**.
    
    ![SQL Workshop - Comandos SQL](images/install-sample-maps-27.png)
    
8.  A consulta a seguir retorna o número de aeroportos com cobertura de terra acima de 1000 acres que estão dentro de 100 km do Texas. Observe o uso do operador espacial nativo **sdo\_within\_distance**. Copie e cole a consulta na janela SQL Commands e clique em **Run** no canto superior direito.
    
        <copy>
        select count(a.id) as number_of_airports
        from EBA_SAMPLE_MAP_AIRPORTS a,
              EBA_SAMPLE_MAP_SIMPLE_STATES b
        where b.state_code= 'TX'
           and land_area_covered > 1000
           and sdo_within_distance(a.geometry, b.geometry, 'distance=100 unit=KM') = 'TRUE'
        </copy>
        
    
    ![Consulta espacial](images/install-sample-maps-28.png)
    
9.  No operador sdo\_within\_distance, atualize a distância para 300 km e execute novamente. Observe as alterações de resultado com base na área de pesquisa maior.
    
    ![Consulta espacial](images/install-sample-maps-29.png)
    

Em um laboratório posterior, você configurará um mapa que exibe os resultados dessa consulta em que o estado e a distância são controlados pelos menus da página.

Agora você instalou e explorou o aplicativo Mapas de amostra e os dados. Em seguida, avance para começar a criar seu próprio aplicativo e mapas.

Isso conclui o laboratório. Agora você pode ir para o próximo laboratório.

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Colaboradores** - Carsten Czarski, Desenvolvimento APEX, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, março de 2023