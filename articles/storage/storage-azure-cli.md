---
title: "Olá aaaUsing 2.0 do CLI do Azure com o Storage do Azure | Microsoft Docs"
description: "Saiba como toouse Olá Interface de linha de comandos do Azure (CLI do Azure) 2.0 com toocreate de armazenamento do Azure e gerir contas de armazenamento e trabalhar com blobs do Azure e os ficheiros. Olá, Azure CLI 2.0 é uma ferramenta de plataforma escrita no Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>Utilizar Olá 2.0 de CLI do Azure com o Storage do Azure

Olá open source plataforma Azure CLI 2.0 fornece um conjunto de comandos para trabalhar com Olá plataforma Azure. Fornece muito Olá mesma funcionalidade encontrada no Olá [portal do Azure](https://portal.azure.com), incluindo acesso a dados avançado.

Neste guia, iremos mostrar-lhe como toouse Olá [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform várias tarefas de trabalhar com recursos na sua conta do Storage do Azure. Recomendamos a transferir e instalar ou atualizar a versão mais recente do toohello do Olá CLI 2.0 antes de utilizar este guia.

Exemplos de Olá guia Olá assumem a utilização de Olá do Olá shell de deteção no Ubuntu, mas outras plataformas devem efetuar da mesma forma. 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este guia pressupõe que compreende os conceitos básicos do Olá do Storage do Azure. Também parte do princípio que está toosatisfy capaz de Olá conta requisitos de criação que são especificados abaixo para o Azure e Olá serviço de armazenamento.

### <a name="accounts"></a>Contas
* **Conta do Azure**: Se ainda não tiver uma subscrição do Azure, [criar uma conta do Azure gratuita](https://azure.microsoft.com/free/).
* **Conta de Armazenamento**: veja [Criar uma conta de armazenamento](../storage/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Instalar Olá Azure CLI 2.0

Transfira e instale Olá 2.0 de CLI do Azure ao seguir as instruções de Olá descritas em [instalar o Azure CLI 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Se tiver problemas com a instalação de Olá, veja Olá [resolução de problemas de instalação](/cli/azure/install-az-cli2#installation-troubleshooting) secção do artigo Olá e Olá [instalar resolução de problemas](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guia no GitHub.
>

## <a name="working-with-hello-cli"></a>Trabalhar com Olá CLI

Quando instalou Olá CLI, pode utilizar Olá `az` comando nos seus comandos de CLI do Azure de Olá de tooaccess de interface de linha de comandos (Bash, Terminal, linha de comandos). Olá tipo `az` comando toosee uma lista completa dos comandos base Olá (Olá saídas de exemplo a seguir foram truncado):

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

Na sua interface de linha de comandos, execute o comando de Olá `az storage --help` Olá toolist `storage` comando subgrupos. Olá as descrições dos subgrupos Olá fornecem uma descrição geral de Olá de funcionalidade Olá que CLI do Azure fornece para trabalhar com os recursos de armazenamento.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Ligar Olá CLI tooyour subscrição do Azure

toowork com recursos de Olá na sua subscrição do Azure, tem primeiro de iniciar sessão tooyour conta do Azure com `az login`. Existem várias formas, que pode iniciar sessão:

* **Início de sessão interativo**:`az login`
* **Iniciar sessão com o nome de utilizador e palavra-passe**:`az login -u johndoe@contoso.com -p VerySecret`
  * Esta ação não funcionar com contas Microsoft ou contas que utilizam a autenticação multifator.
* **Iniciar sessão com um principal de serviço**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Script de exemplo 2.0 da CLI do Azure

Em seguida, iremos irá trabalhar com um script de shell pequenas que emite alguns básico do Azure CLI 2.0 comandos toointeract com recursos de armazenamento do Azure. script de Olá primeiro cria um novo contentor na sua conta de armazenamento, em seguida, carrega um contentor de toothat existente do ficheiro (como um blob). Em seguida, apresenta uma lista de todos os blobs no contentor de Olá e por fim, transfere Olá tooa o destino de ficheiro no seu computador local que especificar.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Configurar e executar o script de Olá**

1. Abra o editor de texto favorito, em seguida, copie e cole Olá precedente script no editor de Olá.

2. Em seguida, atualize tooreflect de variáveis do script Olá as definições de configuração. Substitua Olá os seguintes valores conforme especificado:

   * **\<storage_account_name\>**  nome Olá da sua conta de armazenamento.
   * **\<storage_account_key\>**  chave de acesso primária ou secundária de Olá para a sua conta de armazenamento.
   * **\<container_name\>**  novo toocreate de contentor, por exemplo, "azure-cli-exemplo-container" Olá, um nome.
   * **\<blob_name\>**  um nome para o blob de destino Olá no contentor de Olá.
   * **\<file_to_upload\>**  Olá ficheiro toosmall de caminho no seu computador local, tais como "~ / images/HelloWorld.png".
   * **\<destination_file\>**  Olá caminho do ficheiro de destino, tal como "~ / downloadedImage.png".

3. Depois de ter atualizado variáveis necessárias Olá, guarde o script de Olá e saia do editor. passos seguintes Olá partem do princípio de que com o nome do script **my_storage_sample.sh**.

4. Marque o script de Olá como executável, se necessário:`chmod +x my_storage_sample.sh`

5. Execute o script de Olá. Por exemplo, no Bash:`./my_storage_sample.sh`

Deverá ver saída semelhante toohello seguinte e, Olá  **\<destination_file\>**  especificado na Olá script deve aparecer no seu computador local.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Olá saída anterior está a ser **tabela** formato. Pode especificar que toouse de formato de saída, especificando Olá `--output` argumento nos seus comandos da CLI, ou defina-globalmente utilizando `az configure`.
>

## <a name="manage-storage-accounts"></a>Gerir contas de armazenamento

### <a name="create-a-new-storage-account"></a>Criar uma nova conta de armazenamento
toouse Storage do Azure, necessita de uma conta de armazenamento. Pode criar uma nova conta de armazenamento do Azure depois de configurar o computador demasiado[ligar tooyour subscrição](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location`[Necessário]: localização. Por exemplo, "EUA Oeste".
* `--name`[Necessário]: nome de conta do storage Olá. o nome de Olá tem de ter 3 too24 carateres de comprimento e utilizar apenas carateres alfanuméricos minúsculos.
* `--resource-group`[Necessário]: nome do grupo de recursos.
* `--sku`[Necessário]: Olá SKU de conta de armazenamento. Valores permitidos:
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Definir variáveis de ambiente de conta do storage do Azure predefinida
Pode ter várias contas de armazenamento na sua subscrição do Azure. tooselect uma delas comandos toouse para todo o armazenamento subsequente, pode definir estas variáveis de ambiente:

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Outra forma tooset uma conta do storage predefinida é utilizar uma cadeia de ligação. Em primeiro lugar, obter a cadeia de ligação de Olá com Olá `show-connection-string` comando:

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Em seguida, Olá cópia cadeia de ligação de saída e defina Olá `AZURE_STORAGE_CONNECTION_STRING` variável de ambiente (poderá ter de cadeia de ligação de Olá tooenclose aspas):

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Todos os exemplos de Olá seguintes secções deste artigo partem do princípio de que definiu Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` variáveis de ambiente.
>

## <a name="create-and-manage-blobs"></a>Criar e gerir os blobs
Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS. Esta secção assume que já estiver familiarizado com conceitos de armazenamento de Blobs do Azure. Para obter informações detalhadas, consulte [introdução ao Blob storage do Azure através do .NET](storage-dotnet-how-to-use-blobs.md) e [conceitos do serviço Blob](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Criar um contentor
Todos os BLOBs no armazenamento do Azure tem de ser um contentor. Pode criar um contentor utilizando Olá `az storage container create` comando:

```azurecli
az storage container create --name <container_name>
```

Pode definir um de três níveis de acesso de leitura para um novo contentor especificando Olá opcional `--public-access` argumento:

* `off`(predefinição): os dados de contentor são privado toohello proprietário da conta.
* `blob`: Público acesso de leitura de blobs.
* `container`: Lista de leitura e acesso toohello todo contentor público.

Para obter mais informações, consulte [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Carregar um contentor do blob tooa
Blob storage do Azure suporta bloco, de acréscimo e blobs de páginas. Carregamento blobs tooa contentor utilizando Olá `blob upload` comando:

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Por predefinição, Olá `blob upload` comando carrega blobs de toopage *.vhd ficheiros ou blobs de blocos, caso contrário. toospecify outro tipo quando carregar um blob, pode utilizar Olá `--type` argumento – valores permitido são `append`, `block`, e `page`.

 Para obter mais informações sobre tipos de blob diferente Olá, consulte [compreender os Blobs de blocos, os Blobs de acréscimo e Blobs de páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Transferir um blob a partir de um contentor
Este exemplo demonstra como toodownload um blob a partir de um contentor:

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor

Listar Olá blobs num contentor com Olá [lista de BLOBs de armazenamento az](/cli/azure/storage/blob#list) comando.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Blobs de cópia
Pode copiar blobs dentro ou entre contas de armazenamento e regiões de forma assíncrona.

Olá exemplo seguinte demonstra como toocopy blobs do armazenamento de uma conta tooanother. Vamos primeiro de criar um contentor na conta de armazenamento de origem Olá, especificando o acesso de leitura público para os respetivos blobs. Em seguida, podemos carregar um ficheiro toohello contentor e, por fim, BLOBs de Olá cópia do contentor para um contentor na conta de armazenamento de destino Olá.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

No Olá acima exemplo, o contentor de destino Olá já deve existir na conta de armazenamento de destino Olá para toosucceed de operação de cópia de Olá. Além disso, o blob de origem Olá especificado no Olá `--source-uri` argumento tem de incluir um token de assinatura (SAS) de acesso partilhado ou de estar acessível publicamente, tal como neste exemplo.

### <a name="delete-a-blob"></a>Eliminar um blob
toodelete um blob, utilize Olá `blob delete` comando:

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Criar e gerir partilhas de ficheiros
File storage do Azure oferece um armazenamento partilhado para aplicações utilizando o protocolo Server Message Block (SMB) de Olá. Máquinas virtuais do Microsoft Azure e serviços em nuvem, bem como as aplicações no local, podem partilhar os dados de ficheiro através de partilhas montadas. Pode gerir partilhas de ficheiros e dados de ficheiros através de Olá CLI do Azure. Para obter mais informações sobre o File storage do Azure, consulte [introdução ao File storage do Azure no Windows](storage-dotnet-how-to-use-files.md) ou [como toouse File storage do Azure com o Linux](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Criar uma partilha de ficheiros
Uma partilha de ficheiros do Azure é uma partilha de ficheiros SMB no Azure. Todos os ficheiros e diretórios têm de ser criados numa partilha de ficheiros. Uma conta pode conter um número ilimitado de partilhas e uma partilha pode armazenar um número ilimitado de ficheiros, os limites de capacidade de toohello Olá da conta de armazenamento de cópia de segurança. Olá exemplo seguinte cria uma partilha de ficheiros com o nome **myshare**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Criar um diretório
Um diretório fornece uma estrutura hierárquica numa partilha de ficheiros do Azure. Olá exemplo seguinte cria um diretório com o nome **myDir** numa partilha de ficheiros de Olá.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Um caminho de diretório pode incluir vários níveis, por exemplo **dir1/dir2**. No entanto, tem de se certificar de que todos os diretórios de principal de existir antes de criar um subdiretório. Por exemplo, para o caminho **dir1/dir2**, deve primeiro criar diretório **dir1**, em seguida, criar o diretório **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Carregar uma partilha de tooa de ficheiros local
Olá exemplo seguinte carrega um ficheiro de **~/temp/samplefile.txt** tooroot de Olá **myshare** partilha de ficheiros. Olá `--source` argumento especifica tooupload de ficheiros local existente Olá.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Tal como acontece com a criação de diretórios, pode especificar um caminho de diretório no Olá partilha tooupload Olá tooan existente diretório do ficheiro na partilha de Olá:

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Pode ser um ficheiro na partilha de Olá segurança too1 TB de tamanho.

### <a name="list-hello-files-in-a-share"></a>Lista Olá ficheiros numa partilha
Pode listar ficheiros e diretórios numa partilha através da utilização de Olá `az storage file list` comando:

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Copiar ficheiros      
Pode copiar um ficheiro do ficheiro tooanother, um ficheiro tooa blob ou um ficheiro de tooa de blob. Por exemplo, toocopy um diretório do ficheiro de tooa numa partilha diferentes:        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Passos seguintes
Seguem-se alguns recursos adicionais para aprender mais sobre como trabalhar com Olá Azure CLI 2.0.

* [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Referência de comandos do Azure CLI 2.0](/cli/azure)
* [CLI do Azure 2.0 no GitHub](https://github.com/Azure/azure-cli)
