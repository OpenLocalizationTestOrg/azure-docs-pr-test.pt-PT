---
title: "administração de aaaTenant elevar o acesso - do Azure AD | Microsoft Docs"
description: "Este tópico descreve Olá incorporada em funções para o controlo de acesso baseado em funções (RBAC)."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="c929d-103">Elevar o acesso como um administrador inquilino com controlo de acesso baseado em funções</span><span class="sxs-lookup"><span data-stu-id="c929d-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="c929d-104">Controlo de acesso baseado em funções ajuda os administradores inquilinos a obter Elevações temporárias do acesso para que estes podem conceder permissões superiores que o habitual.</span><span class="sxs-lookup"><span data-stu-id="c929d-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="c929d-105">Um administrador de inquilino pode efetuar a elevação herself toohello função de administrador de acesso do utilizador quando necessário.</span><span class="sxs-lookup"><span data-stu-id="c929d-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="c929d-106">Essa função fornece Olá toogrant de permissões de administrador de inquilinos herself ou outras funções em Olá âmbito "/".</span><span class="sxs-lookup"><span data-stu-id="c929d-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="c929d-107">Esta funcionalidade é importante porque permite inquilino Olá toosee admin que Olá todas as subscrições que existem numa organização.</span><span class="sxs-lookup"><span data-stu-id="c929d-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="c929d-108">Também permite a automatização aplicações (por exemplo, faturação e auditoria) tooaccess todas as subscrições de Olá e fornecer uma vista exata do Estado de Olá da organização Olá para a gestão de faturação ou elemento.</span><span class="sxs-lookup"><span data-stu-id="c929d-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="c929d-109">Como toouse elevateAccess toogive inquilino acesso</span><span class="sxs-lookup"><span data-stu-id="c929d-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="c929d-110">processo de básico Olá funciona com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="c929d-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="c929d-111">Utilizar REST, chamar *elevateAccess*, que concede a Olá a função de administrador de acesso de utilizador em "/" definir o âmbito.</span><span class="sxs-lookup"><span data-stu-id="c929d-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="c929d-112">Criar um [atribuição de função](/rest/api/authorization/roleassignments) tooassign qualquer função em qualquer âmbito.</span><span class="sxs-lookup"><span data-stu-id="c929d-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="c929d-113">Olá seguinte exemplo mostra propriedades Olá para atribuição de Olá função leitor "/" definir o âmbito:</span><span class="sxs-lookup"><span data-stu-id="c929d-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="c929d-114">Enquanto um administrador de acesso de utilizador, pode também eliminar atribuições de funções no "/" definir o âmbito.</span><span class="sxs-lookup"><span data-stu-id="c929d-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="c929d-115">Revogue os privilégios de administrador de acesso do utilizador até que forem necessárias novamente.</span><span class="sxs-lookup"><span data-stu-id="c929d-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="c929d-116">Como tooundo Olá elevateAccess ação</span><span class="sxs-lookup"><span data-stu-id="c929d-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="c929d-117">Quando chamar *elevateAccess* cria uma atribuição de função para si, para toorevoke os privilégios precisa de toodelete Olá atribuição.</span><span class="sxs-lookup"><span data-stu-id="c929d-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="c929d-118">Chamar [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) onde roleName = toodetermine de administrador de acesso de utilizador Olá nome GUID da função de administrador de acesso de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="c929d-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="c929d-119">resposta Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="c929d-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="c929d-120">Guardar Olá GUID de Olá *nome* parâmetro, neste caso, **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="c929d-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="c929d-121">Chamar [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) onde principalId = o seus próprios ObjectId.</span><span class="sxs-lookup"><span data-stu-id="c929d-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="c929d-122">Isto apresenta uma lista de todas as suas atribuições no inquilino Olá.</span><span class="sxs-lookup"><span data-stu-id="c929d-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="c929d-123">Procure Olá um onde está o âmbito de Olá "/" e atribua o nome Olá em RoleDefinitionId extremidades com a função de Olá GUID que encontrar no passo 1.</span><span class="sxs-lookup"><span data-stu-id="c929d-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="c929d-124">atribuição de função Olá deve ter o seguinte aspeto:</span><span class="sxs-lookup"><span data-stu-id="c929d-124">hello role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="c929d-125">Novamente, guardar Olá GUID de Olá *nome* parâmetro, neste caso, **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="c929d-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="c929d-126">Por fim, chamar [eliminar roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) onde roleAssignmentId = nome Olá GUID que encontrar no passo 2.</span><span class="sxs-lookup"><span data-stu-id="c929d-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c929d-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c929d-127">Next steps</span></span>

- <span data-ttu-id="c929d-128">Saiba mais sobre [gestão do controlo de acesso baseado em funções com REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="c929d-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="c929d-129">[Gerir atribuições de acesso](role-based-access-control-manage-assignments.md) no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c929d-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
