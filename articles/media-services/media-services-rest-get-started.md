---
title: "aaaGet à entrega de conteúdo a pedido utilizando REST | Microsoft Docs"
description: "Este tutorial explica passos para Olá implementar uma aplicação de entrega de conteúdos a pedido com Media Services do Azure utilizando a REST API."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 88194b59-e479-43ac-b179-af4f295e3780
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: f270ed59e9ae9745e8403ec6e19d5c3533fc82b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a>Introdução à entrega de conteúdos a pedido utilizando REST
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Este guia de introdução orienta-o pelos passos Olá implementar uma aplicação de entrega de conteúdos de vídeo a pedido (VoD) utilizando as APIs REST de serviços de suporte de dados do Azure (AMS).

tutorial de Olá apresenta o fluxo de trabalho Olá básico dos Media Services e objetos de programação mais comuns Olá e as tarefas necessárias para o desenvolvimento de Media Services. Olá após conclusão do tutorial Olá, terá de ser capaz de toostream ou transferir progressivamente um ficheiro de suporte de dados de exemplo que carregou, codificou e transferiu.

Olá imagem seguinte mostra alguns dos objetos de Olá normalmente utilizada quando desenvolver aplicações VoD contra um modelo de suporte de dados serviços OData Olá.

Clique em Olá imagem tooview-total de tamanho.  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a>Pré-requisitos
Olá pré-requisitos seguintes são necessário toostart desenvolver com os serviços de suporte de dados com REST APIs.

* Uma conta do Azure. Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* Uma conta dos Media Services. toocreate uma conta de Media Services, consulte [como tooCreate uma conta de Media Services](media-services-portal-create-account.md).
* Compreender como toodevelop com a API de REST dos serviços de suporte de dados. Para obter mais informações, consulte [descrição geral da API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).
* Uma aplicação da sua preferência que pode enviar pedidos e respostas HTTP. Este tutorial utiliza [Fiddler](http://www.telerik.com/download/fiddler).

Olá seguintes tarefas é apresentada neste guia de introdução.

1. Inicie o ponto final (utilizando o portal do Azure de Olá) de transmissão em fluxo.
2. Ligar a conta de Media Services do toohello com a REST API.
3. Criar um novo elemento e carregar um ficheiro de vídeo com a REST API.
4. Codificar o ficheiro de origem Olá para um conjunto de ficheiros MP4 de velocidade de transmissão adaptável com a REST API.
5. Publica asset Olá e get de transmissão em fluxo e transferência progressiva URLs REST API.
6. Reproduzir os conteúdos.

>[!NOTE]
>Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy). Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso. Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Para obter detalhes sobre as entidades de REST do AMS utilizados neste tópico, consulte [referência da API REST do Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference). Além disso, consulte [conceitos de Media Services do Azure](media-services-concepts.md).

