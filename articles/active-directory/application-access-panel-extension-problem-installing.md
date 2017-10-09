---
title: "aaaProblem instalar a extensão de browser de painel de acesso de aplicação de Olá | Microsoft Docs"
description: "Como erros comuns toofix encontrado ao instalar a extensão de browser de painel de acesso de Olá"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 5f750d12c5f9b405ec4f81596d5cc5e0a48f9a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-access-panel-browser-extension"></a>Instalar a extensão de browser de painel de acesso de aplicação de Olá do problema

Olá painel de acesso é um portal baseado na web que permitem que um utilizador que possua uma empresa ou escola da conta do Azure Active Directory (Azure AD) tooview e inicie baseado na nuvem aplicações esse administrador Olá do Azure AD concedeu-lhes acesso. Um utilizador que possua as edições do Azure AD também pode utilizar grupos self-service e capacidades de gestão de aplicações através de Olá painel de acesso. Olá painel de acesso separado do Olá portal do Azure e não necessita que os utilizadores toohave uma subscrição do Azure.

toouse baseada em palavra-passe-início de sessão único (SSO) no painel de acesso, Olá extensão do painel de acesso de Olá tem de estar instalado no browser do utilizador Olá. Esta extensão é transferida automaticamente quando um utilizador seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Que cumprem os requisitos de browser para Olá painel de acesso

Olá painel de acesso necessita de um browser que suporte JavaScript e ativou CSS. toouse baseada em palavra-passe-início de sessão único (SSO) no painel de acesso, Olá extensão do painel de acesso de Olá tem de estar instalado no browser do utilizador Olá. Esta extensão é transferida automaticamente quando um utilizador seleciona uma aplicação que está configurada para SSO baseada em palavra-passe.

Para SSO baseada em palavra-passe, podem ser browsers do utilizador final Olá:

-   Internet Explorer 8, 9, 10, 11 - no Windows 7 ou posterior

-   Limite de aniversário da edição do Windows 10 ou posterior 

-   Chrome – No Windows 7 ou posterior e no MacOS X ou posterior

-   Firefox 26.0 ou posterior – no Windows XP SP2 ou posterior e no Mac OS X 10.6 ou posterior

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Como tooinstall Olá extensão de Browser do painel de acesso

Olá tooinstall extensão de Browser do painel de acesso, siga os passos de Olá abaixo:

1.  Abra Olá [painel de acesso](https://myapps.microsoft.com) dos browsers Olá suportado e inicie sessão como um **utilizador** no seu Azure AD.

2.  Clique num **aplicação de palavra-passe SSO** no Olá painel de acesso.

3.  Olá prompt perguntar tooinstall Olá software, selecione **instalar agora**.

4.  Com base no seu browser ser toohello direcionados hiperligação de transferência. **Adicionar** browser de tooyour Olá extensão.

5.  Se o browser pede-lhe, selecione tooeither **ativar** ou **permitir** Olá extensão.

6.  Uma vez instalado, **reiniciar** a sessão do browser.

7.  Inicie sessão no painel de acesso de Olá e veja se pode **iniciar** as aplicações de SSO de palavra-passe

Também pode transferir a extensão de Olá para Chrome e limite de ligações diretas de Olá abaixo:

-   [Extensão de painel de acesso do Chrome](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Extensão de painel de acesso de limite](https://www.microsoft.com/store/apps/9pc9sckkzk84) 

## <a name="setting-up-a-group-policy-for-internet-explorer"></a>Configurar uma política de grupo para o Internet Explorer

Pode configurar uma política de grupo que lhe permitem extensão do tooremotely instalação Olá painel de acesso para o Internet Explorer em máquinas dos seus utilizadores.

Pré-requisitos de Olá incluem:

-   Configurou [serviços de domínio do Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), e associar domínio de tooyour de máquinas dos seus utilizadores.

-   Tem de ter Olá "Editar as definições" permissão tooedit Olá objeto de política de grupo (GPO). Por predefinição, os membros Olá seguintes grupos de segurança têm esta permissão: os administradores do domínio, administradores da empresa e proprietários de criador de política de grupo. [Saiba mais](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).

Siga o tutorial Olá [como tooDeploy Olá a extensão do painel de acesso para o Internet Explorer utilizando a política de grupo](active-directory-saas-ie-group-policy.md) para instruções passo a passo sobre como tooconfigure Olá política de grupo e implementá-la toousers.

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a>Resolver problemas de Olá painel de acesso no Internet Explorer

Siga Olá [Olá de resolução de problemas extensão do painel de acesso para o Internet Explorer](active-directory-saas-ie-troubleshooting.md) guia para acesso de uma ferramenta de diagnóstico e instruções passo a passo sobre como configurar a extensão de Olá de i/e.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Se estes passos de resolução de problemas não resolver o problema de Olá

Abra um pedido de suporte com Olá se disponíveis os seguintes informações:

-   ID de correlação de erro

-   UPN (endereço de e-mail do utilizador)

-   TenantID

-   Tipo de browser

-   Fuso horário e tempo/período de tempo durante o erro ocorre

-   Rastreios de fiddler

## <a name="next-steps"></a>Passos seguintes
[O que é o acesso a aplicações e início de sessão no Azure Active Directory?](active-directory-appssoaccess-whatis.md)
