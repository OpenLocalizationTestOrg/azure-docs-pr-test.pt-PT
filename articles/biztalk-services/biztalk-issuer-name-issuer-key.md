---
title: aaaIssuer nome e a chave do emissor nos BizTalk Services | Microsoft Docs
description: Saiba como o nome do emissor tooretrieve e a chave do emissor para o Service Bus ou controlo de acesso (ACS) nos BizTalk Services. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="1eabc-104">BizTalk Services: Nome e Chave do Emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="1eabc-105">BizTalk Services do Azure utiliza Olá nome do emissor de barramento de serviço e chave do emissor e Olá nome do emissor de controlo de acesso e a chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="1eabc-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="1eabc-106">Especificamente:</span><span class="sxs-lookup"><span data-stu-id="1eabc-106">Specifically:</span></span>

| <span data-ttu-id="1eabc-107">Tarefa</span><span class="sxs-lookup"><span data-stu-id="1eabc-107">Task</span></span> | <span data-ttu-id="1eabc-108">O nome do emissor e chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="1eabc-109">Implementar a aplicação a partir do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1eabc-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="1eabc-110">Nome do emissor de controlo de acesso e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="1eabc-111">Configurar Olá Portal de serviços do BizTalk do Azure</span><span class="sxs-lookup"><span data-stu-id="1eabc-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="1eabc-112">Nome do emissor de controlo de acesso e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="1eabc-113">Criar o LOB reencaminhamentos com Olá adaptador dos BizTalk Services no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1eabc-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="1eabc-114">Nome do emissor de barramento de serviço e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="1eabc-115">Este tópico lista Olá passos tooretrieve Olá nome do emissor e chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="1eabc-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="1eabc-116">Nome do emissor de controlo de acesso e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="1eabc-117">Olá nome do emissor de controlo de acesso e a chave do emissor são utilizados pelo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="1eabc-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="1eabc-118">A aplicação do BizTalk Service do Azure criada no Visual Studio: toosuccessfully implementar a aplicação do serviço de BizTalk no Visual Studio tooAzure, introduza Olá nome do emissor de controlo de acesso e a chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="1eabc-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="1eabc-119">Olá Portal do Azure BizTalk Services: Quando cria um BizTalk Service e abrir Olá BizTalk Services Portal, o nome de emissor de controlo de acesso e a chave do emissor são registados automaticamente para as implementações com Olá os mesmos valores de controlo de acesso.</span><span class="sxs-lookup"><span data-stu-id="1eabc-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="1eabc-120">Obter Olá nome do emissor de controlo de acesso e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="1eabc-121">toouse ACS para autenticação e get Olá valores de nome de emissor e chave do emissor, hello gerais passos incluem:</span><span class="sxs-lookup"><span data-stu-id="1eabc-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="1eabc-122">Instalar Olá [cmdlets Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="1eabc-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="1eabc-123">Adicione a sua conta do Azure:`Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="1eabc-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="1eabc-124">Devolva o nome da sua subscrição:`get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="1eabc-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="1eabc-125">Selecione a sua subscrição:`select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="1eabc-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="1eabc-126">Crie um novo espaço de nomes:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="1eabc-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="1eabc-127">Exemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="1eabc-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="1eabc-128">Quando o espaço de nomes Olá novo ACS for criado (que pode demorar vários minutos), valores de nome de emissor e chave do emissor Olá estão listados na cadeia de ligação de Olá:</span><span class="sxs-lookup"><span data-stu-id="1eabc-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="1eabc-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="1eabc-129">toosummarize:</span></span>  
<span data-ttu-id="1eabc-130">Nome do emissor = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="1eabc-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="1eabc-131">Chave do emissor = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="1eabc-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="1eabc-132">Mais informações sobre as Olá [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1eabc-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="1eabc-133">Nome do emissor de barramento de serviço e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="1eabc-134">Nome do emissor de barramento de serviço e a chave do emissor são utilizados pelo BizTalk Services do adaptador.</span><span class="sxs-lookup"><span data-stu-id="1eabc-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="1eabc-135">No projeto dos BizTalk Services no Visual Studio, utilize o sistema de linha de negócio (LOB) do Olá BizTalk Services do adaptador tooconnect tooan no local.</span><span class="sxs-lookup"><span data-stu-id="1eabc-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="1eabc-136">tooconnect, criar Olá LOB de reencaminhamento e introduza os detalhes de sistema LOB.</span><span class="sxs-lookup"><span data-stu-id="1eabc-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="1eabc-137">Ao fazê-lo, é também introduzir Olá nome do emissor de barramento de serviço e a chave do emissor.</span><span class="sxs-lookup"><span data-stu-id="1eabc-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="1eabc-138">Olá tooretrieve nome do emissor de barramento de serviço e a chave do emissor</span><span class="sxs-lookup"><span data-stu-id="1eabc-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="1eabc-139">Inicie sessão no toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="1eabc-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="1eabc-140">No painel de navegação esquerdo Olá, selecione **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="1eabc-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="1eabc-141">Selecione o seu espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="1eabc-141">Select your namespace.</span></span> <span data-ttu-id="1eabc-142">Na barra de tarefas Olá, selecione **informações de ligação**.</span><span class="sxs-lookup"><span data-stu-id="1eabc-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="1eabc-143">Esta ação apresenta Olá **predefinido emissor** (nome do emissor) e **predefinido chave** (Issuer Key).</span><span class="sxs-lookup"><span data-stu-id="1eabc-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="1eabc-144">Podem ser copiados os respetivos valores.</span><span class="sxs-lookup"><span data-stu-id="1eabc-144">Their values can be copied.</span></span>  

<span data-ttu-id="1eabc-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="1eabc-145">toosummarize:</span></span>  
<span data-ttu-id="1eabc-146">Nome do emissor = emissor predefinido</span><span class="sxs-lookup"><span data-stu-id="1eabc-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="1eabc-147">Chave do emissor = chave predefinida</span><span class="sxs-lookup"><span data-stu-id="1eabc-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="1eabc-148">Seguinte</span><span class="sxs-lookup"><span data-stu-id="1eabc-148">Next</span></span>
<span data-ttu-id="1eabc-149">Tópicos de BizTalk Services do Azure adicionais:</span><span class="sxs-lookup"><span data-stu-id="1eabc-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="1eabc-150">Instalar Olá SDK dos BizTalk Services do Azure</span><span class="sxs-lookup"><span data-stu-id="1eabc-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="1eabc-151">Tutoriais: BizTalk Services do Azure</span><span class="sxs-lookup"><span data-stu-id="1eabc-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="1eabc-152">Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure</span><span class="sxs-lookup"><span data-stu-id="1eabc-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="1eabc-153">BizTalk Services do Azure</span><span class="sxs-lookup"><span data-stu-id="1eabc-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="1eabc-154">Veja Também</span><span class="sxs-lookup"><span data-stu-id="1eabc-154">See Also</span></span>
* [<span data-ttu-id="1eabc-155">Como: tooConfigure do serviço de gestão de ACS utilizar identidades do serviço</span><span class="sxs-lookup"><span data-stu-id="1eabc-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="1eabc-156">Os BizTalk Services: Programador, básicas, Standard e Premium gráfico de edições</span><span class="sxs-lookup"><span data-stu-id="1eabc-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="1eabc-157">BizTalk Services: Portal clássico do Azure através de aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="1eabc-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="1eabc-158">Serviços BizTalk: Gráfico de Estado de Aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="1eabc-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="1eabc-159">Serviços BizTalk: Separadores Dashboard, Monitorizar e Dimensionar</span><span class="sxs-lookup"><span data-stu-id="1eabc-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="1eabc-160">Serviços BizTalk: Cópia de segurança e Restauro</span><span class="sxs-lookup"><span data-stu-id="1eabc-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="1eabc-161">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="1eabc-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

