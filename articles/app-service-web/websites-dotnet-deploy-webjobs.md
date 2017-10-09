---
title: aaaDeploy WebJobs com o Visual Studio
description: "Saiba como toodeploy WebJobs do Azure tooAzure serviço Web Apps do App com o Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="3452a-103">Implementar o WebJobs com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3452a-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="3452a-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="3452a-104">Overview</span></span>
<span data-ttu-id="3452a-105">Este tópico explica como toouse Visual Studio toodeploy uma aplicação de consola projeto aplicação web de tooa no [do serviço de aplicações](http://go.microsoft.com/fwlink/?LinkId=529714) como um [trabalho Web do Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="3452a-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="3452a-106">Para obter informações sobre como toodeploy WebJobs utilizando Olá [Portal do Azure](https://portal.azure.com), consulte [tarefas de execução em segundo plano com WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="3452a-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="3452a-107">Quando o Visual Studio implementa um projeto de aplicação de consola com WebJobs, executa duas tarefas:</span><span class="sxs-lookup"><span data-stu-id="3452a-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="3452a-108">Tempo de execução de cópias ficheiros toohello pasta adequada no Olá web app (*App_Data/tarefas/contínua* para WebJobs contínuos, *App_Data/tarefas/acionada* para WebJobs agendadas e a pedido).</span><span class="sxs-lookup"><span data-stu-id="3452a-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="3452a-109">Configura [tarefas do agendador do Azure](#scheduler) para WebJobs são agendada toorun em alturas específicas.</span><span class="sxs-lookup"><span data-stu-id="3452a-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="3452a-110">(Isto não é necessária para WebJobs contínuos.)</span><span class="sxs-lookup"><span data-stu-id="3452a-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="3452a-111">Um projeto preparados WebJobs tem Olá tooit adicionados itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3452a-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="3452a-112">Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) pacote NuGet.</span><span class="sxs-lookup"><span data-stu-id="3452a-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="3452a-113">A [settings.json webjob publicar](#publishsettings) ficheiro que contém as definições de implementação e programador.</span><span class="sxs-lookup"><span data-stu-id="3452a-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagrama que mostra o que é adicionado a implementação de tooenable tooa aplicação de consola como um trabalho Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="3452a-115">Pode adicionar estes tooan de itens existentes projeto de aplicação de consola ou utilizar um modelo toocreate um novo projeto de aplicação de consola com WebJobs.</span><span class="sxs-lookup"><span data-stu-id="3452a-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="3452a-116">Pode implementar um projeto como um WebJob por si só ou ligue-o projeto web de tooa para que implementa automaticamente sempre que implementar o projeto web de Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="3452a-117">toolink projetos, o Visual Studio inclui o nome de Olá do projeto de ativado o WebJobs Olá num [webjobs list.json](#webjobslist) ficheiros no projeto web de Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagrama que mostra o projeto de WebJob tooweb projeto de ligação](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="3452a-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3452a-119">Prerequisites</span></span>
<span data-ttu-id="3452a-120">Funcionalidades de implementação de WebJobs estão disponíveis no Visual Studio quando instala Olá Azure SDK para .NET:</span><span class="sxs-lookup"><span data-stu-id="3452a-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="3452a-121">[Azure SDK para .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3452a-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="3452a-122"><a id="convert"></a>Ativar a implementação de WebJobs para um projeto de aplicação de consola existente</span><span class="sxs-lookup"><span data-stu-id="3452a-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="3452a-123">Tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="3452a-123">You have two options:</span></span>

* <span data-ttu-id="3452a-124">[Ativar a implementação automática com um projeto web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="3452a-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="3452a-125">Configure um projeto de aplicação de consola existente para que o se implementa automaticamente como um WebJob quando implementar um projeto web.</span><span class="sxs-lookup"><span data-stu-id="3452a-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="3452a-126">Utilize esta opção quando quiser toorun o trabalho Web em Olá mesma aplicação web na qual executar Olá relacionadas com a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="3452a-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="3452a-127">[Ativar a implementação sem um projeto web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="3452a-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="3452a-128">Configure um toodeploy de projeto de aplicação de consola existente como um WebJob por si só, com o projeto de web de tooa nenhuma ligação.</span><span class="sxs-lookup"><span data-stu-id="3452a-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="3452a-129">Utilize esta opção quando quiser toorun um WebJob numa aplicação web por si só, com nenhuma aplicação web em execução na aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="3452a-130">É aconselhável toodo isto na ordem tooscale capaz de toobe os recursos de trabalho Web independentemente os recursos de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="3452a-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="3452a-131"><a id="convertlink"></a>Ativar a implementação automática de WebJobs com um projeto web</span><span class="sxs-lookup"><span data-stu-id="3452a-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="3452a-132">Contexto Olá web projeto **Explorador de soluções**e, em seguida, clique em **adicionar** > **projeto existente como o trabalho Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3452a-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Projeto existente como o trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="3452a-134">Olá [trabalho Web do Azure de adicionar](#configure) é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3452a-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="3452a-135">No Olá **nome do projeto** na lista pendente, selecione Olá tooadd de projeto de aplicação de consola como um WebJob.</span><span class="sxs-lookup"><span data-stu-id="3452a-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Selecionar o projeto na caixa de diálogo Adicionar WebJob do Azure](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="3452a-137">Olá concluída [trabalho Web do Azure de adicionar](#configure) caixa de diálogo e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3452a-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="3452a-138"><a id="convertnolink"></a>Ativar a implementação de WebJobs sem um projeto web</span><span class="sxs-lookup"><span data-stu-id="3452a-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="3452a-139">Projeto de aplicação de consola do contexto Olá no **Explorador de soluções**e, em seguida, clique em **publicar como trabalho Web do Azure...** .</span><span class="sxs-lookup"><span data-stu-id="3452a-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publicar como trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="3452a-141">Olá [trabalho Web do Azure de adicionar](#configure) caixa de diálogo é apresentada, com o projeto de Olá selecionado na Olá **nome do projeto** caixa.</span><span class="sxs-lookup"><span data-stu-id="3452a-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="3452a-142">Olá concluída [trabalho Web do Azure de adicionar](#configure) caixa de diálogo e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3452a-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="3452a-143">Olá **publicar Web** é apresentado o assistente.</span><span class="sxs-lookup"><span data-stu-id="3452a-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="3452a-144">Se não quiser toopublish imediatamente, feche o Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="3452a-145">definições de Olá que introduziu são guardadas para quando quiser demasiado[implementar o projeto de Olá](#deploy).</span><span class="sxs-lookup"><span data-stu-id="3452a-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="3452a-146"><a id="create"></a>Criar um novo projeto WebJobs-ativado</span><span class="sxs-lookup"><span data-stu-id="3452a-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="3452a-147">toocreate um novo projeto WebJobs ativado, pode utilizar Olá aplicação de consola projeto modelo e ativar WebJobs implementação conforme explicado no [Olá secção anterior](#convert).</span><span class="sxs-lookup"><span data-stu-id="3452a-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="3452a-148">Como alternativa, pode utilizar o modelo de novo projeto do Olá WebJobs:</span><span class="sxs-lookup"><span data-stu-id="3452a-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="3452a-149">Utilizar o modelo de novo projeto de WebJobs Olá para um WebJob independente</span><span class="sxs-lookup"><span data-stu-id="3452a-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="3452a-150">Criar um projeto e configurá-lo toodeploy autonomamente como um WebJob, com o projeto de web de tooa nenhuma ligação.</span><span class="sxs-lookup"><span data-stu-id="3452a-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="3452a-151">Utilize esta opção quando quiser toorun um WebJob numa aplicação web por si só, com nenhuma aplicação web em execução na aplicação web de Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="3452a-152">É aconselhável toodo isto na ordem tooscale capaz de toobe os recursos de trabalho Web independentemente os recursos de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="3452a-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="3452a-153">Utilizar o modelo de novo projeto de WebJobs Olá para um projeto web do trabalho Web tooa ligado</span><span class="sxs-lookup"><span data-stu-id="3452a-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="3452a-154">Crie um projeto que está configurado toodeploy automaticamente como um WebJob quando um projeto web na Olá mesma solução for implementada.</span><span class="sxs-lookup"><span data-stu-id="3452a-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="3452a-155">Utilize esta opção quando quiser toorun o trabalho Web em Olá mesma aplicação web na qual executar Olá relacionadas com a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="3452a-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="3452a-156">modelo de novo projeto de WebJobs Olá automaticamente instala os pacotes NuGet e inclui código *Program.cs* para Olá [SDK de WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="3452a-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="3452a-157">Se não quiser toouse Olá SDK de WebJobs, remover ou alterar Olá `host.RunAndBlock` instrução no *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="3452a-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="3452a-158"><a id="createnolink"></a>Utilizar o modelo de novo projeto de WebJobs Olá para um WebJob independente</span><span class="sxs-lookup"><span data-stu-id="3452a-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="3452a-159">Clique em **ficheiro** > **novo projeto**e, em seguida, no Olá **novo projeto** clique da caixa de diálogo **nuvem**  >   **Trabalho Web do Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="3452a-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Caixa de diálogo do projeto nova que mostra o modelo do trabalho Web](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="3452a-161">Siga as instruções de Olá apresentadas anteriormente demasiado[tornar Olá projeto de aplicação de consola um projeto de WebJobs independente](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="3452a-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="3452a-162"><a id="createlink"></a>Utilizar o modelo de novo projeto de WebJobs Olá para um projeto web do trabalho Web tooa ligado</span><span class="sxs-lookup"><span data-stu-id="3452a-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="3452a-163">Contexto Olá web projeto **Explorador de soluções**e, em seguida, clique em **adicionar** > **novo projeto do trabalho Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="3452a-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Nova entrada de menu do projeto de trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="3452a-165">Olá [trabalho Web do Azure de adicionar](#configure) é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3452a-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="3452a-166">Olá concluída [trabalho Web do Azure de adicionar](#configure) caixa de diálogo e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3452a-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="3452a-167"><a id="configure"></a>caixa de diálogo do Olá adicionar WebJob do Azure</span><span class="sxs-lookup"><span data-stu-id="3452a-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="3452a-168">Olá **trabalho Web do Azure de adicionar** caixa de diálogo permite-lhe introduzir o nome do WebJob Olá e executar a definição do modo para o trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="3452a-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Adicionar caixa de diálogo do trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="3452a-170">campos de Olá nesta caixa de diálogo correspondem toofields no Olá **nova tarefa** caixa de diálogo de Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3452a-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="3452a-171">Para obter mais informações, consulte [tarefas de execução em segundo plano com WebJobs](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="3452a-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="3452a-172">Para obter informações sobre a implementação da linha de comandos, consulte [ativação da linha de comandos ou entrega de Azure WebJobs contínuos](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="3452a-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="3452a-173">Se implementar um WebJob e, em seguida, decidir que pretende que o tipo de Olá toochange do trabalho Web e volte a implementar, terá de ficheiro do toodelete Olá settings.json webjobs publicar.</span><span class="sxs-lookup"><span data-stu-id="3452a-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="3452a-174">Esta ação irá tornar o Visual Studio Mostrar Olá novamente, as opções de publicação para que possa alterar o tipo de Olá do trabalho Web.</span><span class="sxs-lookup"><span data-stu-id="3452a-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="3452a-175">Se implementar um WebJob e mais tarde mudar de Olá modo execução contínua de toonon contínua ou vice-versa, o Visual Studio cria um WebJob novo no Azure quando implementar novamente.</span><span class="sxs-lookup"><span data-stu-id="3452a-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="3452a-176">Se alterar outras definições de agendamento, mas deixe executar modo Olá mesmo ou alternar entre agendada e a pedido, atualizações do Visual Studio Olá tarefa existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="3452a-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="3452a-177"><a id="publishsettings"></a>settings.json webjob publicar</span><span class="sxs-lookup"><span data-stu-id="3452a-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="3452a-178">Quando configurar uma aplicação de consola para a implementação de WebJobs, o Visual Studio instala Olá [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet pacote e armazena informações de agendamento um *settings.json webjob publicar*  ficheiros no projeto Olá *propriedades* pasta do projeto de WebJobs Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="3452a-179">Eis um exemplo desse ficheiro:</span><span class="sxs-lookup"><span data-stu-id="3452a-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="3452a-180">Pode editar este ficheiro diretamente e o Visual Studio fornece IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="3452a-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="3452a-181">esquema do ficheiro de Olá é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) e podem ser visualizados não existe.</span><span class="sxs-lookup"><span data-stu-id="3452a-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="3452a-182"><a id="webjobslist"></a>webjobs list.json</span><span class="sxs-lookup"><span data-stu-id="3452a-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="3452a-183">Quando liga um projeto do projeto preparados WebJobs tooa web, Visual Studio armazena o nome de Olá do projeto de WebJobs Olá num *webjobs list.json* ficheiros do projeto web Olá *propriedades* pasta.</span><span class="sxs-lookup"><span data-stu-id="3452a-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="3452a-184">lista de Olá pode conter vários projetos de WebJobs, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="3452a-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="3452a-185">Pode editar este ficheiro diretamente e o Visual Studio fornece IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="3452a-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="3452a-186">esquema do ficheiro de Olá é armazenada em [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) e podem ser visualizados não existe.</span><span class="sxs-lookup"><span data-stu-id="3452a-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="3452a-187"><a id="deploy"></a>Implementar um projeto de WebJobs</span><span class="sxs-lookup"><span data-stu-id="3452a-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="3452a-188">Um projeto de WebJobs que tenha ligado projeto web de tooa implementa automaticamente com o projeto web de Olá.</span><span class="sxs-lookup"><span data-stu-id="3452a-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="3452a-189">Para obter informações sobre a implementação do projeto web, consulte [como toodeploy tooWeb aplicações](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3452a-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="3452a-190">toodeploy um projeto de WebJobs por si só, clique no projeto Olá no **Explorador de soluções** e clique em **publicar como trabalho Web do Azure...** .</span><span class="sxs-lookup"><span data-stu-id="3452a-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publicar como trabalho Web do Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="3452a-192">Para um WebJob independente, Olá mesmo **publicar Web** assistente que é utilizado para projetos web é apresentada, mas com menos toochange disponíveis de definições.</span><span class="sxs-lookup"><span data-stu-id="3452a-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="3452a-193"><a id="nextsteps"></a>Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="3452a-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="3452a-194">Este artigo tem explicado como toodeploy WebJobs utilizando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3452a-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="3452a-195">Para obter mais informações sobre como toodeploy WebJobs do Azure, consulte o artigo [WebJobs do Azure - recomendado recursos - implementação](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="3452a-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