>[!NOTE]
>Ao aceder a entidades nos Media Services, tem de definir campos de cabeçalho específicos e os valores no seus pedidos HTTP. Para obter mais informações, consulte [programa de configuração para o desenvolvimento de API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a>Começar a transmissão em fluxo pontos finais utilizando Olá portal do Azure

Ao trabalhar com uma das situações mais comuns Olá é a entrega de vídeo através de velocidade de transmissão adaptável em fluxo de Media Services do Azure. Os Media Services fornecem um empacotamento dinâmico, permitindo-lhe toodeliver a conteúdo MP4 codificado suportados pelo Media Services (MPEG DASH, HLS, transmissão em fluxo uniforme) just-in-time, sem ter toostore previamente empacotada de formatos de transmissão em fluxo de velocidade de transmissão adaptável versões de cada um destes formatos de transmissão em fluxo.

>[!NOTE]
>Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado. toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado.

toostart Olá ponto final de transmissão em fluxo, Olá a seguir:

1. Inicie sessão no Olá [portal do Azure](https://portal.azure.com/).
2. Na janela de definições de Olá, clique em pontos finais de transmissão em fluxo.
3. Clique em predefinido Olá ponto final de transmissão em fluxo.

    Surge a janela de detalhes de ponto final de transmissão em fluxo de predefinido Olá.

4. Clique Olá ícone de início.
5. Clique em Olá guardar botão toosave as suas alterações.

## <a id="connect"></a>Ligar a conta de Media Services toohello com a REST API

Para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados. É necessário efetuar chamadas subsequentes toohello novo URI.

Por exemplo, se depois tentar tooconnect, obteve seguinte Olá:

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

Deve publicar o seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.

## <a id="upload"></a>Criar um novo elemento e carregar um ficheiro de vídeo com a REST API

Nos Serviços de Multimédia, os ficheiros digitais são carregados para um elemento. Olá **Asset** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto controla e legendas ficheiros (e Olá metadados sobre estes ficheiros.)  Depois de ficheiros de Olá são carregados para o elemento de Olá, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.

Um dos valores de Olá que tiver tooprovide ao criar um recurso é opções de criação do elemento. Olá **opções** propriedade é um valor de enumeração que descreve as opções de encriptação de Olá um recurso que pode ser criado com. Um valor válido é de um dos valores de Olá da lista de Olá abaixo, não uma combinação de valores nesta lista:

* **Nenhum** = **0** -é utilizada qualquer encriptação. Ao utilizar esta opção não está protegido o conteúdo em trânsito ou inativo no armazenamento.
    Se planear toodeliver um MP4 utilizando transferência progressiva, utilize esta opção.
* **StorageEncrypted** = **1** - encripta o seu conteúdo transparente localmente utilizando AES 256 bits encriptação e, em seguida, esta carrega-tooAzure armazenamento onde é armazenado encriptado em pausa. Os elementos protegidos com encriptação de armazenamento são automaticamente não encriptados e colocados num tooencoding anterior de sistema de ficheiros encriptados e opcionalmente encriptado novamente toouploading anterior novamente como um novo elemento de saída. Olá principal motivo para encriptação de armazenamento é quando quiser toosecure os ficheiros de suporte de dados de entrada de alta qualidade com uma encriptação forte Inativos no disco.
* **CommonEncryptionProtected** = **2** -Utilize esta opção se estiver a carregar conteúdo que já foi encriptado e protegido com encriptação comum ou PlayReady DRM (por exemplo, transmissão em fluxo uniforme protegida com PlayReady DRM).
* **EnvelopeEncryptionProtected** = **4** – Utilize esta opção se estiver a carregar HLS encriptado com AES. ficheiros de Olá tem de ter sido codificados e encriptados pelo Gestor de transformação.

### <a name="create-an-asset"></a>Criar um recurso
Um recurso é um contentor para vários tipos ou conjuntos de objetos nos Media Services, incluindo as vídeo, áudio, imagens, coleções de miniaturas, controla de texto e legendas ficheiros. No Olá API REST, criar um recurso necessita de enviar a mensagem de pedido tooMedia serviços e colocar quaisquer informações de propriedade sobre o elemento no corpo do pedido de Olá.

Olá seguinte exemplo mostra como toocreate um recurso.

**Pedido de HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 45

    {"Name":"BigBuckBunny.mp4", "Options":"0"}


**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny2.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>Criar um AssetFile
Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um ficheiro de vídeo ou áudio que é armazenado num contentor de blob. Um ficheiro de recurso é sempre associado a um recurso e um recurso pode conter um ou vários AssetFiles. tarefa de codificador de serviços de multimédia de Olá falhar se um objeto de ficheiro de recurso não está associado um ficheiro digital num contentor de blob.

Depois de carregar o ficheiro de suporte de dados digitais num contentor de blob, pode utilizar Olá **intercalar** HTTP pedido tooupdate Olá AssetFile com informações sobre o ficheiro de suporte de dados (conforme mostrado posteriormente tópico Olá).

**Pedido de HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 164

    {  
       "IsEncrypted":"false",
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**Resposta de HTTP**

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion":null,
       "EncryptionScheme":null,
       "IsEncrypted":false,
       "EncryptionKeyId":null,
       "InitializationVector":null,
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }


### <a name="creating-hello-accesspolicy-with-write-permission"></a>Criar Olá AccessPolicy com permissão de escrita
Antes de carregar ficheiros para o armazenamento de BLOBs, defina acesso Olá direitos de política para escrever tooan ativo. Definir toodo que, após um toohello de pedido HTTP AccessPolicies entidade. Definir um valor de DurationInMinutes após a criação ou receber uma mensagem de erro de servidor interno 500 na resposta. Para obter mais informações sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Olá seguinte exemplo mostra como toocreate um AccessPolicy:

**Pedido de HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 74

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"}

**Resposta de HTTP**

Se tiver êxito, é devolvido Olá seguinte resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 312
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae')
    Server: Microsoft-IIS/8.5
    request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    x-ms-request-id: 74c74545-7e0a-4cd6-a440-c1c48074a970
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:18:06 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#AccessPolicies/@Element",
       "Id":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "Created":"2015-01-18T22:18:06.6370575Z",
       "LastModified":"2015-01-18T22:18:06.6370575Z",
       "Name":"NewUploadPolicy",
       "DurationInMinutes":440.0,
       "Permissions":2
    }

### <a name="get-hello-upload-url"></a>Obter Olá carregar URL

tooreceive Olá URL de carregamento real, crie um localizador SAS. Localizadores definem a hora de início Olá e o tipo de ponto final de ligação para os clientes que pretendem ficheiros tooaccess um recurso. Pode criar várias entidades de localizador para um determinado AccessPolicy e Asset par toohandle diferentes cliente pedidos e as suas necessidades. Cada um destes localizadores utiliza o valor de StartTime Olá plus valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá o comprimento de tempo que pode ser utilizado um URL. Para obter mais informações, consulte [localizador](https://docs.microsoft.com/rest/api/media/operations/locator).

Um URL SAS tem Olá seguinte formato:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

São aplicáveis algumas considerações:

* Não pode ter mais de cinco localizadores exclusivos associados um determinado elemento de uma só vez. Para obter mais informações, consulte localizador.
* Se precisar de tooupload os ficheiros imediatamente, deve definir os minutos de toofive de valor de StartTime antes Olá hora atual. Isto acontece porque poderá haver relógio dissimetrias entre o computador cliente e os Media Services. Além disso, o valor de StartTime tem de constar Olá seguir o formato DateTime: aaaa-MM-aaaathh (por exemplo, "2014-05-23T17:53:50Z").    
* Poderá existir um segundo 30-40 atrasar depois de criar um localizador toowhen está disponível para utilização. Aplica-se este problema tooboth SAS URL e localizadores de origem.

Para obter mais informações sobre SAS localizadores consulte [isto](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogue.

Olá seguinte exemplo mostra como toocreate um localizador de URL SAS, tal como definido por Olá propriedade de tipo no corpo do pedido de Olá ("1" para um localizador SAS) e "2" para um localizador de origem no pedido. Olá **caminho** propriedade devolvida contém um URL de Olá que tem de utilizar tooupload o ficheiro.

**Pedido de HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 178

    {  
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Type":1
    }


**Resposta de HTTP**

Se tiver êxito, é devolvido Olá seguinte resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 949
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54')
    Server: Microsoft-IIS/8.5
    request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    x-ms-request-id: 2adeb1f8-89c5-4cc8-aa4f-08cdfef33ae0
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 03:01:29 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Locators/@Element",
       "Id":"nb:lid:UUID:af57bdd8-6751-4e84-b403-f3c140444b54",
       "ExpirationDateTime":"2015-02-19T00:05:53",
       "Type":1,
       "Path":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "BaseUri":"https://storagetestaccount001.blob.core.windows.net/asset-f438649c-313c-46e2-8d68-7d2550288247",
       "ContentAccessComponent":"?sv=2012-02-12&sr=c&si=af57bdd8-6751-4e84-b403-f3c140444b54&sig=fE4btwEfZtVQFeC0Wh3Kwks2OFPQfzl5qTMW5YytiuY%3D&st=2015-02-18T16%3A45%3A53Z&se=2015-02-19T00%3A05%3A53Z",
       "AccessPolicyId":"nb:pid:UUID:be0ac48d-af7d-4877-9d60-1805d68bffae",
       "AssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StartTime":"2015-02-18T16:45:53",
       "Name":null
    }

### <a name="upload-a-file-into-a-blob-storage-container"></a>Carregue um ficheiro para um contentor de blob storage
Assim que tiver Olá AccessPolicy e o conjunto de localizador, real do ficheiro Olá é carregado tooan contentor de armazenamento de Blobs do Azure utilizando Olá APIs de REST de armazenamento do Azure. Tem de carregar ficheiros Olá como blobs de blocos. Os blobs de página não são suportados pelos Media Services do Azure.  

> [!NOTE]
> Tem de adicionar o nome de ficheiro Olá ficheiro Olá pretende tooupload toohello localizador **caminho** valor recebido na secção anterior Olá. Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Para obter mais informações sobre como trabalhar com blobs de armazenamento do Azure, consulte [API de REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Atualizar Olá AssetFile
Agora que carregar o ficheiro, atualize informações do Olá FileAsset tamanho (e outros). Por exemplo:

    MERGE https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a>Eliminar Olá localizador e AccessPolicy
**Pedido de HTTP**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTTP/1.1 204 No Content
    ...

**Pedido de HTTP**

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTTP/1.1 204 No Content
    ...

## <a id="encode"></a>Codificar o ficheiro de origem Olá para um conjunto de ficheiros MP4 de velocidade de transmissão adaptável

Antes após ingestão relacionadas que ativos para os serviços de suporte de dados, suportes de dados podem ser codificados, transmuxed, como e assim sucessivamente, mesmo ser entregue tooclients. Estas atividades são agendadas e executar várias em segundo plano função instâncias tooensure elevado desempenho e disponibilidade. Estas atividades são denominadas tarefas e cada trabalho é composto por tarefas atómica que Olá trabalho real no ficheiro de elemento Olá (para obter mais informações, consulte [tarefa](/rest/api/media/services/job), [tarefas](/rest/api/media/services/task) descrições).

Conforme foi mencionado anteriormente, quando trabalhar com Media Services do Azure uma das situações mais comuns de Olá é a distribuição de velocidade de transmissão adaptável tooyour clientes de transmissão em fluxo. Os Media Services podem empacotar dinamicamente um conjunto de ficheiros MP4 de velocidade de transmissão adaptável dos seguintes formatos de Olá: HTTP Live Streaming (HLS), transmissão em fluxo uniforme, MPEG DASH.

Olá, secção a seguir mostra como toocreate uma tarefa que contém uma codificação de tarefas. Olá tarefas Especifica tootranscode Olá mezanino ficheiro para um conjunto de MP4s de velocidade de transmissão adaptável utilizando **codificador de multimédia Standard**. secção de Olá também mostra como toomonitor Olá progresso de processamento da tarefa. Quando a tarefa de Olá estiver concluída, seria capaz de toocreate localizadores que são necessários tooget acesso tooyour ativos.

### <a name="get-a-media-processor"></a>Obter um processador de multimédia
Nos Media Services, um processador de multimédia é um componente que processa uma tarefa de processamento específico, tal como a codificação, a conversão do formato, encriptação ou desencriptar os conteúdos de multimédia. Para Olá codificação tarefas mostradas neste tutorial, iremos toouse Olá codificador de multimédia Standard.

Olá id do codificador de código, pedidos Olá seguinte.

**Pedido de HTTP**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta de HTTP**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 273
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    x-ms-request-id: 6beb04b4-55a7-480d-8aa8-e5c5d59ffa1f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 07:54:09 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

### <a name="create-a-job"></a>Criar uma tarefa
Cada tarefa pode ter um ou mais tarefas, dependendo do tipo de Olá do processamento de que pretendem tooaccomplish. Através da REST API Olá, pode criar as tarefas e as respetivas tarefas relacionadas em uma de duas formas: tarefas podem ser definidos inline através da propriedade de navegação de tarefas Olá entidades de tarefa ou através do processamento em lote OData. Olá SDK de Media Services utiliza o processamento em lote. No entanto, para legibilidade de Olá dos exemplos de código Olá neste tópico, as tarefas são definidos inline. Para obter informações sobre o processamento em lote, consulte [Open Data Protocol (OData) Batch processamento](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).

Olá seguinte exemplo mostra como toocreate e publique uma tarefa com uma tarefa definida tooencode um vídeo numa resolução específico e qualidade. Olá seguinte secção de documentação contém a lista de Olá de todos os Olá [tarefas predefinições](http://msdn.microsoft.com/library/mt269960) suportada pelo processador de codificador de multimédia Standard Olá.  

**Pedido de HTTP**

    POST https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: application/json
    Accept: application/json;odata=verbose
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net
    Content-Length: 482

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"Adaptive Streaming",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset>
                <outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          }
       ]
    }

**Resposta de HTTP**

Se tiver êxito, é devolvido Olá seguinte resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1215
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')
    Server: Microsoft-IIS/8.5
    request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    x-ms-request-id: 532ac1ec-a475-4dce-b2d5-7c8ce94ac87c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:04:35 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Job"
          },
          "Tasks":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Tasks"
             }
          },
          "OutputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets"
             }
          },
          "InputMediaAssets":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')/InputMediaAssets"
             }
          },
          "Id":"nb:jid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "Name":"NewTestJob",
          "Created":"2015-01-19T08:04:34.3287057Z",
          "LastModified":"2015-01-19T08:04:34.3287057Z",
          "EndTime":null,
          "Priority":0,
          "RunningDuration":0,
          "StartTime":null,
          "State":0,
          "TemplateId":null,
          "JobNotificationSubscriptions":{  
             "__metadata":{  
                "type":"Collection(Microsoft.Cloud.Media.Vod.Rest.Data.Models.JobNotificationSubscription)"
             },
             "results":[  

             ]
          }
       }
    }


