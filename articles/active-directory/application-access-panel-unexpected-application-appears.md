---
title: "aplicações de aaaHow aparecem no painel de acesso de Olá | Microsoft Docs"
description: "Resolver problemas com a razão pela qual uma aplicação é apresentados no painel de acesso de Olá"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewr: japere
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="74ad0-103">Como as aplicações são apresentadas no painel de acesso de Olá</span><span class="sxs-lookup"><span data-stu-id="74ad0-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="74ad0-104">Olá painel de acesso é um portal baseado na web que permite que um utilizador com um trabalho ou conta de escolares no Azure Active Directory (Azure AD) tooview início baseado na nuvem aplicações e esse Olá administrador do Azure AD concedeu-lhes acesso a.</span><span class="sxs-lookup"><span data-stu-id="74ad0-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="74ad0-105">Estas aplicações estão configuradas em nome de utilizador de Olá no portal do Azure AD Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="74ad0-106">Olá, admin pode aprovisionar utilizador de Olá aplicação toohello diretamente ou grupo tooa que um utilizador faz parte de resultando na aplicação Olá, volte a aparecer no painel de acesso do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="74ad0-107">Geral emite toocheck pela primeira vez</span><span class="sxs-lookup"><span data-stu-id="74ad0-107">General issues toocheck first</span></span>

-   <span data-ttu-id="74ad0-108">Se uma aplicação apenas foi removida de um utilizador ou grupo Olá utilizador seja um membro, tente toosign e terminar novamente no painel de acesso do utilizador Olá após alguns minutos toosee se Olá aplicação for removida.</span><span class="sxs-lookup"><span data-stu-id="74ad0-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="74ad0-109">Se uma licença apenas tiver sido removida de um utilizador ou o utilizador de Olá de grupo é que um membro deste processo poderá demorar muito tempo, dependendo do tamanho de Olá e complexidade do grupo Olá toobe as alterações efetuada.</span><span class="sxs-lookup"><span data-stu-id="74ad0-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="74ad0-110">Permitir tempo adicional antes de iniciar sessão Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="74ad0-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="74ad0-111">Problemas relacionados tooassigning aplicações toousers</span><span class="sxs-lookup"><span data-stu-id="74ad0-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="74ad0-112">Um utilizador pode estar a ver uma aplicação no respetivo painel de acesso porque estes tinham sido anteriormente atribuídos tooit.</span><span class="sxs-lookup"><span data-stu-id="74ad0-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="74ad0-113">Seguem-se algumas toocheck formas:</span><span class="sxs-lookup"><span data-stu-id="74ad0-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="74ad0-114">Certifique-se um utilizador atribuído toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="74ad0-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="74ad0-115">Verifique se um utilizador com uma licença relacionada com a aplicação de toohello</span><span class="sxs-lookup"><span data-stu-id="74ad0-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="74ad0-116">Certifique-se um utilizador atribuído toohello aplicação</span><span class="sxs-lookup"><span data-stu-id="74ad0-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="74ad0-117">toocheck se um utilizador for atribuído toohello aplicação, siga os passos de Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="74ad0-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="74ad0-118">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="74ad0-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="74ad0-119">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="74ad0-120">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="74ad0-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="74ad0-121">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="74ad0-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="74ad0-122">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="74ad0-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="74ad0-123">**Pesquisa** Olá nome da aplicação Olá em questão.</span><span class="sxs-lookup"><span data-stu-id="74ad0-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="74ad0-124">Clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="74ad0-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="74ad0-125">Verifique toosee se o utilizador está atribuído toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="74ad0-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="74ad0-126">Se pretender que o utilizador de Olá tooremove da aplicação Olá, **clique Olá linha** do utilizador Olá e selecione **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="74ad0-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="74ad0-127">Verifique se um utilizador com uma licença relacionada com a aplicação de toohello</span><span class="sxs-lookup"><span data-stu-id="74ad0-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="74ad0-128">toocheck um utilizador atribuído licenças, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="74ad0-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="74ad0-129">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="74ad0-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="74ad0-130">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="74ad0-131">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="74ad0-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="74ad0-132">Clique em **utilizadores e grupos** no menu de navegação de Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="74ad0-133">Clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="74ad0-133">click **All users**.</span></span>

