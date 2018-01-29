---
title: "Esquema de metadados de saída de Media Services do Azure | Microsoft Docs"
description: "O tópico fornece uma descrição geral do esquema de metadados de saída de Media Services do Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: c8792535eeeb71e7233c42bd9ea2a446a1c4d43c
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/08/2018
---
# <a name="output-metadata"></a>Metadados de saída
## <a name="overview"></a>Descrição geral
Uma tarefa de codificação está associada a um recurso de entrada (ou ativos) no qual pretende efetuar algumas tarefas de codificação. Por exemplo, codificar um ficheiro MP4 264 MP4 de velocidade de transmissão adaptável conjuntos; criar uma miniatura; Crie as Sobreposições. Após a conclusão de uma tarefa, é produzido um elemento de saída.  O elemento de saída contém as vídeo, áudio, as miniaturas, etc. O elemento de saída também contém um ficheiro com os metadados sobre o elemento de saída. O nome do ficheiro XML de metadados tem o seguinte formato: &lt;source_file_name&gt;_manifest.xml (por exemplo, BigBuckBunny_manifest.xml).  

Se pretender examinar o ficheiro de metadados, pode criar um **SAS** localizador e transferir o ficheiro para o seu computador local.  

Este artigo descreve os elementos e tipos de esquema XML nos quais o metada de saída (&lt;source_file_name&gt;_manifest.xml) baseia-se. Para obter informações sobre o ficheiro que contém metadados sobre o recurso de entrada, consulte [metadados entrada](media-services-input-metadata-schema.md).  

> [!NOTE]
> Pode encontrar o código de conclusão de esquema e o exemplo XML no final deste artigo.  
>
>

## <a name="AssetFiles "></a>Elemento de raiz AssetFiles
Coleção de AssetFile entradas para a tarefa de codificação.  

### <a name="child-elements"></a>Elementos subordinados
| Nome | Descrição |
| --- | --- |
| **AssetFile**<br/><br/> minOccurs = maxOccurs "0" = "1" |Um [AssetFile elemento](media-services-output-metadata-schema.md) que é uma parte da coleção AssetFiles. |

## <a name="AssetFile "></a>Elemento AssetFile
Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Nome**<br/><br/> Necessário |**xs:String** |O nome de ficheiro de recurso de multimédia. |
| **Tamanho**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:Long** |Tamanho do ficheiro de recurso em bytes. |
| **Duração**<br/><br/> Necessário |**xs: DURATION** |Duração de back-play conteúdo. |

### <a name="child-elements"></a>Elementos subordinados
| Nome | Descrição |
| --- | --- |
| **Origens** |Coleção de ficheiros de suporte de dados de entrada/origem, que foi processada para produzir este AssetFile. Para obter mais informações, consulte [elemento origem](media-services-output-metadata-schema.md). |
| **VideoTracks**<br/><br/> minOccurs = maxOccurs "0" = "1" |Cada AssetFile físico pode conter na mesma vídeos zero ou mais controla interleaved para um formato de contentor adequado. Para obter mais informações, consulte [VideoTracks elemento](media-services-output-metadata-schema.md). |
| **AudioTracks**<br/><br/> minOccurs = maxOccurs "0" = "1" |Cada AssetFile físico pode conter zero ou mais controla áudio interleaved para um formato de contentor adequado no mesmo. Esta é uma coleção de todos os esses controla áudio. Para obter mais informações, consulte [AudioTracks elemento](media-services-output-metadata-schema.md). |

## <a name="Sources "></a>Elemento de origens
Coleção de ficheiros de suporte de dados de entrada/origem, que foi processada para produzir este AssetFile.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos subordinados
| Nome | Descrição |
| --- | --- |
| **Origem**<br/><br/> minOccurs = maxOccurs "1" = "unbounded" |Um ficheiro de origem de entrada/utilizado ao gerar este recurso. Para obter mais informações, consulte [elemento origem](media-services-output-metadata-schema.md). |

## <a name="Source "></a>Elemento de origem
Um ficheiro de origem de entrada/utilizado ao gerar este recurso.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **Nome**<br/><br/> Necessário |**xs:String** |Nome de ficheiro de origem de entrada. |

