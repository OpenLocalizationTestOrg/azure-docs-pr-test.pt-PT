---
title: aaaConnecting tooMedia conta Services utilizando a REST API | Microsoft Docs
description: "Este tópico demonstra como tooconnect tooMedia serviços uisng REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: erikre
editor: 
ms.assetid: 79dc64f1-15d8-4a81-b9d9-3d3c44d2e1e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 1d5064a3612dc96f5c5ad910d183d84fb70a3b6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a><span data-ttu-id="f3211-103">Ligar tooMedia conta Services utilizando a API de REST dos serviços de suporte de dados</span><span class="sxs-lookup"><span data-stu-id="f3211-103">Connecting tooMedia Services Account using Media Services REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3211-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f3211-104">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> * [<span data-ttu-id="f3211-105">REST</span><span class="sxs-lookup"><span data-stu-id="f3211-105">REST</span></span>](media-services-rest-connect-programmatically.md)
> 
> 

<span data-ttu-id="f3211-106">Este tópico descreve como tooobtain tooMicrosoft uma ligação programática Media Services do Azure quando são programação com Olá API de REST dos serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="f3211-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services REST API.</span></span>

<span data-ttu-id="f3211-107">São necessárias duas coisas quando aceder aos serviços de suporte de dados do Microsoft Azure: um token de acesso fornecido pelos serviços de controlo de acesso do Azure (ACS) e Olá URI de Media Services próprio.</span><span class="sxs-lookup"><span data-stu-id="f3211-107">Two things are required when accessing Microsoft Azure Media Services: An access token provided by Azure Access Control Services (ACS), and hello URI of Media Services itself.</span></span> <span data-ttu-id="f3211-108">Pode utilizar qualquer meio que pretender quando criar estes pedidos desde que especifique os valores de cabeçalho correto de Olá e passar corretamente no token de acesso de Olá ao chamar nos Media Services.</span><span class="sxs-lookup"><span data-stu-id="f3211-108">You can use any means you want when creating these requests as long as you specify hello correct header values and pass in hello access token correctly when calling into Media Services.</span></span>

<span data-ttu-id="f3211-109">Olá, os passos seguintes descreve o fluxo de trabalho mais comuns Olá quando utilizar Olá API de REST dos serviços de suporte de dados tooconnect tooMedia Services:</span><span class="sxs-lookup"><span data-stu-id="f3211-109">hello following steps describe hello most common workflow when using hello Media Services REST API tooconnect tooMedia Services:</span></span>

1. <span data-ttu-id="f3211-110">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="f3211-110">Getting an access token</span></span> 
2. <span data-ttu-id="f3211-111">Ligar toohello URI de serviços de suporte de dados</span><span class="sxs-lookup"><span data-stu-id="f3211-111">Connecting toohello Media Services URI</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f3211-112">Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="f3211-112">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="f3211-113">É necessário efetuar chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="f3211-113">You must make subsequent calls toohello new URI.</span></span>
   > <span data-ttu-id="f3211-114">Também poderá receber uma resposta HTTP/1.1 200 contém Olá descrição de metadados de API de ODATA.</span><span class="sxs-lookup"><span data-stu-id="f3211-114">You may also receive a HTTP/1.1 200 response that contains hello ODATA API metadata description.</span></span>
   > 
   > 
3. <span data-ttu-id="f3211-115">Após a sua API chamadas toohello novo URL subsequente.</span><span class="sxs-lookup"><span data-stu-id="f3211-115">Post your subsequent API calls toohello new URL.</span></span> 
   
    <span data-ttu-id="f3211-116">Por exemplo, se depois tentar tooconnect, obteve seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="f3211-116">For example, if after trying tooconnect, you got hello following:</span></span>
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    <span data-ttu-id="f3211-117">Deve publicar o seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="f3211-117">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f3211-118">Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="f3211-118">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="f3211-119">Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso.</span><span class="sxs-lookup"><span data-stu-id="f3211-119">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="f3211-120">Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="f3211-120">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

