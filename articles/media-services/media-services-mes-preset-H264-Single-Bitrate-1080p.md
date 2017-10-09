---
title: "velocidade de transmissão única do aaaH264 1080p codificador de multimédia Standard da configuração predefinida - Azure | Microsoft Docs"
description: "tópico de Olá proporcione uma descrição geral de Olá * * H264 de velocidade de transmissão única p 1080 * * tarefas predefinição."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0951fea8-15af-420b-9648-8c5c1abf8173
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: e06c68e3372c7f1e5903413840c118e2c3426168
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="h264-single-bitrate-1080p"></a><span data-ttu-id="c3972-103">H264 Velocidade de transmissão única 1080p</span><span class="sxs-lookup"><span data-stu-id="c3972-103">H264 Single Bitrate 1080p</span></span>
<span data-ttu-id="c3972-104">`Media Encoder Standard`Define um conjunto de predefinições, que pode utilizar quando criar tarefas de codificação de codificação.</span><span class="sxs-lookup"><span data-stu-id="c3972-104">`Media Encoder Standard` defines a set of encoding presets you can use when creating encoding jobs.</span></span> <span data-ttu-id="c3972-105">Pode utilizar um `preset name` toospecify no qual o formato de que gostaria de tooencode o ficheiro de suporte de dados.</span><span class="sxs-lookup"><span data-stu-id="c3972-105">You can either use a `preset name` toospecify into which format you would like tooencode your media file.</span></span> <span data-ttu-id="c3972-106">Em alternativa, pode criar os seus próprios JSON ou predefinições baseado em XML (utilizando a codificação UTF-8 ou UTF-16.</span><span class="sxs-lookup"><span data-stu-id="c3972-106">Or, you can create your own JSON or XML-based presets (using UTF-8 or UTF-16 encoding.</span></span> <span data-ttu-id="c3972-107">Em seguida, seria passar codificador personalizado toohello predefinidas de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3972-107">You would then pass hello custom preset toohello encoder.</span></span> <span data-ttu-id="c3972-108">Para Olá obter lista de todos os Olá predefinido nomes suportados por este `Media Encoder Standard` codificador, consulte [predefinições de tarefas para o codificador de multimédia Standard](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3972-108">For hello list of all hello preset names supported by this `Media Encoder Standard` encoder, see [Task Presets for Media Encoder Standard](media-services-mes-presets-overview.md).</span></span>  
  
 <span data-ttu-id="c3972-109">Este tópico mostra Olá `H264 Single Bitrate 1080p` no formato XML e o JSON da configuração predefinida.</span><span class="sxs-lookup"><span data-stu-id="c3972-109">This topic shows hello `H264 Single Bitrate 1080p` preset in XML and JSON format.</span></span>  
  
 <span data-ttu-id="c3972-110">Este ficheiro predefinidas produz um único MP4 com velocidade de transmissão de 6750 kbps e stereo áudio AAC.</span><span class="sxs-lookup"><span data-stu-id="c3972-110">This preset produces a single MP4 file with a bitrate of 6750 kbps, and stereo AAC audio.</span></span> <span data-ttu-id="c3972-111">Para obter informações detalhadas sobre o perfil, velocidade de transmissão, fazendo a amostragem taxa, etc. Isto da configuração predefinida, examine Olá XML ou JSON definido abaixo.</span><span class="sxs-lookup"><span data-stu-id="c3972-111">For detailed information about profile, bitrate, sampling rate, etc. of this preset, examine hello XML or JSON defined below.</span></span> <span data-ttu-id="c3972-112">Para explicações de que cada elemento estas predefinições significa e os valores válidos de Olá para cada elemento, consulte Olá [esquema codificador de multimédia Standard](media-services-mes-schema.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="c3972-112">For explanations of what each element in these presets means, and hello valid values for each element, see hello [Media Encoder Standard schema](media-services-mes-schema.md) topic.</span></span>  
  
 <span data-ttu-id="c3972-113">XML</span><span class="sxs-lookup"><span data-stu-id="c3972-113">XML</span></span>  
  
```  
<?xml version="1.0" encoding="utf-16"?>  
<Preset xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="1.0" xmlns="http://www.windowsazure.com/media/encoding/Preset/2014/03">  
  <Encoding>  
    <H264Video>  
      <KeyFrameInterval>00:00:02</KeyFrameInterval>  
      <SceneChangeDetection>true</SceneChangeDetection>  
      <H264Layers>  
        <H264Layer>  
          <Bitrate>6750</Bitrate>  
          <Width>1920</Width>  
          <Height>1080</Height>  
          <FrameRate>0/1</FrameRate>  
          <Profile>Auto</Profile>  
          <Level>auto</Level>  
          <BFrames>3</BFrames>  
          <ReferenceFrames>3</ReferenceFrames>  
          <Slices>0</Slices>  
          <AdaptiveBFrame>true</AdaptiveBFrame>  
          <EntropyMode>Cabac</EntropyMode>  
          <BufferWindow>00:00:05</BufferWindow>  
          <MaxBitrate>6750</MaxBitrate>  
        </H264Layer>  
      </H264Layers>  
      <Chapters />  
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
```  
  
 <span data-ttu-id="c3972-114">JSON</span><span class="sxs-lookup"><span data-stu-id="c3972-114">JSON</span></span>  
  
```  
{  
  "Version": 1.0,  
  "Codecs": [  
    {  
      "KeyFrameInterval": "00:00:02",  
      "SceneChangeDetection": true,  
      "H264Layers": [  
        {  
          "Profile": "Auto",  
          "Level": "auto",  
          "Bitrate": 6750,  
          "MaxBitrate": 6750,  
          "BufferWindow": "00:00:05",  
          "Width": 1920,  
          "Height": 1080,  
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
```
