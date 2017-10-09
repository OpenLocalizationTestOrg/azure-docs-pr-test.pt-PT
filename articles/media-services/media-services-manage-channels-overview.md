---
title: "aaaOverview de em direto de transmissão em fluxo utilizando os Media Services do Azure | Microsoft Docs"
description: "Este tópico fornece uma descrição geral da transmissão em direto com Media Services do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: fb63502e-914d-4c1f-853c-4a7831bb08e8
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: edc49069db6b491902bdcbb808b1974858cc92f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-live-streaming-using-azure-media-services"></a>Descrição geral em direto de transmissão em fluxo utilizando os Media Services do Azure
## <a name="overview"></a>Descrição geral
Quando distribui direta eventos com Media Services do Azure de transmissão em fluxo Olá os seguintes componentes está normalmente relacionado:

* Uma câmara, que é utilizado toobroadcast um evento.
* Um codificador vídeo em direto que converte sinais da Olá câmara toostreams que são enviados tooa em direto de serviço de transmissão em fluxo.

    Opcionalmente, vários codificadores com sincronização de hora em direto. Para determinados eventos críticos em direto que a pedido muito elevada disponibilidade e qualidade da experiência, recomenda-se tooemploy ativo-ativo codificadores com tempo sincronização tooachieve ativação pós-falha totalmente integrada sem perda de dados.
* Um serviço transmissão em fluxo em direto que permite-lhe Olá toodo seguintes:

  * inserir conteúdos em direto utilizando vários protocolos de transmissão em fluxo em direto (por exemplo, RTMP ou Transmissão em Fluxo Uniforme)
  * (opcionalmente) codificação da sua transmissão para uma transmissão em fluxo de velocidade de transmissão adaptável
  * pré-visualizar a sua transmissão em fluxo em direto
  * registo e o arquivo de conteúdo de Olá ingerido na ordem toobe transmissão em fluxo posterior (vídeo a pedido)
  * Distribuir os conteúdos de Olá através de protocolos de transmissão em fluxo comuns (por exemplo, MPEG DASH, uniforme, HLS) diretamente os clientes de tooyour ou tooa rede de entrega de conteúdos (CDN) para uma maior distribuição.

**Serviços de suporte de dados do Microsoft Azure** (AMS) fornecem Olá tooingest de capacidade, codificar, pré-visualizar, armazenar e distribuir os seus conteúdos de transmissão em fluxo em direto.

Quando distribui o conteúdo toocustomers o seu objetivo é toodeliver um dispositivos toovarious vídeo de alta qualidade em condições de rede diferente. tooachieve isto, utilize live codificadores tooencode o fluxo de vídeo de transmissão múltipla (velocidade de transmissão adaptável) do fluxo tooa.  tootake care of de transmissão em fluxo em dispositivos diferentes, utilizar os Media Services [empacotamento dinâmico](media-services-dynamic-packaging-overview.md) toodynamically novamente os protocolos de toodifferent de fluxo do pacote. Os Media Services suportam fornecimento de Olá seguintes tecnologias de transmissão em fluxo velocidade de transmissão adaptável: HTTP Live Streaming (HLS), transmissão em fluxo uniforme, MPEG DASH.

Nos Media Services do Azure, **canais**, **programas**, e **lidam** identificador em direto de Olá todas as funcionalidades, incluindo inserção, formatação, DVR, transmissão em fluxo segurança, escalabilidade e redundância.

Um **Canal** representa um pipeline de processamento de conteúdos de transmissão em fluxo em direto. Um canal pode receber em direto de entrada fluxos no Olá seguintes formas:

