---
title: "aaaUsing PlayReady e/ou Widevine a encriptação comum dinâmica | Microsoft Docs"
description: "Serviços de suporte de dados do Microsoft Azure permite-lhe toodeliver MPEG-DASH, transmissão em fluxo uniforme e Http-Live-Streaming (HLS) fluxos protegidos com o Microsoft PlayReady DRM. Também permite-lhe toodelivery DASH encriptado com Widevine DRM. Este tópico mostra como toodynamically encriptar com PlayReady e Widevine DRM."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 548d1a12-e2cb-45fe-9307-4ec0320567a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 0475e6ec80dcf39eb4e5c4ad4d17f821502951bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-playready-andor-widevine-dynamic-common-encryption"></a><span data-ttu-id="70b1c-105">Utilizar a encriptação comum dinâmica com PlayReady e/ou Widevine</span><span class="sxs-lookup"><span data-stu-id="70b1c-105">Using PlayReady and/or Widevine dynamic common encryption</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="70b1c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="70b1c-106">.NET</span></span>](media-services-protect-with-drm.md)
> * [<span data-ttu-id="70b1c-107">Java</span><span class="sxs-lookup"><span data-stu-id="70b1c-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="70b1c-108">PHP</span><span class="sxs-lookup"><span data-stu-id="70b1c-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
>
>

<span data-ttu-id="70b1c-109">Serviços de suporte de dados do Microsoft Azure permite-lhe toodeliver MPEG-DASH, transmissão em fluxo uniforme e fluxos de HTTP-Live-Streaming (HLS) protegidos com [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span><span class="sxs-lookup"><span data-stu-id="70b1c-109">Microsoft Azure Media Services enables you toodeliver MPEG-DASH, Smooth Streaming, and HTTP-Live-Streaming (HLS) streams protected with [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/).</span></span> <span data-ttu-id="70b1c-110">Também permite-lhe toodeliver encriptado transmissões em fluxo DASH com licenças Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="70b1c-110">It also enables you toodeliver encrypted DASH streams with Widevine DRM licenses.</span></span> <span data-ttu-id="70b1c-111">Tanto PlayReady como Widevine são encriptados por Olá especificação de encriptação comum (ISO/IEC 23001 7 CENC).</span><span class="sxs-lookup"><span data-stu-id="70b1c-111">Both PlayReady and Widevine are encrypted per hello Common Encryption (ISO/IEC 23001-7 CENC) specification.</span></span> <span data-ttu-id="70b1c-112">Pode utilizar [SDK .NET do AMS](https://www.nuget.org/packages/windowsazure.mediaservices/) (começando com a versão de Olá 3.5.1) ou REST API tooconfigure toouse seu AssetDeliveryConfiguration Widevine.</span><span class="sxs-lookup"><span data-stu-id="70b1c-112">You can use [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (starting with hello version 3.5.1) or REST API tooconfigure your AssetDeliveryConfiguration toouse Widevine.</span></span>

<span data-ttu-id="70b1c-113">Os Media Services fornecem um serviço para entrega de licenças PlayReady e Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="70b1c-113">Media Services provides a service for delivering PlayReady and Widevine DRM licenses.</span></span> <span data-ttu-id="70b1c-114">Os Media Services também fornecem APIs que permitem-lhe configurar Olá direitos e restrições que pretende para Olá PlayReady ou Widevine DRM runtime tooenforce quando um utilizador reproduz conteúdo protegido.</span><span class="sxs-lookup"><span data-stu-id="70b1c-114">Media Services also provides APIs that let you configure hello rights and restrictions that you want for hello PlayReady or Widevine DRM runtime tooenforce when a user plays back protected content.</span></span> <span data-ttu-id="70b1c-115">Quando um utilizador solicita um conteúdo DRM protegido, a aplicação de leitor de Olá solicitará uma licença do serviço de licença de Olá AMS.</span><span class="sxs-lookup"><span data-stu-id="70b1c-115">When a user requests a DRM protected content, hello player application will request a license from hello AMS license service.</span></span> <span data-ttu-id="70b1c-116">serviço de licença do AMS Olá irá emitir um leitor de toohello licença se está autorizado.</span><span class="sxs-lookup"><span data-stu-id="70b1c-116">hello AMS license service will issue a license toohello player if it is authorized.</span></span> <span data-ttu-id="70b1c-117">Uma licença PlayReady ou Widevine contém a chave de desencriptação de Olá que pode ser utilizado por Olá cliente player toodecrypt e fluxo Olá conteúdo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-117">A PlayReady or Widevine license contains hello decryption key that can be used by hello client player toodecrypt and stream hello content.</span></span>

<span data-ttu-id="70b1c-118">Também pode utilizar Olá seguir toohelp de parceiros de AMS fornecer licenças Widevine: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="70b1c-118">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span> <span data-ttu-id="70b1c-119">Para obter mais informações, consulte: integração com [Axinom](media-services-axinom-integration.md) e [castLabs](media-services-castlabs-integration.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-119">For more information, see: integration with [Axinom](media-services-axinom-integration.md) and [castLabs](media-services-castlabs-integration.md).</span></span>

<span data-ttu-id="70b1c-120">Os Media Services suportam várias formas de autorização de utilizadores que efetuam pedidos de chave.</span><span class="sxs-lookup"><span data-stu-id="70b1c-120">Media Services supports multiple ways of authorizing users who make key requests.</span></span> <span data-ttu-id="70b1c-121">Olá política de autorização da chave de conteúdo pode ter um ou mais restrições de autorização: aberto ou token restrito.</span><span class="sxs-lookup"><span data-stu-id="70b1c-121">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span> <span data-ttu-id="70b1c-122">política de Olá token restrito tem de ser acompanhada por um token emitido por uma Secure Token serviço (STS).</span><span class="sxs-lookup"><span data-stu-id="70b1c-122">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS).</span></span> <span data-ttu-id="70b1c-123">Os Media Services suportam tokens no Olá [Web Tokens simples](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) formato (SWT) e [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) formato (JWT).</span><span class="sxs-lookup"><span data-stu-id="70b1c-123">Media Services supports tokens in hello [Simple Web Tokens](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2) (SWT) format and [JSON Web Token](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_3) (JWT) format.</span></span> <span data-ttu-id="70b1c-124">Para obter mais informações, consulte a política de autorização de configurar Olá da chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-124">For more information, see Configure hello content key’s authorization policy.</span></span>

<span data-ttu-id="70b1c-125">tootake partido da encriptação dinâmica, terá de toohave um elemento que contenha um conjunto de ficheiros MP4 de velocidade de transmissão múltipla ou ficheiros de origem de transmissão em fluxo uniforme de transmissão múltipla.</span><span class="sxs-lookup"><span data-stu-id="70b1c-125">tootake advantage of dynamic encryption, you need toohave an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="70b1c-126">Também precisa de políticas de entrega de Olá tooconfigure para ativo Olá (descrito mais à frente neste tópico).</span><span class="sxs-lookup"><span data-stu-id="70b1c-126">You also need tooconfigure hello delivery policies for hello asset (described later in this topic).</span></span> <span data-ttu-id="70b1c-127">Em seguida, com base no formato de Olá especificado no URL de transmissão em fluxo de Olá, servidor de transmissão em fluxo a pedido Olá irá garantir que esse fluxo Olá é entregue no protocolo Olá que escolheu.</span><span class="sxs-lookup"><span data-stu-id="70b1c-127">Then, based on hello format specified in hello streaming URL, hello On-Demand Streaming server will ensure that hello stream is delivered in hello protocol you have chosen.</span></span> <span data-ttu-id="70b1c-128">Como resultado, só precisa de toostore e pagamento para ficheiros de Olá num único formato de armazenamento e dos Media Services irão compilar e disponibilizar Olá HTTP resposta adequada com base em cada pedido de um cliente.</span><span class="sxs-lookup"><span data-stu-id="70b1c-128">As a result, you only need toostore and pay for hello files in a single storage format and Media Services will build and serve hello appropriate HTTP response based on each request from a client.</span></span>

<span data-ttu-id="70b1c-129">Este tópico seria útil toodevelopers que funcionam em aplicações que entregam multimédia protegida com vários DRMs, tais como PlayReady e Widevine.</span><span class="sxs-lookup"><span data-stu-id="70b1c-129">This topic would be useful toodevelopers that work on applications that deliver media protected with multiple DRMs, such as PlayReady and Widevine.</span></span> <span data-ttu-id="70b1c-130">tópico de Olá mostra como tooconfigure Olá ao serviço de entrega de licença PlayReady com políticas de autorização para que apenas os clientes autorizados foi receber licenças PlayReady ou Widevine.</span><span class="sxs-lookup"><span data-stu-id="70b1c-130">hello topic shows you how tooconfigure hello PlayReady license delivery service with authorization policies so that only authorized clients could receive PlayReady or Widevine licenses.</span></span> <span data-ttu-id="70b1c-131">Também mostra como toouse encriptação dinâmica com PlayReady ou Widevine DRM sobre DASH.</span><span class="sxs-lookup"><span data-stu-id="70b1c-131">It also shows how toouse dynamic encryption encryption with PlayReady or Widevine DRM over DASH.</span></span>

>[!NOTE]
><span data-ttu-id="70b1c-132">Quando a sua conta de AMS é criada um **predefinido** ponto final de transmissão em fluxo é adicionada a conta de tooyour no Olá **parado** estado.</span><span class="sxs-lookup"><span data-stu-id="70b1c-132">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="70b1c-133">toostart transmissão em fluxo o conteúdo e tomar partido do empacotamento dinâmico e a encriptação dinâmica, Olá ponto final transmissão a partir do qual pretende que o conteúdo de toostream tem toobe no Olá **executar** estado.</span><span class="sxs-lookup"><span data-stu-id="70b1c-133">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

## <a name="download-sample"></a><span data-ttu-id="70b1c-134">Transferir exemplo</span><span class="sxs-lookup"><span data-stu-id="70b1c-134">Download sample</span></span>
<span data-ttu-id="70b1c-135">Pode transferir o exemplo de Olá descrito neste artigo [aqui](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span><span class="sxs-lookup"><span data-stu-id="70b1c-135">You can download hello sample described in this article from [here](https://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm).</span></span>

## <a name="configuring-dynamic-common-encryption-and-drm-license-delivery-services"></a><span data-ttu-id="70b1c-136">Configurar a Encriptação Comum Dinâmica e os Serviços de Entrega de Licença DRM</span><span class="sxs-lookup"><span data-stu-id="70b1c-136">Configuring Dynamic Common Encryption and DRM License Delivery Services</span></span>

<span data-ttu-id="70b1c-137">Olá seguem-se passos gerais que teria tooperform quando proteger os seus elementos com PlayReady, utilizando o serviço de entrega de licença de Media Services Olá e também da encriptação dinâmica.</span><span class="sxs-lookup"><span data-stu-id="70b1c-137">hello following are general steps that you would need tooperform when protecting your assets with PlayReady, using hello Media Services license delivery service, and also using dynamic encryption.</span></span>

1. <span data-ttu-id="70b1c-138">Criar um elemento e carregar ficheiros para o elemento de Olá.</span><span class="sxs-lookup"><span data-stu-id="70b1c-138">Create an asset and upload files into hello asset.</span></span>
2. <span data-ttu-id="70b1c-139">Codificar Olá asset contentora Olá ficheiro toohello velocidade de transmissão adaptável definido MP4.</span><span class="sxs-lookup"><span data-stu-id="70b1c-139">Encode hello asset containing hello file toohello adaptive bitrate MP4 set.</span></span>
3. <span data-ttu-id="70b1c-140">Criar uma chave de conteúdo e associe-a com elemento Olá codificado.</span><span class="sxs-lookup"><span data-stu-id="70b1c-140">Create a content key and associate it with hello encoded asset.</span></span> <span data-ttu-id="70b1c-141">Nos Media Services, chave de conteúdo de Olá contém a chave de encriptação do elemento de Olá.</span><span class="sxs-lookup"><span data-stu-id="70b1c-141">In Media Services, hello content key contains hello asset’s encryption key.</span></span>
4. <span data-ttu-id="70b1c-142">Configure a política de autorização de Olá da chave de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-142">Configure hello content key’s authorization policy.</span></span> <span data-ttu-id="70b1c-143">política de autorização da chave de conteúdo de Olá tem de ser configurada por si e cumprida pelo cliente de Olá para Olá conteúdo toobe chave toohello entregue cliente.</span><span class="sxs-lookup"><span data-stu-id="70b1c-143">hello content key authorization policy must be configured by you and met by hello client in order for hello content key toobe delivered toohello client.</span></span>

    <span data-ttu-id="70b1c-144">Ao criar a política de autorização da chave de conteúdo de Olá, seguintes elementos terão de toospecify Olá: entrega método (PlayReady ou Widevine), restrições (aberto ou token) e o tipo de entrega de chave de toohello específico informações que define a forma como a chave de Olá é entregue cliente toohello ([PlayReady](media-services-playready-license-template-overview.md) ou [Widevine](media-services-widevine-license-template-overview.md) o modelo de licença).</span><span class="sxs-lookup"><span data-stu-id="70b1c-144">When creating hello content key authorization policy, you need toospecify hello following: delivery method (PlayReady or Widevine), restrictions (open or token), and information specific toohello key delivery type that defines how hello key is delivered toohello client ([PlayReady](media-services-playready-license-template-overview.md) or [Widevine](media-services-widevine-license-template-overview.md) license template).</span></span>

5. <span data-ttu-id="70b1c-145">Configure a política de entrega de Olá para um recurso.</span><span class="sxs-lookup"><span data-stu-id="70b1c-145">Configure hello delivery policy for an asset.</span></span> <span data-ttu-id="70b1c-146">configuração de políticas de entrega de Olá inclui: protocolo entrega (por exemplo, MPEG DASH, HLS, transmissão em fluxo uniforme ou todos), Olá tipo de encriptação dinâmica (por exemplo, encriptação comum), PlayReady ou Widevine URL de aquisição de licença.</span><span class="sxs-lookup"><span data-stu-id="70b1c-146">hello delivery policy configuration includes: delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all), hello type of dynamic encryption (for example, Common Encryption), PlayReady or Widevine license acquisition URL.</span></span>

    <span data-ttu-id="70b1c-147">Foi possível aplicar o protocolo de tooeach outra política no Olá mesmo elemento.</span><span class="sxs-lookup"><span data-stu-id="70b1c-147">You could apply different policy tooeach protocol on hello same asset.</span></span> <span data-ttu-id="70b1c-148">Por exemplo, pode aplicar encriptação de PlayReady tooSmooth/DASH e AES Envelope tooHLS.</span><span class="sxs-lookup"><span data-stu-id="70b1c-148">For example, you could apply PlayReady encryption tooSmooth/DASH and AES Envelope tooHLS.</span></span> <span data-ttu-id="70b1c-149">Quaisquer protocolos que não estão definidos numa política de entrega (por exemplo, adicionar uma única política que especifica apenas HLS como protocolo de Olá) serão bloqueados da transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-149">Any protocols that are not defined in a delivery policy (for example, you add a single policy that only specifies HLS as hello protocol) will be blocked from streaming.</span></span> <span data-ttu-id="70b1c-150">Olá toothis de exceção é não se tiver nenhuma política de entrega de elemento definida de todo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-150">hello exception toothis is if you have no asset delivery policy defined at all.</span></span> <span data-ttu-id="70b1c-151">Em seguida, todos os protocolos serão permitidos na Olá encriptado.</span><span class="sxs-lookup"><span data-stu-id="70b1c-151">Then, all protocols will be allowed in hello clear.</span></span>

6. <span data-ttu-id="70b1c-152">Crie um localizador OnDemand na ordem tooget um URL de transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-152">Create an OnDemand locator in order tooget a streaming URL.</span></span>

<span data-ttu-id="70b1c-153">Irá encontrar um exemplo .NET concluído no final de Olá tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="70b1c-153">You will find a complete .NET example at hello end of hello topic.</span></span>

<span data-ttu-id="70b1c-154">Olá seguinte imagem demonstra o fluxo de trabalho de Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="70b1c-154">hello following image demonstrates hello workflow described above.</span></span> <span data-ttu-id="70b1c-155">Aqui o token de Olá é utilizado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="70b1c-155">Here hello token is used for authentication.</span></span>

![Proteger com PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-drm.png)

<span data-ttu-id="70b1c-157">resto Olá deste tópico fornece explicações detalhadas, exemplos de código e ligações tootopics que mostram como tooachieve Olá tarefas descritas acima.</span><span class="sxs-lookup"><span data-stu-id="70b1c-157">hello rest of this topic provides detailed explanations, code examples, and links tootopics that show you how tooachieve hello tasks described above.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="70b1c-158">Limitações atuais</span><span class="sxs-lookup"><span data-stu-id="70b1c-158">Current limitations</span></span>
<span data-ttu-id="70b1c-159">Se adicionar ou atualizar uma política de entrega de elemento, tem de eliminar o localizador de Olá associada (se aplicável) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="70b1c-159">If you add or update an asset delivery policy, you must delete hello associated locator (if any) and create a new locator.</span></span>

<span data-ttu-id="70b1c-160">Limitação ao encriptar com Widevine com os Media Services do Azure: atualmente, não são suportados várias chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-160">Limitation when encrypting with Widevine with Azure Media Services: currently, multiple content keys are not supported.</span></span>

## <a name="create-an-asset-and-upload-files-into-hello-asset"></a><span data-ttu-id="70b1c-161">Criar um elemento e carregar ficheiros para o elemento de Olá</span><span class="sxs-lookup"><span data-stu-id="70b1c-161">Create an asset and upload files into hello asset</span></span>
<span data-ttu-id="70b1c-162">Na ordem toomanage, codificar e transmitir os seus vídeos, primeiro tem de carregar o conteúdo para os Media Services do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="70b1c-162">In order toomanage, encode, and stream your videos, you must first upload your content into Microsoft Azure Media Services.</span></span> <span data-ttu-id="70b1c-163">Assim que seja carregado, o conteúdo estiver armazenado em segurança na nuvem de Olá para processamento adicional e a transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-163">Once uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="70b1c-164">Para obter informações detalhadas, consulte [Carregar Ficheiros para uma conta de Media Services](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-164">For detailed information, see [Upload Files into a Media Services account](media-services-dotnet-upload-files.md).</span></span>

## <a name="encode-hello-asset-containing-hello-file-toohello-adaptive-bitrate-mp4-set"></a><span data-ttu-id="70b1c-165">Codificar Olá asset contentora Olá ficheiro toohello velocidade de transmissão adaptável definido MP4</span><span class="sxs-lookup"><span data-stu-id="70b1c-165">Encode hello asset containing hello file toohello adaptive bitrate MP4 set</span></span>
<span data-ttu-id="70b1c-166">Com a encriptação dinâmica, tudo o que precisa é toocreate um elemento que contenha um conjunto de ficheiros MP4 de velocidade de transmissão múltipla ou ficheiros de origem de transmissão em fluxo uniforme de transmissão múltipla.</span><span class="sxs-lookup"><span data-stu-id="70b1c-166">With dynamic encryption all you need is toocreate an asset that contains a set of multi-bitrate MP4 files or multi-bitrate Smooth Streaming source files.</span></span> <span data-ttu-id="70b1c-167">Em seguida, com base no Olá formato especificado no manifesto de Olá e pedido de fragmento, Olá a pedido de transmissão em fluxo servidor irá garantir que recebem o fluxo de Olá no protocolo Olá que escolheu.</span><span class="sxs-lookup"><span data-stu-id="70b1c-167">Then, based on hello specified format in hello manifest and fragment request, hello On-Demand Streaming server will ensure that you receive hello stream in hello protocol you have chosen.</span></span> <span data-ttu-id="70b1c-168">Como resultado, só precisa de toostore e pagamento para ficheiros de Olá num único formato de armazenamento e o serviço de Media Services irão compilar e disponibilizar a resposta adequada Olá com base nos pedidos de um cliente.</span><span class="sxs-lookup"><span data-stu-id="70b1c-168">As a result, you only need toostore and pay for hello files in single storage format and Media Services service will build and serve hello appropriate response based on requests from a client.</span></span> <span data-ttu-id="70b1c-169">Para obter mais informações, consulte Olá [descrição geral de empacotamento dinâmico](media-services-dynamic-packaging-overview.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="70b1c-169">For more information, see hello [Dynamic Packaging Overview](media-services-dynamic-packaging-overview.md) topic.</span></span>

<span data-ttu-id="70b1c-170">Para obter instruções sobre como tooencode, consulte [como tooencode um elemento com o codificador de multimédia Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-170">For instructions on how tooencode, see [How tooencode an asset using Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md).</span></span>

## <span data-ttu-id="70b1c-171"><a id="create_contentkey"></a>Criar uma chave de conteúdo e associe-a com elemento codificado de Olá</span><span class="sxs-lookup"><span data-stu-id="70b1c-171"><a id="create_contentkey"></a>Create a content key and associate it with hello encoded asset</span></span>
<span data-ttu-id="70b1c-172">Nos Media Services, chave de conteúdo de Olá contém a chave de Olá que pretende que o tooencrypt um recurso de com.</span><span class="sxs-lookup"><span data-stu-id="70b1c-172">In Media Services, hello content key contains hello key that you want tooencrypt an asset with.</span></span>

<span data-ttu-id="70b1c-173">Para obter informações detalhadas, consulte [Criar chave de conteúdo](media-services-dotnet-create-contentkey.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-173">For detailed information, see [Create content key](media-services-dotnet-create-contentkey.md).</span></span>

## <span data-ttu-id="70b1c-174"><a id="configure_key_auth_policy"></a>Configurar a política de autorização de Olá da chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="70b1c-174"><a id="configure_key_auth_policy"></a>Configure hello content key’s authorization policy</span></span>
<span data-ttu-id="70b1c-175">Os Media Services suportam várias formas de autenticar utilizadores que efetuam pedidos de chave.</span><span class="sxs-lookup"><span data-stu-id="70b1c-175">Media Services supports multiple ways of authenticating users who make key requests.</span></span> <span data-ttu-id="70b1c-176">política de autorização da chave de conteúdo de Olá tem de ser configurada por si e cumprida pelo cliente de Olá (leitor) para que toobe chave Olá entregar toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="70b1c-176">hello content key authorization policy must be configured by you and met by hello client (player) in order for hello key toobe delivered toohello client.</span></span> <span data-ttu-id="70b1c-177">Olá política de autorização da chave de conteúdo pode ter um ou mais restrições de autorização: aberto ou token restrito.</span><span class="sxs-lookup"><span data-stu-id="70b1c-177">hello content key authorization policy could have one or more authorization restrictions: open or token restriction.</span></span>

<span data-ttu-id="70b1c-178">Para obter informações detalhadas, consulte [Configurar a Política de Autorização da Chave de Conteúdo](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span><span class="sxs-lookup"><span data-stu-id="70b1c-178">For detailed information, see [Configure Content Key Authorization Policy](media-services-dotnet-configure-content-key-auth-policy.md#playready-dynamic-encryption).</span></span>

## <span data-ttu-id="70b1c-179"><a id="configure_asset_delivery_policy"></a>Configurar a política de entrega de elemento</span><span class="sxs-lookup"><span data-stu-id="70b1c-179"><a id="configure_asset_delivery_policy"></a>Configure asset delivery policy</span></span>
<span data-ttu-id="70b1c-180">Configure a política de entrega de Olá para o seu elemento.</span><span class="sxs-lookup"><span data-stu-id="70b1c-180">Configure hello delivery policy for your asset.</span></span> <span data-ttu-id="70b1c-181">Alguns dos aspetos Olá configuração de política de entrega de elemento inclui:</span><span class="sxs-lookup"><span data-stu-id="70b1c-181">Some things that hello asset delivery policy configuration includes:</span></span>

* <span data-ttu-id="70b1c-182">Olá URL de aquisição de licença DRM.</span><span class="sxs-lookup"><span data-stu-id="70b1c-182">hello DRM license acquisition URL.</span></span>
* <span data-ttu-id="70b1c-183">Olá asset protocolo entrega (por exemplo, MPEG DASH, HLS, transmissão em fluxo uniforme ou todos).</span><span class="sxs-lookup"><span data-stu-id="70b1c-183">hello asset delivery protocol (for example, MPEG DASH, HLS, Smooth Streaming or all).</span></span>
* <span data-ttu-id="70b1c-184">tipo de Olá de encriptação dinâmica (neste caso, a encriptação comum).</span><span class="sxs-lookup"><span data-stu-id="70b1c-184">hello type of dynamic encryption (in this case, Common Encryption).</span></span>

<span data-ttu-id="70b1c-185">Para obter informações detalhadas, consulte [Configurar a política de entrega de elemento](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-185">For detailed information, see [Configure asset delivery policy ](media-services-rest-configure-asset-delivery-policy.md).</span></span>

## <span data-ttu-id="70b1c-186"><a id="create_locator"></a>Criar um OnDemand na ordem tooget um URL de transmissão em fluxo o localizador de transmissão em fluxo</span><span class="sxs-lookup"><span data-stu-id="70b1c-186"><a id="create_locator"></a>Create an OnDemand streaming locator in order tooget a streaming URL</span></span>
<span data-ttu-id="70b1c-187">Terá de tooprovide ao utilizador com Olá transmissão em fluxo de URL para uniforme, DASH ou HLS.</span><span class="sxs-lookup"><span data-stu-id="70b1c-187">You will need tooprovide your user with hello streaming URL for Smooth, DASH or HLS.</span></span>

> [!NOTE]
> <span data-ttu-id="70b1c-188">Se adicionar ou atualizar a sua política de entrega de elementos, tem de eliminar um localizador existente (se aplicável) e criar um novo localizador.</span><span class="sxs-lookup"><span data-stu-id="70b1c-188">If you add or update your asset’s delivery policy, you must delete an existing locator (if any) and create a new locator.</span></span>
>
>

<span data-ttu-id="70b1c-189">Para obter instruções sobre como ver toopublish um recurso e compilação um URL de transmissão em fluxo, [compilar um URL de transmissão em fluxo](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-189">For instructions on how toopublish an asset and build a streaming URL, see [Build a streaming URL](media-services-deliver-streaming-content.md).</span></span>

## <a name="get-a-test-token"></a><span data-ttu-id="70b1c-190">Obter um token de teste</span><span class="sxs-lookup"><span data-stu-id="70b1c-190">Get a test token</span></span>
<span data-ttu-id="70b1c-191">Obter um teste de token com base na restrição de token de Olá que foi utilizada para a política de autorização da chave de Olá.</span><span class="sxs-lookup"><span data-stu-id="70b1c-191">Get a test token based on hello token restriction that was used for hello key authorization policy.</span></span>

    // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
    // back into a TokenRestrictionTemplate class instance.
    TokenRestrictionTemplate tokenTemplate =
        TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

    // Generate a test token based on hello data in hello given TokenRestrictionTemplate.
    //hello GenerateTestToken method returns hello token without hello word “Bearer” in front
    //so you have tooadd it in front of hello token string.
    string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate);
    Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);


<span data-ttu-id="70b1c-192">Pode utilizar Olá [leitor AMS](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest sua transmissão em fluxo.</span><span class="sxs-lookup"><span data-stu-id="70b1c-192">You can use hello [AMS Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html) tootest your stream.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="70b1c-193">Criar e configurar um projeto de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="70b1c-193">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="70b1c-194">Configurar o ambiente de desenvolvimento e preencher o ficheiro de App. config Olá com as informações de ligação, conforme descrito em [desenvolvimento de Media Services com .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="70b1c-194">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="70b1c-195">Adicionar Olá demasiado os seguintes elementos**appSettings** definida no ficheiro App. config:</span><span class="sxs-lookup"><span data-stu-id="70b1c-195">Add hello following elements too**appSettings** defined in your app.config file:</span></span>

        <add key="Issuer" value="http://testacs.com"/>
        <add key="Audience" value="urn:test"/>

## <a name="example"></a><span data-ttu-id="70b1c-196">Exemplo</span><span class="sxs-lookup"><span data-stu-id="70b1c-196">Example</span></span>

<span data-ttu-id="70b1c-197">Olá exemplo seguinte demonstra a funcionalidade que foi introduzida no SDK de Media Services do Azure para .net-versão 3.5.2 (especificamente, Olá capacidade toodefine um Widevine modelo de licença e pedir uma licença Widevine a partir de Media Services do Azure).</span><span class="sxs-lookup"><span data-stu-id="70b1c-197">hello following sample demonstrates functionality that was introduced in Azure Media Services SDK for .Net -Version 3.5.2 (specifically, hello ability toodefine a Widevine license template and request a Widevine license from Azure Media Services).</span></span>

<span data-ttu-id="70b1c-198">Substitua o código de Olá no seu ficheiro Program.cs com o código de Olá apresentado nesta secção.</span><span class="sxs-lookup"><span data-stu-id="70b1c-198">Overwrite hello code in your Program.cs file with hello code shown in this section.</span></span>

>[!NOTE]
><span data-ttu-id="70b1c-199">Existe um limite de 1,000,000 políticas para diferentes políticas do AMS (por exemplo, para a política Locator ou ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="70b1c-199">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="70b1c-200">Deve utilizar Olá mesmo ID de política, se estiver a utilizar sempre Olá mesmo dias / permissões, por exemplo, políticas para os localizadores são tooremain pretendido no local durante muito tempo (políticas não carregamento) de acesso.</span><span class="sxs-lookup"><span data-stu-id="70b1c-200">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> <span data-ttu-id="70b1c-201">Para obter mais informações, veja [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.</span><span class="sxs-lookup"><span data-stu-id="70b1c-201">For more information, see [this](media-services-dotnet-manage-entities.md#limit-access-policies) topic.</span></span>

<span data-ttu-id="70b1c-202">Certifique-se tooupdate variáveis toopoint toofolders onde estão localizados os ficheiros de entrada.</span><span class="sxs-lookup"><span data-stu-id="70b1c-202">Make sure tooupdate variables toopoint toofolders where your input files are located.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using System.Threading;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization;
    using Microsoft.WindowsAzure.MediaServices.Client.DynamicEncryption;
    using Microsoft.WindowsAzure.MediaServices.Client.Widevine;
    using Newtonsoft.Json;

    namespace DynamicEncryptionWithDRM
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly Uri _sampleIssuer =
            new Uri(ConfigurationManager.AppSettings["Issuer"]);
        private static readonly Uri _sampleAudience =
            new Uri(ConfigurationManager.AppSettings["Audience"]);

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static readonly string _mediaFiles =
            Path.GetFullPath(@"../..\Media");

        private static readonly string _singleMP4File =
            Path.Combine(_mediaFiles, @"BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            bool tokenRestriction = false;
            string tokenTemplateString = null;

            IAsset asset = UploadFileAndCreateAsset(_singleMP4File);
            Console.WriteLine("Uploaded asset: {0}", asset.Id);

            IAsset encodedAsset = EncodeToAdaptiveBitrateMP4Set(asset);
            Console.WriteLine("Encoded asset: {0}", encodedAsset.Id);

            IContentKey key = CreateCommonTypeContentKey(encodedAsset);
            Console.WriteLine("Created key {0} for hello asset {1} ", key.Id, encodedAsset.Id);
            Console.WriteLine("PlayReady License Key delivery URL: {0}", key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense));
            Console.WriteLine();

            if (tokenRestriction)
            tokenTemplateString = AddTokenRestrictedAuthorizationPolicy(key);
            else
            AddOpenAuthorizationPolicy(key);

            Console.WriteLine("Added authorization policy: {0}", key.AuthorizationPolicyId);
            Console.WriteLine();

            CreateAssetDeliveryPolicy(encodedAsset, key);
            Console.WriteLine("Created asset delivery policy. \n");
            Console.WriteLine();

            if (tokenRestriction && !String.IsNullOrEmpty(tokenTemplateString))
            {
            // Deserializes a string containing an Xml representation of a TokenRestrictionTemplate
            // back into a TokenRestrictionTemplate class instance.
            TokenRestrictionTemplate tokenTemplate =
                TokenRestrictionTemplateSerializer.Deserialize(tokenTemplateString);

            // Generate a test token based on hello hello data in hello given TokenRestrictionTemplate.
            // Note, you need toopass hello key id Guid because we specified
            // TokenClaim.ContentKeyIdentifierClaim in during hello creation of TokenRestrictionTemplate.
            Guid rawkey = EncryptionUtils.GetKeyIdAsGuid(key.Id);
            string testToken = TokenRestrictionTemplateSerializer.GenerateTestToken(tokenTemplate, null, rawkey,
                                        DateTime.UtcNow.AddDays(365));
            Console.WriteLine("hello authorization token is:\nBearer {0}", testToken);
            Console.WriteLine();
            }

            // You can use hello http://amsplayer.azurewebsites.net/azuremediaplayer.html player tootest streams.
            // Note that DASH works on IE 11 (via PlayReady), Edge (via PlayReady), Chrome (via Widevine).

            string url = GetStreamingOriginLocator(encodedAsset);
            Console.WriteLine("Encrypted DASH URL: {0}/manifest(format=mpd-time-csf)", url);

            Console.ReadLine();
        }

        static public IAsset UploadFileAndCreateAsset(string singleFilePath)
        {
            if (!File.Exists(singleFilePath))
            {
            Console.WriteLine("File does not exist.");
            return null;
            }

            var assetName = Path.GetFileNameWithoutExtension(singleFilePath);
            IAsset inputAsset = _context.Assets.Create(assetName, AssetCreationOptions.None);

            var assetFile = inputAsset.AssetFiles.Create(Path.GetFileName(singleFilePath));

            Console.WriteLine("Created assetFile {0}", assetFile.Name);

            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading {0}", assetFile.Name);

            return inputAsset;
        }

        static public IAsset EncodeToAdaptiveBitrateMP4Set(IAsset inputAsset)
        {
            var encodingPreset = "Adaptive Streaming";

            IJob job = _context.Jobs.Create(String.Format("Encoding into Mp4 {0} too{1}",
                        inputAsset.Name,
                        encodingPreset));

            var mediaProcessors =
            _context.MediaProcessors.Where(p => p.Name.Contains("Media Encoder Standard")).ToList();

            var latestMediaProcessor =
            mediaProcessors.OrderBy(mp => new Version(mp.Version)).LastOrDefault();

            ITask encodeTask = job.Tasks.AddNew("Encoding", latestMediaProcessor, encodingPreset, TaskOptions.None);
            encodeTask.InputAssets.Add(inputAsset);
            encodeTask.OutputAssets.AddNew(String.Format("{0} as {1}", inputAsset.Name, encodingPreset), AssetCreationOptions.StorageEncrypted);

            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
            job.Submit();
            job.GetExecutionProgressTask(CancellationToken.None).Wait();

            return job.OutputMediaAssets[0];
        }


        static public IContentKey CreateCommonTypeContentKey(IAsset asset)
        {

            Guid keyId = Guid.NewGuid();
            byte[] contentKey = GetRandomBuffer(16);

            IContentKey key = _context.ContentKeys.Create(
                        keyId,
                        contentKey,
                        "ContentKey",
                        ContentKeyType.CommonEncryption);

            // Associate hello key with hello asset.
            asset.ContentKeys.Add(key);

            return key;
        }

        static public void AddOpenAuthorizationPolicy(IContentKey contentKey)
        {

            // Create ContentKeyAuthorizationPolicy with Open restrictions
            // and create authorization policy          

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Open",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.Open,
                    Requirements = null
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with no restrictions").
                Result;


            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);
            // Associate hello content key authorization policy with hello content key.
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;
        }

        public static string AddTokenRestrictedAuthorizationPolicy(IContentKey contentKey)
        {
            string tokenTemplateString = GenerateTokenRequirements();

            List<ContentKeyAuthorizationPolicyRestriction> restrictions = new List<ContentKeyAuthorizationPolicyRestriction>
                {
                new ContentKeyAuthorizationPolicyRestriction
                {
                    Name = "Token Authorization Policy",
                    KeyRestrictionType = (int)ContentKeyRestrictionType.TokenRestricted,
                    Requirements = tokenTemplateString,
                }
                };

            // Configure PlayReady and Widevine license templates.
            string PlayReadyLicenseTemplate = ConfigurePlayReadyLicenseTemplate();

            string WidevineLicenseTemplate = ConfigureWidevineLicenseTemplate();

            IContentKeyAuthorizationPolicyOption PlayReadyPolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.PlayReadyLicense,
                restrictions, PlayReadyLicenseTemplate);

            IContentKeyAuthorizationPolicyOption WidevinePolicy =
            _context.ContentKeyAuthorizationPolicyOptions.Create("Token option",
                ContentKeyDeliveryType.Widevine,
                restrictions, WidevineLicenseTemplate);

            IContentKeyAuthorizationPolicy contentKeyAuthorizationPolicy = _context.
                ContentKeyAuthorizationPolicies.
                CreateAsync("Deliver Common Content Key with token restrictions").
                Result;

            contentKeyAuthorizationPolicy.Options.Add(PlayReadyPolicy);
            contentKeyAuthorizationPolicy.Options.Add(WidevinePolicy);

            // Associate hello content key authorization policy with hello content key
            contentKey.AuthorizationPolicyId = contentKeyAuthorizationPolicy.Id;
            contentKey = contentKey.UpdateAsync().Result;

            return tokenTemplateString;
        }

        static private string GenerateTokenRequirements()
        {
            TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);

            template.PrimaryVerificationKey = new SymmetricVerificationKey();
            template.AlternateVerificationKeys.Add(new SymmetricVerificationKey());
            template.Audience = _sampleAudience.ToString();
            template.Issuer = _sampleIssuer.ToString();
            template.RequiredClaims.Add(TokenClaim.ContentKeyIdentifierClaim);

            return TokenRestrictionTemplateSerializer.Serialize(template);
        }

        static private string ConfigurePlayReadyLicenseTemplate()
        {
            // hello following code configures PlayReady License Template using .NET classes
            // and returns hello XML string.

            //hello PlayReadyLicenseResponseTemplate class represents hello template for hello response sent back toohello end user.
            //It contains a field for a custom data string between hello license server and hello application
            //(may be useful for custom app logic) as well as a list of one or more license templates.
            PlayReadyLicenseResponseTemplate responseTemplate = new PlayReadyLicenseResponseTemplate();

            // hello PlayReadyLicenseTemplate class represents a license template for creating PlayReady licenses
            // toobe returned toohello end users.
            //It contains hello data on hello content key in hello license and any rights or restrictions toobe
            //enforced by hello PlayReady DRM runtime when using hello content key.
            PlayReadyLicenseTemplate licenseTemplate = new PlayReadyLicenseTemplate();
            //Configure whether hello license is persistent (saved in persistent storage on hello client)
            //or non-persistent (only held in memory while hello player is using hello license).  
            licenseTemplate.LicenseType = PlayReadyLicenseType.Nonpersistent;

            // AllowTestDevices controls whether test devices can use hello license or not.  
            // If true, hello MinimumSecurityLevel property of hello license
            // is set too150.  If false (hello default), hello MinimumSecurityLevel property of hello license is set too2000.
            licenseTemplate.AllowTestDevices = true;

            // You can also configure hello Play Right in hello PlayReady license by using hello PlayReadyPlayRight class.
            // It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions
            // configured in hello license and on hello PlayRight itself (for playback specific policy).
            // Much of hello policy on hello PlayRight has toodo with output restrictions
            // which control hello types of outputs that hello content can be played over and
            // any restrictions that must be put in place when using a given output.
            // For example, if hello DigitalVideoOnlyContentRestriction is enabled,
            //then hello DRM runtime will only allow hello video toobe displayed over digital outputs
            //(analog video outputs won’t be allowed toopass hello content).

            //IMPORTANT: These types of restrictions can be very powerful but can also affect hello consumer experience.
            // If hello output protections are configured too restrictive,
            // hello content might be unplayable on some clients. For more information, see hello PlayReady Compliance Rules document.

            // For example:
            //licenseTemplate.PlayRight.AgcAndColorStripeRestriction = new AgcAndColorStripeRestriction(1);

            responseTemplate.LicenseTemplates.Add(licenseTemplate);

            return MediaServicesLicenseTemplateSerializer.Serialize(responseTemplate);
        }

        private static string ConfigureWidevineLicenseTemplate()
        {
            var template = new WidevineMessage
            {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                    new ContentKeySpecs
                    {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                    }
                },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
            };

            string configuration = JsonConvert.SerializeObject(template);
            return configuration;
        }

        static public void CreateAssetDeliveryPolicy(IAsset asset, IContentKey key)
        {
            // Get hello PlayReady license service URL.
            Uri acquisitionUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.PlayReadyLicense);

            // GetKeyDeliveryUrl for Widevine attaches hello KID toohello URL.
            // For example: https://amsaccount1.keydelivery.mediaservices.windows.net/Widevine/?KID=268a6dcb-18c8-4648-8c95-f46429e4927c.  
            // hello WidevineBaseLicenseAcquisitionUrl (used below) also tells Dynamaic Encryption
            // tooappend /? KID =< keyId > toohello end of hello url when creating hello manifest.
            // As a result Widevine license acquisition URL will have KID appended twice,
            // so we need tooremove hello KID that in hello URL when we call GetKeyDeliveryUrl.

            Uri widevineUrl = key.GetKeyDeliveryUrl(ContentKeyDeliveryType.Widevine);
            UriBuilder uriBuilder = new UriBuilder(widevineUrl);
            uriBuilder.Query = String.Empty;
            widevineUrl = uriBuilder.Uri;

            Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
            new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
            {
                    {AssetDeliveryPolicyConfigurationKey.PlayReadyLicenseAcquisitionUrl, acquisitionUrl.ToString()},
                    {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl, widevineUrl.ToString()}

            };

            // In this case we only specify Dash streaming protocol in hello delivery policy,
            // All other protocols will be blocked from streaming.
            var assetDeliveryPolicy = _context.AssetDeliveryPolicies.Create(
                "AssetDeliveryPolicy",
            AssetDeliveryPolicyType.DynamicCommonEncryption,
            AssetDeliveryProtocol.Dash,
            assetDeliveryPolicyConfiguration);


            // Add AssetDelivery Policy toohello asset
            asset.DeliveryPolicies.Add(assetDeliveryPolicy);

        }

        /// <summary>
        /// Gets hello streaming origin locator.
        /// </summary>
        /// <param name="assets"></param>
        /// <returns></returns>
        static public string GetStreamingOriginLocator(IAsset asset)
        {

            // Get a reference toohello streaming manifest file from hello  
            // collection of files in hello asset.

            var assetFile = asset.AssetFiles.Where(f => f.Name.ToLower().
                         EndsWith(".ism")).
                         FirstOrDefault();

            // Create a 30-day readonly access policy.
            IAccessPolicy policy = _context.AccessPolicies.Create("Streaming policy",
            TimeSpan.FromDays(30),
            AccessPermissions.Read);

            // Create a locator toohello streaming content on an origin.
            ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
            policy,
            DateTime.UtcNow.AddMinutes(-5));

            // Create a URL toohello manifest file.
            return originLocator.Path + assetFile.Name;
        }

        static private void JobStateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine(string.Format("{0}\n  State: {1}\n  Time: {2}\n\n",
            ((IJob)sender).Name,
            e.CurrentState,
            DateTime.UtcNow.ToString(@"yyyy_M_d__hh_mm_ss")));
        }

        static private byte[] GetRandomBuffer(int length)
        {
            var returnValue = new byte[length];

            using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
            {
            rng.GetBytes(returnValue);
            }

            return returnValue;
        }
        }
    }


## <a name="next-step"></a><span data-ttu-id="70b1c-203">Passo seguinte</span><span class="sxs-lookup"><span data-stu-id="70b1c-203">Next step</span></span>
<span data-ttu-id="70b1c-204">Rever os percursos de aprendizagem dos Serviços de Multimédia</span><span class="sxs-lookup"><span data-stu-id="70b1c-204">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="70b1c-205">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="70b1c-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="70b1c-206">Consultar também</span><span class="sxs-lookup"><span data-stu-id="70b1c-206">See also</span></span>
[<span data-ttu-id="70b1c-207">CENC com Múltipla DRM e Controlo de Acesso</span><span class="sxs-lookup"><span data-stu-id="70b1c-207">CENC with Multi-DRM and Access Control</span></span>](media-services-cenc-with-multidrm-access-control.md)

[<span data-ttu-id="70b1c-208">Configurar empacotamento Widevine com AMS</span><span class="sxs-lookup"><span data-stu-id="70b1c-208">Configure Widevine packaging with AMS</span></span>](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services)

[<span data-ttu-id="70b1c-209">Anunciar os serviços de entrega de licença Widevine da Google nos Serviços de Multimédia do Azure</span><span class="sxs-lookup"><span data-stu-id="70b1c-209">Announcing Google Widevine license delivery services in Azure Media Services</span></span>](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/)
