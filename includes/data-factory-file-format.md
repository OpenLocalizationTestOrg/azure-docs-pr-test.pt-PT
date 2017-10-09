## <a name="specifying-formats"></a>Especificar formatos
O Azure Data Factory suporta Olá formato tipos seguintes:

* [Formato de Texto](#specifying-textformat)
* [Formato JSON](#specifying-jsonformat)
* [Formato Avro](#specifying-avroformat)
* [Formato ORC](#specifying-orcformat)
* [Formato Parquet](#specifying-parquetformat)

### <a name="specifying-textformat"></a>Especificar TextFormat
Se pretender que os ficheiros de texto de Olá tooparse ou escrever dados Olá no formato de texto, defina Olá `format` `type` propriedade demasiado**TextFormat**. Também pode especificar seguinte Olá **opcional** propriedades no Olá `format` secção. Consulte [TextFormat exemplo](#textformat-example) secção sobre como tooconfigure.

| Propriedade | Descrição | Valores permitidos | Necessário |
| --- | --- | --- | --- |
| columnDelimiter |caráter de Olá utilizado tooseparate colunas num ficheiro. Pode considerar a toouse um char unprintable raro que provavelmente não existe nos seus dados: por exemplo, especifique "\u0001" que representa o início do cabeçalho (SOH). |Só é permitido um caráter. Olá **predefinido** valor é **vírgulas (',')**. <br/><br/>toouse um caráter Unicode, consulte demasiado[carateres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget Olá código correspondente para o mesmo. |Não |
| rowDelimiter |caráter de Olá utilizado tooseparate linhas num ficheiro. |Só é permitido um caráter. Olá **predefinido** valor é qualquer um dos Olá os seguintes valores na leitura: **["\r\n", "\r", "\n"]** e **"\r\n"** na escrita. |Não |
| escapeChar |caráter especial Olá utilizado tooescape um delimitador de coluna no conteúdo de Olá do ficheiro de entrada. <br/><br/>Não pode especificar simultaneamente o escapeChar e o quoteChar para uma tabela. |Só é permitido um caráter. Não existem valores predefinidos. <br/><br/>Exemplo: Se tiver vírgulas (', ') como o delimitador de coluna Olá, mas pretende caráter de vírgulas Olá toohave no texto Olá (exemplo: "Olá, mundo"), pode definir '$' como caráter de escape Olá e utilizar a cadeia "$ de Olá, mundo" na origem de Olá. |Não |
| quoteChar |caráter de Olá utilizado tooquote um valor de cadeia. delimitadores de linha e coluna Olá dentro de carateres de aspas Olá teriam de ser tratados como parte do valor de cadeia Olá. Esta propriedade é aplicável tooboth entrada e saída de conjuntos de dados.<br/><br/>Não pode especificar simultaneamente o escapeChar e o quoteChar para uma tabela. |Só é permitido um caráter. Não existem valores predefinidos. <br/><br/>Por exemplo, se tiver vírgulas (', ') como o delimitador de coluna Olá, mas pretende toohave caráter de vírgulas no texto Olá (exemplo: < Olá, mundo >), pode definir "(aspas) como Olá caráter da plica e utilizar Olá cadeia"Olá, mundo"na origem de Olá. |Não |
| nullValue |Um ou mais carateres utilizado toorepresent um valor nulo. |Um ou mais carateres. Olá **predefinido** os valores são **"\N" e "NULL"** na leitura e **"\N"** na escrita. |Não |
| encodingName |Especifique o nome de codificação Olá. |Um nome de codificação válido. Veja [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx). Exemplo: windows-1250 ou shift_jis. Olá **predefinido** valor é **UTF-8**. |Não |
| firstRowAsHeader |Especifica se tooconsider Olá primeira linha como um cabeçalho. Num conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho. Num conjunto de dados de saída, o Data Factory escreve a primeira linha como cabeçalho. <br/><br/>Veja [Cenários para utilizar `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) em cenários de exemplo. |Verdadeiro<br/>**Falso (predefinição)** |Não |
| skipLineCount |Indica o número de Olá de linhas tooskip ao ler dados a partir dos ficheiros de entrada. Se forem especificadas skipLineCount e firstRowAsHeader, linhas de Olá são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de Olá é ler a partir do ficheiro de entrada Olá. <br/><br/>Veja [Cenários para utilizar `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) em cenários de exemplo. |Número inteiro |Não |
| treatEmptyAsNull |Especifica se uma cadeia nula ou vazia tootreat como um valor nulo valor quando a leitura de dados a partir de um ficheiro de entrada. |**Verdadeiro (predefinição)**<br/>Falso |Não |

#### <a name="textformat-example"></a>Exemplo de TextFormat
Olá exemplo seguinte mostra algumas das propriedades de formato Olá para TextFormat.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse um `escapeChar` em vez de `quoteChar`, substitua a linha de Olá `quoteChar` com Olá escapeChar os seguintes:

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Cenários para utilizar firstRowAsHeader e skipLineCount
* Está a copiar um ficheiro de texto do ficheiro não origem tooa e gostaria de tooadd uma linha de cabeçalho que contém os metadados do esquema de Olá (por exemplo: esquema de SQL Server). Especifique `firstRowAsHeader` como verdadeiro no conjunto de dados de saída de Olá para este cenário.
* Está a copiar um ficheiro de texto que contenha um receptor de ficheiro não de tooa de linha de cabeçalho e gostaria de toodrop linha. Especifique `firstRowAsHeader` como verdadeiro no conjunto de dados de entrada Olá.
* Está a copiar um ficheiro de texto e pretender tooskip algumas linhas no início de Olá que não contêm nenhuma informação de dados ou o cabeçalho. Especifique `skipLineCount` tooindicate Olá diversas toobe de linhas ignorado. Se o resto Olá ficheiro Olá contém uma linha de cabeçalho, também pode especificar `firstRowAsHeader`. Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de Olá são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de Olá é ler a partir do ficheiro de entrada Olá

### <a name="specifying-jsonformat"></a>Especificar JsonFormat
demasiado**importar/exportar ficheiros JSON como-é na/da base de dados do Azure Cosmos**, consulte [documentos JSON de importação/exportação](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) secção em conector de base de dados do Azure Cosmos Olá com detalhes.

Se pretender que os ficheiros JSON do tooparse Olá ou escrever dados Olá no formato JSON, defina Olá `format` `type` propriedade demasiado**JsonFormat**. Também pode especificar seguinte Olá **opcional** propriedades no Olá `format` secção. Consulte [JsonFormat exemplo](#jsonformat-example) secção sobre como tooconfigure.

| Propriedade | Descrição | Necessário |
| --- | --- | --- |
| filePattern |Indica o padrão de Olá dos dados armazenados em cada ficheiro JSON. Os valores permitidos são **setOfObjects** e **arrayOfObjects**. Olá **predefinido** valor é **setOfObjects**. Veja a secção [Padrões de ficheiro JSON](#json-file-patterns) para obter detalhes sobre estes padrões. |Não |
| jsonNodeReference | Se pretende tooiterate e extrair dados de objetos de Olá no interior de uma matriz de campo com Olá mesmo padrão, especifique um caminho JSON Olá dessa matriz. Esta propriedade só é suportada quando se copiam dados a partir de ficheiros JSON. | Não |
| jsonPathDefinition | Especifique a expressão de caminho JSON Olá para cada mapeamento de colunas com um nome de coluna personalizado (início com minúsculas). Esta propriedade só é suportada quando se copiam dados a partir de ficheiros JSON, sendo que pode extrair dados de objetos ou matrizes. <br/><br/> Para os campos no objeto raiz, comece com raiz $; para os campos dentro da matriz de Olá escolhido por `jsonNodeReference` propriedade, o início do elemento de matriz Olá. Consulte [JsonFormat exemplo](#jsonformat-example) secção sobre como tooconfigure. | Não |
| encodingName |Especifique o nome de codificação Olá. Para Olá lista de nomes válidos de codificação, consulte: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade. Exemplo: windows-1250 ou shift_jis. Olá **predefinido** valor é: **UTF-8**. |Não |
| nestingSeparator |Caráter é utilizado tooseparate níveis de aninhamento. valor predefinido de Olá é '.' (ponto final). |Não |

#### <a name="json-file-patterns"></a>Padrões de ficheiro JSON

A atividade de cópia pode analisar os seguintes padrões de ficheiros JSON:

- **Tipo I: setOfObjects**

    Cada ficheiro contém um único objeto ou múltiplos objetos delimitados por linha/concatenados. Quando esta opção está selecionada num conjunto de dados de saída, a atividade de cópia produz um único ficheiro JSON com cada objeto por linha (delimitados por linha).

    * **Exemplo de JSON de objeto único**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **Exemplo de JSON delimitado por linha**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **Exemplo de JSON concatenado**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Tipo II: arrayOfObjects**

    Cada ficheiro contém uma matriz de objetos.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a>Exemplo de JsonFormat

**Caso 1: Copiar dados de ficheiros JSON**

Veja a seguir dois tipos de amostras quando copiar dados de ficheiros JSON e Olá toonote pontos genérico:

**Exemplo 1: extrair dados de objeto e matriz**

Neste exemplo, o que esperar um objeto JSON raiz mapeia toosingle registo no resultado da tabela. Se tiver um ficheiro JSON com Olá seguinte conteúdo:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
e pretende toocopy para uma tabela de SQL do Azure da seguinte Olá formatar, extraindo os dados de objetos e a matriz de:

| ID | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

conjunto de dados de entrada Olá com **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes). Mais especificamente:

- `structure`secção define os nomes das colunas de Olá personalizada e tipo de dados correspondente Olá durante a conversão de dados de tootabular. Esta secção se **opcional** não ser que necessite toodo mapeamento de colunas. Veja a secção [Specifying structure definition for rectangular datasets{ (Especificar a definição da estrutura para conjuntos de dados retangulares)](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.
- `jsonPathDefinition`Especifica o caminho JSON Olá para cada coluna indica onde tooextract Olá dados a partir de. dados de toocopy da matriz, pode utilizar **matriz [x] .property** valor tooextract Olá fornecido a propriedade do objeto de xth hello, ou pode utilizar  **matriz [*] .property** toofind valor de Olá de qualquer objeto que contém essa propriedade.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Exemplo 2: cruzada aplicar vários objetos com o mesmo padrão da matriz de Olá**

Neste exemplo, o que esperar tootransform um objeto JSON de raiz para vários registos num resultado de tabela. Se tiver um ficheiro JSON com Olá seguinte conteúdo:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
e pretende toocopy para uma tabela de SQL do Azure da seguinte Olá formatar, pelo dados Olá dentro Olá matriz e associação com informações de raiz comuns Olá cruzada:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

conjunto de dados de entrada Olá com **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes). Mais especificamente:

- `structure`secção define os nomes das colunas de Olá personalizada e tipo de dados correspondente Olá durante a conversão de dados de tootabular. Esta secção se **opcional** não ser que necessite toodo mapeamento de colunas. Veja a secção [Specifying structure definition for rectangular datasets{ (Especificar a definição da estrutura para conjuntos de dados retangulares)](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.
- `jsonNodeReference`indica tooiterate e extrair dados de objetos de Olá com Olá sob o mesmo padrão **matriz** orderlines.
- `jsonPathDefinition`Especifica o caminho JSON Olá para cada coluna indica onde tooextract Olá dados a partir de. Neste exemplo, "ordernumber", "orderdate" e "Cidade" estão sob o objecto raiz com o caminho JSON, começando com "$".", enquanto"order_pd"e"order_price"estão definidas com o caminho derivado do elemento de matriz Olá sem"$"..

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Tenha em atenção Olá seguintes pontos:**

* Se hello `structure` e `jsonPathDefinition` não estão definidas no conjunto de dados de Data Factory Olá hello atividade de cópia Deteta Olá o esquema do objeto primeiro Olá e aplanar objeto Olá de todo.
* Se a entrada JSON Olá tem uma matriz, por predefinição Olá atividade de cópia converte Olá matriz todo valor numa cadeia. Pode escolhê-la utilizando dados tooextract `jsonNodeReference` e/ou `jsonPathDefinition`, ou ignore-lo especificando um não-lo na `jsonPathDefinition`.
* Se existirem duplicado Olá de nomes no mesmo nível, Olá atividade de cópia escolhe Olá último.
* Os nomes das propriedades são sensíveis às maiúsculas e minúsculas. Duas propriedades que tenham o mesmo nome, mas maiúsculas/minúsculas diferentes, são tratadas como duas propriedades separadas.

**Caso 2: Ao escrever no ficheiro de dados de tooJSON**

Se tiver a tabela abaixo na Base de Dados SQL:

| ID | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | José |
| 3 | 20170121 | 4000 | João |

e para cada registo, o que esperar toowrite tooa um objeto JSON no formato abaixo:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

com o conjunto de dados de saída de Olá **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes). Mais especificamente, `structure` secção define os nomes de propriedade Olá personalizado no ficheiro de destino, `nestingSeparator` (predefinição é ".") será utilizado tooidentify camada de nest Olá do nome de Olá. Esta secção se **opcional** , a menos que pretende o nome da propriedade toochange Olá comparar com o nome de coluna de origem ou aninhar algumas das propriedades de Olá.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a>Especificar AvroFormat
Se pretender que os ficheiros do Avro de Olá tooparse ou escrever dados de Olá no formato Avro, defina Olá `format` `type` propriedade demasiado**AvroFormat**. Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá. Exemplo:

```json
"format":
{
    "type": "AvroFormat",
}
```

formato de Avro toouse numa tabela do Hive, pode consultar demasiado[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Tenha em atenção Olá seguintes pontos:  

* Os [tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) não são suportados (registos, enumerações, matrizes, mapas, uniões e fixo).

### <a name="specifying-orcformat"></a>Especificar OrcFormat
Se pretender ficheiros do tooparse Olá ORC ou escrever dados Olá no formato ORC, defina Olá `format` `type` propriedade demasiado**OrcFormat**. Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá. Exemplo:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> Se não estiver a copiar ficheiros ORC **como-é** entre no local e nuvem arquivos de dados, terá de tooinstall Olá JRE 8 (ambiente de tempo de execução Java) no seu computador de gateway. Um gateway de 64 bits requer um JRE de 64 bits e um gateway de 32 bits requer um JRE de 32 bits. Pode encontrar ambas as versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605). Escolha Olá adequado.
>
>

Tenha em atenção Olá seguintes pontos:

* Os tipos de dados complexos não são suportados (ESTRUTURA, MAPA, LISTA, UNIÃO)
* O ficheiro ORC tem três [opções relacionadas com a compressão](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NENHUM, ZLIB, SNAPPY. O Data Factory suporta a leitura de dados a partir de um ficheiro ORC em qualquer um destes formatos de compressão. Utiliza a compressão de Olá codec está nos dados de Olá Olá metadados tooread. No entanto, ao escrever o ficheiro ORC tooan, Data Factory escolhe ZLIB, que é a predefinição de Olá para ORC. Atualmente, não há nenhuma opção toooverride este comportamento.

### <a name="specifying-parquetformat"></a>Especificar ParquetFormat
Se pretender que os ficheiros do tooparse Olá Parquet ou escrever dados Olá no formato Parquet, defina Olá `format` `type` propriedade demasiado**ParquetFormat**. Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá. Exemplo:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> Se não estiver a copiar ficheiros Parquet **como-é** entre no local e nuvem arquivos de dados, terá de tooinstall Olá JRE 8 (ambiente de tempo de execução Java) no seu computador de gateway. Um gateway de 64 bits requer um JRE de 64 bits e um gateway de 32 bits requer um JRE de 32 bits. Pode encontrar ambas as versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605). Escolha Olá adequado.
>
>

Tenha em atenção Olá seguintes pontos:

* Os tipos de dados complexos não são suportados (MAPA, LISTA)
* Ficheiro de parquet tem Olá seguintes opções relacionadas com compressão: NONE, SNAPPY, GZIP e LZO. O Data Factory suporta a leitura de dados a partir de um ficheiro ORC em qualquer um destes formatos de compressão. Utiliza codec de compressão Olá nos dados de Olá Olá metadados tooread. No entanto, ao escrever o ficheiro de Parquet tooa, Data Factory escolhe SNAPPY, que é Olá predefinido para o formato de Parquet. Atualmente, não há nenhuma opção toooverride este comportamento.
