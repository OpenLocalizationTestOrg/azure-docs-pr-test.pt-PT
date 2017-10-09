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
# <a name="get-started-with-delivering-content-on-demand-using-rest"></a><span data-ttu-id="cd2ee-103">Introdução à entrega de conteúdos a pedido utilizando REST</span><span class="sxs-lookup"><span data-stu-id="cd2ee-103">Get started with delivering content on demand using REST</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="cd2ee-104">Este guia de introdução orienta-o pelos passos Olá implementar uma aplicação de entrega de conteúdos de vídeo a pedido (VoD) utilizando as APIs REST de serviços de suporte de dados do Azure (AMS).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-104">This quickstart walks you through hello steps of implementing a Video-on-Demand (VoD) content delivery application using Azure Media Services (AMS) REST APIs.</span></span>

<span data-ttu-id="cd2ee-105">tutorial de Olá apresenta o fluxo de trabalho Olá básico dos Media Services e objetos de programação mais comuns Olá e as tarefas necessárias para o desenvolvimento de Media Services.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-105">hello tutorial introduces hello basic Media Services workflow and hello most common programming objects and tasks required for Media Services development.</span></span> <span data-ttu-id="cd2ee-106">Olá após conclusão do tutorial Olá, terá de ser capaz de toostream ou transferir progressivamente um ficheiro de suporte de dados de exemplo que carregou, codificou e transferiu.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-106">At hello completion of hello tutorial, you will be able toostream or progressively download a sample media file that you uploaded, encoded, and downloaded.</span></span>

<span data-ttu-id="cd2ee-107">Olá imagem seguinte mostra alguns dos objetos de Olá normalmente utilizada quando desenvolver aplicações VoD contra um modelo de suporte de dados serviços OData Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-107">hello following image shows some of hello most commonly used objects when developing VoD applications against hello Media Services OData model.</span></span>

<span data-ttu-id="cd2ee-108">Clique em Olá imagem tooview-total de tamanho.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-108">Click hello image tooview it full size.</span></span>  

<a href="./media/media-services-rest-get-started/media-services-overview-object-model.png" target="_blank"><img src="./media/media-services-rest-get-started/media-services-overview-object-model-small.png"></a> 

## <a name="prerequisites"></a><span data-ttu-id="cd2ee-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cd2ee-109">Prerequisites</span></span>
<span data-ttu-id="cd2ee-110">Olá pré-requisitos seguintes são necessário toostart desenvolver com os serviços de suporte de dados com REST APIs.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-110">hello following prerequisites are required toostart developing with Media Services with REST APIs.</span></span>