Existem alguns pontos importantes toonote qualquer pedido de tarefa:

* Propriedades de TaskBody tem de utilizar literal XML toodefine Olá diversas entrada ou de recursos de saída que são utilizados pelo Olá tarefas. tópico de tarefa Olá contém Olá definição de esquema XML para Olá XML.
* O valor na definição de TaskBody Olá, para cada interna <inputAsset> e <outputAsset> tem de ser definido como JobInputAsset(value) ou JobOutputAsset(value).
* Uma tarefa pode ter vários recursos de saída. Um JobOutputAsset(x) só pode ser utilizado uma vez como resultado de uma tarefa numa tarefa.
* Pode especificar JobInputAsset ou JobOutputAsset como um recurso de entrada de uma tarefa.
* Tarefas tem não formam um ciclo.
* parâmetro de valor de Olá que passou tooJobInputAsset ou JobOutputAsset representa um valor de índice Olá para um recurso. Olá reais ativos são definidos nas propriedades de navegação de InputMediaAssets e OutputMediaAssets Olá no Olá definição de entidade de tarefa.

> [!NOTE]
> Porque os serviços de suporte de dados está incorporado no OData v3, Olá ativos individuais em InputMediaAssets e coleções de propriedade de navegação OutputMediaAssets referenciadas através de um " METADATA: uri" par nome / valor.
>
>

