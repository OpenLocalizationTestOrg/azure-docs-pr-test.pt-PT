---
title: "aaaCreate uma aplicação do Azure de linha de negócio com a autenticação do Azure Active Directory | Microsoft Docs"
description: "Saiba como toocreate um ASP.NET MVC linha de negócio de aplicação no App Service do Azure que efetua a autenticação no Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="fa922-103">Criar uma aplicação do Azure de linha de negócio com a autenticação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa922-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="fa922-104">Este artigo mostra como aplicação toocreate um .NET linha de negócio no [Web Apps do Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) utilizando Olá [autenticação / autorização](../app-service/app-service-authentication-overview.md) funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="fa922-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="fa922-105">Também mostra como toouse Olá [Active Directory Graph API do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery dados de diretório numa aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="fa922-106">inquilino do Azure Active Directory de Olá que utiliza pode ser um diretório só de Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="fa922-107">Em alternativa, pode ser [sincronizadas com o Active Directory no local](../active-directory/active-directory-aadconnect.md) toocreate uma experiência único início de sessão para workers que estão no local e remoto.</span><span class="sxs-lookup"><span data-stu-id="fa922-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="fa922-108">Este artigo utiliza o diretório predefinido de Olá para a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="fa922-109">O que irá criar</span><span class="sxs-lookup"><span data-stu-id="fa922-109">What you will build</span></span>
<span data-ttu-id="fa922-110">Irá criar uma simples aplicação de linha de negócio criar-leitura-atualizar-eliminar (CRUD) nas Web Apps do App Service que controla itens de trabalho com Olá seguintes funcionalidades:</span><span class="sxs-lookup"><span data-stu-id="fa922-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="fa922-111">Autentica os utilizadores no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fa922-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="fa922-112">Utilizadores de diretório de consulta e grupos utilizando [Active Directory Graph API do Azure](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="fa922-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="fa922-113">Utilize Olá ASP.NET MVC *sem autenticação* modelo</span><span class="sxs-lookup"><span data-stu-id="fa922-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="fa922-114">Se precisar de controlo de acesso baseado em funções (RBAC) para a sua aplicação de linha de negócio no Azure, consulte [passo seguinte](#next).</span><span class="sxs-lookup"><span data-stu-id="fa922-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="fa922-115">Do que precisa</span><span class="sxs-lookup"><span data-stu-id="fa922-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="fa922-116">Tem de Olá seguintes toocomplete neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="fa922-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="fa922-117">Um inquilino do Azure Active Directory com utilizadores em vários grupos</span><span class="sxs-lookup"><span data-stu-id="fa922-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="fa922-118">Aplicações de toocreate permissões no inquilino do Azure Active Directory de Olá</span><span class="sxs-lookup"><span data-stu-id="fa922-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="fa922-119">Visual Studio 2013 atualização 4 ou posterior</span><span class="sxs-lookup"><span data-stu-id="fa922-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="fa922-120">Azure SDK 2.8.1 ou posterior</span><span class="sxs-lookup"><span data-stu-id="fa922-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="fa922-121">Criar e implementar uma tooAzure de aplicação web</span><span class="sxs-lookup"><span data-stu-id="fa922-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="fa922-122">No Visual Studio, clique em **ficheiro** > **novo** > **projeto**.</span><span class="sxs-lookup"><span data-stu-id="fa922-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="fa922-123">Selecione **aplicação Web ASP.NET**, nomeie o projeto e, em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa922-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="fa922-124">Selecione Olá **MVC** modelo, em seguida, alterar autenticação Olá demasiado**sem autenticação**.</span><span class="sxs-lookup"><span data-stu-id="fa922-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="fa922-125">Certifique-se **anfitrião na nuvem de Olá** está selecionada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa922-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="fa922-126">No Olá **criar App Service** caixa de diálogo, clique em **adicionar uma conta** (e, em seguida, **adicionar uma conta** na lista pendente de Olá) toolog no tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="fa922-127">Depois de a sessão configure a aplicação web.</span><span class="sxs-lookup"><span data-stu-id="fa922-127">Once logged in configure your web app.</span></span> <span data-ttu-id="fa922-128">Criar um grupo de recursos e um novo plano de serviço de aplicações ao clicar em Olá respetivo **novo** botão.</span><span class="sxs-lookup"><span data-stu-id="fa922-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="fa922-129">Clique em **explorar serviços Azure adicionais** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="fa922-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="fa922-130">No Olá **serviços** separador, clique em  **+**  tooadd uma base de dados do SQL Server para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="fa922-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="fa922-131">No **configurar a base de dados do SQL**, clique em **novo** toocreate uma instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa922-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="fa922-132">No **configurar o SQL Server**, configurar a sua instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fa922-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="fa922-133">Em seguida, clique em **OK**, **OK**, e **criar** tookick desativar a criação da aplicação Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="fa922-134">No **atividade do App Service do Azure**, pode ver quando a criação da aplicação Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="fa922-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="fa922-135">Clique em  **publicar &lt;* appname*> toothis aplicação Web agora * *, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="fa922-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="fa922-136">Depois de concluído o Visual Studio, é aberto Olá publicar a aplicação no browser Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="fa922-137">Configurar o acesso de autenticação e de diretório</span><span class="sxs-lookup"><span data-stu-id="fa922-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="fa922-138">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fa922-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fa922-139">No menu à esquerda Olá, clique em **serviços aplicacionais** > **&lt;*appname*> * * > **autenticação / autorização**.</span><span class="sxs-lookup"><span data-stu-id="fa922-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="fa922-140">Ativar a autenticação do Azure Active Directory, clicando em **no** > **do Azure Active Directory** > **Express** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa922-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="fa922-141">Clique em **guardar** na barra de comando Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="fa922-142">Depois de definições de autenticação de Olá são guardadas com êxito, tente navegar tooyour aplicação novamente no browser Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="fa922-143">As predefinições de impôr a autenticação na aplicação Olá de todo.</span><span class="sxs-lookup"><span data-stu-id="fa922-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="fa922-144">Se já não tiver sessão iniciada, é redirecionada tooa ecrã de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="fa922-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="fa922-145">Depois de a sessão, verá a aplicação protegida por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="fa922-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="fa922-146">Em seguida, precisa de aceder a tooenable toodirectory dados.</span><span class="sxs-lookup"><span data-stu-id="fa922-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="fa922-147">Navegue toohello [portal clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fa922-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="fa922-148">No menu à esquerda Olá, clique em **do Active Directory** > **diretório predefinido** > **aplicações**  >   **&lt;* appname*> * *.</span><span class="sxs-lookup"><span data-stu-id="fa922-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="fa922-149">Esta é a aplicação do Azure Active Directory Olá que serviço de aplicações criado para tooenable Olá autorização / funcionalidade de autenticação.</span><span class="sxs-lookup"><span data-stu-id="fa922-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="fa922-150">Clique em **utilizadores** e **grupos** toomake se de que tem alguns utilizadores e grupos no diretório de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="fa922-151">Se não, crie alguns grupos e utilizadores de teste.</span><span class="sxs-lookup"><span data-stu-id="fa922-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="fa922-152">Clique em **configurar** tooconfigure esta aplicação.</span><span class="sxs-lookup"><span data-stu-id="fa922-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="fa922-153">Desloque para baixo toohello **chaves** secção e adicionar uma chave ao selecionar uma duração.</span><span class="sxs-lookup"><span data-stu-id="fa922-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="fa922-154">Em seguida, clique em **permissões delegadas** e selecione **ler os dados de diretório**.</span><span class="sxs-lookup"><span data-stu-id="fa922-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="fa922-155">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fa922-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="fa922-156">Depois das definições são guardadas, desloque-se para uma cópia de segurança toohello **chaves** secção e clique em Olá **cópia** chave de cliente do botão toocopy Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="fa922-157">Se sair desta página agora, não será capaz de tooaccess este cliente chave nunca novamente.</span><span class="sxs-lookup"><span data-stu-id="fa922-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="fa922-158">Em seguida, terá de tooconfigure a aplicação web com esta chave.</span><span class="sxs-lookup"><span data-stu-id="fa922-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="fa922-159">Inicie sessão no toohello [Explorador de recursos do Azure](https://resources.azure.com) com a sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="fa922-160">Na Olá parte superior da página Olá, clique em **leitura/escrita** alterações toomake Olá Explorador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="fa922-161">Localizar Olá definições de autenticação para a sua aplicação, localizado em subscrições >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **fornecedores** > **Microsoft**  >  **sites** > **&lt;*appname*> * * > **configuração**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="fa922-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="fa922-162">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="fa922-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="fa922-163">No painel de edição de Olá, defina Olá `clientSecret` e `additionalLoginParams` propriedades da seguinte forma.</span><span class="sxs-lookup"><span data-stu-id="fa922-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="fa922-164">Clique em **colocar** em Olá toosubmit superior as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="fa922-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="fa922-165">Agora, tootest se tiver de autorização de Olá token tooaccess Olá Active Directory Graph API do Azure, basta navegar até ao  **https://&lt;*appname*>.azurewebsites.net/.auth/me** na sua browser.</span><span class="sxs-lookup"><span data-stu-id="fa922-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="fa922-166">Se configurou tudo corretamente, deverá ver Olá `access_token` propriedade no Olá resposta JSON.</span><span class="sxs-lookup"><span data-stu-id="fa922-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="fa922-167">Olá `~/.auth/me` caminho de URL é gerido pelo serviço de autenticação da aplicação / toogive de autorização todas as informações de Olá relacionadas com a sessão tooyour autenticado.</span><span class="sxs-lookup"><span data-stu-id="fa922-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="fa922-168">Para obter mais informações, consulte [autenticação e autorização no serviço de aplicações do Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fa922-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="fa922-169">Olá `access_token` tem um período de expiração.</span><span class="sxs-lookup"><span data-stu-id="fa922-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="fa922-170">No entanto, autenticação do serviço de aplicação / autorização fornece funcionalidade de token de atualização com `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="fa922-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="fa922-171">Para obter mais informações sobre como toouse-lo, consulte [App Store do Token de serviço](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="fa922-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="fa922-172">Em seguida, irá fazer algo útil com dados de diretório.</span><span class="sxs-lookup"><span data-stu-id="fa922-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="fa922-173">Adicionar aplicação tooyour de funcionalidade de linha de negócio</span><span class="sxs-lookup"><span data-stu-id="fa922-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="fa922-174">Agora, pode criar um controlador de itens de trabalho CRUD simple.</span><span class="sxs-lookup"><span data-stu-id="fa922-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="fa922-175">Na pasta de ~\Models Olá, crie um ficheiro de classe chamado WorkItem.cs e substitua `public class WorkItem {...}` com Olá seguinte código:</span><span class="sxs-lookup"><span data-stu-id="fa922-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="fa922-176">utilizar System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="fa922-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="fa922-177">classe pública {de item de trabalho</span><span class="sxs-lookup"><span data-stu-id="fa922-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="fa922-178">}</span><span class="sxs-lookup"><span data-stu-id="fa922-178">}</span></span>
   
     <span data-ttu-id="fa922-179">enum pública WorkItemStatus {</span><span class="sxs-lookup"><span data-stu-id="fa922-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="fa922-180">}</span><span class="sxs-lookup"><span data-stu-id="fa922-180">}</span></span>
2. <span data-ttu-id="fa922-181">Crie Olá projeto toomake a lógica de andaime do modelo toohello acessível novo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fa922-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="fa922-182">Adicionar um novo item estruturado `WorkItemsController` toohello ~\Controllers pasta (com o botão direito **controladores**, ponto demasiado**adicionar**e selecione **novo item estruturado**).</span><span class="sxs-lookup"><span data-stu-id="fa922-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="fa922-183">Selecione **controlador MVC 5 com vistas, utilizando o Entity Framework** e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fa922-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="fa922-184">Modelo de Olá selecione que criou, em seguida, clique em  **+**  e, em seguida, **adicionar** tooadd num contexto de dados e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fa922-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="fa922-185">~\Views\WorkItems\Create.cshtml (um item automaticamente estruturado), localize Olá `Html.BeginForm` método de programa auxiliar e torná-Olá alterações realçadas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa922-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="fa922-186">Tenha em atenção que `token` e `tenant` são utilizadas pelo Olá `AadPicker` toomake objeto chama o Active Directory Graph API do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa922-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="fa922-187">Irá adicionar `AadPicker` mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fa922-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="fa922-188">Pode obter apenas bem `token` e `tenant` do lado do cliente Olá com `~/.auth/me`, mas que seria uma chamada de servidor adicionais.</span><span class="sxs-lookup"><span data-stu-id="fa922-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="fa922-189">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fa922-189">For example:</span></span>
   > 
   > <span data-ttu-id="fa922-190">$.ajax ({dataType: "json," url: "/.auth/me", o êxito: função (dados) {var token = dados [0] .access_token; var inquilino = dados [0] .user_claims .find (c = > c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val;}});</span><span class="sxs-lookup"><span data-stu-id="fa922-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="fa922-191">Efetuar Olá alterações mesmas com ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="fa922-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="fa922-192">Olá `AadPicker` objeto é definido num script terá tooadd tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="fa922-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="fa922-193">Faça duplo clique Olá ~\Scripts pasta, aponte demasiado**adicionar**e clique em **ficheiro JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="fa922-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="fa922-194">Tipo `AadPickerLibrary` para Olá filename e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fa922-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="fa922-195">Copie o conteúdo Olá [aqui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) para ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="fa922-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="fa922-196">Script de Olá, Olá `AadPicker` objeto chamadas [Active Directory Graph API do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch para utilizadores e grupos que correspondem à entrada de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="fa922-197">~\Scripts\AadPickerLibrary.js também utiliza Olá [widget de conclusão automática de IU jQuery](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="fa922-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="fa922-198">Por isso, terá de projeto de tooyour tooadd jQuery IU.</span><span class="sxs-lookup"><span data-stu-id="fa922-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="fa922-199">Clique com o botão direito no projeto e clique em **gerir pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="fa922-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="fa922-200">No Gestor de pacotes NuGet Olá, clique em Procurar, tipo **jquery-ui** na barra de pesquisa de Olá e clique em **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="fa922-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="fa922-201">No painel direito Olá, clique em **instalar**, em seguida, clique em **OK** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="fa922-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="fa922-202">Abra ~\App_Start\BundleConfig.cs e Olá alterações realçadas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fa922-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="fa922-203">Existem mais toomanage de formas performant JavaScript e ficheiros CSS na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="fa922-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="fa922-204">No entanto, para simplicidade que apenas vai toopiggyback em pacotes de Olá que são carregados com cada vista.</span><span class="sxs-lookup"><span data-stu-id="fa922-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="fa922-205">Por fim, no ~ \Global.asax, adicionar Olá seguinte linha de código no Olá `Application_Start()` método.</span><span class="sxs-lookup"><span data-stu-id="fa922-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="fa922-206">`Ctrl`+`.`em cada erro de resolução de nomenclatura demasiado corrigir.</span><span class="sxs-lookup"><span data-stu-id="fa922-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="fa922-207">Terá desta linha de código porque utiliza o modelo MVC do Olá predefinido <code>[ValidateAntiForgeryToken]</code> decoration em algumas das ações de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="fa922-208">Devido a comportamento toohello descrito através de [Brock Allen](https://twitter.com/BrockLAllen) em [MVC 4, AntiForgeryToken e afirmações](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) o HTTP POST poderão falhar a validação de token antifalsificação porque:</span><span class="sxs-lookup"><span data-stu-id="fa922-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="fa922-209">Azure Active Directory não envia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider Olá, que é necessário por predefinição pelo token antifalsificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="fa922-210">Se o Azure Active Directory é diretório sincronizado com o AD FS, confiança Olá do AD FS por predefinição não enviar Olá http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider afirmação está, embora seja possível configurar manualmente toosend do AD FS Esta afirmação.</span><span class="sxs-lookup"><span data-stu-id="fa922-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="fa922-211">`ClaimTypes.NameIdentifies`Especifica a afirmação Olá `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que forneça o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fa922-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="fa922-212">Agora, publica as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="fa922-212">Now, publish your changes.</span></span> <span data-ttu-id="fa922-213">Clique no seu projeto e clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="fa922-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="fa922-214">Clique em **definições**, certifique-se de que existe está um tooyour de cadeia de ligação da base de dados do SQL Server, selecione **atualização de base de dados** toomake Olá alterações de esquema para o seu modelo e clique em **publicar** .</span><span class="sxs-lookup"><span data-stu-id="fa922-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="fa922-215">No browser Olá, navegue até toohttps: / /&lt;*appname*>.azurewebsites.net/workitems e clique em **criar novo**.</span><span class="sxs-lookup"><span data-stu-id="fa922-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="fa922-216">Clique na Olá **AssignedToName** caixa.</span><span class="sxs-lookup"><span data-stu-id="fa922-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="fa922-217">Deverá ver agora os utilizadores e grupos do seu inquilino do Azure Active Directory numa lista pendente.</span><span class="sxs-lookup"><span data-stu-id="fa922-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="fa922-218">Pode introduzir toofilter, ou utilizar Olá `Up` ou `Down` chave ou clique em tooselect Olá utilizador ou grupo.</span><span class="sxs-lookup"><span data-stu-id="fa922-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="fa922-219">Clique em **criar** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="fa922-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="fa922-220">Em seguida, clique em **editar** no trabalho Olá criado item tooobserve Olá mesmo comportamento.</span><span class="sxs-lookup"><span data-stu-id="fa922-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="fa922-221">Congrats, está agora a executar uma aplicação de linha de negócio no Azure com acesso de diretório!</span><span class="sxs-lookup"><span data-stu-id="fa922-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="fa922-222">Não há muito mais que pode fazer com o Olá Graph API.</span><span class="sxs-lookup"><span data-stu-id="fa922-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="fa922-223">Consulte [referência da API do Azure AD Graph](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="fa922-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="fa922-224">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="fa922-224">Next Step</span></span>
<span data-ttu-id="fa922-225">Se precisar de controlo de acesso baseado em funções (RBAC) para a sua aplicação de linha de negócio no azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para um exemplo da equipa do Azure Active Directory de Olá.</span><span class="sxs-lookup"><span data-stu-id="fa922-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="fa922-226">Mostra-lhe como tooenable funções para a sua aplicação do Azure Active Directory e, em seguida, autorizar os utilizadores com Olá `[Authorize]` decoration.</span><span class="sxs-lookup"><span data-stu-id="fa922-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="fa922-227">Se a aplicação de linha de negócios tem de aceder a dados tooon local, consulte [acesso recursos no local utilizando as ligações híbridas no App Service do Azure](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fa922-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="fa922-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="fa922-228">Further resources</span></span>
* [<span data-ttu-id="fa922-229">Autenticação e autorização no serviço de aplicações do Azure</span><span class="sxs-lookup"><span data-stu-id="fa922-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="fa922-230">Autenticar com o Active Directory no local na sua aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="fa922-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="fa922-231">Criar uma aplicação de linha de negócio no Azure com a autenticação AD FS</span><span class="sxs-lookup"><span data-stu-id="fa922-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="fa922-232">Autenticação do serviço de aplicações e Olá AD Graph API do Azure</span><span class="sxs-lookup"><span data-stu-id="fa922-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="fa922-233">Amostras do Microsoft Azure Active Directory e a documentação</span><span class="sxs-lookup"><span data-stu-id="fa922-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="fa922-234">Azure Active Directory suportado Token e tipos de afirmação</span><span class="sxs-lookup"><span data-stu-id="fa922-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
