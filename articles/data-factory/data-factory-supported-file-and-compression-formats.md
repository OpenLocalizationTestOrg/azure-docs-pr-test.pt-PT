---
title: "formatos de aaaFile e compressão no Azure Data Factory | Microsoft Docs"
description: "Saiba mais sobre os formatos de ficheiro Olá suportados pelo Azure Data Factory."
keywords: "dados de BLOBs, cópia de Blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="a9e36-104">Formatos de ficheiro e compressão suportados pelo Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a9e36-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="a9e36-105">*Este tópico aplica-se toohello seguir conectores: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Blob do Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [sistema de ficheiros](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), e [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="a9e36-105">*This topic applies toohello following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="a9e36-106">O Azure Data Factory suporta Olá os seguintes tipos de ficheiro de formato:</span><span class="sxs-lookup"><span data-stu-id="a9e36-106">Azure Data Factory supports hello following file format types:</span></span>

* [<span data-ttu-id="a9e36-107">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="a9e36-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="a9e36-108">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="a9e36-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="a9e36-109">Formato Avro</span><span class="sxs-lookup"><span data-stu-id="a9e36-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="a9e36-110">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="a9e36-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="a9e36-111">Formato de parquet</span><span class="sxs-lookup"><span data-stu-id="a9e36-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="a9e36-112">Formato de texto</span><span class="sxs-lookup"><span data-stu-id="a9e36-112">Text format</span></span>
<span data-ttu-id="a9e36-113">Se pretender tooread de um ficheiro de texto ou escrever no ficheiro de texto tooa, defina Olá `type` propriedade no Olá `format` secção do conjunto de dados de Olá demasiado**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-113">If you want tooread from a text file or write tooa text file, set hello `type` property in hello `format` section of hello dataset too**TextFormat**.</span></span> <span data-ttu-id="a9e36-114">Também pode especificar seguinte Olá **opcional** propriedades no Olá `format` secção.</span><span class="sxs-lookup"><span data-stu-id="a9e36-114">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="a9e36-115">Consulte [TextFormat exemplo](#textformat-example) secção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-115">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="a9e36-116">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a9e36-116">Property</span></span> | <span data-ttu-id="a9e36-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="a9e36-117">Description</span></span> | <span data-ttu-id="a9e36-118">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="a9e36-118">Allowed values</span></span> | <span data-ttu-id="a9e36-119">Necessário</span><span class="sxs-lookup"><span data-stu-id="a9e36-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9e36-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="a9e36-120">columnDelimiter</span></span> |<span data-ttu-id="a9e36-121">caráter de Olá utilizado tooseparate colunas num ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a9e36-121">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="a9e36-122">Pode considerar toouse um char unprintable raro que poderão provavelmente não existe nos seus dados.</span><span class="sxs-lookup"><span data-stu-id="a9e36-122">You can consider toouse a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="a9e36-123">Por exemplo, especifique "\u0001", que representa o início do cabeçalho (SOH).</span><span class="sxs-lookup"><span data-stu-id="a9e36-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="a9e36-124">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="a9e36-124">Only one character is allowed.</span></span> <span data-ttu-id="a9e36-125">Olá **predefinido** valor é **vírgulas (',')**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-125">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="a9e36-126">toouse um caráter Unicode, consulte demasiado[carateres Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget Olá código correspondente para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-126">toouse a Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="a9e36-127">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-127">No</span></span> |
| <span data-ttu-id="a9e36-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="a9e36-128">rowDelimiter</span></span> |<span data-ttu-id="a9e36-129">caráter de Olá utilizado tooseparate linhas num ficheiro.</span><span class="sxs-lookup"><span data-stu-id="a9e36-129">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="a9e36-130">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="a9e36-130">Only one character is allowed.</span></span> <span data-ttu-id="a9e36-131">Olá **predefinido** valor é qualquer um dos Olá os seguintes valores na leitura: **["\r\n", "\r", "\n"]** e **"\r\n"** na escrita.</span><span class="sxs-lookup"><span data-stu-id="a9e36-131">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="a9e36-132">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-132">No</span></span> |
| <span data-ttu-id="a9e36-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="a9e36-133">escapeChar</span></span> |<span data-ttu-id="a9e36-134">caráter especial Olá utilizado tooescape um delimitador de coluna no conteúdo de Olá do ficheiro de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9e36-134">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="a9e36-135">Não pode especificar simultaneamente o escapeChar e o quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="a9e36-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="a9e36-136">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="a9e36-136">Only one character is allowed.</span></span> <span data-ttu-id="a9e36-137">Não existem valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="a9e36-137">No default value.</span></span> <br/><br/><span data-ttu-id="a9e36-138">Exemplo: Se tiver vírgulas (', ') como o delimitador de coluna Olá, mas pretende caráter de vírgulas Olá toohave no texto Olá (exemplo: "Olá, mundo"), pode definir '$' como caráter de escape Olá e utilizar a cadeia "$ de Olá, mundo" na origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-138">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="a9e36-139">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-139">No</span></span> |
| <span data-ttu-id="a9e36-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="a9e36-140">quoteChar</span></span> |<span data-ttu-id="a9e36-141">caráter de Olá utilizado tooquote um valor de cadeia.</span><span class="sxs-lookup"><span data-stu-id="a9e36-141">hello character used tooquote a string value.</span></span> <span data-ttu-id="a9e36-142">delimitadores de linha e coluna Olá dentro de carateres de aspas Olá teriam de ser tratados como parte do valor de cadeia Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-142">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="a9e36-143">Esta propriedade é aplicável tooboth entrada e saída de conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="a9e36-143">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="a9e36-144">Não pode especificar simultaneamente o escapeChar e o quoteChar para uma tabela.</span><span class="sxs-lookup"><span data-stu-id="a9e36-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="a9e36-145">Só é permitido um caráter.</span><span class="sxs-lookup"><span data-stu-id="a9e36-145">Only one character is allowed.</span></span> <span data-ttu-id="a9e36-146">Não existem valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="a9e36-146">No default value.</span></span> <br/><br/><span data-ttu-id="a9e36-147">Por exemplo, se tiver vírgulas (', ') como o delimitador de coluna Olá, mas pretende toohave caráter de vírgulas no texto Olá (exemplo: < Olá, mundo >), pode definir "(aspas) como Olá caráter da plica e utilizar Olá cadeia"Olá, mundo"na origem de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-147">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="a9e36-148">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-148">No</span></span> |
| <span data-ttu-id="a9e36-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="a9e36-149">nullValue</span></span> |<span data-ttu-id="a9e36-150">Um ou mais carateres utilizado toorepresent um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-150">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="a9e36-151">Um ou mais carateres.</span><span class="sxs-lookup"><span data-stu-id="a9e36-151">One or more characters.</span></span> <span data-ttu-id="a9e36-152">Olá **predefinido** os valores são **"\N" e "NULL"** na leitura e **"\N"** na escrita.</span><span class="sxs-lookup"><span data-stu-id="a9e36-152">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="a9e36-153">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-153">No</span></span> |
| <span data-ttu-id="a9e36-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="a9e36-154">encodingName</span></span> |<span data-ttu-id="a9e36-155">Especifique o nome de codificação Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-155">Specify hello encoding name.</span></span> |<span data-ttu-id="a9e36-156">Um nome de codificação válido.</span><span class="sxs-lookup"><span data-stu-id="a9e36-156">A valid encoding name.</span></span> <span data-ttu-id="a9e36-157">Veja [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9e36-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="a9e36-158">Exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="a9e36-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="a9e36-159">Olá **predefinido** valor é **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-159">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="a9e36-160">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-160">No</span></span> |
| <span data-ttu-id="a9e36-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="a9e36-161">firstRowAsHeader</span></span> |<span data-ttu-id="a9e36-162">Especifica se tooconsider Olá primeira linha como um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a9e36-162">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="a9e36-163">Num conjunto de dados de entrada, o Data Factory lê a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a9e36-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="a9e36-164">Num conjunto de dados de saída, o Data Factory escreve a primeira linha como cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a9e36-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="a9e36-165">Veja [Cenários para utilizar `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) em cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="a9e36-166">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="a9e36-166">True</span></span><br/><span data-ttu-id="a9e36-167"><b>Falso (predefinição)</b></span><span class="sxs-lookup"><span data-stu-id="a9e36-167"><b>False (default)</b></span></span> |<span data-ttu-id="a9e36-168">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-168">No</span></span> |
| <span data-ttu-id="a9e36-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="a9e36-169">skipLineCount</span></span> |<span data-ttu-id="a9e36-170">Indica o número de Olá de linhas tooskip ao ler dados a partir dos ficheiros de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9e36-170">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="a9e36-171">Se forem especificadas skipLineCount e firstRowAsHeader, linhas de Olá são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de Olá é ler a partir do ficheiro de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-171">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="a9e36-172">Veja [Cenários para utilizar `firstRowAsHeader` e `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) em cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="a9e36-173">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="a9e36-173">Integer</span></span> |<span data-ttu-id="a9e36-174">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-174">No</span></span> |
| <span data-ttu-id="a9e36-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="a9e36-175">treatEmptyAsNull</span></span> |<span data-ttu-id="a9e36-176">Especifica se uma cadeia nula ou vazia tootreat como um valor nulo valor quando a leitura de dados a partir de um ficheiro de entrada.</span><span class="sxs-lookup"><span data-stu-id="a9e36-176">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="a9e36-177">**Verdadeiro (predefinição)**</span><span class="sxs-lookup"><span data-stu-id="a9e36-177">**True (default)**</span></span><br/><span data-ttu-id="a9e36-178">Falso</span><span class="sxs-lookup"><span data-stu-id="a9e36-178">False</span></span> |<span data-ttu-id="a9e36-179">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="a9e36-180">Exemplo de TextFormat</span><span class="sxs-lookup"><span data-stu-id="a9e36-180">TextFormat example</span></span>
<span data-ttu-id="a9e36-181">No Olá seguinte definição JSON para um conjunto de dados, algumas das propriedades opcional Olá especificadas.</span><span class="sxs-lookup"><span data-stu-id="a9e36-181">In hello following JSON definition for a dataset, some of hello optional properties are specified.</span></span>

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

<span data-ttu-id="a9e36-182">toouse um `escapeChar` em vez de `quoteChar`, substitua a linha de Olá `quoteChar` com Olá escapeChar os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a9e36-182">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="a9e36-183">Cenários para utilizar firstRowAsHeader e skipLineCount</span><span class="sxs-lookup"><span data-stu-id="a9e36-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="a9e36-184">Está a copiar um ficheiro de texto do ficheiro não origem tooa e gostaria de tooadd uma linha de cabeçalho que contém os metadados do esquema de Olá (por exemplo: esquema de SQL Server).</span><span class="sxs-lookup"><span data-stu-id="a9e36-184">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="a9e36-185">Especifique `firstRowAsHeader` como verdadeiro no conjunto de dados de saída de Olá para este cenário.</span><span class="sxs-lookup"><span data-stu-id="a9e36-185">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="a9e36-186">Está a copiar um ficheiro de texto que contenha um receptor de ficheiro não de tooa de linha de cabeçalho e gostaria de toodrop linha.</span><span class="sxs-lookup"><span data-stu-id="a9e36-186">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="a9e36-187">Especifique `firstRowAsHeader` como verdadeiro no conjunto de dados de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-187">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="a9e36-188">Está a copiar um ficheiro de texto e pretender tooskip algumas linhas no início de Olá que não contêm nenhuma informação de dados ou o cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="a9e36-188">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="a9e36-189">Especifique `skipLineCount` tooindicate Olá diversas toobe de linhas ignorado.</span><span class="sxs-lookup"><span data-stu-id="a9e36-189">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="a9e36-190">Se o resto Olá ficheiro Olá contém uma linha de cabeçalho, também pode especificar `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="a9e36-190">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="a9e36-191">Se ambos os `skipLineCount` e `firstRowAsHeader` forem especificados, linhas de Olá são ignoradas pela primeira vez e, em seguida, as informações de cabeçalho de Olá é ler a partir do ficheiro de entrada Olá</span><span class="sxs-lookup"><span data-stu-id="a9e36-191">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

## <a name="json-format"></a><span data-ttu-id="a9e36-192">Formato JSON</span><span class="sxs-lookup"><span data-stu-id="a9e36-192">JSON format</span></span>
<span data-ttu-id="a9e36-193">demasiado**importar/exportar um ficheiro JSON como-é na/da base de dados do Azure Cosmos**, consulte Olá [documentos JSON de importação/exportação](data-factory-azure-documentdb-connector.md#importexport-json-documents) secção [mover os dados da base de dados do Azure Cosmos](data-factory-azure-documentdb-connector.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-193">too**import/export a JSON file as-is into/from Azure Cosmos DB**, hello see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="a9e36-194">Se pretender que os ficheiros JSON do tooparse Olá ou escrever dados Olá no formato JSON, defina Olá `type` propriedade no Olá `format` secção demasiado**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-194">If you want tooparse hello JSON files or write hello data in JSON format, set hello `type` property in hello `format` section too**JsonFormat**.</span></span> <span data-ttu-id="a9e36-195">Também pode especificar seguinte Olá **opcional** propriedades no Olá `format` secção.</span><span class="sxs-lookup"><span data-stu-id="a9e36-195">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="a9e36-196">Consulte [JsonFormat exemplo](#jsonformat-example) secção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-196">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="a9e36-197">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a9e36-197">Property</span></span> | <span data-ttu-id="a9e36-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="a9e36-198">Description</span></span> | <span data-ttu-id="a9e36-199">Necessário</span><span class="sxs-lookup"><span data-stu-id="a9e36-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9e36-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="a9e36-200">filePattern</span></span> |<span data-ttu-id="a9e36-201">Indica o padrão de Olá dos dados armazenados em cada ficheiro JSON.</span><span class="sxs-lookup"><span data-stu-id="a9e36-201">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="a9e36-202">Os valores permitidos são **setOfObjects** e **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="a9e36-203">Olá **predefinido** valor é **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-203">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="a9e36-204">Veja a secção [Padrões de ficheiro JSON](#json-file-patterns) para obter detalhes sobre estes padrões.</span><span class="sxs-lookup"><span data-stu-id="a9e36-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="a9e36-205">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-205">No</span></span> |
| <span data-ttu-id="a9e36-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="a9e36-206">jsonNodeReference</span></span> | <span data-ttu-id="a9e36-207">Se pretende tooiterate e extrair dados de objetos de Olá no interior de uma matriz de campo com Olá mesmo padrão, especifique um caminho JSON Olá dessa matriz.</span><span class="sxs-lookup"><span data-stu-id="a9e36-207">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="a9e36-208">Esta propriedade só é suportada quando se copiam dados a partir de ficheiros JSON.</span><span class="sxs-lookup"><span data-stu-id="a9e36-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="a9e36-209">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-209">No</span></span> |
| <span data-ttu-id="a9e36-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="a9e36-210">jsonPathDefinition</span></span> | <span data-ttu-id="a9e36-211">Especifique a expressão de caminho JSON Olá para cada mapeamento de colunas com um nome de coluna personalizado (início com minúsculas).</span><span class="sxs-lookup"><span data-stu-id="a9e36-211">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="a9e36-212">Esta propriedade só é suportada quando se copiam dados a partir de ficheiros JSON, sendo que pode extrair dados de objetos ou matrizes.</span><span class="sxs-lookup"><span data-stu-id="a9e36-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="a9e36-213">Para os campos no objeto raiz, comece com raiz $; para os campos dentro da matriz de Olá escolhido por `jsonNodeReference` propriedade, o início do elemento de matriz Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-213">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="a9e36-214">Consulte [JsonFormat exemplo](#jsonformat-example) secção sobre como tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-214">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="a9e36-215">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-215">No</span></span> |
| <span data-ttu-id="a9e36-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="a9e36-216">encodingName</span></span> |<span data-ttu-id="a9e36-217">Especifique o nome de codificação Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-217">Specify hello encoding name.</span></span> <span data-ttu-id="a9e36-218">Para Olá lista de nomes válidos de codificação, consulte: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriedade.</span><span class="sxs-lookup"><span data-stu-id="a9e36-218">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="a9e36-219">Exemplo: windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="a9e36-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="a9e36-220">Olá **predefinido** valor é: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-220">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="a9e36-221">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-221">No</span></span> |
| <span data-ttu-id="a9e36-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="a9e36-222">nestingSeparator</span></span> |<span data-ttu-id="a9e36-223">Caráter é utilizado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="a9e36-223">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="a9e36-224">valor predefinido de Olá é '.' (ponto final).</span><span class="sxs-lookup"><span data-stu-id="a9e36-224">hello default value is '.' (dot).</span></span> |<span data-ttu-id="a9e36-225">Não</span><span class="sxs-lookup"><span data-stu-id="a9e36-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="a9e36-226">Padrões de ficheiro JSON</span><span class="sxs-lookup"><span data-stu-id="a9e36-226">JSON file patterns</span></span>

<span data-ttu-id="a9e36-227">Atividade de cópia pode analisar Olá padrões de ficheiros JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="a9e36-227">Copy activity can parse hello following patterns of JSON files:</span></span>

- <span data-ttu-id="a9e36-228">**Tipo I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="a9e36-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="a9e36-229">Cada ficheiro contém um único objeto ou múltiplos objetos delimitados por linha/concatenados.</span><span class="sxs-lookup"><span data-stu-id="a9e36-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="a9e36-230">Quando esta opção está selecionada num conjunto de dados de saída, a atividade de cópia produz um único ficheiro JSON com cada objeto por linha (delimitados por linha).</span><span class="sxs-lookup"><span data-stu-id="a9e36-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="a9e36-231">**Exemplo de JSON de objeto único**</span><span class="sxs-lookup"><span data-stu-id="a9e36-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="a9e36-232">**Exemplo de JSON delimitado por linha**</span><span class="sxs-lookup"><span data-stu-id="a9e36-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="a9e36-233">**Exemplo de JSON concatenado**</span><span class="sxs-lookup"><span data-stu-id="a9e36-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="a9e36-234">**Tipo II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="a9e36-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="a9e36-235">Cada ficheiro contém uma matriz de objetos.</span><span class="sxs-lookup"><span data-stu-id="a9e36-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="a9e36-236">Exemplo de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="a9e36-236">JsonFormat example</span></span>

<span data-ttu-id="a9e36-237">**Caso 1: Copiar dados de ficheiros JSON**</span><span class="sxs-lookup"><span data-stu-id="a9e36-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="a9e36-238">Consulte Olá dois exemplos a seguir ao copiar dados de ficheiros JSON.</span><span class="sxs-lookup"><span data-stu-id="a9e36-238">See hello following two samples when copying data from JSON files.</span></span> <span data-ttu-id="a9e36-239">Olá genérico pontos toonote:</span><span class="sxs-lookup"><span data-stu-id="a9e36-239">hello generic points toonote:</span></span>

<span data-ttu-id="a9e36-240">**Exemplo 1: extrair dados de objeto e matriz**</span><span class="sxs-lookup"><span data-stu-id="a9e36-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="a9e36-241">Neste exemplo, o que esperar um objeto JSON raiz mapeia toosingle registo no resultado da tabela.</span><span class="sxs-lookup"><span data-stu-id="a9e36-241">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="a9e36-242">Se tiver um ficheiro JSON com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="a9e36-242">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="a9e36-243">e pretende toocopy para uma tabela de SQL do Azure da seguinte Olá formatar, extraindo os dados de objetos e a matriz de:</span><span class="sxs-lookup"><span data-stu-id="a9e36-243">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="a9e36-244">ID</span><span class="sxs-lookup"><span data-stu-id="a9e36-244">id</span></span> | <span data-ttu-id="a9e36-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="a9e36-245">deviceType</span></span> | <span data-ttu-id="a9e36-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="a9e36-246">targetResourceType</span></span> | <span data-ttu-id="a9e36-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="a9e36-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="a9e36-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="a9e36-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a9e36-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="a9e36-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="a9e36-250">PC</span><span class="sxs-lookup"><span data-stu-id="a9e36-250">PC</span></span> | <span data-ttu-id="a9e36-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="a9e36-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="a9e36-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="a9e36-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="a9e36-253">1/13/2017 11:24:37 AM</span><span class="sxs-lookup"><span data-stu-id="a9e36-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="a9e36-254">conjunto de dados de entrada Olá com **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes).</span><span class="sxs-lookup"><span data-stu-id="a9e36-254">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="a9e36-255">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="a9e36-255">More specifically:</span></span>

- <span data-ttu-id="a9e36-256">`structure`secção define os nomes das colunas de Olá personalizada e tipo de dados correspondente Olá durante a conversão de dados de tootabular.</span><span class="sxs-lookup"><span data-stu-id="a9e36-256">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="a9e36-257">Esta secção se **opcional** não ser que necessite toodo mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="a9e36-257">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="a9e36-258">Consulte [mapear colunas de conjunto de dados de toodestination de colunas de conjunto de dados de origem](data-factory-map-columns.md) secção para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a9e36-258">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="a9e36-259">`jsonPathDefinition`Especifica o caminho JSON Olá para cada coluna indica onde tooextract Olá dados a partir de.</span><span class="sxs-lookup"><span data-stu-id="a9e36-259">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="a9e36-260">dados de toocopy da matriz, pode utilizar **matriz [x] .property** valor tooextract Olá fornecido a propriedade do objeto de xth hello, ou pode utilizar  **matriz [*] .property** toofind valor de Olá de qualquer objeto que contém essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="a9e36-260">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="a9e36-261">**Exemplo 2: cruzada aplicar vários objetos com o mesmo padrão da matriz de Olá**</span><span class="sxs-lookup"><span data-stu-id="a9e36-261">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="a9e36-262">Neste exemplo, o que esperar tootransform um objeto JSON de raiz para vários registos num resultado de tabela.</span><span class="sxs-lookup"><span data-stu-id="a9e36-262">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="a9e36-263">Se tiver um ficheiro JSON com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="a9e36-263">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="a9e36-264">e pretende toocopy para uma tabela de SQL do Azure da seguinte Olá formatar, pelo dados Olá dentro Olá matriz e associação com informações de raiz comuns Olá cruzada:</span><span class="sxs-lookup"><span data-stu-id="a9e36-264">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="a9e36-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="a9e36-265">ordernumber</span></span> | <span data-ttu-id="a9e36-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="a9e36-266">orderdate</span></span> | <span data-ttu-id="a9e36-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="a9e36-267">order_pd</span></span> | <span data-ttu-id="a9e36-268">order_price</span><span class="sxs-lookup"><span data-stu-id="a9e36-268">order_price</span></span> | <span data-ttu-id="a9e36-269">city</span><span class="sxs-lookup"><span data-stu-id="a9e36-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="a9e36-270">01</span><span class="sxs-lookup"><span data-stu-id="a9e36-270">01</span></span> | <span data-ttu-id="a9e36-271">20170122</span><span class="sxs-lookup"><span data-stu-id="a9e36-271">20170122</span></span> | <span data-ttu-id="a9e36-272">P1</span><span class="sxs-lookup"><span data-stu-id="a9e36-272">P1</span></span> | <span data-ttu-id="a9e36-273">23</span><span class="sxs-lookup"><span data-stu-id="a9e36-273">23</span></span> | <span data-ttu-id="a9e36-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="a9e36-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="a9e36-275">01</span><span class="sxs-lookup"><span data-stu-id="a9e36-275">01</span></span> | <span data-ttu-id="a9e36-276">20170122</span><span class="sxs-lookup"><span data-stu-id="a9e36-276">20170122</span></span> | <span data-ttu-id="a9e36-277">P2</span><span class="sxs-lookup"><span data-stu-id="a9e36-277">P2</span></span> | <span data-ttu-id="a9e36-278">13</span><span class="sxs-lookup"><span data-stu-id="a9e36-278">13</span></span> | <span data-ttu-id="a9e36-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="a9e36-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="a9e36-280">01</span><span class="sxs-lookup"><span data-stu-id="a9e36-280">01</span></span> | <span data-ttu-id="a9e36-281">20170122</span><span class="sxs-lookup"><span data-stu-id="a9e36-281">20170122</span></span> | <span data-ttu-id="a9e36-282">P3</span><span class="sxs-lookup"><span data-stu-id="a9e36-282">P3</span></span> | <span data-ttu-id="a9e36-283">231</span><span class="sxs-lookup"><span data-stu-id="a9e36-283">231</span></span> | <span data-ttu-id="a9e36-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="a9e36-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="a9e36-285">conjunto de dados de entrada Olá com **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes).</span><span class="sxs-lookup"><span data-stu-id="a9e36-285">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="a9e36-286">Mais especificamente:</span><span class="sxs-lookup"><span data-stu-id="a9e36-286">More specifically:</span></span>

- <span data-ttu-id="a9e36-287">`structure`secção define os nomes das colunas de Olá personalizada e tipo de dados correspondente Olá durante a conversão de dados de tootabular.</span><span class="sxs-lookup"><span data-stu-id="a9e36-287">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="a9e36-288">Esta secção se **opcional** não ser que necessite toodo mapeamento de colunas.</span><span class="sxs-lookup"><span data-stu-id="a9e36-288">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="a9e36-289">Consulte [mapear colunas de conjunto de dados de toodestination de colunas de conjunto de dados de origem](data-factory-map-columns.md) secção para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="a9e36-289">See [Map source dataset columns toodestination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="a9e36-290">`jsonNodeReference`indica tooiterate e extrair dados de objetos de Olá com Olá sob o mesmo padrão **matriz** orderlines.</span><span class="sxs-lookup"><span data-stu-id="a9e36-290">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="a9e36-291">`jsonPathDefinition`Especifica o caminho JSON Olá para cada coluna indica onde tooextract Olá dados a partir de.</span><span class="sxs-lookup"><span data-stu-id="a9e36-291">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="a9e36-292">Neste exemplo, "ordernumber", "orderdate" e "Cidade" estão sob o objecto raiz com o caminho JSON, começando com "$".", enquanto"order_pd"e"order_price"estão definidas com o caminho derivado do elemento de matriz Olá sem"$"..</span><span class="sxs-lookup"><span data-stu-id="a9e36-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="a9e36-293">**Tenha em atenção Olá seguintes pontos:**</span><span class="sxs-lookup"><span data-stu-id="a9e36-293">**Note hello following points:**</span></span>

* <span data-ttu-id="a9e36-294">Se hello `structure` e `jsonPathDefinition` não estão definidas no conjunto de dados de Data Factory Olá hello atividade de cópia Deteta Olá o esquema do objeto primeiro Olá e aplanar objeto Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-294">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="a9e36-295">Se a entrada JSON Olá tem uma matriz, por predefinição Olá atividade de cópia converte Olá matriz todo valor numa cadeia.</span><span class="sxs-lookup"><span data-stu-id="a9e36-295">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="a9e36-296">Pode escolhê-la utilizando dados tooextract `jsonNodeReference` e/ou `jsonPathDefinition`, ou ignore-lo especificando um não-lo na `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="a9e36-296">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="a9e36-297">Se existirem duplicado Olá de nomes no mesmo nível, Olá atividade de cópia escolhe Olá último.</span><span class="sxs-lookup"><span data-stu-id="a9e36-297">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="a9e36-298">Os nomes das propriedades são sensíveis às maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a9e36-298">Property names are case-sensitive.</span></span> <span data-ttu-id="a9e36-299">Duas propriedades que tenham o mesmo nome, mas maiúsculas/minúsculas diferentes, são tratadas como duas propriedades separadas.</span><span class="sxs-lookup"><span data-stu-id="a9e36-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="a9e36-300">**Caso 2: Ao escrever no ficheiro de dados de tooJSON**</span><span class="sxs-lookup"><span data-stu-id="a9e36-300">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="a9e36-301">Se tiver Olá tabela na base de dados do SQL Server seguinte:</span><span class="sxs-lookup"><span data-stu-id="a9e36-301">If you have hello following table in SQL Database:</span></span>

| <span data-ttu-id="a9e36-302">ID</span><span class="sxs-lookup"><span data-stu-id="a9e36-302">id</span></span> | <span data-ttu-id="a9e36-303">order_date</span><span class="sxs-lookup"><span data-stu-id="a9e36-303">order_date</span></span> | <span data-ttu-id="a9e36-304">order_price</span><span class="sxs-lookup"><span data-stu-id="a9e36-304">order_price</span></span> | <span data-ttu-id="a9e36-305">order_by</span><span class="sxs-lookup"><span data-stu-id="a9e36-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a9e36-306">1</span><span class="sxs-lookup"><span data-stu-id="a9e36-306">1</span></span> | <span data-ttu-id="a9e36-307">20170119</span><span class="sxs-lookup"><span data-stu-id="a9e36-307">20170119</span></span> | <span data-ttu-id="a9e36-308">2000</span><span class="sxs-lookup"><span data-stu-id="a9e36-308">2000</span></span> | <span data-ttu-id="a9e36-309">David</span><span class="sxs-lookup"><span data-stu-id="a9e36-309">David</span></span> |
| <span data-ttu-id="a9e36-310">2</span><span class="sxs-lookup"><span data-stu-id="a9e36-310">2</span></span> | <span data-ttu-id="a9e36-311">20170120</span><span class="sxs-lookup"><span data-stu-id="a9e36-311">20170120</span></span> | <span data-ttu-id="a9e36-312">3500</span><span class="sxs-lookup"><span data-stu-id="a9e36-312">3500</span></span> | <span data-ttu-id="a9e36-313">José</span><span class="sxs-lookup"><span data-stu-id="a9e36-313">Patrick</span></span> |
| <span data-ttu-id="a9e36-314">3</span><span class="sxs-lookup"><span data-stu-id="a9e36-314">3</span></span> | <span data-ttu-id="a9e36-315">20170121</span><span class="sxs-lookup"><span data-stu-id="a9e36-315">20170121</span></span> | <span data-ttu-id="a9e36-316">4000</span><span class="sxs-lookup"><span data-stu-id="a9e36-316">4000</span></span> | <span data-ttu-id="a9e36-317">João</span><span class="sxs-lookup"><span data-stu-id="a9e36-317">Jason</span></span> |

<span data-ttu-id="a9e36-318">e para cada registo, pode esperar toowrite tooa um objeto JSON do Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="a9e36-318">and for each record, you expect toowrite tooa JSON object in hello following format:</span></span>
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

<span data-ttu-id="a9e36-319">com o conjunto de dados de saída de Olá **JsonFormat** está definida como se segue: (definição parcial com apenas Olá relevantes partes).</span><span class="sxs-lookup"><span data-stu-id="a9e36-319">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="a9e36-320">Mais especificamente, `structure` secção define os nomes de propriedade Olá personalizado no ficheiro de destino, `nestingSeparator` (predefinição é ".") são utilizados tooidentify camada de nest Olá do nome de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-320">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") are used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="a9e36-321">Esta secção se **opcional** , a menos que pretende o nome da propriedade toochange Olá comparar com o nome de coluna de origem ou aninhar algumas das propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-321">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="a9e36-322">Formato AVRO</span><span class="sxs-lookup"><span data-stu-id="a9e36-322">AVRO format</span></span>
<span data-ttu-id="a9e36-323">Se pretender que os ficheiros do Avro de Olá tooparse ou escrever dados de Olá no formato Avro, defina Olá `format` `type` propriedade demasiado**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-323">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="a9e36-324">Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-324">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="a9e36-325">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9e36-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="a9e36-326">formato de Avro toouse numa tabela do Hive, pode consultar demasiado[tutorial do Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="a9e36-326">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="a9e36-327">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="a9e36-327">Note hello following points:</span></span>  

* <span data-ttu-id="a9e36-328">[Tipos de dados complexos](http://avro.apache.org/docs/current/spec.html#schema_complex) não são suportados (regista, enumerações, matrizes, mapas, as uniões e fixo).</span><span class="sxs-lookup"><span data-stu-id="a9e36-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="a9e36-329">Formato ORC</span><span class="sxs-lookup"><span data-stu-id="a9e36-329">ORC format</span></span>
<span data-ttu-id="a9e36-330">Se pretender ficheiros do tooparse Olá ORC ou escrever dados Olá no formato ORC, defina Olá `format` `type` propriedade demasiado**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-330">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="a9e36-331">Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-331">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="a9e36-332">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9e36-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="a9e36-333">Se não estiver a copiar ficheiros ORC **como-é** entre no local e nuvem arquivos de dados, terá de tooinstall Olá JRE 8 (ambiente de tempo de execução Java) no seu computador de gateway.</span><span class="sxs-lookup"><span data-stu-id="a9e36-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="a9e36-334">Um gateway de 64 bits requer um JRE de 64 bits e um gateway de 32 bits requer um JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="a9e36-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="a9e36-335">Pode encontrar ambas as versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="a9e36-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="a9e36-336">Escolha Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="a9e36-336">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="a9e36-337">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="a9e36-337">Note hello following points:</span></span>

* <span data-ttu-id="a9e36-338">Os tipos de dados complexos não são suportados (ESTRUTURA, MAPA, LISTA, UNIÃO)</span><span class="sxs-lookup"><span data-stu-id="a9e36-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="a9e36-339">O ficheiro ORC tem três [opções relacionadas com a compressão](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NENHUM, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="a9e36-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="a9e36-340">O Data Factory suporta a leitura de dados a partir de um ficheiro ORC em qualquer um destes formatos de compressão.</span><span class="sxs-lookup"><span data-stu-id="a9e36-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="a9e36-341">Utiliza a compressão de Olá codec está nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="a9e36-341">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="a9e36-342">No entanto, ao escrever o ficheiro ORC tooan, Data Factory escolhe ZLIB, que é a predefinição de Olá para ORC.</span><span class="sxs-lookup"><span data-stu-id="a9e36-342">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="a9e36-343">Atualmente, não há nenhuma opção toooverride este comportamento.</span><span class="sxs-lookup"><span data-stu-id="a9e36-343">Currently, there is no option toooverride this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="a9e36-344">Formato de parquet</span><span class="sxs-lookup"><span data-stu-id="a9e36-344">Parquet format</span></span>
<span data-ttu-id="a9e36-345">Se pretender que os ficheiros do tooparse Olá Parquet ou escrever dados Olá no formato Parquet, defina Olá `format` `type` propriedade demasiado**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-345">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="a9e36-346">Não é necessário toospecify quaisquer propriedades na secção de formato Olá na secção de typeProperties Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-346">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="a9e36-347">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9e36-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="a9e36-348">Se não estiver a copiar ficheiros Parquet **como-é** entre no local e nuvem arquivos de dados, terá de tooinstall Olá JRE 8 (ambiente de tempo de execução Java) no seu computador de gateway.</span><span class="sxs-lookup"><span data-stu-id="a9e36-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="a9e36-349">Um gateway de 64 bits requer um JRE de 64 bits e um gateway de 32 bits requer um JRE de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="a9e36-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="a9e36-350">Pode encontrar ambas as versões [aqui](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="a9e36-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="a9e36-351">Escolha Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="a9e36-351">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="a9e36-352">Tenha em atenção Olá seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="a9e36-352">Note hello following points:</span></span>

* <span data-ttu-id="a9e36-353">Os tipos de dados complexos não são suportados (MAPA, LISTA)</span><span class="sxs-lookup"><span data-stu-id="a9e36-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="a9e36-354">Ficheiro de parquet tem Olá seguintes opções relacionadas com compressão: NONE, SNAPPY, GZIP e LZO.</span><span class="sxs-lookup"><span data-stu-id="a9e36-354">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="a9e36-355">O Data Factory suporta a leitura de dados a partir de um ficheiro ORC em qualquer um destes formatos de compressão.</span><span class="sxs-lookup"><span data-stu-id="a9e36-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="a9e36-356">Utiliza codec de compressão Olá nos dados de Olá Olá metadados tooread.</span><span class="sxs-lookup"><span data-stu-id="a9e36-356">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="a9e36-357">No entanto, ao escrever o ficheiro de Parquet tooa, Data Factory escolhe SNAPPY, que é Olá predefinido para o formato de Parquet.</span><span class="sxs-lookup"><span data-stu-id="a9e36-357">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="a9e36-358">Atualmente, não há nenhuma opção toooverride este comportamento.</span><span class="sxs-lookup"><span data-stu-id="a9e36-358">Currently, there is no option toooverride this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="a9e36-359">Suporte de compressão</span><span class="sxs-lookup"><span data-stu-id="a9e36-359">Compression support</span></span>
<span data-ttu-id="a9e36-360">Processamento de grandes conjuntos de dados pode provocar congestionamentos de e/s e da rede.</span><span class="sxs-lookup"><span data-stu-id="a9e36-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="a9e36-361">Por conseguinte, dados comprimidos nos arquivos podem não só acelerar a transferência de dados em toda a rede de Olá e poupar espaço em disco, mas também colocar melhorias de desempenho significativos no processamento de macrodados.</span><span class="sxs-lookup"><span data-stu-id="a9e36-361">Therefore, compressed data in stores can not only speed up data transfer across hello network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="a9e36-362">Atualmente, a compressão é suportada para os arquivos de dados baseada em ficheiros, tais como o Blob do Azure ou sistema de ficheiros no local.</span><span class="sxs-lookup"><span data-stu-id="a9e36-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="a9e36-363">compressão de toospecify para um conjunto de dados, utilize Olá **compressão** propriedade no conjunto de dados Olá JSON como no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="a9e36-363">toospecify compression for a dataset, use hello **compression** property in hello dataset JSON as in hello following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="a9e36-364">Suponha o conjunto de dados de exemplo de Olá é usado como saída de Olá de uma atividade de cópia, Olá copiar atividade comprime Olá dados de saída com codec GZIP utilizando rácio ideal e, em seguida, escrever dados Olá comprimido num ficheiro denominado pagecounts.csv.gz no Olá Blob Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-364">Suppose hello sample dataset is used as hello output of a copy activity, hello copy activity compresses hello output data with GZIP codec using optimal ratio and then write hello compressed data into a file named pagecounts.csv.gz in hello Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="a9e36-365">Definições de compressão não são suportadas para os dados na Olá **AvroFormat**, **OrcFormat**, ou **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-365">Compression settings are not supported for data in hello **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="a9e36-366">Quando a leitura de ficheiros nestes formatos, o Data Factory Deteta e utiliza o codec de compressão Olá nos metadados Olá.</span><span class="sxs-lookup"><span data-stu-id="a9e36-366">When reading files in these formats, Data Factory detects and uses hello compression codec in hello metadata.</span></span> <span data-ttu-id="a9e36-367">Quando escrever toofiles nestes formatos, o Data Factory escolhe codec de compressão Olá predefinido para esse formato.</span><span class="sxs-lookup"><span data-stu-id="a9e36-367">When writing toofiles in these formats, Data Factory chooses hello default compression codec for that format.</span></span> <span data-ttu-id="a9e36-368">Por exemplo, ZLIB para OrcFormat e SNAPPY para ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="a9e36-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="a9e36-369">Olá **compressão** secção tem duas propriedades:</span><span class="sxs-lookup"><span data-stu-id="a9e36-369">hello **compression** section has two properties:</span></span>  

* <span data-ttu-id="a9e36-370">**Tipo:** codec de compressão Olá, que pode ser **GZIP**, **Deflate**, **BZIP2**, ou **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-370">**Type:** hello compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="a9e36-371">**Nível:** rácio de compressão Olá, o que pode ser **Optimal** ou **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="a9e36-371">**Level:** hello compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="a9e36-372">**Mais rápido:** Olá compressão deve concluir a operação mais rapidamente possível, mesmo que o ficheiro resultante Olá não será comprimido forma ideal.</span><span class="sxs-lookup"><span data-stu-id="a9e36-372">**Fastest:** hello compression operation should complete as quickly as possible, even if hello resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="a9e36-373">**Ideal**: operação de compressão Olá deve ser executadas de forma ideal comprimida, mesmo que a operação de Olá demora um toocomplete mais longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="a9e36-373">**Optimal**: hello compression operation should be optimally compressed, even if hello operation takes a longer time toocomplete.</span></span>

    <span data-ttu-id="a9e36-374">Para obter mais informações, consulte [nível de compressão](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="a9e36-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="a9e36-375">Quando especificar `compression` propriedade de um conjunto de dados de entrada JSON, pipeline Olá pode ler dados comprimidos de origem Olá; e, quando especificar a propriedade Olá num conjunto de dados de saída JSON, atividade de cópia de Olá pode escrever o destino de toohello dados comprimidos.</span><span class="sxs-lookup"><span data-stu-id="a9e36-375">When you specify `compression` property in an input dataset JSON, hello pipeline can read compressed data from hello source; and when you specify hello property in an output dataset JSON, hello copy activity can write compressed data toohello destination.</span></span> <span data-ttu-id="a9e36-376">Seguem-se alguns cenários de exemplo:</span><span class="sxs-lookup"><span data-stu-id="a9e36-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="a9e36-377">Ler dados GZIP comprimido de um blob do Azure, descomprimi-lo e escrever o resultado dados tooan SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data tooan Azure SQL database.</span></span> <span data-ttu-id="a9e36-378">Definir Olá entrado Blob do Azure conjunto de dados com Olá `compression` `type` propriedade JSON como GZIP.</span><span class="sxs-lookup"><span data-stu-id="a9e36-378">You define hello input Azure Blob dataset with hello `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="a9e36-379">Ler dados a partir de um ficheiro de texto simples do sistema de ficheiros no local, comprimi-los utilizando o formato de GZip e escrever Olá comprimido dados tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write hello compressed data tooan Azure blob.</span></span> <span data-ttu-id="a9e36-380">Definir um conjunto de dados de Blobs do Azure de saída com Olá `compression` `type` propriedade JSON como GZip.</span><span class="sxs-lookup"><span data-stu-id="a9e36-380">You define an output Azure Blob dataset with hello `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="a9e36-381">Ficheiro. zip de leitura do servidor FTP, descomprimir-tooget Olá os ficheiros e encaminhado para esses ficheiros para o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a9e36-381">Read .zip file from FTP server, decompress it tooget hello files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="a9e36-382">Definir um conjunto de dados do FTP entrado com Olá `compression` `type` propriedade JSON como ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="a9e36-382">You define an input FTP dataset with hello `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="a9e36-383">Ler um GZIP compressão de dados de um blob do Azure, descomprimi-lo, comprimi-los utilizando BZIP2 e escrever dados de resultado tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a9e36-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data tooan Azure blob.</span></span> <span data-ttu-id="a9e36-384">Definir Olá entrado Blob do Azure conjunto de dados com `compression` `type` definir tooGZIP e Olá conjunto de dados de saída com `compression` `type` definir tooBZIP2 neste caso.</span><span class="sxs-lookup"><span data-stu-id="a9e36-384">You define hello input Azure Blob dataset with `compression` `type` set tooGZIP and hello output dataset with `compression` `type` set tooBZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="a9e36-385">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a9e36-385">Next steps</span></span>
<span data-ttu-id="a9e36-386">Olá seguintes artigos para os arquivos de dados de ficheiros suportados pelo Azure Data Factory, consulte:</span><span class="sxs-lookup"><span data-stu-id="a9e36-386">See hello following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="a9e36-387">Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="a9e36-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="a9e36-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a9e36-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="a9e36-389">FTP</span><span class="sxs-lookup"><span data-stu-id="a9e36-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="a9e36-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="a9e36-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="a9e36-391">Sistema de Ficheiros</span><span class="sxs-lookup"><span data-stu-id="a9e36-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="a9e36-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="a9e36-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
