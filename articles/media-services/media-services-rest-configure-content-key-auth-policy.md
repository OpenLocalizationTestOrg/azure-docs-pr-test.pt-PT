---
title: "política de autorização da chave de conteúdo de aaaConfigure com REST - Azure | Microsoft Docs"
description: "Saiba como tooconfigure uma política de autorização para uma chave de conteúdo utilizando a API de REST dos serviços de suporte de dados."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7af5f9e2-8ed8-43f2-843b-580ce8759fd4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: c058b7682bcbfb736faba18ec7fce33f2f2acb49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-encryption-configure-content-key-authorization-policy"></a><span data-ttu-id="460af-103">Encriptação dinâmica: configurar a política de autorização de chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="460af-103">Dynamic encryption: Configure Content Key Authorization Policy</span></span>
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a><span data-ttu-id="460af-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="460af-104">Overview</span></span>
<span data-ttu-id="460af-105">Media Services do Microsoft Azure permite-lhe toodeliver o conteúdo encriptado (dinamicamente) com AES Advanced Encryption Standard () (utilizando as chaves de encriptação de 128 bits) e PlayReady ou Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="460af-105">Microsoft Azure Media Services enables you toodeliver your content encrypted (dynamically) with Advanced Encryption Standard (AES) (using 128-bit encryption keys) and PlayReady or Widevine DRM.</span></span> <span data-ttu-id="460af-106">Os Media Services também fornecem um serviço para entrega de chaves e licenças PlayReady/Widevine tooauthorized clientes.</span><span class="sxs-lookup"><span data-stu-id="460af-106">Media Services also provides a service for delivering keys and PlayReady/Widevine licenses tooauthorized clients.</span></span>

