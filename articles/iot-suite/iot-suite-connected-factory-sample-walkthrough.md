---
title: "instruções sobre a solução aaaConnected fábrica Azure IoT Suite | Microsoft Docs"
description: "Uma descrição do Olá soluções pré-configuradas de IoT do Azure ligado definições de fábrica e respetiva arquitetura."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 7fd55c51351659401349cfde91a20fce1045b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connected-factory-preconfigured-solution-walkthrough"></a>Instruções da solução pré-configurada de fábrica ligada

Olá IoT Suite ligado fábrica [solução pré-configurada] [ lnk-preconfigured-solutions] é uma implementação de uma solução de industriais ponto-a-ponto que:

* Estabelece ligação tooboth simulado industriais dispositivos que utilizem o OPC UA servidores em linhas de produção de fábrica simulada e dispositivos de servidor de OPC UA reais. Para mais informações sobre OPC UA, consulte Olá [ligado FAQ de fábrica](iot-suite-faq-cf.md).
* Mostra KPIs e OEE operacionais relativos a esses dispositivos e linhas de produção.
* Demonstra como uma aplicação baseada na nuvem pode ser utilizado toointeract com sistemas de servidor de OPC UA.
* Permite-lhe tooconnect os seus próprios dispositivos de servidor de OPC UA.
* Permite-lhe toobrowse e modificar Olá dados do servidor de OPC UA.
* Integra Olá Insights de séries de tempo do Azure (TSI) serviço tooprovide vistas personalizadas dos dados de Olá dos seus servidores de OPC UA.

Pode utilizar Olá solução como um ponto de partida para a sua própria implementação e [personalizar] [ lnk-customize] -toomeet os seus requisitos empresariais específicos.

Este artigo explica algumas das Olá entre os principais elementos de Olá ligado fábrica solução tooenable toounderstand como funciona. Estes conhecimentos ajudam a:

* Resolva problemas na solução de Olá.
* Planear como toocustomize toohello solução toomeet os seus próprios requisitos específicos.
* Estruturar a sua própria solução de IoT que utiliza os serviços do Azure.

Para obter mais informações, consulte Olá [ligado FAQ de fábrica](iot-suite-faq-cf.md).

## <a name="logical-architecture"></a>Arquitetura lógica

Olá diagrama a seguir descreve os componentes lógicos de Olá da solução pré-configurada de Olá:

![Arquitetura lógica da fábrica ligada][connected-factory-logical]

## <a name="communication-patterns"></a>Padrões de comunicação

