---
title: "aaaHow toorequire a autenticação multifator | Microsoft Docs"
description: "Saiba como toorequire multi-factor authentication (MFA) para privilegiado identidades com a extensão do Azure Active Directory Privileged Identity Management Olá."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Como toorequire MFA no Azure AD Privileged Identity Management
Recomendamos que necessitam de autenticação multifator (MFA) para todos os seus administradores. Isto reduz o risco de Olá de um ataque devido a palavra-passe de tooa comprometido.

Pode exigir que os utilizadores ser um desafio MFA quando iniciam sessão no. Olá, mensagem de blogue [MFA para Office 365 e o MFA do Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) compara o que está incluído em subscrições do Office e do Azure, com funcionalidades de Olá contidas na oferta de multi-factor Authentication do Microsoft Azure Olá.

Também pode exigir que os utilizadores ser um desafio MFA quando ativar a uma função no Azure AD PIM. Desta forma, se o utilizador Olá não concluiu um desafio MFA quando que tem sessão iniciada, será pedido toodo Sim pelo PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Exigir a MFA no Azure AD Privileged Identity Management
Quando gerir identidades no PIM como um administrador com função privilegiada, poderá ver alertas que recomendamos MFA para contas com privilégios. Clique em segurança Olá alerta no dashboard do PIM Olá e um novo painel será aberto com uma lista de contas de administrador de Olá deve exigir a MFA.  Pode exigir a MFA selecionando várias funções e, em seguida, clicando em Olá **corrigir** botão, ou pode clique Funções de tooindividual seguintes reticências Olá e, em seguida, clique em Olá **corrigir** botão.

> [!IMPORTANT]
> Agora, direito MFA do Azure só funciona com o trabalho contas escolares ou profissionais, não as contas Microsoft (normalmente, uma conta pessoal que tenha utilizado toosign nos serviços de tooMicrosoft Skype, Xbox, Outlook.com, etc.). Por este motivo, qualquer pessoa com uma conta Microsoft não pode ser um administrador elegível porque estes não podem utilizar MFA tooactivate as respetivas funções. Se estes utilizadores necessitam toocontinue gerir cargas de trabalho através de uma conta Microsoft, efetuar a elevação-los toopermanent administradores por agora.
> 
> 

Além disso, pode alterar o requisito de MFA Olá para uma função específica ao clicar na mesma no Olá secção de funções do dashboard do PIM Olá. Em seguida, clique em **definições** no painel de função Olá e, em seguida, selecionar **ativar** em autenticação multifator.

## <a name="how-azure-ad-pim-validates-mfa"></a>Como o Azure AD PIM valida a MFA
Existem duas opções para validar a MFA quando um utilizador ativa uma função.

a opção mais simples de Olá é toorely na MFA do Azure para utilizadores que esteja a ativar uma função com privilégios. toodo, verifique primeiro se esses utilizadores são licenciados, se necessário e tem registado para MFA do Azure. Obter mais informações sobre como toodo trata [introdução ao Azure multi-factor Authentication na nuvem de Olá](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). É recomendado, mas não ser obrigatório, se configurar o MFA do Azure AD tooenforce para estes utilizadores quando iniciam sessão no. Isto acontece porque as verificações MFA Olá serão efetuadas pelo Azure AD PIM em si.

Em alternativa, se os utilizadores autenticam no local pode ter o seu fornecedor de identidade serão responsáveis pela MFA. Por exemplo, se tiver configurado os serviços de Federação do AD toorequire baseada em smart card a autenticação antes de aceder ao Azure AD, [proteger recursos da nuvem com o Azure multi-factor Authentication e o AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) inclui instruções Para configurar o AD FS toosend afirmações tooAzure AD. Quando um utilizador tenta tooactivate uma função, o Azure AD PIM aceitará que MFA já foi validada para utilizador Olá depois de receber afirmações adequadas Olá.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

