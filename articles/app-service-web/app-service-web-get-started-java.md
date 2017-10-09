---
title: "aaaCreate sua primeira aplicação de web de Java no Azure"
description: "Saiba como toorun web apps no App Service ao implementar uma aplicação básica de Java."
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a><span data-ttu-id="6a4b8-103">Criar a primeira aplicação Web Java no Azure</span><span class="sxs-lookup"><span data-stu-id="6a4b8-103">Create your first Java web app in Azure</span></span>

<span data-ttu-id="6a4b8-104">Olá [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) funcionalidade do [App Service do Azure](../app-service/app-service-value-prop-what-is.md) fornece uma serviço de alojamento na web altamente dimensionável e aplicação de patches personalizada.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-104">hello [Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) feature of [Azure App Service](../app-service/app-service-value-prop-what-is.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="6a4b8-105">Este guia de introdução mostra como toodeploy um Java web tooApp do app Service utilizando Olá [IDE Eclipse para programadores de Java EE](http://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="6a4b8-105">This quickstart shows how toodeploy a Java web app tooApp Service by using hello [Eclipse IDE for Java EE Developers](http://www.eclipse.org/).</span></span>

!["Olá, Azure!”](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a><span data-ttu-id="6a4b8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a4b8-108">Prerequisites</span></span>

<span data-ttu-id="6a4b8-109">toocomplete este guia de introdução, instale:</span><span class="sxs-lookup"><span data-stu-id="6a4b8-109">toocomplete this quickstart, install:</span></span>

* <span data-ttu-id="6a4b8-110">Olá livre [IDE Eclipse para programadores de Java EE](http://www.eclipse.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6a4b8-110">hello free [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/).</span></span> <span data-ttu-id="6a4b8-111">Este guia de introdução utiliza o Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-111">This quickstart uses Eclipse Neon.</span></span>
* <span data-ttu-id="6a4b8-112">Olá [Toolkit do Azure para o Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span><span class="sxs-lookup"><span data-stu-id="6a4b8-112">hello [Azure Toolkit for Eclipse](/azure/azure-toolkit-for-eclipse-installation).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a><span data-ttu-id="6a4b8-113">Criar um projeto Web dinâmico no Eclipse</span><span class="sxs-lookup"><span data-stu-id="6a4b8-113">Create a dynamic web project in Eclipse</span></span>

<span data-ttu-id="6a4b8-114">No Eclipse, selecione **Ficheiro** > **Novo** > **Projeto Web Dinâmico**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-114">In Eclipse, select **File** > **New** > **Dynamic Web Project**.</span></span>

<span data-ttu-id="6a4b8-115">No Olá **novo Dynamic Web Project** caixa de diálogo, o projeto de Olá nome **MyFirstJavaOnAzureWebApp**e selecione **concluir**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-115">In hello **New Dynamic Web Project** dialog box, name hello project **MyFirstJavaOnAzureWebApp**, and select **Finish**.</span></span>
   
![Caixa de diálogo Novo Projeto Web Dinâmico](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a><span data-ttu-id="6a4b8-117">Adicionar uma página JSP</span><span class="sxs-lookup"><span data-stu-id="6a4b8-117">Add a JSP page</span></span>

<span data-ttu-id="6a4b8-118">Se o Explorador de Projeto não for apresentado, restaure-o.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-118">If Project Explorer is not displayed, restore it.</span></span>

![Área de trabalho Java EE para Eclipse](./media/app-service-web-get-started-java/pe.png)

<span data-ttu-id="6a4b8-120">No Explorador de projeto, expanda Olá **MyFirstJavaOnAzureWebApp** projeto.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-120">In Project Explorer, expand hello **MyFirstJavaOnAzureWebApp** project.</span></span>
<span data-ttu-id="6a4b8-121">Clique com botão direito do rato em **WebContent**e, em seguida, selecione **Novo** > **Ficheiro JSP**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-121">Right-click **WebContent**, and then select **New** > **JSP File**.</span></span>

![Menu de um novo ficheiro JSP no Explorador de Projeto](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

<span data-ttu-id="6a4b8-123">No Olá **novo ficheiro JSP** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="6a4b8-123">In hello **New JSP File** dialog box:</span></span>

* <span data-ttu-id="6a4b8-124">Ficheiro de Olá nome **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-124">Name hello file **index.jsp**.</span></span>
* <span data-ttu-id="6a4b8-125">Selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-125">Select **Finish**.</span></span>

  ![Caixa de diálogo Novo Ficheiro JSP](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

<span data-ttu-id="6a4b8-127">No ficheiro de index.jsp Olá, substitua Olá `<body></body>` elemento com Olá markup os seguintes:</span><span class="sxs-lookup"><span data-stu-id="6a4b8-127">In hello index.jsp file, replace hello `<body></body>` element with hello following markup:</span></span>

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

<span data-ttu-id="6a4b8-128">Guarde as alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-128">Save hello changes.</span></span>

## <a name="publish-hello-web-app-tooazure"></a><span data-ttu-id="6a4b8-129">Publicar Olá web app tooAzure</span><span class="sxs-lookup"><span data-stu-id="6a4b8-129">Publish hello web app tooAzure</span></span>

<span data-ttu-id="6a4b8-130">No Explorador de projeto, clique no projeto Olá e, em seguida, selecione **Azure** > **publicar como aplicação Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-130">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

![Menu de contexto Publicar como Aplicação Web do Azure](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

<span data-ttu-id="6a4b8-132">No Olá **Azure sessão** caixa de diálogo, mantenha Olá **interativo** opção e, em seguida, selecione **sessão**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-132">In hello **Azure Sign In** dialog box, keep hello **Interactive** option, and then select **Sign in**.</span></span>

<span data-ttu-id="6a4b8-133">Siga as instruções de início de sessão Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-133">Follow hello sign-in instructions.</span></span>

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="6a4b8-134">Caixa de diálogo Implementar Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="6a4b8-134">Deploy Web App dialog box</span></span>

<span data-ttu-id="6a4b8-135">Depois de ter a sessão tooyour conta do Azure, Olá **implementar Web App** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-135">After you have signed in tooyour Azure account, hello **Deploy Web App** dialog box appears.</span></span>

<span data-ttu-id="6a4b8-136">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-136">Select **Create**.</span></span>

![Caixa de diálogo Implementar Aplicação Web](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a><span data-ttu-id="6a4b8-138">Caixa de diálogo Criar Serviço de Aplicações</span><span class="sxs-lookup"><span data-stu-id="6a4b8-138">Create App Service dialog box</span></span>

<span data-ttu-id="6a4b8-139">Olá **criar App Service** é apresentada a caixa de diálogo com os valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-139">hello **Create App Service** dialog box appears with default values.</span></span> <span data-ttu-id="6a4b8-140">número de Olá **170602185241** mostrado na Olá seguinte imagem é diferente na sua caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-140">hello number **170602185241** shown in hello following image is different in your dialog box.</span></span>

![Caixa de diálogo Criar Serviço de Aplicações](./media/app-service-web-get-started-java/cas1.png)

<span data-ttu-id="6a4b8-142">No Olá **criar App Service** caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="6a4b8-142">In hello **Create App Service** dialog box:</span></span>

* <span data-ttu-id="6a4b8-143">Mantenha o nome de Olá gerado para a aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-143">Keep hello generated name for hello web app.</span></span> <span data-ttu-id="6a4b8-144">Este nome tem de ser exclusivo em todo o Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-144">This name must be unique across Azure.</span></span> <span data-ttu-id="6a4b8-145">nome de Olá faz parte do endereço de URL Olá da aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-145">hello name is part of hello URL address for hello web app.</span></span> <span data-ttu-id="6a4b8-146">Por exemplo: se for o nome da aplicação web Olá **MyJavaWebApp**, Olá URL é *myjavawebapp.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-146">For example: if hello web app name is **MyJavaWebApp**, hello URL is *myjavawebapp.azurewebsites.net*.</span></span>
* <span data-ttu-id="6a4b8-147">Mantenha o contentor de web Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-147">Keep hello default web container.</span></span>
* <span data-ttu-id="6a4b8-148">Selecione uma subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-148">Select an Azure subscription.</span></span>
* <span data-ttu-id="6a4b8-149">No Olá **plano do App service** separador:</span><span class="sxs-lookup"><span data-stu-id="6a4b8-149">On hello **App service plan** tab:</span></span>

  * <span data-ttu-id="6a4b8-150">**Criar um novo**: mantenha Olá, predefinição que é o nome de Olá de Olá plano do App Service.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-150">**Create new**: Keep hello default, which is hello name of hello App Service plan.</span></span>
  * <span data-ttu-id="6a4b8-151">**Localização**: selecione **Europa Ocidental** ou um local perto de si.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-151">**Location**: Select **West Europe** or a location near you.</span></span>
  * <span data-ttu-id="6a4b8-152">**Escalão de preço**: selecione Olá opção gratuita.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-152">**Pricing tier**: Select hello free option.</span></span> <span data-ttu-id="6a4b8-153">Para as funcionalidades, veja [Preços do Serviço de Aplicações](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="6a4b8-153">For features, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

   ![Caixa de diálogo Criar Serviço de Aplicações](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a><span data-ttu-id="6a4b8-155">Separador grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6a4b8-155">Resource group tab</span></span>

<span data-ttu-id="6a4b8-156">Selecione Olá **grupo de recursos** separador. Mantenha o valor de predefinido gerado de Olá Olá grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-156">Select hello **Resource group** tab. Keep hello default generated value for hello resource group.</span></span>

![Separador grupo de recursos](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="6a4b8-158">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-158">Select **Create**.</span></span>

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

<span data-ttu-id="6a4b8-159">Olá Toolkit do Azure cria a aplicação web de Olá e apresenta uma caixa de diálogo de progresso.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-159">hello Azure Toolkit creates hello web app and displays a progress dialog box.</span></span>

![Caixa de diálogo Progresso de Criar Serviço de Aplicações](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a><span data-ttu-id="6a4b8-161">Caixa de diálogo Implementar Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="6a4b8-161">Deploy Web App dialog box</span></span>

<span data-ttu-id="6a4b8-162">No Olá **implementar Web App** caixa de diálogo, selecione **implementar tooroot**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-162">In hello **Deploy Web App** dialog box, select **Deploy tooroot**.</span></span> <span data-ttu-id="6a4b8-163">Se tiver um serviço de aplicações em *wingtiptoys.azurewebsites.net* e não implementar toohello raiz, aplicação web de Olá designada **MyFirstJavaOnAzureWebApp** é implementado demasiado *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-163">If you have an app service at *wingtiptoys.azurewebsites.net* and you do not deploy toohello root, hello web app named **MyFirstJavaOnAzureWebApp** is deployed too*wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.</span></span>

![Caixa de diálogo Implementar Aplicação Web](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

<span data-ttu-id="6a4b8-165">mostra de caixa de diálogo Olá hello do Azure, JDK e seleções de contentor web.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-165">hello dialog box shows hello Azure, JDK, and web container selections.</span></span>

<span data-ttu-id="6a4b8-166">Selecione **implementar** toopublish Olá web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-166">Select **Deploy** toopublish hello web app tooAzure.</span></span>

<span data-ttu-id="6a4b8-167">Quando concluir a publicação de Olá, selecione Olá **publicada** ligação no Olá **registo de atividade do Azure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-167">When hello publishing finishes, select hello **Published** link in hello **Azure Activity Log** dialog box.</span></span>

![Caixa de diálogo de Registo de Atividade do Azure](./media/app-service-web-get-started-java/aal.png)

<span data-ttu-id="6a4b8-169">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="6a4b8-169">Congratulations!</span></span> <span data-ttu-id="6a4b8-170">Implementados com êxito a sua tooAzure de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-170">You have successfully deployed your web app tooAzure.</span></span> 

!["Olá, Azure!”](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a><span data-ttu-id="6a4b8-173">Atualizar a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="6a4b8-173">Update hello web app</span></span>

<span data-ttu-id="6a4b8-174">Alterar exemplo JSP código tooa outra mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-174">Change hello sample JSP code tooa different message.</span></span>

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

<span data-ttu-id="6a4b8-175">Guarde as alterações de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-175">Save hello changes.</span></span>

<span data-ttu-id="6a4b8-176">No Explorador de projeto, clique no projeto Olá e, em seguida, selecione **Azure** > **publicar como aplicação Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-176">In Project Explorer, right-click hello project, and then select **Azure** > **Publish as Azure Web App**.</span></span>

<span data-ttu-id="6a4b8-177">Olá **implementar Web App** é apresentada a caixa de diálogo e mostra hello do serviço de aplicações que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-177">hello **Deploy Web App** dialog box appears and shows hello app service that you previously created.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a4b8-178">Selecione **implementar tooroot** sempre publicar.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-178">Select **Deploy tooroot** each time you publish.</span></span>
>

<span data-ttu-id="6a4b8-179">Selecione a aplicação web de Olá e selecione **implementar**, que publica alterações Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-179">Select hello web app and select **Deploy**, which publishes hello changes.</span></span>

<span data-ttu-id="6a4b8-180">Quando Olá **publicação** ligação for apresentada, selecione-a aplicação de web de toohello toobrowse e ver Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-180">When hello **Publishing** link appears, select it toobrowse toohello web app and see hello changes.</span></span>

## <a name="manage-hello-web-app"></a><span data-ttu-id="6a4b8-181">Gerir a aplicação web de Olá</span><span class="sxs-lookup"><span data-stu-id="6a4b8-181">Manage hello web app</span></span>

<span data-ttu-id="6a4b8-182">Aceda toohello <a href="https://portal.azure.com" target="_blank">portal do Azure</a> toosee Olá web aplicação que criou.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-182">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toosee hello web app that you created.</span></span>

<span data-ttu-id="6a4b8-183">No menu à esquerda de Olá, selecione **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-183">From hello left menu, select **Resource Groups**.</span></span>

![Grupos de tooresource de navegação do portal](media/app-service-web-get-started-java/rg.png)

<span data-ttu-id="6a4b8-185">Selecione o grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-185">Select hello resource group.</span></span> <span data-ttu-id="6a4b8-186">página Olá mostra recursos Olá que criou neste guia de introdução.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-186">hello page shows hello resources that you created in this quickstart.</span></span>

![Grupo de recursos myResourceGroup](media/app-service-web-get-started-java/rg2.png)

<span data-ttu-id="6a4b8-188">Selecione Olá web app (**webapp 170602193915** no Olá anterior a imagem).</span><span class="sxs-lookup"><span data-stu-id="6a4b8-188">Select hello web app (**webapp-170602193915** in hello preceding image).</span></span>

<span data-ttu-id="6a4b8-189">Olá **descrição geral** é apresentada a página.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-189">hello **Overview** page appears.</span></span> <span data-ttu-id="6a4b8-190">Esta página dá-lhe uma vista de como aplicação Olá está a fazer.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-190">This page gives you a view of how hello app is doing.</span></span> <span data-ttu-id="6a4b8-191">Aqui, pode realizar tarefas de gestão básicas, como navegar, parar, iniciar, reiniciar e eliminar.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-191">Here, you can  perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="6a4b8-192">separadores Olá no lado esquerdo do Olá da página Olá mostram Olá configurações diferentes em que pode abrir.</span><span class="sxs-lookup"><span data-stu-id="6a4b8-192">hello tabs on hello left side of hello page show hello different configurations that you can open.</span></span> 

![Página Serviço de Aplicações no portal do Azure](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a><span data-ttu-id="6a4b8-194">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6a4b8-194">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a4b8-195">Mapear domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="6a4b8-195">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
