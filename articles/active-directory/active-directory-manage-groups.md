---
title: aaaUse grupos toomanage acesso tooresources no Azure Active Directory | Microsoft Docs
description: "Como aceder aos grupos de toouse no utilizador do Azure Active Directory toomanage tooon local e de aplicações em nuvem e de recursos."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Gerir o acesso tooresources com grupos do Active Directory do Azure
Azure Active Directory (Azure AD) é uma solução de gestão identidades e acessos abrangente que fornece um conjunto robusto de capacidades toomanage acesso tooon no local e de aplicações em nuvem e de recursos, incluindo os serviços online da Microsoft como o Office 365 e um mundo de aplicações SaaS não Microsoft. Este artigo fornece uma descrição geral, mas se pretender toostart utilizar o Azure AD grupos neste momento, siga as instruções de Olá em [gerir grupos de segurança no Azure AD](active-directory-accessmanagement-manage-groups.md). Se quiser toosee como pode utilizar o PowerShell toomanage grupos no Azure Active directory, pode ler mais em [cmdlets do Azure Active Directory para gestão de grupo](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse do Azure Active Directory, terá de uma conta do Azure. Se não tiver uma conta, pode [inscrever-se numa conta do Azure gratuita](https://azure.microsoft.com/pricing/free-trial/).
>
>

Dentro do Azure AD, uma das principais funcionalidades de Olá é Olá capacidade toomanage acesso tooresources. Estes recursos podem fazer parte do diretório de Olá, como no caso de Olá de objetos de toomanage permissões através de funções no diretório de Olá ou recursos que são directory toohello externo, como aplicações SaaS, serviços do Azure e sites do SharePoint ou no local recursos. Existem quatro formas que um utilizador pode ser atribuído recursos de tooa de direitos de acesso:

1. Atribuição direta

    Os utilizadores podem ser atribuídos diretamente tooa recurso pelo proprietário de Olá desse recurso.
2. Associação ao grupo

    Um grupo pode ser atribuído recursos tooa pelo proprietário do recurso Olá e ao fazê-lo, conceder Olá os membros do recurso de toohello de acesso de grupo. Associação de grupo Olá, em seguida, pode ser gerida pelo proprietário de Olá do grupo de Olá. Efetivamente, os delegados de proprietário do recurso Olá Olá permissão tooassign utilizadores tootheir toohello proprietário do recurso do grupo de Olá.
3. Baseado em regras

    Pode utilizar o proprietário do recurso Olá tooexpress uma regra que utilizadores devem ser atribuídos acesso tooa recursos. resultado de Olá da regra de Olá depende de atributos de Olá utilizados dessa regra e os respetivos valores para utilizadores específicos e ao fazê-lo, o proprietário do recurso Olá delega eficazmente Olá toomanage direita acesso tootheir recursos toohello origem autoritária de Olá atributos que são utilizados na regra Olá. proprietário do recurso Olá ainda gere a regra de Olá próprio e determina quais os atributos e valores fornecem acesso tootheir recursos.
4. Autoridade externa

    recurso de tooa Olá acesso é derivado de uma origem externa; Por exemplo, um grupo que é sincronizado a partir de uma origem autoritária, tais como um diretório no local ou uma aplicação de SaaS, como do WorkDay. proprietário do recurso Olá atribui o recurso de toohello do Olá grupo tooprovide acesso e a origem externa da Olá gere Olá os membros do grupo de Olá.

   ![Descrição geral do diagrama de gestão de acesso](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Ver um vídeo que explica a gestão de acesso
Pode ver um breve vídeo, que explica mais sobre esta:

**Do Azure AD: A associação de toodynamic de introdução para grupos**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Como aceder à gestão de trabalho do Azure Active Directory?
Em Olá centro da solução de gestão de acesso do Azure AD de Olá é o grupo de segurança de Olá. A utilização de um tooresources de acesso de toomanage de grupo de segurança é uma paradigma bem conhecida, que permite obter um recurso de forma flexível e facilmente compreendidos do tooa ao acesso tooprovide para grupo de Olá que se destina de utilizadores. proprietário do recurso Olá (Olá administrador ou do diretório de Olá) pode atribuir um grupo tooprovide um certos acesso toohello direita recursos possuem. Olá os membros do grupo de Olá irão ser fornecidos acesso Olá e proprietário do recurso Olá pode delegar a lista de membros do Olá toomanage direita Olá de uma pessoa, por exemplo, um Gestor de departamento ou um administrador de suporte técnico de toosomeone de grupo.

![Diagrama de gestão de acesso do Azure Active Directory](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

proprietário de Olá de um grupo pode também disponibilizar desse grupo para pedidos de self-service. Ao fazê-lo, um utilizador final pode procurar e localizar o grupo de Olá e certifique-toojoin um pedido, procura eficazmente permissão tooaccess Olá recursos que são geridos através do grupo de Olá. proprietário de Olá do grupo de Olá pode configurar o grupo de Olá, para que os pedidos de associação são aprovados automaticamente ou exigem a aprovação por proprietário Olá do grupo de Olá. Quando um utilizador faz um pedido toojoin um grupo, o pedido de adesão Olá é reencaminhado toohello proprietários do grupo de Olá. Se um dos proprietários Olá aprova o pedido de Olá, utilizador requerente Olá é notificado e o utilizador de Olá é toohello associados a um grupo. Se um dos proprietários Olá nega pedidos de Olá, o utilizador requerente Olá é notificado mas não associados a um grupo de toohello.

## <a name="getting-started-with-access-management"></a>Introdução à gestão de acesso
Tooget pronto a utilizar? Deve tentar terminar algumas das tarefas básico Olá que pode fazer com grupos do Azure AD. Utilize estas capacidades tooprovide especializada aceder toodifferent grupos de pessoas para diferentes recursos na sua organização. Uma lista dos passos básicos de primeiro estão listados abaixo.

* [Criar uma regra simples tooconfigure a filiação dinâmica para um grupo](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Utilizar um grupo toomanage acesso tooSaaS aplicações](active-directory-accessmanagement-group-saasapps.md)
* [Disponibilizar um grupo para o final utilizador self-service](active-directory-accessmanagement-self-service-group-management.md)
* [A sincronizar um tooAzure de grupo no local com o Azure AD Connect](active-directory-aadconnect.md)
* [Gerir proprietários de um grupo](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Passos seguintes
Agora que tem compreendido Olá Noções básicas sobre gestão de acesso, aqui estão algumas funcionalidades avançadas adicionais disponíveis no Azure Active Directory para gerir o acesso tooyour aplicações e recursos.

* [Utilizar atributos toocreate avançadas de regras](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Gerir grupos de segurança no Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Configurar grupos dedicados no Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Referência da Graph API para grupos](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Cmdlets do Azure Active Directory para configurar definições de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
