# Workshop com um único conjunto de laboratórios

## Instruções - Exclua este arquivo quando terminar

1.  Abra o modelo de oficina de amostra no Atom ou no Visual Studio Code
2.  Nós pré-criamos 5 pastas. Um workshop é criado com base em vários laboratórios.
3.  Remova os comentários como este: _Listar objetivos deste laboratório_
4.  Certifique-se de usar pasta minúscula e nome de arquivo e traços para espaços (setup-adb NOT Setup\_ADB)
5.  Seus nomes de imagem devem ter nomes descritivos. Não apenas adb1, adb2, adb3. Para acessibilidade para deficientes, precisamos das descrições da imagem para explicar como é a imagem. Lembre-se de todas as letras minúsculas e traços.
6.  Faça download do nosso documento de QA do WMS. Encontramos oficinas entrar em produção mais rápido quando você sabe o que é necessário para mover para a produção na frente e você usa o esqueleto.

PS: Você não precisa de um Readme.md. O Readme só existe nos níveis superiores da biblioteca. Direcionamos todo o tráfego para LiveLabs, pois não podemos rastrear o uso em GitHub. Não crie links diretos para GitHub, seu workshop pode ser super popular, mas não podemos rastreá-lo para que ninguém saiba.

## Caminho Absoluto para Navegação no menu do Oracle Cloud

**Laboratório 1: Provisionar uma Instância -> Etapa 0: Usar estas Imagens Padronizadas para Navegação do Oracle Cloud (Comumente para Provisionamento)** - Incluímos uma lista de capturas de tela comuns para navegar no Menu do Oracle Cloud. Leia esta seção e use as imagens de caminho absoluto relevantes, quando apropriado. Isso preparará seu workshop para o futuro em caso de atualizações da interface do usuário do Oracle Cloud.

## Estrutura da Pasta

Neste exemplo, o objetivo é criar vários workshops "filhos" a partir de um workshop "pai" mais longo. As crianças são compostas de partes do pai.

oficina de amostra/ -- laboratórios individuais

        provision/
        setup/
        dataload/
        query/
        introduction/
          introduction.md       -- description of the everything workshop, note that it is a "lab" since there is only one
    
    workshops/
       freetier/                -- freetier version of the workshop
        index.html
        manifest.json
       livelabs/                -- livelabs version of the workshop
        index.html
        manifest.json
    

### FreeTier x LiveLabs

*   "FreeTier" - inclui Avaliações Gratuitas, Contas Pagas e, para alguns workshops, contas Always Free (botão marrom)
*   "LiveLabs" - são workshops que usam tenancies fornecidas pela Oracle (botão verde)
*   "Desktop" - esta é uma nova implantação na qual o workshop é encapsulado em um ambiente NoVNC em execução em uma instância de computação

### Sobre o Workshop

O workshop inclui todos os 6 laboratórios individuais em uma única sequência.

A estrutura de pastas inclui um "laboratório" de Introdução que descreve o workshop como um conjunto completo de 6 laboratórios. Observação: talvez você não precise ter uma introdução diferente para cada uma das versões pai e filho dos workshops, isso é apenas ilustrativo.

Olhe para a pasta product-name-workshop/freetier e veja o arquivo manifest.json para ver a estrutura.

> **Observação:** O uso de "Lab n:" nos títulos é opcional

O "lab" de Pré-requisito é o primeiro laboratório em uma pasta comum no oracle-livelabs/repo comum. Como este laboratório já existe, podemos usar um URL RAW/absoluto:

    "filename": "https://oracle-livelabs.github.io/common/labs/cloud-login/cloud-login-livelabs2.md"        },
    

O arquivo manifest.json precisa saber o local de cada laboratório em relação ao local em que ele existe na hierarquia. Nesta estrutura, os laboratórios estão localizados em dois níveis, por exemplo:

    "filename": "../../provision/provision.md"
    

### Por exemplo:

Este [Workshop do APEX](https://oracle-livelabs.github.io/apex/spreadsheet/workshops/freetier/) é um bom exemplo de workshop com um único conjunto de laboratórios: [https://github.com/oracle-livelabs/apex/tree/main/spreadsheet](https://github.com/oracle-livelabs/apex/tree/main/spreadsheet).