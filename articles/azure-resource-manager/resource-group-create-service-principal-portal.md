---
title: "aaaCreate identidade da aplicação do Azure no portal | Microsoft Docs"
description: "Descreve como toocreate uma nova aplicação do Azure Active Directory e que podem ser utilizados com controlo de acesso baseado em funções de Olá no Azure Resource Manager toomanage principal de serviço tooresources de acesso."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="f4d80-103">Utilizar o portal toocreate uma aplicação do Azure Active Directory e o principal de serviço que pode aceder a recursos</span><span class="sxs-lookup"><span data-stu-id="f4d80-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="f4d80-104">Quando tiver uma aplicação que necessita de tooaccess ou modificar recursos, tem de configurar uma aplicação do Azure Active Directory (AD) e atribuir tooit de permissões de Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="f4d80-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="f4d80-105">Esta abordagem é preferível toorunning Olá aplicação com as suas próprias credenciais porque:</span><span class="sxs-lookup"><span data-stu-id="f4d80-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="f4d80-106">Pode atribuir permissões de identidade de aplicação toohello diferentes a suas própria permissões.</span><span class="sxs-lookup"><span data-stu-id="f4d80-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="f4d80-107">Normalmente, estas permissões são tooexactly restrito tem de aplicação que Olá toodo.</span><span class="sxs-lookup"><span data-stu-id="f4d80-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="f4d80-108">Não dispõe de credenciais da aplicação Olá toochange se alterar as suas responsabilidades.</span><span class="sxs-lookup"><span data-stu-id="f4d80-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="f4d80-109">Pode utilizar uma autenticação de certificados de tooautomate ao executar um script automático.</span><span class="sxs-lookup"><span data-stu-id="f4d80-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="f4d80-110">Este tópico mostra como tooperform os passos através do portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="f4d80-111">Concentra-se uma aplicação do inquilino único em que a aplicação Olá é toorun pretendido dentro da organização apenas um.</span><span class="sxs-lookup"><span data-stu-id="f4d80-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="f4d80-112">Normalmente utiliza aplicações de inquilino único para aplicações de linha de negócio que são executadas dentro da sua organização.</span><span class="sxs-lookup"><span data-stu-id="f4d80-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="f4d80-113">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="f4d80-113">Required permissions</span></span>
<span data-ttu-id="f4d80-114">toocomplete neste tópico, tem de ter uma aplicação de tooregister de permissões suficientes com o seu inquilino do Azure AD e atribuir a função de tooa Olá aplicações na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="f4d80-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="f4d80-115">Vamos certificar-se de que ter Olá permissões corretas tooperform esses passos.</span><span class="sxs-lookup"><span data-stu-id="f4d80-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="f4d80-116">Verifique as permissões do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4d80-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="f4d80-117">Inicie sessão no tooyour conta do Azure através de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4d80-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4d80-118">Selecione **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-118">Select **Azure Active Directory**.</span></span>

     ![Selecione do azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="f4d80-120">No Azure Active Directory, selecione **as definições de utilizador**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-120">In Azure Active Directory, select **User settings**.</span></span>

     ![Selecione as definições de utilizador](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="f4d80-122">Verifique Olá **registos de aplicação** definição.</span><span class="sxs-lookup"><span data-stu-id="f4d80-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="f4d80-123">Se definido demasiado**Sim**, os utilizadores que não podem registar aplicações AD.</span><span class="sxs-lookup"><span data-stu-id="f4d80-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="f4d80-124">Esta definição significa que qualquer utilizador no inquilino do Azure AD Olá pode registar uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="f4d80-125">Para poder continuar demasiado[permissões de subscrição do Azure verifique](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="f4d80-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![registos de aplicação de vista](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="f4d80-127">Se os registos de aplicação Olá definição estiver definido demasiado**não**, apenas os utilizadores administradores podem registar aplicações.</span><span class="sxs-lookup"><span data-stu-id="f4d80-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="f4d80-128">É necessário toocheck se a sua conta é um administrador inquilino do Azure AD Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="f4d80-129">Selecione **descrição geral** e **localizar um utilizador** de tarefas rápidas.</span><span class="sxs-lookup"><span data-stu-id="f4d80-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Localizar utilizador](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="f4d80-131">Pesquisa para a sua conta e selecioná-lo quando a encontrá-lo.</span><span class="sxs-lookup"><span data-stu-id="f4d80-131">Search for your account, and select it when you find it.</span></span>

     ![utilizador de pesquisa](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="f4d80-133">Para a sua conta, selecione **função de diretório**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-133">For your account, select **Directory role**.</span></span> 

     ![função de diretório](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="f4d80-135">Ver a sua função de diretório atribuído no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4d80-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="f4d80-136">Se a conta está atribuída a função de utilizador toohello, mas hello registo definição de aplicação (Olá precedente passos) é limitado tooadmin utilizadores, peça ao seu administrador tooeither atribuir tooan função de administrador ou tooenable utilizadores tooregister aplicações.</span><span class="sxs-lookup"><span data-stu-id="f4d80-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![função de vista](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="f4d80-138">Verifique as permissões de subscrição do Azure</span><span class="sxs-lookup"><span data-stu-id="f4d80-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="f4d80-139">Na sua subscrição do Azure, a conta tem de ter `Microsoft.Authorization/*/Write` tooassign uma função do AD aplicação tooa de acesso.</span><span class="sxs-lookup"><span data-stu-id="f4d80-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="f4d80-140">Esta ação é concedida através de Olá [proprietário](../active-directory/role-based-access-built-in-roles.md#owner) função ou [administrador de acesso de utilizador](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) função.</span><span class="sxs-lookup"><span data-stu-id="f4d80-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="f4d80-141">Se a sua conta está atribuída toohello **contribuinte** função, não tem permissão suficiente.</span><span class="sxs-lookup"><span data-stu-id="f4d80-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="f4d80-142">Receberá um erro durante a tentativa de função de principal tooa de serviço de Olá tooassign.</span><span class="sxs-lookup"><span data-stu-id="f4d80-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="f4d80-143">toocheck as permissões de subscrição:</span><span class="sxs-lookup"><span data-stu-id="f4d80-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="f4d80-144">Se não já pretender na sua conta do Azure AD de Olá precedente passos, selecione **do Azure Active Directory** a partir do painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="f4d80-145">Localize a conta do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4d80-145">Find your Azure AD account.</span></span> <span data-ttu-id="f4d80-146">Selecione **descrição geral** e **localizar um utilizador** de tarefas rápidas.</span><span class="sxs-lookup"><span data-stu-id="f4d80-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![Localizar utilizador](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="f4d80-148">Pesquisa para a sua conta e selecioná-lo quando a encontrá-lo.</span><span class="sxs-lookup"><span data-stu-id="f4d80-148">Search for your account, and select it when you find it.</span></span>

     ![utilizador de pesquisa](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="f4d80-150">Selecione **recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-150">Select **Azure resources**.</span></span>

     ![Selecione recursos](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="f4d80-152">Ver as funções atribuídas e determinar se tem permissões adequadas tooassign uma função do AD aplicação tooa.</span><span class="sxs-lookup"><span data-stu-id="f4d80-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="f4d80-153">Se não, peça ao seu tooadd de administrador de subscrição tooUser acesso função de administrador.</span><span class="sxs-lookup"><span data-stu-id="f4d80-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="f4d80-154">Olá seguinte imagem, utilizador de Olá é atribuído toohello função de proprietário para duas subscrições, que significa que o utilizador tem permissões adequadas.</span><span class="sxs-lookup"><span data-stu-id="f4d80-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![Mostrar permissões](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="f4d80-156">Criar uma aplicação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4d80-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="f4d80-157">Inicie sessão no tooyour conta do Azure através de Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4d80-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f4d80-158">Selecione **do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-158">Select **Azure Active Directory**.</span></span>

     ![Selecione do azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="f4d80-160">Selecione **registos de aplicação**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-160">Select **App registrations**.</span></span>   

     ![Selecione os registos de aplicação](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="f4d80-162">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-162">Select **Add**.</span></span>

     ![Adicionar aplicação](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="f4d80-164">Forneça um nome e o URL para a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="f4d80-165">Selecione **aplicação Web / API** ou **nativo** para o tipo de Olá da aplicação que pretende toocreate.</span><span class="sxs-lookup"><span data-stu-id="f4d80-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="f4d80-166">Depois de definir valores de Olá, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-166">After setting hello values, select **Create**.</span></span>

     ![aplicação de nome](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="f4d80-168">Foi criada com a aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="f4d80-169">Obter a chave de autenticação e ID de aplicação</span><span class="sxs-lookup"><span data-stu-id="f4d80-169">Get application ID and authentication key</span></span>
<span data-ttu-id="f4d80-170">Quando programaticamente iniciar sessão, precisa de Olá ID para a sua aplicação e uma chave de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="f4d80-171">tooget os valores, Olá utilize os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="f4d80-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="f4d80-172">De **registos de aplicação** no Azure Active Directory, selecione a aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![Selecionar aplicação](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="f4d80-174">Olá cópia **ID da aplicação** e armazená-las no código da aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="f4d80-175">Olá aplicações no Olá [aplicações de exemplo](#sample-applications) secção Consulte toothis valor como id de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![id de cliente](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="f4d80-177">toogenerate uma chave de autenticação, selecione **chaves**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![Selecione as chaves](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="f4d80-179">Forneça uma descrição da chave de Olá e uma duração para a chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="f4d80-180">Quando terminar, selecione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-180">When done, select **Save**.</span></span>

     ![Guardar chave](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="f4d80-182">Depois de guardar a chave de Olá, é apresentado o valor de Olá da chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="f4d80-183">Copie este valor, porque não é capaz de tooretrieve chave de Olá mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f4d80-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="f4d80-184">Forneça o valor de chave de Olá com toolog de ID de aplicação Olá na como aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="f4d80-185">Armazenar o valor de chave olá onde a aplicação pode obtê-lo.</span><span class="sxs-lookup"><span data-stu-id="f4d80-185">Store hello key value where your application can retrieve it.</span></span>

     ![guardar a chave](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="f4d80-187">Obter ID de inquilino</span><span class="sxs-lookup"><span data-stu-id="f4d80-187">Get tenant ID</span></span>
<span data-ttu-id="f4d80-188">Quando programaticamente iniciar sessão, terá de ID do inquilino toopass Olá com o seu pedido de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="f4d80-189">ID do inquilino Olá tooget, selecione **propriedades** para o seu inquilino do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4d80-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![selecionar propriedades do Azure AD](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="f4d80-191">Olá cópia **ID de diretório**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="f4d80-192">Este valor é o ID do inquilino.</span><span class="sxs-lookup"><span data-stu-id="f4d80-192">This value is your tenant ID.</span></span>

     ![id do inquilino](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="f4d80-194">Atribuir toorole de aplicação</span><span class="sxs-lookup"><span data-stu-id="f4d80-194">Assign application toorole</span></span>
<span data-ttu-id="f4d80-195">tooaccess recursos na sua subscrição, tem de atribuir função de tooa Olá aplicações.</span><span class="sxs-lookup"><span data-stu-id="f4d80-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="f4d80-196">Decida qual a função representa permissões corretas de Olá para aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="f4d80-197">toolearn sobre as funções disponíveis Olá, consulte [RBAC: funções incorporadas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f4d80-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="f4d80-198">Pode definir o âmbito de Olá ao nível de Olá de subscrição de Olá, grupo de recursos ou recursos.</span><span class="sxs-lookup"><span data-stu-id="f4d80-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="f4d80-199">As permissões são herdadas toolower níveis de âmbito.</span><span class="sxs-lookup"><span data-stu-id="f4d80-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="f4d80-200">Por exemplo, a adição de que uma função de leitor de toohello de aplicação para um grupo de recursos, significa pode ler o grupo de recursos de Olá e quaisquer recursos que nele contidos.</span><span class="sxs-lookup"><span data-stu-id="f4d80-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="f4d80-201">Navegue toohello nível do âmbito de que aplicação Olá tooassign desejar.</span><span class="sxs-lookup"><span data-stu-id="f4d80-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="f4d80-202">Por exemplo, tooassign Selecione uma função no âmbito de subscrição de Olá, **subscrições**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="f4d80-203">Em vez disso, pode selecionar um grupo de recursos ou um recurso.</span><span class="sxs-lookup"><span data-stu-id="f4d80-203">You could instead select a resource group or resource.</span></span>

     ![Selecione a subscrição](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="f4d80-205">Selecione Olá determinada subscrição (grupo de recursos ou recursos) tooassign Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![Selecione a subscrição de atribuição](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="f4d80-207">Selecione **(IAM) do controlo de acesso**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-207">Select **Access Control (IAM)**.</span></span>

     ![Selecione o acesso](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="f4d80-209">Selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f4d80-209">Select **Add**.</span></span>

     ![Selecionar adicionar](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="f4d80-211">Selecione a função de Olá desejar tooassign toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="f4d80-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="f4d80-212">Olá imagem seguinte mostra Olá **leitor** função.</span><span class="sxs-lookup"><span data-stu-id="f4d80-212">hello following image shows hello **Reader** role.</span></span>

     ![Selecione a função](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="f4d80-214">Procure a aplicação e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="f4d80-214">Search for your application, and select it.</span></span>

     ![Procure a aplicação](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="f4d80-216">Selecione **OK** toofinish atribuir função Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="f4d80-217">Verá a aplicação na lista de Olá de utilizadores atribuídos tooa função para esse âmbito.</span><span class="sxs-lookup"><span data-stu-id="f4d80-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="f4d80-218">Inicie sessão como uma aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="f4d80-218">Log in as hello application</span></span>

<span data-ttu-id="f4d80-219">A aplicação está agora definida no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4d80-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="f4d80-220">Tem um ID e a chave toouse para iniciar sessão como aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="f4d80-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="f4d80-221">aplicação Olá é atribuída a função de tooa que concede-lhe determinadas ações que pode realizar.</span><span class="sxs-lookup"><span data-stu-id="f4d80-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="f4d80-222">Para informações sobre como iniciar sessão como uma aplicação Olá através de plataformas diferentes, consulte:</span><span class="sxs-lookup"><span data-stu-id="f4d80-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="f4d80-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4d80-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="f4d80-224">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f4d80-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="f4d80-225">REST</span><span class="sxs-lookup"><span data-stu-id="f4d80-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="f4d80-226">.NET</span><span class="sxs-lookup"><span data-stu-id="f4d80-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="f4d80-227">Java</span><span class="sxs-lookup"><span data-stu-id="f4d80-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="f4d80-228">Node.js</span><span class="sxs-lookup"><span data-stu-id="f4d80-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="f4d80-229">Python</span><span class="sxs-lookup"><span data-stu-id="f4d80-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="f4d80-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="f4d80-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="f4d80-231">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f4d80-231">Next steps</span></span>
* <span data-ttu-id="f4d80-232">tooset se uma aplicação multi-inquilino, consulte [tooauthorization do Guia do programador com Olá API do Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f4d80-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="f4d80-233">toolearn sobre como especificar políticas de segurança, consulte [controlo de acesso baseado em funções do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f4d80-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="f4d80-234">Para obter uma lista de ações disponíveis que pode ser concedeu ou negou toousers, consulte [operações de fornecedor de recursos do Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f4d80-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
