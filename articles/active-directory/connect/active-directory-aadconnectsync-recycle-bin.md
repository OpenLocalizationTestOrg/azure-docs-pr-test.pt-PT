---
title: "Sincronização do Azure AD Connect: Ativar Reciclagem AD | Microsoft Docs"
description: "Este tópico recomenda a utilização de Olá da funcionalidade de reciclagem do AD com o Azure AD Connect."
services: active-directory
keywords: "Reciclagem do AD, a eliminação acidental, âncora de origem"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Sincronização do Azure AD Connect: Ativar Reciclagem do AD
Recomenda-se que ative a funcionalidade de reciclagem Olá AD para os diretórios de Active Directory no local, que são sincronizado tooAzure AD. 

Caso o tenha eliminado acidentalmente um local objeto de utilizador do AD e restaure-la utilizando a funcionalidade de Olá, Azure AD restaura objeto de utilizador do Azure AD de Olá correspondente.  Para obter informações sobre a funcionalidade de reciclagem Olá AD, consulte tooarticle [descrição geral do cenário para restaurar eliminar objetos do Active Directory](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Benefícios da ativação Olá AD Reciclagem
Esta funcionalidade ajuda-o com o restauro de objetos de utilizador do Azure AD, Olá seguinte:

* Caso o tenha eliminado acidentalmente um local objeto de utilizador do AD, objeto de utilizador do Azure AD correspondente Olá será eliminado no Olá próximo ciclo de sincronização. Por predefinição, do Azure AD mantém o objeto de utilizador do Azure AD Olá eliminado no estado de eliminação de forma recuperável durante 30 dias.

* Se tiver no local ativada a funcionalidade de reciclagem do AD, pode restaurar Olá eliminado no local o objeto de utilizador do AD sem alterar o valor de âncora de origem. Quando Olá recuperados no local o objeto de utilizador do AD está sincronizado tooAzure AD, do Azure AD irá restaurar Olá correspondente eliminados de forma recuperável objeto de utilizador do Azure AD. Para obter informações sobre o atributo âncora de origem, consulte tooarticle [do Azure AD Connect: conceitos de Design](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Se não tiver no local AD reciclar funcionalidade de reciclagem ativada, poderá ser necessário toocreate um AD utilizador objeto tooreplace Olá objeto eliminado. Se serviço sincronização do Azure AD Connect toouse configurado gerado pelo sistema AD atributo (por exemplo, ObjectGuid) para o atributo de âncora de origem Olá, hello acabada de criar objeto de utilizador do AD será não ter Olá mesmo valor de âncora de origem como Olá eliminou o objeto de utilizador do AD. Quando Olá criado recentemente AD para o objeto de utilizador é sincronizado tooAzure AD, do Azure AD cria um novo objeto de utilizador do Azure AD em vez de restaurar o objeto de utilizador do Azure AD Olá eliminados de forma recuperável.

> [!NOTE]
> Por predefinição, do Azure AD mantém eliminar objetos de utilizador do Azure AD no estado de eliminação de forma recuperável durante 30 dias antes de estes sejam eliminados permanentemente. No entanto, os administradores podem acelerar a eliminação de Olá desses objetos. Depois de objetos de Olá são eliminados definitivamente, já não podem ser recuperados, mesmo quando no local é ativada a funcionalidade de reciclagem do AD.



## <a name="next-steps"></a>Passos seguintes
**Tópicos de descrição geral**

* [Sincronização do Azure AD Connect: Noções e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)

* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
