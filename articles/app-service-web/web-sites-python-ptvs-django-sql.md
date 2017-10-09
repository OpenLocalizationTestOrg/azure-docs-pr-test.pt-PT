---
title: aaaDjango e a SQL Database no Azure com ferramentas do Python 2.2 para Visual Studio
description: "Saiba como toouse hello ferramentas do Python para Visual Studio toocreate uma aplicação web Django que armazena dados numa instância de base de dados SQL e implemente-as Web Apps tooAzure App Service."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="b54f9-103">O Django e a Base de Dados SQL no Azure com Ferramentas do Python 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b54f9-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="b54f9-104">Neste tutorial, iremos utilizar [ferramentas do Python para Visual Studio] toocreate uma simples aplicação web utilizando um dos modelos de exemplo Olá PTVS de consulta.</span><span class="sxs-lookup"><span data-stu-id="b54f9-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="b54f9-105">Este tutorial também está disponível como uma [vídeo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="b54f9-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="b54f9-106">Vamos aprender como toouse uma base de dados do SQL Server alojado no Azure, como tooconfigure Olá toouse de aplicação web uma base de dados do SQL Server e como toopublish Olá aplicação web demasiado[Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b54f9-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b54f9-107">Consulte Olá [Centro para programadores do Python] para consultar mais artigos que abrangem o desenvolvimento de aplicações Web de serviço de aplicação do Azure com a PTVS utilizando Bottle, Flask e Django as estruturas web, com os serviços de armazenamento de tabelas do Azure, MySQL e base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b54f9-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="b54f9-108">Embora este artigo incida no App Service, os passos de Olá são semelhantes quando desenvolver [Cloud Services do Azure].</span><span class="sxs-lookup"><span data-stu-id="b54f9-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b54f9-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b54f9-109">Prerequisites</span></span>
* <span data-ttu-id="b54f9-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b54f9-110">Visual Studio 2015</span></span>
* <span data-ttu-id="b54f9-111">[Python 2.7 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="b54f9-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="b54f9-112">[Ferramentas do Python 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b54f9-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="b54f9-113">[ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b54f9-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="b54f9-114">[Ferramentas do Azure SDK para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="b54f9-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="b54f9-115">Django 1.9 ou posterior</span><span class="sxs-lookup"><span data-stu-id="b54f9-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="b54f9-116">Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service.</span><span class="sxs-lookup"><span data-stu-id="b54f9-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b54f9-117">Sem cartões de crédito; sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="b54f9-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="b54f9-118">Criar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="b54f9-118">Create hello Project</span></span>
<span data-ttu-id="b54f9-119">Nesta secção, vamos criar um projeto do Visual Studio utilizando um modelo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b54f9-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="b54f9-120">Vamos criar um ambiente virtual e instalar pacotes necessários.</span><span class="sxs-lookup"><span data-stu-id="b54f9-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="b54f9-121">Vamos criar uma base de dados local utilizando o sqlite.</span><span class="sxs-lookup"><span data-stu-id="b54f9-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="b54f9-122">Em seguida, iremos irá executar localmente Olá web app.</span><span class="sxs-lookup"><span data-stu-id="b54f9-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="b54f9-123">No Visual Studio, selecione **Ficheiro**, **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="b54f9-124">Olá, modelos de projeto de Olá [ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio] estão disponíveis em **Python**, **amostras**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="b54f9-125">Selecione **projeto de Web Django de inquérito** e clique em OK toocreate projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Caixa de Diálogo Novo Projeto](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="b54f9-127">Será pedido tooinstall de pacotes externos.</span><span class="sxs-lookup"><span data-stu-id="b54f9-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="b54f9-128">Selecione **Instalar num ambiente virtual**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-128">Select **Install into a virtual environment**.</span></span>

     ![Caixa de Diálogo de Pacotes Externos](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="b54f9-130">Selecione **Python 2.7** como o interpretador base Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Caixa de Diálogo Adicionar Ambiente Virtual](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="b54f9-132">No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **Python**e, em seguida, selecione **migrar o Django**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b54f9-133">Em seguida, selecione **Criar Superutilizador do Django**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="b54f9-134">Isto irá abrir uma consola de gestão do Django e criar uma base de dados do sqlite na pasta do projeto de Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="b54f9-135">Siga as indicações de Olá toocreate um utilizador.</span><span class="sxs-lookup"><span data-stu-id="b54f9-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="b54f9-136">Confirme que a aplicação de Olá funciona premindo <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="b54f9-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="b54f9-137">Clique em **início de sessão** na barra de navegação de Olá na parte superior do Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="b54f9-139">Introduza as credenciais de Olá utilizador Olá que criou quando sincronizou a base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="b54f9-141">Clique em **Criar Inquérito de Exemplo**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-141">Click **Create Sample Polls**.</span></span>

      ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="b54f9-143">Clique num inquérito e vote.</span><span class="sxs-lookup"><span data-stu-id="b54f9-143">Click on a poll and vote.</span></span>

      ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="b54f9-145">Criar uma Base de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="b54f9-145">Create a SQL Database</span></span>
<span data-ttu-id="b54f9-146">Para a base de dados de Olá, vamos criar uma base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="b54f9-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="b54f9-147">Pode criar uma base de dados, seguindo estes passos.</span><span class="sxs-lookup"><span data-stu-id="b54f9-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="b54f9-148">Iniciar sessão Olá [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="b54f9-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="b54f9-149">Na Olá parte inferior do painel de navegação de Olá, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="b54f9-150">, clique em **dados + armazenamento** > **base de dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="b54f9-151">Configurar Olá nova base de dados do SQL Server ao criar um novo grupo de recursos e selecione Olá localização adequada para a mesma.</span><span class="sxs-lookup"><span data-stu-id="b54f9-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="b54f9-152">Assim que for criado Olá base de dados do SQL Server, clique em **abrir no Visual Studio** no painel da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="b54f9-153">Clique em **configurar a firewall**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="b54f9-154">No Olá **as definições da Firewall** painel, adicionar uma regra de firewall com **IP inicial** e **IP final** definir toohello endereço IP público do seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="b54f9-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="b54f9-155">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-155">Click **Save**.</span></span>

   <span data-ttu-id="b54f9-156">Isto permitirá que o servidor de base de dados de toohello ligações do seu computador de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="b54f9-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="b54f9-157">No painel da base de dados de Olá, clique **propriedades**, em seguida, clique em **Mostrar cadeias de ligação de base de dados**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="b54f9-158">Utilizar o Olá cópia botão tooput Olá valor **ADO.NET** na área de transferência Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="b54f9-159">Configurar Olá projeto</span><span class="sxs-lookup"><span data-stu-id="b54f9-159">Configure hello Project</span></span>
<span data-ttu-id="b54f9-160">Nesta secção, iremos irá configurar a nossa web app toouse Olá base de dados SQL que acabamos de criar.</span><span class="sxs-lookup"><span data-stu-id="b54f9-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="b54f9-161">Também vamos instalá adicionais Python pacotes necessários toouse SQL as bases de dados com o Django.</span><span class="sxs-lookup"><span data-stu-id="b54f9-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="b54f9-162">Em seguida, iremos irá executar localmente Olá web app.</span><span class="sxs-lookup"><span data-stu-id="b54f9-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="b54f9-163">No Visual Studio, abra **settings.py**, de Olá *ProjectName* pasta.</span><span class="sxs-lookup"><span data-stu-id="b54f9-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="b54f9-164">Cole temporariamente a cadeia de ligação de Olá num editor de Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="b54f9-165">cadeia de ligação de Olá está neste formato:</span><span class="sxs-lookup"><span data-stu-id="b54f9-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="b54f9-166">Editar definição de Olá de `DATABASES` toouse Olá os valores acima.</span><span class="sxs-lookup"><span data-stu-id="b54f9-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="b54f9-167">No Explorador de soluções, em **ambientes do Python**, faça duplo clique no ambiente virtual Olá e selecione **Instalar pacote do Python**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="b54f9-168">Instalar o pacote de Olá `pyodbc` utilizando **pip**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Caixa de diálogo de pacotes de Python instalar](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="b54f9-170">Instalar o pacote de Olá `django-pyodbc-azure` utilizando **pip**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Caixa de diálogo de pacotes de Python instalar](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="b54f9-172">No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **Python**e, em seguida, selecione **migrar o Django**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b54f9-173">Em seguida, selecione **Criar Superutilizador do Django**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="b54f9-174">Esta ação irá criar tabelas de Olá da base de dados do SQL Server Olá que criámos na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="b54f9-175">Siga Olá pede toocreate um utilizador, que não tem o utilizador de Olá toomatch na base de dados do sqlite Olá criado na primeira secção de Olá.</span><span class="sxs-lookup"><span data-stu-id="b54f9-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="b54f9-176">Executar a aplicação Olá com `F5`.</span><span class="sxs-lookup"><span data-stu-id="b54f9-176">Run hello application with `F5`.</span></span> <span data-ttu-id="b54f9-177">Os inquéritos criados com **Criar inquérito de exemplo** e dados de Olá submetidos por voto serão serializados na base de dados do Olá SQL.</span><span class="sxs-lookup"><span data-stu-id="b54f9-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="b54f9-178">Publicar Olá web app tooAzure do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="b54f9-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="b54f9-179">Olá SDK .NET do Azure fornece uma forma fácil toodeploy tooAzure de aplicação web a web Apps do App Service Web.</span><span class="sxs-lookup"><span data-stu-id="b54f9-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="b54f9-180">No **Explorador de soluções**, faça duplo clique no nó do projeto de Olá e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Caixa de Diálogo Publicar Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="b54f9-182">Clique em **Web Apps do Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="b54f9-183">Clique em **novo** toocreate uma nova aplicação web.</span><span class="sxs-lookup"><span data-stu-id="b54f9-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="b54f9-184">Preencha Olá seguintes campos e clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="b54f9-185">**Nome da Aplicação Web**</span><span class="sxs-lookup"><span data-stu-id="b54f9-185">**Web App name**</span></span>
   * <span data-ttu-id="b54f9-186">**Plano do Serviço de Aplicações**</span><span class="sxs-lookup"><span data-stu-id="b54f9-186">**App Service plan**</span></span>
   * <span data-ttu-id="b54f9-187">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="b54f9-187">**Resource group**</span></span>
   * <span data-ttu-id="b54f9-188">**Região**</span><span class="sxs-lookup"><span data-stu-id="b54f9-188">**Region**</span></span>
   * <span data-ttu-id="b54f9-189">Deixe **servidor de base de dados** definido demasiado**nenhuma base de dados**</span><span class="sxs-lookup"><span data-stu-id="b54f9-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="b54f9-190">Aceite todas as outras predefinições e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="b54f9-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="b54f9-191">O browser abrirá automaticamente toohello web publicada aplicação.</span><span class="sxs-lookup"><span data-stu-id="b54f9-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="b54f9-192">Deverá ver o trabalho de aplicação web de Olá conforme esperado, utilizando Olá **SQL** base de dados alojada no Azure.</span><span class="sxs-lookup"><span data-stu-id="b54f9-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="b54f9-193">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b54f9-193">Congratulations!</span></span>

     ![Browser](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="b54f9-195">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="b54f9-195">Next steps</span></span>
<span data-ttu-id="b54f9-196">Siga estes toolearn ligações mais sobre as ferramentas do Python para Visual Studio, Django e a SQL Database.</span><span class="sxs-lookup"><span data-stu-id="b54f9-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="b54f9-197">[Documentação das Ferramentas do Python para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b54f9-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="b54f9-198">[Projetos Web]</span><span class="sxs-lookup"><span data-stu-id="b54f9-198">[Web Projects]</span></span>
  * <span data-ttu-id="b54f9-199">[Projetos do Serviço em Nuvem]</span><span class="sxs-lookup"><span data-stu-id="b54f9-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="b54f9-200">[Depuração Remota no Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="b54f9-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="b54f9-201">[Documentação do Django]</span><span class="sxs-lookup"><span data-stu-id="b54f9-201">[Django Documentation]</span></span>
* <span data-ttu-id="b54f9-202">[Base de Dados SQL]</span><span class="sxs-lookup"><span data-stu-id="b54f9-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b54f9-203">O que mudou</span><span class="sxs-lookup"><span data-stu-id="b54f9-203">What's changed</span></span>
* <span data-ttu-id="b54f9-204">Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b54f9-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro para programadores do Python]: /develop/python/
[Cloud Services do Azure]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Portal do Azure]: https://portal.azure.com
[ferramentas do Python para Visual Studio]: http://aka.ms/ptvs
[Ferramentas do Python 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[ferramentas do Python 2.2 para VSIX de exemplo do Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Ferramentas do Azure SDK para VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentação das Ferramentas do Python para Visual Studio]: http://aka.ms/ptvsdocs
[Depuração Remota no Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projetos Web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projetos do Serviço em Nuvem]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentação do Django]: https://www.djangoproject.com/
[Base de Dados SQL]: /documentation/services/sql-database/
