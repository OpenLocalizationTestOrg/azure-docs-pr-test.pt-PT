---
title: "aaaEmbedding um MPEG-DASH adaptável de transmissão em fluxo vídeo numa aplicação HTML5 com DASH.js | Microsoft Docs"
description: "Este tópico demonstra como tooembed um MPEG-DASH adaptável de transmissão em fluxo vídeo numa aplicação com DASH.js HTML5."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="fab09-103">Incorporar um vídeo de transmissão em fluxo adaptável MPEG-DASH numa aplicação HTML5 com DASH.js</span><span class="sxs-lookup"><span data-stu-id="fab09-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="fab09-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="fab09-104">Overview</span></span>
<span data-ttu-id="fab09-105">MPEG-DASH é uma norma ISO para Olá adaptável de transmissão em fluxo de conteúdo de vídeo, que oferece vantagens significativas para aqueles que queira as vídeo de alta qualidade, adaptável de toodeliver transmissão em fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="fab09-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="fab09-106">Com MPEG-DASH, transmissão Olá irá automaticamente remover a definição inferior tooa quando rede Olá fique congestionada.</span><span class="sxs-lookup"><span data-stu-id="fab09-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="fab09-107">Isto reduz a probabilidade de Olá do Visualizador de Olá enquanto transfere de leitor de Olá Olá alguns tooplay de segundos (também conhecido como colocação em memória intermédia) junto a ver um vídeo "em pausa".</span><span class="sxs-lookup"><span data-stu-id="fab09-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="fab09-108">Como reduz o congestionamento de rede, o leitor de vídeo Olá devolverá por sua vez tooa fluxo de qualidade superior.</span><span class="sxs-lookup"><span data-stu-id="fab09-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="fab09-109">Esta capacidade tooadapt Olá largura de banda da necessário também resulta numa hora de início rápida de vídeo.</span><span class="sxs-lookup"><span data-stu-id="fab09-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="fab09-110">Que significa que Olá primeiro alguns segundos pode ser reproduzida num segmento qualidade inferior fast para transferência e, em seguida, passo segurança qualidade superior tooa assim que o conteúdo suficiente tem foi colocado na memória intermédia.</span><span class="sxs-lookup"><span data-stu-id="fab09-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="fab09-111">Dash.js é um código aberto MPEG-DASH leitor de vídeo escrito em JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fab09-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="fab09-112">O objetivo é tooprovide um leitor robusto, entre plataformas que pode ser livremente reutilizado em aplicações que necessitam de reprodução de vídeo.</span><span class="sxs-lookup"><span data-stu-id="fab09-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="fab09-113">Fornece reprodução de MPEG-DASH em qualquer browser que suporte Olá W3C suporte de dados de origem extensões (MSE), hoje em dia ou seja Chrome, Microsoft Edge e IE11 (noutros browsers indicou as respetivas toosupport intenção MSE).</span><span class="sxs-lookup"><span data-stu-id="fab09-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="fab09-114">Para mais informações sobre DASH.js, js Consulte repositório de dash.js Olá GitHub.</span><span class="sxs-lookup"><span data-stu-id="fab09-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="fab09-115">Criar um leitor de vídeo transmissão em fluxo com base no browser</span><span class="sxs-lookup"><span data-stu-id="fab09-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="fab09-116">toocreate uma página web simples que apresenta um leitor de vídeo com Olá esperado controla como um play, colocar em pausa, rewind etc., precisa de:</span><span class="sxs-lookup"><span data-stu-id="fab09-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="fab09-117">Criar uma página HTML</span><span class="sxs-lookup"><span data-stu-id="fab09-117">Create an HTML page</span></span>
2. <span data-ttu-id="fab09-118">Adicionar Olá etiqueta de vídeo</span><span class="sxs-lookup"><span data-stu-id="fab09-118">Add hello video tag</span></span>
3. <span data-ttu-id="fab09-119">Adicionar o leitor de dash.js Olá</span><span class="sxs-lookup"><span data-stu-id="fab09-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="fab09-120">Inicializar o leitor de Olá</span><span class="sxs-lookup"><span data-stu-id="fab09-120">Initialize hello player</span></span>
5. <span data-ttu-id="fab09-121">Adicionar alguns estilo CSS</span><span class="sxs-lookup"><span data-stu-id="fab09-121">Add some CSS style</span></span>
6. <span data-ttu-id="fab09-122">Ver os resultados de Olá num browser que implementa MSE</span><span class="sxs-lookup"><span data-stu-id="fab09-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="fab09-123">Leitor de Olá inicialização pode ser concluída em apenas alguns a linhas de código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fab09-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="fab09-124">Utilizar dash.js, é realmente esse vídeo tooembed simples MPEG-DASH nas suas aplicações baseadas no browser.</span><span class="sxs-lookup"><span data-stu-id="fab09-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="fab09-125">Criar Olá página HTML</span><span class="sxs-lookup"><span data-stu-id="fab09-125">Creating hello HTML Page</span></span>
<span data-ttu-id="fab09-126">Step-by-Olá primeiro passo é a página de toocreate um padrão HTML que contém Olá **vídeo** elemento, guarde este ficheiro como basicPlayer.html, como o seguinte exemplo de Olá ilustra:</span><span class="sxs-lookup"><span data-stu-id="fab09-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="fab09-127">Adicionar Olá DASH.js leitor</span><span class="sxs-lookup"><span data-stu-id="fab09-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="fab09-128">tooadd Olá dash.js implementação toohello aplicação de referência, terá de ficheiro de dash.all.js Olá toograb da versão de Olá 1.0 do projeto dash.js.</span><span class="sxs-lookup"><span data-stu-id="fab09-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="fab09-129">Este deve ser guardado na pasta de JavaScript Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="fab09-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="fab09-130">Este ficheiro é um ficheiro de conveniência que obtém em conjunto todo o código necessário dash.js Olá num único ficheiro.</span><span class="sxs-lookup"><span data-stu-id="fab09-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="fab09-131">Se tiver um aspeto em torno do repositório de dash.js Olá, irá determinar Olá ficheiros individuais, testar código e muito mais, mas se todos os quiser toodo está dash.js de utilização, em seguida, ficheiros de dash.all.js Olá é o que precisa.</span><span class="sxs-lookup"><span data-stu-id="fab09-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="fab09-132">aplicações do tooadd Olá dash.js leitor tooyour, adicionar uma script toohello head secção de etiquetas de basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="fab09-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="fab09-133">Em seguida, crie um leitor de Olá tooinitialize função quando carrega a página Olá.</span><span class="sxs-lookup"><span data-stu-id="fab09-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="fab09-134">Adicione Olá seguinte script depois de linha de Olá na qual carrega dash.all.js:</span><span class="sxs-lookup"><span data-stu-id="fab09-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