6.  <span data-ttu-id="74ad0-134">**Pesquisa** para utilizador Olá que está interessado e **clique Olá linha** tooselect.</span><span class="sxs-lookup"><span data-stu-id="74ad0-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="74ad0-135">Clique em **licenças** toosee que licenças Olá atualmente atribuída utilizador.</span><span class="sxs-lookup"><span data-stu-id="74ad0-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="74ad0-136">Se o utilizador Olá está atribuído a licença do Office tooan isto ativar tooappear de aplicações do Office de terceiros primeiro no Olá painel de acesso do utilizador.</span><span class="sxs-lookup"><span data-stu-id="74ad0-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="74ad0-137">Problemas relacionados tooassigning aplicações toogroups</span><span class="sxs-lookup"><span data-stu-id="74ad0-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="74ad0-138">Um utilizador pode estar a ver uma aplicação no respetivo painel de acesso porque fazem parte de um grupo que tenha sido atribuído aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="74ad0-139">Seguem-se algumas toocheck formas:</span><span class="sxs-lookup"><span data-stu-id="74ad0-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="74ad0-140">Verifique as associações de grupo do utilizador</span><span class="sxs-lookup"><span data-stu-id="74ad0-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="74ad0-141">Verifique se um utilizador for um membro de um grupo atribuído tooa licença</span><span class="sxs-lookup"><span data-stu-id="74ad0-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="74ad0-142">Verifique as associações de grupo do utilizador</span><span class="sxs-lookup"><span data-stu-id="74ad0-142">Check a user’s group memberships</span></span>

<span data-ttu-id="74ad0-143">toocheck associação a um grupo, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="74ad0-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="74ad0-144">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="74ad0-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="74ad0-145">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="74ad0-146">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="74ad0-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="74ad0-147">Clique em **utilizadores e grupos** no menu de navegação de Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="74ad0-148">Clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="74ad0-148">click **All users**.</span></span>

6.  <span data-ttu-id="74ad0-149">**Pesquisa** para utilizador Olá que está interessado e **clique Olá linha** tooselect.</span><span class="sxs-lookup"><span data-stu-id="74ad0-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="74ad0-150">Clique em **grupos.**</span><span class="sxs-lookup"><span data-stu-id="74ad0-150">click **Groups.**</span></span>

8.  <span data-ttu-id="74ad0-151">Verifique toosee se o utilizador for parte de uma aplicação de toohello do grupo atribuído.</span><span class="sxs-lookup"><span data-stu-id="74ad0-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="74ad0-152">Se pretender que o utilizador de Olá tooremove do grupo de Olá **clique Olá linha** do grupo de Olá e selecione eliminar.</span><span class="sxs-lookup"><span data-stu-id="74ad0-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="74ad0-153">Verifique se um utilizador for um membro de um grupo atribuído tooa licença</span><span class="sxs-lookup"><span data-stu-id="74ad0-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="74ad0-154">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="74ad0-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="74ad0-155">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="74ad0-156">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="74ad0-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="74ad0-157">Clique em **utilizadores e grupos** no menu de navegação de Olá.</span><span class="sxs-lookup"><span data-stu-id="74ad0-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="74ad0-158">Clique em **todos os utilizadores**.</span><span class="sxs-lookup"><span data-stu-id="74ad0-158">click **All users**.</span></span>

6.  <span data-ttu-id="74ad0-159">**Pesquisa** para utilizador Olá que está interessado e **clique Olá linha** tooselect.</span><span class="sxs-lookup"><span data-stu-id="74ad0-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="74ad0-160">Clique em **grupos.**</span><span class="sxs-lookup"><span data-stu-id="74ad0-160">click **Groups.**</span></span>

8.  <span data-ttu-id="74ad0-161">Clique em linha Olá de um grupo específico.</span><span class="sxs-lookup"><span data-stu-id="74ad0-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="74ad0-162">Clique em **licenças** toosee tooit atribuído com o grupo de Olá de licenças.</span><span class="sxs-lookup"><span data-stu-id="74ad0-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="74ad0-163">Se o grupo de Olá está atribuído a licença do Office tooan que isto poderá ativar determinada tooappear de aplicações do Office de terceiros primeiro no Olá painel de acesso do utilizador.</span><span class="sxs-lookup"><span data-stu-id="74ad0-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="74ad0-164">Se estes passos de resolução de problemas não Olá resolver o problema de Olá</span><span class="sxs-lookup"><span data-stu-id="74ad0-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="74ad0-165">Abra um pedido de suporte com Olá se disponíveis os seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="74ad0-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="74ad0-166">ID de correlação de erro</span><span class="sxs-lookup"><span data-stu-id="74ad0-166">Correlation error ID</span></span>

-   <span data-ttu-id="74ad0-167">UPN (endereço de e-mail do utilizador)</span><span class="sxs-lookup"><span data-stu-id="74ad0-167">UPN (user email address)</span></span>

-   <span data-ttu-id="74ad0-168">ID do inquilino</span><span class="sxs-lookup"><span data-stu-id="74ad0-168">Tenant ID</span></span>

-   <span data-ttu-id="74ad0-169">Tipo de browser</span><span class="sxs-lookup"><span data-stu-id="74ad0-169">Browser type</span></span>

-   <span data-ttu-id="74ad0-170">Fuso horário e tempo/período de tempo durante o erro ocorre</span><span class="sxs-lookup"><span data-stu-id="74ad0-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="74ad0-171">Rastreios de fiddler</span><span class="sxs-lookup"><span data-stu-id="74ad0-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="74ad0-172">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="74ad0-172">Next steps</span></span>
[<span data-ttu-id="74ad0-173">Gestão de aplicações com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74ad0-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
