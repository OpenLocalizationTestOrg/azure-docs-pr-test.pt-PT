---
title: ficheiros de aaaUpload para uma conta de Media Services utilizando REST | Microsoft Docs
description: "Saiba como tooget suporte de dados de conteúdo para os serviços de suporte de dados através da criação e carregar ativos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 41df7cbe-b8e2-48c1-a86c-361ec4e5251f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 2a92cecdc32d747d7a478946f069c15931eb32b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-rest"></a>Carregar ficheiros para uma conta de Media Services utilizando REST
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> * [Portal](media-services-portal-upload-files.md)
> 
> 

Nos Serviços de Multimédia, os ficheiros digitais são carregados para um elemento. Olá [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto controla e legendas ficheiros (e Olá metadados sobre estes ficheiros.)  Depois de ficheiros de Olá são carregados para o elemento de Olá, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo. 

> [!NOTE]
> aplicar Olá seguintes considerações:
> 
> * Os Media Services utiliza o valor de Olá de Olá IAssetFile.Name propriedade quando criar os URLs do Olá transmissão em fluxo conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por este motivo, por cento de codificação não é permitida. Olá, valor de Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [por cento codificação-reservados carateres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ". Além disso, só pode existir um '.' para a extensão de nome de ficheiro Olá.
> * o comprimento do nome de Olá Olá não deve ser superior a 260 carateres.
> * Não há um limite toohello tamanho máximo suportado para processamento nos Media Services. Consulte [isto](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre limitação de tamanho de ficheiro Olá.
> 

fluxo de trabalho básico Olá do carregamento de recursos está dividido em Olá seguintes secções:

* Criar um recurso
* Encriptar um elemento (opcional)
* Carregar um tooblob de armazenamento de ficheiros

AMS também permite-lhe elementos de tooupload em massa. Para obter mais informações, veja [esta](media-services-rest-upload-files.md#upload_in_bulk) secção.

> [!NOTE]
> Ao aceder a entidades nos Media Services, tem de definir campos de cabeçalho específicos e os valores no seus pedidos HTTP. Para obter mais informações, consulte [programa de configuração para o desenvolvimento de API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).
> 

## <a name="connect-toomedia-services"></a>Ligar a serviços tooMedia

Para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

>[!NOTE]
>Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados. É necessário efetuar chamadas subsequentes toohello novo URI.

## <a name="upload-assets"></a>Carregar recursos

### <a name="create-an-asset"></a>Criar um recurso

Um recurso é um contentor para vários tipos ou conjuntos de objetos nos Media Services, incluindo as vídeo, áudio, imagens, coleções de miniaturas, controla de texto e legendas ficheiros. No Olá API REST, criar um recurso necessita de enviar a mensagem de pedido tooMedia serviços e colocar quaisquer informações de propriedade sobre o elemento no corpo do pedido de Olá.

Uma das propriedades de Olá que pode especificar quando a criação de um recurso é **opções**. **Opções de** é um valor de enumeração que descreve as opções de encriptação de Olá um recurso que pode ser criado com. Um valor válido é de um dos valores de Olá Olá na lista abaixo, não uma combinação de valores. 

* **Nenhum** = **0**: será utilizada sem encriptação. Este é o valor predefinido de Olá. Tenha em atenção que ao utilizar esta opção o conteúdo não está protegido em trânsito ou inativo no armazenamento.
    Se planear toodeliver um MP4 utilizando transferência progressiva, utilize esta opção. 
* **StorageEncrypted** = **1**: Especifique se pretende para a sua toobe ficheiros encriptado com AES 256 bits encriptação de carregamento e de armazenamento.
  
    Se o seu elemento armazenamento encriptado, tem de configurar política de entrega de elementos. Para obter mais informações consulte [configurar política de entrega de elemento](media-services-rest-configure-asset-delivery-policy.md).
* **CommonEncryptionProtected** = **2**: Especifique se estiver a carregar os ficheiros protegidos com um método de encriptação comum (tais como PlayReady). 
* **EnvelopeEncryptionProtected** = **4**: Especifique se estiver a carregar HLS encriptado com ficheiros AES. Tenha em atenção que ficheiros Olá tem de ter sido codificados e encriptados pelo Gestor de transformação.

> [!NOTE]
> Se o seu elemento irá utilizar a encriptação, tem de criar um **ContentKey** e ligá-lo tooyour asset conforme descrito no seguinte tópico de Olá:[como toocreate um ContentKey](media-services-rest-create-contentkey.md). Tenha em atenção que depois de carregar ficheiros Olá para elemento de Olá, terá de propriedades de encriptação de Olá tooupdate no Olá **AssetFile** entidade com valores de Olá recebeu durante Olá **Asset** encriptação. Fazê-lo utilizando Olá **intercalar** pedido de HTTP. 
> 
> 

Olá seguinte exemplo mostra como toocreate um recurso.

**Pedido de HTTP**

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny.mp4"}

**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTP/1.1 201 Created
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
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":0,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

### <a name="create-an-assetfile"></a>Criar um AssetFile
Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um ficheiro de vídeo ou áudio que é armazenado num contentor de blob. Um ficheiro de recurso é sempre associado a um recurso e um recurso pode conter um ou vários ficheiros de recurso. tarefa de codificador de serviços de multimédia de Olá falhar se um objeto de ficheiro de recurso não está associado um ficheiro digital num contentor de blob.

Tenha em atenção que Olá **AssetFile** instância e o ficheiro de multimédia real de Olá estão dois objetos distintos. instância de AssetFile Olá contém metadados sobre ficheiros de suporte de dados de Olá, enquanto o ficheiro de multimédia Olá contém conteúdo de multimédia real Olá.

Depois de carregar o ficheiro de suporte de dados digitais num contentor de blob, irá utilizar Olá **intercalar** HTTP pedido tooupdate Olá AssetFile com informações sobre o ficheiro de suporte de dados (conforme mostrado posteriormente tópico Olá). 

**Pedido de HTTP**

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
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

### <a name="creating-hello-accesspolicy-with-write-permission"></a>A criar Olá AccessPolicy com permissão de escrita.

>[!NOTE]
>Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy). Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso. Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

Antes de carregar ficheiros para o armazenamento de BLOBs, defina acesso Olá direitos de política para escrever tooan ativo. Definir toodo que, após um toohello de pedido HTTP AccessPolicies entidade. Definir um valor de DurationInMinutes após a criação ou irá receber uma mensagem de erro de servidor interno 500 na resposta. Para obter mais informações sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).

Olá seguinte exemplo mostra como toocreate um AccessPolicy:

**Pedido de HTTP**

    POST https://media.windows.net/api/AccessPolicies HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"NewUploadPolicy", "DurationInMinutes":"440", "Permissions":"2"} 

**Pedido de HTTP**

    If successful, hello following response is returned:

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
tooreceive Olá URL de carregamento real, crie um localizador SAS. Localizadores definem a hora de início Olá e o tipo de ponto final de ligação para os clientes que pretendem ficheiros tooaccess um recurso. Pode criar várias entidades de localizador para um determinado AccessPolicy e Asset par toohandle diferentes cliente pedidos e as suas necessidades. Cada um destes localizadores utilize o valor de StartTime Olá plus valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá o comprimento de tempo pode ser utilizado um URL. Para obter mais informações, consulte [localizador](https://docs.microsoft.com/rest/api/media/operations/locator).

Um URL SAS tem Olá seguinte formato:

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

São aplicáveis algumas considerações:

* Não pode ter mais de cinco localizadores exclusivos associados um determinado elemento de uma só vez. Para obter mais informações, consulte localizador.
* Se precisar de tooupload os ficheiros imediatamente, deve definir os minutos de toofive de valor de StartTime antes Olá hora atual. Isto acontece porque poderá haver relógio dissimetrias entre o computador cliente e os Media Services. Além disso, o valor de StartTime tem de constar Olá seguir o formato DateTime: aaaa-MM-aaaathh (por exemplo, "2014-05-23T17:53:50Z").    
* Poderá existir um segundo 30-40 atrasar depois de criar um localizador toowhen está disponível para utilização. Aplica-se este problema tooboth SAS URL e localizadores de origem.

Olá seguinte exemplo mostra como toocreate um localizador de URL SAS, tal como definido por Olá propriedade de tipo no corpo do pedido de Olá ("1" para um localizador SAS) e "2" para um localizador de origem no pedido. Olá **caminho** propriedade devolvida contém um URL de Olá que tem de utilizar tooupload o ficheiro.

**Pedido de HTTP**

    POST https://media.windows.net/api/Locators HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
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
Assim que tiver Olá AccessPolicy e o conjunto de localizador, real do ficheiro Olá é carregado tooan contentor de Blob Storage do Azure utilizando Olá APIs de REST de armazenamento do Azure. Tem de carregar ficheiros Olá como blobs de blocos. Os blobs de página não são suportados pelos Media Services do Azure.  

> [!NOTE]
> Tem de adicionar o nome de ficheiro Olá ficheiro Olá pretende tooupload toohello localizador **caminho** valor recebido na secção anterior Olá. Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4? . . . 
> 
> 

Para obter mais informações sobre como trabalhar com blobs de armazenamento do Azure, consulte [API de REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).

### <a name="update-hello-assetfile"></a>Atualizar Olá AssetFile
Agora que carregar o ficheiro, atualize informações do Olá FileAsset tamanho (e outros). Por exemplo:

    MERGE https://media.windows.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5') HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {  
       "ContentFileSize":"1186540",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }


**Resposta de HTTP**

Se tiver êxito, seguinte Olá é devolvido: HTTP/1.1 204 não conteúdo

### <a name="delete-hello-locator-and-accesspolicy"></a>Eliminar Olá localizador e AccessPolicy
**Pedido de HTTP**

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTTP/1.1 204 No Content 
    ...

**Pedido de HTTP**

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

**Resposta de HTTP**

Se tiver êxito, é devolvido o seguinte Olá:

    HTTP/1.1 204 No Content 
    ...

## <a id="upload_in_bulk"></a>Carregar recursos em massa
### <a name="create-hello-ingestmanifest"></a>Criar Olá IngestManifest
Olá IngestManifest é um contentor para um conjunto de recursos, ficheiros de recurso e informações de estatística que podem ser utilizado o progresso de Olá toodetermine de ingestão relacionadas em massa para o conjunto de Olá.

**Pedido de HTTP**

    POST https:// media.windows.net/API/IngestManifests HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 36
    Expect: 100-continue

    { "Name" : "ExampleManifestREST" }

### <a name="create-assets"></a>Criar ativos
Antes de criar Olá IngestManifestAsset, terá de toocreate Olá recurso que será concluído com ingestão relacionadas em massa. Um recurso é um contentor para vários tipos ou conjuntos de objetos nos Media Services, incluindo as vídeo, áudio, imagens, coleções de miniaturas, controla de texto e legendas ficheiros. Na REST API Olá, criar um recurso necessita de enviar um tooMicrosoft de pedido de HTTP POST Media Services do Azure e colocar quaisquer informações de propriedade sobre o elemento no corpo do pedido de Olá. Neste exemplo, Olá recurso é criado utilizando a opção de StorageEncrption(1) Olá incluída no corpo do pedido Olá.

**Resposta de HTTP**

    POST https://media.windows.net/API/Assets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 55
    Expect: 100-continue

    { "Name" : "ExampleManifestREST_Asset", "Options" : 1 }

### <a name="create-hello-ingestmanifestassets"></a>Criar Olá IngestManifestAssets
IngestManifestAssets representam ativos dentro de um IngestManifest que são utilizados com ingestão relacionadas em massa. Olá basicamente o manifesto de toohello Olá recurso da hiperligação. Media Services do Azure internamente observa Olá carregamento de ficheiros com base no toohello de coleção associada IngestManifestFiles IngestManifestAsset. Assim que estes ficheiros são carregados, asset Olá está concluída. Pode criar um novo IngestManifestAsset com um pedido POST de HTTP. No corpo do pedido de Olá, incluem Olá IngestManifest Id e Olá Id de recurso que Olá IngestManifestAsset deve ligar em conjunto para ingestão relacionadas em massa.

**Resposta de HTTP**

    POST https://media.windows.net/API/IngestManifestAssets HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 152
    Expect: 100-continue
    { "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "Asset" : { "Id" : "nb:cid:UUID:b757929a-5a57-430b-b33e-c05c6cbef02e"}}


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a>Criar Olá IngestManifestFiles para cada recurso
Um IngestManifestFile representa um objeto de blob de vídeo ou áudio real que será carregado como parte da ingestão relacionadas em massa para um recurso. Encriptação relacionadas com propriedades não são necessárias, a menos que o recurso de Olá está a utilizar uma opção de encriptação. exemplo de Olá utilizado nesta secção demonstra a criação de um IngestManifestFile que utiliza StorageEncryption para Olá recurso que criou anteriormente.

**Resposta de HTTP**

    POST https://media.windows.net/API/IngestManifestFiles HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 367
    Expect: 100-continue

    { "Name" : "REST_Example_File.wmv", "ParentIngestManifestId" : "nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048", "ParentIngestManifestAssetId" : "nb:maid:UUID:beed8531-9a03-9043-b1d8-6a6d1044cdda", "IsEncrypted" : "true", "EncryptionScheme" : "StorageEncryption", "EncryptionVersion" : "1.0", "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510" }

### <a name="upload-hello-files-tooblob-storage"></a>Carregar ficheiros de Olá tooBlob armazenamento
Pode utilizar qualquer aplicação de cliente de alta velocidade com capacidade de carregar Olá asset ficheiros toohello contentor de blob storage Uri fornecido pelo Olá propriedade BlobStorageUriForUpload Olá IngestManifest. É um serviço de carregamento de alta velocidade acentuadas [Aspera a pedido para a aplicação Azure](http://go.microsoft.com/fwlink/?LinkId=272001).

### <a name="monitor-bulk-ingest-progress"></a>Progresso de inserção em massa do monitor
Pode monitorizar o progresso Olá em massa ingestão de operações para um IngestManifest relacionadas através de consultas de propriedade de estatísticas de Olá de Olá IngestManifest. Se a propriedade é um tipo complexo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics). Olá toopoll propriedade estatísticas, submeter um pedido de HTTP GET transmitir Olá IngestManifest ID

## <a name="create-contentkeys-used-for-encryption"></a>Criar ContentKeys utilizada para encriptação
Se o seu elemento irá utilizar a encriptação, tem de criar Olá ContentKey toobe utilizada para encriptação antes de criar Olá ficheiros de recurso. Para a encriptação de armazenamento, hello propriedades seguintes devem ser incluídas no corpo do pedido de Olá.

| Propriedade de corpo do pedido | Descrição |
| --- | --- |
| Id |Olá ContentKey Id que geramos ourselves utilizando Olá seguir formatar, "nb:kid:UUID:<NEW GUID>". |
| ContentKeyType |Este é o tipo de chave de conteúdo de Olá como um valor inteiro para esta chave de conteúdo. Podemos transmitir o valor de Olá 1 para a encriptação de armazenamento. |
| EncryptedContentKey |Vamos criar um novo valor de chave conteúdo que é um valor de 256 bits (32 byte). chave de Olá é encriptada utilizando o certificado x. 509 de encriptação de armazenamento de Olá que obtemos Media Services do Microsoft Azure ao executar um pedido HTTP GET Olá GetProtectionKeyId e GetProtectionKey métodos. |
| ProtectionKeyId |Isto é Olá id de chave de proteção para o certificado x. 509 de encriptação de armazenamento de Olá que foi utilizado tooencrypt nosso chave de conteúdo. |
| ProtectionKeyType |Este é o tipo de encriptação de Olá para a chave de proteção de Olá que estava a chave de conteúdo de Olá tooencrypt utilizados. Este valor é StorageEncryption(1) para o nosso exemplo. |
| Soma de verificação |Olá MD5 calculada soma de verificação para a chave de conteúdo de Olá. Esta é calculada ao encriptar o conteúdo de Olá Id com a chave de conteúdo de Olá. código de exemplo de Olá demonstra como toocalculate Olá soma de verificação. |

**Resposta de HTTP**

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 572
    Expect: 100-continue

    {"Id" : "nb:kid:UUID:316d14d4-b603-4d90-b8db-0fede8aa48f8", "ContentKeyType" : 1, "EncryptedContentKey" : "Y4NPej7heOFa2vsd8ZEOcjjpu/qOq3RJ6GRfxa8CCwtAM83d6J2mKOeQFUmMyVXUSsBCCOdufmieTKi+hOUtNAbyNM4lY4AXI537b9GaY8oSeje0NGU8+QCOuf7jGdRac5B9uIk7WwD76RAJnqyep6U/OdvQV4RLvvZ9w7nO4bY8RHaUaLxC2u4aIRRaZtLu5rm8GKBPy87OzQVXNgnLM01I8s3Z4wJ3i7jXqkknDy4VkIyLBSQvIvUzxYHeNdMVWDmS+jPN9ScVmolUwGzH1A23td8UWFHOjTjXHLjNm5Yq+7MIOoaxeMlKPYXRFKofRY8Qh5o5tqvycSAJ9KUqfg==", "ProtectionKeyId" : "7D9BB04D9D0A4A24800CADBFEF232689E048F69C", "ProtectionKeyType" : 1, "Checksum" : "TfXtjCIlq1Y=" }

### <a name="link-hello-contentkey-toohello-asset"></a>Olá ContentKey toohello recurso de ligação
Olá ContentKey é tooone associado ou mais recursos ao enviar um pedido POST de HTTP. Olá pedido seguinte é um exemplo toolink Olá exemplo ContentKey toohello exemplo recurso por ID.

**Resposta de HTTP**

    POST https://media.windows.net/API/Assets('nb:cid:UUID:b3023475-09b4-4647-9d6d-6fc242822e68')/$links/ContentKeys HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net
    Content-Length: 113
    Expect: 100-continue

    { "uri": "https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A32e6efaf-5fba-4538-b115-9d1cefe43510')"}

**Resposta de HTTP**

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a>Passos seguintes

Agora, pode codificar os elementos que carregar. Para obter mais informações, veja [Codificar elementos](media-services-portal-encode.md)

Também pode utilizar as funções do Azure tootrigger uma tarefa de codificação baseada num ficheiro chegar no contentor de Olá configurado. Para obter mais informações, veja [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

