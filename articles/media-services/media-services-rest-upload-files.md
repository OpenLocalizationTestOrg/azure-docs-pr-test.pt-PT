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
# <a name="upload-files-into-a-media-services-account-using-rest"></a><span data-ttu-id="36fed-103">Carregar ficheiros para uma conta de Media Services utilizando REST</span><span class="sxs-lookup"><span data-stu-id="36fed-103">Upload files into a Media Services account using REST</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36fed-104">.NET</span><span class="sxs-lookup"><span data-stu-id="36fed-104">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="36fed-105">REST</span><span class="sxs-lookup"><span data-stu-id="36fed-105">REST</span></span>](media-services-rest-upload-files.md)
> * [<span data-ttu-id="36fed-106">Portal</span><span class="sxs-lookup"><span data-stu-id="36fed-106">Portal</span></span>](media-services-portal-upload-files.md)
> 
> 

<span data-ttu-id="36fed-107">Nos Serviços de Multimédia, os ficheiros digitais são carregados para um elemento.</span><span class="sxs-lookup"><span data-stu-id="36fed-107">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="36fed-108">Olá [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto controla e legendas ficheiros (e Olá metadados sobre estes ficheiros.)  Depois de ficheiros de Olá são carregados para o elemento de Olá, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="36fed-108">hello [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span> 

> [!NOTE]
> <span data-ttu-id="36fed-109">aplicar Olá seguintes considerações:</span><span class="sxs-lookup"><span data-stu-id="36fed-109">hello following considerations apply:</span></span>
> 
> * <span data-ttu-id="36fed-110">Os Media Services utiliza o valor de Olá de Olá IAssetFile.Name propriedade quando criar os URLs do Olá transmissão em fluxo conteúdo (por exemplo, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Por este motivo, por cento de codificação não é permitida.</span><span class="sxs-lookup"><span data-stu-id="36fed-110">Media Services uses hello value of hello IAssetFile.Name property when building URLs for hello streaming content (for example, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) For this reason, percent-encoding is not allowed.</span></span> <span data-ttu-id="36fed-111">Olá, valor de Olá **nome** propriedade não pode ter qualquer um dos seguintes Olá [por cento codificação-reservados carateres](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] ".</span><span class="sxs-lookup"><span data-stu-id="36fed-111">hello value of hello **Name** property cannot have any of hello following [percent-encoding-reserved characters](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters): !*'();:@&=+$,/?%#[]".</span></span> <span data-ttu-id="36fed-112">Além disso, só pode existir um '.' para a extensão de nome de ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-112">Also, there can only be one '.' for hello file name extension.</span></span>
> * <span data-ttu-id="36fed-113">o comprimento do nome de Olá Olá não deve ser superior a 260 carateres.</span><span class="sxs-lookup"><span data-stu-id="36fed-113">hello length of hello name should not be greater than 260 characters.</span></span>
> * <span data-ttu-id="36fed-114">Não há um limite toohello tamanho máximo suportado para processamento nos Media Services.</span><span class="sxs-lookup"><span data-stu-id="36fed-114">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="36fed-115">Consulte [isto](media-services-quotas-and-limitations.md) tópico para obter detalhes sobre limitação de tamanho de ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-115">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
> 

<span data-ttu-id="36fed-116">fluxo de trabalho básico Olá do carregamento de recursos está dividido em Olá seguintes secções:</span><span class="sxs-lookup"><span data-stu-id="36fed-116">hello basic workflow for uploading Assets is divided into hello following sections:</span></span>

* <span data-ttu-id="36fed-117">Criar um recurso</span><span class="sxs-lookup"><span data-stu-id="36fed-117">Create an Asset</span></span>
* <span data-ttu-id="36fed-118">Encriptar um elemento (opcional)</span><span class="sxs-lookup"><span data-stu-id="36fed-118">Encrypt an Asset (Optional)</span></span>
* <span data-ttu-id="36fed-119">Carregar um tooblob de armazenamento de ficheiros</span><span class="sxs-lookup"><span data-stu-id="36fed-119">Upload a file tooblob storage</span></span>

<span data-ttu-id="36fed-120">AMS também permite-lhe elementos de tooupload em massa.</span><span class="sxs-lookup"><span data-stu-id="36fed-120">AMS also enables you tooupload assets in bulk.</span></span> <span data-ttu-id="36fed-121">Para obter mais informações, veja [esta](media-services-rest-upload-files.md#upload_in_bulk) secção.</span><span class="sxs-lookup"><span data-stu-id="36fed-121">For more information, see [this](media-services-rest-upload-files.md#upload_in_bulk) section.</span></span>

> [!NOTE]
> <span data-ttu-id="36fed-122">Ao aceder a entidades nos Media Services, tem de definir campos de cabeçalho específicos e os valores no seus pedidos HTTP.</span><span class="sxs-lookup"><span data-stu-id="36fed-122">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="36fed-123">Para obter mais informações, consulte [programa de configuração para o desenvolvimento de API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="36fed-123">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>
> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="36fed-124">Ligar a serviços tooMedia</span><span class="sxs-lookup"><span data-stu-id="36fed-124">Connect tooMedia Services</span></span>

<span data-ttu-id="36fed-125">Para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="36fed-125">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="36fed-126">Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="36fed-126">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="36fed-127">É necessário efetuar chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="36fed-127">You must make subsequent calls toohello new URI.</span></span>

## <a name="upload-assets"></a><span data-ttu-id="36fed-128">Carregar recursos</span><span class="sxs-lookup"><span data-stu-id="36fed-128">Upload assets</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="36fed-129">Criar um recurso</span><span class="sxs-lookup"><span data-stu-id="36fed-129">Create an asset</span></span>

<span data-ttu-id="36fed-130">Um recurso é um contentor para vários tipos ou conjuntos de objetos nos Media Services, incluindo as vídeo, áudio, imagens, coleções de miniaturas, controla de texto e legendas ficheiros.</span><span class="sxs-lookup"><span data-stu-id="36fed-130">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="36fed-131">No Olá API REST, criar um recurso necessita de enviar a mensagem de pedido tooMedia serviços e colocar quaisquer informações de propriedade sobre o elemento no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-131">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="36fed-132">Uma das propriedades de Olá que pode especificar quando a criação de um recurso é **opções**.</span><span class="sxs-lookup"><span data-stu-id="36fed-132">One of hello properties that you can specify when creating an asset is **Options**.</span></span> <span data-ttu-id="36fed-133">**Opções de** é um valor de enumeração que descreve as opções de encriptação de Olá um recurso que pode ser criado com.</span><span class="sxs-lookup"><span data-stu-id="36fed-133">**Options** is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="36fed-134">Um valor válido é de um dos valores de Olá Olá na lista abaixo, não uma combinação de valores.</span><span class="sxs-lookup"><span data-stu-id="36fed-134">A valid value is one of hello values from hello list below, not a combination of values.</span></span> 

* <span data-ttu-id="36fed-135">**Nenhum** = **0**: será utilizada sem encriptação.</span><span class="sxs-lookup"><span data-stu-id="36fed-135">**None** = **0**: No encryption will be used.</span></span> <span data-ttu-id="36fed-136">Este é o valor predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-136">This is hello default value.</span></span> <span data-ttu-id="36fed-137">Tenha em atenção que ao utilizar esta opção o conteúdo não está protegido em trânsito ou inativo no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="36fed-137">Note that when using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="36fed-138">Se planear toodeliver um MP4 utilizando transferência progressiva, utilize esta opção.</span><span class="sxs-lookup"><span data-stu-id="36fed-138">If you plan toodeliver an MP4 using progressive download, use this option.</span></span> 
* <span data-ttu-id="36fed-139">**StorageEncrypted** = **1**: Especifique se pretende para a sua toobe ficheiros encriptado com AES 256 bits encriptação de carregamento e de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="36fed-139">**StorageEncrypted** = **1**: Specify if you want for your files toobe encrypted with AES-256 bit encryption for upload and storage.</span></span>
  
    <span data-ttu-id="36fed-140">Se o seu elemento armazenamento encriptado, tem de configurar política de entrega de elementos.</span><span class="sxs-lookup"><span data-stu-id="36fed-140">If your asset is storage encrypted, you must configure asset delivery policy.</span></span> <span data-ttu-id="36fed-141">Para obter mais informações consulte [configurar política de entrega de elemento](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="36fed-141">For more information see [Configuring asset delivery policy](media-services-rest-configure-asset-delivery-policy.md).</span></span>
* <span data-ttu-id="36fed-142">**CommonEncryptionProtected** = **2**: Especifique se estiver a carregar os ficheiros protegidos com um método de encriptação comum (tais como PlayReady).</span><span class="sxs-lookup"><span data-stu-id="36fed-142">**CommonEncryptionProtected** = **2**: Specify if you are uploading files protected with a common encryption method (such as PlayReady).</span></span> 
* <span data-ttu-id="36fed-143">**EnvelopeEncryptionProtected** = **4**: Especifique se estiver a carregar HLS encriptado com ficheiros AES.</span><span class="sxs-lookup"><span data-stu-id="36fed-143">**EnvelopeEncryptionProtected** = **4**: Specify if you are uploading HLS encrypted with AES files.</span></span> <span data-ttu-id="36fed-144">Tenha em atenção que ficheiros Olá tem de ter sido codificados e encriptados pelo Gestor de transformação.</span><span class="sxs-lookup"><span data-stu-id="36fed-144">Note that hello files must have been encoded and encrypted by Transform Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="36fed-145">Se o seu elemento irá utilizar a encriptação, tem de criar um **ContentKey** e ligá-lo tooyour asset conforme descrito no seguinte tópico de Olá:[como toocreate um ContentKey](media-services-rest-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="36fed-145">If your asset will use encryption, you must create a **ContentKey** and link it tooyour asset as described in hello following topic:[How toocreate a ContentKey](media-services-rest-create-contentkey.md).</span></span> <span data-ttu-id="36fed-146">Tenha em atenção que depois de carregar ficheiros Olá para elemento de Olá, terá de propriedades de encriptação de Olá tooupdate no Olá **AssetFile** entidade com valores de Olá recebeu durante Olá **Asset** encriptação.</span><span class="sxs-lookup"><span data-stu-id="36fed-146">Note that after you upload hello files into hello asset, you need tooupdate hello encryption properties on hello **AssetFile** entity with hello values you got during hello **Asset** encryption.</span></span> <span data-ttu-id="36fed-147">Fazê-lo utilizando Olá **intercalar** pedido de HTTP.</span><span class="sxs-lookup"><span data-stu-id="36fed-147">Do it by using hello **MERGE** HTTP request.</span></span> 
> 
> 

<span data-ttu-id="36fed-148">Olá seguinte exemplo mostra como toocreate um recurso.</span><span class="sxs-lookup"><span data-stu-id="36fed-148">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="36fed-149">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-149">**HTTP Request**</span></span>

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

<span data-ttu-id="36fed-150">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-150">**HTTP Response**</span></span>

<span data-ttu-id="36fed-151">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="36fed-151">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="36fed-152">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="36fed-152">Create an AssetFile</span></span>
<span data-ttu-id="36fed-153">Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um ficheiro de vídeo ou áudio que é armazenado num contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="36fed-153">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="36fed-154">Um ficheiro de recurso é sempre associado a um recurso e um recurso pode conter um ou vários ficheiros de recurso.</span><span class="sxs-lookup"><span data-stu-id="36fed-154">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="36fed-155">tarefa de codificador de serviços de multimédia de Olá falhar se um objeto de ficheiro de recurso não está associado um ficheiro digital num contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="36fed-155">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="36fed-156">Tenha em atenção que Olá **AssetFile** instância e o ficheiro de multimédia real de Olá estão dois objetos distintos.</span><span class="sxs-lookup"><span data-stu-id="36fed-156">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="36fed-157">instância de AssetFile Olá contém metadados sobre ficheiros de suporte de dados de Olá, enquanto o ficheiro de multimédia Olá contém conteúdo de multimédia real Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-157">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="36fed-158">Depois de carregar o ficheiro de suporte de dados digitais num contentor de blob, irá utilizar Olá **intercalar** HTTP pedido tooupdate Olá AssetFile com informações sobre o ficheiro de suporte de dados (conforme mostrado posteriormente tópico Olá).</span><span class="sxs-lookup"><span data-stu-id="36fed-158">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span> 

<span data-ttu-id="36fed-159">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-159">**HTTP Request**</span></span>

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

<span data-ttu-id="36fed-160">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-160">**HTTP Response**</span></span>

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

### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="36fed-161">A criar Olá AccessPolicy com permissão de escrita.</span><span class="sxs-lookup"><span data-stu-id="36fed-161">Creating hello AccessPolicy with write permission.</span></span>

>[!NOTE]
><span data-ttu-id="36fed-162">Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="36fed-162">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="36fed-163">Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso.</span><span class="sxs-lookup"><span data-stu-id="36fed-163">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="36fed-164">Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="36fed-164">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="36fed-165">Antes de carregar ficheiros para o armazenamento de BLOBs, defina acesso Olá direitos de política para escrever tooan ativo.</span><span class="sxs-lookup"><span data-stu-id="36fed-165">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="36fed-166">Definir toodo que, após um toohello de pedido HTTP AccessPolicies entidade.</span><span class="sxs-lookup"><span data-stu-id="36fed-166">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="36fed-167">Definir um valor de DurationInMinutes após a criação ou irá receber uma mensagem de erro de servidor interno 500 na resposta.</span><span class="sxs-lookup"><span data-stu-id="36fed-167">Define a DurationInMinutes value upon creation or you will receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="36fed-168">Para obter mais informações sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="36fed-168">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="36fed-169">Olá seguinte exemplo mostra como toocreate um AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="36fed-169">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="36fed-170">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-170">**HTTP Request**</span></span>

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

<span data-ttu-id="36fed-171">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-171">**HTTP Request**</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="36fed-172">Obter Olá carregar URL</span><span class="sxs-lookup"><span data-stu-id="36fed-172">Get hello Upload URL</span></span>
<span data-ttu-id="36fed-173">tooreceive Olá URL de carregamento real, crie um localizador SAS.</span><span class="sxs-lookup"><span data-stu-id="36fed-173">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="36fed-174">Localizadores definem a hora de início Olá e o tipo de ponto final de ligação para os clientes que pretendem ficheiros tooaccess um recurso.</span><span class="sxs-lookup"><span data-stu-id="36fed-174">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="36fed-175">Pode criar várias entidades de localizador para um determinado AccessPolicy e Asset par toohandle diferentes cliente pedidos e as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="36fed-175">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="36fed-176">Cada um destes localizadores utilize o valor de StartTime Olá plus valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá o comprimento de tempo pode ser utilizado um URL.</span><span class="sxs-lookup"><span data-stu-id="36fed-176">Each of these Locators use hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="36fed-177">Para obter mais informações, consulte [localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="36fed-177">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="36fed-178">Um URL SAS tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="36fed-178">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="36fed-179">São aplicáveis algumas considerações:</span><span class="sxs-lookup"><span data-stu-id="36fed-179">Some considerations apply:</span></span>

* <span data-ttu-id="36fed-180">Não pode ter mais de cinco localizadores exclusivos associados um determinado elemento de uma só vez.</span><span class="sxs-lookup"><span data-stu-id="36fed-180">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="36fed-181">Para obter mais informações, consulte localizador.</span><span class="sxs-lookup"><span data-stu-id="36fed-181">For more information, see Locator.</span></span>
* <span data-ttu-id="36fed-182">Se precisar de tooupload os ficheiros imediatamente, deve definir os minutos de toofive de valor de StartTime antes Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="36fed-182">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="36fed-183">Isto acontece porque poderá haver relógio dissimetrias entre o computador cliente e os Media Services.</span><span class="sxs-lookup"><span data-stu-id="36fed-183">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="36fed-184">Além disso, o valor de StartTime tem de constar Olá seguir o formato DateTime: aaaa-MM-aaaathh (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="36fed-184">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="36fed-185">Poderá existir um segundo 30-40 atrasar depois de criar um localizador toowhen está disponível para utilização.</span><span class="sxs-lookup"><span data-stu-id="36fed-185">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="36fed-186">Aplica-se este problema tooboth SAS URL e localizadores de origem.</span><span class="sxs-lookup"><span data-stu-id="36fed-186">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="36fed-187">Olá seguinte exemplo mostra como toocreate um localizador de URL SAS, tal como definido por Olá propriedade de tipo no corpo do pedido de Olá ("1" para um localizador SAS) e "2" para um localizador de origem no pedido.</span><span class="sxs-lookup"><span data-stu-id="36fed-187">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="36fed-188">Olá **caminho** propriedade devolvida contém um URL de Olá que tem de utilizar tooupload o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="36fed-188">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="36fed-189">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-189">**HTTP Request**</span></span>

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

<span data-ttu-id="36fed-190">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-190">**HTTP Response**</span></span>

<span data-ttu-id="36fed-191">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="36fed-191">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="36fed-192">Carregue um ficheiro para um contentor de blob storage</span><span class="sxs-lookup"><span data-stu-id="36fed-192">Upload a file into a blob storage container</span></span>
<span data-ttu-id="36fed-193">Assim que tiver Olá AccessPolicy e o conjunto de localizador, real do ficheiro Olá é carregado tooan contentor de Blob Storage do Azure utilizando Olá APIs de REST de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="36fed-193">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure Blob Storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="36fed-194">Tem de carregar ficheiros Olá como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="36fed-194">You must upload hello files as block blobs.</span></span> <span data-ttu-id="36fed-195">Os blobs de página não são suportados pelos Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="36fed-195">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="36fed-196">Tem de adicionar o nome de ficheiro Olá ficheiro Olá pretende tooupload toohello localizador **caminho** valor recebido na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-196">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="36fed-197">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="36fed-197">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="36fed-198">.</span><span class="sxs-lookup"><span data-stu-id="36fed-198">.</span></span> <span data-ttu-id="36fed-199">.</span><span class="sxs-lookup"><span data-stu-id="36fed-199">.</span></span> <span data-ttu-id="36fed-200">.</span><span class="sxs-lookup"><span data-stu-id="36fed-200">.</span></span> 
> 
> 

<span data-ttu-id="36fed-201">Para obter mais informações sobre como trabalhar com blobs de armazenamento do Azure, consulte [API de REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="36fed-201">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="36fed-202">Atualizar Olá AssetFile</span><span class="sxs-lookup"><span data-stu-id="36fed-202">Update hello AssetFile</span></span>
<span data-ttu-id="36fed-203">Agora que carregar o ficheiro, atualize informações do Olá FileAsset tamanho (e outros).</span><span class="sxs-lookup"><span data-stu-id="36fed-203">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="36fed-204">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="36fed-204">For example:</span></span>

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


<span data-ttu-id="36fed-205">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-205">**HTTP Response**</span></span>

<span data-ttu-id="36fed-206">Se tiver êxito, seguinte Olá é devolvido: HTTP/1.1 204 não conteúdo</span><span class="sxs-lookup"><span data-stu-id="36fed-206">If successful, hello following is returned: HTTP/1.1 204 No Content</span></span>

### <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="36fed-207">Eliminar Olá localizador e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="36fed-207">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="36fed-208">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-208">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="36fed-209">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-209">**HTTP Response**</span></span>

<span data-ttu-id="36fed-210">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="36fed-210">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

<span data-ttu-id="36fed-211">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-211">**HTTP Request**</span></span>

    DELETE https://media.windows.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="36fed-212">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-212">**HTTP Response**</span></span>

<span data-ttu-id="36fed-213">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="36fed-213">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content 
    ...

## <span data-ttu-id="36fed-214"><a id="upload_in_bulk"></a>Carregar recursos em massa</span><span class="sxs-lookup"><span data-stu-id="36fed-214"><a id="upload_in_bulk"></a>Upload assets in bulk</span></span>
### <a name="create-hello-ingestmanifest"></a><span data-ttu-id="36fed-215">Criar Olá IngestManifest</span><span class="sxs-lookup"><span data-stu-id="36fed-215">Create hello IngestManifest</span></span>
<span data-ttu-id="36fed-216">Olá IngestManifest é um contentor para um conjunto de recursos, ficheiros de recurso e informações de estatística que podem ser utilizado o progresso de Olá toodetermine de ingestão relacionadas em massa para o conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-216">hello IngestManifest is a container for a set of assets, asset files, and statistic information that can be used toodetermine hello progress of bulk ingesting for hello set.</span></span>

<span data-ttu-id="36fed-217">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-217">**HTTP Request**</span></span>

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

### <a name="create-assets"></a><span data-ttu-id="36fed-218">Criar ativos</span><span class="sxs-lookup"><span data-stu-id="36fed-218">Create assets</span></span>
<span data-ttu-id="36fed-219">Antes de criar Olá IngestManifestAsset, terá de toocreate Olá recurso que será concluído com ingestão relacionadas em massa.</span><span class="sxs-lookup"><span data-stu-id="36fed-219">Before creating hello IngestManifestAsset, you need toocreate hello Asset that will be completed using bulk ingesting.</span></span> <span data-ttu-id="36fed-220">Um recurso é um contentor para vários tipos ou conjuntos de objetos nos Media Services, incluindo as vídeo, áudio, imagens, coleções de miniaturas, controla de texto e legendas ficheiros.</span><span class="sxs-lookup"><span data-stu-id="36fed-220">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="36fed-221">Na REST API Olá, criar um recurso necessita de enviar um tooMicrosoft de pedido de HTTP POST Media Services do Azure e colocar quaisquer informações de propriedade sobre o elemento no corpo do pedido de Olá. Neste exemplo, Olá recurso é criado utilizando a opção de StorageEncrption(1) Olá incluída no corpo do pedido Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-221">In hello REST API, creating an Asset requires sending a HTTP POST request tooMicrosoft Azure Media Services and placing any property information about your asset in hello request body.In this example, hello Asset is created using hello StorageEncrption(1) option included with hello request body.</span></span>

<span data-ttu-id="36fed-222">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-222">**HTTP Response**</span></span>

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

### <a name="create-hello-ingestmanifestassets"></a><span data-ttu-id="36fed-223">Criar Olá IngestManifestAssets</span><span class="sxs-lookup"><span data-stu-id="36fed-223">Create hello IngestManifestAssets</span></span>
<span data-ttu-id="36fed-224">IngestManifestAssets representam ativos dentro de um IngestManifest que são utilizados com ingestão relacionadas em massa.</span><span class="sxs-lookup"><span data-stu-id="36fed-224">IngestManifestAssets represent Assets within an IngestManifest that are used with bulk ingesting.</span></span> <span data-ttu-id="36fed-225">Olá basicamente o manifesto de toohello Olá recurso da hiperligação.</span><span class="sxs-lookup"><span data-stu-id="36fed-225">hello basically link hello asset toohello manifest.</span></span> <span data-ttu-id="36fed-226">Media Services do Azure internamente observa Olá carregamento de ficheiros com base no toohello de coleção associada IngestManifestFiles IngestManifestAsset.</span><span class="sxs-lookup"><span data-stu-id="36fed-226">Azure Media Services watches internally for hello file upload based on IngestManifestFiles collection associated toohello IngestManifestAsset.</span></span> <span data-ttu-id="36fed-227">Assim que estes ficheiros são carregados, asset Olá está concluída.</span><span class="sxs-lookup"><span data-stu-id="36fed-227">Once these files are uploaded, hello asset is completed.</span></span> <span data-ttu-id="36fed-228">Pode criar um novo IngestManifestAsset com um pedido POST de HTTP.</span><span class="sxs-lookup"><span data-stu-id="36fed-228">You can create a new IngestManifestAsset with a HTTP POST request.</span></span> <span data-ttu-id="36fed-229">No corpo do pedido de Olá, incluem Olá IngestManifest Id e Olá Id de recurso que Olá IngestManifestAsset deve ligar em conjunto para ingestão relacionadas em massa.</span><span class="sxs-lookup"><span data-stu-id="36fed-229">In hello request body, include hello IngestManifest Id and hello Asset Id that hello IngestManifestAsset should link together for bulk ingesting.</span></span>

<span data-ttu-id="36fed-230">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-230">**HTTP Response**</span></span>

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


### <a name="create-hello-ingestmanifestfiles-for-each-asset"></a><span data-ttu-id="36fed-231">Criar Olá IngestManifestFiles para cada recurso</span><span class="sxs-lookup"><span data-stu-id="36fed-231">Create hello IngestManifestFiles for each Asset</span></span>
<span data-ttu-id="36fed-232">Um IngestManifestFile representa um objeto de blob de vídeo ou áudio real que será carregado como parte da ingestão relacionadas em massa para um recurso.</span><span class="sxs-lookup"><span data-stu-id="36fed-232">An IngestManifestFile represents an actual video or audio blob object that will be uploaded as part of bulk ingesting for an asset.</span></span> <span data-ttu-id="36fed-233">Encriptação relacionadas com propriedades não são necessárias, a menos que o recurso de Olá está a utilizar uma opção de encriptação.</span><span class="sxs-lookup"><span data-stu-id="36fed-233">Encryption related properties are not required unless hello asset is using an encryption option.</span></span> <span data-ttu-id="36fed-234">exemplo de Olá utilizado nesta secção demonstra a criação de um IngestManifestFile que utiliza StorageEncryption para Olá recurso que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="36fed-234">hello example used in this section demonstrates creating an IngestManifestFile that uses StorageEncryption for hello Asset previously created.</span></span>

<span data-ttu-id="36fed-235">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-235">**HTTP Response**</span></span>

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

### <a name="upload-hello-files-tooblob-storage"></a><span data-ttu-id="36fed-236">Carregar ficheiros de Olá tooBlob armazenamento</span><span class="sxs-lookup"><span data-stu-id="36fed-236">Upload hello Files tooBlob Storage</span></span>
<span data-ttu-id="36fed-237">Pode utilizar qualquer aplicação de cliente de alta velocidade com capacidade de carregar Olá asset ficheiros toohello contentor de blob storage Uri fornecido pelo Olá propriedade BlobStorageUriForUpload Olá IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="36fed-237">You can use any high speed client application capable of uploading hello asset files toohello blob storage container Uri provided by hello BlobStorageUriForUpload property of hello IngestManifest.</span></span> <span data-ttu-id="36fed-238">É um serviço de carregamento de alta velocidade acentuadas [Aspera a pedido para a aplicação Azure](http://go.microsoft.com/fwlink/?LinkId=272001).</span><span class="sxs-lookup"><span data-stu-id="36fed-238">One notable high speed upload service is [Aspera On Demand for Azure Application](http://go.microsoft.com/fwlink/?LinkId=272001).</span></span>

### <a name="monitor-bulk-ingest-progress"></a><span data-ttu-id="36fed-239">Progresso de inserção em massa do monitor</span><span class="sxs-lookup"><span data-stu-id="36fed-239">Monitor Bulk Ingest Progress</span></span>
<span data-ttu-id="36fed-240">Pode monitorizar o progresso Olá em massa ingestão de operações para um IngestManifest relacionadas através de consultas de propriedade de estatísticas de Olá de Olá IngestManifest.</span><span class="sxs-lookup"><span data-stu-id="36fed-240">You can monitor hello progress of bulk ingesting operations for an IngestManifest by polling hello Statistics property of hello IngestManifest.</span></span> <span data-ttu-id="36fed-241">Se a propriedade é um tipo complexo, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span><span class="sxs-lookup"><span data-stu-id="36fed-241">That property is a complex type, [IngestManifestStatistics](https://docs.microsoft.com/rest/api/media/operations/ingestmanifeststatistics).</span></span> <span data-ttu-id="36fed-242">Olá toopoll propriedade estatísticas, submeter um pedido de HTTP GET transmitir Olá IngestManifest ID</span><span class="sxs-lookup"><span data-stu-id="36fed-242">toopoll hello Statistics property, submit a HTTP GET request passing hello IngestManifest Id.</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="36fed-243">Criar ContentKeys utilizada para encriptação</span><span class="sxs-lookup"><span data-stu-id="36fed-243">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="36fed-244">Se o seu elemento irá utilizar a encriptação, tem de criar Olá ContentKey toobe utilizada para encriptação antes de criar Olá ficheiros de recurso.</span><span class="sxs-lookup"><span data-stu-id="36fed-244">If your asset will use encryption, you must create hello ContentKey toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="36fed-245">Para a encriptação de armazenamento, hello propriedades seguintes devem ser incluídas no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-245">For storage encryption, hello following properties should be included in hello request body.</span></span>

| <span data-ttu-id="36fed-246">Propriedade de corpo do pedido</span><span class="sxs-lookup"><span data-stu-id="36fed-246">Request body property</span></span> | <span data-ttu-id="36fed-247">Descrição</span><span class="sxs-lookup"><span data-stu-id="36fed-247">Description</span></span> |
| --- | --- |
| <span data-ttu-id="36fed-248">Id</span><span class="sxs-lookup"><span data-stu-id="36fed-248">Id</span></span> |<span data-ttu-id="36fed-249">Olá ContentKey Id que geramos ourselves utilizando Olá seguir formatar, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="36fed-249">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span> |
| <span data-ttu-id="36fed-250">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="36fed-250">ContentKeyType</span></span> |<span data-ttu-id="36fed-251">Este é o tipo de chave de conteúdo de Olá como um valor inteiro para esta chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="36fed-251">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="36fed-252">Podemos transmitir o valor de Olá 1 para a encriptação de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="36fed-252">We pass hello value 1 for storage encryption.</span></span> |
| <span data-ttu-id="36fed-253">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="36fed-253">EncryptedContentKey</span></span> |<span data-ttu-id="36fed-254">Vamos criar um novo valor de chave conteúdo que é um valor de 256 bits (32 byte).</span><span class="sxs-lookup"><span data-stu-id="36fed-254">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="36fed-255">chave de Olá é encriptada utilizando o certificado x. 509 de encriptação de armazenamento de Olá que obtemos Media Services do Microsoft Azure ao executar um pedido HTTP GET Olá GetProtectionKeyId e GetProtectionKey métodos.</span><span class="sxs-lookup"><span data-stu-id="36fed-255">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> |
| <span data-ttu-id="36fed-256">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="36fed-256">ProtectionKeyId</span></span> |<span data-ttu-id="36fed-257">Isto é Olá id de chave de proteção para o certificado x. 509 de encriptação de armazenamento de Olá que foi utilizado tooencrypt nosso chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="36fed-257">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span> |
| <span data-ttu-id="36fed-258">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="36fed-258">ProtectionKeyType</span></span> |<span data-ttu-id="36fed-259">Este é o tipo de encriptação de Olá para a chave de proteção de Olá que estava a chave de conteúdo de Olá tooencrypt utilizados.</span><span class="sxs-lookup"><span data-stu-id="36fed-259">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="36fed-260">Este valor é StorageEncryption(1) para o nosso exemplo.</span><span class="sxs-lookup"><span data-stu-id="36fed-260">This value is StorageEncryption(1) for our example.</span></span> |
| <span data-ttu-id="36fed-261">Soma de verificação</span><span class="sxs-lookup"><span data-stu-id="36fed-261">Checksum</span></span> |<span data-ttu-id="36fed-262">Olá MD5 calculada soma de verificação para a chave de conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-262">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="36fed-263">Esta é calculada ao encriptar o conteúdo de Olá Id com a chave de conteúdo de Olá.</span><span class="sxs-lookup"><span data-stu-id="36fed-263">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="36fed-264">código de exemplo de Olá demonstra como toocalculate Olá soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="36fed-264">hello example code demonstrates how toocalculate hello checksum.</span></span> |

<span data-ttu-id="36fed-265">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-265">**HTTP Response**</span></span>

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

### <a name="link-hello-contentkey-toohello-asset"></a><span data-ttu-id="36fed-266">Olá ContentKey toohello recurso de ligação</span><span class="sxs-lookup"><span data-stu-id="36fed-266">Link hello ContentKey toohello Asset</span></span>
<span data-ttu-id="36fed-267">Olá ContentKey é tooone associado ou mais recursos ao enviar um pedido POST de HTTP.</span><span class="sxs-lookup"><span data-stu-id="36fed-267">hello ContentKey is associated tooone or more assets by sending a HTTP POST request.</span></span> <span data-ttu-id="36fed-268">Olá pedido seguinte é um exemplo toolink Olá exemplo ContentKey toohello exemplo recurso por ID.</span><span class="sxs-lookup"><span data-stu-id="36fed-268">hello following request is an example toolink hello example ContentKey toohello example asset by Id.</span></span>

<span data-ttu-id="36fed-269">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-269">**HTTP Response**</span></span>

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

<span data-ttu-id="36fed-270">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="36fed-270">**HTTP Response**</span></span>

    GET https://media.windows.net/API/IngestManifests('nb:mid:UUID:5c77f186-414f-8b48-8231-17f9264e2048') HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=070500D0-F35C-4A5A-9249-485BBF4EC70B&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1334275521&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=GxdBb%2fmEyN7iHdNxbawawHRftLhPFFqxX1JZckuv3hY%3d
    Host: media.windows.net

## <a name="next-steps"></a><span data-ttu-id="36fed-271">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="36fed-271">Next steps</span></span>

<span data-ttu-id="36fed-272">Agora, pode codificar os elementos que carregar.</span><span class="sxs-lookup"><span data-stu-id="36fed-272">You can now encode your uploaded assets.</span></span> <span data-ttu-id="36fed-273">Para obter mais informações, veja [Codificar elementos](media-services-portal-encode.md)</span><span class="sxs-lookup"><span data-stu-id="36fed-273">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="36fed-274">Também pode utilizar as funções do Azure tootrigger uma tarefa de codificação baseada num ficheiro chegar no contentor de Olá configurado.</span><span class="sxs-lookup"><span data-stu-id="36fed-274">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="36fed-275">Para obter mais informações, veja [este exemplo](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="36fed-275">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="36fed-276">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="36fed-276">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="36fed-277">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="36fed-277">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[How tooGet a Media Processor]: media-services-get-media-processor.md

