---
title: "considerações de aaaPerformance para o Gestor de tráfego do Azure | Microsoft Docs"
description: "Compreender o desempenho no Gestor de tráfego e como tootest desempenho do seu Web site ao utilizar o Gestor de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Considerações de desempenho para o Gestor de Tráfego

Esta página explica as considerações de desempenho utilizando o Gestor de tráfego. Considere Olá seguinte cenário:

Tem de instâncias do seu Web site na Olá WestUS e EastAsia regiões. Uma das instâncias de Olá está a falhar verificação de estado de funcionamento de Olá para a sonda de Gestor de tráfego de Olá. O tráfego de aplicação é toohello direcionados região de bom estado de funcionamento. Esta ativação pós-falha é esperada, mas o desempenho pode ser um problema com base na latência de Olá de tráfego de Olá agora estiverem em deslocação região distantes tooa.

## <a name="performance-considerations-for-traffic-manager"></a>Considerações de desempenho para o Gestor de Tráfego

Olá apenas impacto no desempenho que o Gestor de tráfego pode ter no seu Web site é a pesquisa de DNS Olá inicial. Um pedido DNS para o nome de Olá do perfil do Gestor de tráfego é processado pelo servidor de raiz de DNS da Microsoft Olá essa zona de trafficmanager.net Olá anfitriões. Gestor de tráfego preenche e atualiza regularmente, servidores de raiz DNS da Microsoft Olá com base na política do Gestor de tráfego Olá e resultados de pesquisa de Olá. Por isso, mesmo durante a pesquisa de DNS inicial Olá, não existem consultas DNS são enviadas tooTraffic Manager.

Gestor de tráfego é constituído por vários componentes: nome de DNS, servidores, um serviço de API, a camada de armazenamento Olá e um ponto final de serviço de monitorização. Se um componente de serviço do Gestor de tráfego falhar, não há sem qualquer efeito no nome DNS Olá associado ao perfil do Traffic Manager. registos de Olá em servidores de DNS da Microsoft Olá permanecem inalterados. No entanto, a monitorização de ponto final e atualizar o DNS não ocorrer. Por conseguinte, Gestor de tráfego não é possível tooupdate DNS toopoint tooyour ativação pós-falha site quando o site primário fica inativo.

Resolução de nomes DNS é rápida e os resultados são colocadas em cache. velocidade de Olá da pesquisa de DNS inicial Olá depende Olá utiliza o cliente de Olá de servidores DNS para resolução de nomes. Normalmente, um cliente pode realizar uma pesquisa DNS no ~ 50 ms. Olá os resultados da pesquisa de Olá são colocadas em cache Olá enquanto estiver em curso Olá DNS Time-to-live (TTL). Olá TTL predefinido para o Gestor de tráfego é de 300 segundos.

Não, o tráfego de fluir através do Gestor de tráfego. Uma vez concluída a pesquisa de DNS Olá, o cliente de Olá tem um endereço IP para uma instância do seu web site. cliente de Olá liga-se diretamente toothat endereço e não a passar através do Gestor de tráfego. Olá política do Gestor de tráfego que escolher não tem nenhum influência no desempenho de DNS Olá. No entanto, um desempenho encaminhamento-método pode afetar negativamente experiência de aplicação Olá. Por exemplo, se a sua política redireciona o tráfego da América do Norte tooan instância alojados na Ásia, latência de rede Olá para essas sessões pode ser um problema de desempenho.

## <a name="measuring-traffic-manager-performance"></a>Medir o desempenho do Gestor de tráfego

Existem vários sites, pode utilizar o desempenho de Olá toounderstand e comportamento de um perfil do Traffic Manager. Muitas destes sites gratuitas, mas poderão ter limitações. Alguns sites oferecem avançada de monitorização e relatórios para uma taxa.

ferramentas de Olá estes sites medem latências DNS e apresentar Olá resolver endereços IP para localizações de clientes em torno Olá mundo. A maioria destas ferramentas não colocar em cache resultados DNS Olá. Por conseguinte, as ferramentas de Olá mostram pesquisa de DNS completa Olá sempre que é executado um teste. Quando testa a partir do seu próprio cliente, apenas experiência Olá completo DNS pesquisa desempenho uma vez durante a duração do TTL Olá.

## <a name="sample-tools-toomeasure-dns-performance"></a>Desempenho de DNS de toomeasure de ferramentas de exemplo

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS oferece muitas ferramentas de desempenho. ferramenta de comparação de DNS Olá pode apresentar-lhe quanto tempo demora tooresolve o nome de DNS e como que compara tooother fornecedores de serviços DNS.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    É uma das ferramentas mais simples de Olá WebSitePulse. Introduza o tempo de resolução de DNS de toosee URL Olá, primeiro Byte, último Byte e outras estatísticas de desempenho. Pode escolher entre três localizações de teste diferentes. Neste exemplo, pode ver que a execução do primeiro Olá mostra que a pesquisa de DNS demora 0.204 seg.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Porque Olá resultados estão em cache, segundo teste de Olá para Olá mesma pesquisa de DNS do Olá de ponto final do Gestor de tráfego demora 0.002 seg.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [Monitor de aplicação Synthetic de AC](https://asm.ca.com/en/checkit.php)

    Anteriormente conhecida como a ferramenta de Web site de verificação Watchmouse Olá, este site mostram-lhe Olá resolução de DNS em simultâneo de tempo de várias regiões geográficas. Introduza o tempo de resolução de DNS de toosee URL Olá, o tempo de ligação e velocidade de várias localizações geográficas. Utilize este toosee de teste, o serviço alojado é devolvido para localizações diferentes em torno Olá mundo.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Esta ferramenta fornece estatísticas de desempenho para cada elemento de uma página web. Olá separador de análise de página mostra a percentagem de Olá de tempo gasto em pesquisa de DNS.

* [O que é o meu DNS?](http://www.whatsmydns.net/)

    Este site não uma pesquisa de DNS 20 diferentes localizações e apresenta os resultados de Olá num mapa.

* [Aprofundar Web Interface](http://www.digwebinterface.com)

    Este site mostra que informações de DNS, incluindo CNAMEs e registos mais detalhadas. Certifique-se que verifique Olá "Colorize output' e 'Estatísticas' em Opções e selecione"Tudo"em Nameservers.

## <a name="next-steps"></a>Passos Seguintes

[Sobre os métodos de encaminhamento de tráfego do Gestor de tráfego](traffic-manager-routing-methods.md)

[Testar as definições do Gestor de tráfego](traffic-manager-testing-settings.md)

[Operações do Gestor de Tráfego (Referência da API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlets do Gestor de tráfego do Azure](http://go.microsoft.com/fwlink/p/?LinkId=400769)

