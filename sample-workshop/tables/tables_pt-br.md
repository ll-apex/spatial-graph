# Tabelas em LiveLabs

## As mesas são legais!

Você pode definir uma tabela no Markdown da mesma forma:

    | Tables        | Are           | Cool  |
    | ------------- |:-------------:| -----:|
    | **col 3 is**  | right-aligned | $1600 |
    | col 2 is      | *centered*    |   $12 |
    | zebra stripes | ~~are neat~~  |    $1 |
    

O resultado é assim:

| Tabelas | São | Frio |
| --- | :-: | --: |
| **col 3 é** | alinhado à direita | $1600 |
| col 2 é | _centralizado_ | $12 |
| listras zebra | são limpos | $1 |

Você pode ver que há uma legenda de tabela padrão fornecida que, por padrão, é uma concatenação do título do workshop e do título do laboratório.

Se você não gostar do padrão, também poderá fornecer seu próprio título de tabela adicionando a definição de tabela abaixo:

    {: title="My table title"}
    

O markdown completo tem esta aparência:

    | Tables        | Are           | Cool  |
    | ------------- |:-------------:| -----:|
    | **col 3 is**  | right-aligned | $1600 |
    | col 2 is      | *centered*    |   $12 |
    | zebra stripes | ~~are neat~~  |    $1 |
    {: title="My table title"}
    

Agora nossa tabela tem esta aparência:

| Tabelas | São | Frio |
| --- | :-: | --: |
| **col 3 é** | alinhado à direita | $1600 |
| col 2 é | _centralizado_ | $12 |
| listras zebra | são limpos | $1 |
| {: title="Título da minha tabela"} |  |  |

Como você pode ver, a numeração é adicionada automaticamente.

Não é legal?

Você também pode consultar a [LiveLabs Planilha de Referência Rápida de Markdown](https://objectstorage.us-ashburn-1.oraclecloud.com/p/MKKRgodQ0WIIgL_R3QCgCRWCg30g22bXgxCdMk3YeKClB1238ZJXdau_Jsri0nzP/n/c4u04/b/qa-form/o/LiveLabs_MD_Cheat_Sheet.pdf)