* Um codificador em direto no local envia múltipla **RTMP** ou **transmissão em fluxo uniforme** (MP4 fragmentado) toohello canal configurado para **pass-through** entrega. Olá **pass-through** entrega é quando fluxos Olá ingerido pass-through **canal**s sem qualquer processamento adicional. Pode utilizar os seguintes codificadores em direto que saída de transmissão múltipla transmissão em fluxo uniforme de Olá: MediaExcel, Ateme, Imagine comunicações, Envivio, Cisco e elementar. Olá seguintes codificadores em direto de saída RTMP: Adobe Flash suporte de dados em direto codificador (FMLE), Telestream Wirecast, Haivision, Teradek e Transcodificadores tricaster.  Um codificador em direto pode também enviar um canal de tooa de fluxo de velocidade de transmissão única que não está ativado para live encoding, mas que não é recomendada. Quando solicitado, os Media Services disponibilizam Olá fluxo toocustomers.

  > [!NOTE]
  > A utilização de um método pass-through é a forma mais económica Olá toodo live transmissão em fluxo quando estão a fazer vários eventos durante um longo período de tempo e já investiu em codificadores no local. Consulte os detalhes dos [preços](https://azure.microsoft.com/pricing/details/media-services/).
  > 
  > 
* Um codificador em direto no local envia um fluxo de velocidade de transmissão única toohello canal, que é ativada tooperform live encoding com Media Services dos seguintes formatos de Olá: RTMP ou transmissão em fluxo uniforme (MP4 fragmentados). RTP (MPEG-TS) também é suportada, fornecida tem um ligação dedicada toohello Datacenter do Azure. Olá seguintes codificadores em direto com RTMP são conhecidos toowork com canais deste tipo de saída: Telestream Wirecast, FMLE. Olá canal, em seguida, efetua a codificação em direto de entrada Olá fluxo tooa transmissão múltipla (adaptável) vídeo de transmissão única. Quando solicitado, os Media Services disponibilizam Olá fluxo toocustomers.

A partir da versão de Olá 2.10 de serviços de suporte de dados, quando criar um canal, pode especificar de que forma pretende que o canal tooreceive Olá o fluxo de entrada e se pretende ou não pretende para Olá canal tooperform live encoding da sua transmissão em fluxo. Tem duas opções:

* **Nenhum** (pass-through) – especificar este valor, se planear toouse um codificador em direto no local, que será de saída do fluxo de transmissão múltipla (uma sequência de pass-through). Neste caso, transmissão em fluxo recebida Olá passem toohello sem qualquer tipo de codificação de saída. Este é o comportamento de Olá de uma versão anterior too2.10 do canal.  
* **Standard** – escolha este valor, se planear toouse dos Media Services tooencode sua transmissão em fluxo em direto toomulti velocidade de transmissão múltipla. Este método é mais económico para como aumentar verticalmente rapidamente para eventos pouco frequentes. Lembre-se de que existe um impacto de faturação para live encoding e deve Lembre-se de que sai de um canal de codificação em direto no estado de "Em execução" Olá resultará em encargos faturação.  É recomendado que pare imediatamente os canais executar após o evento de transmissão em fluxo em direto é concluída tooavoid encargos extra por hora.

## <a name="comparison-of-channel-types"></a>Comparação dos tipos de canal
A tabela seguinte fornece um guia toocomparing Olá dois tipos de canal suportados nos Media Services

| Funcionalidade | Canal pass-through | Canal de padrão |
| --- | --- | --- |
| Entrada de velocidade de transmissão única é codificada em múltiplos de forma na nuvem de Olá |Não |Sim |
| Resolução máxima, número de camadas |1080p, 8 camadas, 60 + fps |720p, 6 camadas, 30 fps |
| Protocolos de entrada |RTMP, transmissão em fluxo de uniforme |RTMP, transmissão em fluxo uniforme e RTP |
| Preço |Consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/media-services/) e clique no separador "Vídeo em direto" |Consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/media-services/) |
| Tempo de execução máximo |24x7 |8 horas |
| Suporte para inserir slates |Não |Sim |
| Suporte para ad sinalização |Não |Sim |
| Legendas de CEA 608/708 pass-through |Sim |Sim |
| Capacidade toorecover de breves stalls no feed de contribuição |Sim |Não (canal começará slating após 6 + segundos w/o dados de entrada) |
| Suporte para GOPs de entrada não uniforme |Sim |Não – entrada têm de ser corrigida seg 2 GOPs |
| Suporte para a entrada de taxa de moldura variável |Sim |Não – entrada têm de ser corrigida velocidade de fotogramas.<br/>Variações secundárias são tolerated, por exemplo, durante em segundo plano do movimento elevada. Mas o codificador não é possível remover too10 fotogramas por segundo. |
| Auto-shutoff de canais de entrada quando feed está perdido |Não |Após 12 horas, se não houver nenhum programa em execução |

