---
title: "aaaAzure do Active Directory restrições e limitações de ponto final v 2.0 | Microsoft Docs"
description: "Uma lista de limitações e restrições para o ponto final de v 2.0 Olá do Azure AD."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>Deve utilizar ponto final de v 2.0 Olá?
Quando criar aplicações que se integram com o Azure Active Directory, terá de toodecide se protocolos de autenticação e de ponto final de v 2.0 do Olá as suas necessidades. Ponto final do Azure do Active Directory original é ainda totalmente suportado e, em alguns aspetos, é mais avançada funcionalidade de v 2.0. No entanto, Olá ponto final v 2.0 [apresenta as vantagens significativas](active-directory-v2-compare.md) para programadores.

Segue-se a nossa recomendação simplificada para programadores neste ponto no tempo:

* Caso seja necessário suportar contas Microsoft pessoais na sua aplicação, utilize o ponto final de v 2.0 Olá. Mas antes de efetuar, lembre-se de que compreende as limitações de Olá que discutimos neste artigo.
* Se a aplicação só tem toosupport trabalho da Microsoft e contas profissional, não utilize o ponto final de v 2.0 Olá. Em vez disso, consulte tooour [guia para programadores do Azure AD](active-directory-developers-guide.md).

Ao longo do tempo, o ponto final de v 2.0 Olá irá aumentar as restrições de Olá tooeliminate listadas aqui, para que apenas irá necessitar ponto final de v 2.0 do toouse Olá. Olá entretanto, este artigo é toohelp que se destinam a determinar se o ponto final de v 2.0 Olá é adequada para si. Vamos continuar tooupdate este artigo tooreflect Olá estado atual do ponto final de v 2.0 Olá. Verificação de fazer uma cópia tooreevaluate os requisitos de capacidades de v 2.0.

Se tiver uma aplicação do Azure AD existente que não utiliza o ponto final de v 2.0 Olá, não há nenhum toostart necessário a partir do zero. No futuro, Olá, iremos irá fornecer uma forma toouse as aplicações do Azure AD existentes com o ponto final de v 2.0 Olá.

