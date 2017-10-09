---
title: "aaaMedia otimização através de Olá Azure rede de entrega de conteúdos de transmissão em fluxo"
description: "Otimizar os ficheiros de multimédia de transmissão em fluxo para entrega uniforme"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: a05a86204708c7ea7ef1f9be04323cdda6a2d403
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="media-streaming-optimization-via-hello-azure-content-delivery-network"></a>Suporte de dados de transmissão em fluxo otimização através de Olá rede de entrega de conteúdos do Azure 
 
Aumento da utilização de vídeo de alta definição no Olá Internet, que cria dificuldades para entrega eficiente de ficheiros grandes. Os clientes esperam uniforme reprodução de vídeo a pedido ou em direto a recursos de vídeos numa variedade de clientes e redes em todo o mundo Olá. Um mecanismo de entrega rápidos e eficientes para transmissão em fluxo de ficheiros de suporte de dados é crítica tooensure uma experiência de consumidor enjoyable e uniforme.  

Suporte de dados de transmissão em fluxo em direto é particularmente difíceis toodeliver devido a tamanhos grandes Olá e número de visualizadores autorizados em simultâneo. Grandes atrasos fazer com que os utilizadores tooleave. Uma vez fluxos em direto não não possível colocar em cache antecedência e latências grande não são aceitáveis tooviewers, tem de ser entregue fragmentos de vídeos de uma forma atempada. 

Olá pedido sobre os padrões de transmissão em fluxo também fornecem alguns novos desafios. Quando for lançada uma transmissão em fluxo em direto popular ou uma série nova de vídeo a pedido, milhares toomillions de visualizadores autorizados podem solicitar fluxo Olá em Olá mesmo tempo. Neste caso, o pedido inteligente consolidação é vital toonot sobrecarregar servidores de origem Olá quando ativos Olá não são colocadas em cache ainda.
 
Agora, Olá rede entrega de conteúdos do Azure da Akamai oferece uma funcionalidade que fornece recursos de suporte de dados de transmissão em fluxo eficientemente toousers em globo Olá à escala. funcionalidade de Olá reduz as latências dado que reduz a carga de Olá nos servidores de origem de Olá. Esta funcionalidade está disponível com o escalão de preço do Olá Standard da Akamai. 

Olá rede entrega de conteúdos do Azure da Verizon fornece suporte de dados de transmissão em fluxo diretamente no tipo de otimização de entrega do Olá web geral.
 
## <a name="configure-an-endpoint-toooptimize-media-streaming-in-hello-azure-content-delivery-network-from-akamai"></a>Configurar um suporte de dados de toooptimize do ponto final de transmissão em fluxo no Olá rede entrega de conteúdos do Azure da Akamai
 
Pode configurar a entrega de toooptimize de ponto final a entrega de conteúdos (CDN) de rede para ficheiros grandes através de Olá portal do Azure. Também pode utilizar os APIs REST ou qualquer um dos Olá cliente SDKs toodo isto. Olá passos seguintes mostram processo Olá através de Olá portal do Azure:

1. tooadd um novo ponto final, Olá **perfil da CDN** página, selecione **Endpoint**.
  
    ![Novo ponto final](./media/cdn-media-streaming-optimization/01_Adding.png)

2. No Olá **otimizado para** na lista pendente, selecione **vídeo no pedido suporte de dados de transmissão em fluxo** para recursos de vídeo a pedido. Se fizer uma combinação de em direto e, em seguida, transmissão em fluxo de vídeo a pedido, selecione **suporte de dados gerais de transmissão em fluxo**.

    ![Transmissão em fluxo selecionado](./media/cdn-media-streaming-optimization/02_Creating.png) 
 
Depois de criar o ponto final de Olá, aplica-se otimização Olá para todos os ficheiros que correspondem a determinados critérios. Olá seguinte secção descreve este processo. 
 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-akamai"></a>Suporte de dados de transmissão em fluxo otimizações de Olá rede entrega de conteúdos do Azure da Akamai
 
Os fragmentos de suporte de dados de transmissão em fluxo a Otimização da Akamai está eficaz para direta ou suporte de transmissão em fluxo de vídeo a pedido que utiliza suportes de dados individuais para entrega. Este processo é diferente de um único recurso de grande transferido através de transferência progressiva ou através da utilização de pedidos de intervalo de bytes. Para informações sobre essa estilo de entrega de suporte de dados, consulte [otimização de ficheiros grandes](cdn-large-file-optimization.md).


Olá geral do suporte de dados entrega ou as vídeo a pedido entrega otimização tipos de suporte utilizam um CDN com recursos de suporte de dados de toodeliver otimizações de back-end mais rapidamente. Também utilizam configurações para recursos de suporte de dados com base nas melhores práticas aprendidas ao longo do tempo.

### <a name="caching"></a>Colocação em cache

