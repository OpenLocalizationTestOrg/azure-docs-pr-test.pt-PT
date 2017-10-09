---
title: "Sincronização do Azure AD Connect: a alteração Olá AD DS conta palavra-passe de | Microsoft Docs"
description: "Este documento de tópico descreve como tooupdate do Azure AD Connect após Olá palavra-passe da conta de Olá do AD DS é alterado."
services: active-directory
keywords: Conta do AD DS, a conta do Active Directory, a palavra-passe
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>A alteração de palavra-passe de conta do Olá AD DS
conta do Olá AD DS refere-se a conta de utilizador toohello utilizada pelo Azure AD Connect toocommunicate com o Active Directory no local. Se alterar Olá palavra-passe da conta do AD DS de Olá, tem de atualizar o serviço de sincronização ligar do Azure AD com a nova palavra-passe Olá. Caso contrário, Olá que sincronização já não pode sincronizar corretamente com Olá no local do Active Directory e irá encontrar Olá seguintes erros:

* No Olá operação Synchronization Service Manager, qualquer importação ou exportação com no local irá falhar do AD com **credenciais de início não** erro.

* No Visualizador de eventos do Windows, o registo de eventos de aplicações de Olá contém um erro com **6000 de ID de evento** e mensagem **'agente de gestão de Olá "contoso.com" Falha toorun porque as credenciais de Olá foram inválidas'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Como tooupdate Olá serviço de sincronização com a nova palavra-passe para a conta do AD DS
tooupdate Olá serviço de sincronização com a nova palavra-passe Olá:

1. Inicie Olá Synchronization Service Manager (serviço de sincronização inicial →).
</br>![Gestor do serviço de sincronização](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Aceda toohello **conectores** separador.

3. Selecione Olá **conector AD** que corresponde à conta do toohello AD DS para o qual a respetiva palavra-passe foi alterada.

4. Em **ações**, selecione **propriedades**.

5. Na caixa de diálogo pop-up de Olá, selecione **ligar tooActive diretório floresta**:

6. Introduza Olá nova palavra-passe da conta de Olá do AD DS no Olá **palavra-passe** caixa de texto.

7. Clique em **OK** toosave Olá nova palavra-passe e a caixa de diálogo de pop-up Olá fechar.

8. Reinício hello do Azure AD Connect serviço de sincronização em Gestor de controlo de serviço do Windows. Este é tooensure que qualquer referência toohello palavra-passe antiga é removido da cache de memória de Olá.

## <a name="next-steps"></a>Passos seguintes
**Tópicos de descrição geral**

* [Sincronização do Azure AD Connect: Noções e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)

* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
