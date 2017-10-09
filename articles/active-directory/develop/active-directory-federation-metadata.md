---
title: "aaaAzure AD metadados da Federação | Microsoft Docs"
description: "Este artigo descreve o documento de metadados de Federação Olá publica do Azure Active Directory para serviços que aceitam tokens do Azure Active Directory."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a>Metadados de federação
Azure Active Directory (Azure AD) publica um documento de metadados de Federação para serviços que é configurada tokens de segurança de Olá tooaccept que o Azure AD emite. Olá formato do documento de metadados de Federação está descrito em Olá [idioma de Federação de serviços Web (WS-Federation) versão 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que expande [metadados para Olá OASIS Security Assertion Markup Language (SAML) v 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Inquilino específico e os pontos finais de metadados do inquilino independentes
Azure AD publica pontos finais de inquilino específico e independente de inquilino.

Pontos finais de inquilino específico foram concebidos para um determinado inquilino. metadados de Federação de inquilino específico Olá incluem informações sobre o inquilino Olá, incluindo o emissor do inquilino específico e informações de ponto final. As aplicações que restringem o inquilino único do acesso tooa utilizar pontos finais de inquilino específico.

Pontos finais de inquilino independente fornecem informações que são comuns aos inquilinos do Azure AD de tooall. Estas informações aplicam-se tootenants alojados em *login.microsoftonline.com* e é partilhado entre inquilinos. Pontos finais de independente de inquilino são recomendados para aplicações de multi-inquilinos, uma vez que não estão associados com nenhum inquilino específico.

## <a name="federation-metadata-endpoints"></a>Pontos finais de metadados de Federação
Azure AD publica os metadados de Federação em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Para **pontos finais de inquilino específico**, Olá `TenantDomainName` pode ser um dos seguintes tipos de Olá:

* Um nome de domínio registado de um Azure AD de inquilino, tais como: `contoso.onmicrosoft.com`.
* Olá imutável inquilino ID do domínio Olá, tais como `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Para **pontos finais de inquilino independente**, Olá `TenantDomainName` é `common`. Este documento apresenta apenas Olá metadados de Federação elementos que são comuns inquilinos do Azure AD de tooall que estão alojados em login.microsoftonline.com.

Por exemplo, poderá ser um ponto final de inquilino específico `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. ponto final de inquilino independente Olá [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Pode ver o documento de metadados de Federação Olá escrevendo este URL num browser.

## <a name="contents-of-federation-metadata"></a>Conteúdo de metadados de Federação
Olá seguinte secção fornece informações necessárias pela serviços que consomem tokens de Olá emitidos pelo Azure AD.

### <a name="entity-id"></a>ID de entidade
Olá `EntityDescriptor` elemento contém um `EntityID` atributo. Olá, valor de Olá `EntityID` atributo representa o emissor de hello, ou seja, segurança Olá token serviço (STS) esse token Olá emitidos. É importante toovalidate emissor de Olá quando recebe um token.

Olá metadados seguinte mostra um exemplo inquilino específico `EntityDescriptor` elemento com um `EntityID` elemento.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Pode substituir Olá ID do inquilino no ponto final de inquilino independente Olá com seu toocreate de ID do inquilino um inquilino específico `EntityID` valor. valor resultante Olá será Olá igual ao hello emissor de token. estratégia de Olá permite um emissor de Olá toovalidate aplicação multi-inquilino para um determinado inquilino.

Olá metadados seguinte mostra um exemplo independentes do inquilino `EntityID` elemento. Tenha em atenção, esse Olá `{tenant}` é um literal, não um marcador de posição.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certificados de assinatura de tokens
Quando um serviço recebe um token que é emitido por um inquilino do Azure AD, hello assinatura do token de Olá tem de ser validada com uma chave de assinatura que é publicada no documento de metadados de Federação Olá. os metadados de Federação Olá incluem Olá pública parte certificados Olá que inquilinos Olá utilizam para a assinatura de tokens. bytes não processados do certificado Olá aparecem no Olá `KeyDescriptor` elemento. certificado de assinatura de tokens de Olá é válido para o valor de Olá apenas assinatura Olá quando `use` atributo `signing`.

Um documento de metadados de Federação publicado pelo Azure AD pode ter várias chaves de assinatura, por exemplo, quando está a preparar Olá tooupdate certificado de assinatura do Azure AD. Quando um documento de metadados de Federação inclui mais de um certificado, um serviço que está a ser validada tokens Olá deve suportar todos os certificados no documento de Olá.

Olá metadados seguinte mostra um exemplo `KeyDescriptor` elemento com uma chave de assinatura.

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

Olá `KeyDescriptor` elemento é apresentado em dois locais no documento de metadados de Federação Olá; na secção de Olá específico do WS-Federação e secção Olá SAML específicos. certificados de Olá publicados em ambas as secções será Olá à mesma.

Na secção de Olá específico do WS-Federação, um leitor de metadados de WS-Federation seria ler certificados Olá a partir de um `RoleDescriptor` elemento com Olá `SecurityTokenServiceType` tipo.

Olá metadados seguinte mostra um exemplo `RoleDescriptor` elemento.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

Na secção de Olá SAML específico, um leitor de metadados de WS-Federation seria ler certificados Olá a partir de um `IDPSSODescriptor` elemento.

Olá metadados seguinte mostra um exemplo `IDPSSODescriptor` elemento.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Existem não existem diferenças no formato de Olá de certificados específicos de inquilino e independente de inquilino.

### <a name="ws-federation-endpoint-url"></a>URL de ponto final de WS-Federation
os metadados de Federação Olá incluem Olá utiliza o URL que é o Azure AD para o início de sessão único e de fim de sessão no protocolo WS-Federation único. Este ponto final é apresentado no Olá `PassiveRequestorEndpoint` elemento.

Olá metadados seguinte mostra um exemplo `PassiveRequestorEndpoint` elemento para um ponto final de inquilino específico.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Para o ponto final de inquilino independente Olá, Olá URL de WS-Federation aparece no ponto final de Olá WS-Federation, conforme mostrado no seguinte exemplo de Olá.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>URL de ponto final de protocolo SAML
os metadados de Federação Olá incluem Olá URL que utiliza o Azure AD para o início de sessão único e de fim de sessão no protocolo SAML 2.0 único. Estes pontos finais são apresentados no Olá `IDPSSODescriptor` elemento.

Olá início de sessão e fim de sessão URLs são apresentados no Olá `SingleSignOnService` e `SingleLogoutService` elementos.

Olá metadados seguinte mostra um exemplo `PassiveResistorEndpoint` para um ponto final de inquilino específico.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Da mesma forma Olá pontos finais para Olá comuns SAML 2.0 pontos finais de protocolo são publicados nos metadados da Federação independente de inquilino de Olá, conforme mostrado no seguinte exemplo de Olá.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