Se Olá rede entrega de conteúdos do Azure da Akamai Deteta que esse recurso Olá é um manifesto de transmissão em fluxo ou um fragmento, utiliza períodos de expiração de colocação em cache diferentes de entrega de web geral. (Consulte a lista completa de Olá no Olá a tabela seguinte.) Como sempre, cache-control ou cabeçalhos expira enviados a partir da origem de Olá são cumpridos. Se o recurso de Olá não é um recurso de suporte de dados, coloca em cache através da utilização de tempos de expiração de Olá para entrega web geral.

tempo de colocação em cache negativa curto Olá é útil para a descarga de origem de quando número de utilizadores que pedem um fragmento que ainda não existe. Um exemplo é uma transmissão em fluxo em direto onde pacotes hello não estão disponíveis a partir da origem de Olá esse segundo. intervalo já é a colocação em cache Olá também ajuda a descarga de pedidos de origem Olá porque a conteúdos de vídeo, normalmente, não se encontra modificado.
 

|    | Geral<br> Web<br>contínua | Geral<br> suporte de dados<br> transmissão em fluxo | Vídeo a pedido <br>suporte de dados<br> transmissão em fluxo  
--- | --- | --- | ---
A colocação em cache: positivo <br> HTTP 200, 203, 300, <br> 301, 302 e 410 | 7 dias |365 dias | 365 dias   
A colocação em cache: negativo <br> HTTP 204, 305, 404, <br> e 405 | Nenhuma | 1 segundo | 1 segundo
 
### <a name="deal-with-origin-failure"></a>Lidar com falha de origem  

Entrega de multimédia de vídeo a pedido e entrega de multimédia geral também tem tempo limite de origem e um registo de repetição com base nas melhores práticas para padrões de pedido comuns. Por exemplo, uma vez que a entrega de multimédia geral destina-se em direto e entrega de multimédia de vídeo a pedido, utiliza um limite de tempo de ligação de mais curto devido a natureza sensíveis ao tempo toohello transmissão em direto.

Quando uma ligação exceder o tempo limite, Olá CDN repete um número de vezes antes de enviar um cliente de toohello de erro "504 - tempo limite do Gateway". 

Quando um ficheiro corresponde à lista de condições de Olá ficheiros tipo e tamanho, Olá CDN utiliza o comportamento de Olá para suporte de dados de transmissão em fluxo. Caso contrário, utiliza a entrega de web geral.
   
### <a name="conditions-for-media-streaming-optimization"></a>Condições para a otimização de transmissão em fluxo de suporte de dados 

Olá, a tabela seguinte lista o conjunto de Olá de critérios toobe satisfeito para otimização de transmissão em fluxo de suporte de dados: 
 
Tipos de transmissão em fluxo suportados | Extensões de ficheiro  
--- | ---  
Apple HLS | m3u8 m3u, m3ub, chave, ts, aac
Adobe HDS | f4m f4x, drmmeta, arranque, f4f,<br>Estrutura de seg Frag URL <br> (regex de correspondência: ^(/.*)Seq(\d+)-Frag(\d+)
TRAÇO | MPD, traço, divx, ismv, m4s, m4v, mp4, mp4v, <br> sidx webm, mp4a, m4a, isma
Transmissão em fluxo uniforme | o manifesto /, QualityLevels/fragmentos /
  

 
## <a name="media-streaming-optimizations-for-hello-azure-content-delivery-network-from-verizon"></a>Suporte de dados de transmissão em fluxo otimizações de Olá rede entrega de conteúdos do Azure da Verizon

Olá rede entrega de conteúdos do Azure da Verizon fornece recursos de suporte de dados de transmissão em fluxo diretamente, utilizando o tipo de otimização de entrega do Olá web geral. Algumas funcionalidades Olá CDN diretamente ajudar na entrega recursos de suporte de dados por predefinição.

### <a name="partial-cache-sharing"></a>Partilha de cache parciais

Partilha de cache parciais permite que os pedidos de conteúdo toonew do Olá CDN tooserve parcialmente em cache. Por exemplo, se Olá primeiro pedido toohello CDN resulta numa falha de acerto na cache, Olá é enviado pedido toohello origem. Embora este conteúdo incompleto está carregado Olá CDN cache, toohello outros pedidos CDN pode começar a obter estes dados. 

### <a name="cache-fill-wait-time"></a>Tempo de espera de preenchimento de cache

 funcionalidade de tempo de espera de preenchimento de cache de Olá força Olá edge servidor toohold todos os pedidos subsequentes para Olá mesmo recurso até cabeçalhos chegam a partir do servidor de origem Olá de resposta HTTP. Se os cabeçalhos de resposta HTTP da origem de Olá chegam antes de expira temporizador Olá, todos os pedidos que foram colocar em espera são servidos fora Olá cache a crescer. Em Olá mesmo tempo, hello cache é preenchida pelo dados a partir da origem de Olá. Por predefinição, o tempo de espera de preenchimento de cache de Olá está definido too3, 000 milissegundos. 

