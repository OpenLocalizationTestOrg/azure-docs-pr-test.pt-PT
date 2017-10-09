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
# <a name="federation-metadata"></a><span data-ttu-id="66ae1-103">Metadados de federação</span><span class="sxs-lookup"><span data-stu-id="66ae1-103">Federation metadata</span></span>
<span data-ttu-id="66ae1-104">Azure Active Directory (Azure AD) publica um documento de metadados de Federação para serviços que é configurada tokens de segurança de Olá tooaccept que o Azure AD emite.</span><span class="sxs-lookup"><span data-stu-id="66ae1-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="66ae1-105">Olá formato do documento de metadados de Federação está descrito em Olá [idioma de Federação de serviços Web (WS-Federation) versão 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que expande [metadados para Olá OASIS Security Assertion Markup Language (SAML) v 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="66ae1-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="66ae1-106">Inquilino específico e os pontos finais de metadados do inquilino independentes</span><span class="sxs-lookup"><span data-stu-id="66ae1-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="66ae1-107">Azure AD publica pontos finais de inquilino específico e independente de inquilino.</span><span class="sxs-lookup"><span data-stu-id="66ae1-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="66ae1-108">Pontos finais de inquilino específico foram concebidos para um determinado inquilino.</span><span class="sxs-lookup"><span data-stu-id="66ae1-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="66ae1-109">metadados de Federação de inquilino específico Olá incluem informações sobre o inquilino Olá, incluindo o emissor do inquilino específico e informações de ponto final.</span><span class="sxs-lookup"><span data-stu-id="66ae1-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="66ae1-110">As aplicações que restringem o inquilino único do acesso tooa utilizar pontos finais de inquilino específico.</span><span class="sxs-lookup"><span data-stu-id="66ae1-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="66ae1-111">Pontos finais de inquilino independente fornecem informações que são comuns aos inquilinos do Azure AD de tooall.</span><span class="sxs-lookup"><span data-stu-id="66ae1-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="66ae1-112">Estas informações aplicam-se tootenants alojados em *login.microsoftonline.com* e é partilhado entre inquilinos.</span><span class="sxs-lookup"><span data-stu-id="66ae1-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="66ae1-113">Pontos finais de independente de inquilino são recomendados para aplicações de multi-inquilinos, uma vez que não estão associados com nenhum inquilino específico.</span><span class="sxs-lookup"><span data-stu-id="66ae1-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="66ae1-114">Pontos finais de metadados de Federação</span><span class="sxs-lookup"><span data-stu-id="66ae1-114">Federation metadata endpoints</span></span>
<span data-ttu-id="66ae1-115">Azure AD publica os metadados de Federação em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="66ae1-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="66ae1-116">Para **pontos finais de inquilino específico**, Olá `TenantDomainName` pode ser um dos seguintes tipos de Olá:</span><span class="sxs-lookup"><span data-stu-id="66ae1-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="66ae1-117">Um nome de domínio registado de um Azure AD de inquilino, tais como: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="66ae1-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="66ae1-118">Olá imutável inquilino ID do domínio Olá, tais como `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="66ae1-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="66ae1-119">Para **pontos finais de inquilino independente**, Olá `TenantDomainName` é `common`.</span><span class="sxs-lookup"><span data-stu-id="66ae1-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="66ae1-120">Este documento apresenta apenas Olá metadados de Federação elementos que são comuns inquilinos do Azure AD de tooall que estão alojados em login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="66ae1-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="66ae1-121">Por exemplo, poderá ser um ponto final de inquilino específico `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="66ae1-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="66ae1-122">ponto final de inquilino independente Olá [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="66ae1-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="66ae1-123">Pode ver o documento de metadados de Federação Olá escrevendo este URL num browser.</span><span class="sxs-lookup"><span data-stu-id="66ae1-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="66ae1-124">Conteúdo de metadados de Federação</span><span class="sxs-lookup"><span data-stu-id="66ae1-124">Contents of federation Metadata</span></span>
<span data-ttu-id="66ae1-125">Olá seguinte secção fornece informações necessárias pela serviços que consomem tokens de Olá emitidos pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66ae1-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="66ae1-126">ID de entidade</span><span class="sxs-lookup"><span data-stu-id="66ae1-126">Entity ID</span></span>
<span data-ttu-id="66ae1-127">Olá `EntityDescriptor` elemento contém um `EntityID` atributo.</span><span class="sxs-lookup"><span data-stu-id="66ae1-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="66ae1-128">Olá, valor de Olá `EntityID` atributo representa o emissor de hello, ou seja, segurança Olá token serviço (STS) esse token Olá emitidos.</span><span class="sxs-lookup"><span data-stu-id="66ae1-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="66ae1-129">É importante toovalidate emissor de Olá quando recebe um token.</span><span class="sxs-lookup"><span data-stu-id="66ae1-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="66ae1-130">Olá metadados seguinte mostra um exemplo inquilino específico `EntityDescriptor` elemento com um `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="66ae1-131">Pode substituir Olá ID do inquilino no ponto final de inquilino independente Olá com seu toocreate de ID do inquilino um inquilino específico `EntityID` valor.</span><span class="sxs-lookup"><span data-stu-id="66ae1-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="66ae1-132">valor resultante Olá será Olá igual ao hello emissor de token.</span><span class="sxs-lookup"><span data-stu-id="66ae1-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="66ae1-133">estratégia de Olá permite um emissor de Olá toovalidate aplicação multi-inquilino para um determinado inquilino.</span><span class="sxs-lookup"><span data-stu-id="66ae1-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="66ae1-134">Olá metadados seguinte mostra um exemplo independentes do inquilino `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="66ae1-135">Tenha em atenção, esse Olá `{tenant}` é um literal, não um marcador de posição.</span><span class="sxs-lookup"><span data-stu-id="66ae1-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="66ae1-136">Certificados de assinatura de tokens</span><span class="sxs-lookup"><span data-stu-id="66ae1-136">Token signing certificates</span></span>
<span data-ttu-id="66ae1-137">Quando um serviço recebe um token que é emitido por um inquilino do Azure AD, hello assinatura do token de Olá tem de ser validada com uma chave de assinatura que é publicada no documento de metadados de Federação Olá.</span><span class="sxs-lookup"><span data-stu-id="66ae1-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="66ae1-138">os metadados de Federação Olá incluem Olá pública parte certificados Olá que inquilinos Olá utilizam para a assinatura de tokens.</span><span class="sxs-lookup"><span data-stu-id="66ae1-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="66ae1-139">bytes não processados do certificado Olá aparecem no Olá `KeyDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="66ae1-140">certificado de assinatura de tokens de Olá é válido para o valor de Olá apenas assinatura Olá quando `use` atributo `signing`.</span><span class="sxs-lookup"><span data-stu-id="66ae1-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="66ae1-141">Um documento de metadados de Federação publicado pelo Azure AD pode ter várias chaves de assinatura, por exemplo, quando está a preparar Olá tooupdate certificado de assinatura do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="66ae1-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="66ae1-142">Quando um documento de metadados de Federação inclui mais de um certificado, um serviço que está a ser validada tokens Olá deve suportar todos os certificados no documento de Olá.</span><span class="sxs-lookup"><span data-stu-id="66ae1-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="66ae1-143">Olá metadados seguinte mostra um exemplo `KeyDescriptor` elemento com uma chave de assinatura.</span><span class="sxs-lookup"><span data-stu-id="66ae1-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="66ae1-144">Olá `KeyDescriptor` elemento é apresentado em dois locais no documento de metadados de Federação Olá; na secção de Olá específico do WS-Federação e secção Olá SAML específicos.</span><span class="sxs-lookup"><span data-stu-id="66ae1-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="66ae1-145">certificados de Olá publicados em ambas as secções será Olá à mesma.</span><span class="sxs-lookup"><span data-stu-id="66ae1-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="66ae1-146">Na secção de Olá específico do WS-Federação, um leitor de metadados de WS-Federation seria ler certificados Olá a partir de um `RoleDescriptor` elemento com Olá `SecurityTokenServiceType` tipo.</span><span class="sxs-lookup"><span data-stu-id="66ae1-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="66ae1-147">Olá metadados seguinte mostra um exemplo `RoleDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="66ae1-148">Na secção de Olá SAML específico, um leitor de metadados de WS-Federation seria ler certificados Olá a partir de um `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="66ae1-149">Olá metadados seguinte mostra um exemplo `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="66ae1-150">Existem não existem diferenças no formato de Olá de certificados específicos de inquilino e independente de inquilino.</span><span class="sxs-lookup"><span data-stu-id="66ae1-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="66ae1-151">URL de ponto final de WS-Federation</span><span class="sxs-lookup"><span data-stu-id="66ae1-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="66ae1-152">os metadados de Federação Olá incluem Olá utiliza o URL que é o Azure AD para o início de sessão único e de fim de sessão no protocolo WS-Federation único.</span><span class="sxs-lookup"><span data-stu-id="66ae1-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="66ae1-153">Este ponto final é apresentado no Olá `PassiveRequestorEndpoint` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="66ae1-154">Olá metadados seguinte mostra um exemplo `PassiveRequestorEndpoint` elemento para um ponto final de inquilino específico.</span><span class="sxs-lookup"><span data-stu-id="66ae1-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="66ae1-155">Para o ponto final de inquilino independente Olá, Olá URL de WS-Federation aparece no ponto final de Olá WS-Federation, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="66ae1-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="66ae1-156">URL de ponto final de protocolo SAML</span><span class="sxs-lookup"><span data-stu-id="66ae1-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="66ae1-157">os metadados de Federação Olá incluem Olá URL que utiliza o Azure AD para o início de sessão único e de fim de sessão no protocolo SAML 2.0 único.</span><span class="sxs-lookup"><span data-stu-id="66ae1-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="66ae1-158">Estes pontos finais são apresentados no Olá `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="66ae1-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="66ae1-159">Olá início de sessão e fim de sessão URLs são apresentados no Olá `SingleSignOnService` e `SingleLogoutService` elementos.</span><span class="sxs-lookup"><span data-stu-id="66ae1-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="66ae1-160">Olá metadados seguinte mostra um exemplo `PassiveResistorEndpoint` para um ponto final de inquilino específico.</span><span class="sxs-lookup"><span data-stu-id="66ae1-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="66ae1-161">Da mesma forma Olá pontos finais para Olá comuns SAML 2.0 pontos finais de protocolo são publicados nos metadados da Federação independente de inquilino de Olá, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="66ae1-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