## <a name="working-with-channels-that-receive-multi-bitrate-live-stream-from-on-premises-encoders-pass-through"></a>Trabalhar com Canais que recebem transmissões em fluxo em direto com velocidade de transmissão múltipla a partir de codificadores no local (pass-through)
Olá diagrama seguinte mostra Olá principais partes da plataforma de Olá AMS envolvidas no Olá **pass-through** fluxo de trabalho.

![Fluxo de trabalho em direto](./media/media-services-live-streaming-workflow/media-services-live-streaming-current.png)

Para obter mais informações, consulte [Trabalhar com Canais que recebem transmissões em Fluxo em Direto de Múltipla Velocidade de Transmissão a partir de Codificadores no Local](media-services-live-streaming-with-onprem-encoders.md).

## <a name="working-with-channels-that-are-enabled-tooperform-live-encoding-with-azure-media-services"></a>Trabalhar com canais que estão ativadas tooperform em direto de encoding com Media Services do Azure
Olá diagrama seguinte mostra Olá principais partes da plataforma de AMS Olá envolvidas no fluxo de trabalho de transmissão em fluxo em direto onde um canal é ativado tooperform em direto de encoding com Media Services.

![Fluxo de trabalho em direto](./media/media-services-live-streaming-workflow/media-services-live-streaming-new.png)

Para obter mais informações, consulte [trabalhar com canais que é tooPerform ativado em direto Encoding com Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md).

