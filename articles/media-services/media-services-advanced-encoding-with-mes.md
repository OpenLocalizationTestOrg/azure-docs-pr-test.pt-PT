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
# <a name="perform-advanced-encoding-by-customizing-mes-presets"></a>Efetuar a codificação avançadas personalizando MES predefinições 

## <a name="overview"></a>Descrição geral

Este tópico mostra como as predefinições de toocustomize codificador de multimédia Standard. Olá [codificação com o codificador de multimédia Standard utilizando predefinições personalizadas](media-services-custom-mes-presets-with-dotnet.md) tópico mostra como toouse .NET toocreate uma codificação de tarefas e uma tarefa que executa esta tarefa. Uma vez, personalizar uma predefinição, alimentação Olá predefinições personalizado toohello codificação tarefas. 

>[!NOTE]
>Se utilizar uma predefinição XML, certifique-se de que toopreserve Olá ordem elementos, conforme mostrado nos exemplos XML abaixo (por exemplo, KeyFrameInterval deve preceder SceneChangeDetection).
>

Neste tópico, predefinições de personalizado Olá que efetuar Olá seguintes tarefas de codificação são demonstradas.

## <a name="support-for-relative-sizes"></a>Suporte para tamanhos de relativos

Quando a gerar miniaturas, não terá de especificar tooalways saída largura e altura em pixéis. Pode especificá-las em percentagens, no intervalo de Olá [% 1,..., 100%].

### <a name="json-preset"></a>Predefinição JSON
    "Width": "100%",
    "Height": "100%"

### <a name="xml-preset"></a>Predefinição XML
    <Width>100%</Width>
    <Height>100%</Height>

## <a id="thumbnails"></a>Gerar miniaturas

Esta secção mostra como toocustomize uma predefinição que gera miniaturas. Olá predefinição definida abaixo contém informações sobre a forma como pretende tooencode o ficheiro, bem como informações necessárias toogenerate miniaturas. Pode efetuar qualquer uma das predefinições MES Olá documentadas [isto](media-services-mes-presets-overview.md) secção e adicione o código que gera miniaturas.  

> [!NOTE]
> Olá **SceneChangeDetection** definição no Olá seguir predefinidas só pode ser definida tootrue se a codificação de vídeo de velocidade de transmissão única tooa. Se a codificação de transmissão múltipla tooa vídeo e defina **SceneChangeDetection** tootrue, codificador Olá devolve um erro.  
>
>

Para obter informações sobre o esquema, consulte [isto](media-services-mes-schema.md) tópico.

