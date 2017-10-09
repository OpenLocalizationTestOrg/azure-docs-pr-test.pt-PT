---
title: "aaaHow tooUse controlo de acesso baseado em funções na API Management do Azure | Microsoft Docs"
description: "Saiba como toouse Olá funções incorporadas e criar funções personalizadas na API Management do Azure"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Como tooUse baseada em funções do controlo de acesso na API Management do Azure
Gestão de API do Azure baseia-se na gestão de acesso detalhada de tooenable de controlo de acesso em funções do Azure (RBAC) para serviços de gestão de API e entidades (por exemplo, APIs, políticas). Este artigo fornece uma descrição geral das funções incorporadas e personalizadas de Olá na API Management. Se pretender obter mais detalhes sobre a gestão de acesso no portal do Azure de Olá, veja [introdução à gestão de acesso no Olá portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Funções incorporadas
Gestão de API atualmente fornece 3 funções incorporadas e irá adicionar 2 funções mais Olá quase futuro. Estas funções podem ser atribuídas em âmbitos diferentes, incluindo a subscrição, o grupo de recursos e instância de API Management individuais. Por exemplo, se tooan utilizador ao nível do grupo de recursos de Olá é atribuída a função de "Leitor do serviço de gestão de API do Azure" Olá, em seguida, Olá utilizador terá acesso de leitura instâncias de API Management tooall no interior do grupo de recursos de Olá. 

Olá tabela seguinte fornece breves descrições das Olá funções incorporadas. Pode atribuir estas funções utilizando Olá Portal do Azure ou outras ferramentas, incluindo o Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [interface de linha de comandos](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), e [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Para obter detalhes sobre como funções incorporadas tooassign, consulte [utilizar recursos de subscrição do Azure do função atribuições toomanage acesso tooyour](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Função          | Acesso de leitura<sup>[1]</sup> | Acesso de escrita<sup>[2]</sup> | Criação do serviço, eliminação, dimensionamento, VPN e a configuração de domínio personalizado | Acesso toolegacy Publsiher Portal | Descrição
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Contribuinte de serviço de gestão de API do Azure | ✓ | ✓ | ✓ | ✓ | Superutilizador. Tem completa dos serviços de gestão do CRUD acesso tooAPI e entidades (por exemplo, APIs, políticas). Tem o portal do publicador legado de toohello de acesso. |
| Leitor de serviço de gestão de API do Azure | ✓ | | || Tem serviços de gestão do acesso só de leitura tooAPI e entidades. |
| Operador de serviço de gestão de API do Azure | ✓ | | ✓ | | Pode gerir os serviços de gestão de API, mas não entidades.|
| Editor de serviço de gestão de API do Azure<sup>*</sup> | ✓ | ✓ | |  | Pode gerir as entidades de API Management, mas não os serviços.|
| Gestor de conteúdos de gestão de API do Azure<sup>*</sup> | ✓ | | | ✓ | Pode gerir o portal do programador. Acesso só de leitura tooservices e entidades.|

<sup>[1] serviços de gestão do acesso de leitura tooAPI e entidades (por exemplo, APIs, as políticas de)</sup>

<sup>Serviços de gestão do acesso de escrita do [2] tooAPI e entidades, exceto opeartions seguintes: 1) instância criação, eliminação e o dimensionamento de configuração de nome de domínio do 2) VPN configuração personalizada 3)</sup>

<sup>\*função de Editor do serviço de Olá ficará disponível após iremos migrar todos os admin da IU do Olá existente publicador portal toohello portal do Azure. Olá função de Gestor de conteúdos estará disponível depois do portal do publicador Olá é refatorizado tooonly conter portal do programador funcionalidades relacionadas toomanaging Olá.</sup>  


## <a name="custom-roles"></a>Funções personalizadas
Se nenhuma das funções incorporadas Olá as suas necessidades específicas, funções personalizadas podem ser criadas tooprovide mais granular access management para entidades de API Management. Por exemplo, pode criar uma função personalizada que tem acesso só de leitura tooan serviço de API Management, mas só tem acesso de escrita tooone específico API. toolearn obter mais detalhes sobre as funções personalizados, consulte [funções personalizadas no Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Quando cria uma função personalizada, é mais fácil toostart com uma das funções incorporadas Olá. Editar Olá atributos tooadd ações Olá, NotActions ou AssignableScopes, em seguida, guarde as alterações de Olá como uma nova função. Olá exemplo seguinte começa com a função de "Leitor do serviço de gestão de API do Azure" Olá e cria uma função personalizada denominada "Editor de API de Calculadora". pode ser atribuída a função personalizada Olá só tooa que API específica, por conseguinte, irá apenas tem acesso toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Veja uma descrição geral do vídeo

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Passos Seguintes

* Saiba mais sobre o controlo de acesso baseado em funções no Azure
  * [Introdução à gestão de acesso no Olá portal do Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Utilização de recursos de subscrição do Azure de tooyour toomanage acesso função atribuições](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Funções personalizadas no Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