* InputMediaAssets mapeia tooone ou mais recursos que criou nos Media Services. OutputMediaAssets são criados pelo sistema Olá. Não faça referência a um recurso existente.
* OutputMediaAssets pode ter um nome utilizando Olá assetName atributo. Se este atributo não está presente, em seguida, nome de Olá do Olá OutputMediaAsset é qualquer valor de texto interno Olá de Olá <outputAsset> elemento está com um sufixo de valor de nome de tarefa Olá ou valor de Id da tarefa de Olá (no caso de Olá em que a propriedade de nome de Olá não está definida). Por exemplo, se definir um valor para assetName demasiado "Sample", em seguida, Olá seria possível definir a propriedade de nome de OutputMediaAsset demasiado "Sample". No entanto, se não definido um valor para assetName, mas definido o nome da tarefa Olá demasiado "NewJob", em seguida, Olá OutputMediaAsset nome seria "_NewJob JobOutputAsset (valor)".

    Olá seguinte exemplo mostra como tooset Olá assetName atributo:

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* tooenable encadeamento de tarefas:

  * Uma tarefa tem de ter, pelo menos, duas tarefas
  * Tem de existir pelo menos uma tarefa cuja entrada é a saída da tarefa na tarefa de Olá.

Para obter mais informações, consulte [criar uma tarefa de codificação com Olá API de REST dos serviços de suporte de dados](media-services-rest-encode-asset.md).

