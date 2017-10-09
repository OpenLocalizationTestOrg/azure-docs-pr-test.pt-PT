---
title: "monitorização com alertas e as funções do Azure de rede de toodo de captura de pacotes aaaUse proativa | Microsoft Docs"
description: Este artigo descreve como toocreate um alerta acionado captura de pacotes com observador de rede do Azure
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="8ba55-103">Captura de pacotes de utilização para a rede proativa monitorização com alertas e as funções do Azure</span><span class="sxs-lookup"><span data-stu-id="8ba55-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="8ba55-104">Captura de pacotes do observador de rede cria captura sessões tootrack tráfego que entra e sai de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8ba55-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="8ba55-105">Olá ficheiro de captura pode ter um filtro que está definido tootrack Olá apenas o tráfego que pretende que o toomonitor.</span><span class="sxs-lookup"><span data-stu-id="8ba55-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="8ba55-106">Estes dados, em seguida, são armazenados no blob de armazenamento ou localmente no computador convidado de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="8ba55-107">Esta capacidade pode ser iniciada remotamente a partir de outros cenários de automatização, tais como as funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba55-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="8ba55-108">Oferece de captura de pacotes que Hello capturas de proativa de capacidade toorun com base no definido anomalias de rede.</span><span class="sxs-lookup"><span data-stu-id="8ba55-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="8ba55-109">Outras utilizações incluem a recolha de estatísticas de rede, ao obter informações sobre intrusions de rede, as comunicações de cliente-servidor depuração e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8ba55-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="8ba55-110">Recursos que são implementados no Azure executados 24x7.</span><span class="sxs-lookup"><span data-stu-id="8ba55-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="8ba55-111">Utilizador e a sua equipa ativamente não é possível monitorizar o estado de Olá de todos os recursos 24/7.</span><span class="sxs-lookup"><span data-stu-id="8ba55-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="8ba55-112">Por exemplo, o que acontece se ocorrer um problema às 2 AM?</span><span class="sxs-lookup"><span data-stu-id="8ba55-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="8ba55-113">Ao utilizar o observador de rede, alertas e funções a partir de Olá ecossistema do Azure, pode responder proativamente com problemas de toosolve de dados e as ferramentas de Olá na sua rede.</span><span class="sxs-lookup"><span data-stu-id="8ba55-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Cenário][scenario]

## <a name="prerequisites"></a><span data-ttu-id="8ba55-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ba55-115">Prerequisites</span></span>