## <a name="VideoTracks "></a>Elemento VideoTracks
Cada AssetFile físico pode conter na mesma vídeos zero ou mais controla interleaved para um formato de contentor adequado. O **VideoTracks** elemento representa uma coleção de todas as controla as vídeo.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos subordinados
| Nome | Descrição |
| --- | --- |
| **VideoTrack**<br/><br/> minOccurs = maxOccurs "1" = "unbounded" |Controlar de vídeo específico no principal AssetFile. Para obter mais informações, consulte [VideoTrack elemento](media-services-output-metadata-schema.md#VideoTrack). |

## <a name="VideoTrack"></a>Elemento VideoTrack
Controlar de vídeo específico no principal AssetFile.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **ID**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Índice baseado em zero de controlar este vídeo. **Nota:** isto **Id** não é necessariamente TrackID como utilizado num ficheiro MP4. |
| **FourCC**<br/><br/> Necessário |**xs:String** |Codec vídeo FourCC código. |
| **Perfil** |**xs:String** |Perfil de H264 (apenas aplicável a H264 codec). |
| **Nível** |**xs:String** |Nível de H264 (apenas aplicável a H264 codec). |
| **Largura**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Codificado as vídeo largura em pixéis. |
| **Altura**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Altura de vídeo codificada em pixels. |
| **DisplayAspectRatioNumerator**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:Double** |Vídeo proporção numerator. |
| **DisplayAspectRatioDenominator**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:Double** |Denominador de proporção de vídeo. |
| **Framerate**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:decimal** |Taxa de moldura de vídeo no formato .3f de medida. |
| **TargetFramerate**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:decimal** |Taxa de vídeo frame de destino no formato .3f da configuração predefinida. |
| **Velocidade de transmissão**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Taxa de bits de vídeo médio no kilobits por segundo, conforme calculada a partir de AssetFile. Contagens apenas o payload de fluxo de estatísticas básicas e não inclui a sobrecarga de empacotamento. |
| **TargetBitrate**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Destino de velocidade de transmissão média para controlar este vídeo, conforme foi pedido através dos predefinidas, na codificação de kilobits por segundo. |
| **MaxGOPBitrate**<br/><br/> minInclusive = "0" |**xs:int** |Máx. GOP média velocidade de transmissão para este vídeo controlar, no kilobits por segundo. |

## <a name="AudioTracks "></a>Elemento AudioTracks
Cada AssetFile físico pode conter zero ou mais controla áudio interleaved para um formato de contentor adequado no mesmo. O **AudioTracks** elemento representa uma coleção de todos os esses controla áudio.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementos subordinados
| Nome | Descrição |
| --- | --- |
| **AudioTrack**<br/><br/> minOccurs = maxOccurs "1" = "unbounded" |Controlar áudio específico no principal AssetFile. Para obter mais informações, consulte [AudioTrack elemento](media-services-output-metadata-schema.md). |

## <a name="AudioTrack "></a>Elemento AudioTrack
Controlar áudio específico no principal AssetFile.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **ID**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Índice baseado em zero deste controlar áudio. **Nota:** esta não é necessariamente TrackID como utilizado num ficheiro MP4. |
| **Codec** |**xs:String** |Cadeia de codec de áudio controlar. |
| **EncoderVersion** |**xs:String** |Cadeia de versão do codificador opcional, necessária para EAC3. |
| **Canais**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Número de canais de áudio. |
| **SamplingRate**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Frequência de amostragem de áudio em amostras/seg ou Hz. |
| **Velocidade de transmissão**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Taxa de bits de áudio médio em bits por segundo, conforme calculada a partir de AssetFile. Contagens apenas o payload de fluxo de estatísticas básicas e não inclui a sobrecarga de empacotamento. |
| **BitsPerSample**<br/><br/> minInclusive = "0"<br/><br/> Necessário |**xs:int** |Bits por exemplo, para o formato de wFormatTag escreva. |

### <a name="child-elements"></a>Elementos subordinados
| Nome | Descrição |
| --- | --- |
| **LoudnessMeteringResultParameters**<br/><br/> minOccurs = maxOccurs "0" = "1" |Parâmetros de medição de loudness resultado. Para obter mais informações, consulte [LoudnessMeteringResultParameters elemento](media-services-output-metadata-schema.md). |

## <a name="LoudnessMeteringResultParameters "></a>Elemento LoudnessMeteringResultParameters
Parâmetros de medição de loudness resultado.  

Pode encontrar um exemplo XML [exemplo XML](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Atributos
| Nome | Tipo | Descrição |
| --- | --- | --- |
| **DPLMVersionInformation** |**xs:String** |**Dolby** loudness profissionais versão do kit de desenvolvimento de medição. |
| **DialogNormalization**<br/><br/> minInclusive = maxInclusive "-31" = "-1"<br/><br/> Necessário |**xs:int** |DialogNormalization gerado através de DPLM, é necessário quando LoudnessMetering está definido |
| **IntegratedLoudness**<br/><br/> minInclusive = maxInclusive "-70" = "10"<br/><br/> Necessário |**xs:float** |Loudness integrada |
| **IntegratedLoudnessUnit**<br/><br/> Necessário |**xs:String** |Unidade de loudness integrada. |
| **IntegratedLoudnessGatingMethod**<br/><br/> Necessário |**xs:String** |Identificador de controlo |
| **IntegratedLoudnessSpeechPercentage**<br/><br/> minInclusive = "0" maxInclusive = "100" |**xs:float** |Conteúdo de reconhecimento de voz através do programa, como uma percentagem. |
| **SamplePeak**<br/><br/> Necessário |**xs:float** |Valor de exemplo absoluto das horas de ponta, desde repor ou uma vez que foi efetuada a última limpo, por canal.  As unidades são dBFS. |
| **SamplePeakUnit**<br/><br/> corrigido = "dBFS"<br/><br/> Necessário |**xs:anySimpleType** |Unidade de pico de exemplo. |
| **TruePeak**<br/><br/> Necessário |**xs:float** |Máximo de pico verdadeiro valor, de acordo com ITU-R BS.1770-2, desde repor ou uma vez que foi efetuada a última limpo por canal. As unidades são dBTP. |
| **TruePeakUnit**<br/><br/> corrigido = "dBTP"<br/><br/> Necessário |**xs:anySimpleType** |Unidade de pico verdadeiro. |

## <a name="schema-code"></a>Código de esquema
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Width" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video width in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Height" use="required">  
                              <xs:annotation>  
                                <xs:documentation>encoded video height in pixels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:double">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Framerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="MaxGOPBitrate">  
                              <xs:annotation>  
                                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Channels" use="required">  
                              <xs:annotation>  
                                <xs:documentation>number of audio channels</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="SamplingRate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>the media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <a name="xml"></a>Exemplo XML

O seguinte XML é um exemplo de ficheiro de metadados de saída.  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Passos Seguintes
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