### <a name="monitor-processing-progress"></a>Monitor de processamento de progresso
Pode obter o estado da tarefa Olá utilizando a propriedade de estado de Olá, conforme mostrado no seguinte exemplo de Olá.

**Pedido de HTTP**

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


**Resposta de HTTP**

Se tiver êxito, é devolvido Olá seguinte resposta:

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 17
    Content-Type: application/json;odata=verbose;charset=utf-8
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 01324d81-18e2-4493-a3e5-c6186209f0c8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Sun, 13 May 2012 05:16:53 GMT

    {"d":{"State":2}}


### <a name="cancel-a-job"></a>Cancelar uma tarefa
Os Media Services permite-lhe toocancel tarefas em execução através de Olá CancelJob função. Esta chamada devolve um código de 400 erro se tentar toocancel uma tarefa quando o estado é cancelado, cancelar, erro ou foi concluída.

Olá seguinte exemplo mostra como toocall CancelJob.

**Pedido de HTTP**

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


Se tiver êxito, é devolvido um código de 204 resposta com nenhum corpo da mensagem.

> [!NOTE]
> Tem o id da tarefa Olá codificar o URL (normalmente nb:jid:UUID: somevalue) ao transmiti-lo na como tooCancelJob um parâmetro.
>
>

### <a name="get-hello-output-asset"></a>Obter o elemento de saída Olá
Olá código seguinte mostra como toorequest Olá saída asset ID.