* <span data-ttu-id="8ba55-116">versão mais recente do Olá do [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8ba55-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="8ba55-117">Uma instância existente do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="8ba55-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="8ba55-118">Se ainda não tiver um, [criar uma instância do observador de rede](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="8ba55-119">Uma máquina virtual existente no Olá mesma região que o observador de rede com Olá [extensão Windows](../virtual-machines/windows/extensions-nwa.md) ou [extensão da máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="8ba55-120">Cenário</span><span class="sxs-lookup"><span data-stu-id="8ba55-120">Scenario</span></span>

<span data-ttu-id="8ba55-121">Neste exemplo, a VM está a enviar mais segmentos TCP que o habitual e pretender toobe alertado.</span><span class="sxs-lookup"><span data-stu-id="8ba55-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="8ba55-122">Segmentos TCP são utilizados como um exemplo aqui, mas pode utilizar qualquer condição de alerta.</span><span class="sxs-lookup"><span data-stu-id="8ba55-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="8ba55-123">Quando for alertado, quer tooreceive dados ao nível do pacote toounderstand por que motivo aumentou a comunicação.</span><span class="sxs-lookup"><span data-stu-id="8ba55-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="8ba55-124">Em seguida, pode tomar medidas comunicação de tooregular tooreturn Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8ba55-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="8ba55-125">Este cenário pressupõe que tem uma instância existente do observador de rede e um grupo de recursos com uma máquina virtual válida.</span><span class="sxs-lookup"><span data-stu-id="8ba55-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="8ba55-126">Olá a seguir lista é uma descrição geral do fluxo de trabalho de Olá que decorre:</span><span class="sxs-lookup"><span data-stu-id="8ba55-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="8ba55-127">Um alerta é acionado na VM.</span><span class="sxs-lookup"><span data-stu-id="8ba55-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="8ba55-128">alerta de Olá chama a função do Azure através de um webhook.</span><span class="sxs-lookup"><span data-stu-id="8ba55-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="8ba55-129">A função do Azure processa alerta Olá e inicia uma sessão de captura de pacotes do observador de rede.</span><span class="sxs-lookup"><span data-stu-id="8ba55-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="8ba55-130">captura de pacotes hello é executado no Olá VM e recolhe tráfego.</span><span class="sxs-lookup"><span data-stu-id="8ba55-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="8ba55-131">Olá pacote captura ficheiro é carregado tooa a conta de armazenamento para revisão e diagnósticos adicionais.</span><span class="sxs-lookup"><span data-stu-id="8ba55-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="8ba55-132">tooautomate este processo, iremos criar e ligar-se um alerta no nosso tootrigger VM quando o incidente Olá ocorre.</span><span class="sxs-lookup"><span data-stu-id="8ba55-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="8ba55-133">Também iremos criar toocall uma função para o observador de rede.</span><span class="sxs-lookup"><span data-stu-id="8ba55-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="8ba55-134">Este cenário Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="8ba55-134">This scenario does hello following:</span></span>

* <span data-ttu-id="8ba55-135">Cria uma função do Azure que inicia uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="8ba55-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="8ba55-136">Cria uma regra de alerta numa máquina virtual e configura Olá de toocall de regra de alerta de Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba55-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="8ba55-137">Criar uma função do Azure</span><span class="sxs-lookup"><span data-stu-id="8ba55-137">Create an Azure function</span></span>

<span data-ttu-id="8ba55-138">primeiro passo de Olá toocreate um alerta de Olá tooprocess função do Azure e criar uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="8ba55-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="8ba55-139">No Olá [portal do Azure](https://portal.azure.com), selecione **novo** > **computação** > **aplicação de função**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Criar uma aplicação de função][1-1]

2. <span data-ttu-id="8ba55-141">No Olá **aplicação de função** painel, introduza Olá os seguintes valores e, em seguida, selecione **OK** toocreate Olá aplicação:</span><span class="sxs-lookup"><span data-stu-id="8ba55-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="8ba55-142">**Definição**</span><span class="sxs-lookup"><span data-stu-id="8ba55-142">**Setting**</span></span> | <span data-ttu-id="8ba55-143">**Valor**</span><span class="sxs-lookup"><span data-stu-id="8ba55-143">**Value**</span></span> | <span data-ttu-id="8ba55-144">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="8ba55-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8ba55-145">**Nome da aplicação** </span><span class="sxs-lookup"><span data-stu-id="8ba55-145">**App name**</span></span>|<span data-ttu-id="8ba55-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="8ba55-146">PacketCaptureExample</span></span>|<span data-ttu-id="8ba55-147">nome da aplicação de função Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="8ba55-148">**Subscrição**</span><span class="sxs-lookup"><span data-stu-id="8ba55-148">**Subscription**</span></span>|<span data-ttu-id="8ba55-149">[Sua subscrição] Olá subscrição para a aplicação de função de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="8ba55-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="8ba55-150">**Grupo de Recursos**</span><span class="sxs-lookup"><span data-stu-id="8ba55-150">**Resource Group**</span></span>|<span data-ttu-id="8ba55-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="8ba55-151">PacketCaptureRG</span></span>|<span data-ttu-id="8ba55-152">Olá recursos grupo toocontain Olá aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="8ba55-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="8ba55-153">**Plano de alojamento**</span><span class="sxs-lookup"><span data-stu-id="8ba55-153">**Hosting Plan**</span></span>|<span data-ttu-id="8ba55-154">Plano de consumo</span><span class="sxs-lookup"><span data-stu-id="8ba55-154">Consumption Plan</span></span>| <span data-ttu-id="8ba55-155">tipo de Olá de planeie as utilizações de aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="8ba55-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="8ba55-156">As opções são consumo ou plano do App Service do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba55-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="8ba55-157">**Localização**</span><span class="sxs-lookup"><span data-stu-id="8ba55-157">**Location**</span></span>|<span data-ttu-id="8ba55-158">EUA Central</span><span class="sxs-lookup"><span data-stu-id="8ba55-158">Central US</span></span>| <span data-ttu-id="8ba55-159">região Olá na aplicação de função que toocreate Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="8ba55-160">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="8ba55-160">**Storage Account**</span></span>|<span data-ttu-id="8ba55-161">{gerado automaticamente}</span><span class="sxs-lookup"><span data-stu-id="8ba55-161">{autogenerated}</span></span>| <span data-ttu-id="8ba55-162">conta de armazenamento de Olá que as funções do Azure necessita de armazenamento para fins gerais.</span><span class="sxs-lookup"><span data-stu-id="8ba55-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="8ba55-163">No Olá **PacketCaptureExample função aplicações** painel, selecione **funções** > **função personalizada**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="8ba55-164">Selecione **HttpTrigger-Powershell**e, em seguida, introduza Olá restantes informações.</span><span class="sxs-lookup"><span data-stu-id="8ba55-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="8ba55-165">Por fim, toocreate Olá função, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="8ba55-166">**Definição**</span><span class="sxs-lookup"><span data-stu-id="8ba55-166">**Setting**</span></span> | <span data-ttu-id="8ba55-167">**Valor**</span><span class="sxs-lookup"><span data-stu-id="8ba55-167">**Value**</span></span> | <span data-ttu-id="8ba55-168">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="8ba55-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8ba55-169">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="8ba55-169">**Scenario**</span></span>|<span data-ttu-id="8ba55-170">Experimental</span><span class="sxs-lookup"><span data-stu-id="8ba55-170">Experimental</span></span>|<span data-ttu-id="8ba55-171">Tipo de cenário</span><span class="sxs-lookup"><span data-stu-id="8ba55-171">Type of scenario</span></span>|
    |<span data-ttu-id="8ba55-172">**Dar um nome à função**</span><span class="sxs-lookup"><span data-stu-id="8ba55-172">**Name your function**</span></span>|<span data-ttu-id="8ba55-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="8ba55-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="8ba55-174">Nome da função de Olá</span><span class="sxs-lookup"><span data-stu-id="8ba55-174">Name of hello function</span></span>|
    |<span data-ttu-id="8ba55-175">**Nível de autorização**</span><span class="sxs-lookup"><span data-stu-id="8ba55-175">**Authorization level**</span></span>|<span data-ttu-id="8ba55-176">Função</span><span class="sxs-lookup"><span data-stu-id="8ba55-176">Function</span></span>|<span data-ttu-id="8ba55-177">Nível de autorização para a função de Olá</span><span class="sxs-lookup"><span data-stu-id="8ba55-177">Authorization level for hello function</span></span>|

![Exemplo de funções][functions1]

> [!NOTE]
> <span data-ttu-id="8ba55-179">modelo de PowerShell Olá é experimental e não tem suporte completo.</span><span class="sxs-lookup"><span data-stu-id="8ba55-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="8ba55-180">As personalizações são necessárias para este exemplo e são explicadas em Olá os seguintes passos.</span><span class="sxs-lookup"><span data-stu-id="8ba55-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="8ba55-181">Adicionar módulos</span><span class="sxs-lookup"><span data-stu-id="8ba55-181">Add modules</span></span>

<span data-ttu-id="8ba55-182">toouse cmdlets do PowerShell do observador de rede, carregue Olá mais recente do PowerShell módulo toohello aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="8ba55-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="8ba55-183">No seu computador local com módulos Olá mais recentes do Azure PowerShell instalada, execute Olá seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8ba55-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="8ba55-184">Este oferece de exemplo Olá caminho local do seu módulos do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba55-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="8ba55-185">Estas pastas são utilizadas num passo posterior.</span><span class="sxs-lookup"><span data-stu-id="8ba55-185">These folders are used in a later step.</span></span> <span data-ttu-id="8ba55-186">módulos de Olá que são utilizados neste cenário são:</span><span class="sxs-lookup"><span data-stu-id="8ba55-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="8ba55-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8ba55-187">AzureRM.Network</span></span>

    * <span data-ttu-id="8ba55-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8ba55-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="8ba55-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8ba55-189">AzureRM.Resources</span></span>

    ![Pastas de PowerShell][functions5]

1. <span data-ttu-id="8ba55-191">Selecione **as definições de aplicação de função** > **aceda tooApp serviço Editor**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![Definições de aplicação de função][functions2]

1. <span data-ttu-id="8ba55-193">Contexto Olá **AlertPacketCapturePowershell** pasta e, em seguida, crie uma pasta denominada **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="8ba55-194">Crie uma subpasta para cada módulo que precisa.</span><span class="sxs-lookup"><span data-stu-id="8ba55-194">Create a subfolder for each module that you need.</span></span>

    ![Pasta e as subpastas][functions3]

    * <span data-ttu-id="8ba55-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8ba55-196">AzureRM.Network</span></span>

    * <span data-ttu-id="8ba55-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8ba55-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="8ba55-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8ba55-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="8ba55-199">Contexto Olá **AzureRM.Network** subpasta e, em seguida, selecione **carregar ficheiros**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="8ba55-200">Aceda tooyour Azure módulos.</span><span class="sxs-lookup"><span data-stu-id="8ba55-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="8ba55-201">Olá local **AzureRM.Network** pasta, selecione todos os ficheiros de Olá na pasta Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="8ba55-202">Em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="8ba55-203">Repita estes passos para **AzureRM.Profile** e **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Carregar ficheiros][functions6]

1. <span data-ttu-id="8ba55-205">Depois de terminar, cada pasta deve ter ficheiros de módulo do PowerShell Olá do seu computador local.</span><span class="sxs-lookup"><span data-stu-id="8ba55-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Ficheiros de PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="8ba55-207">Autenticação</span><span class="sxs-lookup"><span data-stu-id="8ba55-207">Authentication</span></span>

<span data-ttu-id="8ba55-208">os cmdlets do PowerShell do toouse Olá, tem de autenticar.</span><span class="sxs-lookup"><span data-stu-id="8ba55-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="8ba55-209">Configurar a autenticação na aplicação de função Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="8ba55-210">autenticação tooconfigure, tem de configurar as variáveis de ambiente e carregar uma aplicação de função de toohello do ficheiro de chave encriptada.</span><span class="sxs-lookup"><span data-stu-id="8ba55-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="8ba55-211">Este cenário fornece um exemplo de como autenticação de tooimplement com as funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba55-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="8ba55-212">Existem outra formas toodo isto.</span><span class="sxs-lookup"><span data-stu-id="8ba55-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="8ba55-213">Credenciais encriptado</span><span class="sxs-lookup"><span data-stu-id="8ba55-213">Encrypted credentials</span></span>

<span data-ttu-id="8ba55-214">Olá seguinte script do PowerShell cria um ficheiro de chave denominado **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="8ba55-215">Também fornece uma versão encriptada da palavra-passe de Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="8ba55-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="8ba55-216">Esta palavra-passe é Olá mesma palavra-passe que está definido para a aplicação do Azure Active Directory Olá que é utilizada para autenticação.</span><span class="sxs-lookup"><span data-stu-id="8ba55-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="8ba55-217">No Editor de serviço de aplicações da aplicação de função Olá Olá, crie uma pasta denominada **chaves** em **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="8ba55-218">Em seguida, carregue Olá **PassEncryptKey.key** ficheiros que criou no exemplo de PowerShell Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="8ba55-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Chave de funções][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="8ba55-220">Obter os valores de variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="8ba55-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="8ba55-221">requisito final Olá é tooset segurança Olá as variáveis de ambiente são valores de Olá tooaccess necessário para autenticação.</span><span class="sxs-lookup"><span data-stu-id="8ba55-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="8ba55-222">Olá lista seguinte mostra as variáveis de ambiente de Olá que são criadas:</span><span class="sxs-lookup"><span data-stu-id="8ba55-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="8ba55-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8ba55-223">AzureClientID</span></span>

* <span data-ttu-id="8ba55-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8ba55-224">AzureTenant</span></span>

* <span data-ttu-id="8ba55-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8ba55-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="8ba55-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8ba55-226">AzureClientID</span></span>

<span data-ttu-id="8ba55-227">ID de cliente Olá é Olá ID da aplicação de uma aplicação no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ba55-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="8ba55-228">Se ainda não tiver uma aplicação toouse, execute uma aplicação Olá toocreate de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ba55-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="8ba55-229">palavra-passe de Olá que utilizar para criar aplicação Olá deve ser Olá mesma palavra-passe que criou anteriormente ao guardar o ficheiro de chave Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="8ba55-230">No portal do Azure Olá, selecione **subscrições**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="8ba55-231">Selecione Olá toouse de subscrição e, em seguida, selecione **(IAM) do controlo de acesso**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![Funções IAM][functions9]

1. <span data-ttu-id="8ba55-233">Escolha Olá toouse de conta e, em seguida, selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="8ba55-234">Copiar Olá ID da aplicação.</span><span class="sxs-lookup"><span data-stu-id="8ba55-234">Copy hello Application ID.</span></span>

    ![ID da aplicação de funções][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="8ba55-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8ba55-236">AzureTenant</span></span>

<span data-ttu-id="8ba55-237">Obter ID do inquilino Olá executando Olá PowerShell de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ba55-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="8ba55-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8ba55-238">AzureCredPassword</span></span>

<span data-ttu-id="8ba55-239">Olá o valor da variável de ambiente de AzureCredPassword Olá é valor Olá que obtém a execução Olá PowerShell de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="8ba55-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="8ba55-240">Neste exemplo é Olá, mesmo que é apresentado na Olá anterior **encriptação das credenciais** secção.</span><span class="sxs-lookup"><span data-stu-id="8ba55-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="8ba55-241">Olá valor que precisa é a saída de Olá da Olá `$Encryptedpassword` variável.</span><span class="sxs-lookup"><span data-stu-id="8ba55-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="8ba55-242">Este é Olá serviço principal palavra-passe que encriptada utilizando o script do PowerShell Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="8ba55-243">Variáveis de ambiente de Olá de arquivo</span><span class="sxs-lookup"><span data-stu-id="8ba55-243">Store hello environment variables</span></span>

1. <span data-ttu-id="8ba55-244">Aceda a aplicação de função toohello.</span><span class="sxs-lookup"><span data-stu-id="8ba55-244">Go toohello function app.</span></span> <span data-ttu-id="8ba55-245">Em seguida, selecione **as definições de aplicação de função** > **configurar definições da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![Configurar as definições da aplicação][functions11]

1. <span data-ttu-id="8ba55-247">Adicionar variáveis de ambiente de Olá e respetivas definições de aplicação de toohello valores e, em seguida, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![Definições de aplicação][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="8ba55-249">Adicionar a função de toohello do PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ba55-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="8ba55-250">Está agora a tempo toomake chama para o observador de rede a partir de dentro Olá função do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ba55-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="8ba55-251">Dependendo dos requisitos de Olá, implementação de Olá desta função pode variar.</span><span class="sxs-lookup"><span data-stu-id="8ba55-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="8ba55-252">No entanto, o fluxo geral de Olá de código Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8ba55-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="8ba55-253">Parâmetros de entrada do processo.</span><span class="sxs-lookup"><span data-stu-id="8ba55-253">Process input parameters.</span></span>
2. <span data-ttu-id="8ba55-254">Pacote existente da consulta captura tooverify limites e resolva conflitos de nomes.</span><span class="sxs-lookup"><span data-stu-id="8ba55-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="8ba55-255">Crie uma captura de pacotes com os parâmetros adequados.</span><span class="sxs-lookup"><span data-stu-id="8ba55-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="8ba55-256">Captura de pacotes de consulta periodicamente até que esteja concluída.</span><span class="sxs-lookup"><span data-stu-id="8ba55-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="8ba55-257">Notificar o utilizador Olá que a sessão de captura de pacotes de Olá está concluída.</span><span class="sxs-lookup"><span data-stu-id="8ba55-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="8ba55-258">Olá seguinte exemplo é o código do PowerShell que pode ser utilizado na função de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="8ba55-259">Existem valores que necessitam de toobe substituído para **subscriptionId**, **resourceGroupName**, e **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="8ba55-260">Obter o URL de função Olá</span><span class="sxs-lookup"><span data-stu-id="8ba55-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="8ba55-261">Depois de criar a função, configure o seu URL de Olá toocall alerta associado à função de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="8ba55-262">tooget este valor, o URL da função Olá cópia da sua aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="8ba55-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Localizar o URL da função Olá][functions13]

2. <span data-ttu-id="8ba55-264">Copie o URL de função de Olá para a sua aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="8ba55-264">Copy hello function URL for your function app.</span></span>

    ![Copiar o URL da função Olá][2]

<span data-ttu-id="8ba55-266">Se necessitar de propriedades personalizadas no payload Olá de pedido POST de webhook Olá, consulte demasiado[configurar um webhook num alerta métrico Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="8ba55-267">Configurar um alerta numa VM</span><span class="sxs-lookup"><span data-stu-id="8ba55-267">Configure an alert on a VM</span></span>

<span data-ttu-id="8ba55-268">Os alertas podem ser configuradas toonotify indivíduos quando uma métrica específica atravesse um limiar que é atribuído tooit.</span><span class="sxs-lookup"><span data-stu-id="8ba55-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="8ba55-269">Neste exemplo, alerta Olá é no Olá segmentos TCP que são enviados, mas pode ser acionada alerta Olá para muitas outras métricas.</span><span class="sxs-lookup"><span data-stu-id="8ba55-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="8ba55-270">Neste exemplo, um alerta é configurado toocall uma função do webhook toocall Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="8ba55-271">Criar regra de alerta de Olá</span><span class="sxs-lookup"><span data-stu-id="8ba55-271">Create hello alert rule</span></span>

<span data-ttu-id="8ba55-272">Aceda a máquina virtual existente e tooan e, em seguida, adicione uma regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="8ba55-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="8ba55-273">Documentação mais detalhada sobre como configurar alertas pode ser encontrada em [criar alertas no Monitor do Azure para serviços do Azure - portal do Azure](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="8ba55-274">Introduza Olá os seguintes valores no Olá **regra de alerta** painel e, em seguida, selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="8ba55-275">**Definição**</span><span class="sxs-lookup"><span data-stu-id="8ba55-275">**Setting**</span></span> | <span data-ttu-id="8ba55-276">**Valor**</span><span class="sxs-lookup"><span data-stu-id="8ba55-276">**Value**</span></span> | <span data-ttu-id="8ba55-277">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="8ba55-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="8ba55-278">**Nome**</span><span class="sxs-lookup"><span data-stu-id="8ba55-278">**Name**</span></span>|<span data-ttu-id="8ba55-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="8ba55-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="8ba55-280">Nome da regra de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="8ba55-281">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8ba55-281">**Description**</span></span>|<span data-ttu-id="8ba55-282">Segmentos TCP enviados limiar excedida</span><span class="sxs-lookup"><span data-stu-id="8ba55-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="8ba55-283">Descrição de Olá de regra de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="8ba55-284">**Métricas**</span><span class="sxs-lookup"><span data-stu-id="8ba55-284">**Metric**</span></span>|<span data-ttu-id="8ba55-285">Segmentos TCP enviados</span><span class="sxs-lookup"><span data-stu-id="8ba55-285">TCP segments sent</span></span>| <span data-ttu-id="8ba55-286">alerta do Olá toouse métrica tootrigger Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="8ba55-287">**Condição**</span><span class="sxs-lookup"><span data-stu-id="8ba55-287">**Condition**</span></span>|<span data-ttu-id="8ba55-288">Mais do que</span><span class="sxs-lookup"><span data-stu-id="8ba55-288">Greater than</span></span>| <span data-ttu-id="8ba55-289">Olá condição toouse ao avaliar a métrica de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="8ba55-290">**Limiar**</span><span class="sxs-lookup"><span data-stu-id="8ba55-290">**Threshold**</span></span>|<span data-ttu-id="8ba55-291">100</span><span class="sxs-lookup"><span data-stu-id="8ba55-291">100</span></span>| <span data-ttu-id="8ba55-292">valor de Olá da métrica de Olá que aciona alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="8ba55-293">Este valor deve ser definido tooa um valor válido para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8ba55-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="8ba55-294">**Período**</span><span class="sxs-lookup"><span data-stu-id="8ba55-294">**Period**</span></span>|<span data-ttu-id="8ba55-295">Ao longo de Olá últimos cinco minutos</span><span class="sxs-lookup"><span data-stu-id="8ba55-295">Over hello last five minutes</span></span>| <span data-ttu-id="8ba55-296">Determina o período de Olá no qual toolook para o limiar de Olá de métrica de Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="8ba55-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="8ba55-297">**Webhook**</span></span>|<span data-ttu-id="8ba55-298">[webhook o URL da aplicação de função]</span><span class="sxs-lookup"><span data-stu-id="8ba55-298">[webhook URL from function app]</span></span>| <span data-ttu-id="8ba55-299">URL do webhook Olá da aplicação de função Olá que foi criada nos passos anteriores Olá.</span><span class="sxs-lookup"><span data-stu-id="8ba55-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="8ba55-300">métrica de segmentos Olá TCP não está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="8ba55-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="8ba55-301">Saiba mais sobre como tooenable métricas adicionais, visitando [ativar a monitorização e diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="8ba55-302">Reveja os resultados de Olá</span><span class="sxs-lookup"><span data-stu-id="8ba55-302">Review hello results</span></span>

<span data-ttu-id="8ba55-303">Depois de critérios de Olá para acionadores alerta Olá, é criada uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="8ba55-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="8ba55-304">Aceda tooNetwork observador e, em seguida, selecione **captura de pacotes**.</span><span class="sxs-lookup"><span data-stu-id="8ba55-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="8ba55-305">Nesta página, pode selecionar Olá pacote captura ficheiro ligação toodownload Olá captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="8ba55-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Captura de pacotes de vista][functions14]

<span data-ttu-id="8ba55-307">Se o ficheiro de captura Olá estiver armazenado localmente, pode obtê-lo pelo início de sessão na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="8ba55-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="8ba55-308">Para obter instruções sobre a transferência de ficheiros das contas do storage do Azure, consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8ba55-309">Outra ferramenta, pode utilizar é [Explorador de armazenamento](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8ba55-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="8ba55-310">Após a captura tenha sido transferida, pode vê-la utilizando qualquer ferramenta que pode ler um **.cap** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="8ba55-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="8ba55-311">Seguem-se ligações tootwo destas ferramentas:</span><span class="sxs-lookup"><span data-stu-id="8ba55-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="8ba55-312">Analisador de mensagens da Microsoft</span><span class="sxs-lookup"><span data-stu-id="8ba55-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="8ba55-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="8ba55-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="8ba55-314">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8ba55-314">Next steps</span></span>

<span data-ttu-id="8ba55-315">Saiba como tooview as capturas de pacotes, visitando [análise de captura do pacote com o Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="8ba55-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
