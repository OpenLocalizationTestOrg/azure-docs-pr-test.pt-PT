---
title: "aaaPerform avançadas codificação personalizando MES predefinições | Microsoft Docs"
description: "Este tópico mostra como tooperform avançadas codificação personalizando o codificador de multimédia Standard predefinições de tarefas."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 2a4ade25-e600-4bce-a66e-e29cf4a38369
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: juliako
ms.openlocfilehash: 9caa68fafacaf51f91f0554c5bafe491928d8c77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a><span data-ttu-id="f33ab-103">Efetuar a codificação avançadas personalizando MES predefinições</span><span class="sxs-lookup"><span data-stu-id="f33ab-103">Perform advanced encoding by customizing MES presets</span></span> 

## <a name="overview"></a><span data-ttu-id="f33ab-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="f33ab-104">Overview</span></span>

<span data-ttu-id="f33ab-105">Este tópico mostra como as predefinições de toocustomize codificador de multimédia Standard.</span><span class="sxs-lookup"><span data-stu-id="f33ab-105">This topic shows how toocustomize Media Encoder Standard presets.</span></span> <span data-ttu-id="f33ab-106">Olá [codificação com o codificador de multimédia Standard utilizando predefinições personalizadas](media-services-custom-mes-presets-with-dotnet.md) tópico mostra como toouse .NET toocreate uma codificação de tarefas e uma tarefa que executa esta tarefa.</span><span class="sxs-lookup"><span data-stu-id="f33ab-106">hello [Encoding with Media Encoder Standard using custom presets](media-services-custom-mes-presets-with-dotnet.md) topic shows how toouse .NET toocreate an encoding task and a job that executes this task.</span></span> <span data-ttu-id="f33ab-107">Uma vez, personalizar uma predefinição, alimentação Olá predefinições personalizado toohello codificação tarefas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-107">Once you customize a preset, supply hello custom presets toohello encoding task.</span></span> 

>[!NOTE]
><span data-ttu-id="f33ab-108">Se utilizar uma predefinição XML, certifique-se de que toopreserve Olá ordem elementos, conforme mostrado nos exemplos XML abaixo (por exemplo, KeyFrameInterval deve preceder SceneChangeDetection).</span><span class="sxs-lookup"><span data-stu-id="f33ab-108">If using an XML preset, make sure toopreserve hello order of elements, as shown in XML samples below (for example, KeyFrameInterval should precede SceneChangeDetection).</span></span>
>

<span data-ttu-id="f33ab-109">Neste tópico, predefinições de personalizado Olá que efetuar Olá seguintes tarefas de codificação são demonstradas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-109">In this topic, hello custom presets that perform hello following encoding tasks are demonstrated.</span></span>

## <a name="support-for-relative-sizes"></a><span data-ttu-id="f33ab-110">Suporte para tamanhos de relativos</span><span class="sxs-lookup"><span data-stu-id="f33ab-110">Support for relative sizes</span></span>

<span data-ttu-id="f33ab-111">Quando a gerar miniaturas, não terá de especificar tooalways saída largura e altura em pixéis.</span><span class="sxs-lookup"><span data-stu-id="f33ab-111">When generating thumbnails, you do not need tooalways specify output width and height in pixels.</span></span> <span data-ttu-id="f33ab-112">Pode especificá-las em percentagens, no intervalo de Olá [% 1,..., 100%].</span><span class="sxs-lookup"><span data-stu-id="f33ab-112">You can specify them in percentages, in hello range [1%, …, 100%].</span></span>

### <a name="json-preset"></a><span data-ttu-id="f33ab-113">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-113">JSON preset</span></span>
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a><span data-ttu-id="f33ab-114">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-114">XML preset</span></span>
    <Width>100%</Width>
    <Height>100%</Height>

## <span data-ttu-id="f33ab-115"><a id="thumbnails"></a>Gerar miniaturas</span><span class="sxs-lookup"><span data-stu-id="f33ab-115"><a id="thumbnails"></a>Generate thumbnails</span></span>

<span data-ttu-id="f33ab-116">Esta secção mostra como toocustomize uma predefinição que gera miniaturas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-116">This section shows how toocustomize a preset that generates thumbnails.</span></span> <span data-ttu-id="f33ab-117">Olá predefinição definida abaixo contém informações sobre a forma como pretende tooencode o ficheiro, bem como informações necessárias toogenerate miniaturas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-117">hello preset defined below contains information on how you want tooencode your file as well as information needed toogenerate thumbnails.</span></span> <span data-ttu-id="f33ab-118">Pode efetuar qualquer uma das predefinições MES Olá documentadas [isto](media-services-mes-presets-overview.md) secção e adicione o código que gera miniaturas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-118">You can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and add code that generates thumbnails.</span></span>  

> [!NOTE]
> <span data-ttu-id="f33ab-119">Olá **SceneChangeDetection** definição no Olá seguir predefinidas só pode ser definida tootrue se a codificação de vídeo de velocidade de transmissão única tooa.</span><span class="sxs-lookup"><span data-stu-id="f33ab-119">hello **SceneChangeDetection** setting in hello following preset can only be set tootrue if you are encoding tooa single  bitrate video.</span></span> <span data-ttu-id="f33ab-120">Se a codificação de transmissão múltipla tooa vídeo e defina **SceneChangeDetection** tootrue, codificador Olá devolve um erro.</span><span class="sxs-lookup"><span data-stu-id="f33ab-120">If you are encoding tooa multi-bitrate video and set **SceneChangeDetection** tootrue, hello encoder returns an error.</span></span>  
>
>

