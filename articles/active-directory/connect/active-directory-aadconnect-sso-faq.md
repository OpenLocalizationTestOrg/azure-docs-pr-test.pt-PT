---
title: 'O Azure AD Connect: Totalmente integrada Single Sign-On - perguntas mais frequentes | Microsoft Docs'
description: Perguntas mais sobre o Azure Active Directory totalmente integrada Single Sign-On toofrequently de respostas.
services: active-directory
keywords: "o que é o Azure AD Connect, a instalação do Active Directory, os componentes necessários para o Azure AD, SSO, o início de sessão único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Azure Active Directory totalmente integrada Single Sign-On: Perguntas mais frequentes

Neste artigo, vamos abordar perguntas mais frequentes sobre o Azure Active Directory totalmente integrada Single Sign-On (SSO totalmente integrado). Manter a verificação para o novo conteúdo.

>[!IMPORTANT]
>funcionalidade de SSO totalmente integrado Olá está atualmente em pré-visualização.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Os métodos de início de sessão funcionam SSO totalmente integrado com?

SSO totalmente integrado pode ser combinada com qualquer um dos Olá [sincronização de Hash de palavra-passe](active-directory-aadconnectsync-implement-password-synchronization.md) ou [autenticação pass-through](active-directory-aadconnect-pass-through-authentication.md) métodos de início de sessão. No entanto esta funcionalidade não pode ser utilizada com serviços de Federação do Active Directory (ADFS).

## <a name="is-seamless-sso-a-free-feature"></a>É uma funcionalidade livre de SSO totalmente integrado?

SSO totalmente integrada é uma funcionalidade livre e não precisa de quaisquer edições pagas do Azure AD toouse-lo. Continua a ser livre quando a funcionalidade de Olá atinge disponibilidade geral.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Que aplicações tirar partido das `domain_hint` ou `login_hint` capacidade de parâmetro do SSO totalmente integrado?

Estamos no processo de Olá da lista de Olá das aplicações que enviar estes parâmetros e Olá aqueles que não a compilação. Se tiver aplicações estão interessadas nas, indique na secção de comentários de Olá.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Suporta SSO totalmente integrado `Alternate ID` como Olá nome de utilizador, em vez de `userPrincipalName`?

Sim. Suporta SSO totalmente integrado `Alternate ID` como Olá nome de utilizador quando configurados no Azure AD Connect, conforme mostrado [aqui](active-directory-aadconnect-get-started-custom.md). Nem todas as aplicações do Office 365 suportam `Alternate ID`. Consulte a documentação da aplicação toohello específico para a declaração de suporte de Olá.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Quero tooregister não - Windows 10 dispositivos com o Azure AD, sem utilizar o AD FS. Posso utilizar o SSO totalmente integrada em vez disso?

Sim, este cenário precisa de versão 2.1 ou posterior do Olá [cliente associação à área de trabalho](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Como pode posso rollover de chave de desencriptação de Kerberos Olá de Olá `AZUREADSSOACCT` conta de computador?

É importante toofrequently rollover de chave de desencriptação de Kerberos Olá de Olá `AZUREADSSOACCT` conta de computador (que representa o Azure AD) criada no seu local floresta do AD.

>[!IMPORTANT]
>Recomendamos vivamente que lhe rollover de chave de desencriptação de Kerberos Olá, pelo menos, a cada 30 dias.

Siga estes passos em Olá local no servidor onde está a executar o Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Passo 1. Obter a lista de florestas do AD onde SSO totalmente integrada foi ativada

1. Em primeiro lugar, transferir e instalar Olá [assistente Microsoft Online Services início de sessão](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Em seguida, transferir e instalar Olá [módulo do Azure Active Directory de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` pasta.
4. Módulo PowerShell do SSO totalmente integrado Olá de importação utilizando este comando: `Import-Module .\AzureADSSO.psd1`.
5. Execute o PowerShell como administrador. No PowerShell, chame `New-AzureADSSOAuthenticationContext`. Este comando deverá dar-lhe um pop-up tooenter credenciais de Administrador Global do inquilino.
6. Chamar `Get-AzureADSSOStatus`. Este comando fornece que Olá lista de florestas do AD (olhos a lista de domínios"Olá") em que esta funcionalidade foi ativada.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Passo 2. Atualizar a chave de desencriptação de Kerberos Olá em cada floresta do AD que este foi configurá-lo no

1. Chamar `$creds = Get-Credential`. Quando lhe for pedido, introduza as credenciais de administrador de domínio de Olá para Olá se destina a floresta do AD.
2. Chamar `Update-AzureADSSOForest -OnPremCredentials $creds`. Este comando atualizações Olá chave de desencriptação de Kerberos para Olá `AZUREADSSOACCT` conta de computador nesta floresta específica do AD e atualiza-o no Azure AD.
3. Repita Olá precedente passos para cada floresta do AD que tiver configurado a funcionalidade de Olá no.

>[!IMPORTANT]
>Certifique-se de que _não_ executar Olá `Update-AzureADSSOForest` comando mais do que uma vez. Caso contrário, a funcionalidade de Olá deixa de funcionar até que o tempo de Olá permissões de Kerberos dos seus utilizadores expirarem e são emitido novamente pelo seu Active Directory no local.

## <a name="how-can-i-disable-seamless-sso"></a>Como desativar a SSO totalmente integrado?

Pode ser desativado SSO totalmente integrado com o Azure AD Connect.

Executar o Azure AD Connect, escolha "Alterar utilizador-página sessão" e clique em "Seguinte". Em seguida, desmarque a opção "Ativar início de sessão único" de Olá. Continue através do Assistente de Olá. Após a conclusão do Assistente de Olá, SSO totalmente integrado está desativado no seu inquilino.

No entanto, verá uma mensagem no ecrã que lê da seguinte forma:

"O início de sessão único está agora desactivado, mas existem passos manuais adicionais tooperform na ordem toocomplete limpeza. Saiba mais"

toocomplete Olá processo, siga estes passos manuais Olá no-server no local onde está a executar o Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Passo 1. Obter a lista de florestas do AD onde SSO totalmente integrada foi ativada

1. Em primeiro lugar, transferir e instalar Olá [assistente Microsoft Online Services início de sessão](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Em seguida, transferir e instalar Olá [módulo do Azure Active Directory de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Navegue toohello `%programfiles%\Microsoft Azure Active Directory Connect` pasta.
4. Módulo PowerShell do SSO totalmente integrado Olá de importação utilizando este comando: `Import-Module .\AzureADSSO.psd1`.
5. Execute o PowerShell como administrador. No PowerShell, chame `New-AzureADSSOAuthenticationContext`. Este comando deverá dar-lhe um pop-up tooenter credenciais de Administrador Global do inquilino.
6. Chamar `Get-AzureADSSOStatus`. Este comando fornece que Olá lista de florestas do AD (olhos a lista de domínios"Olá") em que esta funcionalidade foi ativada.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Passo 2. Elimine manualmente Olá `AZUREADSSOACCT` conta de computador de cada floresta do AD que vê listados.

## <a name="next-steps"></a>Passos seguintes

- [**Início Rápido** ](active-directory-aadconnect-sso-quick-start.md) - obter cópias de segurança e executar o SSO totalmente integrada de AD do Azure.
- [**Descrição detalhada da Technical** ](active-directory-aadconnect-sso-how-it-works.md) -compreender como funciona esta funcionalidade.
- [**Resolver problemas** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comuns problemas com a funcionalidade de Olá.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - para apresentação de pedidos de funcionalidades de novo.
