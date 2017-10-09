---
title: registos de aaaIntegrate a partir do Cofre de chaves do Azure com os Hubs de eventos | Microsoft Docs
description: "Tutorial que fornece os passos necessários de Olá toomake Cofre de chaves de registo disponível tooa SIEM utilizando a integração de registo do Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="ea97f-103">Tutorial de integração de registo do Azure: eventos de Cofre de chaves do Azure de processo ao utilizar os Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="ea97f-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="ea97f-104">Pode utilizar a integração de registo do Azure tooretrieve registado eventos e torná-los tooyour disponíveis informações e event management (SIEM) sistema de segurança.</span><span class="sxs-lookup"><span data-stu-id="ea97f-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="ea97f-105">Este tutorial mostra um exemplo de como a integração de registo do Azure podem ser utilizados tooprocess registos adquiridos junto de Event Hubs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea97f-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="ea97f-106">Utilize este tutorial tooget acquainted com a forma como a integração de registo do Azure e do Event Hubs trabalho em conjunto pela seguinte Olá passos de exemplo e compreender a forma como cada passo suporta solução Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="ea97f-107">Em seguida, pode tirar o que aprendeu aqui toocreate o seus próprios toosupport passos requisitos exclusivos da sua empresa.</span><span class="sxs-lookup"><span data-stu-id="ea97f-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="ea97f-108">passos de Olá e comandos neste tutorial não são toobe pretendido copiados e colados.</span><span class="sxs-lookup"><span data-stu-id="ea97f-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="ea97f-109">Se estiver a apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="ea97f-109">They're examples only.</span></span> <span data-ttu-id="ea97f-110">Não utilize comandos do PowerShell Olá "tal como está" no seu ambiente em direto.</span><span class="sxs-lookup"><span data-stu-id="ea97f-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="ea97f-111">Devem ser personalizadas com base no seu ambiente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="ea97f-112">Este tutorial orienta-o através de processo de Olá de colocar o hub de eventos do Cofre de chaves do Azure atividade tooan com sessão iniciada e disponibilizar como sistema do JSON ficheiros tooyour SIEM.</span><span class="sxs-lookup"><span data-stu-id="ea97f-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="ea97f-113">Em seguida, pode configurar os SIEM sistema tooprocess Olá JSON os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="ea97f-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="ea97f-114">A maior parte dos passos deste tutorial Olá envolve configurar cofres de chaves, contas de armazenamento e dos event hubs.</span><span class="sxs-lookup"><span data-stu-id="ea97f-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="ea97f-115">os passos de integração de registo do Azure específicos Olá estão no final deste tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="ea97f-116">Não execute estes passos num ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ea97f-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="ea97f-117">Estes destinam-se apenas num ambiente de laboratório.</span><span class="sxs-lookup"><span data-stu-id="ea97f-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="ea97f-118">Tem de personalizar os passos de Olá antes de os utilizar na produção.</span><span class="sxs-lookup"><span data-stu-id="ea97f-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="ea97f-119">Foram fornecidas informações ao longo de ajuda de forma Olá que compreender motivos Olá atrás de cada passo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="ea97f-120">Artigos de tooother ligações dão-lhe mais detalhes em determinados tópicos.</span><span class="sxs-lookup"><span data-stu-id="ea97f-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="ea97f-121">Para obter mais informações sobre os serviços de Olá menciona suportadas neste tutorial, consulte:</span><span class="sxs-lookup"><span data-stu-id="ea97f-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="ea97f-122">Cofre de Chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="ea97f-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="ea97f-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ea97f-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="ea97f-124">Integração de registos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea97f-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="ea97f-125">Configuração inicial</span><span class="sxs-lookup"><span data-stu-id="ea97f-125">Initial setup</span></span>