solução de Olá utiliza Olá [especificação OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetria dados tooIoT Hub no formato JSON. solução de Olá utiliza Olá [OPC publicador](https://github.com/Azure/iot-edge-opc-publisher) módulo IoT limite para esta finalidade.

solução Olá tem também um cliente de OPC UA integrado de uma aplicação web que pode estabelecer ligações com servidores OPC UA no local. Olá cliente utiliza um [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) e recebe a ajuda da ligação do IoT Hub toomake Olá sem necessidade de portas abertas na firewall do Olá no local. Este padrão de comunicação é denominado [comunicação auxiliada](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/). solução de Olá utiliza Olá [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) módulo IoT limite para esta finalidade.


## <a name="simulation"></a>Simulação

Olá simulated estações e execução de fabrico Olá simulado sistemas (MES) constituem uma linha de produção de fábrica. Olá dispositivos simulados e Olá OPC publicador módulo baseiam-se no Olá [OPC UA .NET padrão] [ lnk-OPC-UA-NET-Standard] publicados pelo Olá OPC Foundation.

Olá OPC Proxy e OPC publicador são implementados como módulos com base no [Azure IoT Edge][lnk-Azure-IoT-Gateway]. Cada linha de produção simulada tem um gateway designado anexado.

Todos os componentes da simulação são executados em contentores do Docker alojados numa VM do Linux do Azure. simulação Olá é linhas produção simulada oito por toorun configurado por predefinição.

## <a name="simulated-production-line"></a>Linha de produção simulada

Uma linha de produção fabrica peças. É composta por diferentes estações: uma estação de montagem, uma de teste e outra de empacotamento.

simulação Olá é executado e dados de Olá que são expostos através de nós OPC UA Olá de atualizações. Todas as estações de linha de produção simulados são orquestradas por Olá MES através de OPC UA.

## <a name="simulated-manufacturing-execution-system"></a>Sistema de execução de fabrico simulado

Olá MES monitoriza cada estação na linha de produção Olá através de alterações de estado do OPC UA toodetect estação. -Chama OPC UA estações de Olá toocontrol de métodos e passa a um produto de uma estação toohello junto até estar concluída.

## <a name="gateway-opc-publisher-module"></a>Módulo de publicador OPC do gateway

Módulo de publicador do OPC liga os servidores OPC UA toohello estação e subscreve toohello OPC nós toobe publicado. módulo Olá converte dados do nó Olá em formato JSON, encripta- e envia-tooIoT Hub como mensagens OPC UA Pub/Sub.

módulo de publicador OPC Olá apenas necessita de uma porta de saída de https (443) e pode trabalhar com a infraestrutura existente do enterprise.

## <a name="gateway-opc-proxy-module"></a>Módulo de proxy OPC do gateway

Olá Gateway OPC UA Proxy módulo túneis mensagens binárias de comando e controlo de OPC UA e requer apenas uma porta de saída de https (443). Funciona com a infraestrutura empresarial existente, incluindo Proxies Web.

Utiliza dispositivos do IoT Hub métodos tootransfer packetized TCP/IP dados na camada de aplicação Olá e, desse modo, garante confiança de ponto final, a encriptação de dados e a integridade utilizar SSL/TLS.

Olá protocolo binário OPC UA retransmitido através do proxy de Olá próprio utiliza UA autenticação e encriptação.

## <a name="azure-time-series-insights"></a>Azure Time Series Insights

Olá Gateway OPC publicador módulo subscreve tooOPC UA nós toodetect de alterações do valores de dados de Olá. Se for detetada uma alteração de dados num de nós de Olá, este módulo, em seguida, envia mensagens tooAzure IoT Hub.

IoT Hub fornece um tooAzure de origem do evento TSI. TSI arquivos de dados para 30 dias, com base no carimbos ligado toohello mensagens. Estes dados incluem:

* O ApplicationUri de OPC UA
* O NodeId de OPC UA
* Valor do nó de Olá
* O Carimbo de data/hora da origem
* O DisplayName de OPC UA

Atualmente, TSI não permitir que os clientes pretenderem dados Olá tookeep quanto toocustomize.

O TSI executa consultas nos dados dos nós com SearchSpan (Time.From, Time.To) e agrega por ApplicationUri, NodeId ou DisplayName de OPC UA.

dados de Olá tooretrieve dados de medidores OEE e KPI de Olá e gráficos de séries de tempo de Olá, foi agregados pelo contagem de eventos, Sum, Avg, Min e Max.

série de tempo de Olá é criada através de um processo diferente. OEE KPIs são calculados a partir dos dados de base de estação e bubbled para topologia de Olá (linhas de produção, fábricas, enterprise) na aplicação Olá.

Além disso, as séries de tempo para topologia de OEE e KPI é calculado na aplicação Olá, sempre que um timespan apresentado está pronto. Por exemplo, a vista Olá é atualizada a cada hora completa.

Vista de séries de tempo de Olá de dados do nó vem diretamente a partir do TSI utilizando uma agregação de timespan.

## <a name="iot-hub"></a>IoT Hub
Olá [IoT hub] [ lnk-IoT Hub] recebe dados enviados do Olá OPC publicador módulo numa nuvem Olá e faz com que o serviço de Azure TSI toohello disponíveis. 

Olá IoT Hub na solução de Olá também:
- Mantém um registo de identidade que armazena os IDs de Olá para todos os módulo de publicador OPC e todos os módulos de Proxy OPC.
- É utilizada como canal de transporte para comunicação bidirecional de Olá OPC Proxy módulo.

## <a name="azure-storage"></a>Storage do Azure
Olá solução utiliza o blob storage do Azure como armazenamento de disco de dados de implementação de VM e toostore Olá.

## <a name="web-app"></a>Aplicação Web
aplicação de web de Olá implementada como parte da solução pré-configurada de Olá compreende de um cliente de OPC UA integrado, processamento de alertas e visualização de telemetria.

## <a name="next-steps"></a>Passos seguintes

Pode continuar a introdução ao IoT Suite ao ler Olá seguintes artigos:

* [Permissões no site azureiotsuite.com de Olá][lnk-permissions]
* [Implementar um gateway no Windows ou Linux para a solução de fábrica pré-configurada Olá ligado](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
