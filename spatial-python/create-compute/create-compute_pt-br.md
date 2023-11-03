# Criar instância de computação com base em imagem personalizada

## Introdução

Uma imagem de computação foi pré-criada com o Python configurado. Neste laboratório, você cria uma instância de computação com base nessa imagem.

Tempo de Laboratório Estimado: xx minutos

### Objetivos

*   Crie uma instância de computação com base em uma imagem personalizada com o Python pré-configurado.

### Pré-requisitos

*   Conclusão do laboratório anterior (Criar Chaves SSH no Cloud Shell)

## Tarefa 1: Criar a instância de computação

1.  Navegue até Computação > Instâncias ![Instâncias de Computação](images/compute-01.png)
    
2.  Clique em **Criar Instância** ![Criar instâncias](images/compute-02.png)
    
3.  Informe um nome como **my-compute** ou deixe o padrão. Selecione um compartimento se você tiver criado um ou deixe o padrão (raiz). Em seguida, na seção de posicionamento, clique em **Editar**. ![Criar instâncias](images/compute-03.png)
    
4.  Se você planeja usar recursos Always Free, selecione o domínio de disponibilidade que oferece o **VM.Standard.E2.1. Forma micro**. ![Criar instâncias](images/compute-04.png)
    
5.  Role para baixo até a seção **Imagem e forma** e clique em **Editar**. ![Criar instâncias](images/compute-05.png)
    
6.  Clique em **Alterar imagem**. ![Criar instâncias](images/compute-06.png)
    
7.  Selecione **Minhas imagens** e **OCID da Imagem** ![Criar instâncias](images/compute-07.png)
    
8.  Copie o OCID abaixo e cole no campo OCID da Imagem e clique em **Selecionar imagem**.
    
        <copy>
         ocid1.image.oc1..aaaaaaaan727cclmzfl2evanaacnganaeobmv6hvakjzqdsk4gncmcklcxha
        </copy>
        
    
    ![Criar instâncias](images/compute-08.png)
    
9.  Role para baixo até a seção Rede e clique em **Editar**. ![Criar instâncias](images/compute-09.png)
    
10.  Se você tiver uma rede existente, poderá usá-la. Caso contrário, selecione **Criar nova rede virtual na nuvem**. Para nomes, digite **my-vcn** e **my-subnet**, ou você poderá deixar os padrões. Selecione um compartimento se você tiver criado um ou deixe o padrão (raiz). Em Endereço IPv4 Público, Confirme se a opção **Designar um endereço IPv4 público** está selecionada. ![Criar instâncias](images/compute-10.png)
    
11.  Role para baixo até a **seção Adicionar chaves SSH**, selecione **Colar chave pública** e clique em **Restaurar** para expandir seu Cloud Shell. ![Criar instâncias](images/compute-11.png)
    
12.  O último comando executado no Cloud Shell imprimiu sua chave pública. Copie sua chave pública do Cloud Shell e cole no campo de chaves SSH na caixa de diálogo Criar instância de computação. Em seguida, recolher o Cloud Shell. ![Criar instâncias](images/compute-12.png)
    
13.  Clique em **Criar**. ![Criar instâncias](images/compute-13.png)
    
14.  Quando o provisionamento estiver concluído, copie o endereço IP público da instância de computação e restaure o Cloud Shell. ![Criar instâncias](images/compute-14.png)
    
15.  Digite o comando a seguir no Cloud Shell para estabelecer conexão com sua instância de computação, na qual você pode colar "\[endereço IP\]", que foi copiado na etapa anterior.
    
        <copy>
         ssh -i ~/.ssh/my-ssh-key opc@[IP address]
        </copy>
        
    
    Quando solicitado a adicionar à lista de hosts conhecidos, responda com **yes**. ![Criar instâncias](images/compute-15.png)
    

Sua instância de computação foi criada e você verificou o acesso SSH.

## Tarefa 2: Abrir porta de rede 8001

1.  No painel de navegação principal, selecione **Networking**. Em seguida, selecione **Redes virtuais na nuvem**. ![Criar instâncias](images/compute-16.png)
    
2.  Clique na VCN criada na tarefa anterior. ![Criar instâncias](images/compute-17.png)
    
3.  Role a tela para baixo e clique em **Security lists** à esquerda, depois clique em **Default Security List for my-vcn**. ![Criar instâncias](images/compute-18.png)
    
4.  Clique em **Adicionar Regras de Entrada**. ![Criar instâncias](images/compute-19.png)
    
5.  Para CIDR de Origem, digite **0.0.0.0/0**. Para Destination Port Range, digite **8001**. Em seguida, clique em **Adicionar Regra de Entrada**. ![Criar instâncias](images/compute-20.png)
    
6.  Role para baixo e observe a nova Regra de Entrada que permite acesso de entrada à porta 8001. ![Criar instâncias](images/compute-21.png)
    

Agora você pode **prosseguir para o próximo laboratório**.

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, Database Product Management, junho de 2023