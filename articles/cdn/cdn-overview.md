---
title: "aaaAzure descrição geral da CDN | Microsoft Docs"
description: "Saiba que Olá é de rede de entrega de conteúdos (CDN) do Azure e como toouse-toodeliver conteúdo de largura de banda alta ao colocar em cache blobs e conteúdo estático."
services: cdn
documentationcenter: 
author: smcevoy
manager: akucer
editor: 
ms.assetid: 866e0c30-1f33-43a5-91f0-d22f033b16c6
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/08/2017
ms.author: v-semcev
ms.openlocfilehash: e0230a6e107969b845985f2f4d357bf93cd40d42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-content-delivery-network-cdn"></a>Descrição geral do Olá Azure rede de entrega de conteúdos (CDN)
> [!NOTE]
> Este documento descreve o que Olá Azure rede de entrega de conteúdos (CDN), como funciona e funcionalidades de Olá de cada produto da CDN do Azure.  Se pretende tooskip estas informações e ir tooa direitas tutorial sobre como toocreate um ponto final de CDN, consulte [utilizar a CDN do Azure](cdn-create-new-endpoint.md).  Se quiser toosee uma lista de localizações de nó CDN atuais, consulte [localizações de POP da CDN do Azure](cdn-pop-locations.md).
> 
> 

Olá rede de entrega de conteúdos (CDN) do Azure coloca em cache conteúdo web estático em localizações estrategicamente colocadas tooprovide o débito máximo para entrega de conteúdos toousers.  Olá CDN oferece aos programadores uma solução global para a entrega de conteúdo de largura de banda alta ao colocar em cache conteúdo Olá em nós físicos em Olá mundo. 

Olá benefícios da utilização de recursos de web site do Olá CDN toocache incluem:

* Melhor desempenho e experiência do utilizador para os utilizadores finais, especialmente quando utilizar as aplicações em que várias ida e volta é necessários conteúdo tooload.
* Grande dimensionamento toobetter identificador elevadas instantâneas, como no início de Olá de um produto iniciar eventos.
* Ao distribuir pedidos de utilizador e que serve o conteúdo a partir de servidores edge, menos tráfego é enviado toohello origem.

## <a name="how-it-works"></a>Como funciona
![Descrição geral da CDN](./media/cdn-overview/cdn-overview.png)

1. Um utilizador (Alice) solicita um ficheiro (também denominado recurso) ao utilizar um URL com um nome de domínio especial, tal como `<endpointname>.azureedge.net`.  O DNS encaminha localização do ponto de presença (POP) Olá pedido toohello melhor desempenho.  Normalmente, este é Olá POP que está mais próximo geograficamente toohello utilizador.
2. Se a servidores edge Olá Olá POP não tem ficheiros Olá na respetiva cache, o servidor edge de Olá pedidos ficheiro Olá da origem de Olá.  origem de Olá pode ser uma aplicação Web do Azure, o serviço em nuvem do Azure, a conta de armazenamento do Azure ou qualquer servidor web acessível publicamente.
3. origem de Olá devolve Olá ficheiro toohello servidor edge, incluindo os cabeçalhos HTTP opcionais que descrevem Time-to-Live do ficheiro de Olá (TTL).
4. servidor do Olá edge coloca em cache de ficheiros de Olá e devolve requerente original do Olá ficheiro toohello (Alice).  ficheiro de Olá permanece em cache no servidor edge de Olá até Olá TTL expire.  Se a origem de Olá não especificou um valor de TTL, predefinição Olá TTL é de sete dias.
5. Os utilizadores adicionais podem, em seguida, Olá pedido mesmo utilizar esse mesmo URL de ficheiro e também podem ser direcionado toothat mesmo POP.
6. Se ainda não tiver expirado Olá TTL para o ficheiro de Olá, o servidor edge de Olá devolve o ficheiro de Olá da cache de Olá.  Isto traduz-se numa experiência de utilizador mais rápida e mais dinâmica.

## <a name="azure-cdn-features"></a>Funcionalidades da CDN do Azure
Existem três produtos da CDN do Azure: **CDN do Azure Standard da Akamai**, **CDN do Azure Standard da Verizon** e **CDN do Azure Premium da Verizon**.  Olá tabela seguinte lista as funcionalidades de Olá disponíveis com cada produto.

