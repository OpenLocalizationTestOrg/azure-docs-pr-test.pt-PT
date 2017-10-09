## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Especificar a definição de estrutura para conjuntos de dados retangular
Olá secção estrutura Olá conjuntos de dados JSON é uma **opcional** secção para tabelas retangular (com linhas e colunas) e contém uma coleção de colunas da tabela de Olá. Irá utilizar a secção de estrutura de Olá para qualquer um com informações de tipo para conversões de tipo ou fazer mapeamentos da coluna. Olá seguintes secções descreve estas funcionalidades em detalhe. 

Cada coluna contém Olá seguintes propriedades:

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| nome |Nome da coluna de Olá. |Sim |
| tipo |Tipo de dados da coluna de Olá. Consulte a secção de conversões de tipo abaixo para mais detalhes sobre quando deve especificar as informações de tipo |Não |
| Cultura |.NET com base toobe culture utilizada quando o tipo for especificado, não sendo tipo .NET Datetime ou Datetimeoffset. Predefinição é "en-us". |Não |
| formato |Formato toobe cadeia utilizada quando o tipo for especificado, não sendo tipo .NET Datetime ou Datetimeoffset. |Não |

Olá exemplo seguinte mostra secção de estrutura de Olá JSON para uma tabela que tem três colunas userid, o nome e lastlogindate.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Utilize Olá seguir as diretrizes para quando as informações de "estrutura" tooinclude e que tooinclude no Olá **estrutura** secção.

* **Para origens de dados estruturados** que armazenar informações de esquema e o tipo de dados, juntamente com Olá dados propriamente ditos (origens, como a tabela do Azure do SQL Server, Oracle, etc.), deve especificar a secção de "estrutura" Olá, apenas se pretender que efetue o mapeamento de colunas de específico não são de colunas de toospecific no sink e os respetivos nomes de colunas de origem Olá mesmo (consulte os detalhes na secção de mapeamento de coluna abaixo). 
  
    Tal como mencionado acima, as informações de tipo Olá são opcionais na secção "estrutura". Para origens de structured, informações de tipo já se encontra disponíveis como parte da definição de conjunto de dados no arquivo de dados de Olá, por isso, não deve incluir informações sobre o tipo ao incluir secção de "estrutura" Olá.
* **Para o esquema em origens de dados de leitura (especificamente BLOBs do Azure)** pode escolher toostore dados sem armazenar quaisquer informações de esquema ou tipo de dados de Olá. Para estes tipos de origens de dados deve incluir "estrutura" Olá 2 casos os seguintes:
  * Pretende que o mapeamento de colunas toodo.
  * Quando o conjunto de dados de Olá é uma origem de uma atividade de cópia, pode fornecer informações sobre o tipo de "estrutura" e fábrica de dados utilizará estas informações de tipo para tipos de toonative de conversão para sink Olá. Consulte [mover tooand de dados de Blobs do Azure](../articles/data-factory/data-factory-azure-blob-connector.md) artigo para obter mais informações.

### <a name="supported-net-based-types"></a>Suportado. Tipos de rede
Olá suporta fábrica de dados .NET em conformidade com CLS a seguir com base em valores de tipo para fornecer informações de tipo na "estrutura" para o esquema em origens de dados de leitura, como o blob do Azure.

* Int16
* Int32 
* Int64
* Único
* duplo
* Decimal
* Byte]
* bool
* Cadeia 
* GUID
* DateTime
* Datetimeoffset
* Timespan 

Para Datetime & Datetimeoffset, também pode especificar opcionalmente "Cultura" & "format" cadeia toofacilitate analisar a cadeia de Datetime personalizada. Consulte o exemplo para a conversão de tipo abaixo.