## <a name="access-control-address"></a><span data-ttu-id="f3211-121">Endereço de controlo de acesso</span><span class="sxs-lookup"><span data-stu-id="f3211-121">Access control address</span></span>
<span data-ttu-id="f3211-122">Endereço de controlo de acesso de Media Services é https://wamsprodglobal001acs.accesscontrol.windows.net, exceto região Norte China, onde é https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span><span class="sxs-lookup"><span data-stu-id="f3211-122">Media Services access control address is https://wamsprodglobal001acs.accesscontrol.windows.net, except for North China region, where it is https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.</span></span>

## <a name="getting-an-access-token"></a><span data-ttu-id="f3211-123">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="f3211-123">Getting an access token</span></span>
<span data-ttu-id="f3211-124">tooaccess Media Services diretamente através da REST API Olá, obter um token de acesso de ACS e utilizá-lo durante a todos os pedidos HTTP que efetuar ao serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="f3211-124">tooaccess Media Services directly through hello REST API, retrieve an access token from ACS and use it during every HTTP request you make into hello service.</span></span> <span data-ttu-id="f3211-125">Este token é semelhante tooother tokens, fornecidos pelo ACS baseados em afirmações de acesso fornecidas no cabeçalho de Olá de um pedido de HTTP e através do protocolo de Olá v2 de OAuth.</span><span class="sxs-lookup"><span data-stu-id="f3211-125">This token is similar tooother tokens provided by ACS based on access claims provided in hello header of an HTTP request and using hello OAuth v2 protocol.</span></span> <span data-ttu-id="f3211-126">Não é necessário qualquer outros pré-requisitos antes de ligar diretamente tooMedia serviços.</span><span class="sxs-lookup"><span data-stu-id="f3211-126">You do not need any other prerequisites before directly connecting tooMedia Services.</span></span>

<span data-ttu-id="f3211-127">Olá exemplo seguinte mostra cabeçalho de pedido HTTP Olá e tooretrieve de corpo utilizado um token.</span><span class="sxs-lookup"><span data-stu-id="f3211-127">hello following example shows hello HTTP request header and body used tooretrieve a token.</span></span>

<span data-ttu-id="f3211-128">**Cabeçalho**:</span><span class="sxs-lookup"><span data-stu-id="f3211-128">**Header**:</span></span>

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


<span data-ttu-id="f3211-129">**Corpo**:</span><span class="sxs-lookup"><span data-stu-id="f3211-129">**Body**:</span></span>

<span data-ttu-id="f3211-130">Terá de tooprove Olá client_id client_secret valores e no corpo de Olá deste pedido; client_id e client_secret correspondem toohello AccountName e AccountKey valores, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="f3211-130">You need tooprove hello client_id and client_secret values in hello body of this request; client_id and client_secret correspond toohello AccountName and AccountKey values, respectively.</span></span> <span data-ttu-id="f3211-131">Estes valores são fornecidos tooyou pelos Media Services quando configurou a sua conta.</span><span class="sxs-lookup"><span data-stu-id="f3211-131">These values are provided tooyou by Media Services when you set up your account.</span></span> 

