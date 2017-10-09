---
title: "aaaAzure início de sessão único no protocolo SAML | Microsoft Docs"
description: "Este artigo descreve o protocolo de início de sessão único no SAML Olá no Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# Protocolo de SAML do início de sessão único
Este artigo abrange os pedidos de autenticação de Olá SAML 2.0 e as respostas que suporta o Azure Active Directory (Azure AD) para Single Sign-On.

Diagrama de protocolo de Olá abaixo descreve Olá único início de sessão na sequência. Olá serviço em nuvem (fornecedor de serviços de Olá) utiliza um toopass de enlace de redirecionamento de HTTP um `AuthnRequest` (pedido de autenticação) elemento tooAzure AD (fornecedor de identidade Olá). Azure AD, em seguida, utiliza um toopost de enlace de post HTTP um `Response` o serviço em nuvem do elemento toohello.

![Fluxo de trabalho de início de sessão único](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
a enviar de serviços em nuvem toorequest uma autenticação de utilizador, um `AuthnRequest` elemento tooAzure AD. Exemplo de SAML 2.0 `AuthnRequest` foi este aspeto:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parâmetro |  | Descrição |
| --- | --- | --- |
| ID |Necessário |Utiliza o Azure AD Olá de toopopulate este atributo `InResponseTo` atributo de Olá devolvida resposta. ID não tem de começar com um número, pelo que uma estratégia de comum é tooprepend uma cadeia como "id" toohello representação de um GUID. Por exemplo, `id6c1c178c166d486687be4aaf5e482730` é um ID válido. |
| Versão |Necessário |Deve ser **2.0**. |
| IssueInstant |Necessário |Esta é uma cadeia de DateTime com um valor de UTC e [formato reportadas round-trip ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure AD espera um valor de DateTime deste tipo, mas não avaliar ou utilize Olá valor. |
| AssertionConsumerServiceUrl |Opcional |Se for indicado, este tem de corresponder ao hello `RedirectUri` do serviço de nuvem Olá no Azure AD. |
| ForceAuthn |Opcional | Este é um valor booleano. Se for VERDADEIRO, isto significa que o utilizador Olá será toore forçada-autenticar, mesmo que tenha uma sessão válida com o Azure AD. |
| IsPassive |Opcional |Este é um valor booleano que especifica se do Azure AD deve autenticar utilizador Olá silenciosamente, sem interação do utilizador, utilizando o cookie de sessão de Olá se existir. Se for VERDADEIRO, do Azure AD tentará utilizador de Olá tooauthenticate utilizando o cookie de sessão de Olá. |

Todos os outros `AuthnRequest` atributos, tais como o consentimento, destino, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex e ProviderName são **ignoradas**.

Azure AD também ignora Olá `Conditions` elemento `AuthnRequest`.

### emissor
Olá `Issuer` elemento um `AuthnRequest` deve corresponder exatamente um dos Olá **ServicePrincipalNames** num serviço em nuvem de Olá no Azure AD. Normalmente, isto é definido toohello **URI de ID de aplicação** que é especificado durante o registo de aplicação.

Um excerpt SAML de exemplo que contém Olá `Issuer` elemento tem o seguinte aspeto:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Este elemento solicita um formato de ID de nome específico na resposta Olá e é opcional no `AuthnRequest` tooAzure elementos enviados AD.

Um exemplo `NameIdPolicy` elemento tem o seguinte aspeto:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Se `NameIDPolicy` é fornecida, pode incluir o opcional `Format` atributo. Olá `Format` atributo pode ter apenas um dos seguintes valores de Olá; qualquer outro valor resulta num erro.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: O azure Active Directory emite Olá NameID afirmação como um identificador pairwise.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: O azure Active Directory emite Olá NameID afirmação no formato de endereço de correio eletrónico.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Este valor permite que o formato do Azure Active Directory tooselect Olá afirmação. Azure Active Directory emite Olá NameID como um identificador pairwise.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: O azure Active Directory emite Olá NameID afirmação como um valor gerado aleatoriamente, que é uma operação SSO atual toohello exclusivo. Isto significa que o valor de Olá é temporário e não pode ser utilizado tooidentify Olá autenticação de utilizador.

Azure AD ignora Olá `AllowCreate` atributo.

### RequestAuthnContext
Olá `RequestedAuthnContext` elemento Especifica os métodos de autenticação de Olá assim o desejar. É opcional no `AuthnRequest` tooAzure elementos enviados AD. AD do Azure suporta apenas um `AuthnContextClassRef` valor: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Controlo de âmbito
Olá `Scoping` elemento, que inclui uma lista de fornecedores de identidade, é opcional no `AuthnRequest` tooAzure elementos enviados AD.

Se for indicado, não incluem Olá `ProxyCount` atributo, `IDPListOption` ou `RequesterID` elemento, como não são suportados.

### Assinatura
Não incluir um `Signature` elemento `AuthnRequest` elementos, do Azure AD não suporta assinados pedidos de autenticação.

### Assunto
Azure AD ignora Olá `Subject` elemento do `AuthnRequest` elementos.

## Resposta
Quando um pedido início de sessão for concluída com êxito, do Azure AD mensagens do serviço de nuvem de toohello uma resposta. Uma exemplo resposta tooa tentativa com êxito início de sessão tem o seguinte aspeto:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Resposta
Olá `Response` elemento inclui o resultado de Olá do pedido de autorização de Olá. Azure AD define Olá `ID`, `Version` e `IssueInstant` valores Olá `Response` elemento. Também define Olá seguintes atributos:

* `Destination`: Quando o início de sessão for concluída com êxito, é definida toohello `RedirectUri` do fornecedor de serviços de Olá (serviço de nuvem).
* `InResponseTo`: Este é definido toohello `ID` atributo de Olá `AuthnRequest` elemento iniciada resposta Olá.

### emissor
Azure AD define Olá `Issuer` elemento demasiado`https://login.microsoftonline.com/<TenantIDGUID>/` onde <TenantIDGUID> Olá inquilino ID do inquilino Olá do Azure AD.

Por exemplo, uma resposta de exemplo com o elemento de emissor foi este aspeto:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Estado
Olá `Status` elemento transmite êxito Olá ou a falha de início de sessão. Inclui Olá `StatusCode` elemento, que contém um código ou um conjunto de códigos aninhados que representa o estado de Olá do pedido de Olá. Também inclui Olá `StatusMessage` elemento, que contém mensagens de erro personalizadas que são geradas durante o processo de início de sessão Olá.

<!-- TODO: Add a authentication protocol error reference -->

Olá que se segue uma SAML resposta tooan tentativa sem êxito início de sessão.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Asserção
Na adição toohello `ID`, `IssueInstant` e `Version`, do Azure AD define Olá seguintes elementos Olá `Assertion` elemento da resposta de Olá.

#### emissor
Isto estiver definido demasiado`https://sts.windows.net/<TenantIDGUID>/`onde <TenantIDGUID> é Olá ID do inquilino do inquilino Olá do Azure AD.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Assinatura
Azure AD inicia asserção Olá na resposta tooa bem-sucedida início de sessão. Olá `Signature` elemento contém uma assinatura digital que o serviço em nuvem Olá pode utilizar a integridade do tooauthenticate Olá origem tooverify Olá de asserção Olá.

toogenerate utiliza esta assinatura digital, do Azure AD Olá chave de assinatura no Olá `IDPSSODescriptor` elemento do seu documento de metadados.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Assunto
Esta ação Especifica principal Olá que é o assunto Olá de declarações de Olá na asserção Olá. Contém um `NameID` elemento, que representa o utilizador autenticado Olá. Olá `NameID` valor é um identificador de destino que é o fornecedor de serviços de direcionados toohello apenas é público-alvo Olá token Olá. É persistente - podem ser revogado, mas nunca é reatribuído. Também é opaco, em que este não expõe nada sobre utilizador Olá e não pode ser utilizado como um identificador para consultas de atributo.

Olá `Method` atributo de Olá `SubjectConfirmation` elemento é sempre definido demasiado`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Condições
Este elemento Especifica as condições que definem Olá aceitável utilizam de asserções de SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Olá `NotBefore` e `NotOnOrAfter` atributos especifique o intervalo de Olá durante o qual Olá asserção é válida.

* Olá, valor de Olá `NotBefore` atributo é igual tooor ligeiramente (menos de um segundo) posterior ao valor Olá `IssueInstant` atributo de Olá `Assertion` elemento. Azure AD não tem em conta qualquer diferença de tempo entre si próprio e Olá (fornecedor de serviços) do serviço em nuvem e não adiciona qualquer tempo de toothis de memória intermédia.
* Olá, valor de Olá `NotOnOrAfter` atributo é 70 minutos posterior ao valor Olá Olá `NotBefore` atributo.

#### Audiência
Contém um URI que identifique um público-alvo. Azure AD define o valor de Olá do elemento toohello valor `Issuer` elemento de Olá `AuthnRequest` que iniciou Olá início de sessão. Olá tooevaluate `Audience` valor, utilize o valor Olá Olá `App ID URI` que foi especificado durante o registo de aplicação.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Como Olá `Issuer` valor hello `Audience` valor deve corresponder exatamente um dos Olá nomes principais de serviço que representa o serviço em nuvem Olá no Azure AD. No entanto, se hello valor de Olá `Issuer` elemento não é um valor URI, hello `Audience` valor na resposta Olá é Olá `Issuer` valor o prefixo `spn:`.

#### AttributeStatement
Contém afirmações sobre o assunto Olá ou utilizador. Olá excerpt seguinte contém uma amostra `AttributeStatement` elemento. botão de reticências Olá indica que o elemento Olá pode incluir vários atributos e valores de atributo.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Nome de afirmação** : Olá valor Olá `Name` atributo (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) está Olá nome principal de utilizador utilizador de Olá autenticado, tais como `testuser@managedtenant.com`.
* **ObjectIdentifier afirmação** : Olá valor Olá `ObjectIdentifier` atributo (`http://schemas.microsoft.com/identity/claims/objectidentifier`) é Olá `ObjectId` do objeto de diretório de Olá representa Olá autenticado o utilizador no Azure AD. `ObjectId`é um imutável globalmente exclusivo e reutilização identificador seguro de Olá autenticado o utilizador.

#### AuthnStatement
Este elemento asserções que esse assunto de asserção Olá foi autenticado por um meio específico num determinado momento.

* Olá `AuthnInstant` atributo especifica o tempo de Olá pelo utilizador que Olá autenticado com o Azure AD.
* Olá `AuthnContext` elemento Especifica o contexto de autenticação de Olá utilizado utilizador de Olá tooauthenticate.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```