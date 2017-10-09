---
title: Tutoriais de fluxo de trabalho do suporte de dados codificador Premium aaaAvanced
description: "Este documento contém instruções que mostram como tooperform avançadas tarefas com o fluxo de trabalho do suporte de dados codificador Premium e também como toocreate complexas os fluxos de trabalho com o estruturador de fluxo de trabalho."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Tutoriais de fluxo de trabalho do suporte de dados codificador Premium avançadas
## <a name="overview"></a>Descrição geral
Este documento contém instruções que mostram como toocustomize fluxos de trabalho com **estruturador de fluxo de trabalho**. Pode encontrar os ficheiros de fluxo de trabalho real Olá [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>TOC
é abrangido Olá os seguintes tópicos:

* [Codificação MXF para uma MP4 de velocidade de transmissão única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Iniciar um novo fluxo de trabalho](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Utilizar Olá entrada de ficheiro do suporte de dados](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [A inspecionar os fluxos de suporte de dados](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Um codificador vídeo para a adicionar. Geração de ficheiros MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Sequência de áudio Olá codificação](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Multiplexação fluxos de áudio e vídeo para um contentor de MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Escrever Olá MP4 o ficheiro](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Criar um recurso de serviços de suporte de dados a partir do ficheiro de saída de Olá](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Olá do teste concluído o fluxo de trabalho localmente](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Codificação MXF para multibitrate MP4s - empacotamento dinâmico ativado](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Adicionar um ou mais saídas MP4 adicionais](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Configurar nomes de saída do ficheiro de Olá](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Adicionar um registo de áudio separada](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Adicionar Olá. ISM SMIL ficheiro](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Codificação MXF para multibitrate MP4 - blueprint avançada](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Tooenhance de descrição geral do fluxo de trabalho](#workflow-overview-to-enhance)
  * [As convenções de nomenclatura de ficheiros](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Publicação de propriedades do componente na raiz do fluxo de trabalho de Olá](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Ter gerado o ficheiro de saída nomes baseiam-se nos valores de propriedade publicada](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Adicionar a saída de MP4 toomultibitrate de miniaturas](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Miniaturas de tooadd de descrição geral de fluxo de trabalho para](#workflow-overview-to-add-thumbnails-to)
  * [Adicionar JPG codificação](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Lidar com a conversão de espaço de cor](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Miniaturas de Olá de escrita](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Detetar erros num fluxo de trabalho](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Fluxo de trabalho concluído](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Corte de baseados no tempo de mensagens em fila de saída multibitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Fluxo de trabalho descrição geral toostart corte para a adicionar](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Utilizar Olá Trimmer de fluxo](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Fluxo de trabalho concluído](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Introdução ao hello componente convertidos em script](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Script num fluxo de trabalho: Olá, mundo](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Com base no período de corte de saída multibitrate MP4](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Blueprint corte para a adição de toostart de descrição geral](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Olá Clip lista XML a utilizar](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Lista de clip Olá modificação de um componente convertidos em script](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Adicionar uma propriedade de conveniência ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Codificação MXF para uma MP4 de velocidade de transmissão única
Esta explicação passo a passo, vamos criar uma velocidade de transmissão única. Ficheiro MP4 com AAC Putador codificado áudio de um. Ficheiro de entrada MXF.

### <a id="MXF_to_MP4_start_new"></a>Iniciar um novo fluxo de trabalho
Abra o estruturador de fluxo de trabalho e selecione "Blueprint de transcodificar o ficheiro"-"nova área de trabalho"-""

novo fluxo de trabalho Olá mostrará 3 elementos:

* Ficheiro de origem principal
* Lista de clip XML
* Ficheiro/elemento de saída  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Novo fluxo de trabalho de codificação*

### <a id="MXF_to_MP4_with_file_input"></a>Utilizar Olá entrada de ficheiro do suporte de dados
Na ordem tooaccept nossa ficheiros de suporte de dados de entrada, um começa com a adição de um componente de entrada de ficheiro do suporte de dados. tooadd um fluxo de trabalho de toohello do componente, procure na caixa de pesquisa do repositório de Olá e arraste a entrada de Olá pretendido para Painel estruturador Olá. Fazê-lo para Olá entrada de ficheiro do suporte de dados e ligue Olá ficheiro de origem principal componente toohello Filename entrada pin do Olá entrada de ficheiro do suporte de dados.

![Entrada de ficheiros de multimédia ligados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Entrada de ficheiros de multimédia ligados*

Antes de podermos fazer muito mais, primeiro precisamos estruturador de fluxo de trabalho de toohello tooindicate o ficheiro de exemplo Gostaríamos toouse toodesign nosso fluxo de trabalho com. toodo por isso, clique em segundo plano do estruturador do painel de Olá e procure a propriedade de ficheiro de origem principal Olá no painel da direita de propriedade de Olá. Clique em ícone da pasta Olá e selecione Olá pretendido ficheiro tootest Olá fluxo de trabalho com. Assim que isto é feito, o componente de entrada de ficheiro do suporte de dados de Olá inspecionar o ficheiro de Olá e preencher os respetivos pins tooreflect Olá Ficheirodesaída-inspecioná-los.

![Entrada do ficheiro de multimédia preenchidas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Entrada do ficheiro de multimédia preenchidas*

Enquanto esta ação Especifica com que a entrada de que Gostaríamos toowork com, não indica ainda onde a saída de Olá codificado deve aceda a. Semelhante toohow Olá, que foi configurado, o ficheiro de origem principal agora configurar Olá propriedade da variável de pasta de saída, imediatamente abaixo do mesmo.

![Propriedades de entrada e saída configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Propriedades de entrada e saída configuradas*

### <a id="MXF_to_MP4_streams"></a>A inspecionar os fluxos de suporte de dados
Muitas vezes, se pretendido tooknow aspeto como nesse fluxo Olá flui através do fluxo de trabalho Olá. tooinspect uma transmissão em fluxo em qualquer ponto num fluxo de trabalho Olá, basta clicar uma saída ou entrada pin em qualquer um dos componentes de Olá. Neste caso, tente clicar no pin de saída de vídeo descomprimidos Olá do nosso entrada de ficheiro do suporte de dados. Uma caixa de diálogo abre-se que permite as vídeo de saída de Olá tooinspect.

![A inspecionar o pin de saída de vídeo descomprimidos Olá](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*A inspecionar o pin de saída de vídeo descomprimidos Olá*

No nosso caso, indica-nos por exemplo, está a lidar com uma entrada de 1920 x 1080 em 24 fotogramas por segundo em 4: amostragem de 2:2 para um vídeo de quase 2 minutos.

### <a id="MXF_to_MP4_file_generation"></a>Um codificador vídeo para a adicionar. Geração de ficheiros MP4
Tenha em atenção que agora, um vídeo descomprimidos e vários pins de saída de áudio descomprimidos estão disponíveis para utilização no nosso entrada de ficheiro do suporte de dados. Na ordem tooencode Olá as vídeo de entrada, precisamos de um componente de codificação - neste caso, para a geração. Ficheiros MP4.

tooencode Olá tooH.264 de fluxo de vídeo, adicione a superfície de toohello de componente codificador vídeo AVC do Olá designer. Este componente assume um fluxo de vídeo uncompress como entrada e disponibiliza um AVC de fluxo de vídeo comprimido no respetivo pin de saída.

![Codificador de AVC desligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Codificador de AVC desligado*

As respetivas propriedades determinam como exatamente Olá codificação ocorre. Vamos tem uma vista de olhos algumas das Olá definições mais importantes:

* Largura de saída e a altura de saída: determinam estes resolução Olá de vídeo Olá codificado. No nosso caso, vamos com 640 x 360
* Velocidade de fotogramas: quando toopassthrough conjunto irá apenas adotar velocidade de fotogramas da origem Olá, é possível toooverride neste apesar. Tenha em atenção que essas conversão framerate não é movimento-compensada.
* Perfil e nível: estes determinam que perfil de Olá AVC e nível. tooconveniently obter mais informações sobre os diferentes níveis de Olá e perfis, clique no ícone de ponto de interrogação Olá no componente de codificador de vídeo AVC Olá e página de ajuda de Olá irá mostrar mais detalhes sobre cada um dos níveis de Olá. Para o nosso exemplo, vamos com perfil principal ao nível 3.2 (predefinição Olá).
* Taxa de modo de controlo e velocidade de transmissão (kbps): no nosso cenário, optar por uma constante de velocidade de transmissão (CBR) de saída em 1200 kbps
* Formato de vídeo: trata sobre Olá VUI (informações de utilização de vídeo) que obtém escrito no fluxo de 264 Olá (informações de lado que podem ser utilizadas por uma apresentação do descodificador tooenhance Olá, mas não essencial toocorrectly descodificar):
* NTSC (típico para EUA ou Japão, utilizando 30 fps)
* PAL (típico para a Europa, utilizando 25 fps)
* Modo de dimensionamento GOP: irá ser configurado de tamanho fixo GOP para a nossa fins com uma chave de intervalo de 2 segundos com GOPs fechado. Isto garante a compatibilidade com Olá que fornece de Media Services do Azure empacotamento dinâmico.

toofeed codificador nosso AVC, ligar o pin de saída de vídeo descomprimidos Olá de Olá entrada de ficheiro do suporte de dados componente toohello as vídeo descomprimidos entrada pin do codificador Olá AVC.

![Codificador de AVC ligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Codificador de AVC principal ligado*

### <a id="MXF_to_MP4_audio"></a>Sequência de áudio Olá codificação
Neste momento, estamos ter codificado vídeo, mas sequência de áudio descomprimidos original Olá ainda tem toobe comprimido. Para este podemos irá aceder com AAC codificação por Olá componente AAC codificador (Dolby). Adicione fluxo de trabalho toohello.

![Codificador de AVC desligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Codificador AAC desligado*

Agora é não existe uma incompatibilidade: há apenas um único descomprimido áudio entrado pin do Olá AAC codificador enquanto mais do que provavelmente Olá de entrada de ficheiro do suporte de dados terá dois diferentes descomprimidos disponível de sequência de áudio: um para Olá deixado de canal de áudio e outro para Olá direito. (Se estiver a lidar com surround som, que é 6 canais). Por isso não é possível toodirectly ligar áudio Olá a partir da origem de entrada de ficheiro do suporte de dados de Olá no codificador de áudio Olá AAC. Olá componente AAC espera que uma sequência de áudio "intercalada" so-called: um fluxo único que tem ambos Olá à esquerda e Olá canais direita interleaved entre si. Depois de sabemos da nossa ficheiros de suporte de dados de origem que controla áudio em que posição na origem de Olá, iremos pode gerar essa sequência de áudio intercalada com Olá corretamente atribuídos posições de orador para a esquerda e direita.

Primeiro uma melhor toogenerated um fluxo de canais de áudio Olá necessário origem intercalado. componente de áudio fluxo Interleaver Olá irá processar esta-nos. Adicionar fluxo de trabalho toohello e ligue saídas de áudio Olá de Olá entrada de ficheiro do suporte de dados para a mesma.

![Ligado Interleaver de sequência de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Ligado Interleaver de sequência de áudio*

Agora que temos uma sequência de áudio intercalada, mas ainda não especificou um onde orador relativos à esquerda ou direita do Olá tooassign posições a. Ordenar toospecify isto, iremos pode tirar partido das Olá orador posição Assigner.

![Adicionar um Assigner de posição de orador](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Adicionar um Assigner de posição de orador*

Configurar Olá orador posição Assigner para utilização com um fluxo de entrada stereo através de um filtro de configuração predefinida de codificador de "Personalizada" e Olá canal predefinido denominado "2.0 (L, R)". (Isto irá atribuir Olá orador esquerdo posição toochannel 1 e Olá orador direita posição toochannel 2.)

Ligar a saída de Olá da entrada de toohello de orador posição Assigner Olá de Olá AAC codificador. Em seguida, informar Olá AAC codificador toowork com um "2.0 (L, R)" canal da configuração predefinida, para que confie toodeal com stereo áudio como entrada.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexação fluxos de áudio e vídeo para um contentor de MP4
Fornecido nosso AVC codificado de transmissão e a nossa AAC codificado sequência de áudio, iremos pode capturar ambos para uma. Contentor de MP4. processo de Olá de combinar vários fluxos para um único é denominado "multiplexação" (ou "muxing"). Neste caso, iremos estiver a interleaving áudio Olá e fluxos de vídeo Olá numa única coherent. Pacote MP4. componente de Olá que coordena isto para um. Contentor de MP4 é designado por Olá Multiplexer ISO MPEG-4. Adicione uma superfície do designer toohello e ligar Olá AVC vídeo codificador e entradas de tooits Olá AAC codificador.

![Ligado MPEG4 Multiplexer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Ligado MPEG4 Multiplexer*

### <a id="MXF_to_MP4_writing_mp4"></a>Escrever Olá MP4 o ficheiro
Ao escrever um ficheiro de saída, é utilizado o componente de saída do ficheiro de Olá. Iremos pode ligar este resultado toohello Olá ISO MPEG-4 Multiplexer para que o resultado obtém escrito toodisk. toodo, ligar Olá contentor (MPEG-4) saída pin toohello escrita entrada pin de Olá ficheiro de saída.

![Ligado a saída do ficheiro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Ligado a saída do ficheiro*

Olá filename que será utilizado é determinado pelo Olá propriedade de ficheiro. Embora essa propriedade pode ser tooa codificado deu um valor, provavelmente um convém tooset-lo através de uma expressão em vez disso.

o fluxo de trabalho do toohave Olá determinar automaticamente saída Olá propriedade de nome de uma expressão de ficheiros, clique em Olá buton seguinte toohello nome do ficheiro (ícone da pasta toohello seguinte). De Olá menu pendente, em seguida, selecione "Expressão". Editor de expressão Olá será apresentada. Limpe conteúdo Olá do editor de Olá primeiro.

![Editor de expressão vazia](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Editor de expressão vazia*

editor de expressão Olá permite tooenter qualquer valor literal, misturada com uma ou mais variáveis. As variáveis de começar com uma cifrão. Como acessos chave de $ Olá, o editor de Olá irá mostrar uma caixa de lista pendente com uma opção de variáveis disponíveis. No nosso caso utilizaremos uma combinação de variável de diretório de saída Olá e a variável de nome de ficheiro de entrada base Olá:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Preenchido fora do Editor de expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Preenchido fora do Editor de expressão*

> [!NOTE]
> Ordem toosee ver um ficheiro de saída da tarefa codificação no Azure, tem de fornecer um valor no editor de expressão Olá.
>
>

Quando o utilizador confirma expressão Olá por atingir ok, janela de propriedade Olá será pré-visualize toowhat valor Olá ficheiro propriedade resolve neste ponto no tempo.

![Expressão de ficheiro resolve dir de saída](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*Expressão de ficheiro resolve dir de saída*

### <a id="MXF_to_MP4_asset_from_output"></a>Criar um recurso de serviços de suporte de dados a partir do ficheiro de saída de Olá
Enquanto é escrever um ficheiro de saída MP4, ainda temos tooindicate que este ficheiro pertence toohello de saída do recurso de que os media services irão gerar como resultado de executar este fluxo de trabalho. toothis final, o nó de elemento/ficheiro de saída de Olá na tela de fluxo de trabalho de Olá é utilizado. Todos os ficheiros de entrada para este nó fará parte do recurso de Media Services do Azure resultante Olá.

Ligar Olá ficheiro saída componente toohello ficheiro/elemento de saída componente toofinish Olá fluxo de trabalho.

![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Fluxo de trabalho concluído*

### <a id="MXF_to_MP4_test"></a>Olá do teste concluído o fluxo de trabalho localmente
tootest Olá fluxo de trabalho localmente, atingiu o botão de reproduzir Olá na barra de ferramentas de Olá na parte superior do Olá. Quando o fluxo de trabalho Olá concluído executar, Inspecione saída Olá criada na pasta de saída Olá configurado. Verá Olá terminou o ficheiro de saída MP4 codificado do ficheiro de origem de entrada de MXF Olá.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Codificação MXF em MP4 - multibitrate empacotamento dinâmico ativado
Esta explicação passo a passo vamos criar um conjunto de vários ficheiros MP4 de velocidade de transmissão com AAC codificado áudio de um único. Ficheiro de entrada MXF.

Quando uma saída de elemento de transmissão múltipla for pretendida para utilização em combinação com funcionalidades de empacotamento dinâmico Olá oferecidas pelos serviços de suporte de dados do Azure, vários ficheiros MP4 alinhada GOP de cada uma resolução e velocidade de transmissão diferentes terá toobe gerado. por isso, Olá toodo [MXF de codificação de mensagens em fila para uma MP4 de velocidade de transmissão única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) explicação passo a passo fornece-nos com um ponto de partida.

![Iniciar o fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Iniciar o fluxo de trabalho*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adicionar um ou mais saídas MP4 adicionais
Todos os ficheiros MP4 no nosso resultante recurso de Media Services do Azure irão suportar uma resolução e velocidade de transmissão diferentes. Vamos adicionar um ou mais MP4 saída ficheiros toohello fluxo de trabalho.

toomake se temos Olá todos os nossos vídeos codificadores criadas com as mesmas definições, tooduplicate mais conveniente Olá codificador vídeo de AVC já existente e configurar outra combinação de resolução e velocidade de transmissão (vamos adicionar um 960 x 540 em 25 fotogramas por segundo em 2,5 Mbps). codificador existente do Olá tooduplicate, cópia colar na superfície do designer Olá.

Ligar o pin de saída de vídeo descomprimidos Olá de Olá entrada de ficheiro do suporte de dados para o nosso novo componente AVC.

![Segundo codificador de AVC ligado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Segundo codificador de AVC ligado*

Agora adapte configuração Olá para o nosso toooutput de codificador AVC de nova 960 x 540 2,5 Mbps. (Utilizar o respetivo propriedades "largura de saída", "Altura de saída" e "Velocidade de transmissão (kbps)" para este.)

Dado que queremos toouse asset resultante de Olá, juntamente com o empacotamento dinâmico dos serviços de suporte de dados do Azure, tem de Olá ponto final de transmissão em fluxo toobe capaz de gerar destes fragmentos HLS/fragmentado MP4/DASH que são exatamente alinhado tooeach outro de uma forma de ficheiros MP4 Se os clientes que são alternar entre diferentes de forma obtêm uma único uniforme contínua áudio e vídeo experiência. toomake que ocorrem, precisamos tooensure que, nas propriedades de Olá de ambos os codificadores AVC Olá tamanho GOP ("grupo de imagens") para ambos os ficheiros MP4 está definida too2 segundos, que podem ser efetuados por:

* Definir Olá GOP tamanho modo tooFixed GOP tamanho e
* segundos de tootwo de intervalo de moldura de chave de Olá.
* também definir Olá GOP IDR controlo tooClosed GOP tooensure colocado é de todos os GOP nos respetivas sem dependências

toomake nosso toounderstand conveniente de fluxo de trabalho, mudar o nome de codificador de AVC primeiro Olá demasiado "codificador de vídeo AVC 640 x 360 1200kbps" e Olá segundo codificador de AVC "codificador vídeo AVC 960 x 540 2500 kbps".

Agora pode adicione uma segunda ISO MPEG-4 Multiplexer e uma segunda saída de ficheiro. Ligue Olá multiplexer toohello novo AVC codificador e certifique-se de que o resultado é direcionado para Olá ficheiro de saída. Em seguida, ligar também Olá AAC codificador áudio saída toohello novo entrada da multiplexer. Olá ficheiro de saída por sua vez, em seguida, possível tooadd de nó de elemento/ficheiro de saída toohello ligado-toohello Asset de serviços de suporte de dados que será criado.

![Segundo Muxer e ficheiro de saída ligados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Segundo Muxer e ficheiro de saída ligados*

Para compatibilidade com o empacotamento dinâmico de Media Services do Azure, configure a contagem de tooGOP Olá do multiplexer modo de segmento ou a duração e defina Olá GOPs por segmento too1. (Deve ser predefinido Olá.)

![Modos de segmento de Muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Modos de segmento de Muxer*

Nota: poderá toorepeat este processo para quaisquer outros velocidade de transmissão e resolução combinações pretende toohave adicionado toohello saída de recurso.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configurar nomes de saída do ficheiro de Olá
Temos de mais do que um elemento de saída de ficheiro único adicionado toohello. Isto fornece uma necessidade toomake se Olá nomes de ficheiros para cada um dos Olá saída ficheiros são diferentes entre si e talvez mesmo aplicam-se uma convenção de nomenclatura de ficheiros, de modo, torna-se limpar do nome de ficheiro Olá está a lidar com.

Atribuição de nome de saída do ficheiro pode ser controlada através da expressões no estruturador de Olá. Abra o painel de propriedade Olá para um dos componentes de saída do ficheiro de Olá e abra o editor de expressão Olá para Olá propriedade de ficheiro. A nossa primeiro ficheiro de saída foi configurado através de Olá seguintes expressão (consulte o tutorial Olá para que vai da [MXF tooa transmissão MP4 saída](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Isto significa que o nosso filename é determinado pelo duas variáveis: Olá saída toowrite de diretório no e hello nome de base do ficheiro de origem. anterior Olá está exposta como uma propriedade numa raiz de fluxo de trabalho de Olá e Olá esta última opção é determinado pelo ficheiro de entrada Olá. Tenha em atenção que diretório de saída Olá está a utilizar para fins de teste local; Esta propriedade será substituída pelo motor de fluxo de trabalho de Olá quando o fluxo de trabalho Olá é executado pelo processador de multimédia baseado na nuvem de Olá nos Media Services do Azure.
toogive ambos os nossa saída ficheiros uma saída consistente de nomenclatura, alteração Olá primeiro ficheiro expressão Nomenclatura para:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

e Olá segundo para:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Execute um teste intermédio executar toomake se ambos os ficheiros de saída MP4 corretamente são gerados.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adicionar um registo de áudio separada
Como Iremos ver mais tarde quando geramos uma toogo de ficheiro ISM com ficheiros MP4 de saída, iremos irá requerer também um ficheiro MP4 de só de áudio como controlar áudio Olá para nosso transmissão em fluxo adaptável. toocreate este ficheiro, adicione um muxer adicionais toohello fluxo de trabalho de (ISO-MPEG-4 Multiplexer) e ligar o pin de saída do codificador AAC Olá com o respetivo pin de entrada para controlar 1.

![Áudio Muxer adicionado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Áudio Muxer adicionado*

Crie uma terceira fluxo saído do ficheiro de saída componente toooutput Olá de Olá muxer e configure a expressão de nomenclatura de ficheiro de Olá como:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Áudio Muxer criação da saída de ficheiro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Áudio Muxer criação da saída de ficheiro*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adicionar Olá. ISM SMIL ficheiro
Para Olá empacotamento dinâmico toowork em combinação com ambos os MP4 ficheiros (e Olá MP4 só de áudio) no nosso recurso dos Media Services, também tem de um ficheiro de manifesto (também designado por um ficheiro de "SMIL": sincronizados idioma de integração de suporte). Este ficheiro indica tooAzure Media Services que ficheiros MP4 estão disponíveis para um empacotamento dinâmico e que esses tooconsider para Olá áudio transmissão em fluxo. Um ficheiro de manifesto típico para um conjunto do MP4 com uma única sequência de áudio tem o seguinte aspeto:

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

ficheiro. ISM Olá contém dentro de uma instrução de comutador, tooeach uma referência de Olá MP4 vídeos ficheiros individuais e além do ficheiro de áudio toothose também um (ou mais) referencia tooan MP4 que contém apenas áudio Olá.

A gerar ficheiro de manifesto Olá para o nosso conjunto do MP4 pode ser feito através de um componente chamado Olá "AMS escritor Manifest". toouse, arraste-o para a superfície de Olá e ligue Olá "Escrever concluída" pins de saída de Olá três ficheiros de saída componentes toohello AMS manifesto do escritor de entrada. Em seguida, certifique-se de que tooconnect Olá resultado Olá AMS manifesto escritor toohello ficheiro/elemento de saída.

Tal como acontece com a nossa outros ficheiros saída componentes, configure o nome de saída do Olá ISM ficheiro com uma expressão:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Nosso fluxo de trabalho concluído aspeto Olá abaixo:

![Terminar MXF toomultibitrate MP4 fluxo de trabalho de](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Terminar MXF toomultibitrate MP4 fluxo de trabalho de*

## <a id="MXF_to__multibitrate_MP4"></a>Codificação MXF para multibitrate MP4 - blueprint avançada
No Olá [instruções anteriores do fluxo de trabalho](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) viu como um único recurso de entrada MXF pode ser convertido para um elemento de saída com ficheiros MP4 de velocidade de transmissão múltipla, um ficheiro MP4 de só de áudio e um ficheiro de manifesto para utilização em conjunto com suporte de dados do Azure Serviços de empacotamento dinâmico.

Estas instruções irão mostrar como alguns dos aspetos Olá podem ser melhorados e efetuadas mais conveniente.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance de descrição geral do fluxo de trabalho
![Multibitrate MP4 tooenhance de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 tooenhance de fluxo de trabalho*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>As convenções de nomenclatura de ficheiros
Fluxo de trabalho anterior Olá especificamos numa expressão simples como base Olá para gerar nomes de ficheiro de saída. Temos algumas duplicação apesar: todos os componentes de ficheiro de saída individual de Olá Olá especificado essa expressão.

Por exemplo, o nosso componente de saída do ficheiro para o ficheiro de vídeo primeiro Olá está configurado com esta expressão:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Enquanto para Olá segundo saída gráfica, temos de uma expressão como:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Não possível limpeza, menos erro suscetível e mais conveniente se podemos foi remova alguns deste duplicação e certifique-coisas mais configuráveis em vez disso? Luckily podemos: capacidades de expressão do designer de Olá em combinação com Olá capacidade toocreate as propriedades personalizadas no nosso raiz de fluxo de trabalho irão dar-numa camada adicional de conveniência.

Vamos assumir que irá unidade nome de ficheiro configuração do Olá de forma de ficheiros MP4 individuais de Olá. Estes forma irá pretendemos tooconfigure no Centro de um colocar (em Olá raiz do nosso gráfico), de onde estejam acedida geração de nome de ficheiro de unidade e tooconfigure. toodo isto, vamos começar por publicar a propriedade de velocidade de transmissão de Olá partir de ambos os AVC codificadores toohello de raiz do nosso fluxo de trabalho, para que este fica acessível a partir de ambos os raiz Olá, bem como codificadores Olá AVC. (Mesmo se apresentados em dois oportunidades diferentes, é apenas um valor subjacente.)

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Publicação de propriedades do componente na raiz do fluxo de trabalho de Olá
Abra o codificador de AVC primeiro Olá, aceda a propriedade de velocidade de transmissão (kbps) toohello e a partir da lista pendente de Olá escolha publicar.

![Propriedade de velocidade de transmissão de Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Propriedade de velocidade de transmissão de Olá publicação*

Configurar Olá publicar diálogo toopublish toohello de raiz do nosso gráfico de fluxo de trabalho, com um nome de "video1bitrate" publicado e um nome a apresentar legível "Velocidade de transmissão do vídeo 1". Configurar um personalizado o nome do grupo chamado "Transmissão em fluxo de forma" e prima publicar.

![Propriedade de velocidade de transmissão de Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Caixa de diálogo de publicação para a propriedade de velocidade de transmissão*

Olá repetida mesmo para a propriedade de velocidade de transmissão de Olá do Olá segunda codificador AVC e dê-lhe nome "video2bitrate" com um nome a apresentar "Velocidade de transmissão do vídeo de 2", no Olá mesmo personalizada "Transmissão em fluxo de forma" de grupo.

Se agora, iremos inspecionar as propriedades de raiz do fluxo de trabalho Olá, iremos ver nosso grupo personalizado com hello apareçam duas propriedades publicadas. Ambos são ao refletir o valor de Olá da respetiva velocidade de transmissão de codificador de AVC respetiva.

![Propriedades de velocidade de transmissão publicada numa raiz de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Sempre que queremos tooaccess estas propriedades a partir do código ou a partir de uma expressão, podemos fazer, como esta:

* a partir do código inline de um componente imediatamente abaixo da raiz de Olá: node.getPropertyAsString('.. / video1bitrate', nulo)
* dentro de uma expressão: ${ROOT_video1bitrate}

Vamos completar o grupo de "Transmissão em fluxo de forma" Olá ao nosso transmissão de áudio controlar no mesmo, bem como a publicação. Dentro propriedades Olá Olá AAC codificador, procure a definição de velocidade de transmissão de Olá e selecione publicar Olá pendente seguinte tooit. Publicar toohello raiz do gráfico de Olá com o nome "audio1bitrate" e o nome "Velocidade de transmissão do áudio 1" no nosso grupo personalizado "Transmissão em fluxo de forma" a apresentar.

![Caixa de diálogo publicação de velocidade de transmissão de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Caixa de diálogo publicação de velocidade de transmissão de áudio*

![Propriedades de áudio e vídeos resultantes numa raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Propriedades de áudio e vídeos resultantes numa raiz*

Tenha em atenção que a alteração de qualquer um desses três valores também configura novamente e alterações Olá valores em componentes respetivos Olá estes estão ligados com (e onde publicados a partir da).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Ter gerado o ficheiro de saída nomes baseiam-se nos valores de propriedade publicada
Em vez de codificar nosso nomes de ficheiro gerado, iremos pode agora alterar nosso expressão de nome de ficheiro em cada um dos toorely de componentes de saída do ficheiro de Olá nas propriedades de velocidade de transmissão de Olá que vamos apenas publicados na raiz do gráfico Olá. Começando com o nosso primeiro saída de ficheiro, localizar a propriedade de ficheiro Olá e Editar expressão Olá como esta:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

parâmetros diferentes de Olá nesta expressão podem ser acedidos e introduzidos por atingir Olá cifrão no teclado Olá enquanto na janela de expressão de Olá. Um dos parâmetros disponíveis Olá é nossa propriedade video1bitrate que iremos publicados anteriormente.

![Aceder a parâmetros dentro de uma expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Aceder a parâmetros dentro de uma expressão*

Olá, mesmo para o resultado de ficheiro Olá para os nosso vídeo segundo:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

e de saída de ficheiro só de áudio Olá:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Se agora, vamos alterar Olá velocidade de transmissão de qualquer um dos vídeo Olá ou ficheiros de áudio, será reconfigurado de codificador respetivos Olá e Convenção de nome de ficheiro com base na velocidade de transmissão de Olá será cumprida todos os automática.

## <a id="thumbnails_to__multibitrate_MP4"></a>Adicionar a saída de MP4 toomultibitrate de miniaturas
A partir de um fluxo de trabalho que gera [um multibitrate MP4 um resultado de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), iremos irá agora ser à procura para adicionar a saída de toohello miniaturas.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Miniaturas de tooadd de descrição geral de fluxo de trabalho para
![Multibitrate MP4 toostart de fluxo de trabalho do](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Multibitrate MP4 toostart de fluxo de trabalho do*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adicionar JPG codificação
heart Olá da nossa em miniatura geração será o componente de codificador JPG Olá, ficheiros JPG toooutput capaz de.

![Codificador JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*Codificador JPG*

Diretamente no entanto, não é possível ligar fluxo nossos vídeo descomprimidos de Olá entrada de ficheiro do suporte de dados para o codificador JPG Olá. Em vez disso, espera toobe entregar frames individuais. Esta ação, podemos fazer através de componente de porta de moldura de vídeo Olá.

![Ligar um codificador JPG toohello do período da porta](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Ligar um codificador JPG toohello do período da porta*

porta de moldura de Olá depois de cada tantas segundos ou frames permite toopass uma moldura de vídeo. pode ser configurado nas propriedades de Olá Olá intervalo e Olá desvio do tempo com que esta situação acontece.

![Propriedades de porta de moldura vídeos](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Propriedades de porta de moldura vídeos*

Vamos criar uma miniatura a cada minuto definindo Olá modo tooTime (segundos) e Olá too60 do intervalo.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Lidar com a conversão de espaço de cor
Enquanto seria parecer lógica os pins de vídeo descomprimidos de porta de moldura Olá e Olá entrada de ficheiro do suporte de dados agora podem ser ligados, iremos deverá receber um aviso se seria fazemo-lo.

![Erro de espaço de cor de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Erro de espaço de cor de entrada*

Isto acontece porque a forma de Olá em que colour informações são representadas na nossa original em bruto descomprimido vídeo sequência provenientes da nossa MXF é diferente da que Olá JPG codificador espera obter. Mais especificamente, uma so-called "cor espaço" de "RGB" ou "Em tons de cinzento" é esperado tooflow no. Isto significa que entrada de transmissão de que Olá vídeo Frame da porta terá toohave uma conversão aplicada sobre o espaço de cor de primeiro.

Arraste para Olá de fluxo de trabalho de Olá conversor de espaço de cor - Intel e ligá-lo a porta de moldura tooour.

![Ligar um Convertor de espaço de cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Ligar um Convertor de espaço de cor*

Na janela de propriedades de Olá, escolha a entrada de Olá BGR 24 Olá predefinição na lista.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniaturas de Olá de escrita
Diferente do vídeo da nossa MP4, Olá codificador JPG componente irá saída mais do que um ficheiro. Na ordem toodeal com esta opção, pode ser utilizado um componente de cenas pesquisa JPG ficheiro escritor: vai demorar miniaturas JPG entradas Olá e escrevê-las, cada nome de ficheiro que está a ser o sufixo por um número diferente. (número de Olá normalmente indicar o número de Olá de segundos/unidades na sequência de Olá que miniatura Olá foi desenhada a partir de.)

![Introdução ao hello cena pesquisa JPG ficheiro escritor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Introdução ao hello cena pesquisa JPG ficheiro escritor*

Configurar a propriedade de caminho de pasta de saída de Olá com a expressão de Olá: ${ROOT_outputWriteDirectory}

e Olá propriedade de prefixo de nome de ficheiro com:

    ${ROOT_sourceFileBaseName}_thumb_

prefixo de Olá irá determinar como ficheiros em miniatura Olá estão a ser designados. Estes irão ser com o sufixo posição de um número com indicação Olá botão no fluxo de Olá.

![Propriedades de pesquisa JPG ficheiro escritor cena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Propriedades de pesquisa JPG ficheiro escritor cena*

Ligar o nó de elemento/ficheiro de saída do Olá cena pesquisa JPG ficheiro escritor toohello.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Detetar erros num fluxo de trabalho
Ligar a entrada de Olá Olá cor espaço conversor toohello em bruto descomprimidos vídeo de saída de. Agora a efetuar um teste local a executar o fluxo de trabalho Olá. Há um fluxo de trabalho de Olá hipótese boa subitamente irá parar de executar e indicar com um contorno vermelho no componente Olá que encontrou um erro:

![Erro de conversor de espaço de cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Erro de conversor de espaço de cor*

Clique ícone de "I" de Olá ligeiramente vermelho na Olá canto superior direito do Olá conversor de espaço de cor componente toosee que é o motivo de Olá falha na tentativa de codificação Olá.

![Caixa de diálogo de erro de conversor de espaço de cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Caixa de diálogo de erro de conversor de espaço de cor*

Transforma, como pode ver, que Olá entrada cor espaço padrão para o conversor de espaço de cor Olá tem toobe rec601 para a nossa conversão pedida de YUV tooRGB. Parecer nosso fluxo não indica de rec601. (Rec 601 é um padrão para codificação entrelaçadas analógica sinais de vídeos em formato digital de vídeo. Especifica uma região de Active Directory que abrangem 720 amostras de luminance e 360 chrominance amostras por linha. cor de Olá codificação sistema é conhecido como YCbCr 4:2:2.)

toofix isto, iremos irá indicar nos metadados de Olá do nosso fluxo que estamos a lidar com rec601 conteúdo. toodo, pelo que iremos utilizar um componente do Atualizador de tipo de dados de vídeo, vamos pôr em prática entre nosso em bruto de origem e Olá cor espaço conversão componente. Este atualizador do tipo de dados permite que uma atualização manual Olá de determinados dados de vídeos propriedades de tipo. Configure tooindicate um padrão de espaço de cor de "Rec 601". Isto fará com que fluxo do Olá Atualizador de tipo de dados de vídeo tootag Olá com espaço de cor de "Rec 601" Olá se tiver ocorrido não existe espaço de cor definido ainda. (Esta não substituirão quaisquer metadados existente, a menos que a caixa de verificação de substituição de Olá tiver sido selecionada.)

![Atualizar o padrão de espaço de cor no Olá Atualizador do tipo de dados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Atualizar o padrão de espaço de cor no Olá Atualizador do tipo de dados*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Fluxo de trabalho concluído
Agora que a nossa nosso fluxo de trabalho estiver concluído, efetue outro toosee de execução do teste-passe.

![Fluxo de trabalho concluído para o resultado de várias mp4 com miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Fluxo de trabalho concluído para o resultado de várias mp4 com miniaturas*

## <a id="time_based_trim"></a>Corte de baseados no tempo de mensagens em fila de saída multibitrate MP4
A partir de um fluxo de trabalho que gera [um multibitrate MP4 um resultado de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), iremos irá agora ser à procura para corte vídeo de origem Olá com base no carimbos de data / hora.

### <a id="time_based_trim_start"></a>Fluxo de trabalho descrição geral toostart corte para a adicionar
![Iniciar o corte de tooadd de fluxo de trabalho para](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Iniciar o corte de tooadd de fluxo de trabalho para*

### <a id="time_based_trim_use_stream_trimmer"></a>Utilizar Olá Trimmer de fluxo
componente de fluxo Trimmer Olá permite início de Olá tootrim e o fim de um fluxo de entrada base nas informações de temporização (segundos, minutos,...). trimmer Olá não suporta corte baseada no intervalo.

![Fluxo Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Fluxo Trimmer*

Em vez de ligar diretamente codificadores Olá AVC e orador posição assigner toohello entrada de ficheiro do suporte de dados, vamos pôr em prática entre essas trimmer de fluxo de Olá. (Um para o sinal de vídeo Olá e outro para o sinal de áudio intercalado Olá.)

![Colocar em entre Trimmer de fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Colocar em entre Trimmer de fluxo*

Vamos configurar trimmer Olá, para que iremos só irá processar vídeos e áudio entre 15 segundos e 60 segundos vídeo Olá.

Aceda a propriedades de toohello de Olá Trimmer de fluxo de vídeo e configurar a hora de início (15s) e propriedades de hora de fim (60s). toomake se de que os nosso trimmer de áudio e vídeo é sempre toohello configurado mesmo começar e terminar valores, vamos publicar esses raiz toohello de fluxo de trabalho Olá.

![Publicar a propriedade de hora de início do fluxo Trimmer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Publicar a propriedade de hora de início do fluxo Trimmer*

![Publicar a caixa de diálogo de propriedades para a hora de início](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Publicar a caixa de diálogo de propriedades para a hora de início*

![Publicar a caixa de diálogo de propriedades para a hora de fim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Publicar a caixa de diálogo de propriedades para a hora de fim*

Se agora, iremos inspecionar raiz Olá do nosso fluxo de trabalho, ambas as propriedades serão neatly apresentados e configuráveis a partir daí.

![Propriedades publicadas disponíveis em raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Propriedades publicadas disponíveis em raiz*

Agora abra as propriedades de corte Olá trimmer áudio Olá e configurar as horas de início e de fim com uma expressão que referencia toohello publicados propriedades na raiz de Olá da nossa fluxo de trabalho.

Para a hora de início de áudio corte Olá:

    ${ROOT_TrimmingStartTime}

e para a respetiva hora de fim:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Fluxo de trabalho concluído
![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Fluxo de trabalho concluído*

## <a id="scripting"></a>Introdução ao hello componente convertidos em script
Componentes com script podem executar scripts arbitrários durante as fases de execução de Olá do nosso fluxo de trabalho. Existem quatro scripts diferentes que podem ser executadas, cada um com características específicas e os seus próprios local no ciclo de vida do fluxo de trabalho Olá:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

documentação de Olá de Olá convertidos em script o componente passa mais detalhadamente para cada um dos Olá acima. No [Olá seguinte secção](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), Olá **realizeScript** script componente é tooconstruct utilizado um xml cliplist no momento de Olá quando o fluxo de trabalho Olá começa. Este script chama-se durante a configuração de componente Olá, o que acontece apenas uma vez no ciclo de vida da mesma.

### <a id="scripting_hello_world"></a>Script num fluxo de trabalho: Olá, mundo
Arraste um componente de criar um script para a superfície do designer Olá e mude o nome (por exemplo, "SetClipListXML").

![Adicionar um componente com script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Adicionar um componente com script*

Quando inspecionar propriedades Olá de Olá componente convertidos em script, Olá serão apresentados quatro tipos de script diferentes, cada script diferentes tooa configurável.

![Propriedades do componente de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propriedades do componente de script*

Desmarque Olá processInputScript e abra o editor de Olá para Olá realizeScript. Agora iremos estiver configurados e pronto a toostart scripting.

Scripts são escritos no Groovy, uma linguagem de script compilada dinamicamente para a plataforma de Java Olá que mantém a compatibilidade com o Java. Na realidade, o código de Java a maioria das é código Groovy válido.

Vamos escrever um script de groovy mundo Olá simples no contexto de Olá da nossa realizeScript. Introduza o seguinte Olá num editor de Olá:

    node.log("hello world");

Agora a executar uma execução de teste local. Após a execução, Inspecione (através do separador sistema Olá Olá convertidos em script componente) Olá propriedade de registos.

![Saída de registo do Olá mundo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Saída de registo do Olá mundo*

objeto de nó Olá iremos chamar o método de registo de Olá, refere-se tooour atual "nó" ou Olá componente que está a scripting dentro. Todos os componentes como tal, tem Olá capacidade toooutput dados de registo disponíveis através do separador de sistema Olá. Neste caso, iremos saída Olá literal de cadeia "Olá mundo". Importante toounderstand aqui é que este pode provar toobe uma ferramenta de depuração valiosas, fornecendo-lhe conhecimentos aprofundados sobre os scripts de Olá, na verdade, está a fazer.

A partir no nosso ambiente de script, iremos também tem acesso tooproperties nos outros componentes. Experimente este:

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

A nossa janela de registo irá mostrar-nos Olá seguintes:

![Saída de registo para aceder aos caminhos de nó](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Saída de registo para aceder aos caminhos de nó*

## <a id="frame_based_trim"></a>Com base no período de corte de saída multibitrate MP4
A partir de um fluxo de trabalho que gera [um multibitrate MP4 um resultado de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), iremos irá agora ser à procura para corte vídeo de origem Olá com base nas contagens de moldura.

### <a id="frame_based_trim_start"></a>Blueprint corte para a adição de toostart de descrição geral
![Corte para a adição de toostart de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Corte para a adição de toostart de fluxo de trabalho*

### <a id="frame_based_trim_clip_list"></a>Olá Clip lista XML a utilizar
Em todos os tutoriais de fluxo de trabalho anterior, utilizámos o componente de entrada de ficheiro do suporte de dados de Olá como nossa vídeo origem de entrada. Para este cenário específico, iremos utilizar componentes de origem da lista de Clip Olá em vez disso. Tenha em atenção que esta não deve ser Olá preferencial forma de trabalho; Utilize apenas Olá Clip lista origem quando existe um toodo razão real, por isso, (tal como no Olá abaixo caso, onde que estamos a efetuar a utilização das capacidades de corte Olá clip lista).

tooswitch do nosso toohello entrada de ficheiro do suporte de dados de origem da lista de Clip, arraste o componente de origem da lista de Clip Olá para a superfície de desenho de Olá e ligue Olá Clip lista XML pin toohello Clip lista XML o nó do estruturador de fluxo de trabalho de Olá. Isto deve preencher Olá Clip lista de origem com pins de saída, de acordo com as vídeo de entrada de tooour. Ligar agora pins de vídeo não comprimidos e descomprimidos áudio Olá de Olá Olá Clip lista origem toohello respetivos AVC codificadores e Interleaver de sequência de áudio. Remova agora Olá entrada de ficheiro do suporte de dados.

![Substituído Olá entrada de ficheiro do suporte de dados com Olá Clip lista de origem](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Substituído Olá entrada de ficheiro do suporte de dados com Olá Clip lista de origem*

componente de origem da lista de Clip Olá aceita como entrada um "XML de lista de Clip". Quando selecionar Olá tootest de ficheiro de origem com localmente, este xml de lista clip é preenchido automaticamente para si.

![Propriedade de Clip lista XML auto-preenchida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Propriedade de Clip lista XML auto-preenchida*

Procura um pouco mais próximo dos toohello xml, este é o aspeto que tem:

![Caixa de diálogo de lista de clip editar](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Caixa de diálogo de lista de clip editar*

Isto no entanto não reflete as capacidades de Olá de Olá clip lista xml. Uma opção que temos é tooadd um elemento "Compactar" em vídeo Olá e origem de áudio, como esta:

![Adicionar uma lista do elemento compactação toohello clip](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Adicionar uma lista do elemento compactação toohello clip*

Se modificar o xml de lista de clip Olá como esta acima e efetuar um teste local executar, verá as vídeo de Olá foi corretamente cortada entre 10 e 20 segundos vídeo Olá.

Contrary toowhat ocorre quando o fizer uma execução local, embora, este xml cliplist muito mesmo não teriam Olá, mesmo que tenha efeito quando aplicada num fluxo de trabalho que é executado em Media Services do Azure. Quando é iniciado o codificador de Premium do Azure, Olá cliplist xml é gerado sempre novamente, com base na codificação de Olá de ficheiro de entrada do Olá tarefa foi indicada. Isto significa que quaisquer alterações que fazemos no xml de Olá Infelizmente deverá ser substituídas.

toocounter Olá cliplist xml que está a ser eliminado quando é iniciada uma tarefa de codificação, iremos pode voltar gerá-la no momento de Olá imediatamente após o início de Olá do nosso fluxo de trabalho. Essas ações personalizadas podem ser criadas através do qual é denominado um "Component convertidos em script". Para obter mais informações, consulte [Introducing Olá convertidos em script componente](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Arraste um componente de criar um script para a superfície do designer Olá e renomeie-demasiado "SetClipListXML".

![Adicionar um componente com script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Adicionar um componente com script*

Quando inspecionar propriedades Olá de Olá componente convertidos em script, Olá serão apresentados quatro tipos de script diferentes, cada script diferentes tooa configurável.

![Propriedades do componente de script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propriedades do componente de script*

### <a id="frame_based_trim_modify_clip_list"></a>Lista de clip Olá modificação de um componente convertidos em script
Antes de voltar iremos poder escrever Olá cliplist xml que é gerado durante o arranque do fluxo de trabalho, precisamos da propriedade do toohave acesso toohello cliplist xml e o conteúdo. Pode fazemo-lo como esta:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clip entrada que está a ser registada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Lista de clip entrada que está a ser registada*

Primeiro é preciso toodetermine uma forma do ponto de até que ponto queremos tootrim Olá vídeo. publicar este utilizador de menor technical toohello conveniente de fluxo de trabalho Olá, de toomake raiz de toohello duas propriedades do gráfico Olá. toodo, clique com o botão direito do rato em superfície do designer Olá e selecione "Adicionar propriedade de":

* Primeira propriedade: "ClippingTimeStart" do tipo: "TIMECODE"
* Segunda propriedade: "ClippingTimeEnd" do tipo: "TIMECODE"

![Adicionar caixa de diálogo de propriedades para a hora de início de recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Adicionar caixa de diálogo de propriedades para a hora de início de recorte*

![Publicado recorte propriedades de tempo na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Publicado recorte propriedades de tempo na raiz do fluxo de trabalho*

Configure o valor adequado de tooa de propriedades:

![Configurar Olá recorte propriedades de início e de fim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Configurar Olá recorte propriedades de início e de fim*

Agora, de dentro do nosso script, iremos podem aceder a ambas as propriedades, como esta:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Janela de registo que mostra início e fim de recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Janela de registo que mostra início e fim de recorte*

Vamos analisar as cadeias de timecode Olá num formulário toouse mais prático, utilizando uma expressão regular simple:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Janela de registo com o resultado do timecode analisado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Janela de registo com o resultado do timecode analisado*

Com estas informações em execução, iremos agora pode modificar o início de Olá do Olá cliplist xml tooreflect e hora de fim para Olá pretendido recorte exata de moldura de filmes Olá.

![Elementos de compactação do tooadd de código do script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Elementos de compactação do tooadd de código do script*

Isto foi feito através de operações de manipulação de cadeia normal. Olá resultante clip modificado lista xml não é gravado toohello clipListXML propriedade na raiz do fluxo de trabalho Olá através do método de "setProperty" Olá. janela de registo Olá após a execução de outro teste seria Mostrar nos Olá seguintes:

![Lista de clip resultante Olá de registo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Lista de clip resultante Olá de registo*

Efetue um toosee de execução do teste como fluxos de áudio e vídeo Olá tem sido anexados. Como vai fazer mais do que um teste-execução com diferentes valores para os pontos de corte Olá, irá notar que às serão não ser levados em consideração no entanto! motivo Olá para isto é que designer Olá, ao contrário Olá tempo de execução do Azure, não substituição Olá cliplist xml cada execução. Isto significa que apenas hello muito primeira definiu Olá e terminar pontos, fará com que Olá xml tootransform, todos os outros Olá vezes, nosso cláusula de proteção (se (clipListXML.indexOf ("<trim>") = = -1)) irá impedir que o fluxo de trabalho Olá adicionar outra compactação elemento quando já existe um presente.

toomake nosso fluxo de trabalho conveniente tootest localmente, é melhor adicionar algum código de manutenção próxima inspeciona se um elemento de compactação já estava presente. Se assim for, iremos removê-lo antes de continuar, modificando Olá xml com novos valores de Olá. Em vez de utilizar manipulações de cadeia simples, é provavelmente mais segura toodo isto através do objeto de real xml de modelo de análise.

Antes de pode adicionamos desse código, embora, precisamos tooadd que um número de declarações de importação no Olá início do nosso script primeiro:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Depois da primeira, adicionamos Olá necessário o código de limpeza:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Este código passa apenas acima ponto Olá que adicionamos Olá elementos compactação toohello cliplist xml.

Neste momento, estamos poderá executar e modificar nosso fluxo de trabalho como sucederia com queremos enquanto tem alterações de Olá aplicadas alguma vez.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Adicionar uma propriedade de conveniência ClippingEnabled
Como não poderá sempre toohappen de corte, vamos concluir desativar nosso fluxo de trabalho, adicionando um conveniente sinalizador booleano que indica se pretende ou não queremos tooenable corte / recorte.

Tal como anteriormente, publicar uma nova propriedade toohello de raiz do nosso fluxo de trabalho chamado "ClippingEnabled" do tipo "BOOLEANO".

![Publicar uma propriedade para ativar recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Publicar uma propriedade para ativar recorte*

Com Olá abaixo cláusula guard simples, iremos pode verificar se é necessário o corte e decidir se nossa lista de clip como tal, precisa de toobe modificado ou não.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Código de conclusão
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>Consulte também
[Introdução às Premium codificação, no suporte de dados do Azure, os serviços](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Como tooUse Premium codificação na Media Services do Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[A codificação de conteúdo a pedido com o serviço de multimédia do Azure](media-services-encode-asset.md#media-encoder-premium-workflow)

[Formatos e Codecs de Fluxo de Trabalho Premium do Codificador de Multimédia](media-services-premium-workflow-encoder-formats.md)

[Ficheiros de fluxo de trabalho de exemplo](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Ferramenta de Explorador de serviços de suporte de dados do Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
