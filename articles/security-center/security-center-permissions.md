---
title: "aaaPermissions no Centro de segurança do Azure | Microsoft Docs"
description: "Este artigo explica como o Centro de segurança do Azure utiliza o controlo de acesso baseado em funções tooassign toousers de permissões e identifica Olá permitida ações para cada função."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a><span data-ttu-id="c9711-103">Permissões no Centro de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c9711-103">Permissions in Azure Security Center</span></span>

<span data-ttu-id="c9711-104">Centro de segurança do Azure utiliza [controlo de acesso baseado em funções (RBAC)](../active-directory/role-based-access-control-configure.md), que fornece [funções incorporadas](../active-directory/role-based-access-built-in-roles.md) que podem ser atribuídas toousers, grupos e serviços no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9711-104">Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned toousers, groups, and services in Azure.</span></span>

<span data-ttu-id="c9711-105">Centro de segurança avalia configuração Olá dos problemas de segurança de tooidentify de recursos e vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="c9711-105">Security Center assesses hello configuration of your resources tooidentify security issues and vulnerabilities.</span></span> <span data-ttu-id="c9711-106">No Centro de segurança, verá apenas as informações relacionadas com recursos tooa quando são atribuídos função Olá de proprietário, Contribuidor ou leitor para Olá subscrição ou grupo de recursos que um recurso pertence.</span><span class="sxs-lookup"><span data-stu-id="c9711-106">In Security Center, you only see information related tooa resource when you are assigned hello role of Owner, Contributor, or Reader for hello subscription or resource group that a resource belongs to.</span></span>

<span data-ttu-id="c9711-107">Funções de toothese de adição, existem duas funções específicas do Centro de segurança:</span><span class="sxs-lookup"><span data-stu-id="c9711-107">In addition toothese roles, there are two specific Security Center roles:</span></span>

* <span data-ttu-id="c9711-108">**Leitor de segurança**: um utilizador que pertence toothis função tem de ver direitos tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="c9711-108">**Security Reader**: A user that belongs toothis role has viewing rights tooSecurity Center.</span></span> <span data-ttu-id="c9711-109">utilizador Olá pode ver as recomendações, alertas, uma política de segurança e Estados de segurança, mas não é possível efetuar alterações.</span><span class="sxs-lookup"><span data-stu-id="c9711-109">hello user can view recommendations, alerts, a security policy, and security states, but cannot make changes.</span></span>
* <span data-ttu-id="c9711-110">**Administrador de segurança**: um utilizador que pertence a função de toothis tem Olá mesmo direitos como Olá leitor de segurança e pode também atualizar a política de segurança de Olá e dispensar alertas e recomendações.</span><span class="sxs-lookup"><span data-stu-id="c9711-110">**Security Administrator**: A user that belongs toothis role has hello same rights as hello Security Reader and can also update hello security policy and dismiss alerts and recommendations.</span></span>

> [!NOTE]
> <span data-ttu-id="c9711-111">funções de segurança de Olá, leitor de segurança e administrador de segurança, tem acesso apenas no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="c9711-111">hello security roles, Security Reader and Security Administrator, have access only in Security Center.</span></span> <span data-ttu-id="c9711-112">funções de segurança de Olá não têm acesso tooother serviço áreas do Azure como armazenamento, Web & Mobile ou Internet das coisas.</span><span class="sxs-lookup"><span data-stu-id="c9711-112">hello security roles do not have access tooother service areas of Azure such as Storage, Web & Mobile, or Internet of Things.</span></span>
>
>

## <a name="roles-and-allowed-actions"></a><span data-ttu-id="c9711-113">Funções e as ações permitidas</span><span class="sxs-lookup"><span data-stu-id="c9711-113">Roles and allowed actions</span></span>

<span data-ttu-id="c9711-114">Olá tabela seguinte apresenta as funções e permitido ações no Centro de segurança.</span><span class="sxs-lookup"><span data-stu-id="c9711-114">hello following table displays roles and allowed actions in Security Center.</span></span> <span data-ttu-id="c9711-115">Um X indica que a ação de Olá é permitida para essa função.</span><span class="sxs-lookup"><span data-stu-id="c9711-115">An X indicates that hello action is allowed for that role.</span></span>