<span data-ttu-id="f3211-132">Tenha em atenção que Olá AccountKey para conta de Media Services tem de ser codificados de URL (consulte [codificação de percentagem](http://tools.ietf.org/html/rfc3986#section-2.1) quando utilizá-lo como valor de client_secret Olá do seu pedido de token de acesso.</span><span class="sxs-lookup"><span data-stu-id="f3211-132">Note that hello AccountKey for your Media Services account must be URL-encoded (see [Percent-Encoding](http://tools.ietf.org/html/rfc3986#section-2.1) when using it as hello client_secret value in your access token request.</span></span>

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="f3211-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f3211-133">For example:</span></span> 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


<span data-ttu-id="f3211-134">Olá exemplo seguinte mostra resposta HTTP de Olá que contém o acesso de Olá token no corpo de resposta de Olá.</span><span class="sxs-lookup"><span data-stu-id="f3211-134">hello following example shows hello HTTP response that contains hello access token in hello response body.</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache, no-store
    Pragma: no-cache
    Content-Type: application/json; charset=utf-8
    Expires: -1
    request-id: a65150f5-2784-4a01-a4b7-33456187ad83
    X-Content-Type-Options: nosniff
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 15 Jan 2015 08:07:20 GMT
    Content-Length: 670

    {  
       "token_type":"http://schemas.xmlsoap.org/ws/2009/11/swt-token-profile-1.0",
       "access_token":"http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421330840&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=uf69n82KlqZmkJDNxhJkOxpyIpA2HDyeGUTtSnq1vlE%3d",
       "expires_in":"21600",
       "scope":"urn:WindowsAzureMediaServices"
    }


> [!NOTE]
> <span data-ttu-id="f3211-135">É recomendado toocache Olá "access_token" e "expires_in" valores tooan armazenamento externo.</span><span class="sxs-lookup"><span data-stu-id="f3211-135">It is recommended toocache hello "access_token " and "expires_in " values tooan external storage.</span></span> <span data-ttu-id="f3211-136">dados de token de Olá mais tarde foi obtidos a partir do armazenamento de Olá e novamente utilizados na sua chamadas da API de REST de serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="f3211-136">hello token data could later be retrieved from hello storage and re-used in your Media Services REST API calls.</span></span> <span data-ttu-id="f3211-137">Isto é especialmente útil para cenários onde token Olá pode ser partilhado com segurança entre vários processos ou computadores.</span><span class="sxs-lookup"><span data-stu-id="f3211-137">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
> 
> 

<span data-ttu-id="f3211-138">Certifique-se de que toomonitor Olá "expires_in" valor acesso Olá token e Atualize as chamadas de REST API com novos tokens conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f3211-138">Make sure toomonitor hello "expires_in" value of hello access token and update your REST API calls with new tokens as needed.</span></span>

### <a name="connecting-toohello-media-services-uri"></a><span data-ttu-id="f3211-139">Ligar toohello URI de serviços de suporte de dados</span><span class="sxs-lookup"><span data-stu-id="f3211-139">Connecting toohello Media Services URI</span></span>
<span data-ttu-id="f3211-140">raiz de Olá URI para os Media Services é https://media.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="f3211-140">hello root URI for Media Services is https://media.windows.net/.</span></span> <span data-ttu-id="f3211-141">Inicialmente, deve ligar toothis URI e se receber um redirecionamento 301 na resposta, deve efetuar chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="f3211-141">You should initially connect toothis URI, and if you get a 301 redirect back in response, you should make subsequent calls toohello new URI.</span></span> <span data-ttu-id="f3211-142">Além disso, não utilize qualquer lógica automática-redirecionamento/siga os pedidos.</span><span class="sxs-lookup"><span data-stu-id="f3211-142">In addition, do not use any auto-redirect/follow logic in your requests.</span></span> <span data-ttu-id="f3211-143">Verbos HTTP e corpos de pedido não são reencaminhados toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="f3211-143">HTTP verbs and request bodies will not be forwarded toohello new URI.</span></span>

<span data-ttu-id="f3211-144">Tenha em atenção que raiz Olá URI para carregar e transferir ficheiros de recurso é https://yourstorageaccount.blob.core.windows.net/ onde o nome de conta do storage Olá Olá um mesmo que utilizou durante a configuração de conta de Media Services.</span><span class="sxs-lookup"><span data-stu-id="f3211-144">Note that hello root URI for uploading and downloading Asset files is https://yourstorageaccount.blob.core.windows.net/ where hello storage account name is hello same one you used during your Media Services account setup.</span></span>

<span data-ttu-id="f3211-145">Olá seguinte o exemplo demonstra HTTP pedido toohello dos Media Services raiz URI (https://media.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="f3211-145">hello following example demonstrates HTTP request toohello Media Services root URI (https://media.windows.net/).</span></span> <span data-ttu-id="f3211-146">pedido de Olá obtém um redirecionamento 301 na resposta.</span><span class="sxs-lookup"><span data-stu-id="f3211-146">hello request gets a 301 redirect back in response.</span></span> <span data-ttu-id="f3211-147">Olá pedido subsequente está a utilizar Olá novo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span><span class="sxs-lookup"><span data-stu-id="f3211-147">hello subsequent request is using hello new URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).</span></span>     

<span data-ttu-id="f3211-148">**Pedido de HTTP**:</span><span class="sxs-lookup"><span data-stu-id="f3211-148">**HTTP Request**:</span></span>

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


<span data-ttu-id="f3211-149">**Resposta de HTTP**:</span><span class="sxs-lookup"><span data-stu-id="f3211-149">**HTTP Response**:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
    Server: Microsoft-IIS/8.5
    request-id: 987d7652-497a-44e5-b815-f492e02aef97
    x-ms-request-id: 987d7652-497a-44e5-b815-f492e02aef97
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:53 GMT
    Content-Length: 164

    <html><head><title>Object moved</title></head><body>
    <h2>Object moved too<a href="https://wamsbayclus001rest-hs.cloudapp.net/api/">here</a>.</h2>
    </body></html>


<span data-ttu-id="f3211-150">**Pedido de HTTP** (utilizando Olá novo URI):</span><span class="sxs-lookup"><span data-stu-id="f3211-150">**HTTP Request** (using hello new URI):</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="f3211-151">**Resposta de HTTP**:</span><span class="sxs-lookup"><span data-stu-id="f3211-151">**HTTP Response**:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1250
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    x-ms-request-id: 5f52ea9d-177e-48fe-9709-24953d19f84a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sat, 17 Jan 2015 07:44:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata","value":[{"name":"AccessPolicies","url":"AccessPolicies"},{"name":"Locators","url":"Locators"},{"name":"ContentKeys","url":"ContentKeys"},{"name":"ContentKeyAuthorizationPolicyOptions","url":"ContentKeyAuthorizationPolicyOptions"},{"name":"ContentKeyAuthorizationPolicies","url":"ContentKeyAuthorizationPolicies"},{"name":"Files","url":"Files"},{"name":"Assets","url":"Assets"},{"name":"AssetDeliveryPolicies","url":"AssetDeliveryPolicies"},{"name":"IngestManifestFiles","url":"IngestManifestFiles"},{"name":"IngestManifestAssets","url":"IngestManifestAssets"},{"name":"IngestManifests","url":"IngestManifests"},{"name":"StorageAccounts","url":"StorageAccounts"},{"name":"Tasks","url":"Tasks"},{"name":"NotificationEndPoints","url":"NotificationEndPoints"},{"name":"Jobs","url":"Jobs"},{"name":"TaskTemplates","url":"TaskTemplates"},{"name":"JobTemplates","url":"JobTemplates"},{"name":"MediaProcessors","url":"MediaProcessors"},{"name":"EncodingReservedUnitTypes","url":"EncodingReservedUnitTypes"},{"name":"Operations","url":"Operations"},{"name":"StreamingEndpoints","url":"StreamingEndpoints"},{"name":"Channels","url":"Channels"},{"name":"Programs","url":"Programs"}]}



> [!NOTE]
> <span data-ttu-id="f3211-152">Depois de obter Olá URI novo, o que é Olá URI que deve ser utilizado toocommunicate com os Media Services.</span><span class="sxs-lookup"><span data-stu-id="f3211-152">Once you get hello new URI, that is hello URI that should be used toocommunicate with Media Services.</span></span> 
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="f3211-153">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="f3211-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f3211-154">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="f3211-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