<span data-ttu-id="ea97f-126">Antes de concluir os passos de Olá neste artigo, é necessário o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ea97f-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="ea97f-127">Uma subscrição do Azure e a conta que subscrição com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="ea97f-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="ea97f-128">Se não tiver uma subscrição, pode criar um [conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ea97f-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="ea97f-129">Um sistema com toohello de acesso à internet que cumpra Olá os requisitos para instalar a integração de registo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea97f-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="ea97f-130">sistema Olá alojado no local ou pode ser num serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ea97f-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="ea97f-131">[Integração de registo do Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalado.</span><span class="sxs-lookup"><span data-stu-id="ea97f-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="ea97f-132">tooinstall-lo:</span><span class="sxs-lookup"><span data-stu-id="ea97f-132">tooinstall it:</span></span>

   <span data-ttu-id="ea97f-133">a.</span><span class="sxs-lookup"><span data-stu-id="ea97f-133">a.</span></span> <span data-ttu-id="ea97f-134">Utilize o sistema toohello tooconnect de ambiente de trabalho remoto mencionado no passo 2.</span><span class="sxs-lookup"><span data-stu-id="ea97f-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="ea97f-135">b.</span><span class="sxs-lookup"><span data-stu-id="ea97f-135">b.</span></span> <span data-ttu-id="ea97f-136">Copie o sistema de toohello instalador do Olá a integração de registo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea97f-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="ea97f-137">Pode [transferir ficheiros de instalação de Olá](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="ea97f-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="ea97f-138">c.</span><span class="sxs-lookup"><span data-stu-id="ea97f-138">c.</span></span> <span data-ttu-id="ea97f-139">Inicie o instalador Olá e aceitar os termos de licenciamento de Software do Olá Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea97f-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="ea97f-140">d.</span><span class="sxs-lookup"><span data-stu-id="ea97f-140">d.</span></span> <span data-ttu-id="ea97f-141">Se irá fornecer informações de telemetria, deixe a caixa de verificação de Olá selecionada.</span><span class="sxs-lookup"><span data-stu-id="ea97f-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="ea97f-142">Se seria não enviar tooMicrosoft de informações de utilização, desmarque a caixa de verificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="ea97f-143">Para obter mais informações sobre a integração de registo do Azure e como tooinstall-lo, consulte [a integração de registo do Azure com o registo de diagnóstico do Azure e o reencaminhamento de eventos do Windows](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ea97f-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="ea97f-144">versão de PowerShell mais recente Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="ea97f-145">Se tiver instalado o Windows Server 2016, em seguida, tiver, pelo menos, PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="ea97f-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="ea97f-146">Se estiver a utilizar qualquer outra versão do Windows Server, poderá ter uma versão anterior do PowerShell instalada.</span><span class="sxs-lookup"><span data-stu-id="ea97f-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="ea97f-147">Pode verificar a versão de Olá introduzindo ```get-host``` numa janela do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea97f-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="ea97f-148">Se não tiver PowerShell 5.0 instalado, pode [transferi-lo](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="ea97f-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="ea97f-149">Depois de ter, pelo menos, PowerShell 5.0, pode continuar a versão mais recente do tooinstall Olá:</span><span class="sxs-lookup"><span data-stu-id="ea97f-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="ea97f-150">a.</span><span class="sxs-lookup"><span data-stu-id="ea97f-150">a.</span></span> <span data-ttu-id="ea97f-151">Na janela do PowerShell, introduza Olá ```Install-Module Azure``` comando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="ea97f-152">Conclua os passos de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="ea97f-153">b.</span><span class="sxs-lookup"><span data-stu-id="ea97f-153">b.</span></span> <span data-ttu-id="ea97f-154">Introduza Olá ```Install-Module AzureRM``` comando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="ea97f-155">Conclua os passos de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="ea97f-156">Para obter mais informações, consulte [instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="ea97f-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="ea97f-157">Criar suporte de infraestrutura de elementos</span><span class="sxs-lookup"><span data-stu-id="ea97f-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="ea97f-158">Abra uma janela elevada do PowerShell e aceda demasiado**C:\Program Files\Microsoft Azure registo integração**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="ea97f-159">Importe Olá AzLog cmdlets ao executar o script de Olá LoadAzLogModule.ps1.</span><span class="sxs-lookup"><span data-stu-id="ea97f-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="ea97f-160">Introduza Olá `.\LoadAzLogModule.ps1` comando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="ea97f-161">(Olá de aviso ". \ \" nesse comando.) Deverá ver algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="ea97f-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Lista de módulos carregados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="ea97f-163">Introduza Olá `Login-AzureRmAccount` comando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="ea97f-164">Na janela de início de sessão de Olá, introduza as informações de credencial de Olá para a subscrição de Olá que irá utilizar para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ea97f-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="ea97f-165">Se este for Olá pela primeira vez que está a registar no tooAzure desta máquina, verá uma mensagem sobre dados de utilização do Microsoft toocollect do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea97f-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="ea97f-166">Recomendamos que ative a recolha de dados porque será utilizado tooimprove Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea97f-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="ea97f-167">Após a autenticação com êxito, tem sessão iniciada e ver informações Olá Olá seguinte captura de ecrã.</span><span class="sxs-lookup"><span data-stu-id="ea97f-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="ea97f-168">Tome nota do nome de ID e a subscrição da subscrição Olá, porque irá precisar deles mais tarde passos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ea97f-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![Janela do PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="ea97f-170">Crie variáveis toostore valores que serão utilizados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="ea97f-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="ea97f-171">Introduza cada um dos Olá seguintes linhas de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea97f-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="ea97f-172">Poderá ser necessário tooadjust Olá valores toomatch no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ea97f-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="ea97f-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(O nome da sua subscrição poderão ser diferente.</span><span class="sxs-lookup"><span data-stu-id="ea97f-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="ea97f-174">Pode vê-lo como parte da saída de Olá do comando anterior Olá.)</span><span class="sxs-lookup"><span data-stu-id="ea97f-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="ea97f-175">```$location = 'West US'```(Esta variável será onde devem ser criados os recursos de localização do Olá toopass utilizados.</span><span class="sxs-lookup"><span data-stu-id="ea97f-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="ea97f-176">Pode alterar esta variável toobe qualquer localização da sua escolha.)</span><span class="sxs-lookup"><span data-stu-id="ea97f-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="ea97f-177">``` $name = 'azlogtest' + $random```(nome de Olá pode ser qualquer coisa, mas deve incluir apenas letras minúsculas e números).</span><span class="sxs-lookup"><span data-stu-id="ea97f-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="ea97f-178">``` $storageName = $name```(Esta variável será utilizada para o nome de conta de armazenamento Olá).</span><span class="sxs-lookup"><span data-stu-id="ea97f-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="ea97f-179">```$rgname = $name ```(Esta variável será utilizada para o nome do grupo de recursos de Olá).</span><span class="sxs-lookup"><span data-stu-id="ea97f-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="ea97f-180">``` $eventHubNameSpaceName = $name```(Este é o nome de Olá do espaço de nomes de hub de eventos de Olá.)</span><span class="sxs-lookup"><span data-stu-id="ea97f-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="ea97f-181">Especifique a subscrição de Olá com os quais irão trabalhar com:</span><span class="sxs-lookup"><span data-stu-id="ea97f-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="ea97f-182">Criar um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="ea97f-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="ea97f-183">Se introduzir `$rg` neste momento, deverá ver a captura de ecrã saída semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="ea97f-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Saída após a criação de um grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="ea97f-185">Crie uma conta de armazenamento que será utilizado tookeep controlar de informações de estado:</span><span class="sxs-lookup"><span data-stu-id="ea97f-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="ea97f-186">Crie o espaço de nomes de hub de eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-186">Create hello event hub namespace.</span></span> <span data-ttu-id="ea97f-187">Isto é necessário toocreate um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea97f-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="ea97f-188">Obter ID de regra de Olá que será utilizado com o fornecedor de insights Olá:</span><span class="sxs-lookup"><span data-stu-id="ea97f-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="ea97f-189">Obter todas as localizações do Azure possíveis e adicionar Olá nomes tooa variável que pode ser utilizado num passo posterior:</span><span class="sxs-lookup"><span data-stu-id="ea97f-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="ea97f-190">a.</span><span class="sxs-lookup"><span data-stu-id="ea97f-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="ea97f-191">b.</span><span class="sxs-lookup"><span data-stu-id="ea97f-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="ea97f-192">Se introduzir `$locations` neste momento, ver os nomes de localização de Olá sem informações adicionais de Olá devolvidas pelo Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="ea97f-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="ea97f-193">Crie um perfil de registo do Gestor de recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="ea97f-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="ea97f-194">Para mais informações sobre Olá perfil de registos do Azure, consulte [descrição geral do Olá registo de atividade do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="ea97f-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ea97f-195">Poderá receber uma mensagem de erro quando tenta toocreate um perfil de registo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="ea97f-196">Em seguida, pode rever documentação Olá para Get-AzureRmLogProfile e Remove-AzureRmLogProfile.</span><span class="sxs-lookup"><span data-stu-id="ea97f-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="ea97f-197">Se executar Get-AzureRmLogProfile, pode ver informações sobre o perfil de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="ea97f-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="ea97f-198">Pode eliminar o perfil de registo existente Olá introduzindo Olá ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.</span><span class="sxs-lookup"><span data-stu-id="ea97f-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Erro de perfil do Gestor de recursos](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="ea97f-200">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="ea97f-200">Create a key vault</span></span>

1. <span data-ttu-id="ea97f-201">Crie Cofre de chaves de Olá:</span><span class="sxs-lookup"><span data-stu-id="ea97f-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="ea97f-202">Configure o registo para o Cofre de chaves Olá:</span><span class="sxs-lookup"><span data-stu-id="ea97f-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="ea97f-203">Gerar a atividade de registo</span><span class="sxs-lookup"><span data-stu-id="ea97f-203">Generate log activity</span></span>

<span data-ttu-id="ea97f-204">Pedidos necessitam toobe enviado tooKey atividade de registo do cofre toogenerate.</span><span class="sxs-lookup"><span data-stu-id="ea97f-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="ea97f-205">Ações, como a geração de chaves, armazenar segredos, ou ao ler os segredos do Cofre de chaves, irá criar entradas de registo.</span><span class="sxs-lookup"><span data-stu-id="ea97f-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="ea97f-206">Apresentar as chaves de armazenamento atual Olá:</span><span class="sxs-lookup"><span data-stu-id="ea97f-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="ea97f-207">Gerar um novo **key2**:</span><span class="sxs-lookup"><span data-stu-id="ea97f-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="ea97f-208">Voltar a apresentar chaves Olá e ver que **key2** contém um valor diferente:</span><span class="sxs-lookup"><span data-stu-id="ea97f-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="ea97f-209">Defina e ler um segredo toogenerate entradas de registo adicionais:</span><span class="sxs-lookup"><span data-stu-id="ea97f-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="ea97f-210">a.</span><span class="sxs-lookup"><span data-stu-id="ea97f-210">a.</span></span> <span data-ttu-id="ea97f-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="ea97f-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Devolveu secreta](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="ea97f-213">Configurar a integração de registos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea97f-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="ea97f-214">Agora que configurou o hub de eventos de tooan de registo do Cofre de chaves Olá elementos necessários toohave todos os, terá de tooconfigure a integração de registo do Azure:</span><span class="sxs-lookup"><span data-stu-id="ea97f-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="ea97f-215">Execute o comando de AzLog Olá para cada hub de eventos:</span><span class="sxs-lookup"><span data-stu-id="ea97f-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="ea97f-216">Depois de um minuto ou da execução Olá últimos dois comandos, deve ver ficheiros JSON que está a ser gerados.</span><span class="sxs-lookup"><span data-stu-id="ea97f-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="ea97f-217">Pode confirmar que pela monitorização de diretório de Olá **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="ea97f-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea97f-218">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ea97f-218">Next steps</span></span>

- [<span data-ttu-id="ea97f-219">Integração de registos do Azure FAQ</span><span class="sxs-lookup"><span data-stu-id="ea97f-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="ea97f-220">Introdução à integração do registo do Azure</span><span class="sxs-lookup"><span data-stu-id="ea97f-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="ea97f-221">Integrar o seu sistemas SIEM registos de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ea97f-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
