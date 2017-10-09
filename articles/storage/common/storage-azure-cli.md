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
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="a677e-104">Utilizar Olá 2.0 de CLI do Azure com o Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="a677e-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="a677e-105">Olá open source plataforma Azure CLI 2.0 fornece um conjunto de comandos para trabalhar com Olá plataforma Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="a677e-106">Fornece muito Olá mesma funcionalidade encontrada no Olá [portal do Azure](https://portal.azure.com), incluindo acesso a dados avançado.</span><span class="sxs-lookup"><span data-stu-id="a677e-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="a677e-107">Neste guia, iremos mostrar-lhe como toouse Olá [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform várias tarefas de trabalhar com recursos na sua conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="a677e-108">Recomendamos a transferir e instalar ou atualizar a versão mais recente do toohello do Olá CLI 2.0 antes de utilizar este guia.</span><span class="sxs-lookup"><span data-stu-id="a677e-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="a677e-109">Exemplos de Olá guia Olá assumem a utilização de Olá do Olá shell de deteção no Ubuntu, mas outras plataformas devem efetuar da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="a677e-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="a677e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a677e-110">Prerequisites</span></span>
<span data-ttu-id="a677e-111">Este guia pressupõe que compreende os conceitos básicos do Olá do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="a677e-112">Também parte do princípio que está toosatisfy capaz de Olá conta requisitos de criação que são especificados abaixo para o Azure e Olá serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a677e-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="a677e-113">Contas</span><span class="sxs-lookup"><span data-stu-id="a677e-113">Accounts</span></span>
* <span data-ttu-id="a677e-114">**Conta do Azure**: Se ainda não tiver uma subscrição do Azure, [criar uma conta do Azure gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a677e-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="a677e-115">**Conta de Armazenamento**: veja [Criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a677e-115">**Storage account**: See [Create a storage account](storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="a677e-116">Instalar Olá Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a677e-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="a677e-117">Transfira e instale Olá 2.0 de CLI do Azure ao seguir as instruções de Olá descritas em [instalar o Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a677e-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="a677e-118">Se tiver problemas com a instalação de Olá, veja Olá [resolução de problemas de instalação](/cli/azure/install-az-cli2#installation-troubleshooting) secção do artigo Olá e Olá [instalar resolução de problemas](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guia no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a677e-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="a677e-119">Trabalhar com Olá CLI</span><span class="sxs-lookup"><span data-stu-id="a677e-119">Working with hello CLI</span></span>

<span data-ttu-id="a677e-120">Quando instalou Olá CLI, pode utilizar Olá `az` comando nos seus comandos de CLI do Azure de Olá de tooaccess de interface de linha de comandos (Bash, Terminal, linha de comandos).</span><span class="sxs-lookup"><span data-stu-id="a677e-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="a677e-121">Olá tipo `az` comando toosee uma lista completa dos comandos base Olá (Olá saídas de exemplo a seguir foram truncado):</span><span class="sxs-lookup"><span data-stu-id="a677e-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

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

<span data-ttu-id="a677e-122">Na sua interface de linha de comandos, execute o comando de Olá `az storage --help` Olá toolist `storage` comando subgrupos.</span><span class="sxs-lookup"><span data-stu-id="a677e-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="a677e-123">Olá as descrições dos subgrupos Olá fornecem uma descrição geral de Olá de funcionalidade Olá que CLI do Azure fornece para trabalhar com os recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a677e-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

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

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="a677e-124">Ligar Olá CLI tooyour subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="a677e-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="a677e-125">toowork com recursos de Olá na sua subscrição do Azure, tem primeiro de iniciar sessão tooyour conta do Azure com `az login`.</span><span class="sxs-lookup"><span data-stu-id="a677e-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="a677e-126">Existem várias formas, que pode iniciar sessão:</span><span class="sxs-lookup"><span data-stu-id="a677e-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="a677e-127">**Início de sessão interativo**:`az login`</span><span class="sxs-lookup"><span data-stu-id="a677e-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="a677e-128">**Iniciar sessão com o nome de utilizador e palavra-passe**:`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="a677e-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="a677e-129">Esta ação não funcionar com contas Microsoft ou contas que utilizam a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="a677e-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="a677e-130">**Iniciar sessão com um principal de serviço**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="a677e-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="a677e-131">Script de exemplo 2.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a677e-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="a677e-132">Em seguida, iremos irá trabalhar com um script de shell pequenas que emite alguns básico do Azure CLI 2.0 comandos toointeract com recursos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="a677e-133">script de Olá primeiro cria um novo contentor na sua conta de armazenamento, em seguida, carrega um contentor de toothat existente do ficheiro (como um blob).</span><span class="sxs-lookup"><span data-stu-id="a677e-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="a677e-134">Em seguida, apresenta uma lista de todos os blobs no contentor de Olá e por fim, transfere Olá tooa o destino de ficheiro no seu computador local que especificar.</span><span class="sxs-lookup"><span data-stu-id="a677e-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

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

<span data-ttu-id="a677e-135">**Configurar e executar o script de Olá**</span><span class="sxs-lookup"><span data-stu-id="a677e-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="a677e-136">Abra o editor de texto favorito, em seguida, copie e cole Olá precedente script no editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="a677e-137">Em seguida, atualize tooreflect de variáveis do script Olá as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="a677e-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="a677e-138">Substitua Olá os seguintes valores conforme especificado:</span><span class="sxs-lookup"><span data-stu-id="a677e-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="a677e-139">**\<storage_account_name\>**  nome Olá da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a677e-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="a677e-140">**\<storage_account_key\>**  chave de acesso primária ou secundária de Olá para a sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a677e-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="a677e-141">**\<container_name\>**  novo toocreate de contentor, por exemplo, "azure-cli-exemplo-container" Olá, um nome.</span><span class="sxs-lookup"><span data-stu-id="a677e-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="a677e-142">**\<blob_name\>**  um nome para o blob de destino Olá no contentor de Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="a677e-143">**\<file_to_upload\>**  Olá ficheiro toosmall de caminho no seu computador local, tais como "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="a677e-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="a677e-144">**\<destination_file\>**  Olá caminho do ficheiro de destino, tal como "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="a677e-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="a677e-145">Depois de ter atualizado variáveis necessárias Olá, guarde o script de Olá e saia do editor.</span><span class="sxs-lookup"><span data-stu-id="a677e-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="a677e-146">passos seguintes Olá partem do princípio de que com o nome do script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="a677e-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="a677e-147">Marque o script de Olá como executável, se necessário:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="a677e-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="a677e-148">Execute o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-148">Execute hello script.</span></span> <span data-ttu-id="a677e-149">Por exemplo, no Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="a677e-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="a677e-150">Deverá ver saída semelhante toohello seguinte e, Olá  **\<destination_file\>**  especificado na Olá script deve aparecer no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="a677e-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

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
> <span data-ttu-id="a677e-151">Olá saída anterior está a ser **tabela** formato.</span><span class="sxs-lookup"><span data-stu-id="a677e-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="a677e-152">Pode especificar que toouse de formato de saída, especificando Olá `--output` argumento nos seus comandos da CLI, ou defina-globalmente utilizando `az configure`.</span><span class="sxs-lookup"><span data-stu-id="a677e-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="a677e-153">Gerir contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a677e-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="a677e-154">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a677e-154">Create a new storage account</span></span>
<span data-ttu-id="a677e-155">toouse Storage do Azure, necessita de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a677e-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="a677e-156">Pode criar uma nova conta de armazenamento do Azure depois de configurar o computador demasiado[ligar tooyour subscrição](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="a677e-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="a677e-157">`--location`[Necessário]: localização.</span><span class="sxs-lookup"><span data-stu-id="a677e-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="a677e-158">Por exemplo, "EUA Oeste".</span><span class="sxs-lookup"><span data-stu-id="a677e-158">For example, "West US".</span></span>
* <span data-ttu-id="a677e-159">`--name`[Necessário]: nome de conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="a677e-160">o nome de Olá tem de ter 3 too24 carateres de comprimento e utilizar apenas carateres alfanuméricos minúsculos.</span><span class="sxs-lookup"><span data-stu-id="a677e-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="a677e-161">`--resource-group`[Necessário]: nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a677e-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="a677e-162">`--sku`[Necessário]: Olá SKU de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a677e-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="a677e-163">Valores permitidos:</span><span class="sxs-lookup"><span data-stu-id="a677e-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="a677e-164">Definir variáveis de ambiente de conta do storage do Azure predefinida</span><span class="sxs-lookup"><span data-stu-id="a677e-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="a677e-165">Pode ter várias contas de armazenamento na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="a677e-166">tooselect uma delas comandos toouse para todo o armazenamento subsequente, pode definir estas variáveis de ambiente:</span><span class="sxs-lookup"><span data-stu-id="a677e-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="a677e-167">Outra forma tooset uma conta do storage predefinida é utilizar uma cadeia de ligação.</span><span class="sxs-lookup"><span data-stu-id="a677e-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="a677e-168">Em primeiro lugar, obter a cadeia de ligação de Olá com Olá `show-connection-string` comando:</span><span class="sxs-lookup"><span data-stu-id="a677e-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="a677e-169">Em seguida, Olá cópia cadeia de ligação de saída e defina Olá `AZURE_STORAGE_CONNECTION_STRING` variável de ambiente (poderá ter de cadeia de ligação de Olá tooenclose aspas):</span><span class="sxs-lookup"><span data-stu-id="a677e-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="a677e-170">Todos os exemplos de Olá seguintes secções deste artigo partem do princípio de que definiu Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="a677e-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="a677e-171">Criar e gerir os blobs</span><span class="sxs-lookup"><span data-stu-id="a677e-171">Create and manage blobs</span></span>
<span data-ttu-id="a677e-172">Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a677e-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="a677e-173">Esta secção assume que já estiver familiarizado com conceitos de armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="a677e-174">Para obter informações detalhadas, consulte [introdução ao Blob storage do Azure através do .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [conceitos do serviço Blob](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="a677e-174">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="a677e-175">Criar um contentor</span><span class="sxs-lookup"><span data-stu-id="a677e-175">Create a container</span></span>
<span data-ttu-id="a677e-176">Todos os BLOBs no armazenamento do Azure tem de ser um contentor.</span><span class="sxs-lookup"><span data-stu-id="a677e-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="a677e-177">Pode criar um contentor utilizando Olá `az storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="a677e-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="a677e-178">Pode definir um de três níveis de acesso de leitura para um novo contentor especificando Olá opcional `--public-access` argumento:</span><span class="sxs-lookup"><span data-stu-id="a677e-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="a677e-179">`off`(predefinição): os dados de contentor são privado toohello proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="a677e-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="a677e-180">`blob`: Público acesso de leitura de blobs.</span><span class="sxs-lookup"><span data-stu-id="a677e-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="a677e-181">`container`: Lista de leitura e acesso toohello todo contentor público.</span><span class="sxs-lookup"><span data-stu-id="a677e-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="a677e-182">Para obter mais informações, consulte [gerir o acesso de leitura anónimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a677e-182">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="a677e-183">Carregar um contentor do blob tooa</span><span class="sxs-lookup"><span data-stu-id="a677e-183">Upload a blob tooa container</span></span>
<span data-ttu-id="a677e-184">Blob storage do Azure suporta bloco, de acréscimo e blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="a677e-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="a677e-185">Carregamento blobs tooa contentor utilizando Olá `blob upload` comando:</span><span class="sxs-lookup"><span data-stu-id="a677e-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="a677e-186">Por predefinição, Olá `blob upload` comando carrega blobs de toopage *.vhd ficheiros ou blobs de blocos, caso contrário.</span><span class="sxs-lookup"><span data-stu-id="a677e-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="a677e-187">toospecify outro tipo quando carregar um blob, pode utilizar Olá `--type` argumento – valores permitido são `append`, `block`, e `page`.</span><span class="sxs-lookup"><span data-stu-id="a677e-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="a677e-188">Para obter mais informações sobre tipos de blob diferente Olá, consulte [compreender os Blobs de blocos, os Blobs de acréscimo e Blobs de páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="a677e-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="a677e-189">Transferir um blob a partir de um contentor</span><span class="sxs-lookup"><span data-stu-id="a677e-189">Download a blob from a container</span></span>
<span data-ttu-id="a677e-190">Este exemplo demonstra como toodownload um blob a partir de um contentor:</span><span class="sxs-lookup"><span data-stu-id="a677e-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="a677e-191">Lista Olá blobs num contentor</span><span class="sxs-lookup"><span data-stu-id="a677e-191">List hello blobs in a container</span></span>

<span data-ttu-id="a677e-192">Listar Olá blobs num contentor com Olá [lista de BLOBs de armazenamento az](/cli/azure/storage/blob#list) comando.</span><span class="sxs-lookup"><span data-stu-id="a677e-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="a677e-193">Blobs de cópia</span><span class="sxs-lookup"><span data-stu-id="a677e-193">Copy blobs</span></span>
<span data-ttu-id="a677e-194">Pode copiar blobs dentro ou entre contas de armazenamento e regiões de forma assíncrona.</span><span class="sxs-lookup"><span data-stu-id="a677e-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="a677e-195">Olá exemplo seguinte demonstra como toocopy blobs do armazenamento de uma conta tooanother.</span><span class="sxs-lookup"><span data-stu-id="a677e-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="a677e-196">Vamos primeiro de criar um contentor na conta de armazenamento de origem Olá, especificando o acesso de leitura público para os respetivos blobs.</span><span class="sxs-lookup"><span data-stu-id="a677e-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="a677e-197">Em seguida, podemos carregar um ficheiro toohello contentor e, por fim, BLOBs de Olá cópia do contentor para um contentor na conta de armazenamento de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

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

<span data-ttu-id="a677e-198">No Olá acima exemplo, o contentor de destino Olá já deve existir na conta de armazenamento de destino Olá para toosucceed de operação de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="a677e-199">Além disso, o blob de origem Olá especificado no Olá `--source-uri` argumento tem de incluir um token de assinatura (SAS) de acesso partilhado ou de estar acessível publicamente, tal como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="a677e-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="a677e-200">Eliminar um blob</span><span class="sxs-lookup"><span data-stu-id="a677e-200">Delete a blob</span></span>
<span data-ttu-id="a677e-201">toodelete um blob, utilize Olá `blob delete` comando:</span><span class="sxs-lookup"><span data-stu-id="a677e-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="a677e-202">Criar e gerir partilhas de ficheiros</span><span class="sxs-lookup"><span data-stu-id="a677e-202">Create and manage file shares</span></span>
<span data-ttu-id="a677e-203">File storage do Azure oferece um armazenamento partilhado para aplicações utilizando o protocolo Server Message Block (SMB) de Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="a677e-204">Máquinas virtuais do Microsoft Azure e serviços em nuvem, bem como as aplicações no local, podem partilhar os dados de ficheiro através de partilhas montadas.</span><span class="sxs-lookup"><span data-stu-id="a677e-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="a677e-205">Pode gerir partilhas de ficheiros e dados de ficheiros através de Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="a677e-206">Para obter mais informações sobre o File storage do Azure, consulte [introdução ao File storage do Azure no Windows](../storage-dotnet-how-to-use-files.md) ou [como toouse File storage do Azure com o Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a677e-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="a677e-207">Criar uma partilha de ficheiros</span><span class="sxs-lookup"><span data-stu-id="a677e-207">Create a file share</span></span>
<span data-ttu-id="a677e-208">Uma partilha de ficheiros do Azure é uma partilha de ficheiros SMB no Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="a677e-209">Todos os ficheiros e diretórios têm de ser criados numa partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="a677e-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="a677e-210">Uma conta pode conter um número ilimitado de partilhas e uma partilha pode armazenar um número ilimitado de ficheiros, os limites de capacidade de toohello Olá da conta de armazenamento de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="a677e-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="a677e-211">Olá exemplo seguinte cria uma partilha de ficheiros com o nome **myshare**.</span><span class="sxs-lookup"><span data-stu-id="a677e-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="a677e-212">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="a677e-212">Create a directory</span></span>
<span data-ttu-id="a677e-213">Um diretório fornece uma estrutura hierárquica numa partilha de ficheiros do Azure.</span><span class="sxs-lookup"><span data-stu-id="a677e-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="a677e-214">Olá exemplo seguinte cria um diretório com o nome **myDir** numa partilha de ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="a677e-215">Um caminho de diretório pode incluir vários níveis, por exemplo **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="a677e-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="a677e-216">No entanto, tem de se certificar de que todos os diretórios de principal de existir antes de criar um subdiretório.</span><span class="sxs-lookup"><span data-stu-id="a677e-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="a677e-217">Por exemplo, para o caminho **dir1/dir2**, deve primeiro criar diretório **dir1**, em seguida, criar o diretório **dir2**.</span><span class="sxs-lookup"><span data-stu-id="a677e-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="a677e-218">Carregar uma partilha de tooa de ficheiros local</span><span class="sxs-lookup"><span data-stu-id="a677e-218">Upload a local file tooa share</span></span>
<span data-ttu-id="a677e-219">Olá exemplo seguinte carrega um ficheiro de **~/temp/samplefile.txt** tooroot de Olá **myshare** partilha de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="a677e-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="a677e-220">Olá `--source` argumento especifica tooupload de ficheiros local existente Olá.</span><span class="sxs-lookup"><span data-stu-id="a677e-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="a677e-221">Tal como acontece com a criação de diretórios, pode especificar um caminho de diretório no Olá partilha tooupload Olá tooan existente diretório do ficheiro na partilha de Olá:</span><span class="sxs-lookup"><span data-stu-id="a677e-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="a677e-222">Pode ser um ficheiro na partilha de Olá segurança too1 TB de tamanho.</span><span class="sxs-lookup"><span data-stu-id="a677e-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="a677e-223">Lista Olá ficheiros numa partilha</span><span class="sxs-lookup"><span data-stu-id="a677e-223">List hello files in a share</span></span>
<span data-ttu-id="a677e-224">Pode listar ficheiros e diretórios numa partilha através da utilização de Olá `az storage file list` comando:</span><span class="sxs-lookup"><span data-stu-id="a677e-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="a677e-225">Copiar ficheiros</span><span class="sxs-lookup"><span data-stu-id="a677e-225">Copy files</span></span>      
<span data-ttu-id="a677e-226">Pode copiar um ficheiro do ficheiro tooanother, um ficheiro tooa blob ou um ficheiro de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="a677e-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="a677e-227">Por exemplo, toocopy um diretório do ficheiro de tooa numa partilha diferentes:</span><span class="sxs-lookup"><span data-stu-id="a677e-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="a677e-228">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a677e-228">Next steps</span></span>
<span data-ttu-id="a677e-229">Seguem-se alguns recursos adicionais para aprender mais sobre como trabalhar com Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="a677e-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="a677e-230">Introdução ao Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a677e-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="a677e-231">Referência de comandos do Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a677e-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="a677e-232">CLI do Azure 2.0 no GitHub</span><span class="sxs-lookup"><span data-stu-id="a677e-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