**Pedido de HTTP**

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


**Resposta de HTTP**

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 445
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    x-ms-request-id: 73cd605d-066a-46f1-8358-f4bd25a9220a
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 08:28:13 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets",
       "value":[  
          {  
             "Id":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "State":0,
             "Created":"2015-01-19T07:52:15.603",
             "LastModified":"2015-01-19T07:52:15.603",
             "AlternateId":null,
             "Name":"Multibitrate MP4s",
             "Options":0,
             "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c",
             "StorageAccountName":"storagetestaccount001"
          }
       ]
    }



## <a id="publish_get_urls"></a>Publicar asset Olá e get de transmissão em fluxo e transferência progressiva URLs REST API

toostream ou transferir um recurso, primeiro tem de demasiado "publicar"-lo, criando um localizador. Os localizadores fornecem toofiles acesso contidos no elemento de Olá. Os Media Services suportam dois tipos de Localizadores: OnDemandOrigin localizadores, toostream utilizados suportes de dados (por exemplo, MPEG DASH, HLS ou transmissão em fluxo uniforme) e localizadores de assinatura de acesso (SAS), utilizados ficheiros de multimédia toodownload. Para obter mais informações sobre SAS localizadores consulte [isto](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogue.

Depois de criar os localizadores Olá, pode criar URLs de Olá que são utilizado toostream ou transferir os seus ficheiros.

>[!NOTE]
>Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado. toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado.

Um URL de transmissão em fluxo para transmissão em fluxo uniforme tem Olá seguinte formato:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

Um URL de transmissão em fluxo para HLS tem Olá seguinte formato:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

Um URL de transmissão em fluxo para MPEG DASH tem Olá seguinte formato:

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Ficheiros de toodownload um URL SAS utilizado tem Olá seguinte formato:

    {blob container name}/{asset name}/{file name}/{SAS signature}

Esta secção mostra como seguinte de Olá tooperform tarefas necessárias demasiado "publicar" os elementos.  

* Criar Olá AccessPolicy com permissão de leitura
* Criar um URL SAS para transferir conteúdo
* Criar um URL de origem para conteúdo de transmissão em fluxo

### <a name="creating-hello-accesspolicy-with-read-permission"></a>Criar Olá AccessPolicy com permissão de leitura
Antes de transferir ou qualquer conteúdo de multimédia de transmissão em fluxo, definir em primeiro lugar um AccessPolicy com permissões para ler e criar a entidade localizador adequada Olá que especifica o tipo de Olá de mecanismo de entrega que pretende tooenable para os seus clientes. Para obter mais informações sobre as propriedades de Olá disponíveis, consulte [propriedades de entidade AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).

Olá seguinte exemplo mostra como toospecify Olá AccessPolicy para permissões de leitura para um ativo especificado.

    POST https://wamsbayclus001rest-hs.net/API/AccessPolicies HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 74
    Expect: 100-continue

    {"Name": "DownloadPolicy", "DurationInMinutes" : "300", "Permissions" : 1}

Se tiver êxito, é devolvido um código de 201 êxito que descrevem a entidade de AccessPolicy Olá que criou. Em seguida, utilize Olá AccessPolicy Id juntamente com Olá Id de recurso do elemento de Olá que contenha os ficheiros de Olá pretende que a entidade de localizador de Olá de toocreate toodeliver (por exemplo, um elemento de saída).

> [!NOTE]
> Este fluxo de trabalho básico é Olá igual ao carregar um ficheiro quando um recurso de ingestão de relacionadas (conforme foi apresentadas anteriormente neste tópico). Além disso, como carregar ficheiros, se precisam de utilizador (ou os seus clientes) tooaccess os ficheiros imediatamente, defina os minutos de toofive de valor de StartTime antes Olá hora atual. Esta ação é necessária porque poderá haver relógio dissimetrias entre o cliente de Olá e dos Media Services. Olá StartTime valor tem de constar Olá seguir o formato DateTime: aaaa-MM-aaaathh (por exemplo, "2014-05-23T17:53:50Z").
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a>Criar um URL SAS para transferir conteúdo
Olá código a seguir mostra como tooget um URL que pode ser utilizado toodownload um ficheiro de multimédia criado e carregou anteriormente. Olá AccessPolicy tem conjunto de permissões de leitura e o caminho de localizador Olá refere-se o URL de transferência do tooa SAS.

    POST https://wamsbayclus001rest-hs.net/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-b1ae-2233-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c", "StartTime" : "2014-05-17T16:45:53", "Type":1}

Se tiver êxito, é devolvido Olá seguinte resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 1150
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 8cfd8556-3064-416a-97f2-67d9e35f0911
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:32 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A8e5a821d-2194-4d00-8884-adf979856874')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/Asset"
             }
          },
          "Id":"nb:lid:UUID:8e5a821d-2194-4d00-8884-adf979856874",
          "ExpirationDateTime":"\/Date(1337049393000)\/",
          "Type":1,
          "Path":"https://storagetestaccount001.blob.core.windows.net/asset-71d2dd33-efdf-ec43-8ea1-136a110bd42c?st=2012-05-14T21%3A36%3A33Z&se=2012-05-15T02%3A36%3A33Z&sr=c&si=8e5a821d-2194-4d00-8884-adf979856874&sig=y75dViDpC5V8WutrXM%2B%2FGpR3uOtqmlISiNlHU1YUBOg%3D",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:71d2dd33-efdf-ec43-8ea1-136a110bd42c",
          "StartTime":"\/Date(1337031393000)\/"
       }
    }