<span data-ttu-id="f33ab-121">Para obter informações sobre o esquema, consulte [isto](media-services-mes-schema.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="f33ab-121">For information about schema, see [this](media-services-mes-schema.md) topic.</span></span>

<span data-ttu-id="f33ab-122">Certifique-se de que tooreview Olá [considerações](#considerations) secção.</span><span class="sxs-lookup"><span data-stu-id="f33ab-122">Make sure tooreview hello [Considerations](#considerations) section.</span></span>

### <span data-ttu-id="f33ab-123"><a id="json"></a>Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-123"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": "true",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 4500,
              "MaxBitrate": 4500,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "ReferenceFrames": 3,
              "EntropyMode": "Cabac",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"

            }
          ],
          "Type": "H264Video"
        },
        {
          "JpgLayers": [
            {
              "Quality": 90,
              "Type": "JpgLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "{Best}",
          "Type": "JpgImage"
        },
        {
          "PngLayers": [
            {
              "Type": "PngLayer",
              "Width": 640,
              "Height": 360,
            }
          ],
          "Start": "00:00:01",
          "Step": "00:00:10",
          "Range": "00:00:58",
          "Type": "PngImage"
        },
        {
          "BmpLayers": [
            {
              "Type": "BmpLayer",
              "Width": 640,
              "Height": 360
            }
          ],
          "Start": "10%",
          "Step": "10%",
          "Range": "90%",
          "Type": "BmpImage"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "JpgFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "PngFormat"
          }
        },
        {
          "FileName": "{Basename}_{Index}{Extension}",
          "Format": {
            "Type": "BmpFormat"
          }
        },
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <span data-ttu-id="f33ab-124"><a id="xml"></a>Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-124"><a id="xml"></a>XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <SceneChangeDetection>true</SceneChangeDetection>
          <H264Layers>
            <H264Layer>
              <Bitrate>4500</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>4500</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
        <JpgImage Start="{Best}">
          <JpgLayers>
            <JpgLayer>
              <Width>640</Width>
              <Height>360</Height>
              <Quality>90</Quality>
            </JpgLayer>
          </JpgLayers>
        </JpgImage>
        <BmpImage Start="10%" Step="10%" Range="90%">
          <BmpLayers>
            <BmpLayer>
              <Width>640</Width>
              <Height>360</Height>
            </BmpLayer>
          </BmpLayers>
        </BmpImage>
        <PngImage Start="00:00:01" Step="00:00:10" Range="00:00:58">
          <PngLayers>
            <PngLayer>
              <Width>640</Width>
              <Height>360</Height>
            </PngLayer>
          </PngLayers>
        </PngImage>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <JpgFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <BmpFormat />
        </Output>
        <Output FileName="{Basename}_{Index}{Extension}">
          <PngFormat />
        </Output>
      </Outputs>
    </Preset>

### <a name="considerations"></a><span data-ttu-id="f33ab-125">Considerações</span><span class="sxs-lookup"><span data-stu-id="f33ab-125">Considerations</span></span>

<span data-ttu-id="f33ab-126">aplicar Olá seguintes considerações:</span><span class="sxs-lookup"><span data-stu-id="f33ab-126">hello following considerations apply:</span></span>

* <span data-ttu-id="f33ab-127">utilização Olá carimbos explícitas para iniciar/passo/intervalo assume que a origem de entrada Olá longo pelo menos 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="f33ab-127">hello use of explicit timestamps for Start/Step/Range assumes that hello input source is at least 1 minute long.</span></span>
* <span data-ttu-id="f33ab-128">Elementos de jpg/Png/BmpImage tem início, passo e os atributos de cadeia no intervalo – estes podem ser interpretados como:</span><span class="sxs-lookup"><span data-stu-id="f33ab-128">Jpg/Png/BmpImage elements have Start, Step, and Range string attributes – these can be interpreted as:</span></span>

  * <span data-ttu-id="f33ab-129">Número de moldura que se encontrem números inteiros de não negativo, por exemplo "Start": "120"</span><span class="sxs-lookup"><span data-stu-id="f33ab-129">Frame Number if they are non-negative integers, for example "Start": "120",</span></span>
  * <span data-ttu-id="f33ab-130">Duração de toosource relativo se expresso como %-o sufixo, por exemplo "Start": "15%", ou</span><span class="sxs-lookup"><span data-stu-id="f33ab-130">Relative toosource duration if expressed as %-suffixed, for example "Start": "15%", OR</span></span>
  * <span data-ttu-id="f33ab-131">Timestamp se expresso como hh: mm:...</span><span class="sxs-lookup"><span data-stu-id="f33ab-131">Timestamp if expressed as HH:MM:SS…</span></span> <span data-ttu-id="f33ab-132">Formatar, por exemplo "Start": "00: 01:00"</span><span class="sxs-lookup"><span data-stu-id="f33ab-132">format, for example "Start" : "00:01:00"</span></span>

    <span data-ttu-id="f33ab-133">Pode combinar e misturar notações como..</span><span class="sxs-lookup"><span data-stu-id="f33ab-133">You can mix and match notations as you please.</span></span>

    <span data-ttu-id="f33ab-134">Além disso, o início suporta também uma Macro especial: {melhores}, que tenta toodetermine Olá primeiro "interessantes" moldura do conteúdo de Olá Nota: (passo e o intervalo são ignoradas quando início está definido demasiado {melhor})</span><span class="sxs-lookup"><span data-stu-id="f33ab-134">Additionally, Start also supports a special Macro:{Best}, which attempts toodetermine hello first “interesting” frame of hello content NOTE: (Step and Range are ignored when Start is set too{Best})</span></span>
  * <span data-ttu-id="f33ab-135">As predefinições: Iniciar: {melhor}</span><span class="sxs-lookup"><span data-stu-id="f33ab-135">Defaults: Start:{Best}</span></span>
* <span data-ttu-id="f33ab-136">Formato de saída tem toobe explicitamente fornecido para cada formato de imagem: Png/Jpg/BmpFormat.</span><span class="sxs-lookup"><span data-stu-id="f33ab-136">Output format needs toobe explicitly provided for each Image format: Jpg/Png/BmpFormat.</span></span> <span data-ttu-id="f33ab-137">Quando presente, MES corresponde à JpgVideo tooJpgFormat e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="f33ab-137">When present, MES matches JpgVideo tooJpgFormat and so on.</span></span> <span data-ttu-id="f33ab-138">OutputFormat introduz uma nova Macro específico de imagem codec: {índice}, que necessita de toobe presente (uma vez e apenas uma vez) para formatos de saída de imagem.</span><span class="sxs-lookup"><span data-stu-id="f33ab-138">OutputFormat introduces a new image-codec specific Macro: {Index}, which needs toobe present (once and only once) for image output formats.</span></span>

## <span data-ttu-id="f33ab-139"><a id="trim_video"></a>Compactar um vídeo (recorte)</span><span class="sxs-lookup"><span data-stu-id="f33ab-139"><a id="trim_video"></a>Trim a video (clipping)</span></span>
<span data-ttu-id="f33ab-140">Este talks secção sobre como modificar o codificador de Olá predefinições tooclip ou compactar as vídeo de entrada olá onde Olá entrada é um ficheiro de mezanino so-called ou o ficheiro a pedido.</span><span class="sxs-lookup"><span data-stu-id="f33ab-140">This section talks about modifying hello encoder presets tooclip or trim hello input video where hello input is a so-called mezzanine file or on-demand file.</span></span> <span data-ttu-id="f33ab-141">Olá codificador também pode ser utilizado tooclip ou compactar um recurso, o que é capturado ou arquivado a partir de um fluxo em direto – Olá os detalhes para este estão disponíveis no [este blogue](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span><span class="sxs-lookup"><span data-stu-id="f33ab-141">hello encoder can also be used tooclip or trim an asset, which is captured or archived from a live stream – hello details for this are available in [this blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).</span></span>

<span data-ttu-id="f33ab-142">tootrim seus vídeos, pode efetuar qualquer uma das predefinições MES Olá documentadas [isto](media-services-mes-presets-overview.md) secção e modificar Olá **origens** elemento (tal como mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="f33ab-142">tootrim your videos, you can take any of hello MES presets documented [this](media-services-mes-presets-overview.md) section and modify hello **Sources** element (as shown below).</span></span> <span data-ttu-id="f33ab-143">Olá. o valor de StartTime tem toomatch Olá absoluto carimbos de vídeo de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="f33ab-143">hello value of StartTime needs toomatch hello absolute timestamps of hello input video.</span></span> <span data-ttu-id="f33ab-144">Por exemplo, se hello primeiro frame de vídeo de entrada Olá tem um carimbo de 12:00:10.000, em seguida, StartTime deve ser, pelo menos, 12:00:10.000 e superior.</span><span class="sxs-lookup"><span data-stu-id="f33ab-144">For example, if hello first frame of hello input video has a timestamp of 12:00:10.000, then StartTime should be at least 12:00:10.000 and greater.</span></span> <span data-ttu-id="f33ab-145">Exemplo de Olá abaixo, iremos partem do princípio de que o vídeo de entrada Olá tem um timestamp inicial igual a zero.</span><span class="sxs-lookup"><span data-stu-id="f33ab-145">In hello example below, we assume that hello input video has a starting timestamp of zero.</span></span> <span data-ttu-id="f33ab-146">**Origens** devem ser colocados no início Olá Olá predefinição.</span><span class="sxs-lookup"><span data-stu-id="f33ab-146">**Sources** should be placed at hello beginning of hello preset.</span></span>

### <span data-ttu-id="f33ab-147"><a id="json"></a>Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-147"><a id="json"></a>JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "StartTime": "00:00:04",
          "Duration": "00:00:16"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 3400,
              "MaxBitrate": 3400,
              "BufferWindow": "00:00:05",
              "Width": 1280,
              "Height": 720,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 2250,
              "MaxBitrate": 2250,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1500,
              "MaxBitrate": 1500,
              "BufferWindow": "00:00:05",
              "Width": 960,
              "Height": 540,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1000,
              "MaxBitrate": 1000,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 650,
              "MaxBitrate": 650,
              "BufferWindow": "00:00:05",
              "Width": 640,
              "Height": 360,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            },
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 400,
              "MaxBitrate": 400,
              "BufferWindow": "00:00:05",
              "Width": 320,
              "Height": 180,
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="xml-preset"></a><span data-ttu-id="f33ab-148">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-148">XML preset</span></span>
<span data-ttu-id="f33ab-149">tootrim seus vídeos, pode efetuar qualquer uma das predefinições MES Olá documentadas [aqui](media-services-mes-presets-overview.md) e modificar Olá **origens** elemento (tal como mostrado abaixo).</span><span class="sxs-lookup"><span data-stu-id="f33ab-149">tootrim your videos, you can take any of hello MES presets documented [here](media-services-mes-presets-overview.md) and modify hello **Sources** element (as shown below).</span></span>

    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source StartTime="PT4S" Duration="PT14S"/>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>3400</Bitrate>
              <Width>1280</Width>
              <Height>720</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>3400</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>2250</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>2250</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1500</Bitrate>
              <Width>960</Width>
              <Height>540</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1500</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>1000</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1000</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>650</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>650</MaxBitrate>
            </H264Layer>
            <H264Layer>
              <Bitrate>400</Bitrate>
              <Width>320</Width>
              <Height>180</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>3</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cabac</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>400</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <AACAudio>
          <Profile>AACLC</Profile>
          <Channels>2</Channels>
          <SamplingRate>48000</SamplingRate>
          <Bitrate>128</Bitrate>
        </AACAudio>
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}_{Width}x{Height}_{VideoBitrate}.mp4">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>

## <span data-ttu-id="f33ab-150"><a id="overlay"></a>Criar uma sobreposição</span><span class="sxs-lookup"><span data-stu-id="f33ab-150"><a id="overlay"></a>Create an overlay</span></span>

<span data-ttu-id="f33ab-151">Olá codificador de multimédia Standard permite-lhe toooverlay uma imagem para um vídeo existente.</span><span class="sxs-lookup"><span data-stu-id="f33ab-151">hello Media Encoder Standard allows you toooverlay an image onto an existing video.</span></span> <span data-ttu-id="f33ab-152">Atualmente, é suportado os seguintes formatos de Olá: png, jpg, gif e bmp.</span><span class="sxs-lookup"><span data-stu-id="f33ab-152">Currently, hello following formats are supported: png, jpg, gif, and bmp.</span></span> <span data-ttu-id="f33ab-153">Olá predefinição definida abaixo está um exemplo básico da sobreposição de vídeo.</span><span class="sxs-lookup"><span data-stu-id="f33ab-153">hello preset defined below is a basic example  of a video overlay.</span></span>

<span data-ttu-id="f33ab-154">Além disso toodefining um ficheiro predefinido, tem também toolet Media Services saber qual o ficheiro no recurso de Olá é a imagem de sobreposição de Olá e qual o ficheiro é vídeo de origem Olá em que pretende que a imagem de Olá toooverlay.</span><span class="sxs-lookup"><span data-stu-id="f33ab-154">In addition toodefining a preset file, you also have toolet Media Services know which file in hello asset is hello overlay image and which file is hello source video onto which you want toooverlay hello image.</span></span> <span data-ttu-id="f33ab-155">ficheiro de vídeo Olá tem toobe Olá **primário** ficheiro.</span><span class="sxs-lookup"><span data-stu-id="f33ab-155">hello video file has toobe hello **primary** file.</span></span>

<span data-ttu-id="f33ab-156">Se estiver a utilizar o .NET, adicione Olá seguintes duas funções de exemplo de .NET toohello definido no [isto](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tópico.</span><span class="sxs-lookup"><span data-stu-id="f33ab-156">If you are using .NET, add hello following two functions toohello .NET example defined in [this](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) topic.</span></span> <span data-ttu-id="f33ab-157">Olá **UploadMediaFilesFromFolder** função carregamentos de ficheiros a partir de uma pasta (por exemplo, BigBuckBunny.mp4 e Image001.png) e define Olá ficheiro toobe Olá primário ficheiro mp4 no recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="f33ab-157">hello **UploadMediaFilesFromFolder** function uploads files from a folder (for example, BigBuckBunny.mp4 and Image001.png) and sets hello mp4 file toobe hello primary file in hello asset.</span></span> <span data-ttu-id="f33ab-158">Olá **EncodeWithOverlay** função utiliza Olá personalizado predefinidas ficheiro que foi passado tooit (por exemplo, Olá predefinido dessa forma) toocreate Olá tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="f33ab-158">hello **EncodeWithOverlay** function uses hello custom preset file that was passed tooit (for example, hello preset that follows) toocreate hello encoding task.</span></span>


    static public IAsset UploadMediaFilesFromFolder(string folderPath)
    {
        IAsset asset = _context.Assets.CreateFromFolder(folderPath, AssetCreationOptions.None);
    
        foreach (var af in asset.AssetFiles)
        {
            // hello following code assumes 
            // you have an input folder with one MP4 and one overlay image file.
            if (af.Name.Contains(".mp4"))
                af.IsPrimary = true;
            else
                af.IsPrimary = false;
    
            af.Update();
        }
    
        return asset;
    }

    static public IAsset EncodeWithOverlay(IAsset assetSource, string customPresetFileName)
    {
        // Declare a new job.
        IJob job = _context.Jobs.Create("Media Encoder Standard Job");
        // Get a media processor reference, and pass tooit hello name of hello 
        // processor toouse for hello specific task.
        IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

        // Load hello XML (or JSON) from hello local file.
        string configuration = File.ReadAllText(customPresetFileName);

        // Create a task
        ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input assets toobe encoded.
        // This asset contains a source file and an overlay file.
        task.InputAssets.Add(assetSource);

        // Add an output asset toocontain hello results of hello job. 
        task.OutputAssets.AddNew("Output asset",
            AssetCreationOptions.None);

        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
        job.Submit();
        job.GetExecutionProgressTask(CancellationToken.None).Wait();

        return job.OutputMediaAssets[0];
    }


> [!NOTE]
> <span data-ttu-id="f33ab-159">Limitações atuais:</span><span class="sxs-lookup"><span data-stu-id="f33ab-159">Current limitations:</span></span>
>
> <span data-ttu-id="f33ab-160">definição de opacidade de sobreposição de Olá não é suportada.</span><span class="sxs-lookup"><span data-stu-id="f33ab-160">hello overlay opacity setting is not supported.</span></span>
>
> <span data-ttu-id="f33ab-161">O ficheiro de vídeo de origem e o ficheiro de imagem de sobreposição de Olá tem toobe no mesmo elemento de Olá e Olá conjunto do ficheiro de vídeo necessidades toobe como ficheiro principal Olá este recurso.</span><span class="sxs-lookup"><span data-stu-id="f33ab-161">Your source video file and hello overlay image file have toobe in hello same asset, and hello video file needs toobe set as hello primary file in this asset.</span></span>
>
>

### <a name="json-preset"></a><span data-ttu-id="f33ab-162">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-162">JSON preset</span></span>
    {
      "Version": 1.0,
      "Sources": [
        {
          "Streams": [],
          "Filters": {
            "VideoOverlay": {
              "Position": {
                "X": 100,
                "Y": 100,
                "Width": 100,
                "Height": 50
              },
              "AudioGainLevel": 0.0,
              "MediaParams": [
                {
                  "OverlayLoopCount": 1
                },
                {
                  "IsOverlay": true,
                  "OverlayLoopCount": 1,
                  "InputLoop": true
                }
              ],
              "Source": "Image001.png",
              "Clip": {
                "Duration": "00:00:05"
              },
              "FadeInDuration": {
                "Duration": "00:00:01"
              },
              "FadeOutDuration": {
                "StartTime": "00:00:03",
                "Duration": "00:00:04"
              }
            }
          },
          "Pad": true
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "H264Layers": [
            {
              "Profile": "Auto",
              "Level": "auto",
              "Bitrate": 1045,
              "MaxBitrate": 1045,
              "BufferWindow": "00:00:05",
              "ReferenceFrames": 3,
              "EntropyMode": "Cavlc",
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Type": "CopyAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}{Extension}",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }


### <a name="xml-preset"></a><span data-ttu-id="f33ab-163">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-163">XML preset</span></span>
    <?xml version="1.0" encoding="utf-16"?>
    <Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">
      <Sources>
        <Source>
          <Streams />
          <Filters>
            <VideoOverlay>
              <Source>Image001.png</Source>
              <Clip Duration="PT5S" />
              <FadeInDuration Duration="PT1S" />
              <FadeOutDuration StartTime="PT3S" Duration="PT4S" />
              <Position X="100" Y="100" Width="100" Height="50" />
              <Opacity>0</Opacity>
              <AudioGainLevel>0</AudioGainLevel>
              <MediaParams>
                <MediaParam>
                  <IsOverlay>false</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>false</InputLoop>
                </MediaParam>
                <MediaParam>
                  <IsOverlay>true</IsOverlay>
                  <OverlayLoopCount>1</OverlayLoopCount>
                  <InputLoop>true</InputLoop>
                </MediaParam>
              </MediaParams>
            </VideoOverlay>
          </Filters>
          <Pad>true</Pad>
        </Source>
      </Sources>
      <Encoding>
        <H264Video>
          <KeyFrameInterval>00:00:02</KeyFrameInterval>
          <H264Layers>
            <H264Layer>
              <Bitrate>1045</Bitrate>
              <Width>640</Width>
              <Height>360</Height>
              <FrameRate>0/1</FrameRate>
              <Profile>Auto</Profile>
              <Level>auto</Level>
              <BFrames>0</BFrames>
              <ReferenceFrames>3</ReferenceFrames>
              <Slices>0</Slices>
              <AdaptiveBFrame>true</AdaptiveBFrame>
              <EntropyMode>Cavlc</EntropyMode>
              <BufferWindow>00:00:05</BufferWindow>
              <MaxBitrate>1045</MaxBitrate>
            </H264Layer>
          </H264Layers>
        </H264Video>
        <CopyAudio />
      </Encoding>
      <Outputs>
        <Output FileName="{Basename}{Extension}">
          <MP4Format />
        </Output>
      </Outputs>
    </Preset>


## <span data-ttu-id="f33ab-164"><a id="silent_audio"></a>Inserir um registo de áudio automática quando a entrada não tem nenhum áudio</span><span class="sxs-lookup"><span data-stu-id="f33ab-164"><a id="silent_audio"></a>Insert a silent audio track when input has no audio</span></span>
<span data-ttu-id="f33ab-165">Por predefinição, se enviar um codificador de entrada toohello que contém apenas os vídeos e nenhum áudio, em seguida, Olá elemento de saída contém ficheiros que contêm as vídeos apenas dados.</span><span class="sxs-lookup"><span data-stu-id="f33ab-165">By default, if you send an input toohello encoder that contains only video, and no audio, then hello output asset contains files that contain only video data.</span></span> <span data-ttu-id="f33ab-166">Alguns jogadores não conseguir toohandle, esse fluxos de saída.</span><span class="sxs-lookup"><span data-stu-id="f33ab-166">Some players may not be able toohandle such output streams.</span></span> <span data-ttu-id="f33ab-167">Pode utilizar esta definição tooforce Olá codificador tooadd uma saída de toohello automática controlar áudio nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="f33ab-167">You can use this setting tooforce hello encoder tooadd a silent audio track toohello output in that scenario.</span></span>

<span data-ttu-id="f33ab-168">tooforce Olá codificador tooproduce um elemento que contenha um registo de áudio automática quando a entrada não tem nenhum áudio, especifique o valor de "InsertSilenceIfNoAudio" Olá.</span><span class="sxs-lookup"><span data-stu-id="f33ab-168">tooforce hello encoder tooproduce an asset that contains a silent audio track when input has no audio, specify hello "InsertSilenceIfNoAudio" value.</span></span>

<span data-ttu-id="f33ab-169">Pode efetuar qualquer uma das Olá MES predefinições documentadas em [isto](media-services-mes-presets-overview.md) secção e torne Olá modificação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f33ab-169">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

### <a name="json-preset"></a><span data-ttu-id="f33ab-170">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-170">JSON preset</span></span>
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a><span data-ttu-id="f33ab-171">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-171">XML preset</span></span>
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <span data-ttu-id="f33ab-172"><a id="deinterlacing"></a>Desativar anular interlacing automática</span><span class="sxs-lookup"><span data-stu-id="f33ab-172"><a id="deinterlacing"></a>Disable auto de-interlacing</span></span>
<span data-ttu-id="f33ab-173">Os clientes não precisam de toodo nada se estes como Olá interlace toobe conteúdos automaticamente entrelaçada anular.</span><span class="sxs-lookup"><span data-stu-id="f33ab-173">Customers don’t need toodo anything if they like hello interlace contents toobe automatically de-interlaced.</span></span> <span data-ttu-id="f33ab-174">Quando o Olá automática anular interlacing Olá (predefinição) MES Olá automaticamente a deteção de fotogramas entrelaçadas e apenas interlaces anular frames marcados como entrelaçadas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-174">When hello auto de-interlacing is on (default) hello MES does hello auto detection of interlaced frames and only de-interlaces frames marked as interlaced.</span></span>

<span data-ttu-id="f33ab-175">Pode desativar Olá anular interlacing automática.</span><span class="sxs-lookup"><span data-stu-id="f33ab-175">You can turn hello auto de-interlacing off.</span></span> <span data-ttu-id="f33ab-176">Esta opção não é recomendada.</span><span class="sxs-lookup"><span data-stu-id="f33ab-176">This option is not recommended.</span></span>

### <a name="json-preset"></a><span data-ttu-id="f33ab-177">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-177">JSON preset</span></span>
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a><span data-ttu-id="f33ab-178">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-178">XML preset</span></span>
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <span data-ttu-id="f33ab-179"><a id="audio_only"></a>Predefinições de só de áudio</span><span class="sxs-lookup"><span data-stu-id="f33ab-179"><a id="audio_only"></a>Audio-only presets</span></span>
<span data-ttu-id="f33ab-180">Esta secção demonstra predefinições MES dois só de áudio: AAC áudio e AAC boa qualidade áudio.</span><span class="sxs-lookup"><span data-stu-id="f33ab-180">This section demonstrates two audio-only MES presets: AAC Audio and AAC Good Quality Audio.</span></span>

### <a name="aac-audio"></a><span data-ttu-id="f33ab-181">Áudio AAC</span><span class="sxs-lookup"><span data-stu-id="f33ab-181">AAC Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

### <a name="aac-good-quality-audio"></a><span data-ttu-id="f33ab-182">Áudio de boa qualidade AAC</span><span class="sxs-lookup"><span data-stu-id="f33ab-182">AAC Good Quality Audio</span></span>
    {
      "Version": 1.0,
      "Codecs": [
        {
          "Profile": "AACLC",
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 192,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_AAC_{AudioBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="f33ab-183"><a id="concatenate"></a>Concatenar duas ou mais ficheiros de vídeo</span><span class="sxs-lookup"><span data-stu-id="f33ab-183"><a id="concatenate"></a>Concatenate two or more video files</span></span>

<span data-ttu-id="f33ab-184">Olá exemplo a seguir ilustra como pode gerar um tooconcatenate predefinida dois ou mais ficheiros de vídeo.</span><span class="sxs-lookup"><span data-stu-id="f33ab-184">hello following example illustrates how you can generate a preset tooconcatenate two or more video files.</span></span> <span data-ttu-id="f33ab-185">cenário mais comuns Olá é quando quiser tooadd um cabeçalho ou um vídeo de principais de toohello trailer.</span><span class="sxs-lookup"><span data-stu-id="f33ab-185">hello most common scenario is when you want tooadd a header or a trailer toohello main video.</span></span> <span data-ttu-id="f33ab-186">Olá destina-se de utilização é quando propriedades (resolução de vídeo, velocidade de fotogramas, contagem de controlar áudio, etc.) de partilha de ficheiros de vídeo Olá a ser editados em conjunto.</span><span class="sxs-lookup"><span data-stu-id="f33ab-186">hello intended use is when hello video files being edited together share  properties (video resolution, frame rate, audio track count, etc.).</span></span> <span data-ttu-id="f33ab-187">Deve asseguramos não toomix vídeos de taxas de moldura diferente ou com um número diferente de áudio controla.</span><span class="sxs-lookup"><span data-stu-id="f33ab-187">You should take care not toomix videos of different frame rates, or with different number of audio tracks.</span></span>

>[!NOTE]
><span data-ttu-id="f33ab-188">Olá de estrutura atual da funcionalidade de concatenação Olá espera que Olá entrada aplicações de clips de vídeos são consistentes em termos de resolução, velocidade de fotogramas etc.</span><span class="sxs-lookup"><span data-stu-id="f33ab-188">hello current design of hello concatenation feature expects that hello input video clips are consistent in terms of resolution, frame rate etc.</span></span> 

### <a name="requirements-and-considerations"></a><span data-ttu-id="f33ab-189">Requisitos e considerações</span><span class="sxs-lookup"><span data-stu-id="f33ab-189">Requirements and considerations</span></span>

* <span data-ttu-id="f33ab-190">Vídeos de entrada devem ter apenas um registo de áudio.</span><span class="sxs-lookup"><span data-stu-id="f33ab-190">Input videos should only have one audio track.</span></span>
* <span data-ttu-id="f33ab-191">Vídeos de entrada devem ter todos os Olá velocidade de fotogramas da mesma.</span><span class="sxs-lookup"><span data-stu-id="f33ab-191">Input videos should all have hello same frame rate.</span></span>
* <span data-ttu-id="f33ab-192">Tem de carregar os seus vídeos para recursos separados e definir vídeos Olá como ficheiro principal Olá cada recurso.</span><span class="sxs-lookup"><span data-stu-id="f33ab-192">You must upload your videos into separate assets and set hello videos as hello primary file in each asset.</span></span>
* <span data-ttu-id="f33ab-193">Terá de duração de Olá tooknow dos seus vídeos.</span><span class="sxs-lookup"><span data-stu-id="f33ab-193">You need tooknow hello duration of your videos.</span></span>
* <span data-ttu-id="f33ab-194">Olá predefinidos exemplos abaixo parte do princípio de que todos os vídeos de entrada de Olá começar com um carimbo de zero.</span><span class="sxs-lookup"><span data-stu-id="f33ab-194">hello preset examples below assumes that all hello input videos start with a timestamp of zero.</span></span> <span data-ttu-id="f33ab-195">Terá de valores de StartTime toomodify Olá se tem de vídeos de Olá timestamp inicial diferentes, como é normalmente caso de Olá de arquivos em direto.</span><span class="sxs-lookup"><span data-stu-id="f33ab-195">You need toomodify hello StartTime values if hello videos have different starting timestamp, as is typically hello case with live archives.</span></span>
* <span data-ttu-id="f33ab-196">Olá JSON predefinição torna referências explícitas toohello AssetID valores de ativos Olá de entrada.</span><span class="sxs-lookup"><span data-stu-id="f33ab-196">hello JSON preset makes explicit references toohello AssetID values of hello input assets.</span></span>
* <span data-ttu-id="f33ab-197">código de exemplo de Olá parte do princípio de que Olá que JSON da configuração predefinido foi guardada tooa ficheiro local, como "C:\supportFiles\preset.json".</span><span class="sxs-lookup"><span data-stu-id="f33ab-197">hello sample code assumes that hello JSON preset has been saved tooa local file, such as "C:\supportFiles\preset.json".</span></span> <span data-ttu-id="f33ab-198">Também parte do princípio que foram criados dois recursos através do carregamento de ficheiros de vídeo de dois e de que sabe Olá resultantes AssetID valores.</span><span class="sxs-lookup"><span data-stu-id="f33ab-198">It also assumes that two assets have been created by uploading two video files, and that you know hello resultant AssetID values.</span></span>
* <span data-ttu-id="f33ab-199">Olá fragmento de código e JSON predefinição mostra um exemplo de concatenar ficheiros de vídeo de dois.</span><span class="sxs-lookup"><span data-stu-id="f33ab-199">hello code snippet and JSON preset shows an example of concatenating two video files.</span></span> <span data-ttu-id="f33ab-200">Pode expandi-lo toomore que dois vídeos por:</span><span class="sxs-lookup"><span data-stu-id="f33ab-200">You can extend it toomore than two videos by:</span></span>

  1. <span data-ttu-id="f33ab-201">Chamar uma tarefa. InputAssets.Add() repetidamente tooadd mais vídeos, por ordem.</span><span class="sxs-lookup"><span data-stu-id="f33ab-201">Calling task.InputAssets.Add() repeatedly tooadd more videos, in order.</span></span>
  2. <span data-ttu-id="f33ab-202">Efetuar correspondente edita elemento toohello "origens" Olá JSON, ao adicionar mais entradas, Olá mesma ordem.</span><span class="sxs-lookup"><span data-stu-id="f33ab-202">Making corresponding edits toohello "Sources" element in hello JSON, by adding more entries, in hello same order.</span></span>

### <a name="net-code"></a><span data-ttu-id="f33ab-203">Código de .NET</span><span class="sxs-lookup"><span data-stu-id="f33ab-203">.NET code</span></span>

    IAsset asset1 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:606db602-efd7-4436-97b4-c0b867ba195b").FirstOrDefault();
    IAsset asset2 = _context.Assets.Where(asset => asset.Id == "nb:cid:UUID:a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e").FirstOrDefault();

    // Declare a new job.
    IJob job = _context.Jobs.Create("Media Encoder Standard Job for Concatenating Videos");
    // Get a media processor reference, and pass tooit hello name of the
    // processor toouse for hello specific task.
    IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

    // Load hello XML (or JSON) from hello local file.
    string configuration = File.ReadAllText(@"c:\supportFiles\preset.json");

    // Create a task
    ITask task = job.Tasks.AddNew("Media Encoder Standard encoding task",
        processor,
        configuration,
        TaskOptions.None);

    // Specify hello input videos toobe concatenated (in order).
    task.InputAssets.Add(asset1);
    task.InputAssets.Add(asset2);
    // Add an output asset toocontain hello results of hello job.
    // This output is specified as AssetCreationOptions.None, which
    // means hello output asset is not encrypted.
    task.OutputAssets.AddNew("Output asset",
        AssetCreationOptions.None);

    job.StateChanged += new EventHandler<JobStateChangedEventArgs>(JobStateChanged);
    job.Submit();
    job.GetExecutionProgressTask(CancellationToken.None).Wait();

### <a name="json-preset"></a><span data-ttu-id="f33ab-204">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-204">JSON preset</span></span>

<span data-ttu-id="f33ab-205">Atualize o seu personalizado com ids de ativos de Olá que pretende que o tooconcatenate e através de segmento de momento adequado Olá para cada vídeo da configuração predefinido.</span><span class="sxs-lookup"><span data-stu-id="f33ab-205">Update your custom preset with ids of hello assets that you want tooconcatenate, and with hello appropriate time segment for each video.</span></span>

    {
      "Version": 1.0,
      "Sources": [
        {
          "AssetID": "606db602-efd7-4436-97b4-c0b867ba195b",
          "StartTime": "00:00:01",
          "Duration": "00:00:15"
        },
        {
          "AssetID": "a7e2b90f-0565-4a94-87fe-0a9fa07b9c7e",
          "StartTime": "00:00:02",
          "Duration": "00:00:05"
        }
      ],
      "Codecs": [
        {
          "KeyFrameInterval": "00:00:02",
          "SceneChangeDetection": true,
          "H264Layers": [
            {
              "Level": "auto",
              "Bitrate": 1800,
              "MaxBitrate": 1800,
              "BufferWindow": "00:00:05",
              "BFrames": 3,
              "ReferenceFrames": 3,
              "AdaptiveBFrame": true,
              "Type": "H264Layer",
              "Width": "640",
              "Height": "360",
              "FrameRate": "0/1"
            }
          ],
          "Type": "H264Video"
        },
        {
          "Channels": 2,
          "SamplingRate": 48000,
          "Bitrate": 128,
          "Type": "AACAudio"
        }
      ],
      "Outputs": [
        {
          "FileName": "{Basename}_{Width}x{Height}_{VideoBitrate}.mp4",
          "Format": {
            "Type": "MP4Format"
          }
        }
      ]
    }

## <span data-ttu-id="f33ab-206"><a id="crop"></a>Vídeos de cortar com o codificador de multimédia Standard</span><span class="sxs-lookup"><span data-stu-id="f33ab-206"><a id="crop"></a>Crop videos with Media Encoder Standard</span></span>
<span data-ttu-id="f33ab-207">Consulte Olá [recortar vídeos com o codificador de multimédia Standard](media-services-crop-video.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="f33ab-207">See hello [Crop videos with Media Encoder Standard](media-services-crop-video.md) topic.</span></span>

## <span data-ttu-id="f33ab-208"><a id="no_video"></a>Inserir um vídeo controlar quando a entrada não tem nenhum vídeo</span><span class="sxs-lookup"><span data-stu-id="f33ab-208"><a id="no_video"></a>Insert a video track when input has no video</span></span>

<span data-ttu-id="f33ab-209">Por predefinição, se enviar um codificador de entrada toohello que contém apenas áudio e vídeo de nenhuma, em seguida, Olá elemento de saída contém ficheiros que contêm dados de áudio apenas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-209">By default, if you send an input toohello encoder that contains only audio, and no video, then hello output asset contains files that contain only audio data.</span></span> <span data-ttu-id="f33ab-210">Alguns jogadores, incluindo o leitor de multimédia do Azure (consulte [isto](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) pode não ser capaz de toohandle esses fluxos.</span><span class="sxs-lookup"><span data-stu-id="f33ab-210">Some players, including Azure Media Player (see [this](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) may not be able toohandle such streams.</span></span> <span data-ttu-id="f33ab-211">Pode utilizar esta definição tooforce Olá codificador tooadd uma saída de toohello monochrome controlar vídeo nesse cenário.</span><span class="sxs-lookup"><span data-stu-id="f33ab-211">You can use this setting tooforce hello encoder tooadd a monochrome video track toohello output in that scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="f33ab-212">Forçar Olá codificador tooinsert um saída controlar vídeo aumenta Olá tamanho de Olá elemento de saída e assim Olá custo tarifas de Olá codificação tarefas.</span><span class="sxs-lookup"><span data-stu-id="f33ab-212">Forcing hello encoder tooinsert an output video track increases hello size of hello output Asset, and thereby hello cost incurred for hello encoding Task.</span></span> <span data-ttu-id="f33ab-213">Deve executar testes tooverify que este aumento resultante tem apenas um impacto modest no seu encargos mensais.</span><span class="sxs-lookup"><span data-stu-id="f33ab-213">You should run tests tooverify that this resultant increase has only a modest impact on your monthly charges.</span></span>
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a><span data-ttu-id="f33ab-214">A inserção de vídeo no apenas Olá mais baixa de velocidade de transmissão</span><span class="sxs-lookup"><span data-stu-id="f33ab-214">Inserting video at only hello lowest bitrate</span></span>

<span data-ttu-id="f33ab-215">Suponhamos que está a utilizar uma velocidade de transmissão vários codificação predefinido, tal como ["H264 múltipla 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode toda a sua entrada de catálogo para transmissão em fluxo, que contém uma mistura de ficheiros de vídeo e ficheiros só de áudio.</span><span class="sxs-lookup"><span data-stu-id="f33ab-215">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="f33ab-216">Neste cenário, quando a entrada de Olá não tem nenhum vídeo, poderá ser útil tooforce Olá codificador tooinsert em tons monocromáticos vídeo controlar em apenas Olá menor velocidade de transmissão, como tooinserting oposição ao vídeo em cada velocidade de transmissão de saída.</span><span class="sxs-lookup"><span data-stu-id="f33ab-216">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at just hello lowest bitrate, as opposed tooinserting video at every output bitrate.</span></span> <span data-ttu-id="f33ab-217">tooachieve isto, terá de toouse Olá **InsertBlackIfNoVideoBottomLayerOnly** sinalizador.</span><span class="sxs-lookup"><span data-stu-id="f33ab-217">tooachieve this, you need toouse hello **InsertBlackIfNoVideoBottomLayerOnly** flag.</span></span>

<span data-ttu-id="f33ab-218">Pode efetuar qualquer uma das Olá MES predefinições documentadas em [isto](media-services-mes-presets-overview.md) secção e torne Olá modificação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f33ab-218">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="f33ab-219">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-219">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="f33ab-220">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-220">XML preset</span></span>

<span data-ttu-id="f33ab-221">Quando utilizar XML, utilize condição = "InsertBlackIfNoVideoBottomLayerOnly" como um atributo toohello **H264Video** o elemento e a condição = "InsertSilenceIfNoAudio" como um atributo demasiado**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="f33ab-221">When using XML, use Condition="InsertBlackIfNoVideoBottomLayerOnly" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideoBottomLayerOnly">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .
```

### <a name="inserting-video-at-all-output-bitrates"></a><span data-ttu-id="f33ab-222">Inserir em todas as vídeo de saída de forma</span><span class="sxs-lookup"><span data-stu-id="f33ab-222">Inserting video at all output bitrates</span></span>
<span data-ttu-id="f33ab-223">Suponhamos que está a utilizar uma velocidade de transmissão vários codificação predefinido, tal como ["H264 múltipla 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode toda a sua entrada de catálogo para transmissão em fluxo, que contém uma mistura de ficheiros de vídeo e ficheiros só de áudio.</span><span class="sxs-lookup"><span data-stu-id="f33ab-223">Suppose you are using a multiple bitrate encoding preset such as ["H264 Multiple Bitrate 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode your entire input catalog for streaming, which contains a mix of video files and audio-only files.</span></span> <span data-ttu-id="f33ab-224">Neste cenário, quando a entrada de Olá não tem nenhum vídeo, poderá ser útil tooforce Olá codificador tooinsert um vídeo monochrome controlar em todos os Olá de forma de saída.</span><span class="sxs-lookup"><span data-stu-id="f33ab-224">In this scenario, when hello input has no video, you may want tooforce hello encoder tooinsert a monochrome video track at all hello output bitrates.</span></span> <span data-ttu-id="f33ab-225">Isto garante que a saída ativos são todos os homogéneo com relativamente toonumber de vídeo controla e controla áudio.</span><span class="sxs-lookup"><span data-stu-id="f33ab-225">This ensures that your output Assets are all homogenous with respect toonumber of video tracks and audio tracks.</span></span> <span data-ttu-id="f33ab-226">tooachieve isto, terá de toospecify Olá sinalizador "InsertBlackIfNoVideo".</span><span class="sxs-lookup"><span data-stu-id="f33ab-226">tooachieve this, you need toospecify hello "InsertBlackIfNoVideo" flag.</span></span>

<span data-ttu-id="f33ab-227">Pode efetuar qualquer uma das Olá MES predefinições documentadas em [isto](media-services-mes-presets-overview.md) secção e torne Olá modificação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="f33ab-227">You can take any of hello MES presets documented in [this](media-services-mes-presets-overview.md) section, and make hello following modification:</span></span>

#### <a name="json-preset"></a><span data-ttu-id="f33ab-228">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-228">JSON preset</span></span>
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a><span data-ttu-id="f33ab-229">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-229">XML preset</span></span>

<span data-ttu-id="f33ab-230">Quando utilizar XML, utilize condição = "InsertBlackIfNoVideo" como um atributo toohello **H264Video** o elemento e a condição = "InsertSilenceIfNoAudio" como um atributo demasiado**AACAudio**.</span><span class="sxs-lookup"><span data-stu-id="f33ab-230">When using XML, use Condition="InsertBlackIfNoVideo" as an attribute toohello **H264Video** element and  Condition="InsertSilenceIfNoAudio" as an attribute too**AACAudio**.</span></span>

```
. . .
<Encoding>
  <H264Video Condition="InsertBlackIfNoVideo">
    <KeyFrameInterval>00:00:02</KeyFrameInterval>
    <SceneChangeDetection>true</SceneChangeDetection>
    <StretchMode>AutoSize</StretchMode>
    <H264Layers>
      <H264Layer>
        . . .
      </H264Layer>
    </H264Layers>
    <Chapters />
  </H264Video>
  <AACAudio Condition="InsertSilenceIfNoAudio">
    <Profile>AACLC</Profile>
    <Channels>2</Channels>
    <SamplingRate>48000</SamplingRate>
    <Bitrate>128</Bitrate>
  </AACAudio>
</Encoding>
. . .  
```

## <span data-ttu-id="f33ab-231"><a id="rotate_video"></a>Roda um vídeo</span><span class="sxs-lookup"><span data-stu-id="f33ab-231"><a id="rotate_video"></a>Rotate a video</span></span>
<span data-ttu-id="f33ab-232">Olá [codificador de multimédia Standard](media-services-dotnet-encode-with-media-encoder-standard.md) suporta rotação pelos ângulos de 0/90/180/270.</span><span class="sxs-lookup"><span data-stu-id="f33ab-232">hello [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) supports rotation by angles of 0/90/180/270.</span></span> <span data-ttu-id="f33ab-233">comportamento predefinido de Olá é "Auto", onde tenta toodetect Olá rotação metadados no ficheiro de vídeo de entrada de Olá e compensá-lo.</span><span class="sxs-lookup"><span data-stu-id="f33ab-233">hello default behavior is "Auto", where it tries toodetect hello rotation metadata in hello incoming video file and compensate for it.</span></span> <span data-ttu-id="f33ab-234">Incluem Olá seguinte **origens** tooone de elemento de predefinições de Olá definido no [isto](media-services-mes-presets-overview.md) secção:</span><span class="sxs-lookup"><span data-stu-id="f33ab-234">Include hello following **Sources** element tooone of hello presets defined in [this](media-services-mes-presets-overview.md) section:</span></span>

### <a name="json-preset"></a><span data-ttu-id="f33ab-235">Predefinição JSON</span><span class="sxs-lookup"><span data-stu-id="f33ab-235">JSON preset</span></span>
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...
### <a name="xml-preset"></a><span data-ttu-id="f33ab-236">Predefinição XML</span><span class="sxs-lookup"><span data-stu-id="f33ab-236">XML preset</span></span>
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

<span data-ttu-id="f33ab-237">Além disso, consulte [isto](media-services-mes-schema.md#PreserveResolutionAfterRotation) tópico para obter mais informações sobre como o codificador de Olá interpreta as definições de largura e altura Olá no Olá da configuração predefinida, quando é acionada compensação de rotação.</span><span class="sxs-lookup"><span data-stu-id="f33ab-237">Also, see [this](media-services-mes-schema.md#PreserveResolutionAfterRotation) topic for more information on how hello encoder interprets hello Width and Height settings in hello preset, when rotation compensation is triggered.</span></span>

<span data-ttu-id="f33ab-238">Pode utilizar Olá valor "0" tooindicate toohello codificador tooignore rotação metadados, se estiver presente, vídeo de entrada Olá.</span><span class="sxs-lookup"><span data-stu-id="f33ab-238">You can use hello value "0" tooindicate toohello encoder tooignore rotation metadata, if present, in hello input video.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f33ab-239">Percursos de aprendizagem dos Media Services</span><span class="sxs-lookup"><span data-stu-id="f33ab-239">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f33ab-240">Enviar comentários</span><span class="sxs-lookup"><span data-stu-id="f33ab-240">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="f33ab-241">Veja Também</span><span class="sxs-lookup"><span data-stu-id="f33ab-241">See Also</span></span>
[<span data-ttu-id="f33ab-242">Descrição geral de codificação de serviços de multimédia</span><span class="sxs-lookup"><span data-stu-id="f33ab-242">Media Services Encoding Overview</span></span>](media-services-encode-asset.md)
