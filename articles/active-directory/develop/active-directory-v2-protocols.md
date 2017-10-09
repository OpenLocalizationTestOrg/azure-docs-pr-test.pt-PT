---
title: "aaaLearn sobre Olá autorização protocolos suportados pelo Azure AD v 2.0 | Microsoft Docs"
description: "Um tooprotocols guia suportado pelo ponto final de v 2.0 do Olá do Azure AD."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5fb4fa1b-8fc4-438e-b3b0-258d8c145f22
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f90511b1880ff223f725c1f79df9f79bddccc7bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# v 2.0 protocolos - OAuth 2.0 & OpenID Connect
ponto final de v 2.0 Olá pode utilizar o Azure AD para identidade-como-um-serviço com protocolos padrão da indústria, OpenID Connect e OAuth 2.0.  Embora seja compatível com normas serviço Olá, pode ser ligeiras diferenças entre as duas implementações destes protocolos.  informações de Olá aqui será útil se escolher toowrite código enviando diretamente & processar pedidos de HTTP ou utilize um 3rd terceiros abrir biblioteca de origem, em vez de utilizar uma das nossas bibliotecas de open source para.
<!-- TODO: Need link toolibraries above -->

> [!NOTE]
> Nem todos os cenários do Azure Active Directory e funcionalidades são suportadas pelo ponto final de v 2.0 Olá.  toodetermine se deve utilizar o ponto final de v 2.0 Olá, leia sobre [limitações de v 2.0](active-directory-v2-limitations.md).
>
>

## Olá Noções básicas
Praticamente todos os fluxos de OAuth & OpenID Connect, existem quatro entidades envolvidas no exchange Olá:

![Funções de OAuth 2.0](../../media/active-directory-v2-flows/protocols_roles.png)

* Olá **autorização servidor** é o ponto final de v 2.0 Olá.  É responsável por assegurar que a identidade do utilizador Olá, conceder revogar acesso tooresources e emitir tokens.  É também conhecida como fornecedor de identidade Olá - -lo em segurança processa nada toodo do utilizador Olá informação, os respetivos acesso e Olá relações de fidedignidade entre as partes de um fluxo.
* Olá **proprietário do recurso** é, geralmente, o utilizador final de Olá.  É terceiros Olá que é proprietário dos dados Olá e tem Olá energia tooallow parties terceira tooaccess essa dados ou ao recurso.
* Olá **cliente OAuth** é a sua aplicação, identificada por um ID de aplicação.  Normalmente, é terceiros Olá que o utilizador final de Olá interage com e que solicita tokens do servidor de autorização de Olá.  cliente de Olá deve ser concedida permissão tooaccess Olá recurso pelo proprietário do recurso Olá.
* Olá **servidor recursos** é onde residem o recurso de Olá ou dados.  Confianças Olá autorização servidor toosecurely autenticar e autorizar Olá cliente OAuth e utiliza portador tooensure access_tokens que acedem a recursos de tooa pode ser concedido.

## Registo de aplicação
Cada aplicação que utiliza o ponto final de v 2.0 Olá terá toobe registar [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) antes de pode interagir com OAuth ou o OpenID Connect.  processo de registo de aplicação Olá irão recolher & atribuir a aplicação de tooyour alguns valores:

* Um **Id da aplicação** que identificam de forma a aplicação
* A **URI de redirecionamento** ou **identificador de pacote** que podem ser utilizados toodirect respostas tooyour back-app
* Alguns outros valores específicos de cenário.

Para obter mais detalhes, saiba como demasiado[registar uma aplicação](active-directory-v2-app-registration.md).

## Pontos Finais
Depois de registado, aplicação Olá comunica com o Azure AD enviando pedidos toohello v 2.0 endpoint:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Onde Olá `{tenant}` pode efetuar uma das quatro valores diferentes:

| Valor | Descrição |
| --- | --- |
| `common` |Permite que os utilizadores com contas Microsoft pessoais e de trabalho/escola contas do Azure Active Directory toosign numa aplicação Olá. |
| `organizations` |Permite que apenas os utilizadores com contas de trabalho/escola do Azure Active Directory toosign numa aplicação Olá. |
| `consumers` |Permite que apenas os utilizadores com pessoal toosign de contas (MSA) da Microsoft na aplicação Olá. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` ou `contoso.onmicrosoft.com` |Permite que apenas os utilizadores com contas de trabalho/profissional de um determinado toosign de inquilino do Azure Active Directory na aplicação Olá.  O nome de domínio amigável de Olá Olá inquilino do Azure AD ou o identificador de guid do inquilino Olá pode ser utilizado. |

Para obter mais informações sobre como toointeract com estes pontos finais, escolha um tipo de aplicação específica abaixo.

## Tokens
implementação de v 2.0 Olá de OAuth 2.0 e o OpenID Connect tornar utilizar muita tokens de portador, incluindo os tokens de portador representados como JWTs. Um token de portador é um token de segurança simples que concede Olá "portador" acesso tooa recurso protegido. Este sentido, Olá "portador" é qualquer entidade que pode apresentar o token de Olá. Embora um terceiros devem primeiro autenticar com o token de portador do Azure AD tooreceive Olá, se Olá necessário passos não são tidas em token de Olá toosecure na transmissão e o armazenamento, podem ser intercetado e utilizado por uma entidade indesejada. Enquanto algumas tokens de segurança tem um mecanismo incorporado para impedir que as partes não autorizadas a utilizá-los, os tokens de portador não têm este mecanismo e tem de ser transportados num canal seguro, como de segurança de camada de transporte (HTTPS). Se um token de portador é transmitido no Olá limpar, um ataque de média de ataques man-in Olá pode ser utilizado por um token de Olá tooacquire malicioso de terceiros e utilizá-lo para um recurso de tooa protegido de acessos não autorizados. Olá princípios de segurança mesmo se aplica quando armazenar ou colocação em cache os tokens de portador para utilização posterior. Certifique-se sempre de que a aplicação transmite e armazena os tokens de portador de forma segura. Para mais considerações de segurança em tokens de portador, consulte [RFC 6750 secção 5](http://tools.ietf.org/html/rfc6750).

Obter mais detalhes dos diferentes tipos de tokens utilizados no ponto final de v 2.0 Olá está disponível no [Olá referência de token de ponto final v 2.0](active-directory-v2-tokens.md).

## Protocolos
Se estiver pronto toosee alguns exemplos de pedidos, começar com uma das Olá abaixo tutoriais.  Cada um deles corresponde tooa cenário de autenticação específica.  Se precisar de ajuda para determinar qual é o fluxo de direito de Olá para si, consulte [Olá tipos de aplicações, pode criar com v 2.0 de Olá](active-directory-v2-flows.md).

* [Criar Mobile e aplicação nativa com OAuth 2.0](active-directory-v2-protocols-oauth-code.md)
* [Criar Web aplicações com abrir ID Connect](active-directory-v2-protocols-oidc.md)
* [Criar aplicações de página única com Olá fluxo implícito de OAuth 2.0](active-directory-v2-protocols-implicit.md)
* [Criar aplicações Daemons ou os processos do lado do servidor com o Olá fluxo de credenciais do OAuth 2.0 cliente](active-directory-v2-protocols-oauth-client-creds.md)
* [Obter os tokens de uma API Web com Olá OAuth 2.0 no nome do fluxo](active-directory-v2-protocols-oauth-on-behalf-of.md)
