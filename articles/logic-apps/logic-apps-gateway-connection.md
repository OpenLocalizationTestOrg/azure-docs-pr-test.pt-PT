---
title: aaaAccess origens de dados no local para Azure Logic Apps | Microsoft Docs
description: "Configurar o gateway de dados no local Olá para que possa aceder a origens de dados no local a partir das logic apps"
keywords: "aceder a dados no local, a transferência de dados, a encriptação e origens de dados"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="c6cb5-104">Origens de dados de acesso no local a partir das logic apps com o gateway de dados do Olá no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="c6cb5-105">tooaccess origens de dados no local das logic apps, configurar um gateway de dados no local que podem utilizar aplicações lógicas com conectores suportados.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="c6cb5-106">gateway de Olá atua como uma ponte que fornece a transferência de dados rápida e encriptação entre origens de dados no local e as logic apps.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="c6cb5-107">gateway de Olá transmite dados a partir de origens do local em canais encriptados através de Olá Service Bus do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="c6cb5-108">Todo o tráfego origina como tráfego de saída seguro de agente de gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="c6cb5-109">Saiba mais sobre [como funciona o gateway de dados de Olá](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="c6cb5-110">gateway de Olá suporta origens de dados de toothese ligações no local:</span><span class="sxs-lookup"><span data-stu-id="c6cb5-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="c6cb5-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="c6cb5-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="c6cb5-112">DB2</span><span class="sxs-lookup"><span data-stu-id="c6cb5-112">DB2</span></span>  
*   <span data-ttu-id="c6cb5-113">Sistema de Ficheiros</span><span class="sxs-lookup"><span data-stu-id="c6cb5-113">File System</span></span>
*   <span data-ttu-id="c6cb5-114">Informix</span><span class="sxs-lookup"><span data-stu-id="c6cb5-114">Informix</span></span>
*   <span data-ttu-id="c6cb5-115">MQ</span><span class="sxs-lookup"><span data-stu-id="c6cb5-115">MQ</span></span>
*   <span data-ttu-id="c6cb5-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="c6cb5-116">MySQL</span></span>
*   <span data-ttu-id="c6cb5-117">Base de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="c6cb5-117">Oracle Database</span></span>
*   <span data-ttu-id="c6cb5-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c6cb5-118">PostgreSQL</span></span>
*   <span data-ttu-id="c6cb5-119">Servidor de aplicações SAP</span><span class="sxs-lookup"><span data-stu-id="c6cb5-119">SAP Application Server</span></span> 
*   <span data-ttu-id="c6cb5-120">Servidor de mensagens SAP</span><span class="sxs-lookup"><span data-stu-id="c6cb5-120">SAP Message Server</span></span>
*   <span data-ttu-id="c6cb5-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="c6cb5-121">SharePoint</span></span>
*   <span data-ttu-id="c6cb5-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="c6cb5-122">SQL Server</span></span>
*   <span data-ttu-id="c6cb5-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="c6cb5-123">Teradata</span></span>

<span data-ttu-id="c6cb5-124">Estes passos mostram como tooset segurança Olá no local toowork de gateway de dados com as logic apps.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="c6cb5-125">Para obter mais informações sobre conectores suportados, consulte [conectores para o Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="c6cb5-126">Para obter informações sobre como toouse Olá gateway com outros serviços, consulte estes artigos:</span><span class="sxs-lookup"><span data-stu-id="c6cb5-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="c6cb5-127">Gateway de dados do Microsoft Power BI no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="c6cb5-128">Gateway de dados no local do Analysis Services do Azure</span><span class="sxs-lookup"><span data-stu-id="c6cb5-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="c6cb5-129">Gateway de dados do Microsoft Flow no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="c6cb5-130">Gateway de dados do Microsoft PowerApps no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="c6cb5-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="c6cb5-131">Requirements</span></span>

* <span data-ttu-id="c6cb5-132">Tem de ter já [instalado o gateway de dados de Olá num computador local](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="c6cb5-133">Quando inicia sessão no portal do Azure de toohello, tiver toouse Olá a mesma conta escolar ou profissional que foi utilizada demasiado[instalar o gateway de dados no local de Olá](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="c6cb5-134">A conta de início de sessão também tem de ter uma subscrição do Azure toouse quando cria um recurso de gateway no Olá portal do Azure para a sua instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="c6cb5-135">A instalação do gateway já não pode ser reclamada por um recurso de gateway do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="c6cb5-136">Pode associar o seu gateway instalação tooonly um gateway do Azure recurso.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="c6cb5-137">Afirmação acontece quando criar o recurso do gateway de Olá, para que a instalação de Olá não está disponível para outros recursos.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="c6cb5-138">Configurar a ligação de gateway de dados de Olá</span><span class="sxs-lookup"><span data-stu-id="c6cb5-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="c6cb5-139">1. Instalar o gateway de dados do Olá no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="c6cb5-140">Se ainda não o fez, siga Olá [gateway de dados no local do passos tooinstall Olá](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="c6cb5-141">Antes de continuar com Olá outros passos, certifique-se de que instalou o gateway de dados de Olá num computador local.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="c6cb5-142">2. Criar um recurso do Azure para o gateway de dados do Olá no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="c6cb5-143">Depois de instalar o gateway de Olá num computador local, tem de criar o gateway de dados como um recurso no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="c6cb5-144">Este passo também associa o seu recurso de gateway com a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="c6cb5-145">Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="c6cb5-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="c6cb5-146">Certifique-se toouse Olá mesmo trabalho do Azure ou o endereço de e-mail profissional utilizado o gateway de Olá tooinstall.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="c6cb5-147">No menu à esquerda de Olá no Azure, escolha **novo** > **integração empresarial com** > **gateway de dados no local** conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="c6cb5-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Localizar "gateway de dados no local"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="c6cb5-149">No Olá **criar gateway de ligação** painel, forneça estes detalhes toocreate o recurso do gateway de dados:</span><span class="sxs-lookup"><span data-stu-id="c6cb5-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="c6cb5-150">**Nome**: introduza um nome para o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="c6cb5-151">**Subscrição**: selecione Olá tooassociate de subscrição do Azure com o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="c6cb5-152">Esta subscrição deve ser Olá mesma subscrição que a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="c6cb5-153">subscrição de predefinição Olá baseia Olá conta do Azure que utilizou toosign no.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="c6cb5-154">**Grupo de recursos**: criar um grupo de recursos ou selecione um grupo de recursos existente para implementar o recurso do gateway.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="c6cb5-155">Grupos de recursos ajudam a gerir recursos do Azure relacionados como uma coleção.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="c6cb5-156">**Localização**: Azure restringe esta localização toohello mesma região que foi selecionado para o serviço de nuvem do gateway Olá durante [instalação do gateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="c6cb5-157">Certifique-se de que a localização do recurso de gateway de Olá corresponde à localização do serviço de nuvem do Olá gateway.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="c6cb5-158">Caso contrário, a instalação do gateway pode não aparecer na lista de gateways Olá instalado para lhe tooselect passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="c6cb5-159">Pode utilizar regiões diferentes para o seu recurso de gateway e para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="c6cb5-160">**Nome de instalação**: se a instalação do gateway não estiver selecionada, selecione o gateway de Olá que instalou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="c6cb5-161">Escolha tooadd Olá gateway recursos tooyour dashboard do Azure, **Pin toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="c6cb5-162">Quando tiver terminado, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="c6cb5-163">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c6cb5-163">For example:</span></span>

    ![Forneça detalhes toocreate o gateway de dados no local](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="c6cb5-165">toofind ou ver o seu gateway de dados em qualquer altura, menu Olá principal do Azure à esquerda, aceda demasiado **mais serviços** > **integração empresarial com** > **dados no local Gateways**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Aceda demasiado "Mais serviços", "Integração empresarial com o", "Gateways de dados no local"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="c6cb5-167">3. Ligar o gateway de dados no local de toohello de aplicação de lógica</span><span class="sxs-lookup"><span data-stu-id="c6cb5-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="c6cb5-168">Agora que já criou o seu recurso de gateway de dados e associado à sua subscrição do Azure com esse recurso, crie uma ligação entre o gateway de dados de aplicação e Olá lógica.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="c6cb5-169">A localização de ligação do gateway tem de existir na Olá mesma região que a sua aplicação lógica, mas pode utilizar um gateway de dados existe numa região diferente.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="c6cb5-170">No portal do Azure Olá, criar ou abrir a sua aplicação lógica no Designer de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="c6cb5-171">Adicione um conector que suporte ligações no local, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="c6cb5-172">A seguir a ordem de Olá apresentada, selecione **ligar através do gateway de dados no local**, forneça um nome de ligação exclusiva Olá informações necessárias e selecione o recurso de gateway de dados de Olá que pretende que o toouse.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="c6cb5-173">Quando tiver terminado, escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="c6cb5-174">Um nome de ligação exclusiva ajuda-o a identificar facilmente essa ligação mais tarde, especialmente quando cria várias ligações.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="c6cb5-175">Se aplicável, também inclua o domínio de qualificado Olá para o seu nome de utilizador.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Criar ligação entre o gateway de dados e aplicação lógica](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="c6cb5-177">Parabéns, a ligação de gateway está agora preparada para sua toouse de aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="c6cb5-178">Editar as definições de ligação de gateway</span><span class="sxs-lookup"><span data-stu-id="c6cb5-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="c6cb5-179">Depois de criar uma ligação de gateway para a sua aplicação lógica, pode querer toolater Olá Update para essa ligação específica.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="c6cb5-180">ligação de gateway do toofind Olá:</span><span class="sxs-lookup"><span data-stu-id="c6cb5-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="c6cb5-181">No painel de aplicação de lógica de Olá, sob **ferramentas de desenvolvimento**, selecione **API ligações**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="c6cb5-182">Olá **API ligações** painel mostra todas as ligações de API associadas com a sua aplicação lógica, incluindo ligações de gateway.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Aceda a aplicação de lógica de tooyour, selecione "API ligações"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="c6cb5-184">Ou, no menu Olá principal do Azure à esquerda, vá demasiado **mais serviços** > **Web & Mobile Services** > **API ligações** para todas as ligações de API incluindo ligações do gateway, que estão associadas a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="c6cb5-185">Ou, no Olá principal do Azure menu à esquerda, aceda demasiado**todos os recursos** para todas as ligações de API, incluindo ligações de gateway, que estão associadas a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="c6cb5-186">Selecione a ligação de gateway Olá que pretender tooview ou a editar e escolha **ligação editar API**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="c6cb5-187">Se as atualizações não entre em vigor, tente [parando e reiniciando o serviço de gateway do Windows hello](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="c6cb5-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="c6cb5-188">Comutador ou eliminar o recurso de gateway de dados no local</span><span class="sxs-lookup"><span data-stu-id="c6cb5-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="c6cb5-189">toocreate um recurso de gateway diferentes, o gateway de associar a um recurso diferente ou remova o recurso do gateway Olá, pode eliminar o recurso do gateway Olá sem afetar a instalação do gateway Olá.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="c6cb5-190">Menu Olá principal do Azure à esquerda, aceda demasiado**todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="c6cb5-191">Localize e selecione o recurso de gateway de dados.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="c6cb5-192">Escolha **Gateway de dados no local**e na barra de ferramentas de recurso Olá, escolha **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c6cb5-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="c6cb5-193">Perguntas mais frequentes</span><span class="sxs-lookup"><span data-stu-id="c6cb5-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="c6cb5-194">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c6cb5-194">Next steps</span></span>

* [<span data-ttu-id="c6cb5-195">Proteger as suas aplicações lógicas</span><span class="sxs-lookup"><span data-stu-id="c6cb5-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="c6cb5-196">Exemplos e cenários para aplicações lógicas comuns</span><span class="sxs-lookup"><span data-stu-id="c6cb5-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