Olá devolvido **caminho** propriedade contém Olá SAS URL.

> [!NOTE]
> Se transferir conteúdo do armazenamento encriptado, tem manualmente desencriptá-lo antes de composição, ou utilize Olá MediaProcessor de desencriptação de armazenamento num toooutput de tarefa de processamento processados ficheiros Olá limpar tooan OutputAsset e, em seguida, transferir a partir desse recurso. Para obter mais informações sobre o processamento, consulte Criar uma tarefa de codificação com Olá API de REST dos serviços de suporte de dados. Além disso, os localizadores de URL SAS não pode ser atualizados depois de terem sido criadas. Por exemplo, não é possível reutilizar Olá localizador mesmo com um valor de StartTime atualizado. Trata-se devido a forma de Olá URLs de SAS que são criados. Se quiser tooaccess um recurso para transferência após um localizador tiver expirado, terá de criar um novo com uma StartTime novo.
>
>

### <a name="download-files"></a>Transferir ficheiros
Assim que tiver Olá AccessPolicy e o conjunto de localizador, pode transferir ficheiros utilizando Olá APIs de REST de armazenamento do Azure.  

> [!NOTE]
> Tem de adicionar o nome de ficheiro Olá ficheiro Olá pretende toodownload toohello localizador **caminho** valor recebido na secção anterior Olá. Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . .
>
>

