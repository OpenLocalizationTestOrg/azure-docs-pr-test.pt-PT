---
title: "página aaaApplication não ser apresentados corretamente para uma aplicação de Proxy de aplicações | Microsoft Docs"
description: "Documentação de orientação durante a página Olá não está corretamente apresentação de uma aplicação de Proxy de aplicação ter integrado com o Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Página da aplicação não é apresentado corretamente para uma aplicação de Proxy de aplicações

Este artigo ajuda-o tootroubleshoot problemas com aplicações de Proxy de aplicações do Azure Active Directory quando navegar toohello página, mas algo na página Olá não ter um aspeto correto.

## <a name="overview"></a>Descrição geral
Quando publica uma aplicação de Proxy de aplicações, apenas páginas na sua raiz estão acessíveis quando aceder à aplicação Olá. Se a página Olá não apresentar corretamente, Olá raiz URL interno utilizado para a aplicação Olá poderá estar em falta alguns recursos de página. tooresolve, certifique-se tiver publicado *todos os* Olá recursos para a página Olá como parte da sua aplicação.

Pode verificar este é o problema de Olá abrindo o controlador de rede (tais como o Fiddler ou F12 ferramentas no Internet Explorer/Edge), a carregar a página Olá e está à procura de 404 erros. Indica que as páginas de Olá que atualmente não não possível localizar e ainda poderão ter toobe publicado.

Como um exemplo de neste caso, partem do princípio de ter publicado uma aplicação de despesas utilizando um URL interno de <http://myapps/expenses>, mas a folha de estilos Olá utiliza a aplicação Olá <http://myapps/style.css>. Neste caso, Olá folha de estilos não está publicada na sua aplicação, para carregar a aplicação de despesas Olá gerar um erro ao tentar tooload style.css 404. Neste exemplo, seria possível resolver o problema de Olá através da publicação de aplicação Olá com um URL interno de <http://myapp/> em vez disso.

## <a name="problems-with-publishing-as-one-application"></a>Problemas com a publicação como uma aplicação

Se não for possível toopublish Olá, todos os recursos dentro da mesma aplicação, terá toopublish várias aplicações e ativar as ligações entre eles.

toodo por isso, recomendamos a utilização Olá [domínios personalizados](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) solução. No entanto, esta solução requer que detém o certificado de Olá para o seu domínio e as suas aplicações utilizam nomes de domínio completamente qualificado (FQDN). Para outras opções, consulte Olá [resolver problemas de ligações quebrada documentação](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Passos seguintes
[Publicar aplicações através do Proxy de aplicações do Azure AD](application-proxy-publish-azure-portal.md)
