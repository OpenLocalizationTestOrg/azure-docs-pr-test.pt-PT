---
title: aaaAzure FAQ de estado de funcionamento de recursos | Microsoft Docs
description: "Descrição geral do Estado de funcionamento de recursos do Azure"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>FAQ do Estado de funcionamento do recurso do Azure
Saiba Olá atende toocommon perguntas sobre o estado de funcionamento de recursos de Azure.

## <a name="what-is-azure-resource-health"></a>O que é o estado de funcionamento de recursos de Azure?
O estado de funcionamento dos recursos ajuda-o a diagnosticar e a obter suporte quando um problema do Azure afeta os seus recursos. Informa-sobre Olá atuais e anteriores estado de funcionamento dos seus recursos e ajuda a mitigar os problemas. O estado de funcionamento dos recursos fornece suporte técnico quando precisa de ajuda para resolver problemas relacionados com o serviço do Azure.  

## <a name="what-is-hello-resource-health-intended-for"></a>O que é Olá que estado de funcionamento de recursos concebido para?
Assim que foi detetado um problema com um recurso, o estado de funcionamento do recurso pode ajudar a diagnosticar a causa de raiz de Olá. Fornece ajuda toomitigate Olá problema e o suporte técnico quando precisar de mais ajuda com problemas de serviço do Azure.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Verifica o estado de funcionamento são efetuadas pelo Estado de funcionamento do recurso?
Estado de funcionamento do recurso efetua verificações de vários com base no Olá [tipo de recurso](resource-health-checks-resource-types.md). Estas verificações são tooimplement concebida três tipos de problemas: 
- Eventos não planeados, por exemplo, um reinício inesperado de anfitrião
- Eventos planeados, como atualizações do SO do anfitrião agendada
- Eventos acionados pelas ações do utilizador, por exemplo, um utilizador iniciar uma máquina virtual

## <a name="what-does-each-of-hello-health-status-mean"></a>O que cada Estado de funcionamento de Olá significa?
Existem três Estados de funcionamento de diferentes:
- Está disponível: Sabemos de quaisquer problemas conhecidos no Olá plataforma Azure que pode estar a afetar este recurso
- Indisponível: Estado de funcionamento do recurso detetou problemas que têm maior impacto na recursos Olá
- Desconhecido: Estado de funcionamento de recursos pode não determinar Olá estado de funcionamento de um recurso porque foi parado receber informações acerca do mesmo. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>O que Olá média de estado desconhecido? Algo está errado os meus recursos?
Estado de funcionamento de Olá está definido toounknown quando o estado de funcionamento do recurso para receber informações sobre um recurso específico. Enquanto este estado não é uma indicação definitiva Olá do Estado do recurso de Olá, nos casos em que existem problemas, pode indicar que há um problema do Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Como posso obter ajuda para um recurso que não está disponível?
Pode submeter um pedido de suporte a partir do painel de estado de funcionamento de recursos de Olá. Não é necessário um contrato de suporte com a Microsoft tooopen um pedido ao recurso de Olá não está disponível porque os eventos de plataforma.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Estado de funcionamento do recurso distinguir entre indisponibilidade cased por problemas de plataforma versus algo que posso foi?
Sim, quando um recurso não está disponível, o estado de funcionamento do recurso identifica a causa de raiz de Olá dentro de uma destas categorias: 
-   Ação iniciada pelo utilizador
-   Evento planeado 
-   Evento não planeado