| <span data-ttu-id="c9711-116">Função</span><span class="sxs-lookup"><span data-stu-id="c9711-116">Role</span></span> | <span data-ttu-id="c9711-117">Editar política de segurança</span><span class="sxs-lookup"><span data-stu-id="c9711-117">Edit security policy</span></span> | <span data-ttu-id="c9711-118">Aplicar as recomendações de segurança para um recurso</span><span class="sxs-lookup"><span data-stu-id="c9711-118">Apply security recommendations for a resource</span></span> | <span data-ttu-id="c9711-119">Dispensar alertas e recomendações</span><span class="sxs-lookup"><span data-stu-id="c9711-119">Dismiss alerts and recommendations</span></span> | <span data-ttu-id="c9711-120">Ver alertas e recomendações</span><span class="sxs-lookup"><span data-stu-id="c9711-120">View alerts and recommendations</span></span> |
|:--- |:---:|:---:|:---:|:---:|
| <span data-ttu-id="c9711-121">Proprietário da subscrição</span><span class="sxs-lookup"><span data-stu-id="c9711-121">Subscription Owner</span></span> | <span data-ttu-id="c9711-122">X</span><span class="sxs-lookup"><span data-stu-id="c9711-122">X</span></span> | <span data-ttu-id="c9711-123">X</span><span class="sxs-lookup"><span data-stu-id="c9711-123">X</span></span> | <span data-ttu-id="c9711-124">X</span><span class="sxs-lookup"><span data-stu-id="c9711-124">X</span></span> | <span data-ttu-id="c9711-125">X</span><span class="sxs-lookup"><span data-stu-id="c9711-125">X</span></span> |
| <span data-ttu-id="c9711-126">Contribuinte de subscrição</span><span class="sxs-lookup"><span data-stu-id="c9711-126">Subscription Contributor</span></span> | <span data-ttu-id="c9711-127">X</span><span class="sxs-lookup"><span data-stu-id="c9711-127">X</span></span> | <span data-ttu-id="c9711-128">X</span><span class="sxs-lookup"><span data-stu-id="c9711-128">X</span></span> | <span data-ttu-id="c9711-129">X</span><span class="sxs-lookup"><span data-stu-id="c9711-129">X</span></span> | <span data-ttu-id="c9711-130">X</span><span class="sxs-lookup"><span data-stu-id="c9711-130">X</span></span> |
| <span data-ttu-id="c9711-131">Proprietário do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c9711-131">Resource Group Owner</span></span> | -- | <span data-ttu-id="c9711-132">X</span><span class="sxs-lookup"><span data-stu-id="c9711-132">X</span></span> | -- | <span data-ttu-id="c9711-133">X</span><span class="sxs-lookup"><span data-stu-id="c9711-133">X</span></span> |
| <span data-ttu-id="c9711-134">Grupo de recursos contribuinte</span><span class="sxs-lookup"><span data-stu-id="c9711-134">Resource Group Contributor</span></span> | -- | <span data-ttu-id="c9711-135">X</span><span class="sxs-lookup"><span data-stu-id="c9711-135">X</span></span> | -- | <span data-ttu-id="c9711-136">X</span><span class="sxs-lookup"><span data-stu-id="c9711-136">X</span></span> |
| <span data-ttu-id="c9711-137">Leitor</span><span class="sxs-lookup"><span data-stu-id="c9711-137">Reader</span></span> | -- | -- | -- | <span data-ttu-id="c9711-138">X</span><span class="sxs-lookup"><span data-stu-id="c9711-138">X</span></span> |
| <span data-ttu-id="c9711-139">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="c9711-139">Security Administrator</span></span> | <span data-ttu-id="c9711-140">X</span><span class="sxs-lookup"><span data-stu-id="c9711-140">X</span></span> | -- | <span data-ttu-id="c9711-141">X</span><span class="sxs-lookup"><span data-stu-id="c9711-141">X</span></span> | <span data-ttu-id="c9711-142">X</span><span class="sxs-lookup"><span data-stu-id="c9711-142">X</span></span> |
| <span data-ttu-id="c9711-143">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="c9711-143">Security Reader</span></span> | -- | -- | -- | <span data-ttu-id="c9711-144">X</span><span class="sxs-lookup"><span data-stu-id="c9711-144">X</span></span> |

> [!NOTE]
> <span data-ttu-id="c9711-145">Recomendamos que atribua Olá função menos permissiva necessária para os utilizadores toocomplete as respetivas tarefas.</span><span class="sxs-lookup"><span data-stu-id="c9711-145">We recommend that you assign hello least permissive role needed for users toocomplete their tasks.</span></span> <span data-ttu-id="c9711-146">Por exemplo, atribua toousers de função de leitor Olá que basta tooview informações sobre o estado de funcionamento do Olá segurança de um recurso, mas não tomar medidas, tal como aplicar recomendações ou editar políticas.</span><span class="sxs-lookup"><span data-stu-id="c9711-146">For example, assign hello Reader role toousers who only need tooview information about hello security health of a resource but not take action, such as applying recommendations or editing policies.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c9711-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c9711-147">Next steps</span></span>
<span data-ttu-id="c9711-148">Este artigo explicado como o Centro de segurança utiliza o RBAC tooassign permissões toousers e identificado Olá permitida ações para cada função.</span><span class="sxs-lookup"><span data-stu-id="c9711-148">This article explained how Security Center uses RBAC tooassign permissions toousers and identified hello allowed actions for each role.</span></span> <span data-ttu-id="c9711-149">Agora que está familiarizado com atribuições de funções de Olá necessário toomonitor Olá estado de segurança da sua subscrição, edite as políticas de segurança e aplicar recomendações, saiba como:</span><span class="sxs-lookup"><span data-stu-id="c9711-149">Now that you're familiar with hello role assignments needed toomonitor hello security state of your subscription, edit security policies, and apply recommendations, learn how to:</span></span>

- [<span data-ttu-id="c9711-150">Definir políticas de segurança no Centro de segurança</span><span class="sxs-lookup"><span data-stu-id="c9711-150">Set security policies in Security Center</span></span>](security-center-policies.md)
- [<span data-ttu-id="c9711-151">Gerir recomendações de segurança no Centro de segurança</span><span class="sxs-lookup"><span data-stu-id="c9711-151">Manage security recommendations in Security Center</span></span>](security-center-recommendations.md)
- [<span data-ttu-id="c9711-152">Monitorizar estado de funcionamento de segurança de Olá dos seus recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c9711-152">Monitor hello security health of your Azure resources</span></span>](security-center-monitoring.md)
- [<span data-ttu-id="c9711-153">Gerir e responder a alertas de toosecurity no Centro de segurança</span><span class="sxs-lookup"><span data-stu-id="c9711-153">Manage and respond toosecurity alerts in Security Center</span></span>](security-center-managing-and-responding-alerts.md)
- [<span data-ttu-id="c9711-154">Monitorizar soluções de segurança de parceiros</span><span class="sxs-lookup"><span data-stu-id="c9711-154">Monitor partner security solutions</span></span>](security-center-partner-solutions.md)
