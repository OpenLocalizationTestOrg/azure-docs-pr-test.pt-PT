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
# <a name="connecting-toomedia-services-account-using-media-services-rest-api"></a>Ligar tooMedia conta Services utilizando a API de REST dos serviços de suporte de dados
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-connect-programmatically.md)
> * [REST](media-services-rest-connect-programmatically.md)
> 
> 

Este tópico descreve como tooobtain tooMicrosoft uma ligação programática Media Services do Azure quando são programação com Olá API de REST dos serviços de suporte de dados.

São necessárias duas coisas quando aceder aos serviços de suporte de dados do Microsoft Azure: um token de acesso fornecido pelos serviços de controlo de acesso do Azure (ACS) e Olá URI de Media Services próprio. Pode utilizar qualquer meio que pretender quando criar estes pedidos desde que especifique os valores de cabeçalho correto de Olá e passar corretamente no token de acesso de Olá ao chamar nos Media Services.

Olá, os passos seguintes descreve o fluxo de trabalho mais comuns Olá quando utilizar Olá API de REST dos serviços de suporte de dados tooconnect tooMedia Services:

1. Obter um token de acesso 
2. Ligar toohello URI de serviços de suporte de dados 
   
   > [!NOTE]
   > Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados. É necessário efetuar chamadas subsequentes toohello novo URI.
   > Também poderá receber uma resposta HTTP/1.1 200 contém Olá descrição de metadados de API de ODATA.
   > 
   > 
3. Após a sua API chamadas toohello novo URL subsequente. 
   
    Por exemplo, se depois tentar tooconnect, obteve seguinte Olá:
   
        HTTP/1.1 301 Moved Permanently
        Location: https://wamsbayclus001rest-hs.cloudapp.net/api/
   
    Deve publicar o seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.

    >[!NOTE]
    >Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy). Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso. Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

## <a name="access-control-address"></a>Endereço de controlo de acesso
Endereço de controlo de acesso de Media Services é https://wamsprodglobal001acs.accesscontrol.windows.net, exceto região Norte China, onde é https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn.

## <a name="getting-an-access-token"></a>Obter um token de acesso
tooaccess Media Services diretamente através da REST API Olá, obter um token de acesso de ACS e utilizá-lo durante a todos os pedidos HTTP que efetuar ao serviço de Olá. Este token é semelhante tooother tokens, fornecidos pelo ACS baseados em afirmações de acesso fornecidas no cabeçalho de Olá de um pedido de HTTP e através do protocolo de Olá v2 de OAuth. Não é necessário qualquer outros pré-requisitos antes de ligar diretamente tooMedia serviços.

Olá exemplo seguinte mostra cabeçalho de pedido HTTP Olá e tooretrieve de corpo utilizado um token.

**Cabeçalho**:

    POST https://wamsprodglobal001acs.accesscontrol.windows.net/v2/OAuth2-13 HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Host: wamsprodglobal001acs.accesscontrol.windows.net
    Content-Length: 120
    Expect: 100-continue
    Connection: Keep-Alive
    Accept: application/json


**Corpo**:

Terá de tooprove Olá client_id client_secret valores e no corpo de Olá deste pedido; client_id e client_secret correspondem toohello AccountName e AccountKey valores, respetivamente. Estes valores são fornecidos tooyou pelos Media Services quando configurou a sua conta. 

Tenha em atenção que Olá AccountKey para conta de Media Services tem de ser codificados de URL (consulte [codificação de percentagem](http://tools.ietf.org/html/rfc3986#section-2.1) quando utilizá-lo como valor de client_secret Olá do seu pedido de token de acesso.

    grant_type=client_credentials&client_id=ams_account_name&client_secret=URL_encoded_ams_account_key&scope=urn%3aWindowsAzureMediaServices


Por exemplo: 

    grant_type=client_credentials&client_id=amstestaccount001&client_secret=wUNbKhNj07oqjqU3Ah9R9f4kqTJ9avPpfe6Pk3YZ7ng%3d&scope=urn%3aWindowsAzureMediaServices


Olá exemplo seguinte mostra resposta HTTP de Olá que contém o acesso de Olá token no corpo de resposta de Olá.

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
> É recomendado toocache Olá "access_token" e "expires_in" valores tooan armazenamento externo. dados de token de Olá mais tarde foi obtidos a partir do armazenamento de Olá e novamente utilizados na sua chamadas da API de REST de serviços de suporte de dados. Isto é especialmente útil para cenários onde token Olá pode ser partilhado com segurança entre vários processos ou computadores.
> 
> 

Certifique-se de que toomonitor Olá "expires_in" valor acesso Olá token e Atualize as chamadas de REST API com novos tokens conforme necessário.

### <a name="connecting-toohello-media-services-uri"></a>Ligar toohello URI de serviços de suporte de dados
raiz de Olá URI para os Media Services é https://media.windows.net/. Inicialmente, deve ligar toothis URI e se receber um redirecionamento 301 na resposta, deve efetuar chamadas subsequentes toohello novo URI. Além disso, não utilize qualquer lógica automática-redirecionamento/siga os pedidos. Verbos HTTP e corpos de pedido não são reencaminhados toohello novo URI.

Tenha em atenção que raiz Olá URI para carregar e transferir ficheiros de recurso é https://yourstorageaccount.blob.core.windows.net/ onde o nome de conta do storage Olá Olá um mesmo que utilizou durante a configuração de conta de Media Services.

Olá seguinte o exemplo demonstra HTTP pedido toohello dos Media Services raiz URI (https://media.windows.net/). pedido de Olá obtém um redirecionamento 301 na resposta. Olá pedido subsequente está a utilizar Olá novo URI (https://wamsbayclus001rest-hs.cloudapp.net/api/).     

**Pedido de HTTP**:

    GET https://media.windows.net/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: media.windows.net


**Resposta de HTTP**:

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


**Pedido de HTTP** (utilizando Olá novo URI):

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/ HTTP/1.1
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f19258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421500579&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=ElVWXOnMVggFQl%2ft9vhdcv1qH1n%2fE8l3hRef4zPmrzg%3d
    x-ms-version: 2.11
    Accept: application/json
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta de HTTP**:

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
> Depois de obter Olá URI novo, o que é Olá URI que deve ser utilizado toocommunicate com os Media Services. 
> 
> 

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