Certifique-se de que tooreview Olá [considerações](#considerations) secção.

### <a id="json"></a>Predefinição JSON
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


### <a id="xml"></a>Predefinição XML
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

### <a name="considerations"></a>Considerações

aplicar Olá seguintes considerações:

* utilização Olá carimbos explícitas para iniciar/passo/intervalo assume que a origem de entrada Olá longo pelo menos 1 minuto.
* Elementos de jpg/Png/BmpImage tem início, passo e os atributos de cadeia no intervalo – estes podem ser interpretados como:

  * Número de moldura que se encontrem números inteiros de não negativo, por exemplo "Start": "120"
  * Duração de toosource relativo se expresso como %-o sufixo, por exemplo "Start": "15%", ou
  * Timestamp se expresso como hh: mm:... Formatar, por exemplo "Start": "00: 01:00"

    Pode combinar e misturar notações como..

    Além disso, o início suporta também uma Macro especial: {melhores}, que tenta toodetermine Olá primeiro "interessantes" moldura do conteúdo de Olá Nota: (passo e o intervalo são ignoradas quando início está definido demasiado {melhor})
  * As predefinições: Iniciar: {melhor}
* Formato de saída tem toobe explicitamente fornecido para cada formato de imagem: Png/Jpg/BmpFormat. Quando presente, MES corresponde à JpgVideo tooJpgFormat e assim sucessivamente. OutputFormat introduz uma nova Macro específico de imagem codec: {índice}, que necessita de toobe presente (uma vez e apenas uma vez) para formatos de saída de imagem.

## <a id="trim_video"></a>Compactar um vídeo (recorte)
Este talks secção sobre como modificar o codificador de Olá predefinições tooclip ou compactar as vídeo de entrada olá onde Olá entrada é um ficheiro de mezanino so-called ou o ficheiro a pedido. Olá codificador também pode ser utilizado tooclip ou compactar um recurso, o que é capturado ou arquivado a partir de um fluxo em direto – Olá os detalhes para este estão disponíveis no [este blogue](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).

tootrim seus vídeos, pode efetuar qualquer uma das predefinições MES Olá documentadas [isto](media-services-mes-presets-overview.md) secção e modificar Olá **origens** elemento (tal como mostrado abaixo). Olá. o valor de StartTime tem toomatch Olá absoluto carimbos de vídeo de entrada Olá. Por exemplo, se hello primeiro frame de vídeo de entrada Olá tem um carimbo de 12:00:10.000, em seguida, StartTime deve ser, pelo menos, 12:00:10.000 e superior. Exemplo de Olá abaixo, iremos partem do princípio de que o vídeo de entrada Olá tem um timestamp inicial igual a zero. **Origens** devem ser colocados no início Olá Olá predefinição.

### <a id="json"></a>Predefinição JSON
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

### <a name="xml-preset"></a>Predefinição XML
tootrim seus vídeos, pode efetuar qualquer uma das predefinições MES Olá documentadas [aqui](media-services-mes-presets-overview.md) e modificar Olá **origens** elemento (tal como mostrado abaixo).

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

## <a id="overlay"></a>Criar uma sobreposição

Olá codificador de multimédia Standard permite-lhe toooverlay uma imagem para um vídeo existente. Atualmente, é suportado os seguintes formatos de Olá: png, jpg, gif e bmp. Olá predefinição definida abaixo está um exemplo básico da sobreposição de vídeo.

Além disso toodefining um ficheiro predefinido, tem também toolet Media Services saber qual o ficheiro no recurso de Olá é a imagem de sobreposição de Olá e qual o ficheiro é vídeo de origem Olá em que pretende que a imagem de Olá toooverlay. ficheiro de vídeo Olá tem toobe Olá **primário** ficheiro.

Se estiver a utilizar o .NET, adicione Olá seguintes duas funções de exemplo de .NET toohello definido no [isto](media-services-custom-mes-presets-with-dotnet.md#encoding_with_dotnet) tópico. Olá **UploadMediaFilesFromFolder** função carregamentos de ficheiros a partir de uma pasta (por exemplo, BigBuckBunny.mp4 e Image001.png) e define Olá ficheiro toobe Olá primário ficheiro mp4 no recurso de Olá. Olá **EncodeWithOverlay** função utiliza Olá personalizado predefinidas ficheiro que foi passado tooit (por exemplo, Olá predefinido dessa forma) toocreate Olá tarefa de codificação.


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
> Limitações atuais:
>
> definição de opacidade de sobreposição de Olá não é suportada.
>
> O ficheiro de vídeo de origem e o ficheiro de imagem de sobreposição de Olá tem toobe no mesmo elemento de Olá e Olá conjunto do ficheiro de vídeo necessidades toobe como ficheiro principal Olá este recurso.
>
>

### <a name="json-preset"></a>Predefinição JSON
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


### <a name="xml-preset"></a>Predefinição XML
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


## <a id="silent_audio"></a>Inserir um registo de áudio automática quando a entrada não tem nenhum áudio
Por predefinição, se enviar um codificador de entrada toohello que contém apenas os vídeos e nenhum áudio, em seguida, Olá elemento de saída contém ficheiros que contêm as vídeos apenas dados. Alguns jogadores não conseguir toohandle, esse fluxos de saída. Pode utilizar esta definição tooforce Olá codificador tooadd uma saída de toohello automática controlar áudio nesse cenário.

tooforce Olá codificador tooproduce um elemento que contenha um registo de áudio automática quando a entrada não tem nenhum áudio, especifique o valor de "InsertSilenceIfNoAudio" Olá.

Pode efetuar qualquer uma das Olá MES predefinições documentadas em [isto](media-services-mes-presets-overview.md) secção e torne Olá modificação os seguintes:

### <a name="json-preset"></a>Predefinição JSON
    {
      "Channels": 2,
      "SamplingRate": 44100,
      "Bitrate": 96,
      "Type": "AACAudio",
      "Condition": "InsertSilenceIfNoAudio"
    }

### <a name="xml-preset"></a>Predefinição XML
    <AACAudio Condition="InsertSilenceIfNoAudio">
      <Channels>2</Channels>
      <SamplingRate>44100</SamplingRate>
      <Bitrate>96</Bitrate>
    </AACAudio>

## <a id="deinterlacing"></a>Desativar anular interlacing automática
Os clientes não precisam de toodo nada se estes como Olá interlace toobe conteúdos automaticamente entrelaçada anular. Quando o Olá automática anular interlacing Olá (predefinição) MES Olá automaticamente a deteção de fotogramas entrelaçadas e apenas interlaces anular frames marcados como entrelaçadas.

Pode desativar Olá anular interlacing automática. Esta opção não é recomendada.

### <a name="json-preset"></a>Predefinição JSON
    "Sources": [
    {
     "Filters": {
        "Deinterlace": {
          "Mode": "Off"
        }
      },
    }
    ]

### <a name="xml-preset"></a>Predefinição XML
    <Sources>
    <Source>
      <Filters>
        <Deinterlace>
          <Mode>Off</Mode>
        </Deinterlace>
      </Filters>
    </Source>
    </Sources>


## <a id="audio_only"></a>Predefinições de só de áudio
Esta secção demonstra predefinições MES dois só de áudio: AAC áudio e AAC boa qualidade áudio.

### <a name="aac-audio"></a>Áudio AAC
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

### <a name="aac-good-quality-audio"></a>Áudio de boa qualidade AAC
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

## <a id="concatenate"></a>Concatenar duas ou mais ficheiros de vídeo

Olá exemplo a seguir ilustra como pode gerar um tooconcatenate predefinida dois ou mais ficheiros de vídeo. cenário mais comuns Olá é quando quiser tooadd um cabeçalho ou um vídeo de principais de toohello trailer. Olá destina-se de utilização é quando propriedades (resolução de vídeo, velocidade de fotogramas, contagem de controlar áudio, etc.) de partilha de ficheiros de vídeo Olá a ser editados em conjunto. Deve asseguramos não toomix vídeos de taxas de moldura diferente ou com um número diferente de áudio controla.

>[!NOTE]
>Olá de estrutura atual da funcionalidade de concatenação Olá espera que Olá entrada aplicações de clips de vídeos são consistentes em termos de resolução, velocidade de fotogramas etc. 

### <a name="requirements-and-considerations"></a>Requisitos e considerações

* Vídeos de entrada devem ter apenas um registo de áudio.
* Vídeos de entrada devem ter todos os Olá velocidade de fotogramas da mesma.
* Tem de carregar os seus vídeos para recursos separados e definir vídeos Olá como ficheiro principal Olá cada recurso.
* Terá de duração de Olá tooknow dos seus vídeos.
* Olá predefinidos exemplos abaixo parte do princípio de que todos os vídeos de entrada de Olá começar com um carimbo de zero. Terá de valores de StartTime toomodify Olá se tem de vídeos de Olá timestamp inicial diferentes, como é normalmente caso de Olá de arquivos em direto.
* Olá JSON predefinição torna referências explícitas toohello AssetID valores de ativos Olá de entrada.
* código de exemplo de Olá parte do princípio de que Olá que JSON da configuração predefinido foi guardada tooa ficheiro local, como "C:\supportFiles\preset.json". Também parte do princípio que foram criados dois recursos através do carregamento de ficheiros de vídeo de dois e de que sabe Olá resultantes AssetID valores.
* Olá fragmento de código e JSON predefinição mostra um exemplo de concatenar ficheiros de vídeo de dois. Pode expandi-lo toomore que dois vídeos por:

  1. Chamar uma tarefa. InputAssets.Add() repetidamente tooadd mais vídeos, por ordem.
  2. Efetuar correspondente edita elemento toohello "origens" Olá JSON, ao adicionar mais entradas, Olá mesma ordem.

### <a name="net-code"></a>Código de .NET

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

### <a name="json-preset"></a>Predefinição JSON

Atualize o seu personalizado com ids de ativos de Olá que pretende que o tooconcatenate e através de segmento de momento adequado Olá para cada vídeo da configuração predefinido.

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

## <a id="crop"></a>Vídeos de cortar com o codificador de multimédia Standard
Consulte Olá [recortar vídeos com o codificador de multimédia Standard](media-services-crop-video.md) tópico.

## <a id="no_video"></a>Inserir um vídeo controlar quando a entrada não tem nenhum vídeo

Por predefinição, se enviar um codificador de entrada toohello que contém apenas áudio e vídeo de nenhuma, em seguida, Olá elemento de saída contém ficheiros que contêm dados de áudio apenas. Alguns jogadores, incluindo o leitor de multimédia do Azure (consulte [isto](https://feedback.azure.com/forums/169396-azure-media-services/suggestions/8082468-audio-only-scenarios)) pode não ser capaz de toohandle esses fluxos. Pode utilizar esta definição tooforce Olá codificador tooadd uma saída de toohello monochrome controlar vídeo nesse cenário.

> [!NOTE]
> Forçar Olá codificador tooinsert um saída controlar vídeo aumenta Olá tamanho de Olá elemento de saída e assim Olá custo tarifas de Olá codificação tarefas. Deve executar testes tooverify que este aumento resultante tem apenas um impacto modest no seu encargos mensais.
>

### <a name="inserting-video-at-only-hello-lowest-bitrate"></a>A inserção de vídeo no apenas Olá mais baixa de velocidade de transmissão

Suponhamos que está a utilizar uma velocidade de transmissão vários codificação predefinido, tal como ["H264 múltipla 720p"](media-services-mes-preset-h264-multiple-bitrate-720p.md) tooencode toda a sua entrada de catálogo para transmissão em fluxo, que contém uma mistura de ficheiros de vídeo e ficheiros só de áudio. Neste cenário, quando a entrada de Olá não tem nenhum vídeo, poderá ser útil tooforce Olá codificador tooinsert em tons monocromáticos vídeo controlar em apenas Olá menor velocidade de transmissão, como tooinserting oposição ao vídeo em cada velocidade de transmissão de saída. tooachieve isto, terá de toouse Olá **InsertBlackIfNoVideoBottomLayerOnly** sinalizador.

Pode efetuar qualquer uma das Olá MES predefinições documentadas em [isto](media-services-mes-presets-overview.md) secção e torne Olá modificação os seguintes:

#### <a name="json-preset"></a>Predefinição JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideoBottomLayerOnly",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Predefinição XML

Quando utilizar XML, utilize condição = "InsertBlackIfNoVideoBottomLayerOnly" como um atributo toohello **H264Video** o elemento e a condição = "InsertSilenceIfNoAudio" como um atributo demasiado**AACAudio**.

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

### <a name="inserting-video-at-all-output-bitrates"></a>Inserir em todas as vídeo de saída de forma
Suponhamos que está a utilizar uma velocidade de transmissão vários codificação predefinido, tal como ["H264 múltipla 720p](media-services-mes-preset-H264-Multiple-Bitrate-720p.md) tooencode toda a sua entrada de catálogo para transmissão em fluxo, que contém uma mistura de ficheiros de vídeo e ficheiros só de áudio. Neste cenário, quando a entrada de Olá não tem nenhum vídeo, poderá ser útil tooforce Olá codificador tooinsert um vídeo monochrome controlar em todos os Olá de forma de saída. Isto garante que a saída ativos são todos os homogéneo com relativamente toonumber de vídeo controla e controla áudio. tooachieve isto, terá de toospecify Olá sinalizador "InsertBlackIfNoVideo".

Pode efetuar qualquer uma das Olá MES predefinições documentadas em [isto](media-services-mes-presets-overview.md) secção e torne Olá modificação os seguintes:

#### <a name="json-preset"></a>Predefinição JSON
    {
          "KeyFrameInterval": "00:00:02",
          "StretchMode": "AutoSize",
          "Condition": "InsertBlackIfNoVideo",
          "H264Layers": [
          …
          ]
    }

#### <a name="xml-preset"></a>Predefinição XML

Quando utilizar XML, utilize condição = "InsertBlackIfNoVideo" como um atributo toohello **H264Video** o elemento e a condição = "InsertSilenceIfNoAudio" como um atributo demasiado**AACAudio**.

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

## <a id="rotate_video"></a>Roda um vídeo
Olá [codificador de multimédia Standard](media-services-dotnet-encode-with-media-encoder-standard.md) suporta rotação pelos ângulos de 0/90/180/270. comportamento predefinido de Olá é "Auto", onde tenta toodetect Olá rotação metadados no ficheiro de vídeo de entrada de Olá e compensá-lo. Incluem Olá seguinte **origens** tooone de elemento de predefinições de Olá definido no [isto](media-services-mes-presets-overview.md) secção:

### <a name="json-preset"></a>Predefinição JSON
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
### <a name="xml-preset"></a>Predefinição XML
    <Sources>
           <Source>
          <Streams />
          <Filters>
            <Rotation>90</Rotation>
          </Filters>
        </Source>
    </Sources>

Além disso, consulte [isto](media-services-mes-schema.md#PreserveResolutionAfterRotation) tópico para obter mais informações sobre como o codificador de Olá interpreta as definições de largura e altura Olá no Olá da configuração predefinida, quando é acionada compensação de rotação.

Pode utilizar Olá valor "0" tooindicate toohello codificador tooignore rotação metadados, se estiver presente, vídeo de entrada Olá.

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Veja Também
[Descrição geral de codificação de serviços de multimédia](media-services-encode-asset.md)
