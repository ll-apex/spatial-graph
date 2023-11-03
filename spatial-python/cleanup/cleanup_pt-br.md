# Limpar

## Introdução

Você pode limpar seu ambiente de workshop redefinindo seu Autonomous Database para o estado pré-workshop.

Tempo de Laboratório Estimado: 2 minutos

### Objetivos

*   Redefinir o Autonomous Database para o estado pré-workshop

### Pré-requisitos

*   Instância ativa do Autonomous Database

## Tarefa 1: Redefinir o Autonomous Database para o estado pré-workshop

1.  Execute o seguinte para remover todos os artefatos de banco de dados criados neste workshop.
    
        <copy>
        import oracledb
        my_pwd = open('./my-pwd.txt','r').readline().strip()
        my_dsn = open('./my-dsn.txt','r').readline().strip()
        connection = oracledb.connect(user="admin", password=my_pwd, dsn=my_dsn)
        cursor = connection.cursor()
        cursor.execute("drop table transactions")
        cursor.execute("drop table locations")
        cursor.execute("drop table transaction_labels")
        cursor.execute("drop function lonlat_to_proj_geom")
        cursor.execute("delete from user_sdo_geom_metadata")
        connection.commit()
        </copy>
        

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, agosto de 2023