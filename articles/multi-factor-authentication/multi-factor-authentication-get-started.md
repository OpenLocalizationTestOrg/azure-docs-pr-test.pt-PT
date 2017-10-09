---
title: aaaChoose entre a nuvem do MFA do Azure ou de servidor | Microsoft Docs
description: "Escolha a solução de segurança de autenticação multifator Olá é adequada para si ao perguntar, que am posso tentava toosecure e onde estão os meus utilizadores localizado.  Em seguida, selecione a nuvem, o servidor MFA ou o AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Escolher a solução de Azure multi-factor Authentication de Olá por si
Porque existem vários tipos de multi-factor Authentication (MFA) do Azure, é necessário responder a algumas perguntas toofigure, saída qual é a versão é Olá adequada, um toouse.  Estas perguntas são:

* [O que estou a tentar posso toosecure](#what-am-i-trying-to-secure)
* [Onde estão localizados os utilizadores de Olá](#where-are-the-users-located)
* [Que funcionalidades preciso?](#what-featured-do-i-need)

Olá secções seguintes fornecem orientações sobre como determinar cada uma destas respostas.

## <a name="what-am-i-trying-toosecure"></a>O que estou a tentar posso toosecure?
solução de verificação de dois passos correto de Olá toodetermine, primeiro é necessário responder pergunta sobre Olá que estão a tentar toosecure com um segundo método de autenticação.  É uma aplicação que está no Azure?  Ou um sistema de acesso remoto?  Através da determinação de está a tentar toosecure, iremos pode responder Olá pergunta sobre onde multi-factor Authentication tem de toobe ativada.  

| Quais são toosecure tentar | MFA na nuvem de Olá | Servidor MFA |
| --- |:---:|:---:|
| Aplicações Microsoft originais |● |● |
| Aplicações de SaaS na Galeria de aplicações de Olá |● |  |
| Aplicações Web publicadas através do Proxy de Aplicação do Azure AD |● |  |
| Aplicações IIS não publicadas através do Proxy de Aplicação do Azure AD | |● |
| Acesso remoto, tais como VPN, RDG | ● | ● |

## <a name="where-are-hello-users-located"></a>Onde estão localizados os utilizadores de Olá
Em seguida, observar onde estão localizados os nossos utilizadores ajuda toodetermine Olá solução correta toouse, se na nuvem de Olá ou Olá, no local com o servidor MFA.

| Localização do Utilizador | MFA na nuvem de Olá | Servidor MFA |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD e AD no local utilizando federação com o AD FS |● |● |
| Azure AD e AD no local utilizando DirSync, Azure AD Sync, Azure AD Connect - sem sincronização de palavras-passe |● |● |
| Azure AD e AD no local utilizando DirSync, Azure AD Sync, Azure AD Connect - com sincronização de palavras-passe |● | |
| Active Directory no local | |● |

## <a name="what-features-do-i-need"></a>Que funcionalidades preciso?
Olá tabela seguinte compara as funcionalidades de Olá que estão disponíveis com multi-factor Authentication na nuvem de Olá e com Olá servidor multi-factor Authentication.

| Funcionalidade | MFA na nuvem de Olá | Servidor MFA |
| --- |:---:|:---:|
| Notificação da aplicação móvel como um segundo fator | ● | ● |
| Código de verificação da aplicação móvel como um segundo fator | ● | ● |
| Chamada telefónica como segundo fator | ● | ● |
| SMS unidirecional como segundo fator | ● | ● |
| SMS bidirecional como segundo fator | | ● |
| Tokens de Hardware como segundo fator | | ● |
| Palavras-passe da aplicação para os clientes do Office 365 que não suportam MFA | ● | |
| Controlo de administração sobre métodos de autenticação | ● | ● |
| Modo PIN | | ● |
| Alerta de fraudes |● | ● |
| Relatórios do MFA |● | ● |
| Omissão de Uso Individual | | ● |
| Saudações personalizadas para chamadas telefónicas | ● | ● |
| ID do autor da chamada personalizável para chamadas telefónicas | ● | ● |
| IPs Fidedignos | ● | ● |
| Memorizar MFA para dispositivos fidedignos | ● | |
| Acesso condicional | ● | ● |
| Cache |  | ● |

## <a name="next-steps"></a>Passos seguintes

Agora que Determinámos se toouse na nuvem a autenticação multifator ou Olá servidor MFA no local, podemos começar a configurar e utilizar o Azure multi-factor Authentication. **Selecione o ícone de Olá que representa o seu cenário**

<center>




[![Cloud](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![Servidor](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
