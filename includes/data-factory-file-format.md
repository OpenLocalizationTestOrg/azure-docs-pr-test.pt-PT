## <a name="specifying-formats"></a><span data-ttu-id="c93b8-101">Especificar formatos</span><span class="sxs-lookup"><span data-stu-id="c93b8-101">Specifying formats</span></span>
<span data-ttu-id="c93b8-102">O Azure Data Factory suporta Olá formato tipos seguintes:</span><span class="sxs-lookup"><span data-stu-id="c93b8-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="c93b8-103">Formato de Texto</span><span class="sxs-lookup"><span data-stu-id="c93b8-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="c93b8-104">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="c93b8-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="c93b8-105">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="c93b8-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="c93b8-106">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="c93b8-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="c93b8-107">Formato Parquet</span><span class="sxs-lookup"><span data-stu-id="c93b8-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="c93b8-108">Especificar TextFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-108">Specifying TextFormat</span></span>
<span data-ttu-id="c93b8-109">Se pretender que os ficheiros de texto de Olá tooparse ou escrever dados Olá no formato de texto, defina Olá `format` `type` propriedade demasiado**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="c93b8-110">Também pode especificar seguinte Olá **opcional** propriedades no Olá `format` secção.</span><span class="sxs-lookup"><span data-stu-id="c93b8-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="c93b8-111">Consulte [TextFormat exemplo](#textformat-example) secção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c93b8-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="c93b8-112">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c93b8-112">Property</span></span> | <span data-ttu-id="c93b8-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="c93b8-113">Description</span></span> | <span data-ttu-id="c93b8-114">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="c93b8-114">Allowed values</span></span> | <span data-ttu-id="c93b8-115">Necessário</span><span class="sxs-lookup"><span data-stu-id="c93b8-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c93b8-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c93b8-116">columnDelimiter</span></span> |<span data-ttu-id="c93b8-117">caráter de Olá utilizado tooseparate colunas num ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c93b8-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="c93b8-118">Pode considerar a toouse um char unprintable raro que provavelmente não existe nos seus dados: por exemplo, especifique "\u0001" que representa o início do cabeçalho (SOH).</span><span class="sxs-lookup"><span data-stu-id="c93b8-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="c93b8-119">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="c93b8-119">Only one character is allowed.</span></span> <span data-ttu-id="c93b8-120">Olá **predefinido** valor é **vírgulas (',')**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="c93b8-121">toouse um caráter Unicode, consulte demasiado[carateres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget Olá código correspondente para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="c93b8-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="c93b8-122">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-122">No</span></span> |
| <span data-ttu-id="c93b8-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="c93b8-123">rowDelimiter</span></span> |<span data-ttu-id="c93b8-124">caráter de Olá utilizado tooseparate linhas num ficheiro.</span><span class="sxs-lookup"><span data-stu-id="c93b8-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="c93b8-125">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="c93b8-125">Only one character is allowed.</span></span> <span data-ttu-id="c93b8-126">Olá **predefinido** valor é qualquer um dos Olá os seguintes valores na leitura: **["\r\n", "\r", "\n"]** e **"\r\n"** na escrita.</span><span class="sxs-lookup"><span data-stu-id="c93b8-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="c93b8-127">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-127">No</span></span> |
| <span data-ttu-id="c93b8-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="c93b8-128">escapeChar</span></span> |<span data-ttu-id="c93b8-129">caráter especial Olá utilizado tooescape um delimitador de coluna no conteúdo de Olá do ficheiro de entrada.</span><span class="sxs-lookup"><span data-stu-id="c93b8-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="c93b8-130">Não pode especificar simultaneamente o escapeChar e o quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c93b8-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="c93b8-131">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="c93b8-131">Only one character is allowed.</span></span> <span data-ttu-id="c93b8-132">Não existem valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="c93b8-132">No default value.</span></span> <br/><br/><span data-ttu-id="c93b8-133">Exemplo: Se tiver vírgulas (', ') como o delimitador de coluna Olá, mas pretende caráter de vírgulas Olá toohave no texto Olá (exemplo: "Olá, mundo"), pode definir '$' como caráter de escape Olá e utilizar a cadeia "$ de Olá, mundo" na origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="c93b8-134">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-134">No</span></span> |
| <span data-ttu-id="c93b8-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="c93b8-135">quoteChar</span></span> |<span data-ttu-id="c93b8-136">caráter de Olá utilizado tooquote um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="c93b8-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="c93b8-137">delimitadores de linha e coluna Olá dentro de carateres de aspas Olá teriam de ser tratados como parte do valor de cadeia Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="c93b8-138">Esta propriedade é aplicável tooboth entrada e saída de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="c93b8-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="c93b8-139">Não pode especificar simultaneamente o escapeChar e o quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c93b8-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="c93b8-140">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="c93b8-140">Only one character is allowed.</span></span> <span data-ttu-id="c93b8-141">Não existem valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="c93b8-141">No default value.</span></span> <br/><br/><span data-ttu-id="c93b8-142">Por exemplo, se tiver vírgulas (', ') como o delimitador de coluna Olá, mas pretende toohave caráter de vírgulas no texto Olá (exemplo: < Olá, mundo >), pode definir "(aspas) como Olá caráter da plica e utilizar Olá cadeia"Olá, mundo"na origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="c93b8-143">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-143">No</span></span> |
| <span data-ttu-id="c93b8-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="c93b8-144">nullValue</span></span> |<span data-ttu-id="c93b8-145">Um ou mais carateres utilizado toorepresent um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="c93b8-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="c93b8-146">Um ou mais carateres.</span><span class="sxs-lookup"><span data-stu-id="c93b8-146">One or more characters.</span></span> <span data-ttu-id="c93b8-147">Olá **predefinido** os valores são **"\N" e "NULL"** na leitura e **"\N"** na escrita.</span><span class="sxs-lookup"><span data-stu-id="c93b8-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="c93b8-148">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-148">No</span></span> |
| <span data-ttu-id="c93b8-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="c93b8-149">encodingName</span></span> |<span data-ttu-id="c93b8-150">Especifique o nome de codificação Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-150">Specify hello encoding name.</span></span> |<span data-ttu-id="c93b8-151">Um nome de codificação válido.</span><span class="sxs-lookup"><span data-stu-id="c93b8-151">A valid encoding name.</span></span> <span data-ttu-id="c93b8-152">Veja [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="c93b8-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="c93b8-153">Exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="c93b8-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="c93b8-154">Olá **predefinido** valor é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="c93b8-155">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-155">No</span></span> |
| <span data-ttu-id="c93b8-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="c93b8-156">firstRowAsHeader</span></span> |<span data-ttu-id="c93b8-157">Especifica se tooconsider Olá primeira linha como um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="c93b8-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="c93b8-158">Num conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="c93b8-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="c93b8-159">Num conjunto de dados de saída, o Data Factory escreve a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="c93b8-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="c93b8-160">Veja [Cenários para utilizar `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) em cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c93b8-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="c93b8-161">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="c93b8-161">True</span></span><br/><span data-ttu-id="c93b8-162">**Falso (predefinição)**</span><span class="sxs-lookup"><span data-stu-id="c93b8-162">**False (default)**</span></span> |<span data-ttu-id="c93b8-163">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-163">No</span></span> |
| <span data-ttu-id="c93b8-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="c93b8-164">skipLineCount</span></span> |<span data-ttu-id="c93b8-165">Indica o número de Olá de linhas tooskip ao ler dados a partir dos ficheiros de entrada.</span><span class="sxs-lookup"><span data-stu-id="c93b8-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="c93b8-166">Se forem especificadas skipLineCount e firstRowAsHeader, linhas de Olá são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de Olá é ler a partir do ficheiro de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="c93b8-167">Veja [Cenários para utilizar `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) em cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c93b8-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="c93b8-168">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c93b8-168">Integer</span></span> |<span data-ttu-id="c93b8-169">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-169">No</span></span> |
| <span data-ttu-id="c93b8-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="c93b8-170">treatEmptyAsNull</span></span> |<span data-ttu-id="c93b8-171">Especifica se uma cadeia nula ou vazia tootreat como um valor nulo valor quando a leitura de dados a partir de um ficheiro de entrada.</span><span class="sxs-lookup"><span data-stu-id="c93b8-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="c93b8-172">**Verdadeiro (predefinição)**</span><span class="sxs-lookup"><span data-stu-id="c93b8-172">**True (default)**</span></span><br/><span data-ttu-id="c93b8-173">Falso</span><span class="sxs-lookup"><span data-stu-id="c93b8-173">False</span></span> |<span data-ttu-id="c93b8-174">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="c93b8-175">Exemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-175">TextFormat example</span></span>
<span data-ttu-id="c93b8-176">Olá exemplo seguinte mostra algumas das propriedades de formato Olá para TextFormat.</span><span class="sxs-lookup"><span data-stu-id="c93b8-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="c93b8-177">toouse um `escapeChar` em vez de `quoteChar`, substitua a linha de Olá `quoteChar` com Olá escapeChar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c93b8-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="c93b8-178">Cenários para utilizar firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="c93b8-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="c93b8-179">Está a copiar um ficheiro de texto do ficheiro não origem tooa e gostaria de tooadd uma linha de cabeçalho que contém os metadados do esquema de Olá (por exemplo: esquema de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="c93b8-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="c93b8-180">Especifique `firstRowAsHeader` como verdadeiro no conjunto de dados de saída de Olá para este cenário.</span><span class="sxs-lookup"><span data-stu-id="c93b8-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="c93b8-181">Está a copiar um ficheiro de texto que contenha um receptor de ficheiro não de tooa de linha de cabeçalho e gostaria de toodrop linha.</span><span class="sxs-lookup"><span data-stu-id="c93b8-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="c93b8-182">Especifique `firstRowAsHeader` como verdadeiro no conjunto de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="c93b8-183">Está a copiar um ficheiro de texto e pretender tooskip algumas linhas no início de Olá que não contêm nenhuma informação de dados ou o cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="c93b8-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="c93b8-184">Especifique `skipLineCount` tooindicate Olá diversas toobe de linhas ignorado.</span><span class="sxs-lookup"><span data-stu-id="c93b8-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="c93b8-185">Se o resto Olá ficheiro Olá contém uma linha de cabeçalho, também pode especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="c93b8-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="c93b8-186">Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de Olá são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de Olá é ler a partir do ficheiro de entrada Olá</span><span class="sxs-lookup"><span data-stu-id="c93b8-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="c93b8-187">Especificar JsonFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-187">Specifying JsonFormat</span></span>
<span data-ttu-id="c93b8-188">demasiado**importar/exportar ficheiros JSON como-é na/da base de dados do Azure Cosmos**, consulte [documentos JSON de importação/exportação](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) secção em conector de base de dados do Azure Cosmos Olá com detalhes.</span><span class="sxs-lookup"><span data-stu-id="c93b8-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="c93b8-189">Se pretender que os ficheiros JSON do tooparse Olá ou escrever dados Olá no formato JSON, defina Olá `format` `type` propriedade demasiado**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="c93b8-190">Também pode especificar seguinte Olá **opcional** propriedades no Olá `format` secção.</span><span class="sxs-lookup"><span data-stu-id="c93b8-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="c93b8-191">Consulte [JsonFormat exemplo](#jsonformat-example) secção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c93b8-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="c93b8-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c93b8-192">Property</span></span> | <span data-ttu-id="c93b8-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="c93b8-193">Description</span></span> | <span data-ttu-id="c93b8-194">Necessário</span><span class="sxs-lookup"><span data-stu-id="c93b8-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c93b8-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="c93b8-195">filePattern</span></span> |<span data-ttu-id="c93b8-196">Indica o padrão de Olá dos dados armazenados em cada ficheiro JSON.</span><span class="sxs-lookup"><span data-stu-id="c93b8-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="c93b8-197">Os valores permitidos são **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="c93b8-198">Olá **predefinido** valor é **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="c93b8-199">Veja a secção [Padrões de ficheiro JSON](#json-file-patterns) para obter detalhes sobre estes padrões.</span><span class="sxs-lookup"><span data-stu-id="c93b8-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="c93b8-200">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-200">No</span></span> |
| <span data-ttu-id="c93b8-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="c93b8-201">jsonNodeReference</span></span> | <span data-ttu-id="c93b8-202">Se pretende tooiterate e extrair dados de objetos de Olá no interior de uma matriz de campo com Olá mesmo padrão, especifique um caminho JSON Olá dessa matriz.</span><span class="sxs-lookup"><span data-stu-id="c93b8-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="c93b8-203">Esta propriedade só é suportada quando se copiam dados a partir de ficheiros JSON.</span><span class="sxs-lookup"><span data-stu-id="c93b8-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="c93b8-204">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-204">No</span></span> |
| <span data-ttu-id="c93b8-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="c93b8-205">jsonPathDefinition</span></span> | <span data-ttu-id="c93b8-206">Especifique a expressão de caminho JSON Olá para cada mapeamento de colunas com um nome de coluna personalizado (início com minúsculas).</span><span class="sxs-lookup"><span data-stu-id="c93b8-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="c93b8-207">Esta propriedade só é suportada quando se copiam dados a partir de ficheiros JSON, sendo que pode extrair dados de objetos ou matrizes.</span><span class="sxs-lookup"><span data-stu-id="c93b8-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="c93b8-208">Para os campos no objeto raiz, comece com raiz $; para os campos dentro da matriz de Olá escolhido por `jsonNodeReference` propriedade, o início do elemento de matriz Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="c93b8-209">Consulte [JsonFormat exemplo](#jsonformat-example) secção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="c93b8-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="c93b8-210">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-210">No</span></span> |
| <span data-ttu-id="c93b8-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="c93b8-211">encodingName</span></span> |<span data-ttu-id="c93b8-212">Especifique o nome de codificação Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-212">Specify hello encoding name.</span></span> <span data-ttu-id="c93b8-213">Para Olá lista de nomes válidos de codificação, consulte: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade.</span><span class="sxs-lookup"><span data-stu-id="c93b8-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="c93b8-214">Exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="c93b8-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="c93b8-215">Olá **predefinido** valor é: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="c93b8-216">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-216">No</span></span> |
| <span data-ttu-id="c93b8-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="c93b8-217">nestingSeparator</span></span> |<span data-ttu-id="c93b8-218">Caráter é utilizado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="c93b8-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="c93b8-219">valor predefinido de Olá é '.' (ponto final).</span><span class="sxs-lookup"><span data-stu-id="c93b8-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="c93b8-220">Não</span><span class="sxs-lookup"><span data-stu-id="c93b8-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="c93b8-221">Padrões de ficheiro JSON</span><span class="sxs-lookup"><span data-stu-id="c93b8-221">JSON file patterns</span></span>

<span data-ttu-id="c93b8-222">A atividade de cópia pode analisar os seguintes padrões de ficheiros JSON:</span><span class="sxs-lookup"><span data-stu-id="c93b8-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="c93b8-223">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="c93b8-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="c93b8-224">Cada ficheiro contém um único objeto ou múltiplos objetos delimitados por linha/concatenados.</span><span class="sxs-lookup"><span data-stu-id="c93b8-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="c93b8-225">Quando esta opção está selecionada num conjunto de dados de saída, a atividade de cópia produz um único ficheiro JSON com cada objeto por linha (delimitados por linha).</span><span class="sxs-lookup"><span data-stu-id="c93b8-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="c93b8-226">**Exemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="c93b8-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="c93b8-227">**Exemplo de JSON delimitado por linha**</span><span class="sxs-lookup"><span data-stu-id="c93b8-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="c93b8-228">**Exemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="c93b8-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="c93b8-229">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="c93b8-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="c93b8-230">Cada ficheiro contém uma matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="c93b8-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="c93b8-231">Exemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-231">JsonFormat example</span></span>

<span data-ttu-id="c93b8-232">**Caso 1: Copiar dados de ficheiros JSON**</span><span class="sxs-lookup"><span data-stu-id="c93b8-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="c93b8-233">Veja a seguir dois tipos de amostras quando copiar dados de ficheiros JSON e Olá toonote pontos genérico:</span><span class="sxs-lookup"><span data-stu-id="c93b8-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="c93b8-234">**Exemplo 1: extrair dados de objeto e matriz**</span><span class="sxs-lookup"><span data-stu-id="c93b8-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="c93b8-235">Neste exemplo, o que esperar um objeto JSON raiz mapeia toosingle registo no resultado da tabela.</span><span class="sxs-lookup"><span data-stu-id="c93b8-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="c93b8-236">Se tiver um ficheiro JSON com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="c93b8-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="c93b8-237">e pretende toocopy para uma tabela de SQL do Azure da seguinte Olá formatar, extraindo os dados de objetos e a matriz de:</span><span class="sxs-lookup"><span data-stu-id="c93b8-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="c93b8-238">ID</span><span class="sxs-lookup"><span data-stu-id="c93b8-238">id</span></span> | <span data-ttu-id="c93b8-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="c93b8-239">deviceType</span></span> | <span data-ttu-id="c93b8-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="c93b8-240">targetResourceType</span></span> | <span data-ttu-id="c93b8-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="c93b8-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="c93b8-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="c93b8-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c93b8-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="c93b8-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="c93b8-244">PC</span><span class="sxs-lookup"><span data-stu-id="c93b8-244">PC</span></span> | <span data-ttu-id="c93b8-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="c93b8-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="c93b8-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="c93b8-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="c93b8-247">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="c93b8-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="c93b8-248">conjunto de dados de entrada Olá com **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes).</span><span class="sxs-lookup"><span data-stu-id="c93b8-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="c93b8-249">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="c93b8-249">More specifically:</span></span>

- <span data-ttu-id="c93b8-250">`structure`secção define os nomes das colunas de Olá personalizada e tipo de dados correspondente Olá durante a conversão de dados de tootabular.</span><span class="sxs-lookup"><span data-stu-id="c93b8-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="c93b8-251">Esta secção se **opcional** não ser que necessite toodo mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="c93b8-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="c93b8-252">Veja a secção [Specifying structure definition for rectangular datasets{ (Especificar a definição da estrutura para conjuntos de dados retangulares)](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="c93b8-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="c93b8-253">`jsonPathDefinition`Especifica o caminho JSON Olá para cada coluna indica onde tooextract Olá dados a partir de.</span><span class="sxs-lookup"><span data-stu-id="c93b8-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="c93b8-254">dados de toocopy da matriz, pode utilizar **matriz [x] .property** valor tooextract Olá fornecido a propriedade do objeto de xth hello, ou pode utilizar  **matriz [*] .property** toofind valor de Olá de qualquer objeto que contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="c93b8-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="c93b8-255">**Exemplo 2: cruzada aplicar vários objetos com o mesmo padrão da matriz de Olá**</span><span class="sxs-lookup"><span data-stu-id="c93b8-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="c93b8-256">Neste exemplo, o que esperar tootransform um objeto JSON de raiz para vários registos num resultado de tabela.</span><span class="sxs-lookup"><span data-stu-id="c93b8-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="c93b8-257">Se tiver um ficheiro JSON com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="c93b8-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="c93b8-258">e pretende toocopy para uma tabela de SQL do Azure da seguinte Olá formatar, pelo dados Olá dentro Olá matriz e associação com informações de raiz comuns Olá cruzada:</span><span class="sxs-lookup"><span data-stu-id="c93b8-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="c93b8-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="c93b8-259">ordernumber</span></span> | <span data-ttu-id="c93b8-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="c93b8-260">orderdate</span></span> | <span data-ttu-id="c93b8-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="c93b8-261">order_pd</span></span> | <span data-ttu-id="c93b8-262">order_price</span><span class="sxs-lookup"><span data-stu-id="c93b8-262">order_price</span></span> | <span data-ttu-id="c93b8-263">city</span><span class="sxs-lookup"><span data-stu-id="c93b8-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c93b8-264">01</span><span class="sxs-lookup"><span data-stu-id="c93b8-264">01</span></span> | <span data-ttu-id="c93b8-265">20170122</span><span class="sxs-lookup"><span data-stu-id="c93b8-265">20170122</span></span> | <span data-ttu-id="c93b8-266">P1</span><span class="sxs-lookup"><span data-stu-id="c93b8-266">P1</span></span> | <span data-ttu-id="c93b8-267">23</span><span class="sxs-lookup"><span data-stu-id="c93b8-267">23</span></span> | <span data-ttu-id="c93b8-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="c93b8-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="c93b8-269">01</span><span class="sxs-lookup"><span data-stu-id="c93b8-269">01</span></span> | <span data-ttu-id="c93b8-270">20170122</span><span class="sxs-lookup"><span data-stu-id="c93b8-270">20170122</span></span> | <span data-ttu-id="c93b8-271">P2</span><span class="sxs-lookup"><span data-stu-id="c93b8-271">P2</span></span> | <span data-ttu-id="c93b8-272">13</span><span class="sxs-lookup"><span data-stu-id="c93b8-272">13</span></span> | <span data-ttu-id="c93b8-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="c93b8-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="c93b8-274">01</span><span class="sxs-lookup"><span data-stu-id="c93b8-274">01</span></span> | <span data-ttu-id="c93b8-275">20170122</span><span class="sxs-lookup"><span data-stu-id="c93b8-275">20170122</span></span> | <span data-ttu-id="c93b8-276">P3</span><span class="sxs-lookup"><span data-stu-id="c93b8-276">P3</span></span> | <span data-ttu-id="c93b8-277">231</span><span class="sxs-lookup"><span data-stu-id="c93b8-277">231</span></span> | <span data-ttu-id="c93b8-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="c93b8-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="c93b8-279">conjunto de dados de entrada Olá com **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes).</span><span class="sxs-lookup"><span data-stu-id="c93b8-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="c93b8-280">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="c93b8-280">More specifically:</span></span>

- <span data-ttu-id="c93b8-281">`structure`secção define os nomes das colunas de Olá personalizada e tipo de dados correspondente Olá durante a conversão de dados de tootabular.</span><span class="sxs-lookup"><span data-stu-id="c93b8-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="c93b8-282">Esta secção se **opcional** não ser que necessite toodo mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="c93b8-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="c93b8-283">Veja a secção [Specifying structure definition for rectangular datasets{ (Especificar a definição da estrutura para conjuntos de dados retangulares)](#specifying-structure-definition-for-rectangular-datasets) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="c93b8-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="c93b8-284">`jsonNodeReference`indica tooiterate e extrair dados de objetos de Olá com Olá sob o mesmo padrão **matriz** orderlines.</span><span class="sxs-lookup"><span data-stu-id="c93b8-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="c93b8-285">`jsonPathDefinition`Especifica o caminho JSON Olá para cada coluna indica onde tooextract Olá dados a partir de.</span><span class="sxs-lookup"><span data-stu-id="c93b8-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="c93b8-286">Neste exemplo, "ordernumber", "orderdate" e "Cidade" estão sob o objecto raiz com o caminho JSON, começando com "$".", enquanto"order_pd"e"order_price"estão definidas com o caminho derivado do elemento de matriz Olá sem"$"..</span><span class="sxs-lookup"><span data-stu-id="c93b8-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="c93b8-287">**Tenha em atenção Olá seguintes pontos:**</span><span class="sxs-lookup"><span data-stu-id="c93b8-287">**Note hello following points:**</span></span>

* <span data-ttu-id="c93b8-288">Se hello `structure` e `jsonPathDefinition` não estão definidas no conjunto de dados de Data Factory Olá hello atividade de cópia Deteta Olá o esquema do objeto primeiro Olá e aplanar objeto Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="c93b8-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="c93b8-289">Se a entrada JSON Olá tem uma matriz, por predefinição Olá atividade de cópia converte Olá matriz todo valor numa cadeia.</span><span class="sxs-lookup"><span data-stu-id="c93b8-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="c93b8-290">Pode escolhê-la utilizando dados tooextract `jsonNodeReference` e/ou `jsonPathDefinition`, ou ignore-lo especificando um não-lo na `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="c93b8-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="c93b8-291">Se existirem duplicado Olá de nomes no mesmo nível, Olá atividade de cópia escolhe Olá último.</span><span class="sxs-lookup"><span data-stu-id="c93b8-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="c93b8-292">Os nomes das propriedades são sensíveis às maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c93b8-292">Property names are case-sensitive.</span></span> <span data-ttu-id="c93b8-293">Duas propriedades que tenham o mesmo nome, mas maiúsculas/minúsculas diferentes, são tratadas como duas propriedades separadas.</span><span class="sxs-lookup"><span data-stu-id="c93b8-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="c93b8-294">**Caso 2: Ao escrever no ficheiro de dados de tooJSON**</span><span class="sxs-lookup"><span data-stu-id="c93b8-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="c93b8-295">Se tiver a tabela abaixo na Base de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="c93b8-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="c93b8-296">ID</span><span class="sxs-lookup"><span data-stu-id="c93b8-296">id</span></span> | <span data-ttu-id="c93b8-297">order_date</span><span class="sxs-lookup"><span data-stu-id="c93b8-297">order_date</span></span> | <span data-ttu-id="c93b8-298">order_price</span><span class="sxs-lookup"><span data-stu-id="c93b8-298">order_price</span></span> | <span data-ttu-id="c93b8-299">order_by</span><span class="sxs-lookup"><span data-stu-id="c93b8-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c93b8-300">1</span><span class="sxs-lookup"><span data-stu-id="c93b8-300">1</span></span> | <span data-ttu-id="c93b8-301">20170119</span><span class="sxs-lookup"><span data-stu-id="c93b8-301">20170119</span></span> | <span data-ttu-id="c93b8-302">2000</span><span class="sxs-lookup"><span data-stu-id="c93b8-302">2000</span></span> | <span data-ttu-id="c93b8-303">David</span><span class="sxs-lookup"><span data-stu-id="c93b8-303">David</span></span> |
| <span data-ttu-id="c93b8-304">2</span><span class="sxs-lookup"><span data-stu-id="c93b8-304">2</span></span> | <span data-ttu-id="c93b8-305">20170120</span><span class="sxs-lookup"><span data-stu-id="c93b8-305">20170120</span></span> | <span data-ttu-id="c93b8-306">3500</span><span class="sxs-lookup"><span data-stu-id="c93b8-306">3500</span></span> | <span data-ttu-id="c93b8-307">José</span><span class="sxs-lookup"><span data-stu-id="c93b8-307">Patrick</span></span> |
| <span data-ttu-id="c93b8-308">3</span><span class="sxs-lookup"><span data-stu-id="c93b8-308">3</span></span> | <span data-ttu-id="c93b8-309">20170121</span><span class="sxs-lookup"><span data-stu-id="c93b8-309">20170121</span></span> | <span data-ttu-id="c93b8-310">4000</span><span class="sxs-lookup"><span data-stu-id="c93b8-310">4000</span></span> | <span data-ttu-id="c93b8-311">João</span><span class="sxs-lookup"><span data-stu-id="c93b8-311">Jason</span></span> |

<span data-ttu-id="c93b8-312">e para cada registo, o que esperar toowrite tooa um objeto JSON no formato abaixo:</span><span class="sxs-lookup"><span data-stu-id="c93b8-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="c93b8-313">com o conjunto de dados de saída de Olá **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes).</span><span class="sxs-lookup"><span data-stu-id="c93b8-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="c93b8-314">Mais especificamente, `structure` secção define os nomes de propriedade Olá personalizado no ficheiro de destino, `nestingSeparator` (predefinição é ".") será utilizado tooidentify camada de nest Olá do nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="c93b8-315">Esta secção se **opcional** , a menos que pretende o nome da propriedade toochange Olá comparar com o nome de coluna de origem ou aninhar algumas das propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="c93b8-316">Especificar AvroFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-316">Specifying AvroFormat</span></span>
<span data-ttu-id="c93b8-317">Se pretender que os ficheiros do Avro de Olá tooparse ou escrever dados de Olá no formato Avro, defina Olá `format` `type` propriedade demasiado**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="c93b8-318">Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="c93b8-319">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c93b8-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="c93b8-320">formato de Avro toouse numa tabela do Hive, pode consultar demasiado[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="c93b8-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="c93b8-321">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="c93b8-321">Note hello following points:</span></span>  

* <span data-ttu-id="c93b8-322">Os [tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) não são suportados (registos, enumerações, matrizes, mapas, uniões e fixo).</span><span class="sxs-lookup"><span data-stu-id="c93b8-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="c93b8-323">Especificar OrcFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-323">Specifying OrcFormat</span></span>
<span data-ttu-id="c93b8-324">Se pretender ficheiros do tooparse Olá ORC ou escrever dados Olá no formato ORC, defina Olá `format` `type` propriedade demasiado**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="c93b8-325">Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="c93b8-326">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c93b8-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="c93b8-327">Se não estiver a copiar ficheiros ORC **como-é** entre no local e nuvem arquivos de dados, terá de tooinstall Olá JRE 8 (ambiente de tempo de execução Java) no seu computador de gateway.</span><span class="sxs-lookup"><span data-stu-id="c93b8-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="c93b8-328">Um gateway de 64 bits requer um JRE de 64 bits e um gateway de 32 bits requer um JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="c93b8-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="c93b8-329">Pode encontrar ambas as versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="c93b8-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="c93b8-330">Escolha Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="c93b8-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="c93b8-331">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="c93b8-331">Note hello following points:</span></span>

* <span data-ttu-id="c93b8-332">Os tipos de dados complexos não são suportados (ESTRUTURA, MAPA, LISTA, UNIÃO)</span><span class="sxs-lookup"><span data-stu-id="c93b8-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="c93b8-333">O ficheiro ORC tem três [opções relacionadas com a compressão](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NENHUM, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="c93b8-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="c93b8-334">O Data Factory suporta a leitura de dados a partir de um ficheiro ORC em qualquer um destes formatos de compressão.</span><span class="sxs-lookup"><span data-stu-id="c93b8-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="c93b8-335">Utiliza a compressão de Olá codec está nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="c93b8-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="c93b8-336">No entanto, ao escrever o ficheiro ORC tooan, Data Factory escolhe ZLIB, que é a predefinição de Olá para ORC.</span><span class="sxs-lookup"><span data-stu-id="c93b8-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="c93b8-337">Atualmente, não há nenhuma opção toooverride este comportamento.</span><span class="sxs-lookup"><span data-stu-id="c93b8-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="c93b8-338">Especificar ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="c93b8-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="c93b8-339">Se pretender que os ficheiros do tooparse Olá Parquet ou escrever dados Olá no formato Parquet, defina Olá `format` `type` propriedade demasiado**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c93b8-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="c93b8-340">Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá.</span><span class="sxs-lookup"><span data-stu-id="c93b8-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="c93b8-341">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c93b8-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="c93b8-342">Se não estiver a copiar ficheiros Parquet **como-é** entre no local e nuvem arquivos de dados, terá de tooinstall Olá JRE 8 (ambiente de tempo de execução Java) no seu computador de gateway.</span><span class="sxs-lookup"><span data-stu-id="c93b8-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="c93b8-343">Um gateway de 64 bits requer um JRE de 64 bits e um gateway de 32 bits requer um JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="c93b8-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="c93b8-344">Pode encontrar ambas as versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="c93b8-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="c93b8-345">Escolha Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="c93b8-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="c93b8-346">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="c93b8-346">Note hello following points:</span></span>

* <span data-ttu-id="c93b8-347">Os tipos de dados complexos não são suportados (MAPA, LISTA)</span><span class="sxs-lookup"><span data-stu-id="c93b8-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="c93b8-348">Ficheiro de parquet tem Olá seguintes opções relacionadas com compressão: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="c93b8-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="c93b8-349">O Data Factory suporta a leitura de dados a partir de um ficheiro ORC em qualquer um destes formatos de compressão.</span><span class="sxs-lookup"><span data-stu-id="c93b8-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="c93b8-350">Utiliza codec de compressão Olá nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="c93b8-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="c93b8-351">No entanto, ao escrever o ficheiro de Parquet tooa, Data Factory escolhe SNAPPY, que é Olá predefinido para o formato de Parquet.</span><span class="sxs-lookup"><span data-stu-id="c93b8-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="c93b8-352">Atualmente, não há nenhuma opção toooverride este comportamento.</span><span class="sxs-lookup"><span data-stu-id="c93b8-352">Currently, there is no option toooverride this behavior.</span></span>
