---
title: aaaUsing Azure PowerShell com o Storage do Azure | Microsoft Docs
description: "Saiba como toouse Olá cmdlets do PowerShell do Azure para armazenamento do Azure toocreate e gerir contas de armazenamento trabalhar com blobs, tabelas, filas e ficheiros configurar e consultar a análise de armazenamento e criar assinaturas de acesso partilhado."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a>Utilizar o Azure PowerShell com o Storage do Azure
## <a name="overview"></a>Descrição geral
O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell. É uma shell de linha de comandos e linguagem de script baseada em tarefas concebida especialmente para a administração de sistemas. Com o PowerShell, pode facilmente controlar e automatizar administração Olá dos seus serviços do Azure e aplicações. Por exemplo, pode utilizar Olá tooperform cmdlets de Olá mesmas tarefas que pode realizar através de Olá [portal do Azure](https://portal.azure.com).

Neste guia, iremos irá explorar como toouse Olá [Cmdlets de armazenamento do Azure](/powershell/module/azurerm.storage/#storage) tooperform uma variedade de tarefas de desenvolvimento e de administração com o Storage do Azure.

Este guia pressupõe que tem experiência anterior na utilização [Storage do Azure](https://azure.microsoft.com/documentation/services/storage/) e [do Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx). Guia de Olá fornece um número de scripts de utilização de Olá toodemonstrate do PowerShell com o Storage do Azure. Deve ser atualizado as variáveis do script de Olá, com base na sua configuração antes de executar cada script.

secção primeiro Olá este guia fornece uma leitura rápida no armazenamento do Azure e o PowerShell. Para obter informações detalhadas e instruções, iniciar a partir de Olá [pré-requisitos para utilizar o Azure PowerShell com o Storage do Azure](#prerequisites-for-using-azure-powershell-with-azure-storage).

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a>Introdução ao Storage do Azure e do PowerShell em 5 minutos
Esta secção mostra-lhe como tooaccess Storage do Azure através do PowerShell em 5 minutos.

**Novo tooAzure:** obter uma subscrição do Microsoft Azure e uma conta Microsoft associada essa subscrição. Para obter informações sobre as opções de compra do Azure, consulte [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [opções de compra](https://azure.microsoft.com/pricing/purchase-options/), e [ofertas de membros](https://azure.microsoft.com/pricing/member-offers/) (para os membros de MSDN, Microsoft Partner Network, BizSpark e outros programas Microsoft).

Consulte [atribuir funções de administrador no Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as subscrições do Azure.

**Depois de criar uma conta e subscrição do Microsoft Azure:**

1. Transfira e instale os mais recentes Olá [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).
2. Início Windows PowerShell script ambiente integrado (ISE): Num computador local, aceda toohello **iniciar** menu. Tipo **ferramentas administrativas** e clique em toorun-lo. No Olá **ferramentas administrativas** janela, clique com botão direito **ISE do Windows PowerShell**, clique em **executar como administrador**.
3. No **ISE do Windows PowerShell**, clique em **ficheiro** > **novo** toocreate um novo ficheiro de script.
4. Agora, iremos irá dar-lhe um script simple que mostra básico tooaccess de comandos do PowerShell do armazenamento do Azure. script de Olá será primeiro solicitar a sua tooadd de credenciais de conta do Azure conta do Azure toohello PowerShell ambiente local. Em seguida, o script de Olá predefinir Olá subscrição do Azure e criar uma nova conta de armazenamento no Azure. Em seguida, o script de Olá irá criar um novo contentor nesta nova conta de armazenamento e carregar um contentor de toothat (blob) do ficheiro de imagem existente. Depois de script de Olá apresenta uma lista de todos os blobs no contentor, irá criar um novo diretório de destino no computador local e transferir o ficheiro de imagem de Olá.
5. No Olá seguinte secção de código, selecione o script de Olá entre comentários de Olá **#begin** e **#end**. Prima CTRL + C toocopy-toohello área de transferência.

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. No **ISE do Windows PowerShell**, prima o script de Olá CTRL + V toocopy. Clique em **ficheiro** > **guardar**. No Olá **guardar como** janela de caixa de diálogo, o nome de Olá do tipo de ficheiro de script de Olá, tais como "mystoragescript." Clique em **Guardar**.
7. Agora, terá de variáveis de script tooupdate Olá com base nas suas definições de configuração. Tem de atualizar Olá **$SubscriptionName** variável com a sua própria subscrição. Pode manter Olá outras variáveis conforme especificado no script de Olá ou atualizá-las conforme desejar.
   
   * **$SubscriptionName:** tem de atualizar esta variável com o seu próprio nome de subscrição. Siga um dos seguintes três formas toolocate Olá nome da sua subscrição de Olá:
     
    a. No **ISE do Windows PowerShell**, clique em **ficheiro** > **novo** toocreate um novo ficheiro de script. Script toohello novo ficheiro de script a seguir de Olá cópia e clique em **depurar** > **executar**. Olá seguinte script será primeiro peça ao seu tooadd de credenciais de conta do Azure conta do Azure toohello PowerShell ambiente local e em seguida, mostra todas as subscrições de Olá que estão ligados toohello local a sessão do PowerShell. Tome nota do nome Olá subscrição Olá que pretende que toouse ao seguir este tutorial:
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    b. toolocate e copie a sua subscrição nome no Olá [portal do Azure](https://portal.azure.com), no Olá menu do Hub no Olá à esquerda, clique em **subscrições**. Copie o nome de Olá da subscrição que pretende que toouse durante a execução de scripts de Olá neste guia.
     
     ![Portal do Azure](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    c. toolocate e copie a sua subscrição nome no Olá [Portal clássico do Azure](https://manage.windowsazure.com/), desloque para baixo e clique em **definições** no Olá à esquerda do lado do portal de Olá. Clique em **subscrições** toosee uma lista das suas subscrições. Nome de Olá de cópia da subscrição que pretende que sejam toouse durante a execução de scripts de Olá fornecidos neste guia.
     
     ![Portal Clássico do Azure](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * **$StorageAccountName:** utilizar Olá fornecido nome de script de Olá ou introduza um novo nome para a sua conta de armazenamento. **Importante:** Olá nome da conta de armazenamento Olá tem de ser exclusivo no Azure. Tem de ser em minúsculas, demasiado!
   * **$Location:** utilizar Olá fornecido "EUA Oeste" no script de Olá ou escolher outras localizações do Azure, como EUA leste, Europa do Norte e assim sucessivamente.
   * **$ContainerName:** utilizar Olá fornecido nome de script de Olá ou introduza um novo nome para o contentor.
   * **$ImageToUpload:** introduza uma imagem de tooa caminho no seu computador local, como: "C:\Images\HelloWorld.png".
   * **$DestinationFolder:** introduza um caminho os tooa diretório local toostore ficheiros transferidos do armazenamento do Azure, tais como: "C:\DownloadImages".
8. Depois de atualizar as variáveis do script de Olá no ficheiro de "mystoragescript.ps1" Olá, clique em **ficheiro** > **guardar**. Em seguida, clique em **depurar** > **executar** ou prima **F5** script de Olá toorun.  

Após a execução do script Olá, deve ter uma pasta de destino local que inclua o ficheiro de imagem de Olá transferido. Olá seguinte captura de ecrã mostra um exemplo de saída:

![Transferir Blobs](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> Olá "com o PowerShell e o armazenamento do Azure em 5 minutos" secção introdução fornecida uma introdução rápida sobre toouse Azure PowerShell com o Storage do Azure. Para obter informações detalhadas e instruções, Aconselhamo-lo Olá tooread secções a seguir.
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a>Pré-requisitos para utilizar o Azure PowerShell com o Storage do Azure
Precisa de uma conta e subscrição toorun Olá cmdlets do Azure PowerShell fornecidos neste guia, conforme descrito acima.

O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell. Para obter informações sobre como instalar e configurar o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Recomendamos que pode transfere e instalar ou atualizar o módulo Azure PowerShell mais recente do toohello antes de utilizar este guia.

Pode executar cmdlets Olá na consola do Olá padrão do Windows PowerShell ou Olá Windows PowerShell Integrated Scripting Environment (ISE). Por exemplo, tooopen **ISE do Windows PowerShell**, aceda toohello menu de iniciar, escreva ferramentas administrativas e clique em toorun-lo. Na janela do Olá ferramentas administrativas, clique no ISE do Windows PowerShell, clique em executar como administrador.

## <a name="how-toomanage-storage-accounts-in-azure"></a>Como contas de armazenamento toomanage no Azure

Vamos observe gerir contas do storage no Azure com o PowerShell

### <a name="how-tooset-a-default-azure-subscription"></a>Como tooset uma predefinição de subscrição do Azure
toomanage o Storage do Azure com o Azure PowerShell, terá de tooauthenticate cliente ambiente com o Azure através de autenticação do Azure Active Directory ou a autenticação baseada em certificado. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) tutorial. Este guia utiliza a autenticação do Azure Active Directory de Olá.

1. No ISE do Windows PowerShell, escreva o Olá tooadd de comando a seguir a conta do Azure toohello PowerShell ambiente local:

    ```powershell
    Add-AzureAccount
    ```

2. Na janela de "Iniciar sessão tooMicrosoft Azure" Olá, endereço de correio eletrónico do tipo Olá e palavra-passe associada à sua conta. Azure autentica guarda as informações de credencial de Olá e, em seguida, fecha a janela de Olá.

3. Em seguida, execute Olá Olá tooview de comandos do Azure contas no seu ambiente de PowerShell local e verifique se a sua conta é apresentada a seguir:
   
    ```powershell
    Get-AzureAccount
    ```
4. Em seguida, executar Olá seguintes cmdlet tooview todas as subscrições de Olá que estão ligados toohello local a sessão do PowerShell e certifique-se de que a sua subscrição está listada:

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. tooset uma predefinição de subscrição do Azure, execute o cmdlet Olá Select-AzureSubscription:

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. Verifique o nome de Olá da subscrição da predefinição de Olá executando o cmdlet Get-AzureSubscription de Olá:

    ```powershell
    Get-AzureSubscription -Default
    ```

7. toosee todos os Olá disponíveis cmdlets do PowerShell para o armazenamento do Azure, execute:
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a>Como toocreate uma nova conta de armazenamento do Azure
toouse storage do Azure, terá de uma conta de armazenamento. Pode criar uma nova conta de armazenamento do Azure após ter configurado a sua subscrição do computador tooconnect tooyour.

1. Execute Olá Get-AzureLocation cmdlet toofind todas as localizações de centros de dados disponíveis Olá:

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. Em seguida, execute Olá AzureStorageAccount novo cmdlet toocreate uma nova conta de armazenamento. Olá exemplo seguinte cria uma nova conta de armazenamento no Centro de dados do Olá "EUA Oeste".
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> nome de Olá da sua conta de armazenamento tem de ser exclusivo no Azure e tem de ser em minúsculas. Para as convenções de nomenclatura e restrições, consulte [sobre contas de armazenamento do Azure](storage-create-storage-account.md) e [nomenclatura e referência de contentores, Blobs e metadados](http://msdn.microsoft.com/library/azure/dd135715.aspx).
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a>Como tooset uma conta de armazenamento do Azure predefinida
Pode ter várias contas de armazenamento na sua subscrição. Pode escolher um deles e defina-o como conta do storage predefinida Olá para todos os Olá armazenamento comandos no Olá mesma sessão do PowerShell. Isto permite-lhe os comandos do toorun Olá Azure PowerShell armazenamento sem especificar o contexto de armazenamento Olá explicitamente.

1. tooset uma conta de armazenamento predefinido para a sua subscrição, pode executar o cmdlet do Set-AzureSubscription de Olá.

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. Em seguida, execute Olá Get-AzureSubscription cmdlet tooverify que a conta de armazenamento Olá está associada a sua conta de subscrição predefinida. Este comando devolve as propriedades de subscrição de Olá na subscrição atual Olá, incluindo a respetiva conta de armazenamento atual.

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a>Como toolist todo o armazenamento do Azure contas numa subscrição
Cada subscrição do Azure pode ter segurança too100 contas de armazenamento. Para informações mais atualizadas à sua Olá, nos limites, consulte [subscrição do Azure e limites de serviço, Quotas e restrições](../azure-subscription-service-limits.md).

Execute Olá cmdlet toofind nome Olá e estado Olá de contas de armazenamento na subscrição atual Olá os seguintes:

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a>Como toocreate um contexto de armazenamento do Azure
O contexto de armazenamento do Azure é um objeto de credenciais de armazenamento do PowerShell tooencapsulate Olá. Utilizar um contexto de armazenamento durante a execução de qualquer cmdlet subsequente permite tooauthenticate o pedido sem especificar explicitamente a conta de armazenamento Olá e a sua chave de acesso. Pode criar um contexto de armazenamento em várias formas, como a chave de acesso e o nome de conta do storage, token de assinatura (SAS) de acesso partilhado, cadeia de ligação, ou anonymous. Para obter mais informações, consulte [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).  

Utilize um dos seguintes três formas toocreate de Olá um contexto de armazenamento:

* Executar Olá [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) toofind cmdlet terminar a chave de acesso de armazenamento primário Olá para a sua conta de armazenamento do Azure. Em seguida, chame Olá [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate um contexto de armazenamento:

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* Gerar um token de assinatura de acesso partilhado para um contentor de armazenamento do Azure e utilizá-lo toocreate um contexto de armazenamento:

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    Para obter mais informações, consulte [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) e [através de acesso partilhado assinaturas (SAS)](storage-dotnet-shared-access-signature-part-1.md).

* Em alguns casos, poderá ser útil pontos finais de serviço do toospecify Olá quando criar um contexto de armazenamento nova. Isto poderá ser necessário quando tiver registado um nome de domínio personalizado para a sua conta de armazenamento com o serviço de Blob Olá ou se quiser toouse uma assinatura de acesso partilhado para aceder a recursos de armazenamento. Defina pontos finais de serviço Olá numa cadeia de ligação e utilizá-lo toocreate um contexto de armazenamento novo conforme mostrado abaixo:

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

Para obter mais informações sobre como tooconfigure uma cadeia de ligação de armazenamento, consulte [configurar cadeias de ligação](storage-configure-connection-string.md).

Agora que tem de configurar o computador e aprendeu como toomanage subscrições e contas de armazenamento com o Azure PowerShell, volte toohello seguinte secção toolearn como blobs toomanage do Azure e instantâneos do blob.

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a>Como tooretrieve e voltar a gerar chaves de armazenamento do Azure
Uma conta de armazenamento do Azure inclui duas chaves de conta. Pode utilizar Olá seguintes cmdlet tooretrieve as suas chaves.

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

Utilize Olá seguintes cmdlet tooretrieve uma chave específica. Os valores válidos são principais e secundários.  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

Se quiser tooregenerate as chaves, utilize Olá seguinte cmdlet. Valores válidos para - KeyType são "Primário" ou "Secundário"

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a>Como blobs toomanage do Azure
Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, tais como texto ou dados binários, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS. Esta secção assume que já estiver familiarizado com conceitos de serviço de armazenamento de Blobs do Azure Olá. Para obter informações detalhadas, consulte [introdução ao Blob storage através do .NET](storage-dotnet-how-to-use-blobs.md) e [conceitos do serviço Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="how-toocreate-a-container"></a>Como toocreate um contentor
Todos os BLOBs no armazenamento do Azure tem de ser um contentor. Pode criar um contentor privado utilizando o cmdlet Olá AzureStorageContainer novo:

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> Existem três níveis de acesso de leitura anónimo: **desativar**, **Blob**, e **contentor**. tooprevent anónimo tooblobs, parâmetro de permissão de Olá do conjunto de acesso demasiado**desativar**. Por predefinição, o novo contentor de Olá é privado e pode ser acedido apenas por proprietário da conta Olá. público anónimo tooallow ler tooblob aceder a recursos, mas não toocontainer metadados ou toohello uma lista de blobs no contentor de Olá, defina o parâmetro de permissão de Olá demasiado**Blob**. público completa tooallow ler tooblob aceder a recursos, os metadados do contentor e Olá lista de blobs no contentor de Olá, defina o parâmetro de permissão de Olá demasiado**contentor**. Para obter mais informações, consulte [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md).
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a>Como tooupload um blob para um contentor
O Blob Storage do Azure suporta blobs de blocos e blobs de páginas. Para obter mais informações, consulte [compreender os Blobs de blocos, os BLobs de acréscimo e Blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload os blobs no contentor de tooa, pode utilizar Olá [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet. Por predefinição, este comando carrega o blob de bloco tooa do Olá ficheiros locais. tipo de Olá toospecify para BLOBs Olá, pode utilizar o parâmetro de - BlobType Olá.

Olá exemplo a seguir executa Olá [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget Olá todos os ficheiros na pasta especificada Olá e, em seguida, transmite-os cmdlet seguinte toohello utilizando o operador de pipeline de Olá. Olá [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet carrega o contentor de tooyour Olá ficheiros locais:

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a>Como toodownload blobs a partir de um contentor
Olá seguinte o exemplo demonstra como toodownload blobs a partir de um contentor. exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento utilizando Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso primária. Em seguida, o exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet. Em seguida, o exemplo de Olá utiliza Olá [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) blobs de toodownload cmdlet na pasta de destino local Olá.

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a>Como toocopy blobs a partir de um tooanother de contentor de armazenamento
Pode copiar os blobs em contas do storage e regiões no modo assíncrono. Olá exemplo seguinte demonstra como toocopy blobs do armazenamento de um contentor tooanother em duas contas de armazenamento diferente. exemplo de Olá primeiro define variáveis para contas de armazenamento de origem e de destino e, em seguida, cria um contexto de armazenamento para cada conta. Em seguida, o exemplo de Olá copia blobs a partir Olá origem contentor toohello destino contentor utilizando Olá [início AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet. exemplo de Olá assume que contas de armazenamento de origem e destino Olá e contentores de existir.

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

Tenha em atenção que este exemplo efetua uma cópia assíncrona. Pode monitorizar o estado de Olá de cada cópia executando Olá [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.

### <a name="how-toocopy-blobs-from-a-secondary-location"></a>Como toocopy blobs a partir de uma localização secundária
Pode copiar os blobs da localização secundária de Olá de uma conta ativada RA-GRS.

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a>Como toodelete um blob
toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame o cmdlet Remove-AzureStorageBlob de Olá no mesmo. Olá seguinte o exemplo elimina todos os blobs Olá num determinado contentor. exemplo de Olá primeiro define as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento. Em seguida, o exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá e executa o cmdlet [remover AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs a partir de um contentor no armazenamento do Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a>Como instantâneos do blob toomanage do Azure
Azure permite-lhe criar um instantâneo de um blob. Um instantâneo é uma versão só de leitura de um blob que é executada num ponto no tempo. Assim que tiver sido criado um instantâneo,-lo pode ser ler, copiar, ou eliminada, mas não modificado. Os instantâneos proporcionar uma tooback de forma a segurança de um blob como é apresentado um momento. Para obter mais informações, consulte [criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).

### <a name="how-toocreate-a-blob-snapshot"></a>Como toocreate um instantâneo de blob
toocreate um snaphot de um blob, obtenha primeiro uma referência de blob e, em seguida, chame Olá `ICloudBlob.CreateSnapshot` método. Olá exemplo seguinte define primeiro as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento. Em seguida, o exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá e executa o cmdlet [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a>Como instantâneos de toolist um blob
Pode criar tantas instantâneos quantas quiser a um blob. Pode listar os instantâneos de Olá associados à sua tootrack blob os instantâneos atuais. Olá exemplo seguinte utiliza uma Olá predefinida de blob e chamadas [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) instantâneos de Olá toolist cmdlet desse blob.  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a>Como toocopy um instantâneo de um blob
Pode copiar um instantâneo de um instantâneo do blob toorestore Olá. Para obter informações detalhadas e restrições, consulte [criar um instantâneo de um Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx). Olá exemplo seguinte define primeiro as variáveis para uma conta de armazenamento e, em seguida, cria um contexto de armazenamento. Em seguida, o exemplo de Olá define variáveis de nome de contentor e BLOBs Olá. exemplo de Olá obtém uma referência de blob utilizando Olá [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) Olá e executa o cmdlet [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) método toocreate um instantâneo. Em seguida, o exemplo de Olá executa Olá [início AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy Olá instantâneo um blob utilizando o objeto de ICloudBlob de Olá de blob de origem Olá. Certifique-se as variáveis de Olá tooupdate com base na sua configuração antes de exemplo de Olá em execução. Tenha em atenção que Olá seguinte o exemplo assume que Olá contentores de origem e de destino e o blob de origem Olá já existe.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

Agora que tem aprendeu como toomanage Azure blobs e BLOBs instantâneos com o Azure PowerShell, aceda a toolearn de secção seguinte toohello como toomanage tabelas, filas e os ficheiros.

## <a name="how-toomanage-azure-tables-and-table-entities"></a>Como toomanage Azure tabelas e entidades de tabela
Serviço de armazenamento de tabela do Azure é um arquivo de dados NoSQL, que pode utilizar toostore e consultar conjuntos enormes de dados estruturados não relacionais. componentes principais do Olá do serviço de Olá são propriedades, tabelas e entidades. Uma tabela é uma coleção de entidades. Uma entidade é um conjunto de propriedades. Cada entidade pode ter propriedades de too252, que são todos os pares nome-valor. Esta secção assume que já estiver familiarizado com conceitos de serviço de armazenamento do Azure tabela Olá. Para obter informações detalhadas, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx) e [introdução ao Table storage do Azure através do .NET](storage-dotnet-how-to-use-tables.md).

Olá subsecções a seguir, irá aprender como toomanage Table storage do Azure service com o Azure PowerShell. Hello os cenários abrangidos incluem **criar**, **eliminar**, e **obter** **tabelas**, bem como **adicionar**, **consultar**, e **eliminar as entidades da tabela**.

### <a name="how-toocreate-a-table"></a>Como toocreate uma tabela
Cada tabela têm de residir numa conta de armazenamento do Azure. Olá exemplo seguinte demonstra como toocreate uma tabela no armazenamento do Azure. exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar. Em seguida, utiliza Olá [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate uma tabela no armazenamento do Azure.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a>Como tooretrieve uma tabela
Pode consultar e obter uma ou todas as tabelas numa conta do Storage. Olá exemplo seguinte demonstra como tooretrieve utilizando uma tabela indicada Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

Se chamar o cmdlet Get-AzureStorageTable de Olá sem quaisquer parâmetros, obtém todas as tabelas de armazenamento para uma conta de armazenamento.

### <a name="how-toodelete-a-table"></a>Como toodelete uma tabela
Pode eliminar uma tabela a partir de uma conta de armazenamento utilizando Olá [remover AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a>Como toomanage tabela entidades
Atualmente, o Azure PowerShell não fornece as entidades da tabela toomanage cmdlets diretamente. operações de tooperform em entidades de tabela, pode utilizar classes Olá indicadas na Olá [biblioteca de clientes do Storage do Azure para .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).

#### <a name="how-tooadd-table-entities"></a>Como tooadd tabela entidades
tooadd uma tabela de tooa de entidade, primeiro crie um objeto que define as propriedades de entidade. Uma entidade pode ter propriedades de too255, incluindo 3 Propriedades do sistema: **PartitionKey**, **RowKey**, e **Timestamp**. É responsável por a inserir e a atualizar os valores de Olá de **PartitionKey** e **RowKey**. Olá servidor gere valor Olá **Timestamp**, que não pode ser modificado. Em conjunto Olá **PartitionKey** e **RowKey** identificar de forma exclusiva cada entidade dentro de uma tabela.

* **PartitionKey**: determina partição Olá entidade Olá armazenadas.
* **RowKey**: identifica de forma exclusiva a entidade de Olá dentro de partição Olá.

Pode definir too252 propriedades personalizadas para uma entidade. Para obter mais informações, consulte [Olá compreender o modelo de dados do serviço tabela](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Olá exemplo seguinte demonstra como tabela de tooa tooadd entidades. exemplo de Olá mostra como tooretrieve Olá tabela do empregado e adiciona várias entidades. Em primeiro lugar, estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar. Em seguida, obtém Olá fornecido tabela utilizando Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Se a tabela Olá não existe, Olá [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet é utilizado toocreate uma tabela no armazenamento do Azure. Em seguida, o exemplo Olá define uma tabela de toohello adicionar entidade tooadd entidades de função personalizada, especificando a partição de cada entidade e a chave de linha. Olá de chamadas de função Olá adicionar entidade [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet no Olá [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) classe toocreate um objeto de entidade. Posteriormente, o exemplo de Olá chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) método neste tooadd de objeto de entidade tooa tabela.

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a>Como tooquery tabela entidades
tooquery uma tabela, utilize Olá [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) classe. Olá seguinte exemplo assume que já tiver executado script Olá indicada na Olá como secção de entidades tooadd deste guia. exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento utilizando o contexto de armazenamento de Olá, que inclui o nome de conta do storage Olá e a sua chave de acesso. Em seguida, este tenta tooretrieve Olá criado anteriormente "funcionários" tabela, utilizando Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Chamar Olá [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet no Olá Microsoft.WindowsAzure.Storage.Table.TableQuery classe cria um novo objeto de consulta. exemplo de Olá procura entidades Olá que têm uma coluna de 'ID' cujo valor é 1 conforme especificado num filtro de cadeia. Para obter informações detalhadas, consulte [consultar tabelas e entidades](http://msdn.microsoft.com/library/azure/dd894031.aspx). Quando executar esta consulta, devolve todas as entidades que correspondem aos critérios de filtro de Olá.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a>Como toodelete tabela entidades
Pode eliminar uma entidade com as chaves de partição e linha. Olá seguinte exemplo assume que já tiver executado script Olá indicada na Olá como secção de entidades tooadd deste guia. exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento utilizando o contexto de armazenamento de Olá, que inclui o nome de conta do storage Olá e a sua chave de acesso. Em seguida, este tenta tooretrieve Olá criado anteriormente "funcionários" tabela, utilizando Olá [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet. Se existir a tabela de Olá, o exemplo de Olá chama Olá [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) tooretrieve método uma entidade com base nos seus valores de chave de partição e da fila. Em seguida, passe Olá entidade toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete de método.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a>Como toomanage Azure filas e mensagens de fila de espera
Armazenamento de filas do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acedidas de qualquer local no mundo Olá através de chamadas autenticadas com HTTP ou HTTPS. Esta secção assume que já estiver familiarizado com conceitos do serviço de armazenamento de filas do Azure de Olá. Para obter informações detalhadas, consulte [introdução ao armazenamento de filas do Azure através do .NET](storage-dotnet-how-to-use-queues.md).

Esta secção irá mostrar como toomanage armazenamento de filas do Azure service com o Azure PowerShell. Olá os cenários abrangidos incluem **a inserir** e **eliminar** fila de mensagens, bem como **criar**, **eliminar**e **obter filas**.

### <a name="how-toocreate-a-queue"></a>Como toocreate uma fila
Olá exemplo seguinte primeiro estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar. Em seguida, chama [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate uma fila com o nome 'queuename'.

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

Para informações sobre as convenções de nomenclatura para o serviço de fila do Azure, consulte [nomenclatura de filas e metadados](http://msdn.microsoft.com/library/azure/dd179349.aspx).

### <a name="how-tooretrieve-a-queue"></a>Como tooretrieve uma fila
Pode consultar e obter uma fila específica ou uma lista de todas as filas de Olá numa conta do Storage. Olá exemplo seguinte demonstra como tooretrieve uma fila especificada utilizando Olá [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

Se chamar Olá [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet sem quaisquer parâmetros, obtém uma lista de todas as filas de Olá.

### <a name="how-toodelete-a-queue"></a>Como toodelete uma fila
toodelete uma fila e todas as mensagens de Olá nela contidas, chamada Olá remover AzureStorageQueue cmdlet. Olá seguinte exemplo mostra como toodelete uma fila especificada utilizando Olá cmdlet Remove-AzureStorageQueue.

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a>Como tooinsert uma mensagem para uma fila
em primeiro lugar, tooinsert uma mensagem numa fila existente, crie uma nova instância do Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Em seguida, chame Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método. Um CloudQueueMessage pode ser criado a partir de uma cadeia (no formato UTF-8) ou uma matriz de bytes.

Olá seguinte o exemplo demonstra como tooadd mensagem tooa fila. exemplo de Olá primeiro estabelece uma ligação tooAzure armazenamento Olá armazenamento contexto da conta, que inclui o nome de conta do storage Olá e a sua chave de acesso a utilizar. Em seguida, obtém fila especificada Olá utilizando Olá [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet. Se a fila de Olá, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet é utilizado toocreate uma instância de Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) classe. Posteriormente, o exemplo de Olá chama Olá [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) método neste tooadd de objeto de mensagem tooa fila. Eis o código que obtém uma fila e insere a mensagem de saudação 'MessageInfo':

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a>Como a fila toode em Olá junto da mensagem
O código remove uma mensagem da fila em dois passos. Quando chamar Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) método, obterá Olá a seguinte mensagem numa fila. Uma mensagem devolvida por **GetMessage** torna-se invisível tooany outro código de leitura de mensagens desta fila. toofinish remover mensagem de saudação da fila de Olá, também tem de chamar Olá [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) método. Este processo de dois passos da remoção de uma mensagem garante que se o código de falha tooprocess que pode obter uma mensagem devido a falha de toohardware ou de software, outra instância do seu código Olá a mesma mensagem e tente novamente. As chamadas de código **DeleteMessage** imediatamente após a mensagem de saudação foi processada.

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a>Como toomanage ficheiros do Azure partilhas e ficheiros
File storage do Azure oferece um armazenamento partilhado para aplicações utilizando o protocolo SMB padrão do Olá. Máquinas virtuais do Microsoft Azure e serviços em nuvem podem partilhar os dados de ficheiros em componentes da aplicação através de partilhas montadas e as aplicações no local podem aceder a dados de ficheiros numa partilha através da API de armazenamento de ficheiros de Olá ou do Azure PowerShell.

Para obter mais informações sobre o File storage do Azure, consulte [introdução ao File storage do Azure no Windows](storage-dotnet-how-to-use-files.md) e [API de REST do serviço de ficheiro](http://msdn.microsoft.com/library/azure/dn167006.aspx).

## <a name="how-tooset-and-query-storage-analytics"></a>Como tooset e a consulta de análise de armazenamento
Pode utilizar [análise de armazenamento do Azure](storage-analytics.md) toocollect métricas para as suas contas do storage do Azure e dados de registo sobre pedidos enviados tooyour conta de armazenamento. Pode utilizar o armazenamento métricas toomonitor Olá estado de funcionamento de uma conta de armazenamento e armazenamento registo toodiagnose e resolver problemas com a sua conta de armazenamento. Pode configurar a monitorização utilizando Olá portal do Azure ou o Windows PowerShell ou através de programação utilizando a biblioteca de clientes do storage Olá. Registo de armazenamento acontece do lado do servidor e permite-lhe detalhes toorecord para pedidos com êxito ou falhados na sua conta de armazenamento. Estes registos permitem-lhe toosee detalhes de leitura, escrita e eliminação operações contra as tabelas, filas e blobs, bem como Olá algumas das razões para pedidos falhados.

toolearn como tooenable e ver as métricas do Storage de dados com o PowerShell, consulte [como tooenable as métricas do Storage através do PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).

toolearn como tooenable e obter registos de armazenamento de dados com o PowerShell, consulte [como tooenable armazenamento registo com o PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) e [localizar os dados de registo registo armazenamento](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).
Para obter informações detalhadas sobre como utilizar as métricas do Storage e armazenamento registo tootroubleshoot problemas de armazenamento, consulte [monitorização, Diagnosing e resolução de problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a>Como toomanage partilhado (SAS) de assinatura de acesso e política de acesso armazenada
Assinaturas de acesso partilhado são uma parte importante do modelo de segurança de Olá para qualquer aplicação utilizando o armazenamento do Azure. Estes são úteis para fornecer permissões limitadas tooyour armazenamento conta tooclients que não devem ter a chave de conta Olá. Por predefinição, só o proprietário Olá Olá de conta do storage pode aceder a blobs, tabelas e filas dentro dessa conta. Se a sua aplicação ou serviço necessitar da toomake estes clientes de tooother disponíveis recursos sem partilha a sua chave de acesso, tem três opções:

* Defina toopermit acesso de leitura anónimo toohello contentor para um contentor permissões e os respetivos blobs. Não é permitida para tabelas ou filas.
* Utilize uma assinatura de acesso partilhado que concede acesso restrito direitos toocontainers, blobs, filas e tabelas para um intervalo de tempo específico.
* Utilize um tooobtain de política de acesso armazenado um nível adicional de controlo sobre assinaturas de acesso partilhado para um contentor ou os respetivos blobs, para uma fila ou para uma tabela. Olá política de acesso armazenada permite-lhe a hora de início toochange Olá, hora de expiração ou permissões para uma assinatura ou toorevoke-lo Depois foi emitido.

Pode ser uma assinatura de acesso partilhado de uma das duas formas:

* **SAS ad hoc**: Quando cria um SAS ad hoc, a hora de início de Olá, a hora de expiração e as permissões para Olá SAS são especificadas no Olá URI de SAS. Este tipo de SAS que pode ser criado num contentor de blob, tabela ou fila que é não revocable.
* **SAS com a política de acesso armazenada**: uma política de acesso armazenada está definida um contentor de recursos um contentor de blob, tabela ou fila - e pode utilizá-lo toomanage restrições para um ou mais assinaturas de acesso partilhado. Quando associa um SAS com uma política de acesso armazenada, Olá SAS herda as restrições de Olá - Olá iniciar tempo, hora de expiração e permissões - definidas para a política de acesso de Olá armazenado. Este tipo de SAS é revocable.

Para obter mais informações, consulte [através de acesso partilhado assinaturas (SAS)](storage-dotnet-shared-access-signature-part-1.md) e [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md).

Olá secções seguintes, irá aprender como toocreate uma política de acesso de token e armazenadas de assinatura de acesso partilhado para as tabelas do Azure. O Azure PowerShell fornece cmdlets semelhantes para contentores, blobs e filas bem. scripts de Olá toorun nesta secção, transferir Olá [Azure PowerShell versão 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) ou posterior.

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a>Como toocreate uma política com base no token de assinatura de acesso partilhado
Utilize Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenada. Em seguida, chame Olá [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo token de assinatura de baseado em política de acesso partilhado para uma tabela de armazenamento do Azure.

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a>Como toocreate um token de assinatura de acesso partilhado (não revocable) ad hoc
Olá utilize [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate um novo ad hoc (não revocable) assinatura de acesso partilhado token para uma tabela de armazenamento do Azure:

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a>Como toocreate uma política de acesso armazenada
Utilize Olá AzureStorageTableStoredAccessPolicy novo cmdlet toocreate uma nova política de acesso armazenados para uma tabela de armazenamento do Azure:

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a>Como tooupdate uma política de acesso armazenada
Utilize Olá conjunto AzureStorageTableStoredAccessPolicy cmdlet tooupdate uma política de acesso armazenada existente para uma tabela de armazenamento do Azure:

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a>Como toodelete uma política de acesso armazenada
Utilize Olá remover AzureStorageTableStoredAccessPolicy cmdlet toodelete uma política de acesso armazenados numa tabela de armazenamento do Azure:

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a>Como toouse Storage do Azure dos EUA e o Azure China
Um ambiente do Azure é uma implementação independentemente do Microsoft Azure, tal como [Azure Government para EUA](https://azure.microsoft.com/features/gov/), [AzureCloud para o global Azure](https://portal.azure.com), e [AzureChinaCloud para o Azure operado pela 21Vianet na China](http://www.windowsazure.cn/). Pode implementar novos ambientes do Azure para U.S government e o Azure China.

Storage do Azure com AzureChinaCloud toouse, terá de toocreate um contexto de armazenamento que estão associado com AzureChinaCloud. Siga estes tooget passos tiver iniciado:

1. Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Olá ambientes do Azure disponíveis:
   
    ```powershell
    Get-AzureEnvironment
    ```

2. Adicione um tooWindows de conta do Azure China do PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. Crie um contexto de armazenamento para uma conta de AzureChinaCloud:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

toouse Storage do Azure com [E.U.A. Azure Government](https://azure.microsoft.com/features/gov/), deve definir um novo ambiente e, em seguida, criar um contexto de armazenamento novo com este ambiente:

1. Executar Olá [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Olá ambientes do Azure disponíveis:

    ```powershell
    Get-AzureEnvironment
    ```

2. Adicione um tooWindows de conta do Azure US Government do PowerShell:
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. Crie um contexto de armazenamento para uma conta de AzureUSGovernment:
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
Para obter mais informações, consulte:

* [Guia para programadores do Microsoft Azure Government](../azure-government-developer-guide.md).
* [Descrição geral das diferenças quando criar uma aplicação no serviço China](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a>Passos Seguintes
Neste guia, aprendeu como toomanage Storage do Azure com o Azure PowerShell. Aqui estão alguns artigos relacionados e recursos para aprender mais sobre os mesmos.

* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Cmdlets do PowerShell do Storage do Azure](/powershell/module/azurerm.storage/#storage)
* [Referência do Windows PowerShell](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