Para obter mais informações sobre como trabalhar com blobs de armazenamento do Azure, consulte [API de REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

Como resultado Olá codificação tarefa que efetuou anteriormente (codificação num conjunto de MP4 adaptável), terá de vários ficheiros MP4 que pode transferir progressivamente. Por exemplo:    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a>Criar um URL de transmissão em fluxo para conteúdos de transmissão em fluxo
Olá a seguir mostra código como toocreate um localizador de URL de transmissão em fluxo:

    POST https://wamsbayclus001rest-hs/API/Locators HTTP/1.1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1337067658&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=dithjGvlXR9HlyAf5DE99N5OCYkPAxsHIcsTSjm9%2fVE%3d
    Host: wamsbayclus001rest-hs
    Content-Length: 182
    Expect: 100-continue

    {"AccessPolicyId": "nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8", "AssetId" : "nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3", "StartTime" : "2014-05-17T16:45:53",, "Type":2}

Se tiver êxito, é devolvido Olá seguinte resposta:

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 981
    Content-Type: application/json;odata=verbose;charset=utf-8
    Location: https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')
    Server: Microsoft-IIS/7.5
    x-ms-request-id: 2eac4158-fc78-4fa2-81ee-c9f582dc385f
    X-Content-Type-Options: nosniff
    DataServiceVersion: 1.0;
    X-AspNet-Version: 4.0.30319
    X-Powered-By: ASP.NET
    Date: Mon, 14 May 2012 21:41:39 GMT

    {  
       "d":{  
          "__metadata":{  
             "id":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')",
             "type":"Microsoft.Cloud.Media.Vod.Rest.Data.Models.Locator"
          },
          "AccessPolicy":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/AccessPolicy"
             }
          },
          "Asset":{  
             "__deferred":{  
                "uri":"https://wamsbayclus001rest-hs.net/api/Locators('nb%3Alid%3AUUID%3A52034bf6-dfae-4d83-aad3-3bd87dcb1a5d')/Asset"
             }
          },
          "Id":"nb:lid:UUID:52034bf6-dfae-4d83-aad3-3bd87dcb1a5d",
          "ExpirationDateTime":"\/Date(1337049395000)\/",
          "Type":2,
          "Path":"http://wamsbayclus001rest-hs.net/52034bf6-dfae-4d83-aad3-3bd87dcb1a5d/",
          "AccessPolicyId":"nb:pid:UUID:38c71dd0-44c5-4c5f-8418-08bb6fbf7bf8",
          "AssetId":"nb:cid:UUID:eb5540a2-116e-4d36-b084-7e9958f7f3c3",
          "StartTime":"\/Date(1337031395000)\/"
       }
    }

toostream um URL de origem de transmissão em fluxo uniforme num leitor de multimédia de transmissão em fluxo, tem de anexar a propriedade Path Olá com nome Olá Olá transmissão em fluxo uniforme manifesto do ficheiro, seguido por "/ manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

toostream HLS, acrescente (formato = m3u8-aapl) após Olá "/ manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

toostream MPEG DASH, acrescente (formato = mpd-time-csf) após Olá "/ manifest".

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <a id="play"></a>Reproduza o seu conteúdo
toostream vídeo, utilize [leitor de Media Services do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

tootest transferência progressiva transferir, cole um URL no browser (por exemplo, IE, Chrome, Safari).

## <a name="next-steps-media-services-learning-paths"></a>Passos Seguintes: percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