* <span data-ttu-id="cd2ee-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-111">An Azure account.</span></span> <span data-ttu-id="cd2ee-112">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cd2ee-113">Uma conta dos Media Services.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-113">A Media Services account.</span></span> <span data-ttu-id="cd2ee-114">toocreate uma conta de Media Services, consulte [como tooCreate uma conta de Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-114">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="cd2ee-115">Compreender como toodevelop com a API de REST dos serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-115">Understanding of how toodevelop with Media Services REST API.</span></span> <span data-ttu-id="cd2ee-116">Para obter mais informações, consulte [descrição geral da API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-116">For more information, see [Media Services REST API overview](media-services-rest-how-to-use.md).</span></span>
* <span data-ttu-id="cd2ee-117">Uma aplicação da sua preferência que pode enviar pedidos e respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-117">An application of your choice that can send HTTP requests and responses.</span></span> <span data-ttu-id="cd2ee-118">Este tutorial utiliza [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-118">This tutorial uses [Fiddler](http://www.telerik.com/download/fiddler).</span></span>

<span data-ttu-id="cd2ee-119">Olá seguintes tarefas é apresentada neste guia de introdução.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-119">hello following tasks are shown in this quickstart.</span></span>

1. <span data-ttu-id="cd2ee-120">Inicie o ponto final (utilizando o portal do Azure de Olá) de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-120">Start streaming endpoint (using hello Azure portal).</span></span>
2. <span data-ttu-id="cd2ee-121">Ligar a conta de Media Services do toohello com a REST API.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-121">Connect toohello Media Services account with REST API.</span></span>
3. <span data-ttu-id="cd2ee-122">Criar um novo elemento e carregar um ficheiro de vídeo com a REST API.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-122">Create a new asset and upload a video file with REST API.</span></span>
4. <span data-ttu-id="cd2ee-123">Codificar o ficheiro de origem Olá para um conjunto de ficheiros MP4 de velocidade de transmissão adaptável com a REST API.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-123">Encode hello source file into a set of adaptive bitrate MP4 files with REST API.</span></span>
5. <span data-ttu-id="cd2ee-124">Publica asset Olá e get de transmissão em fluxo e transferência progressiva URLs REST API.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-124">Publish hello asset and get streaming and progressive download URLs with REST API.</span></span>
6. <span data-ttu-id="cd2ee-125">Reproduzir os conteúdos.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-125">Play your content.</span></span>

>[!NOTE]
><span data-ttu-id="cd2ee-126">Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-126">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="cd2ee-127">Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-127">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="cd2ee-128">Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-128">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="cd2ee-129">Para obter detalhes sobre as entidades de REST do AMS utilizados neste tópico, consulte [referência da API REST do Azure Media Services](/rest/api/media/services/azure-media-services-rest-api-reference).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-129">For details about AMS REST entities used in this topic, see [Azure Media Services REST API Reference](/rest/api/media/services/azure-media-services-rest-api-reference).</span></span> <span data-ttu-id="cd2ee-130">Além disso, consulte [conceitos de Media Services do Azure](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-130">Also, see [Azure Media Services concepts](media-services-concepts.md).</span></span>

>[!NOTE]
><span data-ttu-id="cd2ee-131">Ao aceder a entidades nos Media Services, tem de definir campos de cabeçalho específicos e os valores no seus pedidos HTTP.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-131">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="cd2ee-132">Para obter mais informações, consulte [programa de configuração para o desenvolvimento de API de REST de serviços de suporte de dados](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-132">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="start-streaming-endpoints-using-hello-azure-portal"></a><span data-ttu-id="cd2ee-133">Começar a transmissão em fluxo pontos finais utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cd2ee-133">Start streaming endpoints using hello Azure portal</span></span>

<span data-ttu-id="cd2ee-134">Ao trabalhar com uma das situações mais comuns Olá é a entrega de vídeo através de velocidade de transmissão adaptável em fluxo de Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-134">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="cd2ee-135">Os Media Services fornecem um empacotamento dinâmico, permitindo-lhe toodeliver a conteúdo MP4 codificado suportados pelo Media Services (MPEG DASH, HLS, transmissão em fluxo uniforme) just-in-time, sem ter toostore previamente empacotada de formatos de transmissão em fluxo de velocidade de transmissão adaptável versões de cada um destes formatos de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-135">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="cd2ee-136">Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-136">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="cd2ee-137">toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-137">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="cd2ee-138">toostart Olá ponto final de transmissão em fluxo, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-138">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="cd2ee-139">Inicie sessão no Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-139">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cd2ee-140">Na janela de definições de Olá, clique em pontos finais de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-140">In hello Settings window, click Streaming endpoints.</span></span>
3. <span data-ttu-id="cd2ee-141">Clique em predefinido Olá ponto final de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-141">Click hello default streaming endpoint.</span></span>

    <span data-ttu-id="cd2ee-142">Surge a janela de detalhes de ponto final de transmissão em fluxo de predefinido Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-142">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="cd2ee-143">Clique Olá ícone de início.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-143">Click hello Start icon.</span></span>
5. <span data-ttu-id="cd2ee-144">Clique em Olá guardar botão toosave as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-144">Click hello Save button toosave your changes.</span></span>

## <span data-ttu-id="cd2ee-145"><a id="connect"></a>Ligar a conta de Media Services toohello com a REST API</span><span class="sxs-lookup"><span data-stu-id="cd2ee-145"><a id="connect"></a>Connect toohello Media Services account with REST API</span></span>

<span data-ttu-id="cd2ee-146">Para obter informações sobre como tooconnect toohello AMS API, consulte o artigo [Olá de acesso API de serviços de suporte de dados do Azure com a autenticação do Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-146">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="cd2ee-147">Depois de ligar com êxito toohttps://media.windows.net, receberá um redirecionamento 301 especificando noutro URI de serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-147">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="cd2ee-148">É necessário efetuar chamadas subsequentes toohello novo URI.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-148">You must make subsequent calls toohello new URI.</span></span>

<span data-ttu-id="cd2ee-149">Por exemplo, se depois tentar tooconnect, obteve seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-149">For example, if after trying tooconnect, you got hello following:</span></span>

    HTTP/1.1 301 Moved Permanently
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/

<span data-ttu-id="cd2ee-150">Deve publicar o seu subsequentes API chamadas toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-150">You should post your subsequent API calls toohttps://wamsbayclus001rest-hs.cloudapp.net/api/.</span></span>

## <span data-ttu-id="cd2ee-151"><a id="upload"></a>Criar um novo elemento e carregar um ficheiro de vídeo com a REST API</span><span class="sxs-lookup"><span data-stu-id="cd2ee-151"><a id="upload"></a>Create a new asset and upload a video file with REST API</span></span>

<span data-ttu-id="cd2ee-152">Nos Serviços de Multimédia, os ficheiros digitais são carregados para um elemento.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-152">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="cd2ee-153">Olá **Asset** entidade pode conter vídeo, áudio, imagens, coleções de miniaturas, texto controla e legendas ficheiros (e Olá metadados sobre estes ficheiros.)  Depois de ficheiros de Olá são carregados para o elemento de Olá, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-153">hello **Asset** entity can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.)  Once hello files are uploaded into hello asset, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="cd2ee-154">Um dos valores de Olá que tiver tooprovide ao criar um recurso é opções de criação do elemento.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-154">One of hello values that you have tooprovide when creating an asset is asset creation options.</span></span> <span data-ttu-id="cd2ee-155">Olá **opções** propriedade é um valor de enumeração que descreve as opções de encriptação de Olá um recurso que pode ser criado com.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-155">hello **Options** property is an enumeration value that describes hello encryption options that an Asset can be created with.</span></span> <span data-ttu-id="cd2ee-156">Um valor válido é de um dos valores de Olá da lista de Olá abaixo, não uma combinação de valores nesta lista:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-156">A valid value is one of hello values from hello list below, not a combination of values from this list:</span></span>

* <span data-ttu-id="cd2ee-157">**Nenhum** = **0** -é utilizada qualquer encriptação.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-157">**None** = **0** - No encryption is used.</span></span> <span data-ttu-id="cd2ee-158">Ao utilizar esta opção não está protegido o conteúdo em trânsito ou inativo no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-158">When using this option your content is not protected in transit or at rest in storage.</span></span>
    <span data-ttu-id="cd2ee-159">Se planear toodeliver um MP4 utilizando transferência progressiva, utilize esta opção.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-159">If you plan toodeliver an MP4 using progressive download, use this option.</span></span>
* <span data-ttu-id="cd2ee-160">**StorageEncrypted** = **1** - encripta o seu conteúdo transparente localmente utilizando AES 256 bits encriptação e, em seguida, esta carrega-tooAzure armazenamento onde é armazenado encriptado em pausa.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-160">**StorageEncrypted** = **1** - Encrypts your clear content locally using AES-256 bit encryption and then uploads it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="cd2ee-161">Os elementos protegidos com encriptação de armazenamento são automaticamente não encriptados e colocados num tooencoding anterior de sistema de ficheiros encriptados e opcionalmente encriptado novamente toouploading anterior novamente como um novo elemento de saída.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-161">Assets protected with Storage Encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="cd2ee-162">Olá principal motivo para encriptação de armazenamento é quando quiser toosecure os ficheiros de suporte de dados de entrada de alta qualidade com uma encriptação forte Inativos no disco.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-162">hello primary use case for Storage Encryption is when you want toosecure your high-quality input media files with strong encryption at rest on disk.</span></span>
* <span data-ttu-id="cd2ee-163">**CommonEncryptionProtected** = **2** -Utilize esta opção se estiver a carregar conteúdo que já foi encriptado e protegido com encriptação comum ou PlayReady DRM (por exemplo, transmissão em fluxo uniforme protegida com PlayReady DRM).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-163">**CommonEncryptionProtected** = **2** - Use this option if you are uploading content that has already been encrypted and protected with Common Encryption or PlayReady DRM (for example, Smooth Streaming protected with PlayReady DRM).</span></span>
* <span data-ttu-id="cd2ee-164">**EnvelopeEncryptionProtected** = **4** – Utilize esta opção se estiver a carregar HLS encriptado com AES.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-164">**EnvelopeEncryptionProtected** = **4** – Use this option if you are uploading HLS encrypted with AES.</span></span> <span data-ttu-id="cd2ee-165">ficheiros de Olá tem de ter sido codificados e encriptados pelo Gestor de transformação.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-165">hello files must have been encoded and encrypted by Transform Manager.</span></span>

### <a name="create-an-asset"></a><span data-ttu-id="cd2ee-166">Criar um recurso</span><span class="sxs-lookup"><span data-stu-id="cd2ee-166">Create an asset</span></span>
<span data-ttu-id="cd2ee-167">Um recurso é um contentor para vários tipos ou conjuntos de objetos nos Media Services, incluindo as vídeo, áudio, imagens, coleções de miniaturas, controla de texto e legendas ficheiros.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-167">An asset is a container for multiple types or sets of objects in Media Services, including video, audio, images, thumbnail collections, text tracks, and closed caption files.</span></span> <span data-ttu-id="cd2ee-168">No Olá API REST, criar um recurso necessita de enviar a mensagem de pedido tooMedia serviços e colocar quaisquer informações de propriedade sobre o elemento no corpo do pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-168">In hello REST API, creating an Asset requires sending POST request tooMedia Services and placing any property information about your asset in hello request body.</span></span>

<span data-ttu-id="cd2ee-169">Olá seguinte exemplo mostra como toocreate um recurso.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-169">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="cd2ee-170">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-170">**HTTP Request**</span></span>

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


<span data-ttu-id="cd2ee-171">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-171">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-172">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-172">If successful, hello following is returned:</span></span>

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

### <a name="create-an-assetfile"></a><span data-ttu-id="cd2ee-173">Criar um AssetFile</span><span class="sxs-lookup"><span data-stu-id="cd2ee-173">Create an AssetFile</span></span>
<span data-ttu-id="cd2ee-174">Olá [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entidade representa um ficheiro de vídeo ou áudio que é armazenado num contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-174">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="cd2ee-175">Um ficheiro de recurso é sempre associado a um recurso e um recurso pode conter um ou vários AssetFiles.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-175">An asset file is always associated with an asset, and an asset may contain one or many AssetFiles.</span></span> <span data-ttu-id="cd2ee-176">tarefa de codificador de serviços de multimédia de Olá falhar se um objeto de ficheiro de recurso não está associado um ficheiro digital num contentor de blob.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-176">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="cd2ee-177">Depois de carregar o ficheiro de suporte de dados digitais num contentor de blob, pode utilizar Olá **intercalar** HTTP pedido tooupdate Olá AssetFile com informações sobre o ficheiro de suporte de dados (conforme mostrado posteriormente tópico Olá).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-177">After you upload your digital media file into a blob container, you use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (as shown later in hello topic).</span></span>

<span data-ttu-id="cd2ee-178">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-178">**HTTP Request**</span></span>

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


<span data-ttu-id="cd2ee-179">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-179">**HTTP Response**</span></span>

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


### <a name="creating-hello-accesspolicy-with-write-permission"></a><span data-ttu-id="cd2ee-180">Criar Olá AccessPolicy com permissão de escrita</span><span class="sxs-lookup"><span data-stu-id="cd2ee-180">Creating hello AccessPolicy with write permission</span></span>
<span data-ttu-id="cd2ee-181">Antes de carregar ficheiros para o armazenamento de BLOBs, defina acesso Olá direitos de política para escrever tooan ativo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-181">Before uploading any files into blob storage, set hello access policy rights for writing tooan asset.</span></span> <span data-ttu-id="cd2ee-182">Definir toodo que, após um toohello de pedido HTTP AccessPolicies entidade.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-182">toodo that, POST an HTTP request toohello AccessPolicies entity set.</span></span> <span data-ttu-id="cd2ee-183">Definir um valor de DurationInMinutes após a criação ou receber uma mensagem de erro de servidor interno 500 na resposta.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-183">Define a DurationInMinutes value upon creation or you receive a 500 Internal Server error message back in response.</span></span> <span data-ttu-id="cd2ee-184">Para obter mais informações sobre AccessPolicies, consulte [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-184">For more information on AccessPolicies, see [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy).</span></span>

<span data-ttu-id="cd2ee-185">Olá seguinte exemplo mostra como toocreate um AccessPolicy:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-185">hello following example shows how toocreate an AccessPolicy:</span></span>

<span data-ttu-id="cd2ee-186">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-186">**HTTP Request**</span></span>

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

<span data-ttu-id="cd2ee-187">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-187">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-188">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-188">If successful, hello following response is returned:</span></span>

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

### <a name="get-hello-upload-url"></a><span data-ttu-id="cd2ee-189">Obter Olá carregar URL</span><span class="sxs-lookup"><span data-stu-id="cd2ee-189">Get hello Upload URL</span></span>

<span data-ttu-id="cd2ee-190">tooreceive Olá URL de carregamento real, crie um localizador SAS.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-190">tooreceive hello actual upload URL, create a SAS Locator.</span></span> <span data-ttu-id="cd2ee-191">Localizadores definem a hora de início Olá e o tipo de ponto final de ligação para os clientes que pretendem ficheiros tooaccess um recurso.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-191">Locators define hello start time and type of connection endpoint for clients that want tooaccess Files in an Asset.</span></span> <span data-ttu-id="cd2ee-192">Pode criar várias entidades de localizador para um determinado AccessPolicy e Asset par toohandle diferentes cliente pedidos e as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-192">You can create multiple Locator entities for a given AccessPolicy and Asset pair toohandle different client requests and needs.</span></span> <span data-ttu-id="cd2ee-193">Cada um destes localizadores utiliza o valor de StartTime Olá plus valor DurationInMinutes Olá Olá AccessPolicy toodetermine Olá o comprimento de tempo que pode ser utilizado um URL.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-193">Each of these Locators uses hello StartTime value plus hello DurationInMinutes value of hello AccessPolicy toodetermine hello length of time a URL can be used.</span></span> <span data-ttu-id="cd2ee-194">Para obter mais informações, consulte [localizador](https://docs.microsoft.com/rest/api/media/operations/locator).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-194">For more information, see [Locator](https://docs.microsoft.com/rest/api/media/operations/locator).</span></span>

<span data-ttu-id="cd2ee-195">Um URL SAS tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-195">A SAS URL has hello following format:</span></span>

    {https://myaccount.blob.core.windows.net}/{asset name}/{video file name}?{SAS signature}

<span data-ttu-id="cd2ee-196">São aplicáveis algumas considerações:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-196">Some considerations apply:</span></span>

* <span data-ttu-id="cd2ee-197">Não pode ter mais de cinco localizadores exclusivos associados um determinado elemento de uma só vez.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-197">You cannot have more than five unique Locators associated with a given Asset at one time.</span></span> <span data-ttu-id="cd2ee-198">Para obter mais informações, consulte localizador.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-198">For more information, see Locator.</span></span>
* <span data-ttu-id="cd2ee-199">Se precisar de tooupload os ficheiros imediatamente, deve definir os minutos de toofive de valor de StartTime antes Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-199">If you need tooupload your files immediately, you should set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="cd2ee-200">Isto acontece porque poderá haver relógio dissimetrias entre o computador cliente e os Media Services.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-200">This is because there may be clock skew between your client machine and Media Services.</span></span> <span data-ttu-id="cd2ee-201">Além disso, o valor de StartTime tem de constar Olá seguir o formato DateTime: aaaa-MM-aaaathh (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="cd2ee-201">Also, your StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>    
* <span data-ttu-id="cd2ee-202">Poderá existir um segundo 30-40 atrasar depois de criar um localizador toowhen está disponível para utilização.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-202">There may be a 30-40 second delay after a Locator is created toowhen it is available for use.</span></span> <span data-ttu-id="cd2ee-203">Aplica-se este problema tooboth SAS URL e localizadores de origem.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-203">This issue applies tooboth SAS URL and Origin Locators.</span></span>

<span data-ttu-id="cd2ee-204">Para obter mais informações sobre SAS localizadores consulte [isto](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogue.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-204">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="cd2ee-205">Olá seguinte exemplo mostra como toocreate um localizador de URL SAS, tal como definido por Olá propriedade de tipo no corpo do pedido de Olá ("1" para um localizador SAS) e "2" para um localizador de origem no pedido.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-205">hello following example shows how toocreate a SAS URL Locator, as defined by hello Type property in hello request body ("1" for a SAS locator and "2" for an On-Demand origin locator).</span></span> <span data-ttu-id="cd2ee-206">Olá **caminho** propriedade devolvida contém um URL de Olá que tem de utilizar tooupload o ficheiro.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-206">hello **Path** property returned contains hello URL that you must use tooupload your file.</span></span>

<span data-ttu-id="cd2ee-207">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-207">**HTTP Request**</span></span>

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


<span data-ttu-id="cd2ee-208">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-208">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-209">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-209">If successful, hello following response is returned:</span></span>

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

### <a name="upload-a-file-into-a-blob-storage-container"></a><span data-ttu-id="cd2ee-210">Carregue um ficheiro para um contentor de blob storage</span><span class="sxs-lookup"><span data-stu-id="cd2ee-210">Upload a file into a blob storage container</span></span>
<span data-ttu-id="cd2ee-211">Assim que tiver Olá AccessPolicy e o conjunto de localizador, real do ficheiro Olá é carregado tooan contentor de armazenamento de Blobs do Azure utilizando Olá APIs de REST de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-211">Once you have hello AccessPolicy and Locator set, hello actual file is uploaded tooan Azure blob storage container using hello Azure Storage REST APIs.</span></span> <span data-ttu-id="cd2ee-212">Tem de carregar ficheiros Olá como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-212">You must upload hello files as block blobs.</span></span> <span data-ttu-id="cd2ee-213">Os blobs de página não são suportados pelos Media Services do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-213">Page blobs are not supported by Azure Media Services.</span></span>  

> [!NOTE]
> <span data-ttu-id="cd2ee-214">Tem de adicionar o nome de ficheiro Olá ficheiro Olá pretende tooupload toohello localizador **caminho** valor recebido na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-214">You must add hello file name for hello file you want tooupload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="cd2ee-215">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="cd2ee-215">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="cd2ee-216">.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-216">.</span></span> <span data-ttu-id="cd2ee-217">.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-217">.</span></span> <span data-ttu-id="cd2ee-218">.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-218">.</span></span>
>
>

<span data-ttu-id="cd2ee-219">Para obter mais informações sobre como trabalhar com blobs de armazenamento do Azure, consulte [API de REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-219">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

### <a name="update-hello-assetfile"></a><span data-ttu-id="cd2ee-220">Atualizar Olá AssetFile</span><span class="sxs-lookup"><span data-stu-id="cd2ee-220">Update hello AssetFile</span></span>
<span data-ttu-id="cd2ee-221">Agora que carregar o ficheiro, atualize informações do Olá FileAsset tamanho (e outros).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-221">Now that you've uploaded your file, update hello FileAsset size (and other) information.</span></span> <span data-ttu-id="cd2ee-222">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-222">For example:</span></span>

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


<span data-ttu-id="cd2ee-223">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-223">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-224">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-224">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <a name="delete-hello-locator-and-accesspolicy"></a><span data-ttu-id="cd2ee-225">Eliminar Olá localizador e AccessPolicy</span><span class="sxs-lookup"><span data-stu-id="cd2ee-225">Delete hello Locator and AccessPolicy</span></span>
<span data-ttu-id="cd2ee-226">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-226">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/Locators('nb%3Alid%3AUUID%3Aaf57bdd8-6751-4e84-b403-f3c140444b54') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="cd2ee-227">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-227">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-228">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-228">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

<span data-ttu-id="cd2ee-229">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-229">**HTTP Request**</span></span>

    DELETE https://wamsbayclus001rest-hs.cloudapp.net/api/AccessPolicies('nb%3Apid%3AUUID%3Abe0ac48d-af7d-4877-9d60-1805d68bffae') HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421662918&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=utmoXXbm9Q7j4tW1yJuMVA3egRiQy5FPygwadkmPeaY%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net

<span data-ttu-id="cd2ee-230">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-230">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-231">Se tiver êxito, é devolvido o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-231">If successful, hello following is returned:</span></span>

    HTTP/1.1 204 No Content
    ...

## <span data-ttu-id="cd2ee-232"><a id="encode"></a>Codificar o ficheiro de origem Olá para um conjunto de ficheiros MP4 de velocidade de transmissão adaptável</span><span class="sxs-lookup"><span data-stu-id="cd2ee-232"><a id="encode"></a>Encode hello source file into a set of adaptive bitrate MP4 files</span></span>

<span data-ttu-id="cd2ee-233">Antes após ingestão relacionadas que ativos para os serviços de suporte de dados, suportes de dados podem ser codificados, transmuxed, como e assim sucessivamente, mesmo ser entregue tooclients.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-233">After ingesting Assets into Media Services, media can be encoded, transmuxed, watermarked, and so on, before it is delivered tooclients.</span></span> <span data-ttu-id="cd2ee-234">Estas atividades são agendadas e executar várias em segundo plano função instâncias tooensure elevado desempenho e disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-234">These activities are scheduled and run against multiple background role instances tooensure high performance and availability.</span></span> <span data-ttu-id="cd2ee-235">Estas atividades são denominadas tarefas e cada trabalho é composto por tarefas atómica que Olá trabalho real no ficheiro de elemento Olá (para obter mais informações, consulte [tarefa](/rest/api/media/services/job), [tarefas](/rest/api/media/services/task) descrições).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-235">These activities are called Jobs and each Job is composed of atomic Tasks that do hello actual work on hello Asset file (for more information, see [Job](/rest/api/media/services/job), [Task](/rest/api/media/services/task) descriptions).</span></span>

<span data-ttu-id="cd2ee-236">Conforme foi mencionado anteriormente, quando trabalhar com Media Services do Azure uma das situações mais comuns de Olá é a distribuição de velocidade de transmissão adaptável tooyour clientes de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-236">As was mentioned earlier, when working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="cd2ee-237">Os Media Services podem empacotar dinamicamente um conjunto de ficheiros MP4 de velocidade de transmissão adaptável dos seguintes formatos de Olá: HTTP Live Streaming (HLS), transmissão em fluxo uniforme, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-237">Media Services can dynamically package a set of adaptive bitrate MP4 files into one of hello following formats: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span>

<span data-ttu-id="cd2ee-238">Olá, secção a seguir mostra como toocreate uma tarefa que contém uma codificação de tarefas.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-238">hello following section shows how toocreate a job that contains one encoding task.</span></span> <span data-ttu-id="cd2ee-239">Olá tarefas Especifica tootranscode Olá mezanino ficheiro para um conjunto de MP4s de velocidade de transmissão adaptável utilizando **codificador de multimédia Standard**.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-239">hello task specifies tootranscode hello mezzanine file into a set of adaptive bitrate MP4s using **Media Encoder Standard**.</span></span> <span data-ttu-id="cd2ee-240">secção de Olá também mostra como toomonitor Olá progresso de processamento da tarefa.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-240">hello section also shows how toomonitor hello job processing progress.</span></span> <span data-ttu-id="cd2ee-241">Quando a tarefa de Olá estiver concluída, seria capaz de toocreate localizadores que são necessários tooget acesso tooyour ativos.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-241">When hello job is complete, you would be able toocreate locators that are needed tooget access tooyour assets.</span></span>

### <a name="get-a-media-processor"></a><span data-ttu-id="cd2ee-242">Obter um processador de multimédia</span><span class="sxs-lookup"><span data-stu-id="cd2ee-242">Get a media processor</span></span>
<span data-ttu-id="cd2ee-243">Nos Media Services, um processador de multimédia é um componente que processa uma tarefa de processamento específico, tal como a codificação, a conversão do formato, encriptação ou desencriptar os conteúdos de multimédia.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-243">In Media Services, a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="cd2ee-244">Para Olá codificação tarefas mostradas neste tutorial, iremos toouse Olá codificador de multimédia Standard.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-244">For hello encoding task shown in this tutorial, we are going toouse hello Media Encoder Standard.</span></span>

<span data-ttu-id="cd2ee-245">Olá id do codificador de código, pedidos Olá seguinte.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-245">hello following code requests hello encoder's id.</span></span>

<span data-ttu-id="cd2ee-246">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-246">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=f7f09258-6753-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="cd2ee-247">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-247">**HTTP Response**</span></span>

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

### <a name="create-a-job"></a><span data-ttu-id="cd2ee-248">Criar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="cd2ee-248">Create a job</span></span>
<span data-ttu-id="cd2ee-249">Cada tarefa pode ter um ou mais tarefas, dependendo do tipo de Olá do processamento de que pretendem tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-249">Each Job can have one or more Tasks depending on hello type of processing that you want tooaccomplish.</span></span> <span data-ttu-id="cd2ee-250">Através da REST API Olá, pode criar as tarefas e as respetivas tarefas relacionadas em uma de duas formas: tarefas podem ser definidos inline através da propriedade de navegação de tarefas Olá entidades de tarefa ou através do processamento em lote OData.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-250">Through hello REST API, you can create Jobs and their related Tasks in one of two ways: Tasks can be defined inline through hello Tasks navigation property on Job entities, or through OData batch processing.</span></span> <span data-ttu-id="cd2ee-251">Olá SDK de Media Services utiliza o processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-251">hello Media Services SDK uses batch processing.</span></span> <span data-ttu-id="cd2ee-252">No entanto, para legibilidade de Olá dos exemplos de código Olá neste tópico, as tarefas são definidos inline.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-252">However, for hello readability of hello code examples in this topic, tasks are defined inline.</span></span> <span data-ttu-id="cd2ee-253">Para obter informações sobre o processamento em lote, consulte [Open Data Protocol (OData) Batch processamento](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-253">For information on batch processing, see [Open Data Protocol (OData) Batch Processing](http://www.odata.org/documentation/odata-version-3-0/batch-processing/).</span></span>

<span data-ttu-id="cd2ee-254">Olá seguinte exemplo mostra como toocreate e publique uma tarefa com uma tarefa definida tooencode um vídeo numa resolução específico e qualidade.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-254">hello following example shows you how toocreate and post a Job with one Task set tooencode a video at a specific resolution and quality.</span></span> <span data-ttu-id="cd2ee-255">Olá seguinte secção de documentação contém a lista de Olá de todos os Olá [tarefas predefinições](http://msdn.microsoft.com/library/mt269960) suportada pelo processador de codificador de multimédia Standard Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-255">hello following documentation section contains hello list of all hello [task presets](http://msdn.microsoft.com/library/mt269960) supported by hello Media Encoder Standard processor.</span></span>  

<span data-ttu-id="cd2ee-256">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-256">**HTTP Request**</span></span>

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

<span data-ttu-id="cd2ee-257">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-257">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-258">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-258">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="cd2ee-259">Existem alguns pontos importantes toonote qualquer pedido de tarefa:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-259">There are a few important things toonote in any Job request:</span></span>

* <span data-ttu-id="cd2ee-260">Propriedades de TaskBody tem de utilizar literal XML toodefine Olá diversas entrada ou de recursos de saída que são utilizados pelo Olá tarefas.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-260">TaskBody properties MUST use literal XML toodefine hello number of input, or output assets that are used by hello Task.</span></span> <span data-ttu-id="cd2ee-261">tópico de tarefa Olá contém Olá definição de esquema XML para Olá XML.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-261">hello Task topic contains hello XML Schema Definition for hello XML.</span></span>
* <span data-ttu-id="cd2ee-262">O valor na definição de TaskBody Olá, para cada interna <inputAsset> e <outputAsset> tem de ser definido como JobInputAsset(value) ou JobOutputAsset(value).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-262">In hello TaskBody definition, each inner value for <inputAsset> and <outputAsset> must be set as JobInputAsset(value) or JobOutputAsset(value).</span></span>
* <span data-ttu-id="cd2ee-263">Uma tarefa pode ter vários recursos de saída.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-263">A task can have multiple output assets.</span></span> <span data-ttu-id="cd2ee-264">Um JobOutputAsset(x) só pode ser utilizado uma vez como resultado de uma tarefa numa tarefa.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-264">One JobOutputAsset(x) can only be used once as an output of a task in a job.</span></span>
* <span data-ttu-id="cd2ee-265">Pode especificar JobInputAsset ou JobOutputAsset como um recurso de entrada de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-265">You can specify JobInputAsset or JobOutputAsset as an input asset of a task.</span></span>
* <span data-ttu-id="cd2ee-266">Tarefas tem não formam um ciclo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-266">Tasks must not form a cycle.</span></span>
* <span data-ttu-id="cd2ee-267">parâmetro de valor de Olá que passou tooJobInputAsset ou JobOutputAsset representa um valor de índice Olá para um recurso.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-267">hello value parameter that you pass tooJobInputAsset or JobOutputAsset represents hello index value for an Asset.</span></span> <span data-ttu-id="cd2ee-268">Olá reais ativos são definidos nas propriedades de navegação de InputMediaAssets e OutputMediaAssets Olá no Olá definição de entidade de tarefa.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-268">hello actual Assets are defined in hello InputMediaAssets and OutputMediaAssets navigation properties on hello Job entity definition.</span></span>

> [!NOTE]
> <span data-ttu-id="cd2ee-269">Porque os serviços de suporte de dados está incorporado no OData v3, Olá ativos individuais em InputMediaAssets e coleções de propriedade de navegação OutputMediaAssets referenciadas através de um " METADATA: uri" par nome / valor.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-269">Because Media Services is built on OData v3, hello individual assets in InputMediaAssets and OutputMediaAssets navigation property collections are referenced through a "__metadata : uri" name-value pair.</span></span>
>
>

* <span data-ttu-id="cd2ee-270">InputMediaAssets mapeia tooone ou mais recursos que criou nos Media Services.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-270">InputMediaAssets maps tooone or more Assets you have created in Media Services.</span></span> <span data-ttu-id="cd2ee-271">OutputMediaAssets são criados pelo sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-271">OutputMediaAssets are created by hello system.</span></span> <span data-ttu-id="cd2ee-272">Não faça referência a um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-272">They do not reference an existing asset.</span></span>
* <span data-ttu-id="cd2ee-273">OutputMediaAssets pode ter um nome utilizando Olá assetName atributo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-273">OutputMediaAssets can be named using hello assetName attribute.</span></span> <span data-ttu-id="cd2ee-274">Se este atributo não está presente, em seguida, nome de Olá do Olá OutputMediaAsset é qualquer valor de texto interno Olá de Olá <outputAsset> elemento está com um sufixo de valor de nome de tarefa Olá ou valor de Id da tarefa de Olá (no caso de Olá em que a propriedade de nome de Olá não está definida).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-274">If this attribute is not present, then hello name of hello OutputMediaAsset is whatever hello inner text value of hello <outputAsset> element is with a suffix of either hello Job Name value, or hello Job Id value (in hello case where hello Name property isn't defined).</span></span> <span data-ttu-id="cd2ee-275">Por exemplo, se definir um valor para assetName demasiado "Sample", em seguida, Olá seria possível definir a propriedade de nome de OutputMediaAsset demasiado "Sample".</span><span class="sxs-lookup"><span data-stu-id="cd2ee-275">For example, if you set a value for assetName too"Sample", then hello OutputMediaAsset Name property would be set too"Sample".</span></span> <span data-ttu-id="cd2ee-276">No entanto, se não definido um valor para assetName, mas definido o nome da tarefa Olá demasiado "NewJob", em seguida, Olá OutputMediaAsset nome seria "_NewJob JobOutputAsset (valor)".</span><span class="sxs-lookup"><span data-stu-id="cd2ee-276">However, if you did not set a value for assetName, but did set hello job name too"NewJob", then hello OutputMediaAsset Name would be "JobOutputAsset(value)_NewJob".</span></span>

    <span data-ttu-id="cd2ee-277">Olá seguinte exemplo mostra como tooset Olá assetName atributo:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-277">hello following example shows how tooset hello assetName attribute:</span></span>

        "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"
* <span data-ttu-id="cd2ee-278">tooenable encadeamento de tarefas:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-278">tooenable task chaining:</span></span>

  * <span data-ttu-id="cd2ee-279">Uma tarefa tem de ter, pelo menos, duas tarefas</span><span class="sxs-lookup"><span data-stu-id="cd2ee-279">A job must have at least two tasks</span></span>
  * <span data-ttu-id="cd2ee-280">Tem de existir pelo menos uma tarefa cuja entrada é a saída da tarefa na tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-280">There must be at least one task whose input is output of another task in hello job.</span></span>

<span data-ttu-id="cd2ee-281">Para obter mais informações, consulte [criar uma tarefa de codificação com Olá API de REST dos serviços de suporte de dados](media-services-rest-encode-asset.md).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-281">For more information see, [Creating an Encoding Job with hello Media Services REST API](media-services-rest-encode-asset.md).</span></span>

### <a name="monitor-processing-progress"></a><span data-ttu-id="cd2ee-282">Monitor de processamento de progresso</span><span class="sxs-lookup"><span data-stu-id="cd2ee-282">Monitor Processing Progress</span></span>
<span data-ttu-id="cd2ee-283">Pode obter o estado da tarefa Olá utilizando a propriedade de estado de Olá, conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-283">You can retrieve hello Job status by using hello State property, as shown in hello following example.</span></span>

<span data-ttu-id="cd2ee-284">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-284">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/State HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=zf84471d-2233-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908022&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=RYXOraO6Z%2f7l9whWZQN%2bypeijgHwIk8XyikA01Kx1%2bk%3d
    Host: wamsbayclus001rest-hs.net
    Content-Length: 0


<span data-ttu-id="cd2ee-285">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-285">**HTTP Response**</span></span>

<span data-ttu-id="cd2ee-286">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-286">If successful, hello following response is returned:</span></span>

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


### <a name="cancel-a-job"></a><span data-ttu-id="cd2ee-287">Cancelar uma tarefa</span><span class="sxs-lookup"><span data-stu-id="cd2ee-287">Cancel a job</span></span>
<span data-ttu-id="cd2ee-288">Os Media Services permite-lhe toocancel tarefas em execução através de Olá CancelJob função.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-288">Media Services allows you toocancel running jobs through hello CancelJob function.</span></span> <span data-ttu-id="cd2ee-289">Esta chamada devolve um código de 400 erro se tentar toocancel uma tarefa quando o estado é cancelado, cancelar, erro ou foi concluída.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-289">This call returns a 400 error code if you try toocancel a Job when its state is canceled, canceling, error, or finished.</span></span>

<span data-ttu-id="cd2ee-290">Olá seguinte exemplo mostra como toocall CancelJob.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-290">hello following example shows how toocall CancelJob.</span></span>

<span data-ttu-id="cd2ee-291">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-291">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.net/API/CancelJob?jobid='nb%3ajid%3aUUID%3a71d2dd33-efdf-ec43-8ea1-136a110bd42c' HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.2
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=youraccountname&urn%3aSubscriptionId=2f84471d-b1ae-4e75-aa09-010f0fc0cf5b&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1336908753&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=kolAgnFfbQIeRv4lWxKSFa4USyjWXRm15Kd%2bNd5g8eA%3d
    Host: wamsbayclus001rest-hs.net


<span data-ttu-id="cd2ee-292">Se tiver êxito, é devolvido um código de 204 resposta com nenhum corpo da mensagem.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-292">If successful, a 204 response code is returned with no message body.</span></span>

> [!NOTE]
> <span data-ttu-id="cd2ee-293">Tem o id da tarefa Olá codificar o URL (normalmente nb:jid:UUID: somevalue) ao transmiti-lo na como tooCancelJob um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-293">You must URL-encode hello job id (normally nb:jid:UUID: somevalue) when passing it in as a parameter tooCancelJob.</span></span>
>
>

### <a name="get-hello-output-asset"></a><span data-ttu-id="cd2ee-294">Obter o elemento de saída Olá</span><span class="sxs-lookup"><span data-stu-id="cd2ee-294">Get hello output asset</span></span>
<span data-ttu-id="cd2ee-295">Olá código seguinte mostra como toorequest Olá saída asset ID.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-295">hello following code shows how toorequest hello output asset Id.</span></span>

<span data-ttu-id="cd2ee-296">**Pedido de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-296">**HTTP Request**</span></span>

    GET https://wamsbayclus001rest-hs.cloudapp.net/api/Jobs('nb%3Ajid%3AUUID%3A71d2dd33-efdf-ec43-8ea1-136a110bd42c')/OutputMediaAssets() HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-2233-4ca2-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421675491&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=9hUudHYnATpi5hN3cvTfgw%2bL4N3tL0fdsRnQnm6ZYIU%3d
    x-ms-version: 2.11
    Host: wamsbayclus001rest-hs.cloudapp.net


<span data-ttu-id="cd2ee-297">**Resposta de HTTP**</span><span class="sxs-lookup"><span data-stu-id="cd2ee-297">**HTTP Response**</span></span>

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



## <span data-ttu-id="cd2ee-298"><a id="publish_get_urls"></a>Publicar asset Olá e get de transmissão em fluxo e transferência progressiva URLs REST API</span><span class="sxs-lookup"><span data-stu-id="cd2ee-298"><a id="publish_get_urls"></a>Publish hello asset and get streaming and progressive download URLs with REST API</span></span>

<span data-ttu-id="cd2ee-299">toostream ou transferir um recurso, primeiro tem de demasiado "publicar"-lo, criando um localizador.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-299">toostream or download an asset, you first need too"publish" it by creating a locator.</span></span> <span data-ttu-id="cd2ee-300">Os localizadores fornecem toofiles acesso contidos no elemento de Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-300">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="cd2ee-301">Os Media Services suportam dois tipos de Localizadores: OnDemandOrigin localizadores, toostream utilizados suportes de dados (por exemplo, MPEG DASH, HLS ou transmissão em fluxo uniforme) e localizadores de assinatura de acesso (SAS), utilizados ficheiros de multimédia toodownload.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-301">Media Services supports two types of locators: OnDemandOrigin locators, used toostream media (for example, MPEG DASH, HLS, or Smooth Streaming) and Access Signature (SAS) locators, used toodownload media files.</span></span> <span data-ttu-id="cd2ee-302">Para obter mais informações sobre SAS localizadores consulte [isto](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blogue.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-302">For more information about SAS locators see [this](http://southworks.com/blog/2015/05/27/reusing-azure-media-services-locators-to-avoid-facing-the-5-shared-access-policy-limitation/) blog.</span></span>

<span data-ttu-id="cd2ee-303">Depois de criar os localizadores Olá, pode criar URLs de Olá que são utilizado toostream ou transferir os seus ficheiros.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-303">Once you create hello locators, you can build hello URLs that are used toostream or download your files.</span></span>

>[!NOTE]
><span data-ttu-id="cd2ee-304">Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-304">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="cd2ee-305">toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-305">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span>

<span data-ttu-id="cd2ee-306">Um URL de transmissão em fluxo para transmissão em fluxo uniforme tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-306">A streaming URL for Smooth Streaming has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="cd2ee-307">Um URL de transmissão em fluxo para HLS tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-307">A streaming URL for HLS has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="cd2ee-308">Um URL de transmissão em fluxo para MPEG DASH tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-308">A streaming URL for MPEG DASH has hello following format:</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="cd2ee-309">Ficheiros de toodownload um URL SAS utilizado tem Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-309">A SAS URL used toodownload files has hello following format:</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

<span data-ttu-id="cd2ee-310">Esta secção mostra como seguinte de Olá tooperform tarefas necessárias demasiado "publicar" os elementos.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-310">This section shows how tooperform hello following tasks necessary too"publish" your assets.</span></span>  

* <span data-ttu-id="cd2ee-311">Criar Olá AccessPolicy com permissão de leitura</span><span class="sxs-lookup"><span data-stu-id="cd2ee-311">Creating hello AccessPolicy with read permission</span></span>
* <span data-ttu-id="cd2ee-312">Criar um URL SAS para transferir conteúdo</span><span class="sxs-lookup"><span data-stu-id="cd2ee-312">Creating a SAS URL for downloading content</span></span>
* <span data-ttu-id="cd2ee-313">Criar um URL de origem para conteúdo de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="cd2ee-313">Creating an origin URL for streaming content</span></span>

### <a name="creating-hello-accesspolicy-with-read-permission"></a><span data-ttu-id="cd2ee-314">Criar Olá AccessPolicy com permissão de leitura</span><span class="sxs-lookup"><span data-stu-id="cd2ee-314">Creating hello AccessPolicy with read permission</span></span>
<span data-ttu-id="cd2ee-315">Antes de transferir ou qualquer conteúdo de multimédia de transmissão em fluxo, definir em primeiro lugar um AccessPolicy com permissões para ler e criar a entidade localizador adequada Olá que especifica o tipo de Olá de mecanismo de entrega que pretende tooenable para os seus clientes.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-315">Before downloading or streaming any media content, first define an AccessPolicy with read permissions and create hello appropriate Locator entity that specifies hello type of delivery mechanism you want tooenable for your clients.</span></span> <span data-ttu-id="cd2ee-316">Para obter mais informações sobre as propriedades de Olá disponíveis, consulte [propriedades de entidade AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-316">For more information on hello properties available, see [AccessPolicy Entity Properties](https://docs.microsoft.com/rest/api/media/operations/accesspolicy#accesspolicy_properties).</span></span>

<span data-ttu-id="cd2ee-317">Olá seguinte exemplo mostra como toospecify Olá AccessPolicy para permissões de leitura para um ativo especificado.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-317">hello following example shows how toospecify hello AccessPolicy for read permissions for a given Asset.</span></span>

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

<span data-ttu-id="cd2ee-318">Se tiver êxito, é devolvido um código de 201 êxito que descrevem a entidade de AccessPolicy Olá que criou.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-318">If successful, a 201 success code is returned describing hello AccessPolicy entity that you created.</span></span> <span data-ttu-id="cd2ee-319">Em seguida, utilize Olá AccessPolicy Id juntamente com Olá Id de recurso do elemento de Olá que contenha os ficheiros de Olá pretende que a entidade de localizador de Olá de toocreate toodeliver (por exemplo, um elemento de saída).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-319">You then use hello AccessPolicy Id along with hello Asset Id of hello asset that contains hello file you want toodeliver(such as an output asset) toocreate hello Locator entity.</span></span>

> [!NOTE]
> <span data-ttu-id="cd2ee-320">Este fluxo de trabalho básico é Olá igual ao carregar um ficheiro quando um recurso de ingestão de relacionadas (conforme foi apresentadas anteriormente neste tópico).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-320">This basic workflow is hello same as uploading a file when ingesting an Asset (as was discussed earlier in this topic).</span></span> <span data-ttu-id="cd2ee-321">Além disso, como carregar ficheiros, se precisam de utilizador (ou os seus clientes) tooaccess os ficheiros imediatamente, defina os minutos de toofive de valor de StartTime antes Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-321">Also, like uploading files, if you (or your clients) need tooaccess your files immediately, set your StartTime value toofive minutes before hello current time.</span></span> <span data-ttu-id="cd2ee-322">Esta ação é necessária porque poderá haver relógio dissimetrias entre o cliente de Olá e dos Media Services.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-322">This action is necessary because there may be clock skew between hello client and Media Services.</span></span> <span data-ttu-id="cd2ee-323">Olá StartTime valor tem de constar Olá seguir o formato DateTime: aaaa-MM-aaaathh (por exemplo, "2014-05-23T17:53:50Z").</span><span class="sxs-lookup"><span data-stu-id="cd2ee-323">hello StartTime value must be in hello following DateTime format: YYYY-MM-DDTHH:mm:ssZ (for example, "2014-05-23T17:53:50Z").</span></span>
>
>

### <a name="creating-a-sas-url-for-downloading-content"></a><span data-ttu-id="cd2ee-324">Criar um URL SAS para transferir conteúdo</span><span class="sxs-lookup"><span data-stu-id="cd2ee-324">Creating a SAS URL for downloading content</span></span>
<span data-ttu-id="cd2ee-325">Olá código a seguir mostra como tooget um URL que pode ser utilizado toodownload um ficheiro de multimédia criado e carregou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-325">hello following code shows how tooget a URL that can be used toodownload a media file created and uploaded previously.</span></span> <span data-ttu-id="cd2ee-326">Olá AccessPolicy tem conjunto de permissões de leitura e o caminho de localizador Olá refere-se o URL de transferência do tooa SAS.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-326">hello AccessPolicy has read permissions set and hello Locator path refers tooa SAS download URL.</span></span>

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

<span data-ttu-id="cd2ee-327">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-327">If successful, hello following response is returned:</span></span>

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


<span data-ttu-id="cd2ee-328">Olá devolvido **caminho** propriedade contém Olá SAS URL.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-328">hello returned **Path** property contains hello SAS URL.</span></span>

> [!NOTE]
> <span data-ttu-id="cd2ee-329">Se transferir conteúdo do armazenamento encriptado, tem manualmente desencriptá-lo antes de composição, ou utilize Olá MediaProcessor de desencriptação de armazenamento num toooutput de tarefa de processamento processados ficheiros Olá limpar tooan OutputAsset e, em seguida, transferir a partir desse recurso.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-329">If you download storage encrypted content, you must manually decrypt it before rendering it, or use hello Storage Decryption MediaProcessor in a processing task toooutput processed files in hello clear tooan OutputAsset and then download from that Asset.</span></span> <span data-ttu-id="cd2ee-330">Para obter mais informações sobre o processamento, consulte Criar uma tarefa de codificação com Olá API de REST dos serviços de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-330">For more information on processing, see Creating an Encoding Job with hello Media Services REST API.</span></span> <span data-ttu-id="cd2ee-331">Além disso, os localizadores de URL SAS não pode ser atualizados depois de terem sido criadas.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-331">Also, SAS URL Locators cannot be updated after they have been created.</span></span> <span data-ttu-id="cd2ee-332">Por exemplo, não é possível reutilizar Olá localizador mesmo com um valor de StartTime atualizado.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-332">For example, you cannot reuse hello same Locator with an updated StartTime value.</span></span> <span data-ttu-id="cd2ee-333">Trata-se devido a forma de Olá URLs de SAS que são criados.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-333">This is because of hello way SAS URLs are created.</span></span> <span data-ttu-id="cd2ee-334">Se quiser tooaccess um recurso para transferência após um localizador tiver expirado, terá de criar um novo com uma StartTime novo.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-334">If you want tooaccess an asset for download after a Locator has expired, then you must create a new one with a new StartTime.</span></span>
>
>

### <a name="download-files"></a><span data-ttu-id="cd2ee-335">Transferir ficheiros</span><span class="sxs-lookup"><span data-stu-id="cd2ee-335">Download files</span></span>
<span data-ttu-id="cd2ee-336">Assim que tiver Olá AccessPolicy e o conjunto de localizador, pode transferir ficheiros utilizando Olá APIs de REST de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-336">Once you have hello AccessPolicy and Locator set, you can download files using hello Azure Storage REST APIs.</span></span>  

> [!NOTE]
> <span data-ttu-id="cd2ee-337">Tem de adicionar o nome de ficheiro Olá ficheiro Olá pretende toodownload toohello localizador **caminho** valor recebido na secção anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-337">You must add hello file name for hello file you want toodownload toohello Locator **Path** value received in hello previous section.</span></span> <span data-ttu-id="cd2ee-338">Por exemplo, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span><span class="sxs-lookup"><span data-stu-id="cd2ee-338">For example, https://storagetestaccount001.blob.core.windows.net/asset-e7b02da4-5a69-40e7-a8db-e8f4f697aac0/BigBuckBunny.mp4?</span></span> <span data-ttu-id="cd2ee-339">.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-339">.</span></span> <span data-ttu-id="cd2ee-340">.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-340">.</span></span> <span data-ttu-id="cd2ee-341">.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-341">.</span></span>
>
>

<span data-ttu-id="cd2ee-342">Para obter mais informações sobre como trabalhar com blobs de armazenamento do Azure, consulte [API de REST do serviço Blob](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-342">For more information on working with Azure storage blobs, see [Blob Service REST API](https://docs.microsoft.com/rest/api/storageservices/Blob-Service-REST-API).</span></span>

<span data-ttu-id="cd2ee-343">Como resultado Olá codificação tarefa que efetuou anteriormente (codificação num conjunto de MP4 adaptável), terá de vários ficheiros MP4 que pode transferir progressivamente.</span><span class="sxs-lookup"><span data-stu-id="cd2ee-343">As a result of hello encoding job that you performed earlier (encoding into Adaptive MP4 set), you have multiple MP4 files that you can progressively download.</span></span> <span data-ttu-id="cd2ee-344">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-344">For example:</span></span>    

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_96kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z

    https://storagetestaccount001.blob.core.windows.net/asset-38058602-a4b8-4b33-b9f0-6880dc1490ea/BigBuckBunny_AAC_und_ch2_56kbps.mp4?sv=2012-02-12&sr=c&si=166d5154-b801-410b-a226-ee2f8eac1929&sig=P2iNZJAvAWpp%2Bj9yV6TQjoz5DIIaj7ve8ARynmEM6Xk%3D&se=2015-02-14T01:13:05Z


### <a name="creating-a-streaming-url-for-streaming-content"></a><span data-ttu-id="cd2ee-345">Criar um URL de transmissão em fluxo para conteúdos de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="cd2ee-345">Creating a streaming URL for streaming content</span></span>
<span data-ttu-id="cd2ee-346">Olá a seguir mostra código como toocreate um localizador de URL de transmissão em fluxo:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-346">hello following code shows how toocreate a streaming URL Locator:</span></span>

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

<span data-ttu-id="cd2ee-347">Se tiver êxito, é devolvido Olá seguinte resposta:</span><span class="sxs-lookup"><span data-stu-id="cd2ee-347">If successful, hello following response is returned:</span></span>

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

<span data-ttu-id="cd2ee-348">toostream um URL de origem de transmissão em fluxo uniforme num leitor de multimédia de transmissão em fluxo, tem de anexar a propriedade Path Olá com nome Olá Olá transmissão em fluxo uniforme manifesto do ficheiro, seguido por "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="cd2ee-348">toostream a Smooth Streaming origin URL in a streaming media player, you must append hello Path property with hello name of hello Smooth Streaming manifest file, followed by "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest

<span data-ttu-id="cd2ee-349">toostream HLS, acrescente (formato = m3u8-aapl) após Olá "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="cd2ee-349">toostream HLS, append (format=m3u8-aapl) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=m3u8-aapl)

<span data-ttu-id="cd2ee-350">toostream MPEG DASH, acrescente (formato = mpd-time-csf) após Olá "/ manifest".</span><span class="sxs-lookup"><span data-stu-id="cd2ee-350">toostream MPEG DASH, append (format=mpd-time-csf) after hello "/manifest".</span></span>

    http://amstestaccount001.streaming.mediaservices.windows.net/ebf733c4-3e2e-4a68-b67b-cc5159d1d7f2/BigBuckBunny.ism/manifest(format=mpd-time-csf)


## <span data-ttu-id="cd2ee-351"><a id="play"></a>Reproduza o seu conteúdo</span><span class="sxs-lookup"><span data-stu-id="cd2ee-351"><a id="play"></a>Play your content</span></span>
<span data-ttu-id="cd2ee-352">toostream vídeo, utilize [leitor de Media Services do Azure](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-352">toostream you video, use [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

<span data-ttu-id="cd2ee-353">tootest transferência progressiva transferir, cole um URL no browser (por exemplo, IE, Chrome, Safari).</span><span class="sxs-lookup"><span data-stu-id="cd2ee-353">tootest progressive download, paste a URL into a browser (for example, IE, Chrome, Safari).</span></span>

## <a name="next-steps-media-services-learning-paths"></a><span data-ttu-id="cd2ee-354">Passos Seguintes: percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="cd2ee-354">Next Steps: Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="cd2ee-355">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="cd2ee-355">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
