---
title: "inquilino do Azure Active Directory de Olá de aaaChange no Azure RemoteApp | Microsoft Docs"
description: "Saiba como o inquilino do toochange Olá do Azure Active Directory associados com o Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Alterar inquilino do Azure Active Directory Olá no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

O Azure RemoteApp utiliza o Azure Active Directory (Azure AD) tooallow de acesso de utilizadores. inquilino Olá apenas do Azure AD, que pode utilizar no Azure RemoteApp é Olá um associados Olá subscrição do Azure. Pode ver subscrição Olá associado no Olá **definições** página Olá portal. Observe Olá **diretório** coluna no Olá **subscrições** separador.

> [!NOTE]
> Para toosucceed esta alteração, remova primeiro todos os utilizadores de inquilino do Azure Active Directory existente Olá de todas as coleções do Azure RemoteApp. toodo, aceda toohello Portal do Azure, aceda toohello **Azure RemoteApp** separador e abra cada coleção do Azure RemoteApp. Aceda toohello **utilizadores** separador e remover utilizadores que pertencem tooyour inquilino de Azure Active Directory atual. Repita para todas as coleções existentes do Azure RemoteApp. Sem fazê-lo, não será capaz de toocreate ou coleções de patch.
> 
> 

Se quiser toouse um inquilino diferente, utilize estes passos toochange Olá associação sua subscrição:

1. No portal de Olá, remova qualquer toowhich de utilizadores do Azure AD concedeu acesso tooAzure coleções do RemoteApp. (Ver nota Olá acima para obter os passos sobre como toodo isto.)
2. Defina uma conta Microsoft (anteriormente denominada Live ID) como administrador de serviços de Olá. (Não sabe se já estiver Olá, admin serviço? Pode descobrir clicando **definições -> administradores**.) Agora, eis como alterar que:
   
   1. Em Olá utilizador no canto superior direito Olá e, em seguida, clique em **ver minha fatura**.
   2. Clique em subscrição Olá. Em seguida, na página de nova Olá, desloque para baixo e clique em **editar detalhes da subscrição** no Olá à direita. (A ordenação de Olá média na parte inferior direita, se essa ajuda-o a encontrá-lo.)
   3. Escreva Olá Microsoft conta para utilizador Olá que deve ser Olá Admin de serviço
3. Agora, termine a sessão no portal de Olá e, em seguida, inicie sessão novamente com Olá conta Microsoft que especificou no passo anterior Olá.
4. Clique em **novo -> aplicação serviços -> Active Directory Active-Directory > -> personalizada criar**.
5. Em **diretório**, escolha **utilizar diretório existente**. Vamos toohave toosign fora do portal de Olá agora, por isso, escolher **estou pronto toobe terminar sessão agora**.
6. Voltar a iniciar sessão em Olá portal como um administrador global do diretório de Olá pretende tooadd. (Se já não é um administrador global, será após um round de iniciar sessão e, em seguida, terminar sessão.)
7. Será pedido quando iniciarem sessão se quiser toouse inquilino do AD existente com a sua subscrição. Clique em **continuar**e, em seguida, clique em **terminar sessão agora**.
8. Inicie sessão novamente novamente e voltar atrás demasiado**definições -> subscrições**. Selecione a sua subscrição e, em seguida, clique em **Editar diretório**. Selecione o inquilino Olá do Azure AD que pretende que o toouse.

Agora, pode utilizar Olá do Azure AD novo inquilino toocontrol acesso toohello acesso de utilizador de subscrição e tooconfigure do Azure no Azure RemoteApp.

