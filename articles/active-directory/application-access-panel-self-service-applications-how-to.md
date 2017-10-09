---
title: "acesso de aplicação personalizada aaaHow toouse | Microsoft Docs"
description: "Ativar o acesso de aplicação personalizada tooallow toofind de utilizadores as suas próprias aplicações"
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
ms.reviewer: japere
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="a4340-103">Como aceder a aplicações de self-service toouse</span><span class="sxs-lookup"><span data-stu-id="a4340-103">How toouse self-service application access</span></span>

<span data-ttu-id="a4340-104">Antes dos utilizadores Self-podem detetar as aplicações a partir do respetivo painel de acesso, terá de tooenable **acesso à aplicação self-service** aplicações tooany pretende tooallow utilizadores tooself-detetar e pedir acesso para.</span><span class="sxs-lookup"><span data-stu-id="a4340-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="a4340-105">Esta funcionalidade é uma excelente forma de toosave tempo e dinheiro como um grupo de TI e é altamente recomendada como parte de uma implementação de aplicações modernas com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4340-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="a4340-106">Utilizar esta funcionalidade, pode:</span><span class="sxs-lookup"><span data-stu-id="a4340-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="a4340-107">Permitir que os utilizadores Self-detetar as aplicações de Olá [painel de acesso de aplicação](https://myapps.microsoft.com/) sem bothering Olá IT grupo.</span><span class="sxs-lookup"><span data-stu-id="a4340-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="a4340-108">Adicione esses grupo de pré-configurado de tooa de utilizadores para que possa ver quem tiver solicitado acesso, remover o acesso e gerir funções de Olá atribuídas toothem.</span><span class="sxs-lookup"><span data-stu-id="a4340-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="a4340-109">Opcionalmente, permitir que um aprovador empresarial pedidos de acesso de aplicação tooapprove pelo Olá grupo TI não tem.</span><span class="sxs-lookup"><span data-stu-id="a4340-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="a4340-110">Opcionalmente, configure cópias de segurança too10 se a indivíduos que podem aprovar acesso toothis aplicação.</span><span class="sxs-lookup"><span data-stu-id="a4340-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="a4340-111">Opcionalmente, permitir que um aprovador empresarial palavras-passe do tooset Olá esses utilizadores podem utilizar toosign na aplicação toohello, diretamente a partir do aprovador de negócio a Olá [painel de acesso de aplicação](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a4340-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="a4340-112">Opcionalmente, automaticamente diretamente a atribuir a função de aplicação de tooan de utilizadores atribuídos self-service.</span><span class="sxs-lookup"><span data-stu-id="a4340-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="a4340-113">Ativar o acesso de aplicação personalizada tooallow toofind de utilizadores as suas próprias aplicações</span><span class="sxs-lookup"><span data-stu-id="a4340-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="a4340-114">Acesso de aplicação personalizada é tooself de utilizadores de tooallow uma excelente forma-detetar aplicações, opcionalmente, permitir Olá negócio tooapprove acesso grupo toothose aplicações.</span><span class="sxs-lookup"><span data-stu-id="a4340-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="a4340-115">Pode permitir que as credenciais grupo Olá negócio toomanage Olá atribuído toothose utilizadores para a direita da palavra-passe de início de sessão único em aplicações da respetiva painéis de acesso.</span><span class="sxs-lookup"><span data-stu-id="a4340-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="a4340-116">aplicação de tooan de acesso por aplicação self-service tooenable, siga Olá passos abaixo:</span><span class="sxs-lookup"><span data-stu-id="a4340-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a4340-117">Abra Olá [ **Portal do Azure** ](https://portal.azure.com/) e inicie sessão como um **Administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="a4340-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a4340-118">Abra Olá **extensão do Active Directory do Azure** clicando **mais serviços** em Olá parte inferior do menu de navegação esquerda principal Olá.</span><span class="sxs-lookup"><span data-stu-id="a4340-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a4340-119">Escreva **"do Azure Active Directory**" na caixa de pesquisa de filtro de Olá e selecione Olá **do Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a4340-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a4340-120">Clique em **aplicações empresariais** do menu de navegação esquerdo do Olá do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a4340-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a4340-121">Clique em **todas as aplicações** tooview uma lista de todas as suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="a4340-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a4340-122">Se não vir aplicação Olá que pretende mostrar aqui, utilize Olá **filtro** controlo, Olá parte superior do Olá **todas as aplicações lista** e conjunto Olá **mostrar** opção demasiado **Todas as aplicações.**</span><span class="sxs-lookup"><span data-stu-id="a4340-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a4340-123">Selecione aplicação Olá pretende tooenable self-service access toofrom Olá List, lista.</span><span class="sxs-lookup"><span data-stu-id="a4340-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="a4340-124">Quando carrega a aplicação Olá, clique em **self-service** do menu de navegação esquerdo da aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="a4340-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a4340-125">tooenable acesso a aplicações de self-service para esta aplicação, ative Olá **permitir que os utilizadores a aplicação do toorequest acesso toothis?** alternar demasiado**Sim.**</span><span class="sxs-lookup"><span data-stu-id="a4340-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="a4340-126">Em seguida, tooselect Olá grupo toowhich os utilizadores que pedem acesso toothis aplicações devem ser adicionadas, clique em etiqueta de toohello seguinte Seletor Olá **toowhich grupo deve ser atribuído aos utilizadores adicionar?** e selecione um grupo.</span><span class="sxs-lookup"><span data-stu-id="a4340-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="a4340-127">**Opcional:** se quiser toorequire uma aprovação de negócio antes dos utilizadores têm permissão de acesso, defina Olá **exigir a aprovação antes de conceder acesso toothis aplicação?** alternar demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="a4340-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="a4340-128">**Opcional: para aplicações utilizando a palavra-passe início de sessão único em apenas,** se desejar tooallow essas empresas aprovadores toospecify Olá palavras-passe que são enviadas toothis aplicação para os utilizadores aprovados, defina Olá **permitir aprovadores tooset palavras-passe do utilizador para esta aplicação?**  alternar demasiado**Sim**.</span><span class="sxs-lookup"><span data-stu-id="a4340-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="a4340-129">**Opcional:** aprovadores de negócio de Olá toospecify autorizados tooapprove aplicação de toothis de acesso, clique em etiqueta de toohello seguinte Seletor Olá **que é permitida a aplicação do tooapprove acesso toothis?** tooselect cópias de segurança too10 aprovadores de negócio individuais.</span><span class="sxs-lookup"><span data-stu-id="a4340-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="a4340-130">Não são suportados grupos.</span><span class="sxs-lookup"><span data-stu-id="a4340-130">Groups are not supported.</span></span>

13. <span data-ttu-id="a4340-131">**Opcional:** **para aplicações que expõem funções**, se assim o desejar a função de tooa do tooassign utilizadores aprovados self-service, clique em Olá Seletor seguinte toohello **toowhich função devem ser atribuído aos utilizadores deste aplicação?**  tooselect Olá função toowhich devem ser atribuídos estes utilizadores.</span><span class="sxs-lookup"><span data-stu-id="a4340-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="a4340-132">Clique em Olá **guardar** botão, Olá parte superior do Olá painel toofinish.</span><span class="sxs-lookup"><span data-stu-id="a4340-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="a4340-133">Depois de concluir a configuração da aplicação de self-service, os utilizadores podem navegar tootheir [painel de acesso de aplicação](https://myapps.microsoft.com/) e clique em Olá **+ adicionar** botão toofind Olá aplicações toowhich tiver ativado Acesso de self-service.</span><span class="sxs-lookup"><span data-stu-id="a4340-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="a4340-134">Aprovadores negócio também veem uma notificação no respetivo [painel de acesso de aplicação](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a4340-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="a4340-135">Pode ativar uma mensagem de e-mail a indicar quando um utilizador pediu a aplicação de tooan de acesso que requer a sua aprovação.</span><span class="sxs-lookup"><span data-stu-id="a4340-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="a4340-136">Estas aprovações suportam aprovação único fluxos de trabalho apenas, que significa que, se especificar vários aprovadores, qualquer aprovador único pode aprovar acesso toohello aplicação.</span><span class="sxs-lookup"><span data-stu-id="a4340-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4340-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a4340-137">Next steps</span></span>
[<span data-ttu-id="a4340-138">Configurar o Azure Active Directory para gestão de grupos self-service</span><span class="sxs-lookup"><span data-stu-id="a4340-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
