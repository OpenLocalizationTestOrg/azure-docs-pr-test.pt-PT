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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Incorporar um vídeo de transmissão em fluxo adaptável MPEG-DASH numa aplicação HTML5 com DASH.js
## <a name="overview"></a>Descrição geral
MPEG-DASH é uma norma ISO para Olá adaptável de transmissão em fluxo de conteúdo de vídeo, que oferece vantagens significativas para aqueles que queira as vídeo de alta qualidade, adaptável de toodeliver transmissão em fluxo de saída. Com MPEG-DASH, transmissão Olá irá automaticamente remover a definição inferior tooa quando rede Olá fique congestionada. Isto reduz a probabilidade de Olá do Visualizador de Olá enquanto transfere de leitor de Olá Olá alguns tooplay de segundos (também conhecido como colocação em memória intermédia) junto a ver um vídeo "em pausa". Como reduz o congestionamento de rede, o leitor de vídeo Olá devolverá por sua vez tooa fluxo de qualidade superior. Esta capacidade tooadapt Olá largura de banda da necessário também resulta numa hora de início rápida de vídeo. Que significa que Olá primeiro alguns segundos pode ser reproduzida num segmento qualidade inferior fast para transferência e, em seguida, passo segurança qualidade superior tooa assim que o conteúdo suficiente tem foi colocado na memória intermédia.

Dash.js é um código aberto MPEG-DASH leitor de vídeo escrito em JavaScript. O objetivo é tooprovide um leitor robusto, entre plataformas que pode ser livremente reutilizado em aplicações que necessitam de reprodução de vídeo. Fornece reprodução de MPEG-DASH em qualquer browser que suporte Olá W3C suporte de dados de origem extensões (MSE), hoje em dia ou seja Chrome, Microsoft Edge e IE11 (noutros browsers indicou as respetivas toosupport intenção MSE). Para mais informações sobre DASH.js, js Consulte repositório de dash.js Olá GitHub.

## <a name="creating-a-browser-based-streaming-video-player"></a>Criar um leitor de vídeo transmissão em fluxo com base no browser
toocreate uma página web simples que apresenta um leitor de vídeo com Olá esperado controla como um play, colocar em pausa, rewind etc., precisa de:

1. Criar uma página HTML
2. Adicionar Olá etiqueta de vídeo
3. Adicionar o leitor de dash.js Olá
4. Inicializar o leitor de Olá
5. Adicionar alguns estilo CSS
6. Ver os resultados de Olá num browser que implementa MSE

Leitor de Olá inicialização pode ser concluída em apenas alguns a linhas de código JavaScript. Utilizar dash.js, é realmente esse vídeo tooembed simples MPEG-DASH nas suas aplicações baseadas no browser.

## <a name="creating-hello-html-page"></a>Criar Olá página HTML
Step-by-Olá primeiro passo é a página de toocreate um padrão HTML que contém Olá **vídeo** elemento, guarde este ficheiro como basicPlayer.html, como o seguinte exemplo de Olá ilustra:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Adicionar Olá DASH.js leitor
tooadd Olá dash.js implementação toohello aplicação de referência, terá de ficheiro de dash.all.js Olá toograb da versão de Olá 1.0 do projeto dash.js. Este deve ser guardado na pasta de JavaScript Olá da sua aplicação. Este ficheiro é um ficheiro de conveniência que obtém em conjunto todo o código necessário dash.js Olá num único ficheiro. Se tiver um aspeto em torno do repositório de dash.js Olá, irá determinar Olá ficheiros individuais, testar código e muito mais, mas se todos os quiser toodo está dash.js de utilização, em seguida, ficheiros de dash.all.js Olá é o que precisa.

aplicações do tooadd Olá dash.js leitor tooyour, adicionar uma script toohello head secção de etiquetas de basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Em seguida, crie um leitor de Olá tooinitialize função quando carrega a página Olá. Adicione Olá seguinte script depois de linha de Olá na qual carrega dash.all.js:

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

Esta função cria um DashContext pela primeira vez. Este é utilizado tooconfigure Olá aplicação para um ambiente específico de tempo de execução. Do ponto de vista técnico, define Olá classes Olá framework de injeção de dependência devem utilizar ao construir a aplicação Olá. Na maioria dos casos, irá utilizar Dash.di.DashContext.

Em seguida, instanciar a classe principal do Olá do framework de dash.js Olá, MediaPlayer. Esta classe contém core Olá métodos necessários, tal como reproduzir e colocar em pausa, gere relação Olá com o elemento de vídeo Olá e também interpretação Olá do ficheiro de descrição de apresentação de suporte de dados (MPD) Olá que descreve toobe vídeo Olá reproduzido.

função de startup() Olá de Olá MediaPlayer classe é chamada tooensure esse player Olá está pronto tooplay de vídeo. Entre outras coisas esta função assegura que todas as classes de necessário Olá (conforme definido pelo contexto Olá) foram carregadas. Depois de leitor de Olá estiver pronto, pode anexar Olá elemento de vídeo tooit utilizando Olá attachView() função. Isto permite Olá MediaPlayer tooinject Olá transmissão num elemento de Olá e também controlar reprodução conforme necessário.

Transmita o URL de Olá de Olá MPD ficheiro toohello MediaPlayer para que o se conhece Olá vídeo é esperado tooplay.hello setupVideo() função acabou de criar terá toobe executado assim que a página Olá totalmente carregou. Fazê-lo utilizando o evento de onload Olá do elemento de corpo de Olá. Alterar o <body> elemento:

    <body onload="setupVideo()">

Finalmente, defina o tamanho de Olá do elemento de vídeo Olá utilizando CSS. Num ambiente de transmissão em fluxo adaptável, isto é especialmente importante porque o tamanho de Olá de vídeo a ser reproduzido Olá pode alterar como reprodução feita toochanging condições de rede. Nesta demonstração simple simplesmente forçar Olá elemento de vídeo toobe 80% da janela do browser disponíveis de Olá adicionando Olá CSS toohello head secção página Olá os seguintes:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Reproduzir um vídeo
tooplay um vídeo, o browser no ficheiro de basicPlayback.html Olá apontar e clique em play no leitor de vídeo Olá apresentado.

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Veja Também
[Desenvolver aplicações de leitor de vídeo](media-services-develop-video-players.md)

[Repositório do GitHub dash.js](https://github.com/Dash-Industry-Forum/dash.js) 

