---
title: "aaaGet começar a utilizar o Azure CLI 2.0 do Azure Data Lake Analytics | Microsoft Docs"
description: "Saiba como criar uma tarefa de Data Lake Analytics, utilizando U-SQL toouse Olá 2.0 de Interface de linha de comandos do Azure toocreate uma conta de Data Lake Analytics e submeter a tarefa de Olá. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Introdução ao Azure Data Lake Analytics com a CLI 2.0 do Azure
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Neste tutorial, vai desenvolver uma tarefa que lê um ficheiro de valores separados por tabulações (TSV) e converte-o num ficheiro de valores separados por vírgulas (CSV). toogo através de Olá suportado mesmo tutorial, utilizando outras ferramentas, utilize Olá na lista pendente na parte superior de Olá desta secção.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, tem de ter Olá seguintes itens:

* **Uma subscrição do Azure**. Consulte [Obter uma avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **CLI 2.0 do Azure**. Consulte [instalar e configurar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Inicie sessão no tooAzure

toolog no tooyour subscrição do Azure:

```
azurecli
az login
```

São o URL do pedido toobrowse tooa e introduza um código de autenticação.  E, em seguida, siga Olá instruções tooenter as suas credenciais.

Depois de ter sessão iniciada, o comando de início de sessão de Olá lista as suas subscrições.

toouse uma subscrição específica:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Criar conta de Data Lake Analytics
Tem de ter uma conta de Data Lake Analytics antes de poder executar quaisquer tarefas. toocreate uma conta de Data Lake Analytics, tem de especificar Olá seguintes itens:

* **Grupo de Recursos do Azure**. Uma conta do Data Lake Analytics tem de ser criada dentro de um grupo de recursos do Azure. [O Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permite-lhe toowork com recursos de Olá na sua aplicação como um grupo. Pode implementar, atualizar ou eliminar todos os recursos de Olá para a sua aplicação numa operação única e coordenada.  

toolist Olá existente grupos de recursos na sua subscrição:

```
az group list
```

toocreate um novo grupo de recursos:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Nome da conta do Data Lake Analytics**. Cada conta do Data Lake Analytics tem um nome.
* **Localização**. Utilize um dos centros de dados do Azure de Olá que suporta o Data Lake Analytics.
* **Conta do Data Lake Store predefinida**: cada conta do Data Lake Analytics tem uma conta do Data Lake Store predefinida.

toolist Olá Data Lake Store conta existente:

```
az dls account list
```

toocreate uma nova conta de Data Lake Store:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Utilize Olá seguindo a sintaxe toocreate uma conta de Data Lake Analytics:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Depois de criar uma conta, pode utilizar Olá seguintes contas de Olá toolist de comandos e mostrar os detalhes da conta:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Carregar dados tooData Lake Store
Neste tutorial, vai processar alguns registos de pesquisa.  registo de pesquisa de Olá pode ser armazenado no Data Lake store ou armazenamento de Blobs do Azure.

Olá portal do Azure fornece uma interface de utilizador para copiar alguns exemplo dados ficheiros toohello Data Lake Store conta predefinida, que incluem um ficheiro de registo de pesquisa. Consulte [preparar dados de origem](data-lake-analytics-get-started-portal.md) conta de Data Lake Store do tooupload Olá dados toohello predefinido.

ficheiros de tooupload utilizando CLI 2.0, utilize Olá os seguintes comandos:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

A Data Lake Analytics também pode aceder ao armazenamento de Blobs do Azure.  Para carregar o armazenamento de BLOBs de tooAzure de dados, consulte [Using Olá CLI do Azure com o Storage do Azure](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Submeter tarefas de Data Lake Analytics
tarefas de Data Lake Analytics Olá são escritas em linguagem U-SQL de Olá. toolearn mais sobre U-SQL, consulte [introdução à linguagem U-SQL](data-lake-analytics-u-sql-get-started.md) e [eence de linguagem U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate um script de tarefa do Data Lake Analytics**

Crie um ficheiro de texto com o seguinte script U-SQL e guarde a estação de trabalho do Olá texto ficheiro tooyour:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Este script U-SQL lê Olá origem ficheiro de dados utilizando **extractors**e, em seguida, cria um ficheiro csv, utilizando **outputters**.

Não modifique os dois caminhos de Olá, exceto se copiar o ficheiro de origem Olá para uma localização diferente.  O Data Lake Analytics cria a pasta de saída Olá se não existir.

É mais simples toouse de caminhos relativos para ficheiros armazenados em contas do Data Lake Store predefinida. Também pode utilizar caminhos absolutos.  Por exemplo:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Tem de utilizar os ficheiros de tooaccess caminhos absolutos em contas de armazenamento ligadas.  Olá sintaxe para ficheiros armazenados numa conta de armazenamento do Azure ligada é:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> O contentor de Blobs do Azure com blobs públicos não é suportado.      
> O contentor de Blobs do Azure com contentores públicos não é suportado.      
>

**tarefas de toosubmit**

Utilize Olá seguindo a sintaxe toosubmit uma tarefa.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Por exemplo:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**tarefas de toolist e mostrar os detalhes da tarefa**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**tarefas de toocancel**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Obter resultados de tarefa

Depois de uma tarefa é concluída, pode utilizar Olá os seguintes comandos toolist Olá ficheiros de saída e transferir ficheiros Olá:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Por exemplo:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Pipelines e recorrências

**Obter informações sobre pipelines e recorrências**

Olá utilize `az dla job pipeline` comandos informações de pipeline de Olá toosee previamente submetido tarefas.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Olá utilize `az dla job recurrence` comandos toosee Olá periodicidade relativas tarefas anteriormente submetidas.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Passos seguintes

* Olá toosee documento de referência do Data Lake Analytics CLI 2.0, consulte [Data Lake Analytics](https://docs.microsoft.com/cli/azure/dla).
* Olá toosee documento de referência do Data Lake Store CLI 2.0, consulte [Data Lake Store](https://docs.microsoft.com/cli/azure/dls).
* toosee uma consulta mais complexa, consulte [analisar registos de site utilizando o Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
