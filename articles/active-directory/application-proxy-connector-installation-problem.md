---
title: "instalar aaaProblem Olá conector do agente de Proxy de aplicações | Microsoft Docs"
description: "Como tootroubleshoot problemas que poderá Olá, enfrentam ao instalar o conector do agente de Proxy de aplicações"
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
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a>Problema Olá conector do agente de Proxy de aplicações a instalar

Conector do Proxy de aplicações do Microsoft AAD é um componente de domínio interno que utiliza a conectividade de Olá tooestablish de ligações de saída do domínio interno do Olá nuvem ponto final disponível toohello.

## <a name="general-problem-areas-with-connector-installation"></a>Áreas de problema geral com a instalação do conector

Quando a instalação de Olá de um conector falha, causa de raiz de Olá é normalmente uma das Olá seguintes áreas:

1.  **Conectividade** – toocomplete uma instalação com êxito, Olá tooregister de necessidades do novo conector e estabelecer propriedades de fidedignidade futuras. Isto é feito através da ligação toohello serviço de nuvem do Proxy de aplicações do AAD.

2.  **Estabelecimento de confiança** – novo conector de Olá cria um certificado autoassinado e regista toohello o serviço em nuvem.

3.  **Autenticação de Olá, admin** – durante a instalação, Olá utilizador tem de fornecer credenciais de administrador de instalação de conectores toocomplete Olá.

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a>Certifique-se de que serviço de Proxy de aplicações de nuvem de toohello de conectividade e página Microsoft Login

**Objetivo:** Certifique-se de que a máquina conector Olá pode ligar-se de ponto final do registo de Proxy de aplicações do AAD toohello, bem como a página de início de sessão da Microsoft.

1.  Abra um toohello browser e aceda a seguinte página web: <https://aadap-portcheck.connectorporttest.msappproxy.net> e certifique-se de que tooCentral de conectividade Olá E.U.A. e centros de dados de EUA Leste com as portas 9090 e 9091 está a funcionar.

2.  Se qualquer um dessas portas não for bem sucedida (não tem uma marca de verificação verde), certifique-se de que Olá Firewall ou tem o proxy de back-end \*. msappproxy.net com portas 9090 e 9091 definido corretamente.

3.  Abra um browser (separador separado) e aceda toohello seguir página web: <https://login.microsoftonline.com>, certifique-se de que pode iniciar sessão toothat página.

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a>Certifique-se de que os componentes de máquina e back-end suportem para o certificado de confiança do Proxy de aplicações

**Objetivo:** Certifique-se de que a máquina de conector Olá, back-end proxy e firewall do podem suportar certificado Olá criado pelo conector Olá confiança futuras.

>[!NOTE]
>conector Olá tenta toocreate um certificado de SHA512 que é suportado pelo TLS1.2. Se a máquina Olá ou firewall back-end de Olá e proxy não suportar TLS1.2, instalação de Olá falhar.
>
>

**problema de Olá tooresolve:**

1.  Certifique-se a máquina de Olá suporta TLS1.2 – versões de todas as janelas após 2012 R2 devem suportar TLS 1.2. Se a máquina de conector está a partir de uma versão do 2012 R2 ou versões anteriores, certifique-se de que Olá KBs seguintes estão instalados na máquina de Olá: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2>

2.  Contacte o administrador de rede e peça tooverify que Olá back-end proxy e de firewall não bloqueia SHA512 para tráfego de saída.

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a>Certifique-se de administração utilizados tooinstall Olá conector

**Objetivo:** Certifique-se de que o utilizador Olá que tenta conector de Olá tooinstall é um administrador com as credenciais corretas. Atualmente, Olá utilizador tem de ser um administrador global para Olá toosucceed de instalação.

**as credenciais de Olá tooverify estão corretas:**

Ligar demasiado<https://login.microsoftonline.com> e utilize Olá as mesmas credenciais. Certifique-se de que o início de sessão Olá é efetuada com êxito. Pode verificar a função de utilizador Olá acedendo demasiado**do Azure Active Directory**  - &gt; **utilizadores e grupos**  - &gt; **todos os utilizadores**. 

Selecione a sua conta de utilizador, em seguida, "função de diretório" no menu resultante Olá. Certifique-se de que essa função selecionada Olá é "Administrador Global". Se não é possível tooaccess qualquer um dos Olá páginas ao longo estes passos, não é um administrador global.

## <a name="next-steps"></a>Passos seguintes
[Compreender os conectores de Proxy de aplicações do Azure AD](application-proxy-understand-connectors.md)
