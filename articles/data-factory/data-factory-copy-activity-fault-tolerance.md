---
title: "tolerância a falhas aaaAdd na atividade de cópia de fábrica de dados do Azure por ignorar linhas incompatíveis | Microsoft Docs"
description: "Saiba como tooadd tolerância a falhas na atividade de cópia de fábrica de dados do Azure por ignorar linhas incompatíveis durante a cópia"
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
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="19e5c-103">Adicione tolerância a falhas na atividade de cópia ao ignorar linhas incompatíveis</span><span class="sxs-lookup"><span data-stu-id="19e5c-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

<span data-ttu-id="19e5c-104">O Azure Data Factory [atividade de cópia](data-factory-data-movement-activities.md) oferece linhas incompatível do duas formas toohandle ao copiar dados entre os arquivos de dados de origem e dependente:</span><span class="sxs-lookup"><span data-stu-id="19e5c-104">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways toohandle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="19e5c-105">Pode abortar e efetuar a cópia de Olá atividade quando os dados incompatíveis encontrado (comportamento predefinido).</span><span class="sxs-lookup"><span data-stu-id="19e5c-105">You can abort and fail hello copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="19e5c-106">Pode continuar toocopy todos os dados de Olá adicionando tolerância a falhas e a ignorar as linhas de dados incompatíveis.</span><span class="sxs-lookup"><span data-stu-id="19e5c-106">You can continue toocopy all of hello data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="19e5c-107">Além disso, pode iniciar sessão linhas incompatível Olá no Blob storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="19e5c-107">In addition, you can log hello incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="19e5c-108">Em seguida, que pode examinar Olá registo toolearn Olá causa da falha de Olá, corrigir dados Olá na origem de dados de Olá e repita a atividade de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="19e5c-108">You can then examine hello log toolearn hello cause for hello failure, fix hello data on hello data source, and retry hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="19e5c-109">Cenários suportados</span><span class="sxs-lookup"><span data-stu-id="19e5c-109">Supported scenarios</span></span>
<span data-ttu-id="19e5c-110">Atividade de cópia suporta três cenários para detetar, ignorar, dados e registo incompatíveis:</span><span class="sxs-lookup"><span data-stu-id="19e5c-110">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="19e5c-111">**Incompatibilidade entre Olá tipo de dados de origem e o tipo nativo de Olá sink**</span><span class="sxs-lookup"><span data-stu-id="19e5c-111">**Incompatibility between hello source data type and hello sink native type**</span></span>

    <span data-ttu-id="19e5c-112">Por exemplo: copiar dados de um ficheiro CSV no Blob storage tooa SQL da base de dados com uma definição de esquema que contém três **INT** colunas de tipo.</span><span class="sxs-lookup"><span data-stu-id="19e5c-112">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="19e5c-113">Olá linhas do ficheiro CSV que contêm dados numéricos, tais como `123,456,789` são copiados com êxito toohello arquivo de sink.</span><span class="sxs-lookup"><span data-stu-id="19e5c-113">hello CSV file rows that contain numeric data, such as `123,456,789` are copied successfully toohello sink store.</span></span> <span data-ttu-id="19e5c-114">No entanto, Olá linhas que contêm valores não numéricos, tais como `123,456,abc` são detetados como incompatíveis e são ignorados.</span><span class="sxs-lookup"><span data-stu-id="19e5c-114">However, hello rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="19e5c-115">**Erro de correspondência no número de Olá de colunas entre a origem de Olá e o sink de Olá**</span><span class="sxs-lookup"><span data-stu-id="19e5c-115">**Mismatch in hello number of columns between hello source and hello sink**</span></span>

    <span data-ttu-id="19e5c-116">Por exemplo: copiar dados de um ficheiro CSV no Blob storage tooa SQL da base de dados com uma definição de esquema que contenha seis colunas.</span><span class="sxs-lookup"><span data-stu-id="19e5c-116">For example: Copy data from a CSV file in Blob storage tooa SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="19e5c-117">Olá linhas que contêm seis colunas são um ficheiro CSV foi copiado com êxito toohello arquivo de sink.</span><span class="sxs-lookup"><span data-stu-id="19e5c-117">hello CSV file rows that contain six columns are copied successfully toohello sink store.</span></span> <span data-ttu-id="19e5c-118">Olá CSV ficheiro linhas que contêm mais ou menos de seis colunas são detetadas como incompatíveis e são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="19e5c-118">hello CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="19e5c-119">**Violação da chave primária ao escrever a base de dados relacional tooa**</span><span class="sxs-lookup"><span data-stu-id="19e5c-119">**Primary key violation when writing tooa relational database**</span></span>

    <span data-ttu-id="19e5c-120">Por exemplo: copiar dados de uma base de dados SQL de tooa de servidor do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="19e5c-120">For example: Copy data from a SQL server tooa SQL database.</span></span> <span data-ttu-id="19e5c-121">Uma chave primária está definida na base de dados SQL de receptores de Olá, mas essa nenhuma chave primária está definida no SQL server origem Olá.</span><span class="sxs-lookup"><span data-stu-id="19e5c-121">A primary key is defined in hello sink SQL database, but no such primary key is defined in hello source SQL server.</span></span> <span data-ttu-id="19e5c-122">linhas de Olá duplicada que existam na origem de Olá não podem ser copiado toohello sink.</span><span class="sxs-lookup"><span data-stu-id="19e5c-122">hello duplicated rows that exist in hello source cannot be copied toohello sink.</span></span> <span data-ttu-id="19e5c-123">Atividade de cópia copia apenas Olá primeira linha dos dados de origem Olá no sink Olá.</span><span class="sxs-lookup"><span data-stu-id="19e5c-123">Copy Activity copies only hello first row of hello source data into hello sink.</span></span> <span data-ttu-id="19e5c-124">Olá origem subsequentes linhas que contêm o valor de chave primária Olá duplicado são detetadas como incompatíveis e são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="19e5c-124">hello subsequent source rows that contain hello duplicated primary key value are detected as incompatible and are skipped.</span></span>

