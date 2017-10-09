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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Elevar o acesso como um administrador inquilino com controlo de acesso baseado em funções

Controlo de acesso baseado em funções ajuda os administradores inquilinos a obter Elevações temporárias do acesso para que estes podem conceder permissões superiores que o habitual. Um administrador de inquilino pode efetuar a elevação herself toohello função de administrador de acesso do utilizador quando necessário. Essa função fornece Olá toogrant de permissões de administrador de inquilinos herself ou outras funções em Olá âmbito "/".

Esta funcionalidade é importante porque permite inquilino Olá toosee admin que Olá todas as subscrições que existem numa organização. Também permite a automatização aplicações (por exemplo, faturação e auditoria) tooaccess todas as subscrições de Olá e fornecer uma vista exata do Estado de Olá da organização Olá para a gestão de faturação ou elemento.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Como toouse elevateAccess toogive inquilino acesso

processo de básico Olá funciona com Olá os seguintes passos:

1. Utilizar REST, chamar *elevateAccess*, que concede a Olá a função de administrador de acesso de utilizador em "/" definir o âmbito.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Criar um [atribuição de função](/rest/api/authorization/roleassignments) tooassign qualquer função em qualquer âmbito. Olá seguinte exemplo mostra propriedades Olá para atribuição de Olá função leitor "/" definir o âmbito:

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

3. Enquanto um administrador de acesso de utilizador, pode também eliminar atribuições de funções no "/" definir o âmbito.

4. Revogue os privilégios de administrador de acesso do utilizador até que forem necessárias novamente.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Como tooundo Olá elevateAccess ação

Quando chamar *elevateAccess* cria uma atribuição de função para si, para toorevoke os privilégios precisa de toodelete Olá atribuição.

1.  Chamar [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) onde roleName = toodetermine de administrador de acesso de utilizador Olá nome GUID da função de administrador de acesso de utilizador de Olá. resposta Olá deve ter o seguinte aspeto:

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

    Guardar Olá GUID de Olá *nome* parâmetro, neste caso, **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Chamar [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) onde principalId = o seus próprios ObjectId. Isto apresenta uma lista de todas as suas atribuições no inquilino Olá. Procure Olá um onde está o âmbito de Olá "/" e atribua o nome Olá em RoleDefinitionId extremidades com a função de Olá GUID que encontrar no passo 1. atribuição de função Olá deve ter o seguinte aspeto:

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

    Novamente, guardar Olá GUID de Olá *nome* parâmetro, neste caso, **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Por fim, chamar [eliminar roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) onde roleAssignmentId = nome Olá GUID que encontrar no passo 2.

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [gestão do controlo de acesso baseado em funções com REST](role-based-access-control-manage-access-rest.md)

- [Gerir atribuições de acesso](role-based-access-control-manage-assignments.md) no Olá portal do Azure
