# Conecte-se ao Compute

## Introdução

Para acessar sua computação de host Python, você precisa de um par de chaves SSH. O Oracle Cloud Infrastructure (OCI) Cloud Shell é um terminal baseado em web browser acessível na Console do Oracle Cloud que fornece acesso a um shell do Linux. Você recuperará um par de chaves SSH e estabelecerá conexão com seu host Python no OCI Cloud Shell.

Tempo de Laboratório Estimado: 5 minutos

Assista ao vídeo abaixo para uma rápida apresentação do laboratório. [Laboratório 1](videohub:1_0tvxm2q0)

### Objetivos

*   Recuperar endereço IP de computação
*   Recuperar par de chaves SSH
*   Criar conexão SSH para computação

### Pré-requisitos

*   Você deve estar conectado à console do OCI

## Tarefa 1: Recuperar endereço IP da instância de computação

1.  No menu principal, navegue até Compute > Instances

![Abrir Cloud Shell](images/compute-01.png)

2.  Na página de instruções do workshop, clique em **View Login Info** na parte superior esquerda e copie o nome do seu Compartimento.

![Abrir Cloud Shell](images/compartment.png)

1.  Na console do OCI, cole no nome do Compartimento e selecione-o no pull-down.

![Abrir Cloud Shell](images/compute-02.png)

4.  Observe o IP Público da sua instância de computação. Você o usará posteriormente neste e em outros Laboratórios.

![Abrir Cloud Shell](images/compute-03.png)

## Tarefa 2: Recuperar chaves SSH

1.  Abra o Cloud Shell.
    
    ![Abrir Cloud Shell](images/compute-04.png)
    
2.  Se solicitado a executar o tutorial, digite N e digite Enter.
    
    ![Abrir Cloud Shell](images/compute-05.png)
    
3.  Na linha de comando, execute cada um dos itens a seguir para criar e navegar até sua pasta SSH.
    
        <copy>
        mkdir ~/.ssh
        </copy>
        
    
          ```
        cd ~/.ssh \`\`\`

![Criar chaves](images/compute-06.png)

1.  Na linha de comando, execute o seguinte para recuperar e listar um arquivo zip que contém chaves SSH.
    
        <copy>
        wget https://objectstorage.us-ashburn-1.oraclecloud.com/p/hfpJ4-8XrB5tWBDUWvgnCmGch_1WHhihBrRpHNIzj6JSq5O5hbwp2wsqRPYbg8Gm/n/c4u04/b/livelabsfiles/o/labfiles/ocw23-keys.zip
        </copy>
        
    
        <copy>
        ls
        </copy>
        
    
    ![Criar chaves](images/compute-07.png)
    
2.  Na linha de comando, execute o seguinte para descompactar e listar o conteúdo do arquivo zip.
    
        <copy>
        unzip ocw23-keys
        </copy>
        
    
        <copy>
        ls
        </copy>
        

![Criar chaves](images/compute-08.png)

## Tarefa 3: Estabelecer conexão com a instância de computação

2.  Na linha de comando, execute o seguinte para estabelecer conexão com sua instância de computação Python, em que Endereço IP é o Endereço IP de computação da Tarefa 1.
    
        <copy>
         ssh -i ~/.ssh/ocw23-rsa opc@[IP address]
        </copy>
        
    
    Se solicitado a adicionar à lista de hosts conhecidos, responda com **yes**.
    
    ![Criar chaves](images/compute-09.png)
    
3.  Clique no ícone de recolhimento para minimizar o Cloud Shell.
    
    ![Recolher Cloud Shell](images/compute-10.png)
    
4.  Observe o botão Restaurar para reabrir o Cloud Shell. Você reabrirá o Cloud Shell em um Laboratório subsequente.
    
    ![Restaurar Cloud Shell](images/compute-11.png)
    

Agora você pode **prosseguir para o próximo laboratório**.

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Colaboradores** - Rahul Tasker, Denise Myrick, Ramu Gutierrez
*   **Última Atualização em/Data** - David Lapp, agosto de 2023