## <a name="configuration"></a><span data-ttu-id="19e5c-125">Configuração</span><span class="sxs-lookup"><span data-stu-id="19e5c-125">Configuration</span></span>
<span data-ttu-id="19e5c-126">Olá exemplo seguinte fornece um tooconfigure de definição JSON a ignorar as linhas de incompatível Olá na atividade de cópia:</span><span class="sxs-lookup"><span data-stu-id="19e5c-126">hello following example provides a JSON definition tooconfigure skipping hello incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="19e5c-127">Propriedade</span><span class="sxs-lookup"><span data-stu-id="19e5c-127">Property</span></span> | <span data-ttu-id="19e5c-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="19e5c-128">Description</span></span> | <span data-ttu-id="19e5c-129">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="19e5c-129">Allowed values</span></span> | <span data-ttu-id="19e5c-130">Necessário</span><span class="sxs-lookup"><span data-stu-id="19e5c-130">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="19e5c-131">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="19e5c-131">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="19e5c-132">Ative a ignorar incompatíveis linhas durante a cópia ou não.</span><span class="sxs-lookup"><span data-stu-id="19e5c-132">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="19e5c-133">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="19e5c-133">True</span></span><br/><span data-ttu-id="19e5c-134">FALSE (predefinição)</span><span class="sxs-lookup"><span data-stu-id="19e5c-134">False (default)</span></span> | <span data-ttu-id="19e5c-135">Não</span><span class="sxs-lookup"><span data-stu-id="19e5c-135">No</span></span> |
| <span data-ttu-id="19e5c-136">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="19e5c-136">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="19e5c-137">Um grupo de propriedades que podem ser especificados quando quiser linhas incompatível do toolog Olá.</span><span class="sxs-lookup"><span data-stu-id="19e5c-137">A group of properties that can be specified when you want toolog hello incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="19e5c-138">Não</span><span class="sxs-lookup"><span data-stu-id="19e5c-138">No</span></span> |
| <span data-ttu-id="19e5c-139">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="19e5c-139">**linkedServiceName**</span></span> | <span data-ttu-id="19e5c-140">serviço de Olá ligado do Storage do Azure toostore Olá registo que contém as linhas de Olá foi ignorada.</span><span class="sxs-lookup"><span data-stu-id="19e5c-140">hello linked service of Azure Storage toostore hello log that contains hello skipped rows.</span></span> | <span data-ttu-id="19e5c-141">nome de Olá de um [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) serviço, que se refere-se a instância de armazenamento toohello que pretende que o ficheiro de registo do toouse toostore Olá ligado.</span><span class="sxs-lookup"><span data-stu-id="19e5c-141">hello name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers toohello storage instance that you want toouse toostore hello log file.</span></span> | <span data-ttu-id="19e5c-142">Não</span><span class="sxs-lookup"><span data-stu-id="19e5c-142">No</span></span> |
| <span data-ttu-id="19e5c-143">**caminho**</span><span class="sxs-lookup"><span data-stu-id="19e5c-143">**path**</span></span> | <span data-ttu-id="19e5c-144">caminho de Olá Olá do ficheiro de registo que contém Olá ignorada linhas.</span><span class="sxs-lookup"><span data-stu-id="19e5c-144">hello path of hello log file that contains hello skipped rows.</span></span> | <span data-ttu-id="19e5c-145">Especifique o caminho de armazenamento de BLOBs de Olá que pretende que os dados do toouse toolog Olá incompatível.</span><span class="sxs-lookup"><span data-stu-id="19e5c-145">Specify hello Blob storage path that you want toouse toolog hello incompatible data.</span></span> <span data-ttu-id="19e5c-146">Se não fornecer um caminho, o serviço de Olá cria um contentor para si.</span><span class="sxs-lookup"><span data-stu-id="19e5c-146">If you do not provide a path, hello service creates a container for you.</span></span> | <span data-ttu-id="19e5c-147">Não</span><span class="sxs-lookup"><span data-stu-id="19e5c-147">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="19e5c-148">Monitorização</span><span class="sxs-lookup"><span data-stu-id="19e5c-148">Monitoring</span></span>
<span data-ttu-id="19e5c-149">Após a conclusão da atividade de cópia de Olá executar, pode ver o número de Olá de linhas ignorados na secção monitorização de Olá:</span><span class="sxs-lookup"><span data-stu-id="19e5c-149">After hello copy activity run completes, you can see hello number of skipped rows in hello monitoring section:</span></span>

![Monitor ignorada linhas incompatíveis](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="19e5c-151">Se configurar linhas incompatível do toolog Olá, pode encontrar o ficheiro de registo de Olá neste caminho: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` no ficheiro de registo de Olá, pode ver as linhas de Olá que foram ignoradas e Olá causa de raiz de incompatibilidade Olá.</span><span class="sxs-lookup"><span data-stu-id="19e5c-151">If you configure toolog hello incompatible rows, you can find hello log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In hello log file, you can see hello rows that were skipped and hello root cause of hello incompatibility.</span></span>

<span data-ttu-id="19e5c-152">Dados originais Olá e erro correspondente Olá são registadas no ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="19e5c-152">Both hello original data and hello corresponding error are logged in hello file.</span></span> <span data-ttu-id="19e5c-153">Um exemplo de conteúdo do ficheiro de registo de Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="19e5c-153">An example of hello log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="19e5c-154">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="19e5c-154">Next steps</span></span>
<span data-ttu-id="19e5c-155">toolearn mais informações sobre a atividade de cópia de fábrica de dados do Azure, consulte [mover dados utilizando a atividade de cópia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="19e5c-155">toolearn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
