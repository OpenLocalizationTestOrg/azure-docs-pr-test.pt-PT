---
title: aaaHow toouse Azure RemoteApp com contas de utilizador do Office 365 | Microsoft Docs
description: Saiba como toouse Azure RemoteApp com os meus contas de utilizador do Office 365
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: aba70fd3-60b0-4b44-9321-1ab18760ccd5
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d2dbed2a6838adf9bb0f7508eb7dcecb0a74a62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-remoteapp-with-office-365-user-accounts"></a>Como toouse Azure RemoteApp com contas de utilizador do Office 365
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Se tiver uma subscrição do Office 365 tem um Azure Active Directory que armazena os nomes de utilizador e palavras-passe utilizadas tooaccess serviços do Office 365. Por exemplo, quando os utilizadores ativarem do Office 365 ProPlus efetuam a autenticação contra toocheck do Azure AD de licenças. Maioria dos clientes seria como toouse Olá mesmo diretório com o Azure RemoteApp.

Se estiver a implementar o Azure RemoteApp muito provável que está a utilizar uma subscrição do Azure que está associada um diferente do Azure AD. Ordenar toouse diretório no Office 365, terá de toomove Olá subscrição do Azure no diretório.

Para informações sobre como as aplicações de cliente toodeploy do Office 365, consulte [como toouse subscrição do Office 365 com o Azure RemoteApp](remoteapp-officesubscription.md).

## <a name="phase-1-register-your-free-office-365-azure-active-directory-subscription"></a>Fase 1: Registar a sua subscrição do Office 365 Azure Active Directory gratuita
Se estiver a utilizar Olá portal clássico do Azure, utilize os passos de Olá em [registar a sua subscrição gratuita do Azure Active Directory](https://technet.microsoft.com/library/dn832618.aspx) tooget acesso administrativo tooyour do Azure AD através do Olá Portal de gestão do Azure. Como resultado de Olá deste processo deve ser capaz de toolog para Olá portal do Azure e ver o diretório não existe – neste momento, não verão muito mais porque hello subscrição Azure completo que estiver a utilizar com o Azure RemoteApp está a ser um diretório diferente.

Lembre-se de que o nome de Olá e a palavra-passe da conta de administrador Olá criadas neste passo – serão necessários na fase 2.

Se estiver a utilizar Olá portal do Azure, veja [como tooregister e ativar um Azure Active Directory gratuito através do portal do Office 365](http://azureblogger.com/2016/01/how-to-register-and-activate-a-free-azure-active-directory-using-office-365-portal/).

## <a name="phase-2-change-hello-azure-ad-associated-with-your-azure-subscription"></a>Fase 2: Olá de alteração do Azure AD associada com a sua subscrição do Azure.
Vamos toochange sua subscrição do Azure do seu diretório atual para o diretório do Olá do Office 365 que trabalhou com na fase 1.

Siga as instruções de Olá descritas [inquilino do Azure Active Directory de Olá de alteração no Azure RemoteApp](remoteapp-changetenant.md). Paga toohello especial atenção os seguintes passos:

* Passo 1 de #: Se tiver implementado o Azure RemoteApp (ARA) nesta subscrição, certifique-se que remover todas as contas de utilizador do Azure AD a partir de qualquer coleção ARA em primeiro lugar, antes de tentar tudo o resto. Em alternativa, pode considerar a eliminar as coleções existentes.
* Passo #2: Este é um passo crítico. Terá de toouse uma conta Microsoft (por exemplo, @outlook.com) como um administrador de serviços na subscrição Olá; Isto acontece porque não é possível temos quaisquer contas de utilizador do Olá existente do Azure AD ligado toohello subscrição – se fazemos, iremos não será capaz de toomove-tooa diferentes do Azure AD.
* Passo #4: Ao adicionar um diretório existente, sistema Olá irá pedir-lhe toosign com a conta de administrador Olá esse directório. Certifique-se de que conta de administrador de Olá toouse da fase 1.
* Passo #5: Altere o diretório de principal de Olá do diretório do Olá subscrição tooyour do Office 365. resultado do Olá final deve ser que em Definições -> subscrições a sua subscrição apresenta uma lista de diretórios de Olá do Office 365. 
  ![Alterar o diretório da subscrição Olá Olá principal](./media/remoteapp-o365user/settings.png)

Neste momento a sua subscrição do Azure RemoteApp está associada com o Office 365 do Azure AD; Pode utilizar contas de utilizador do Office 365 existentes Olá com o Azure RemoteApp!

