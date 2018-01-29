---
title: Administrador de inquilinos elevar o acesso - do Azure AD | Microsoft Docs
description: "Este tópico descreve a incorporado em funções para o controlo de acesso baseado em funções (RBAC)."
services: active-directory
documentationcenter: 
author: andredm7
manager: mtillman
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 10/30/2017
ms.author: andredm
ms.openlocfilehash: 894ccd13684a79590b75821514ef6922abb8fdaf
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/11/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Elevar o acesso como um administrador inquilino com controlo de acesso baseado em funções

Controlo de acesso baseado em funções ajuda os administradores inquilinos a obter Elevações temporárias do acesso para que estes podem conceder permissões superiores que o habitual. Um administrador de inquilino pode efetuar a elevação herself para a função de administrador de acesso do utilizador quando necessário. Essa função fornece o inquilino permissões de administrador para conceder herself ou outras funções no âmbito "/".

Esta funcionalidade é importante porque permite que o administrador de inquilino ver todas as subscrições que existem numa organização. Também permite que aplicações de automatização, como faturação e de auditoria para aceder a todas as subscrições e fornecer uma vista exata do Estado da organização para a gestão de recursos ou de faturação.  

## <a name="use-elevateaccess-for-tenant-access-with-azure-ad-admin-center"></a>Utilizar elevateAccess para acesso de inquilino com o Centro de administração do Azure AD

1. Vá para o [Centro de administração do Azure Active Directory](https://aad.portal.azure.com) e inicie sessão com que as credenciais.

2. Escolha **propriedades** do Azure AD deixado menu.

3. No **propriedades** painel, localizar **Administrador Global pode gerir subscrições do Azure**, escolha **Sim**, em seguida, **guardar**.
    > [!IMPORTANT] 
    > Quando escolhe **Sim**, atribui o **administrador de acesso de utilizador** função na raiz "/" (âmbito de raiz) para o utilizador com a qual tem sessão iniciada no Portal. **Isto permite ao utilizador ver todas as outras subscrições do Azure.**
    
    > [!NOTE] 
    > Quando escolhe **não**, remove o **administrador de acesso de utilizador** função na raiz "/" (âmbito de raiz) para o utilizador com a qual tem sessão iniciada no Portal.

> [!TIP] 
> A impressão é que esta é uma propriedade Global do Azure Active Directory, no entanto, funciona numa base por utilizador para o utilizador atualmente com sessão iniciada. Quando tiver direitos de Administrador Global no Azure Active Directory, pode invocar a funcionalidade de elevateAccess para o utilizador que tem sessão iniciada no Centro de administração do Azure Active Directory.

![Globaladmin de centro de administração - propriedades - do Azure AD pode gerir a subscrição do Azure - captura de ecrã](./media/role-based-access-control-tenant-admin-access/aad-azure-portal-global-admin-can-manage-azure-subscriptions.png)

## <a name="view-role-assignments-at-the--scope-using-powershell"></a>Ver as atribuições de função no âmbito "/" com o PowerShell
Para ver o **administrador de acesso de utilizador** atribuição no  **/**  âmbito, utilize o `Get-AzureRmRoleAssignment` cmdlet do PowerShell.
    
```
Get-AzureRmRoleAssignment* | where {$_.RoleDefinitionName -eq "User Access Administrator" -and $_SignInName -eq "<username@somedomain.com>" -and $_.Scope -eq "/"}
```

**Exemplo de saída**:

RoleAssignmentId: /providers/Microsoft.Authorization/roleAssignments/098d572e-c1e5-43ee-84ce-8dc459c7e1f0    
Âmbito: /    
DisplayName: nome de utilizador    
SignInName:username@somedomain.com    
RoleDefinitionName: Administrador de acesso de utilizador    
Em RoleDefinitionId: 18d7d88d-d35e-4fb5-a5c3-7773c20a72d9    
ObjectId: d65fd0e9-c185-472c-8f26-1dafa01f72cc    
ObjectType: utilizador    

## <a name="delete-the-role-assignment-at--scope-using-powershell"></a>Eliminar a atribuição de função em "/" definir o âmbito com o Powershell:
Pode eliminar a atribuição de utilizar o seguinte cmdlet do PowerShell:
```
Remove-AzureRmRoleAssignment -SignInName <username@somedomain.com> -RoleDefinitionName "User Access Administrator" -Scope "/" 
```

## <a name="use-elevateaccess-to-give-tenant-access-with-the-rest-api"></a>Utilizar elevateAccess para dar acesso do inquilino com a API REST

O processo básico funciona com os seguintes passos:

1. Utilizar REST, chamar *elevateAccess*, que lhe concede a função de administrador de acesso de utilizador em "/" definir o âmbito.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Criar um [atribuição de função](/rest/api/authorization/roleassignments) atribuir qualquer função em qualquer âmbito. O exemplo seguinte mostra as propriedades para atribuir a função do leitor "/" definir o âmbito:

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


## <a name="how-to-undo-the-elevateaccess-action-with-the-rest-api"></a>Como anular a ação de elevateAccess com a API REST

Quando chamar *elevateAccess* cria uma atribuição de função para si, por isso revogar esses privilégios terá de eliminar a atribuição.

1.  OBTER definições de funções de chamada onde roleName = administrador de acesso de utilizador para determinar o nome do GUID da função de administrador de acesso de utilizador.
    1.  OBTER *filtro de $ https://management.azure.com/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01& = roleName + eq + "utilizador + + ao administrador de acesso*

        ```
        {"value":[{"properties":{
        "roleName":"User Access Administrator",
        "type":"BuiltInRole",
        "description":"Lets you manage user access to Azure resources.",
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

        Guarde o GUID do *nome* parâmetro, neste caso, **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Também precisa de listar a atribuição de função de administrador inquilino no âmbito de inquilino. Liste todas as atribuições de âmbito de inquilino para o PrincipalId de TenantAdmin que efetuou o acesso de elevate chamada. Isto irá listar todas as atribuições de inquilino para o ObjectID. 
    1. OBTER *filtro de $ https://management.azure.com/providers/Microsoft.Authorization/roleAssignments?api-version=2015-07-01& = principalId + eq + {objectid}*
    
        >[!NOTE] 
        >Um administrador inquilino não deve ter muitos atribuições, se a consulta acima devolve demasiadas atribuições, também pode consultar para todas as atribuições de apenas ao nível do âmbito de inquilino e filtrar os resultados: obter *https://management.azure.com/providers/ Microsoft.Authorization/roleAssignments? api-version = 2015-07-01 & $filter=atScope()*
        
    2. As chamadas acima devolvem uma lista de atribuições de funções. Localizar a atribuição de função em que o âmbito é "/" e o em RoleDefinitionId termina com o nome da função GUID que encontrar no passo 1 e PrincipalId corresponde o ObjectId de administrador inquilino. A atribuição de função tem o seguinte aspeto:

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
        
        Novamente, guarde o GUID do *nome* parâmetro, neste caso, **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

    3. Por fim, utilize o realçado **RoleAssignment ID** para eliminar a atribuição adicionada por elevar o acesso:

        Eliminar https://management.azure.com /providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099?api-version=2015-07-01

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre [gestão do controlo de acesso baseado em funções com REST](role-based-access-control-manage-access-rest.md)

- [Gerir atribuições de acesso](role-based-access-control-manage-assignments.md) no portal do Azure
