# Acesse JupyterLab

## Introdução

Notebooks são documentos interativos para código, texto descritivo e visualizações. Neste workshop, você usa o código aberto JupyterLab, que fornece um ambiente de notebook baseado na Web com muitos recursos fáceis de usar, como upload de arquivos.

Tempo de Laboratório Estimado: 5 minutos

### Objetivos

*   Verifique o acesso a JupyterLab
*   Explore a funcionalidade de notebook
*   Selecione a opção para executar o restante do laboratório prático

## Tarefa 1: Recuperar endereço IP para JupyterLab

1.  No menu principal, navegue até Compute > Instances

![Recuperar endereço IP](images/compute-01.png)

2.  Na página de instruções do workshop, clique em **View Login Info** na parte superior esquerda e copie o nome do seu Compartimento.

![Recuperar endereço IP](images/compartment.png)

1.  Na console do OCI, cole no nome do Compartimento e selecione-o no pull-down.

![Recuperar endereço IP](images/compute-02.png)

4.  Observe o IP Público da sua instância de computação. JupyerLab foi definido nesta instância. Você o usará posteriormente neste e em outros Laboratórios.

![Recuperar endereço IP](images/compute-03.png)

## Tarefa 2: Verificar acesso a JupyterLab

1.  Abra uma nova guia do navegador e insira o URL **http://\[IP address\]:8001/lab** em que \[IP address\] seja o endereço recuperado na Tarefa 1.
    
    ![Acesse JupyterLab](images/access-jupyter-01.png)
    
2.  Informe a senha **livelabs** e clique em **Fazer Login**.
    

## Tarefa 2: Explorar Notebooks Jupyter

O Jupyter Notebook é uma ferramenta interativa baseada na Web que permite criar e compartilhar documentos que contêm código ao vivo, equações, visualizações e texto. É amplamente utilizado na comunidade de ciência de dados para prototipagem e análise de dados.

Nesta tarefa, analisaremos os conceitos básicos do uso do Jupyter Notebook.

1.  Crie um novo notebook.
    
    Quando seu ambiente Jupyter for carregado, você deverá ver uma guia do acionador aberta.
    
    ![A aba Iniciador está aberta](./images/launcher1.png)
    
    Se você não vir a janela do acionador, selecione o arquivo no canto superior esquerdo da janela e selecione "Novo acionador".
    
    ![Abrir nova guia do acionador](./images/launcher2.png)
    
    Na janela do acionador, selecione "Python 3" para criar um novo notebook usando a linguagem de programação Python. Um novo notebook será criado e você poderá começar a trabalhar nele inserindo código nas células de código ou adicionando texto de markdown nas células de markdown.
    
    ![criar um novo notebook Python](./images/launcher3.png)
    
2.  Adicionar um texto de markdown.
    
    Clique na célula de código e use o menu suspenso use o tipo de célula para selecionar 'Markdown'
    
    ![Célula Adicionar Markdown](./images/notebook1.png)
    
    Cole o seguinte na célula e clique no botão de reprodução na barra de ferramentas ou pressione Shift+Enter para executar a célula.
    
        	<copy>
        	# My First Notebook
        	This is my first Jupyter notebook
        	</copy>
        
    
    ![Resultado do markdown](./images/notebook2.png)
    
3.  Escreva um código Python. Cole o seguinte na próxima célula e execute-o. A frase "Olá, mundo!" deve aparecer abaixo da cela.
    
        	<copy>
        	print('Hello, World!')
        	</copy>
        
        
    
    ![olá, exemplo do mundo](./images/notebook3.png)
    
4.  Para salvar um Jupyter Notebook, clique no ícone "Salvar" na barra de ferramentas ou pressione Ctrl+S (ou Cmd+S em macOS). O notebook será salvo com a extensão de arquivo .ipynb.
    

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Colaboradores** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Última Atualização em/Data** - David Lapp, agosto de 2023