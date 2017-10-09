---
title: aaaFlask e armazenamento de tabelas do Azure no Azure com ferramentas do Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas do Python para Visual Studio toocreate uma aplicação web Flask que armazena dados no Table Storage do Azure e implemente-as Web Apps tooAzure App Service."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="cb80e-103">Flask e Table Storage do Azure no Azure com ferramentas do Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb80e-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="cb80e-104">Neste tutorial, iremos utilizar [ferramentas do Python para Visual Studio] toocreate uma simples aplicação web utilizando um dos modelos de exemplo Olá PTVS de consulta.</span><span class="sxs-lookup"><span data-stu-id="cb80e-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="cb80e-105">Este tutorial também está disponível como uma [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="cb80e-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="cb80e-106">aplicação de web de inquérito Olá define uma abstração para o repositório de, pelo que pode facilmente mudar entre diferentes tipos de repositórios (dentro da memória, armazenamento de tabelas do Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="cb80e-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="cb80e-107">Iremos irá aprender como de conta toocreate um Storage do Azure, como a tooconfigure Olá toouse de aplicação web Table Storage do Azure e como toopublish Olá aplicação web demasiado[Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="cb80e-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="cb80e-108">Consulte Olá [Centro para programadores do Python] para consultar mais artigos que abrangem o desenvolvimento de aplicações Web de serviço de aplicação do Azure com a PTVS utilizando Bottle, Flask e Django as estruturas web, com os serviços de MongoDB, Table Storage do Azure, MySQL e base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cb80e-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="cb80e-109">Embora este artigo incida no App Service, os passos de Olá são semelhantes quando desenvolver [Cloud Services do Azure].</span><span class="sxs-lookup"><span data-stu-id="cb80e-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb80e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb80e-110">Prerequisites</span></span>
* <span data-ttu-id="cb80e-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cb80e-111">Visual Studio 2015</span></span>
* <span data-ttu-id="cb80e-112">[Ferramentas do Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cb80e-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="cb80e-113">[ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cb80e-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="cb80e-114">[Ferramentas do Azure SDK para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="cb80e-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="cb80e-115">[Python 2.7 de 32 bits] ou [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="cb80e-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="cb80e-116">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="cb80e-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cb80e-117">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="cb80e-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="cb80e-118">Criar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="cb80e-118">Create hello Project</span></span>
<span data-ttu-id="cb80e-119">Nesta secção, vamos criar um projeto do Visual Studio utilizando um modelo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="cb80e-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="cb80e-120">Vamos criar um ambiente virtual e instalar pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="cb80e-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="cb80e-121">Em seguida, será executado aplicação Olá localmente utilizando o repositório de dentro da memória Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="cb80e-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="cb80e-122">No Visual Studio, selecione **Ficheiro**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="cb80e-123">Olá, modelos de projeto de Olá [ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio] estão disponíveis em **Python**, **amostras**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="cb80e-124">Selecione **inquéritos Flask Web Project** e clique em OK toocreate projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="cb80e-124">Select **Polls Flask Web Project** and click OK toocreate hello project.</span></span>
   
     ![Caixa de Diálogo Novo Projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="cb80e-126">Será pedido tooinstall de pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="cb80e-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="cb80e-127">Selecione **Instalar num ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-127">Select **Install into a virtual environment**.</span></span>
   
     ![Caixa de Diálogo de Pacotes Externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="cb80e-129">Selecione **Python 2.7** ou **Python 3.4** como o interpretador base Olá.</span><span class="sxs-lookup"><span data-stu-id="cb80e-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Caixa de Diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="cb80e-131">Confirme que a aplicação de Olá funciona premindo `F5`.</span><span class="sxs-lookup"><span data-stu-id="cb80e-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="cb80e-132">Por predefinição, a aplicação Olá utiliza um repositório de memória que não necessita de qualquer configuração.</span><span class="sxs-lookup"><span data-stu-id="cb80e-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="cb80e-133">Todos os dados é perdida quando o servidor de web de Olá está parado.</span><span class="sxs-lookup"><span data-stu-id="cb80e-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="cb80e-134">Clique em **Criar inquérito de exemplo**, em seguida, clique num inquérito e votar.</span><span class="sxs-lookup"><span data-stu-id="cb80e-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="cb80e-136">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cb80e-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="cb80e-137">operações de armazenamento toouse, precisa de uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb80e-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="cb80e-138">Pode criar uma conta de armazenamento, seguindo estes passos.</span><span class="sxs-lookup"><span data-stu-id="cb80e-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="cb80e-139">Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cb80e-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cb80e-140">Clique em Olá **novo** ícone na parte superior do Olá esquerda do Portal de Olá, em seguida, clique em **dados + armazenamento** > **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="cb80e-141">Clique em **criar**, em seguida, atribua um nome exclusivo de conta de armazenamento de Olá e crie um novo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="cb80e-141">Click on **Create**, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Criação rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="cb80e-143">Quando tiver sido criada a conta de armazenamento Olá, Olá **notificações** botão será flash um verde **êxito** e painel de conta de armazenamento a Olá está aberta tooshow que pertence toohello novo recurso do grupo criar.</span><span class="sxs-lookup"><span data-stu-id="cb80e-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="cb80e-144">Clique em Olá **chaves de acesso** parte no painel de conta de armazenamento a Olá.</span><span class="sxs-lookup"><span data-stu-id="cb80e-144">Click hello **Access Keys** part in hello storage account's blade.</span></span> <span data-ttu-id="cb80e-145">Tome nota do nome da conta Olá e Olá chave1.</span><span class="sxs-lookup"><span data-stu-id="cb80e-145">Take note of hello account name and hello key1.</span></span>
   
      ![Chaves](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="cb80e-147">Vamos precisar este tooconfigure informações projeto na secção seguinte, Olá.</span><span class="sxs-lookup"><span data-stu-id="cb80e-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="cb80e-148">Configurar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="cb80e-148">Configure hello Project</span></span>
<span data-ttu-id="cb80e-149">Nesta secção, iremos irá configurar a nossa conta de armazenamento do Olá do aplicação toouse que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="cb80e-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="cb80e-150">Iremos ver como as definições de ligação de tooobtain do Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb80e-150">We'll see how tooobtain connection settings from hello Azure Portal.</span></span> <span data-ttu-id="cb80e-151">Em seguida, iremos irá executar aplicação Olá localmente.</span><span class="sxs-lookup"><span data-stu-id="cb80e-151">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="cb80e-152">No Visual Studio, clique com o botão direito no nó do projeto no Explorador de soluções e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="cb80e-153">Clique em Olá **depurar** separador.</span><span class="sxs-lookup"><span data-stu-id="cb80e-153">Click on hello **Debug** tab.</span></span>
   
     ![Definições de depuração do projeto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="cb80e-155">Definir Olá valores de variáveis de ambiente de que a aplicação Olá **comando do servidor de depuração**, **ambiente**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-155">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="cb80e-156">Isto irá definir variáveis de ambiente de Olá quando que **iniciar depuração**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-156">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="cb80e-157">Se quiser Olá variáveis toobe definido quando a **iniciar sem depuração**, Olá conjunto mesmo valores em **executar comando de servidor** bem.</span><span class="sxs-lookup"><span data-stu-id="cb80e-157">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="cb80e-158">Em alternativa, pode definir variáveis de ambiente utilizando Olá painel de controlo do Windows.</span><span class="sxs-lookup"><span data-stu-id="cb80e-158">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="cb80e-159">Esta é uma opção melhor se pretender tooavoid armazenar credenciais no código fonte / ficheiro de projeto.</span><span class="sxs-lookup"><span data-stu-id="cb80e-159">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="cb80e-160">Tenha em atenção que, terá de toorestart Visual Studio para Olá nova ambiente valores toobe toohello disponíveis aplicação.</span><span class="sxs-lookup"><span data-stu-id="cb80e-160">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="cb80e-161">código de Olá que implementa o repositório do Olá Table Storage do Azure está a ser **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-161">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="cb80e-162">Consulte Olá [documentação] para obter mais informações sobre como toouse serviço tabela do Python.</span><span class="sxs-lookup"><span data-stu-id="cb80e-162">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="cb80e-163">Executar a aplicação Olá com `F5`.</span><span class="sxs-lookup"><span data-stu-id="cb80e-163">Run hello application with `F5`.</span></span> <span data-ttu-id="cb80e-164">Os inquéritos criados com **Criar inquérito de exemplo** e dados de Olá submetidos por voto serão serializados na Table Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb80e-164">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cb80e-165">Olá ambiente Virtual do Python 2.7 pode causar uma quebra de exceção no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb80e-165">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="cb80e-166">Prima `F5` toocontinue ao carregar o projeto web de Olá.</span><span class="sxs-lookup"><span data-stu-id="cb80e-166">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="cb80e-167">Procurar toohello **sobre** tooverify de página que Olá aplicação está a utilizar Olá **Table Storage do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="cb80e-167">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="cb80e-169">Explorar Olá Table Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="cb80e-169">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="cb80e-170">É fácil tooview e editar as tabelas do storage utilizando Cloud Explorer no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cb80e-170">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="cb80e-171">Nesta secção iremos utilizar o Explorador de servidores tooview Olá do conteúdo das tabelas de aplicação Olá inquérito.</span><span class="sxs-lookup"><span data-stu-id="cb80e-171">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="cb80e-172">Isto requer toobe de ferramentas do Microsoft Azure instalada, que estão disponíveis como parte da Olá [Azure SDK para .NET].</span><span class="sxs-lookup"><span data-stu-id="cb80e-172">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="cb80e-173">Abra **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="cb80e-174">Expanda **contas do Storage**, a conta de armazenamento, em seguida, **tabelas**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="cb80e-176">Faça duplo clique no Olá **inquéritos** ou **escolhas** conteúdo de Olá tooview da tabela de Olá na janela de documento, bem como adicionar/remover/editar entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="cb80e-176">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Resultados da consulta de tabela](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="cb80e-178">Publicar Olá web app tooAzure do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="cb80e-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="cb80e-179">Olá SDK .NET do Azure fornece uma forma fácil toodeploy sua tooAzure de aplicação web do serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="cb80e-179">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="cb80e-180">No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Caixa de Diálogo Publicar Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="cb80e-182">Clique em **Web Apps do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="cb80e-183">Clique em **novo** toocreate uma nova aplicação web.</span><span class="sxs-lookup"><span data-stu-id="cb80e-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="cb80e-184">Preencha Olá seguintes campos e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-184">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="cb80e-185">**Nome da Aplicação Web**</span><span class="sxs-lookup"><span data-stu-id="cb80e-185">**Web App name**</span></span>
   * <span data-ttu-id="cb80e-186">**Plano do Serviço de Aplicações**</span><span class="sxs-lookup"><span data-stu-id="cb80e-186">**App Service plan**</span></span>
   * <span data-ttu-id="cb80e-187">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="cb80e-187">**Resource group**</span></span>
   * <span data-ttu-id="cb80e-188">**Região**</span><span class="sxs-lookup"><span data-stu-id="cb80e-188">**Region**</span></span>
   * <span data-ttu-id="cb80e-189">Deixe **servidor de base de dados** definido demasiado**nenhuma base de dados**</span><span class="sxs-lookup"><span data-stu-id="cb80e-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="cb80e-190">Aceite todas as outras predefinições e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="cb80e-191">O browser abrirá automaticamente toohello web publicada aplicação.</span><span class="sxs-lookup"><span data-stu-id="cb80e-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="cb80e-192">Se procurar toohello sobre página, verá que utiliza Olá **dentro da memória** repositório, não Olá **Table Storage do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="cb80e-192">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="cb80e-193">Isto acontece porque as variáveis de ambiente de Olá não são definidas na instância do Olá Web Apps no App Service do Azure, para que utiliza os valores predefinidos de Olá especificados no **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-193">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="cb80e-194">Configurar a instância de Web Apps Olá</span><span class="sxs-lookup"><span data-stu-id="cb80e-194">Configure hello Web Apps instance</span></span>
<span data-ttu-id="cb80e-195">Nesta secção, iremos irá configurar variáveis de ambiente para a instância de Web Apps Olá.</span><span class="sxs-lookup"><span data-stu-id="cb80e-195">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="cb80e-196">No [Portal do Azure](https://portal.azure.com), abra o painel da aplicação web Olá clicando **procurar** > **serviços aplicacionais** > nome da aplicação web.</span><span class="sxs-lookup"><span data-stu-id="cb80e-196">In [Azure Portal](https://portal.azure.com), open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="cb80e-197">No painel da sua aplicação web, clique em **todas as definições**, em seguida, clique em **definições da aplicação**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="cb80e-198">Desloque para baixo toohello **as definições de aplicação** secção e definir valores de Olá para **REPOSITÓRIO\_nome**, **armazenamento\_nome** e  **ARMAZENAMENTO\_chave** conforme descrito em Olá **projeto de Olá configurar** secção acima.</span><span class="sxs-lookup"><span data-stu-id="cb80e-198">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Definições de aplicação](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="cb80e-200">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb80e-200">Click on **Save**.</span></span> <span data-ttu-id="cb80e-201">Após ter recebido notificações Olá que foram aplicadas alterações de Olá, clique em **procurar** Olá Web principal no painel da aplicação.</span><span class="sxs-lookup"><span data-stu-id="cb80e-201">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="cb80e-202">Deverá ver o trabalho de aplicação web de Olá conforme esperado, utilizando Olá **Table Storage do Azure** repositório.</span><span class="sxs-lookup"><span data-stu-id="cb80e-202">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="cb80e-203">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="cb80e-203">Congratulations!</span></span>
   
     ![Browser](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="cb80e-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="cb80e-205">Next steps</span></span>
<span data-ttu-id="cb80e-206">Siga estes toolearn ligações mais sobre as ferramentas do Python para Visual Studio, Flask e Table Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb80e-206">Follow these links toolearn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="cb80e-207">[Documentação das Ferramentas do Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cb80e-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="cb80e-208">[Projetos Web]</span><span class="sxs-lookup"><span data-stu-id="cb80e-208">[Web Projects]</span></span>
  * <span data-ttu-id="cb80e-209">[Projetos do Serviço em Nuvem]</span><span class="sxs-lookup"><span data-stu-id="cb80e-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="cb80e-210">[Depuração Remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="cb80e-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="cb80e-211">[Documentação do flask]</span><span class="sxs-lookup"><span data-stu-id="cb80e-211">[Flask Documentation]</span></span>
* <span data-ttu-id="cb80e-212">[Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="cb80e-212">[Azure Storage]</span></span>
* <span data-ttu-id="cb80e-213">[Azure SDK for Python] (Azure SDK para Python)</span><span class="sxs-lookup"><span data-stu-id="cb80e-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="cb80e-214">[Como tooUse Olá o serviço de armazenamento de tabela do Python]</span><span class="sxs-lookup"><span data-stu-id="cb80e-214">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="cb80e-215">O que mudou</span><span class="sxs-lookup"><span data-stu-id="cb80e-215">What's changed</span></span>
* <span data-ttu-id="cb80e-216">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="cb80e-216">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro para programadores do Python]: /develop/python/
[Cloud Services do Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentação]:../cosmos-db/table-storage-how-to-use-python.md
[Como tooUse Olá o serviço de armazenamento de tabela do Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK para .NET]: http://azure.microsoft.com/downloads/ (Azure SDK para .NET)
[ferramentas do Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas do Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do Azure SDK para VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentação das Ferramentas do Python para Visual Studio]: http://aka.ms/ptvsdocs
[Documentação do flask]: http://flask.pocoo.org/
[Depuração Remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do Serviço em Nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Armazenamento do Azure]: http://azure.microsoft.com/documentation/services/storage/
[Azure SDK for Python]: https://github.com/Azure/azure-sdk-for-python (Azure SDK para Python)