No portal de Olá, ações iniciada pelo utilizador são apresentadas utilizando um ícone de notificação azul, enquanto eventos planeados e não são apresentados utilizando um ícone de aviso vermelho. São fornecidos mais detalhes nas Olá [descrição geral do Estado de funcionamento do recurso](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Pode integrar o estado de funcionamento do recurso com a minha ferramentas de monitorização?
Estado de funcionamento de recursos é um toohelp serviço concebido diagnosticar e atenuar problemas de serviço do Azure que afetam os seus recursos. Apesar de poder utilizar Olá API do Estado de funcionamento de recursos tooprogrammatically obter o estado de funcionamento de Olá, recomendamos que utilize métricas toomonitor os recursos. Quando é detetado um problema, estado de funcionamento do recurso ajuda-o a determinar a causa de raiz de Olá e orienta-o ações tooaddress-los. Visite [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn mais informações sobre como pode utilizar as métricas toocheck os recursos.

## <a name="where-do-i-find-resource-health"></a>Onde posso encontrar o estado de funcionamento do recurso?
Depois de iniciar sessão no portal do Azure de toohello, existem várias formas, pode aceder ao estado de funcionamento de recursos:
- Navegue tooyour recursos. No painel navegação esquerda Olá, selecione **estado de funcionamento de recursos**
- Aceda toohello painel de monitorização do Azure.  No painel navegação esquerda Olá, selecione **estado de funcionamento do recurso**.
- Abra Olá **ajuda + suporte** painel, selecionando o ponto de interrogação Olá na Olá canto superior direito do portal de Olá e, em seguida, selecionar **ajuda + suporte**. Uma vez que abre painel Olá, selecionar **estado de funcionamento de recursos**

Também pode utilizar Olá API do Estado de funcionamento de recursos tooobtain obter informações sobre o estado de funcionamento do Olá dos seus recursos.

## <a name="is-resource-health-available-for-all-resource-types"></a>Estado de funcionamento do recurso está disponível para todos os tipos de recursos?
Olá lista de verificações de estado de funcionamento e tipos de recurso suportados através do Estado de funcionamento de recursos pode ser encontrada [aqui](resource-health-checks-resource-types.md).

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>O que devo fazer se os meus recursos está a ser mostrada disponível, mas se considerar que não é?"
Quando a verificação do Estado de funcionamento de Olá de um recurso, à direita em estado de funcionamento de Olá pode clicar em **comunicar o estado de funcionamento incorreto**. Antes de Submeter relatório Olá, terá de opção de Olá de fornecer detalhes adicionais sobre o motivo pelo qual considerar o estado de funcionamento atual Olá está incorreto.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Estado de funcionamento do recurso está disponível para todas as regiões do Azure? 
Estado de funcionamento do recurso está disponível em todos os geos do Azure, exceto Olá seguintes regiões:
- Gov (US) - Virginia
- Gov (US) - Iowa
- US DoD Leste
- US DoD Centro
- Alemanha Central
- Alemanha Nordeste
- Leste da China
- China Norte

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Como estado de funcionamento do recurso é diferente do notificações de serviço de portal do Azure do Dashboard de estado de funcionamento do serviço ou Olá Olá?
informações de Olá fornecidas pelo Estado de funcionamento do recurso são mais específicas que o que é fornecido pela Olá Dashboard de estado de funcionamento do serviço Azure.

Enquanto [Azure estado](https://status.azure.com) e as notificações do portal do serviço de Olá informam sobre problemas de serviço que afetam a um conjunto amplo de clientes (por exemplo uma região do Azure), o estado de funcionamento do recurso expõe mais granular sobre eventos que são relevantes apenas toohello de recurso específico. Por exemplo, se um anfitrião inesperadamente é reiniciado, o estado de funcionamento do recurso alerta apenas esses clientes cujas máquinas virtuais estavam a ser executadas nesse anfitrião.

É importante toonotice esse tooprovide que concluir visibilidade dos eventos afetar os recursos, o estado de funcionamento de recursos também eventos analisa publicados em notificações de serviço e Olá Dashboard de estado de funcionamento do serviço.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>É necessário tooactivate estado de funcionamento de recursos para cada recurso?
Não, as informações de estado de funcionamento estão disponíveis para todos os tipos de recursos disponíveis através do Estado de funcionamento do recurso. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Precisamos tooenable estado de funcionamento do recurso para a minha organização?
Não.  Estado de funcionamento de recursos do Azure está acessível na Olá portal do Azure sem quaisquer requisitos de configuração.

## <a name="is-resource-health-available-free-of-charge"></a>É o estado de funcionamento de recursos disponíveis gratuitamente?
Sim.  Estado de funcionamento de recursos do Azure é gratuitamente.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Quais são as recomendações de Olá que fornece o estado de funcionamento do recurso?
Com base no estado de funcionamento de Olá, estado de funcionamento do recurso fornece recomendações com o objetivo Olá reduzindo Olá tempo que gasto a resolução de problemas. Para obter recursos disponíveis, recomendações Olá focar-se na forma como os clientes de problemas mais comuns do toosolve Olá encontrarem. Se não estiver disponível devido a recursos de Olá tooan evento não planeado do Azure, que o foco de Olá estarão na prestar assistência, durante e após o processo de recuperação Olá. 

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre o estado de funcionamento de recursos:
-  [Descrição geral do Estado de funcionamento de recursos do Azure](Resource-health-overview.md)
-  [Os tipos de recursos e verificações do estado de funcionamento disponíveis através do Azure Resource Health](resource-health-checks-resource-types.md)
