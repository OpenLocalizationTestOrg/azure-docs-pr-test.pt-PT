---
title: "aaaAzure as credenciais de implementação do serviço de aplicações | Microsoft Docs"
description: "Saiba como toouse Olá as credenciais de implementação do App Service do Azure."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a><span data-ttu-id="e227c-103">Configurar as credenciais de implementação para o App Service do Azure</span><span class="sxs-lookup"><span data-stu-id="e227c-103">Configure deployment credentials for Azure App Service</span></span>
<span data-ttu-id="e227c-104">[App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) suportam dois tipos de credenciais para [implementação de Git local](app-service-deploy-local-git.md) e [implementação de FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="e227c-104">[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) supports two types of credentials for [local Git deployment](app-service-deploy-local-git.md) and [FTP/S deployment](app-service-deploy-ftp.md).</span></span> <span data-ttu-id="e227c-105">Estes são não Olá, mesmo que as suas credenciais do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e227c-105">These are not hello same as your Azure Active Directory credentials.</span></span>

* <span data-ttu-id="e227c-106">**Credenciais de utilizador ao nível**: um conjunto de credenciais de conta do Azure completo de Olá.</span><span class="sxs-lookup"><span data-stu-id="e227c-106">**User-level credentials**: one set of credentials for hello entire Azure account.</span></span> <span data-ttu-id="e227c-107">Pode ser utilizado toodeploy tooApp serviço para qualquer aplicação, em qualquer subscrição, o que Olá conta do Azure tem tooaccess de permissão.</span><span class="sxs-lookup"><span data-stu-id="e227c-107">It can be used toodeploy tooApp Service for any app, in any subscription, that hello Azure account has permission tooaccess.</span></span> <span data-ttu-id="e227c-108">Estes são o conjunto de credenciais predefinido do Olá que configurar na **serviços aplicacionais** > **&lt;APP_NAME>.azurewebsites.NET >** > **ascredenciaisdeimplementação**.</span><span class="sxs-lookup"><span data-stu-id="e227c-108">These are hello default credentials set that you configure in **App Services** > **&lt;app_name>** > **Deployment credentials**.</span></span> <span data-ttu-id="e227c-109">Isto também é Olá conjunto predefinido que é apresentado no portal de Olá GUI (por exemplo, Olá **descrição geral** e **propriedades** da sua aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span><span class="sxs-lookup"><span data-stu-id="e227c-109">This is also hello default set that's surfaced in hello portal GUI (such as hello **Overview** and **Properties** of your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources)).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e227c-110">Quando delegar tooAzure de aceder aos recursos através de controlo de acesso baseado em ' (RBAC) da função ou coadministrador de permissões, cada utilizador do Azure que recebe acesso tooan aplicação pode utilizar sua credenciais de nível de utilizador pessoais até que o acesso é revogado.</span><span class="sxs-lookup"><span data-stu-id="e227c-110">When you delegate access tooAzure resources via Role Based Access Control (RBAC) or co-admin permissions, each Azure user that receives access tooan app can use his/her personal user-level credentials until access is revoked.</span></span> <span data-ttu-id="e227c-111">Estas credenciais de implementação não devem ser partilhados com outros utilizadores do Azure.</span><span class="sxs-lookup"><span data-stu-id="e227c-111">These deployment credentials should not be shared with other Azure users.</span></span>
    >
    >

* <span data-ttu-id="e227c-112">**Credenciais ao nível da aplicação**: um conjunto de credenciais para cada aplicação.</span><span class="sxs-lookup"><span data-stu-id="e227c-112">**App-level credentials**: one set of credentials for each app.</span></span> <span data-ttu-id="e227c-113">Pode ser utilizado toodeploy aplicação de toothat apenas.</span><span class="sxs-lookup"><span data-stu-id="e227c-113">It can be used toodeploy toothat app only.</span></span> <span data-ttu-id="e227c-114">credenciais de Olá para cada aplicação é gerada automaticamente durante a criação da aplicação e se encontra da aplicação Olá perfil de publicação.</span><span class="sxs-lookup"><span data-stu-id="e227c-114">hello credentials for each app is generated automatically at app creation, and is found in hello app's publish profile.</span></span> <span data-ttu-id="e227c-115">Não é possível configurar manualmente as credenciais de Olá, mas pode repô-los para uma aplicação em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="e227c-115">You cannot manually configure hello credentials, but you can reset them for an app anytime.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e227c-116">Na ordem toogive alguém aceder a credenciais toothese através de função de acesso baseado em controlo (RBAC), terá de toomake-los contribuinte ou superior no Olá aplicação Web.</span><span class="sxs-lookup"><span data-stu-id="e227c-116">In order toogive someone access toothese credentials via Role Based Access Control (RBAC), you need toomake them contributor or higher on hello Web App.</span></span> <span data-ttu-id="e227c-117">Os leitores não são permitidos toopublish e, por conseguinte, não é possível aceder essas credenciais.</span><span class="sxs-lookup"><span data-stu-id="e227c-117">Readers are not allowed toopublish, and hence can't access those credentials.</span></span>
    >
    >

## <span data-ttu-id="e227c-118"><a name="userscope"></a>Definir e repor as credenciais de nível de utilizador</span><span class="sxs-lookup"><span data-stu-id="e227c-118"><a name="userscope"></a>Set and reset user-level credentials</span></span>

<span data-ttu-id="e227c-119">Pode configurar as suas credenciais de nível de utilizador em qualquer aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="e227c-119">You can configure your user-level credentials in any app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span> <span data-ttu-id="e227c-120">Independentemente disso, a aplicação que pode configurar estas credenciais, aplica-se aplicações de tooall e para todas as subscrições no seu Azure da conta.</span><span class="sxs-lookup"><span data-stu-id="e227c-120">Regardless in which app you configure these credentials, it applies tooall apps and for all subscriptions in your Azure account.</span></span> 

<span data-ttu-id="e227c-121">tooconfigure as suas credenciais de nível de utilizador:</span><span class="sxs-lookup"><span data-stu-id="e227c-121">tooconfigure your user-level credentials:</span></span>

1. <span data-ttu-id="e227c-122">No Olá [portal do Azure](https://portal.azure.com), clique em do serviço de aplicações >  **&lt;any_app >** > **as credenciais de implementação**.</span><span class="sxs-lookup"><span data-stu-id="e227c-122">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Deployment credentials**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e227c-123">No portal de Olá, tem de ter pelo menos uma aplicação para que possam aceder ao painel de credenciais de implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="e227c-123">In hello portal, you must have at least one app before you can access hello deployment credentials blade.</span></span> <span data-ttu-id="e227c-124">No entanto, com Olá [CLI do Azure](app-service-web-app-azure-resource-manager-xplat-cli.md), pode configurar as credenciais de nível de utilizador sem uma aplicação existente.</span><span class="sxs-lookup"><span data-stu-id="e227c-124">However, with hello [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), you can configure user-level credentials without an existing app.</span></span>

2. <span data-ttu-id="e227c-125">Configurar o nome de utilizador Olá e a palavra-passe e, em seguida, clique em **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e227c-125">Configure hello user name and password, and then click **Save**.</span></span>

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

<span data-ttu-id="e227c-126">Assim que tiver configurado as suas credenciais de implementação, pode encontrar Olá *Git* nome de utilizador de implementação na sua aplicação **descrição geral**,</span><span class="sxs-lookup"><span data-stu-id="e227c-126">Once you have set your deployment credentials, you can find hello *Git* deployment username in your app's **Overview**,</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

<span data-ttu-id="e227c-127">e e *FTP* nome de utilizador de implementação na sua aplicação **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="e227c-127">and and *FTP* deployment username in your app's **Properties**.</span></span>

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> <span data-ttu-id="e227c-128">Azure mostra a palavra-passe de implementação de nível de utilizador.</span><span class="sxs-lookup"><span data-stu-id="e227c-128">Azure does not show your user-level deployment password.</span></span> <span data-ttu-id="e227c-129">Se se esquecer da palavra-passe de Olá, não é possível obtê-lo.</span><span class="sxs-lookup"><span data-stu-id="e227c-129">If you forget hello password, you can't retrieve it.</span></span> <span data-ttu-id="e227c-130">No entanto, pode repor as suas credenciais, seguindo os passos de Olá nesta secção.</span><span class="sxs-lookup"><span data-stu-id="e227c-130">However, you can reset your credentials by following hello steps in this section.</span></span>
>
>  

## <span data-ttu-id="e227c-131"><a name="appscope"></a>Obter e repor as credenciais de nível de aplicação</span><span class="sxs-lookup"><span data-stu-id="e227c-131"><a name="appscope"></a>Get and reset app-level credentials</span></span>
<span data-ttu-id="e227c-132">Para cada aplicação no App Service, as suas credenciais ao nível da aplicação são armazenadas na Olá perfil de publicação de XML.</span><span class="sxs-lookup"><span data-stu-id="e227c-132">For each app in App Service, its app-level credentials are stored in hello XML publish profile.</span></span>

<span data-ttu-id="e227c-133">credenciais do tooget Olá ao nível da aplicação:</span><span class="sxs-lookup"><span data-stu-id="e227c-133">tooget hello app-level credentials:</span></span>

1. <span data-ttu-id="e227c-134">No Olá [portal do Azure](https://portal.azure.com), clique em do serviço de aplicações >  **&lt;any_app >** > **descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="e227c-134">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="e227c-135">Clique em **... Mais** > **perfil de publicação de Get**, e inicia a transferência para um. Ficheiro PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="e227c-135">Click **...More** > **Get publish profile**, and download starts for a .PublishSettings file.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. <span data-ttu-id="e227c-136">Olá aberta. PublishSettings de ficheiros e determinar Olá `<publishProfile>` etiqueta com o atributo de Olá `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="e227c-136">Open hello .PublishSettings file and find hello `<publishProfile>` tag with hello attribute `publishMethod="FTP"`.</span></span> <span data-ttu-id="e227c-137">Em seguida, obter o `userName` e `password` atributos.</span><span class="sxs-lookup"><span data-stu-id="e227c-137">Then, get its `userName` and `password` attributes.</span></span>
<span data-ttu-id="e227c-138">Estas são as credenciais do Olá ao nível da aplicação.</span><span class="sxs-lookup"><span data-stu-id="e227c-138">These are hello app-level credentials.</span></span>

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    <span data-ttu-id="e227c-139">Credenciais de utilizador ao nível do toohello semelhante, o nome de utilizador de implementação de Olá FTP está num formato de Olá de `<app_name>\<username>`, e nome de utilizador de implementação de Git de Olá é apenas `<username>` sem Olá anterior `<app_name>\`.</span><span class="sxs-lookup"><span data-stu-id="e227c-139">Similar toohello user-level credentials, hello FTP deployment username is in hello format of `<app_name>\<username>`, and hello Git deployment username is just `<username>` without hello preceding `<app_name>\`.</span></span>

<span data-ttu-id="e227c-140">credenciais do tooreset Olá ao nível da aplicação:</span><span class="sxs-lookup"><span data-stu-id="e227c-140">tooreset hello app-level credentials:</span></span>

1. <span data-ttu-id="e227c-141">No Olá [portal do Azure](https://portal.azure.com), clique em do serviço de aplicações >  **&lt;any_app >** > **descrição geral**.</span><span class="sxs-lookup"><span data-stu-id="e227c-141">In hello [Azure portal](https://portal.azure.com), click App Service > **&lt;any_app>** > **Overview**.</span></span>

2. <span data-ttu-id="e227c-142">Clique em **... Mais** > **perfil de publicação de reposição**.</span><span class="sxs-lookup"><span data-stu-id="e227c-142">Click **...More** > **Reset publish profile**.</span></span> <span data-ttu-id="e227c-143">Clique em **Sim** tooconfirm Olá repor.</span><span class="sxs-lookup"><span data-stu-id="e227c-143">Click **Yes** tooconfirm hello reset.</span></span>

    <span data-ttu-id="e227c-144">a ação repor Olá invalida qualquer anteriormente transferidos. Ficheiros PublishSettings.</span><span class="sxs-lookup"><span data-stu-id="e227c-144">hello reset action invalidates any previously-downloaded .PublishSettings files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e227c-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e227c-145">Next steps</span></span>

<span data-ttu-id="e227c-146">Saiba como toouse toodeploy estas credenciais a aplicação da [local Git](app-service-deploy-local-git.md) ou utilizando [FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="e227c-146">Find out how toouse these credentials toodeploy your app from [local Git](app-service-deploy-local-git.md) or using [FTP/S](app-service-deploy-ftp.md).</span></span>