## <a name="description-of-a-channel-and-its-related-components"></a>Descrição de um canal e os respetivos componentes relacionados
### <a name="channel"></a>Canal
Nos Media Services, [canal](https://docs.microsoft.com/rest/api/media/operations/channel)s são responsáveis por processar o conteúdo de transmissão em fluxo em direto. Um canal fornece um ponto final de entrada (URL de inserção) que, em seguida, fornecer transcoder em direto tooa. canal de Olá recebe fluxos de entrada em direto de transcoder em direto Olá e torna a mesma disponível para transmissão em fluxo através de um ou mais lidam. Canais também fornecem um ponto final de pré-visualização (URL de pré-visualização) que utilize toopreview e validar a sua transmissão em fluxo antes do processamento adicional e entrega.

Pode obter Olá ingestão de URL e o URL de pré-visualização de Olá quando criar o canal de Olá. tooget estes URLs, canal de Olá não tem toobe no estado de Olá foi iniciado. Quando estiver pronto toostart enviar por push dados de um transcoder em direto no canal Olá, o canal de Olá tem de ser iniciado. Assim que for iniciada transcoder em direto Olá a ingestão de dados, pode pré-visualizar a transmissão.

Cada conta de Media Services pode conter vários canais, vários programas e lidam vários. Consoante as necessidades de segurança e de largura de banda de Olá, StreamingEndpoint serviços podem ser tooone dedicado ou mais canais. Qualquer StreamingEndpoint pode solicitar a partir de qualquer canal.

### <a name="program"></a>Programa
A [programa](https://docs.microsoft.com/rest/api/media/operations/program) permite-lhe a publicação de Olá toocontrol e armazenamento de segmentos numa transmissão em fluxo em direto. Canais gerem Programas. Olá relação canal e o programa é muito semelhante tootraditional suporte de dados em que um canal tem uma transmissão em fluxo constante de conteúdo e um programa é confinada toosome excedeu o tempo limite de evento nesse canal.
Pode especificar Olá número de horas que pretende tooretain Olá registada conteúdo para o programa de Olá por definição Olá **ArchiveWindowLength** propriedade. Este valor pode ser definido a partir de um mínimo de máximo de tooa de 5 minutos de 25 horas.

ArchiveWindowLength dita também Olá período de tempo máximo os clientes podem recuar a partir da posição atual em direto Olá. Programas podem ser executados ao longo do período de tempo especificado Olá, mas o conteúdo que se situe atrás da duração da janela Olá é continuamente descartado. Este valor desta propriedade também determina o cliente de Olá quanto possam crescer manifestos.

Cada programa está associado um Elemento. programa de Olá toopublish tem de criar um localizador para Olá associadas ao recurso. Ter este localizador irá permitir toobuild um URL de transmissão em fluxo que pode fornecer tooyour clientes.

Um canal suporta até toothree programas a executar em simultâneo para que possa criar vários arquivos do Olá mesmo fluxo de entrada. Isto permite-lhe toopublish e arquivar diferentes partes de um evento conforme necessário. Por exemplo, o requisito comercial será tooarchive 6 horas de um programa mas toobroadcast apenas últimos 10 minutos. tooaccomplish isto, terá de programas em execução em simultâneo de dois toocreate. Um programa está definido tooarchive 6 horas do evento de Olá mas Olá programa não está publicado. Olá outro programa está definido tooarchive durante 10 minutos e este programa está publicado.

## <a name="billing-implications"></a>Implicações de faturação
Um canal começa assim que faz a transição de estado de demasiado "em execução" através de Olá API de faturação.  

Olá tabela seguinte mostra como os Estados de canal mapeiam Estados toobilling Olá API e o portal do Azure. Tenha em atenção que são ligeiramente diferentes entre Olá API e Portal UX. Olá Estados Assim que um canal está no estado "Em execução" de Olá através de Olá API ou num Olá "Pronto" ou "Transmissão em fluxo" no portal do Azure de Olá, faturação estará ativa.

Canal de Olá toostop de faturação mais, tiver tooStop Olá canal através de Olá API ou em Olá portal do Azure.
É responsável por parar os canais quando tiver terminado com o canal de Olá. Canal de Olá falha toostop irá resultar no faturação contínua.

> [!NOTE]
> Ao trabalhar com canais padrão, AMS será automaticamente shutoff nenhum canal que ainda está no estado "Em execução" 12 horas depois de feed de entrada Olá perde-se e existem não existem programas em execução. No entanto, pode ainda será faturado por Olá de tempo de Olá que canal estava num estado "Em execução".
>
>

### <a id="states"></a>Estados de canal e a forma como efectuam o mapeamento toohello modo de faturação
estado atual Olá de um canal. Os valores possíveis incluem:

* **Parado**. Isto é Estado inicial Olá Olá canal após a respetiva criação (a menos que autostart tiver sido selecionada no portal de Olá.) Não existem faturação ocorre neste estado. Neste estado, podem ser atualizadas as propriedades de canal de Olá mas não é permitida a transmissão em fluxo.
* **Iniciar**. Olá canal está a ser iniciada. Não existem faturação ocorre neste estado. Não são permitidas transmissões em fluxo nem atualizações durante este estado. Se ocorrer um erro, Olá canal devolve toohello estado parado.
* **Executar**. Olá canal é capaz de processar fluxos em direto. Agora, está faturação utilização. Tem de parar Olá canal tooprevent ainda mais a faturação.
* **Parar**. Olá canal está a ser parado. Não existem faturação ocorre neste estado transitório. Não são permitidas transmissões em fluxo nem atualizações durante este estado.
* **Eliminar**. Olá canal está a ser eliminada. Não existem faturação ocorre neste estado transitório. Não são permitidas transmissões em fluxo nem atualizações durante este estado.

Olá tabela seguinte mostra como o modo de faturação do mapa toohello de Estados de canal.

| Estado do canal | Indicadores IU do portal | É faturação? |
| --- | --- | --- |
| A Iniciar |A Iniciar |Não (estado transitório) |
| A Executar |Pronto (nenhum programa em execução)<br/>ou<br/>A Transmitir em fluxo (pelo menos um programa em execução) |SIM |
| A Parar |A Parar |Não (estado transitório) |
| Parada |Parada |Não |

## <a name="media-services-learning-paths"></a>Percursos de aprendizagem dos Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Enviar comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Tópicos relacionados
[Especificação de inserção de Media Services do Azure Live MP4 fragmentados](media-services-fmp4-live-ingest-overview.md)

[Trabalhar com canais que é tooPerform ativado em direto Encoding com Media Services do Azure](media-services-manage-live-encoder-enabled-channels.md)

[Trabalhar com Canais que Recebem Transmissões em Fluxo em Direto com Velocidade de Transmissão Múltipla a partir de Codificadores no Local (Working with Channels that Receive Multi-bitrate Live Stream from On-premises Encoders)](media-services-live-streaming-with-onprem-encoders.md)

[Quotas e limitações](media-services-quotas-and-limitations.md).  

[Conceitos de serviços de multimédia](media-services-concepts.md)
