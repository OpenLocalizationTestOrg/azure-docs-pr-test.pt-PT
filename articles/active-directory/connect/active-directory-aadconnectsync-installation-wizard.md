---
title: "Novamente executar Assistente de instalação de Olá do Azure AD Connect | Microsoft Docs"
description: "Explica como o Assistente de instalação de Olá funciona Olá segunda vez que executá-la."
keywords: "Assistente de instalação do Olá do Azure AD Connect permite-lhe configurar Olá de definições de manutenção segunda vez que executá-la"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Sincronização do Azure AD Connect: executar o Assistente de instalação de Olá uma segunda vez
Olá pela primeira vez, execute o Assistente de instalação do Olá do Azure AD Connect, explica como tooconfigure a instalação. Se executar novamente o Assistente de instalação de Olá, oferece opções de manutenção.

Pode encontrar o Assistente de instalação de Olá no menu de início de Olá denominado **do Azure AD Connect**.

![Menu Iniciar](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Quando iniciar o Assistente de instalação de Olá, verá uma página com estas opções:

![Página com uma lista de tarefas adicionais](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Se tiver instalado o AD FS com o Azure AD Connect, terá ainda mais opções. Olá opções adicionais tiver para AD FS estão documentados na [gestão ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Selecione uma das tarefas de Olá e clique em **seguinte** toocontinue.

> [!IMPORTANT]
> Enquanto tiver o Assistente de instalação de Olá abrir, todas as operações no motor de sincronização de Olá são suspensas. Certifique-se que fechar o Assistente de instalação de Olá, assim que concluir as alterações de configuração.
>
>

## <a name="view-current-configuration"></a>Ver a configuração atual
Esta opção fornece-lhe uma vista rápida do que as suas opções atualmente configuradas.

![Página com uma lista de todas as opções e o respetivo estado](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Clique em **anterior** toogo anterior. Se selecionar **saída**, feche o Assistente de instalação de Olá.

## <a name="customize-synchronization-options"></a>Personalizar opções de sincronização
Esta opção é a configuração da sincronização toomake utilizados alterações toohello. Verá um subconjunto das opções a partir do caminho de instalação do Olá configuração personalizada. Ver esta opção, mesmo se tiver utilizado inicialmente instalação rápida.

* [Adicionar mais diretórios](active-directory-aadconnect-get-started-custom.md#connect-your-directories). Para remover um diretório, consulte [eliminar um conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Alterar o domínio e a UO filtragem](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).
* Remova a filtragem de grupos.
* [Alterar as funcionalidades opcionais](active-directory-aadconnect-get-started-custom.md#optional-features).

Olá outras opções de instalação inicial Olá não podem ser alteradas e não estão disponíveis. Estas opções são:

* Alterar o atributo de Olá toouse para userPrincipalName e sourceAnchor.
* Alterar Olá associar método destinada a objetos da floresta diferente.
* Ative a filtragem baseada no grupo.

## <a name="refresh-directory-schema"></a>Atualizar o esquema de diretório
Esta opção é utilizada se tiver alterado o esquema de Olá dos seus no local florestas do AD DS. Por exemplo, poderá ter instalado o Exchange ou atualizado o esquema de tooa Windows Server 2012 com objetos de dispositivo. Neste caso, tem de esquema do tooinstruct do Azure AD Connect tooread Olá novamente do AD DS e atualizar a sua cache. Esta ação gera também de novo Olá regras de sincronização. Se adicionar o esquema do Exchange Olá, por exemplo, as regras de sincronização de Olá para o Exchange estão adicionadas toohello configuração.

Quando seleciona esta opção, são listados todos os diretórios de Olá na configuração. Pode manter a predefinição de Olá e atualizar todas as florestas ou anule a seleção de algumas delas.

![Página com uma lista de todos os diretórios no ambiente de Olá](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Configurar o modo de teste
Esta opção permite-lhe tooenable e desativar o modo de teste no servidor de Olá. Podem encontrar mais informações sobre testes de modo e como são utilizadas no [operações](active-directory-aadconnectsync-operations.md#staging-mode).

opção de Olá mostra se o teste está atualmente ativada ou desativada:  
![Opção que também está a mostrar o estado atual do Olá do modo de teste](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange Olá Estado, selecione esta opção e selecione ou unselect Olá caixa de verificação.  
![Opção que também está a mostrar o estado atual do Olá do modo de teste](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Alterar a sessão do utilizador
Esta opção permite-lhe toochange toofederation de sincronização de palavra-passe ou Olá inverso. Não é possível alterar demasiado**não configurar**.

Para obter mais informações sobre esta opção, consulte [sessão do utilizador](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre o modelo de configuração de Olá utilizado por uma sincronização do Azure AD Connect no [compreender de aprovisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Tópicos de descrição geral**

* [Sincronização do Azure AD Connect: Noções e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)