<span data-ttu-id="fab09-135">Esta função cria um DashContext pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="fab09-135">This function first creates a DashContext.</span></span> <span data-ttu-id="fab09-136">Este é utilizado tooconfigure Olá aplicação para um ambiente específico de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="fab09-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="fab09-137">Do ponto de vista técnico, define Olá classes Olá framework de injeção de dependência devem utilizar ao construir a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="fab09-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="fab09-138">Na maioria dos casos, irá utilizar Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="fab09-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="fab09-139">Em seguida, instanciar a classe principal do Olá do framework de dash.js Olá, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="fab09-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="fab09-140">Esta classe contém core Olá métodos necessários, tal como reproduzir e colocar em pausa, gere relação Olá com o elemento de vídeo Olá e também interpretação Olá do ficheiro de descrição de apresentação de suporte de dados (MPD) Olá que descreve toobe vídeo Olá reproduzido.</span><span class="sxs-lookup"><span data-stu-id="fab09-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="fab09-141">função de startup() Olá de Olá MediaPlayer classe é chamada tooensure esse player Olá está pronto tooplay de vídeo.</span><span class="sxs-lookup"><span data-stu-id="fab09-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="fab09-142">Entre outras coisas esta função assegura que todas as classes de necessário Olá (conforme definido pelo contexto Olá) foram carregadas.</span><span class="sxs-lookup"><span data-stu-id="fab09-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="fab09-143">Depois de leitor de Olá estiver pronto, pode anexar Olá elemento de vídeo tooit utilizando Olá attachView() função.</span><span class="sxs-lookup"><span data-stu-id="fab09-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="fab09-144">Isto permite Olá MediaPlayer tooinject Olá transmissão num elemento de Olá e também controlar reprodução conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="fab09-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="fab09-145">Transmita o URL de Olá de Olá MPD ficheiro toohello MediaPlayer para que o se conhece Olá vídeo é esperado tooplay.hello setupVideo() função acabou de criar terá toobe executado assim que a página Olá totalmente carregou.</span><span class="sxs-lookup"><span data-stu-id="fab09-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="fab09-146">Fazê-lo utilizando o evento de onload Olá do elemento de corpo de Olá.</span><span class="sxs-lookup"><span data-stu-id="fab09-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="fab09-147">Alterar o <body> elemento:</span><span class="sxs-lookup"><span data-stu-id="fab09-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="fab09-148">Finalmente, defina o tamanho de Olá do elemento de vídeo Olá utilizando CSS.</span><span class="sxs-lookup"><span data-stu-id="fab09-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="fab09-149">Num ambiente de transmissão em fluxo adaptável, isto é especialmente importante porque o tamanho de Olá de vídeo a ser reproduzido Olá pode alterar como reprodução feita toochanging condições de rede.</span><span class="sxs-lookup"><span data-stu-id="fab09-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="fab09-150">Nesta demonstração simple simplesmente forçar Olá elemento de vídeo toobe 80% da janela do browser disponíveis de Olá adicionando Olá CSS toohello head secção página Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fab09-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="fab09-151">Reproduzir um vídeo</span><span class="sxs-lookup"><span data-stu-id="fab09-151">Playing a Video</span></span>
<span data-ttu-id="fab09-152">tooplay um vídeo, o browser no ficheiro de basicPlayback.html Olá apontar e clique em play no leitor de vídeo Olá apresentado.</span><span class="sxs-lookup"><span data-stu-id="fab09-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fab09-153">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="fab09-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fab09-154">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="fab09-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="fab09-155">Veja Também</span><span class="sxs-lookup"><span data-stu-id="fab09-155">See Also</span></span>
[<span data-ttu-id="fab09-156">Desenvolver aplicações de leitor de vídeo</span><span class="sxs-lookup"><span data-stu-id="fab09-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="fab09-157">Repositório do GitHub dash.js</span><span class="sxs-lookup"><span data-stu-id="fab09-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