<span data-ttu-id="460af-107">Se pretender que para os Media Services tooencrypt um recurso, tem de tooassociate uma chave de encriptação (**CommonEncryption** ou **EnvelopeEncryption**) com recurso de Olá (conforme descrito [aqui](media-services-rest-create-contentkey.md)) e também configurar políticas de autorização para a chave de Olá (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="460af-107">If you want for Media Services tooencrypt an asset, you need tooassociate an encryption key (**CommonEncryption** or **EnvelopeEncryption**) with hello asset (as described [here](media-services-rest-create-contentkey.md)) and also configure authorization policies for hello key (as described in this article).</span></span>

<span data-ttu-id="460af-108">Quando um fluxo é solicitado por um leitor, os Media Services utilizam Olá especificado toodynamically chave encriptar o seu conteúdo através da encriptação AES ou PlayReady.</span><span class="sxs-lookup"><span data-stu-id="460af-108">When a stream is requested by a player, Media Services uses hello specified key toodynamically encrypt your content using AES or PlayReady encryption.</span></span> <span data-ttu-id="460af-109">fluxo de Olá toodecrypt, player Olá irá solicitar a chave de Olá do serviço de entrega de chave Olá.</span><span class="sxs-lookup"><span data-stu-id="460af-109">toodecrypt hello stream, hello player will request hello key from hello key delivery service.</span></span> <span data-ttu-id="460af-110">toodecide ou não está a utilizador Olá autorizado a chave de Olá tooget, serviço de Olá avalia as políticas de autorização de Olá que especificou para a chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="460af-110">toodecide whether or not hello user is authorized tooget hello key, hello service evaluates hello authorization policies that you specified for hello key.</span></span>

<span data-ttu-id="460af-111">Os Media Services suportam várias formas de autenticar utilizadores que efetuam pedidos de chave.</span><span class="sxs-lookup"><span data-stu-id="460af-111">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="460af-112">Olá política de autorização da chave de conteúdo pode ter um ou mais restrições de autorização: **abrir** ou **token** restrição.</span><span class="sxs-lookup"><span data-stu-id="460af-112">hello content key authorization policy could have one or more authorization restrictions: **open** or **token** restriction.</span></span> <span data-ttu-id="460af-113">política de Olá token restrito tem de ser acompanhada por um token emitido por uma Secure Token serviço (STS).</span><span class="sxs-lookup"><span data-stu-id="460af-113">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="460af-114">Os Media Services suportam tokens no Olá **Web Tokens simples** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e * * formato **(JWT) JSON Web Token.</span><span class="sxs-lookup"><span data-stu-id="460af-114">Media Services supports tokens in hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format and **JSON Web Token **(JWT) format.</span></span>

<span data-ttu-id="460af-115">Serviços de suporte de dados não fornece serviços de Token seguro.</span><span class="sxs-lookup"><span data-stu-id="460af-115">Media Services does not provide Secure Token Services.</span></span> <span data-ttu-id="460af-116">Pode criar um STS personalizado ou tirar partido dos tokens de tooissue ACS do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="460af-116">You can create a custom STS or leverage Microsoft Azure ACS tooissue tokens.</span></span> <span data-ttu-id="460af-117">Olá STS tem de ser configurado toocreate um token assinado com a chave especificada Olá e emitem afirmações que foi especificado na configuração de restrição de token de Olá (conforme descrito neste artigo).</span><span class="sxs-lookup"><span data-stu-id="460af-117">hello STS must be configured toocreate a token signed with hello specified key and issue claims that you specified in hello token restriction configuration (as described in this article).</span></span> <span data-ttu-id="460af-118">Olá serviço de entrega de chave de Media Services irá devolver cliente de toohello chave de encriptação de Olá se Olá token é válido e hello afirmações num token de Olá corresponderem os que são configurados para a chave de conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="460af-118">hello Media Services key delivery service will return hello encryption key toohello client if hello token is valid and hello claims in hello token match those configured for hello content key.</span></span>

<span data-ttu-id="460af-119">Para obter mais informações, veja</span><span class="sxs-lookup"><span data-stu-id="460af-119">For more information, see</span></span>

[<span data-ttu-id="460af-120">Autenticação de token JWT</span><span class="sxs-lookup"><span data-stu-id="460af-120">JWT token authentication</span></span>](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<span data-ttu-id="460af-121">[Integrar a aplicação do Azure Media Services OWIN MVC com base no Azure Active Directory e restringir a entrega de chave de conteúdo com base em afirmações JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span><span class="sxs-lookup"><span data-stu-id="460af-121">[Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</span></span>

<span data-ttu-id="460af-122">[Utilize as ACS de Azure tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span><span class="sxs-lookup"><span data-stu-id="460af-122">[Use Azure ACS tooissue tokens](http://mingfeiy.com/acs-with-key-services).</span></span>

### <a name="some-considerations-apply"></a><span data-ttu-id="460af-123">São aplicáveis algumas considerações:</span><span class="sxs-lookup"><span data-stu-id="460af-123">Some considerations apply:</span></span>
* <span data-ttu-id="460af-124">toobe toouse capaz de um empacotamento dinâmico e a encriptação dinâmica, certifique-se Olá de transmissão em fluxo ponto final a partir das quais pretende toostream o conteúdo no Olá **executar** estado.</span><span class="sxs-lookup"><span data-stu-id="460af-124">toobe able toouse dynamic packaging and dynamic encryption, make sure hello streaming endpoint from which you want toostream  your content is in hello **Running** state.</span></span>
* <span data-ttu-id="460af-125">O elemento tem de conter um conjunto de MP4s de velocidade de transmissão adaptável ou ficheiros de transmissão em fluxo uniforme de velocidade de transmissão adaptável.</span><span class="sxs-lookup"><span data-stu-id="460af-125">Your asset must contain a set of adaptive bitrate MP4s or  adaptive bitrate Smooth Streaming files.</span></span> <span data-ttu-id="460af-126">Para obter mais informações, consulte [codificar um elemento](media-services-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="460af-126">For more information, see [Encode an asset](media-services-encode-asset.md).</span></span>
* <span data-ttu-id="460af-127">Carregar e codificar seus ativos utilizando **AssetCreationOptions.StorageEncrypted** opção.</span><span class="sxs-lookup"><span data-stu-id="460af-127">Upload and encode your assets using **AssetCreationOptions.StorageEncrypted** option.</span></span>
* <span data-ttu-id="460af-128">Se planear toohave várias chaves de conteúdo que necessitam de Olá mesma configuração de política, é vivamente recomendado toocreate uma política de autorização único e reutilizá-lo com várias chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="460af-128">If you plan toohave multiple content keys that require hello same policy configuration, it is strongly recommended toocreate a single authorization policy and reuse it with multiple content keys.</span></span>
* <span data-ttu-id="460af-129">serviço de entrega de chave de Olá coloca em cache ContentKeyAuthorizationPolicy e os respetivos objetos relacionados (opções de política e restrições) para 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="460af-129">hello Key Delivery service caches ContentKeyAuthorizationPolicy and its related objects (policy options and restrictions) for 15 minutes.</span></span>  <span data-ttu-id="460af-130">Se criar um ContentKeyAuthorizationPolicy e especifique toouse uma restrição "Token", em seguida, testá-lo e, em seguida, atualizar a política de Olá demasiado "abrir" restrição, irá demorar cerca de 15 minutos antes de Olá política comutadores toohello "Abrir" versão da política de Olá.</span><span class="sxs-lookup"><span data-stu-id="460af-130">If you create a ContentKeyAuthorizationPolicy and specify toouse a “Token” restriction, then test it, and then update hello policy too“Open” restriction, it will take roughly 15 minutes before hello policy switches toohello “Open” version of hello policy.</span></span>
* <span data-ttu-id="460af-131">Se adicionar ou atualizar a sua política de entrega de elementos, tem de eliminar um localizador existente (se aplicável) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="460af-131">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
* <span data-ttu-id="460af-132">Atualmente, não é possível encriptar transferências de transferência progressiva.</span><span class="sxs-lookup"><span data-stu-id="460af-132">Currently, you cannot encrypt progressive downloads.</span></span>

## <a name="aes-128-dynamic-encryption"></a><span data-ttu-id="460af-133">Encriptação dinâmica AES-128</span><span class="sxs-lookup"><span data-stu-id="460af-133">AES-128 Dynamic Encryption</span></span>
> [!NOTE]
> <span data-ttu-id="460af-134">Ao trabalhar com Olá API de REST dos serviços de suporte de dados, Olá aplicam seguintes considerações:</span><span class="sxs-lookup"><span data-stu-id="460af-134">When working with hello Media Services REST API, hello following considerations apply:</span></span>
> 
> <span data-ttu-id="460af-135">Ao aceder a entidades nos Media Services, tem de definir campos de cabeçalho específicos e os valores no seus pedidos HTTP.</span><span class="sxs-lookup"><span data-stu-id="460af-135">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="460af-136">Para obter mais informações, consulte [programa de configuração para o desenvolvimento de API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="460af-136">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 
> <span data-ttu-id="460af-137">Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="460af-137">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="460af-138">É necessário efetuar chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="460af-138">You must make subsequent calls toohello new URI.</span></span> <span data-ttu-id="460af-139">Para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="460af-139">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
> 
> 

### <a name="open-restriction"></a><span data-ttu-id="460af-140">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="460af-140">Open Restriction</span></span>
<span data-ttu-id="460af-141">Abra restrição significa sistema Olá irá fornecer tooanyone de chave Olá que faz um pedido de chave.</span><span class="sxs-lookup"><span data-stu-id="460af-141">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="460af-142">Esta restrição poderão ser úteis para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="460af-142">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="460af-143">Olá seguinte exemplo cria uma política de autorização aberta e adiciona-toohello chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="460af-143">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="460af-144"><a id="ContentKeyAuthorizationPolicies"></a>Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="460af-144"><a id="ContentKeyAuthorizationPolicies"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="460af-145">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-145">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423578086&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lZlyQ2%2bvH73qtJsb42%2fH3xF7r7EvQFR3UXyezuDENFU%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 36

    {"Name":"Open Authorization Policy"}

<span data-ttu-id="460af-146">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-146">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 211
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Adb4593da-f4d1-4cc5-a92a-d20eacbabee4')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d732dbfa-54fc-474c-99d6-9b46a006f389
    request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    x-ms-request-id: aabfa731-e884-4bf3-8314-492b04747ac4
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:25:56 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:db4593da-f4d1-4cc5-a92a-d20eacbabee4","Name":"Open Authorization Policy"}

#### <span data-ttu-id="460af-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="460af-147"><a id="ContentKeyAuthorizationPolicyOptions"></a>Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="460af-148">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-148">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 168

    {"Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="460af-149">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-149">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 349
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: d225e357-e60e-4f42-add8-9d93aba1409a
    request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    x-ms-request-id: 81bcad37-295b-431f-972f-b23f2e4172c9
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 08:56:40 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:57829b17-1101-4797-919b-f816f4a007b7","Name":"policy","KeyDeliveryType":2,"KeyDeliveryConfiguration":"","Restrictions":[{"Name":"HLS Open Authorization Policy","KeyRestrictionType":0,"Requirements":null}]}

#### <span data-ttu-id="460af-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Ligação ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="460af-150"><a id="LinkContentKeyAuthorizationPoliciesWithOptions"></a>Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="460af-151">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-151">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3A0baa438b-8ac2-4c40-a53c-4d4722b78715')/$links/Options HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580006&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=Ref3EsonGF7fUKCwGwGgiMnZitzIzsDOvvMTeVrVVPg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9847f705-f2ca-4e95-a478-8f823dbbaa29
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 154

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A57829b17-1101-4797-919b-f816f4a007b7')"}

<span data-ttu-id="460af-152">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-152">Response:</span></span>

    HTTP/1.1 204 No Content

#### <span data-ttu-id="460af-153"><a id="AddAuthorizationPolicyToKey"></a>Adicionar chave de conteúdo de toohello de política de autorização</span><span class="sxs-lookup"><span data-stu-id="460af-153"><a id="AddAuthorizationPolicyToKey"></a>Add authorization policy toohello content key</span></span>
<span data-ttu-id="460af-154">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-154">Request:</span></span>

    PUT https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A2e6d36a7-a17c-4e9a-830d-eca23ad1a6f9') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: e613efff-cb6a-41b4-984a-f4f8fb6e76a4
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 78

    {"AuthorizationPolicyId":"nb:ckpid:UUID:c06cebb8-c4f0-4d1a-ba00-3273fb2bc3ad"}

<span data-ttu-id="460af-155">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-155">Response:</span></span>

    HTTP/1.1 204 No Content

### <a name="token-restriction"></a><span data-ttu-id="460af-156">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="460af-156">Token Restriction</span></span>
<span data-ttu-id="460af-157">Esta secção descreve como toocreate um conteúdo política de autorização da chave e associá-la a chave de conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="460af-157">This section describes how toocreate a content key authorization policy and associate it with hello content key.</span></span> <span data-ttu-id="460af-158">política de autorização de Olá descreve os requisitos de autorização tem de ser cumprido toodetermine se o utilizador de Olá é a chave de Olá tooreceive autorizados (por exemplo, a lista de "chave de verificação" Olá conter chave Olá esse token Olá foi assinada com).</span><span class="sxs-lookup"><span data-stu-id="460af-158">hello authorization policy describes what authorization requirements must be met toodetermine if hello user is authorized tooreceive hello key (for example, does hello “verification key” list contain hello key that hello token was signed with).</span></span>

<span data-ttu-id="460af-159">opção de restrição de token de Olá tooconfigure, terá de toouse um XML requisitos de autorização do token de Olá toodescribe.</span><span class="sxs-lookup"><span data-stu-id="460af-159">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="460af-160">XML de configuração de restrição de token de Olá deve ter toohello esquema XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="460af-160">hello token restriction configuration XML must conform toohello following XML schema.</span></span>

#### <span data-ttu-id="460af-161"><a id="schema"></a>Esquema de restrição de token</span><span class="sxs-lookup"><span data-stu-id="460af-161"><a id="schema"></a>Token restriction schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:complexType name="TokenClaim">
        <xs:sequence>
          <xs:element name="ClaimType" nillable="true" type="xs:string" />
          <xs:element minOccurs="0" name="ClaimValue" nillable="true" type="xs:string" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenClaim" nillable="true" type="tns:TokenClaim" />
      <xs:complexType name="TokenRestrictionTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AlternateVerificationKeys" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
          <xs:element name="Audience" nillable="true" type="xs:anyURI" />
          <xs:element name="Issuer" nillable="true" type="xs:anyURI" />
          <xs:element name="PrimaryVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
          <xs:element minOccurs="0" name="RequiredClaims" nillable="true" type="tns:ArrayOfTokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="TokenRestrictionTemplate" nillable="true" type="tns:TokenRestrictionTemplate" />
      <xs:complexType name="ArrayOfTokenVerificationKey">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenVerificationKey" nillable="true" type="tns:ArrayOfTokenVerificationKey" />
      <xs:complexType name="TokenVerificationKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="TokenVerificationKey" nillable="true" type="tns:TokenVerificationKey" />
      <xs:complexType name="ArrayOfTokenClaim">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="TokenClaim" nillable="true" type="tns:TokenClaim" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfTokenClaim" nillable="true" type="tns:ArrayOfTokenClaim" />
      <xs:complexType name="SymmetricVerificationKey">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:TokenVerificationKey">
            <xs:sequence>
              <xs:element name="KeyValue" nillable="true" type="xs:base64Binary" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="SymmetricVerificationKey" nillable="true" type="tns:SymmetricVerificationKey" />
    </xs:schema>

<span data-ttu-id="460af-162">Quando configurar Olá **token** restringido a política, tem de especificar Olá primário * * verificação chave * *, **emissor** e **público-alvo** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="460af-162">When configuring hello **token** restricted policy, you must specify hello primary** verification key**, **issuer** and **audience** parameters.</span></span> <span data-ttu-id="460af-163">Olá * * a chave de verificação principal * * contém chave Olá Olá token foi assinada com, **emissor** é serviço de token seguro Olá esse token de Olá problemas.</span><span class="sxs-lookup"><span data-stu-id="460af-163">hello **primary verification key **contains hello key that hello token was signed with, **issuer** is hello secure token service that issues hello token.</span></span> <span data-ttu-id="460af-164">Olá **público-alvo** (por vezes denominado **âmbito**) descreve intenção Olá de token de Olá ou recurso de Olá token Olá autoriza o acesso.</span><span class="sxs-lookup"><span data-stu-id="460af-164">hello **audience** (sometimes called **scope**) describes hello intent of hello token or hello resource hello token authorizes access to.</span></span> <span data-ttu-id="460af-165">Olá serviço de entrega de chave de Media Services valida se estes valores no token de Olá correspondem aos valores de Olá no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="460af-165">hello Media Services key delivery service validates that these values in hello token match hello values in hello template.</span></span> 

<span data-ttu-id="460af-166">Olá seguinte exemplo cria uma política de autorização com uma restrição de token.</span><span class="sxs-lookup"><span data-stu-id="460af-166">hello following example creates an authorization policy with a token restriction.</span></span> <span data-ttu-id="460af-167">Neste exemplo, cliente Olá teria toopresent um token que contém: assinatura de chave (VerificationKey), um emissor de token e afirmações necessárias.</span><span class="sxs-lookup"><span data-stu-id="460af-167">In this example, hello client would have toopresent a token that contains: signing key (VerificationKey), a token issuer, and required claims.</span></span>

### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="460af-168">Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="460af-168">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="460af-169">Crie Olá "Política de restrição de Token", conforme mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="460af-169">Create hello "Token Restriction Policy" as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="460af-170">Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="460af-170">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="460af-171">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-171">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbbef702-e769-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423580720&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5LsNu%2b0D4eD3UOP3BviTLDkUjaErdUx0ekJ8402xidQ%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1079

    {"Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="460af-172">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-172">Response:</span></span>    

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1260
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae1ef6145-46e8-4ee6-9756-b1cf96328c23')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 2643d836-bfe7-438e-9ba2-bc6ff28e4a53
    request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    x-ms-request-id: 2310b716-aeaa-421e-913e-3ce2f6f685ca
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:10:37 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e1ef6145-46e8-4ee6-9756-b1cf96328c23","Name":"Token option for HLS","KeyDeliveryType":2,"KeyDeliveryConfiguration":null,"Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>BklyAFiPTQsuJNKriQJBZHYaKM2CkCTDQX2bw9sMYuvEC9sjW0W7GUIBygQL/+POEeUqCYPnmEU2g0o1GW2Oqg==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>E5BUHiN4vBdzUzdP0IWaHFMMU3D1uRZgF16TOhSfwwHGSw+Kbf0XqsHzEIYk11M372viB9vbiacsdcQksA0ftw==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="460af-173">Ligação ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="460af-173">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="460af-174">Ligação ContentKeyAuthorizationPolicies com opções conforme é mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="460af-174">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="460af-175">Adicionar chave de conteúdo de toohello de política de autorização</span><span class="sxs-lookup"><span data-stu-id="460af-175">Add authorization policy toohello content key</span></span>
<span data-ttu-id="460af-176">Adicione AuthorizationPolicy toohello ContentKey conforme é mostrado [aqui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="460af-176">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <a name="playready-dynamic-encryption"></a><span data-ttu-id="460af-177">Encriptação PlayReady dinâmico</span><span class="sxs-lookup"><span data-stu-id="460af-177">PlayReady Dynamic Encryption</span></span>
<span data-ttu-id="460af-178">Os Media Services permite-lhe direitos de Olá de tooconfigure e as restrições que pretende para Olá tooenforce de tempo de execução de PlayReady DRM quando um utilizador está a tentar tooplay volta a conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="460af-178">Media Services enables you tooconfigure hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplay back protected content.</span></span> 

<span data-ttu-id="460af-179">Quando proteger o seu conteúdo com PlayReady, uma das ações de Olá terá toospecify na sua política de autorização é uma cadeia XML que define Olá [o modelo de licença PlayReady](media-services-playready-license-template-overview.md).</span><span class="sxs-lookup"><span data-stu-id="460af-179">When protecting your content with PlayReady, one of hello things you need toospecify in your authorization policy is an XML string that defines hello [PlayReady license template](media-services-playready-license-template-overview.md).</span></span> 

### <a name="open-restriction"></a><span data-ttu-id="460af-180">Restrição aberta</span><span class="sxs-lookup"><span data-stu-id="460af-180">Open Restriction</span></span>
<span data-ttu-id="460af-181">Abra restrição significa sistema Olá irá fornecer tooanyone de chave Olá que faz um pedido de chave.</span><span class="sxs-lookup"><span data-stu-id="460af-181">Open restriction means hello system will deliver hello key tooanyone who makes a key request.</span></span> <span data-ttu-id="460af-182">Esta restrição poderão ser úteis para fins de teste.</span><span class="sxs-lookup"><span data-stu-id="460af-182">This restriction might be useful for testing purposes.</span></span>

<span data-ttu-id="460af-183">Olá seguinte exemplo cria uma política de autorização aberta e adiciona-toohello chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="460af-183">hello following example creates an open authorization policy and adds it toohello content key.</span></span>

#### <span data-ttu-id="460af-184"><a id="ContentKeyAuthorizationPolicies2"></a>Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="460af-184"><a id="ContentKeyAuthorizationPolicies2"></a>Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="460af-185">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-185">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=bbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 58

    {"Name":"Deliver Common Content Key"}

<span data-ttu-id="460af-186">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-186">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 233
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicies('nb%3Ackpid%3AUUID%3Acc3c64a8-e2fc-4e09-bf60-ac954251a387')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 9e7fa407-f84e-43aa-8f05-9790b46e279b
    request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    x-ms-request-id: b3d33c1b-a9cb-4120-ac0c-18f64846c147
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:26:00 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicies/@Element","Id":"nb:ckpid:UUID:cc3c64a8-e2fc-4e09-bf60-ac954251a387","Name":"Deliver Common Content Key"}


#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="460af-187">Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="460af-187">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="460af-188">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-188">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423581565&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=JiNSG3w6r2C0nIyfKvTZj1uPJGjuitD%2b0sbfZ%2b2JDZI%3d
    x-ms-version: 2.11
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 593

    {"Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

<span data-ttu-id="460af-189">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-189">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 774
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3A1052308c-4df7-4fdb-8d21-4d2141fc2be0')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: f160ad25-b457-4bc6-8197-315604c5e585
    request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    x-ms-request-id: 563f5a42-50a4-4c4a-add8-a833f8364231
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:23:24 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:1052308c-4df7-4fdb-8d21-4d2141fc2be0","Name":"","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Open","KeyRestrictionType":0,"Requirements":null}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="460af-190">Ligação ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="460af-190">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="460af-191">Ligação ContentKeyAuthorizationPolicies com opções conforme é mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="460af-191">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="460af-192">Adicionar chave de conteúdo de toohello de política de autorização</span><span class="sxs-lookup"><span data-stu-id="460af-192">Add authorization policy toohello content key</span></span>
<span data-ttu-id="460af-193">Adicione AuthorizationPolicy toohello ContentKey conforme é mostrado [aqui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="460af-193">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

### <a name="token-restriction"></a><span data-ttu-id="460af-194">Restrição de token</span><span class="sxs-lookup"><span data-stu-id="460af-194">Token Restriction</span></span>
<span data-ttu-id="460af-195">opção de restrição de token de Olá tooconfigure, terá de toouse um XML requisitos de autorização do token de Olá toodescribe.</span><span class="sxs-lookup"><span data-stu-id="460af-195">tooconfigure hello token restriction option, you need toouse an XML toodescribe hello token’s authorization requirements.</span></span> <span data-ttu-id="460af-196">XML de configuração de restrição de token de Olá deve ter o esquema XML toohello mostrada na [isto](#schema) secção.</span><span class="sxs-lookup"><span data-stu-id="460af-196">hello token restriction configuration XML must conform toohello XML schema shown in [this](#schema) section.</span></span>

#### <a name="create-contentkeyauthorizationpolicies"></a><span data-ttu-id="460af-197">Criar ContentKeyAuthorizationPolicies</span><span class="sxs-lookup"><span data-stu-id="460af-197">Create ContentKeyAuthorizationPolicies</span></span>
<span data-ttu-id="460af-198">Crie ContentKeyAuthorizationPolicies conforme mostrado [aqui](#ContentKeyAuthorizationPolicies2).</span><span class="sxs-lookup"><span data-stu-id="460af-198">Create ContentKeyAuthorizationPolicies as shown [here](#ContentKeyAuthorizationPolicies2).</span></span>

#### <a name="create-contentkeyauthorizationpolicyoptions"></a><span data-ttu-id="460af-199">Criar ContentKeyAuthorizationPolicyOptions</span><span class="sxs-lookup"><span data-stu-id="460af-199">Create ContentKeyAuthorizationPolicyOptions</span></span>
<span data-ttu-id="460af-200">Pedido:</span><span class="sxs-lookup"><span data-stu-id="460af-200">Request:</span></span>

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 3.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423583561&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=5eZnkOsSv%2fLLEKmS%2bWObBlsNYyee8BQlp%2bUYbjugcJg%3d
    x-ms-version: 2.11
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 1525

    {"Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

<span data-ttu-id="460af-201">Resposta:</span><span class="sxs-lookup"><span data-stu-id="460af-201">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1706
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeyAuthorizationPolicyOptions('nb%3Ackpoid%3AUUID%3Ae42bbeae-de42-4077-90e9-a844f297ef70')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: ab079b0e-2ba9-4cf1-b549-a97bfa6cd2d3
    request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    x-ms-request-id: ccf8a4ba-731e-4124-8192-079592c251cc
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Tue, 10 Feb 2015 09:58:47 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeyAuthorizationPolicyOptions/@Element","Id":"nb:ckpoid:UUID:e42bbeae-de42-4077-90e9-a844f297ef70","Name":"Token option","KeyDeliveryType":1,"KeyDeliveryConfiguration":"<PlayReadyLicenseResponseTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1\"><LicenseTemplates><PlayReadyLicenseTemplate><AllowTestDevices>false</AllowTestDevices><ContentKey i:type=\"ContentEncryptionKeyFromHeader\" /><LicenseType>Nonpersistent</LicenseType><PlayRight /></PlayReadyLicenseTemplate></LicenseTemplates></PlayReadyLicenseResponseTemplate>","Restrictions":[{"Name":"Token Authorization Policy","KeyRestrictionType":1,"Requirements":"<TokenRestrictionTemplate xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/TokenRestrictionTemplate/v1\"><AlternateVerificationKeys><TokenVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>w52OyHVqXT8aaupGxuJ3NGt8M6opHDOtx132p4r6q4hLI6ffnLusgEGie1kedUewVoIe1tqDkVE6xsIV7O91KA==</KeyValue></TokenVerificationKey></AlternateVerificationKeys><Audience>urn:test</Audience><Issuer>http://testacs.com/</Issuer><PrimaryVerificationKey i:type=\"SymmetricVerificationKey\"><KeyValue>dYwLKIEMBljLeY9VM7vWdlhps31Fbt0XXhqP5VyjQa33bJXleBtkzQ6dF5AtwI9gDcdM2dV2TvYNhCilBKjMCg==</KeyValue></PrimaryVerificationKey><RequiredClaims><TokenClaim><ClaimType>urn:microsoft:azure:mediaservices:contentkeyidentifier</ClaimType><ClaimValue i:nil=\"true\" /></TokenClaim></RequiredClaims><TokenType>SWT</TokenType></TokenRestrictionTemplate>"}]}

#### <a name="link-contentkeyauthorizationpolicies-with-options"></a><span data-ttu-id="460af-202">Ligação ContentKeyAuthorizationPolicies com opções</span><span class="sxs-lookup"><span data-stu-id="460af-202">Link ContentKeyAuthorizationPolicies with Options</span></span>
<span data-ttu-id="460af-203">Ligação ContentKeyAuthorizationPolicies com opções conforme é mostrado [aqui](#ContentKeyAuthorizationPolicies).</span><span class="sxs-lookup"><span data-stu-id="460af-203">Link ContentKeyAuthorizationPolicies with Options as shown [here](#ContentKeyAuthorizationPolicies).</span></span>

#### <a name="add-authorization-policy-toohello-content-key"></a><span data-ttu-id="460af-204">Adicionar chave de conteúdo de toohello de política de autorização</span><span class="sxs-lookup"><span data-stu-id="460af-204">Add authorization policy toohello content key</span></span>
<span data-ttu-id="460af-205">Adicione AuthorizationPolicy toohello ContentKey conforme é mostrado [aqui](#AddAuthorizationPolicyToKey).</span><span class="sxs-lookup"><span data-stu-id="460af-205">Add AuthorizationPolicy toohello ContentKey as shown [here](#AddAuthorizationPolicyToKey).</span></span>

## <span data-ttu-id="460af-206"><a id="types"></a>Tipos de utilizado quando se definem ContentKeyAuthorizationPolicy</span><span class="sxs-lookup"><span data-stu-id="460af-206"><a id="types"></a>Types used when defining ContentKeyAuthorizationPolicy</span></span>
### <span data-ttu-id="460af-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span><span class="sxs-lookup"><span data-stu-id="460af-207"><a id="ContentKeyRestrictionType"></a>ContentKeyRestrictionType</span></span>
    public enum ContentKeyRestrictionType
    {
        Open = 0,
        TokenRestricted = 1,
        IPRestricted = 2,
    }

### <span data-ttu-id="460af-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span><span class="sxs-lookup"><span data-stu-id="460af-208"><a id="ContentKeyDeliveryType"></a>ContentKeyDeliveryType</span></span>
    public enum ContentKeyDeliveryType
    {
        None = 0,
        PlayReadyLicense = 1,
        BaselineHttp = 2,
        Widevine = 3
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="460af-209">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="460af-209">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="460af-210">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="460af-210">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="460af-211">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="460af-211">Next Steps</span></span>
<span data-ttu-id="460af-212">Agora que configurou a política de autorização da chave de conteúdo, aceda toohello [como política de entrega de elemento tooconfigure](media-services-rest-configure-asset-delivery-policy.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="460af-212">Now that you have configured content key's authorization policy, go toohello [How tooconfigure asset delivery policy](media-services-rest-configure-asset-delivery-policy.md) topic.</span></span>