## <a name="restrictions-on-app-types"></a>Restrições em tipos de aplicação
Atualmente, hello seguintes tipos de aplicações não são suportados pelo ponto final de v 2.0 Olá. Para obter uma descrição dos tipos de aplicação suportados, consulte [tipos de aplicação para o ponto final de v 2.0 do Azure Active Directory Olá](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>APIs da Web autónoma
Pode utilizar o ponto final de v 2.0 Olá demasiado[criar uma API Web que está protegida com OAuth 2.0](active-directory-v2-flows.md#web-apis). No entanto, essa API Web pode receber tokens apenas a partir de uma aplicação que tem Olá a mesma aplicação um ID. Não é possível aceder a uma API Web de um cliente que tenha um ID de aplicação diferente. cliente de Olá não ser capaz de toorequest ou obter permissões tooyour Web API.

toosee como toobuild uma API Web que aceita tokens a partir de um cliente que tenha Olá mesmo ID de aplicação, consulte Olá amostras de Web API de ponto final v 2.0 no nosso [introdução](active-directory-appmodel-v2-overview.md#getting-started) secção.

## <a name="restrictions-on-app-registrations"></a>Restrições de registos de aplicação
Atualmente, para cada aplicação que pretende que o toointegrate com o ponto final de v 2.0 Olá, tem de criar um registo de aplicação no Olá novo [Portal de registo de aplicações do Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). Existente do Azure AD ou aplicações da conta Microsoft não são compatíveis com o ponto final de v 2.0 Olá. As aplicações que estão registadas em qualquer portal diferente Olá Portal de registo de aplicação não são compatíveis com o ponto final de v 2.0 Olá. Olá futura, vamos planear tooprovide toouse uma forma uma aplicação existente como uma aplicação v 2.0. Atualmente, no entanto, não há nenhum caminho de migração para um toowork aplicação existente com o ponto final de v 2.0 Olá.

Além disso, os registos de aplicações que criar no Olá [Portal de registo de aplicação](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ter Olá seguintes limitações:

* Apenas dois segredos de aplicação são permitidos por ID de aplicação.
* Um registo de aplicação, registado por um utilizador com uma conta Microsoft pessoal, pode ser visualizado e gerido apenas por uma conta de programador único. Não é possível partilhar entre vários programadores.  Se quiser tooshare registo da aplicação entre vários programadores, pode criar aplicação Olá ao iniciar sessão portal de registo de Olá com uma conta do Azure AD.
* Existem várias restrições no formato de Olá de redirecionamento Olá URI que é permitida. Para obter mais informações sobre redirecionamento URIs, consulte a secção seguinte Olá.

## <a name="restrictions-on-redirect-uris"></a>Restrições no URI de redirecionamento
Atualmente, as aplicações que são registadas no Olá Portal de registo de aplicação são tooa restrito limitada de conjunto de valores URI de redirecionamento. Olá redirecionamento URI para serviços e aplicações web têm de começar com o esquema de Olá `https`, e todos os valores URI de redirecionamento têm de partilhar um único domínio DNS. Por exemplo, não é possível registar uma aplicação web que tem um destes URI de redirecionamento:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

sistema de registo Olá compara o nome DNS todo Olá de Olá existente redirecionamento toohello DNS nome URI de redirecionamento Olá URI que estiver a adicionar. o nome DNS do Olá pedido tooadd Olá irá falhar se alguma das Olá seguintes condições for verdadeira:  

* nome DNS completo Olá de URI de redirecionamento do novo Olá não corresponde ao nome DNS Olá de URI de redirecionamento existente Olá.
* Olá nome DNS completo do URI de redirecionamento do novo Olá não é um subdomínio do URI de redirecionamento existente Olá.

Por exemplo, se a aplicação Olá tiver este URI de redirecionamento:

`https://login.contoso.com`

Pode adicionar tooit, como esta:

`https://login.contoso.com/new`

Neste caso, o nome DNS Olá corresponde exatamente. Ou pode fazer o seguinte:

`https://new.login.contoso.com`

Neste caso, está a referenciar tooa subdomínio DNS login.contoso.com. Se quiser toohave uma aplicação que tenha início de sessão east.contoso.com e west.contoso.com início de sessão como os URIs de redirecionamento, tem de adicionar que os URIs de redirecionamento pela seguinte ordem:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

Pode adicionar Olá última dois porque são subdomínios de Olá primeiro URI de redirecionamento, contoso.com. Esta limitação será removida de uma versão futura.

toolearn como tooregister uma aplicação no Olá Portal de registo de aplicação, consulte [como tooregister uma aplicação com o ponto final de v 2.0 Olá](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Restrições sobre serviços e APIs
Atualmente, o ponto final de v 2.0 Olá suporta início de sessão para qualquer aplicação que está registado no Olá Portal de registo de aplicação e que está na lista de Olá de [suportada autenticação fluxos](active-directory-v2-flows.md). No entanto, estas aplicações podem obter tokens de acesso de OAuth 2.0 para um conjunto muito limitado de recursos. problemas de ponto final de v 2.0 Olá apenas para os tokens de acesso:

* aplicação Olá que pedidos de token de Olá. Uma aplicação pode adquirir um token de acesso para si, se a aplicação lógica Olá é composta por vários componentes diferentes ou camadas. toosee este cenário na ação, consulte a nossa [introdução](active-directory-appmodel-v2-overview.md#getting-started) tutoriais.
* Olá correio do Outlook, calendário e APIs REST de contactos, todos os que estão localizados em https://outlook.office.com. toolearn como toowrite uma aplicação que acede a estas APIs, ver Olá [Office introdução](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) tutoriais.
* APIs de Microsoft Graph. Pode saber mais sobre [Microsoft Graph](https://graph.microsoft.io) e dados Olá tooyou disponível.

Outros serviços não são suportados neste momento. Mais Microsoft Online Services será adicionado em Olá futura, além disso toosupport para sua própria personalizada APIs da Web e serviços.

## <a name="restrictions-on-libraries-and-sdks"></a>Restrições na SDKs e de bibliotecas
Atualmente, o suporte de biblioteca para o ponto final de v 2.0 Olá está limitado. Se pretender que o ponto final de v 2.0 do toouse Olá numa aplicação de produção, tem estas opções:

* Se está a criar uma aplicação web, pode utilizar com segurança Microsoft middleware geralmente disponível do lado do servidor tooperform início de sessão e token validação. Estes incluem Olá OWIN abrir ID Connect middleware para ASP.NET e Olá Node.js Passport Plug-in. Para exemplos de código que utilizam o middleware da Microsoft, consulte a nossa [introdução](active-directory-appmodel-v2-overview.md#getting-started) secção.
* Se está a criar uma aplicação de ambiente de trabalho ou de dispositivo móvel, pode utilizar uma das nossa bibliotecas de autenticação da Microsoft (MSAL) de pré-visualização.  Estas bibliotecas estão na pré-visualização suportado de produção, pelo que é seguro toouse-los em aplicações de produção. Pode ler mais sobre os termos de Olá de Olá de pré-visualização e Olá bibliotecas disponíveis no nosso [referência de bibliotecas de autenticação](active-directory-v2-libraries.md).
* Para plataformas não abrangidas por bibliotecas Microsoft, pode integrar com o ponto final de v 2.0 Olá por diretamente enviar e receber mensagens de protocolo no código da aplicação. Olá v 2.0 OpenID Connect e OAuth protocolos [explicitamente estão documentados](active-directory-v2-protocols.md) toohelp efetuar essa uma integração.
* Por fim, pode utilizar a open source abrir ID Connect e OAuth bibliotecas toointegrate com o ponto final de v 2.0 Olá. protocolo de v 2.0 Olá deve ser compatível com muitos bibliotecas de open source protocolo sem alterações principais. disponibilidade de Olá destes tipos de bibliotecas varia consoante a plataforma e de idioma. Olá [abrir ID Connect](http://openid.net/connect/) e [OAuth 2.0](http://oauth.net/2/) sites manter uma lista de implementações populares. Para obter mais informações, consulte [bibliotecas de v 2.0 e a autenticação do Azure Active Directory](active-directory-v2-libraries.md)e Olá à lista de bibliotecas de cliente de open source e exemplos de que foi testados com o ponto final de v 2.0 Olá.

## <a name="restrictions-on-protocols"></a>Restrições de protocolos
ponto final de v 2.0 Olá não suporta SAML ou WS-Federation; só suporta abrir ID Connect e OAuth 2.0.  Nem todas as funcionalidades e capacidades de protocolos de OAuth tem sido incorporadas no ponto final de v 2.0 Olá. Estas capacidades e funcionalidades do protocolo atualmente são *não está disponível* no ponto final de v 2.0 Olá:

* Tokens de ID, que são emitidos pelo ponto final de v 2.0 Olá não contêm um `email` de afirmações de utilizador de Olá, mesmo se adquirir permissão a partir da Olá utilizador tooview ao respetivo e-mail.
* ponto final de OpenID Connect UserInfo Olá não está implementado no ponto final de v 2.0 Olá. No entanto, todos os dados de perfil de utilizador que potencialmente seria receberá neste ponto final está disponível no Olá Microsoft Graph `/me` ponto final.
* ponto final de v 2.0 Olá não suporta afirmações emissoras de função ou grupo em tokens de ID.
* Olá [concessão de credenciais de palavra-passe do OAuth 2.0 recursos proprietário](https://tools.ietf.org/html/rfc6749#section-4.3) não é suportado pelo ponto final de v 2.0 Olá.

No addtion, ponto final de v 2.0 Olá não suporta protocolos de WS-Federation ou qualquer outra forma de Olá SAML.

toobetter compreender o âmbito de Olá da funcionalidade de protocolo suportado no ponto final de v 2.0 Olá, leia a nossa [referência do protocolo OpenID Connect e OAuth 2.0](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Restrições para contas profissional e escolar
Se utilizou o Active Directory Authentication Library (ADAL) em aplicações do Windows, poderá ter demorado partido da autenticação integrada do Windows, que utiliza a concessão de asserção Olá Security Assertion Markup Language (SAML). Com esta concessão, os utilizadores de federado do Azure AD os inquilinos podem autenticar silenciosamente com as respetivas instâncias de Active Directory no local sem introduzir as credenciais. Atualmente, a concessão de asserção SAML de Olá não é suportada no ponto final de v 2.0 Olá.
