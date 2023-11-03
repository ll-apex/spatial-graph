# Redefinir ADB para estado de pré-workshop

## Introdução

Este laboratório é para remover tudo o que foi criado nos laboratórios anteriores para que você possa começar de novo, se necessário.

Tempo de Laboratório Estimado: 2 minutos

### Sobre

Neste laboratório, todos os artefatos criados anteriormente são eliminados.

### Objetivos

*   Redefina o ADB para o estado do pré-workshop.

### Pré-requisitos

*   Conclusão do Laboratório 3; Preparar Dados Espaciais

## Tarefa 1: Remover tudo o que foi criado neste workshop

1.  Para remover tabelas e índices criados neste workshop, execute o seguinte usando o botão executar script na Planilha SQL.
    
    ![Texto alternativo da imagem](images/run-script.png)
    
        <copy> 
        DROP TABLE WAREHOUSES;
        DROP TABLE STORES;
        DROP TABLE REGIONS;
        DROP TABLE TORNADO_PATHS;
        </copy>
        
2.  Para eliminar metadados espaciais inseridos neste workshop, execute o seguinte usando o botão run script na Planilha SQL.
    
        <copy> 
        DELETE FROM USER_SDO_GEOM_METADATA
        WHERE TABLE_NAME IN (
            'WAREHOUSES', 
            'STORES', 
            'REGIONS', 
            'TORNADO_PATHS');
        COMMIT;
        </copy>
        
3.  Para eliminar a função criada neste workshop, execute o seguinte:
    
        <copy> 
        DROP FUNCTION GET_GEOMETRY;
        </copy>
        

## Agradecimentos

*   **Autor** - David Lapp, Database Product Management, Oracle
*   **Última Atualização em/Data** - David Lapp, setembro de 2022