|  | Standard da Akamai | Standard da Verizon | Premium da Verizon |
| --- | --- | --- | --- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Funções e Otimizações de Desempenho__ |
| [Aceleração de Site Dinâmico](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration) | **&#x2713;**  | **&#x2713;** | **&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Aceleração de Site Dinâmico - Compressão de Imagem Adaptável](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#adaptive-image-compression-akamai-only) | **&#x2713;**  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Aceleração de Site Dinâmico - Obtenção Prévia de Objeto](https://docs.microsoft.com/azure/cdn/cdn-dynamic-site-acceleration#object-prefetch-akamai-only) | **&#x2713;**  |  |  |
| [Otimização da Transmissão em fluxo de Vídeo](https://docs.microsoft.com/azure/cdn/cdn-media-streaming-optimization) | **&#x2713;**  | \* |  \* |
| [Otimização de Ficheiros Grandes](https://docs.microsoft.com/azure/cdn/cdn-large-file-optimization) | **&#x2713;**  | \* |  \* |
| [Balanceamento de carga de Servidor Global (GSLB)](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-load-balancing-azure) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Remoção rápida](cdn-purge-endpoint.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Pré-carregamento de recursos](cdn-preload-endpoint.md) | |**&#x2713;** |**&#x2713;** |
| [Colocação em cache de cadeias de consulta](cdn-query-string.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Pilha dupla de IPv4/IPv6 |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Suporte HTTP/2](cdn-http2.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Segurança__ |
| Suporta HTTPS com ponto final CDN |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [HTTPS de domínio personalizado](cdn-custom-ssl.md) | |**&#x2713;** |**&#x2713;** |
| [Suporte de nomes de domínio personalizado](cdn-map-content-to-custom-domain.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Filtro geográfico](cdn-restrict-access-by-country.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Autenticação de tokens](cdn-token-auth.md)|  |  |**&#x2713;**| 
| [Proteção contra DDOS](https://www.us-cert.gov/ncas/tips/ST04-015) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__Análises e Relatórios__ |
| [Análise principal](cdn-analyze-usage-patterns.md) | **&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Relatórios HTTP avançados](cdn-advanced-http-reports.md) | | |**&#x2713;** |
| [Estatísticas em tempo real](cdn-real-time-stats.md) | | |**&#x2713;** |
| [Alertas em tempo real](cdn-real-time-alerts.md) | | |**&#x2713;** |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; __Facilidade de Utilização__ |
| Integração fácil com os serviços Azure, tais como o [Armazenamento](cdn-create-a-storage-account-with-cdn.md), [Serviços Cloud](cdn-cloud-service-with-cdn.md), [Aplicações Web](../app-service-web/app-service-web-tutorial-content-delivery-network.md) e [Serviços de Multimédia](../media-services/media-services-portal-manage-streaming-endpoints.md) |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| Gestão através da [API REST](https://msdn.microsoft.com/library/mt634456.aspx), do [.NET](cdn-app-dev-net.md), do [Node.js](cdn-app-dev-node.md) ou do [PowerShell](cdn-manage-powershell.md). |**&#x2713;** |**&#x2713;** |**&#x2713;** |
| [Motor de entrega de conteúdo personalizável com base em regras](cdn-rules-engine.md) | | |**&#x2713;** |
| Definições de cache/cabeçalho (utilizando o [motor de regras](cdn-rules-engine.md)) | | |**&#x2713;** |
| Redirecionar/reescrever URL (utilizando o [motor de regras](cdn-rules-engine.md)) | | |**&#x2713;** |
| Regras de dispositivos móveis (utilizando o [motor de regras](cdn-rules-engine.md)) | | |**&#x2713;** |

\*A Verizon suporta o fornecimento de ficheiros grandes e multimédia diretamente através do General Web Delivery.


> [!TIP]
> Existe uma funcionalidade que gostaria de toosee na CDN do Azure?  [Envie-nos comentários](https://feedback.azure.com/forums/169397-cdn)! 
> 
> 

## <a name="next-steps"></a>Passos seguintes
tooget utilizar a CDN, consulte [utilizar a CDN do Azure](cdn-create-new-endpoint.md).

Se for um cliente existente da CDN, já pode gerir os pontos finais da CDN através de Olá [portal do Microsoft Azure](https://portal.azure.com) ou com [PowerShell](cdn-manage-powershell.md).

toosee Olá CDN em ação, consulte Olá [vídeo da nossa sessão de compilação 2016](https://azure.microsoft.com/documentation/videos/build-2016-leveraging-the-new-azure-cdn-apis-to-build-wicked-fast-applications/).

Saiba como tooautomate CDN do Azure com [.NET](cdn-app-dev-net.md) ou [Node.js](cdn-app-dev-node.md).

Para obter informações sobre preços, consulte [Preços da CDN](https://azure.microsoft.com/pricing/details/cdn/).

