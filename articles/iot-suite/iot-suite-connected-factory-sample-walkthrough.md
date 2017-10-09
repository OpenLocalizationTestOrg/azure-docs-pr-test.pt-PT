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
# <a name="connected-factory-preconfigured-solution-walkthrough"></a><span data-ttu-id="3e9a5-103">Instruções da solução pré-configurada de fábrica ligada</span><span class="sxs-lookup"><span data-stu-id="3e9a5-103">Connected factory preconfigured solution walkthrough</span></span>

<span data-ttu-id="3e9a5-104">Olá IoT Suite ligado fábrica [solução pré-configurada] [ lnk-preconfigured-solutions] é uma implementação de uma solução de industriais ponto-a-ponto que:</span><span class="sxs-lookup"><span data-stu-id="3e9a5-104">hello IoT Suite connected factory [preconfigured solution][lnk-preconfigured-solutions] is an implementation of an end-to-end industrial solution that:</span></span>

* <span data-ttu-id="3e9a5-105">Estabelece ligação tooboth simulado industriais dispositivos que utilizem o OPC UA servidores em linhas de produção de fábrica simulada e dispositivos de servidor de OPC UA reais.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-105">Connects tooboth simulated industrial devices running OPC UA servers in simulated factory production lines, and real OPC UA server devices.</span></span> <span data-ttu-id="3e9a5-106">Para mais informações sobre OPC UA, consulte Olá [ligado FAQ de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3e9a5-106">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="3e9a5-107">Mostra KPIs e OEE operacionais relativos a esses dispositivos e linhas de produção.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-107">Shows operational KPIs and OEE of those devices and production lines.</span></span>
* <span data-ttu-id="3e9a5-108">Demonstra como uma aplicação baseada na nuvem pode ser utilizado toointeract com sistemas de servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-108">Demonstrates how a cloud-based application could be used toointeract with OPC UA server systems.</span></span>
* <span data-ttu-id="3e9a5-109">Permite-lhe tooconnect os seus próprios dispositivos de servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-109">Enables you tooconnect your own OPC UA server devices.</span></span>
* <span data-ttu-id="3e9a5-110">Permite-lhe toobrowse e modificar Olá dados do servidor de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-110">Enables you toobrowse and modify hello OPC UA server data.</span></span>
* <span data-ttu-id="3e9a5-111">Integra Olá Insights de séries de tempo do Azure (TSI) serviço tooprovide vistas personalizadas dos dados de Olá dos seus servidores de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-111">Integrates with hello Azure Time Series Insights (TSI) service tooprovide customized views of hello data from your OPC UA servers.</span></span>

<span data-ttu-id="3e9a5-112">Pode utilizar Olá solução como um ponto de partida para a sua própria implementação e [personalizar] [ lnk-customize] -toomeet os seus requisitos empresariais específicos.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-112">You can use hello solution as a starting point for your own implementation and [customize][lnk-customize] it toomeet your own specific business requirements.</span></span>

<span data-ttu-id="3e9a5-113">Este artigo explica algumas das Olá entre os principais elementos de Olá ligado fábrica solução tooenable toounderstand como funciona.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-113">This article walks you through some of hello key elements of hello connected factory solution tooenable you toounderstand how it works.</span></span> <span data-ttu-id="3e9a5-114">Estes conhecimentos ajudam a:</span><span class="sxs-lookup"><span data-stu-id="3e9a5-114">This knowledge helps you to:</span></span>

* <span data-ttu-id="3e9a5-115">Resolva problemas na solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-115">Troubleshoot issues in hello solution.</span></span>
* <span data-ttu-id="3e9a5-116">Planear como toocustomize toohello solução toomeet os seus próprios requisitos específicos.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-116">Plan how toocustomize toohello solution toomeet your own specific requirements.</span></span>
* <span data-ttu-id="3e9a5-117">Estruturar a sua própria solução de IoT que utiliza os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-117">Design your own IoT solution that uses Azure services.</span></span>

<span data-ttu-id="3e9a5-118">Para obter mais informações, consulte Olá [ligado FAQ de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="3e9a5-118">For more information, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="3e9a5-119">Arquitetura lógica</span><span class="sxs-lookup"><span data-stu-id="3e9a5-119">Logical architecture</span></span>

<span data-ttu-id="3e9a5-120">Olá diagrama a seguir descreve os componentes lógicos de Olá da solução pré-configurada de Olá:</span><span class="sxs-lookup"><span data-stu-id="3e9a5-120">hello following diagram outlines hello logical components of hello preconfigured solution:</span></span>

![Arquitetura lógica da fábrica ligada][connected-factory-logical]

## <a name="communication-patterns"></a><span data-ttu-id="3e9a5-122">Padrões de comunicação</span><span class="sxs-lookup"><span data-stu-id="3e9a5-122">Communication patterns</span></span>

<span data-ttu-id="3e9a5-123">solução de Olá utiliza Olá [especificação OPC UA Pub/Sub](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetria dados tooIoT Hub no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-123">hello solution uses hello [OPC UA Pub/Sub specification](https://opcfoundation.org/news/opc-foundation-news/opc-foundation-announces-support-of-publish-subscribe-for-opc-ua/) toosend OPC UA telemetry data tooIoT Hub in JSON format.</span></span> <span data-ttu-id="3e9a5-124">solução de Olá utiliza Olá [OPC publicador](https://github.com/Azure/iot-edge-opc-publisher) módulo IoT limite para esta finalidade.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-124">hello solution uses hello [OPC Publisher](https://github.com/Azure/iot-edge-opc-publisher) IoT Edge module for this purpose.</span></span>

<span data-ttu-id="3e9a5-125">solução Olá tem também um cliente de OPC UA integrado de uma aplicação web que pode estabelecer ligações com servidores OPC UA no local.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-125">hello solution also has an OPC UA client integrated into a web application that can establish connections with on-premises OPC UA servers.</span></span> <span data-ttu-id="3e9a5-126">Olá cliente utiliza um [proxy inverso](https://wikipedia.org/wiki/Reverse_proxy) e recebe a ajuda da ligação do IoT Hub toomake Olá sem necessidade de portas abertas na firewall do Olá no local.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-126">hello client uses a [reverse-proxy](https://wikipedia.org/wiki/Reverse_proxy) and receives help from IoT Hub toomake hello connection without requiring open ports in hello on-premises firewall.</span></span> <span data-ttu-id="3e9a5-127">Este padrão de comunicação é denominado [comunicação auxiliada](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span><span class="sxs-lookup"><span data-stu-id="3e9a5-127">This communication pattern is called [service-assisted communication](https://blogs.msdn.microsoft.com/clemensv/2014/02/09/service-assisted-communication-for-connected-devices/).</span></span> <span data-ttu-id="3e9a5-128">solução de Olá utiliza Olá [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) módulo IoT limite para esta finalidade.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-128">hello solution uses hello [OPC Proxy](https://github.com/Azure/iot-edge-opc-proxy/) IoT Edge module for this purpose.</span></span>


## <a name="simulation"></a><span data-ttu-id="3e9a5-129">Simulação</span><span class="sxs-lookup"><span data-stu-id="3e9a5-129">Simulation</span></span>

<span data-ttu-id="3e9a5-130">Olá simulated estações e execução de fabrico Olá simulado sistemas (MES) constituem uma linha de produção de fábrica.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-130">hello simulated stations and hello simulated manufacturing execution systems (MES) make up a factory production line.</span></span> <span data-ttu-id="3e9a5-131">Olá dispositivos simulados e Olá OPC publicador módulo baseiam-se no Olá [OPC UA .NET padrão] [ lnk-OPC-UA-NET-Standard] publicados pelo Olá OPC Foundation.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-131">hello simulated devices and hello OPC Publisher Module are based on hello [OPC UA .NET Standard][lnk-OPC-UA-NET-Standard] published by hello OPC Foundation.</span></span>

<span data-ttu-id="3e9a5-132">Olá OPC Proxy e OPC publicador são implementados como módulos com base no [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span><span class="sxs-lookup"><span data-stu-id="3e9a5-132">hello OPC Proxy and OPC Publisher are implemented as modules based on [Azure IoT Edge][lnk-Azure-IoT-Gateway].</span></span> <span data-ttu-id="3e9a5-133">Cada linha de produção simulada tem um gateway designado anexado.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-133">Each simulated production line has a designated gateway attached.</span></span>

<span data-ttu-id="3e9a5-134">Todos os componentes da simulação são executados em contentores do Docker alojados numa VM do Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-134">All simulation components run in Docker containers  hosted in an Azure Linux VM.</span></span> <span data-ttu-id="3e9a5-135">simulação Olá é linhas produção simulada oito por toorun configurado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-135">hello simulation is configured toorun eight simulated production lines by default.</span></span>

## <a name="simulated-production-line"></a><span data-ttu-id="3e9a5-136">Linha de produção simulada</span><span class="sxs-lookup"><span data-stu-id="3e9a5-136">Simulated production line</span></span>

<span data-ttu-id="3e9a5-137">Uma linha de produção fabrica peças.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-137">A production line manufactures parts.</span></span> <span data-ttu-id="3e9a5-138">É composta por diferentes estações: uma estação de montagem, uma de teste e outra de empacotamento.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-138">It is composed of different stations: an assembly station, a test station, and a packaging station.</span></span>

<span data-ttu-id="3e9a5-139">simulação Olá é executado e dados de Olá que são expostos através de nós OPC UA Olá de atualizações.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-139">hello simulation runs and updates hello data that is exposed through hello OPC UA nodes.</span></span> <span data-ttu-id="3e9a5-140">Todas as estações de linha de produção simulados são orquestradas por Olá MES através de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-140">All simulated production line stations are orchestrated by hello MES through OPC UA.</span></span>

## <a name="simulated-manufacturing-execution-system"></a><span data-ttu-id="3e9a5-141">Sistema de execução de fabrico simulado</span><span class="sxs-lookup"><span data-stu-id="3e9a5-141">Simulated manufacturing execution system</span></span>

<span data-ttu-id="3e9a5-142">Olá MES monitoriza cada estação na linha de produção Olá através de alterações de estado do OPC UA toodetect estação.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-142">hello MES monitors each station in hello production line through OPC UA toodetect station status changes.</span></span> <span data-ttu-id="3e9a5-143">-Chama OPC UA estações de Olá toocontrol de métodos e passa a um produto de uma estação toohello junto até estar concluída.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-143">It calls OPC UA methods toocontrol hello stations and passes a product from one station toohello next until it is complete.</span></span>

## <a name="gateway-opc-publisher-module"></a><span data-ttu-id="3e9a5-144">Módulo de publicador OPC do gateway</span><span class="sxs-lookup"><span data-stu-id="3e9a5-144">Gateway OPC publisher module</span></span>

<span data-ttu-id="3e9a5-145">Módulo de publicador do OPC liga os servidores OPC UA toohello estação e subscreve toohello OPC nós toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-145">OPC Publisher Module connects toohello station OPC UA servers and subscribes toohello OPC nodes toobe published.</span></span> <span data-ttu-id="3e9a5-146">módulo Olá converte dados do nó Olá em formato JSON, encripta- e envia-tooIoT Hub como mensagens OPC UA Pub/Sub.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-146">hello module converts hello node data into JSON format, encrypts it, and sends it tooIoT Hub as OPC UA Pub/Sub messages.</span></span>

<span data-ttu-id="3e9a5-147">módulo de publicador OPC Olá apenas necessita de uma porta de saída de https (443) e pode trabalhar com a infraestrutura existente do enterprise.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-147">hello OPC Publisher module only requires an outbound https port (443) and can work with existing enterprise infrastructure.</span></span>

## <a name="gateway-opc-proxy-module"></a><span data-ttu-id="3e9a5-148">Módulo de proxy OPC do gateway</span><span class="sxs-lookup"><span data-stu-id="3e9a5-148">Gateway OPC proxy module</span></span>

<span data-ttu-id="3e9a5-149">Olá Gateway OPC UA Proxy módulo túneis mensagens binárias de comando e controlo de OPC UA e requer apenas uma porta de saída de https (443).</span><span class="sxs-lookup"><span data-stu-id="3e9a5-149">hello Gateway OPC UA Proxy Module tunnels binary OPC UA command and control messages and only requires an outbound https port (443).</span></span> <span data-ttu-id="3e9a5-150">Funciona com a infraestrutura empresarial existente, incluindo Proxies Web.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-150">It can work with existing enterprise infrastructure, including Web Proxies.</span></span>

<span data-ttu-id="3e9a5-151">Utiliza dispositivos do IoT Hub métodos tootransfer packetized TCP/IP dados na camada de aplicação Olá e, desse modo, garante confiança de ponto final, a encriptação de dados e a integridade utilizar SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-151">It uses IoT Hub Device methods tootransfer packetized TCP/IP data at hello application layer and thus ensures endpoint trust, data encryption, and integrity using SSL/TLS.</span></span>

<span data-ttu-id="3e9a5-152">Olá protocolo binário OPC UA retransmitido através do proxy de Olá próprio utiliza UA autenticação e encriptação.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-152">hello OPC UA binary protocol relayed through hello proxy itself uses UA authentication and encryption.</span></span>

## <a name="azure-time-series-insights"></a><span data-ttu-id="3e9a5-153">Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="3e9a5-153">Azure Time Series Insights</span></span>

<span data-ttu-id="3e9a5-154">Olá Gateway OPC publicador módulo subscreve tooOPC UA nós toodetect de alterações do valores de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-154">hello Gateway OPC Publisher Module subscribes tooOPC UA server nodes toodetect change in hello data values.</span></span> <span data-ttu-id="3e9a5-155">Se for detetada uma alteração de dados num de nós de Olá, este módulo, em seguida, envia mensagens tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-155">If a data change is detected in one of hello nodes, this module then sends messages tooAzure IoT Hub.</span></span>

<span data-ttu-id="3e9a5-156">IoT Hub fornece um tooAzure de origem do evento TSI.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-156">IoT Hub provides an event source tooAzure TSI.</span></span> <span data-ttu-id="3e9a5-157">TSI arquivos de dados para 30 dias, com base no carimbos ligado toohello mensagens.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-157">TSI stores data for 30 days based on timestamps attached toohello messages.</span></span> <span data-ttu-id="3e9a5-158">Estes dados incluem:</span><span class="sxs-lookup"><span data-stu-id="3e9a5-158">This data includes:</span></span>

* <span data-ttu-id="3e9a5-159">O ApplicationUri de OPC UA</span><span class="sxs-lookup"><span data-stu-id="3e9a5-159">OPC UA ApplicationUri</span></span>
* <span data-ttu-id="3e9a5-160">O NodeId de OPC UA</span><span class="sxs-lookup"><span data-stu-id="3e9a5-160">OPC UA NodeId</span></span>
* <span data-ttu-id="3e9a5-161">Valor do nó de Olá</span><span class="sxs-lookup"><span data-stu-id="3e9a5-161">Value of hello node</span></span>
* <span data-ttu-id="3e9a5-162">O Carimbo de data/hora da origem</span><span class="sxs-lookup"><span data-stu-id="3e9a5-162">Source timestamp</span></span>
* <span data-ttu-id="3e9a5-163">O DisplayName de OPC UA</span><span class="sxs-lookup"><span data-stu-id="3e9a5-163">OPC UA DisplayName</span></span>

<span data-ttu-id="3e9a5-164">Atualmente, TSI não permitir que os clientes pretenderem dados Olá tookeep quanto toocustomize.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-164">Currently, TSI does not allow customers toocustomize how long they wish tookeep hello data for.</span></span>

<span data-ttu-id="3e9a5-165">O TSI executa consultas nos dados dos nós com SearchSpan (Time.From, Time.To) e agrega por ApplicationUri, NodeId ou DisplayName de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-165">TSI queries against node data using a SearchSpan (Time.From, Time.To) and aggregates by OPC UA ApplicationUri or OPC UA NodeId or OPC UA DisplayName.</span></span>

<span data-ttu-id="3e9a5-166">dados de Olá tooretrieve dados de medidores OEE e KPI de Olá e gráficos de séries de tempo de Olá, foi agregados pelo contagem de eventos, Sum, Avg, Min e Max.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-166">tooretrieve hello data for hello OEE and KPI gauges, and hello time series charts, data is aggregated by count of events, Sum, Avg, Min, and Max.</span></span>

<span data-ttu-id="3e9a5-167">série de tempo de Olá é criada através de um processo diferente.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-167">hello time series are built using a different process.</span></span> <span data-ttu-id="3e9a5-168">OEE KPIs são calculados a partir dos dados de base de estação e bubbled para topologia de Olá (linhas de produção, fábricas, enterprise) na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-168">OEE and KPIs are calculated from station base data and bubbled up for hello topology (production lines, factories, enterprise) in hello application.</span></span>

<span data-ttu-id="3e9a5-169">Além disso, as séries de tempo para topologia de OEE e KPI é calculado na aplicação Olá, sempre que um timespan apresentado está pronto.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-169">Additionally, time series for OEE and KPI topology is calculated in hello app, whenever a displayed timespan is ready.</span></span> <span data-ttu-id="3e9a5-170">Por exemplo, a vista Olá é atualizada a cada hora completa.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-170">For example, hello day view is updated every full hour.</span></span>

<span data-ttu-id="3e9a5-171">Vista de séries de tempo de Olá de dados do nó vem diretamente a partir do TSI utilizando uma agregação de timespan.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-171">hello time series view of node data comes directly from TSI using an aggregation for timespan.</span></span>

## <a name="iot-hub"></a><span data-ttu-id="3e9a5-172">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="3e9a5-172">IoT Hub</span></span>
<span data-ttu-id="3e9a5-173">Olá [IoT hub] [ lnk-IoT Hub] recebe dados enviados do Olá OPC publicador módulo numa nuvem Olá e faz com que o serviço de Azure TSI toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-173">hello [IoT hub][lnk-IoT Hub] receives data sent from hello OPC Publisher Module into hello cloud and makes it available toohello Azure TSI service.</span></span> 

<span data-ttu-id="3e9a5-174">Olá IoT Hub na solução de Olá também:</span><span class="sxs-lookup"><span data-stu-id="3e9a5-174">hello IoT Hub in hello solution also:</span></span>
- <span data-ttu-id="3e9a5-175">Mantém um registo de identidade que armazena os IDs de Olá para todos os módulo de publicador OPC e todos os módulos de Proxy OPC.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-175">Maintains an identity registry that stores hello IDs for all OPC Publisher Module and all OPC Proxy Modules.</span></span>
- <span data-ttu-id="3e9a5-176">É utilizada como canal de transporte para comunicação bidirecional de Olá OPC Proxy módulo.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-176">Is used as transport channel for bidirectional communication of hello OPC Proxy Module.</span></span>

## <a name="azure-storage"></a><span data-ttu-id="3e9a5-177">Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="3e9a5-177">Azure Storage</span></span>
<span data-ttu-id="3e9a5-178">Olá solução utiliza o blob storage do Azure como armazenamento de disco de dados de implementação de VM e toostore Olá.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-178">hello solution uses Azure blob storage as disk storage for hello VM and toostore deployment data.</span></span>

## <a name="web-app"></a><span data-ttu-id="3e9a5-179">Aplicação Web</span><span class="sxs-lookup"><span data-stu-id="3e9a5-179">Web app</span></span>
<span data-ttu-id="3e9a5-180">aplicação de web de Olá implementada como parte da solução pré-configurada de Olá compreende de um cliente de OPC UA integrado, processamento de alertas e visualização de telemetria.</span><span class="sxs-lookup"><span data-stu-id="3e9a5-180">hello web app deployed as part of hello preconfigured solution comprises of an integrated OPC UA client, alerts processing and telemetry visualization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e9a5-181">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="3e9a5-181">Next steps</span></span>

<span data-ttu-id="3e9a5-182">Pode continuar a introdução ao IoT Suite ao ler Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="3e9a5-182">You can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="3e9a5-183">[Permissões no site azureiotsuite.com de Olá][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="3e9a5-183">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="3e9a5-184">Implementar um gateway no Windows ou Linux para a solução de fábrica pré-configurada Olá ligado</span><span class="sxs-lookup"><span data-stu-id="3e9a5-184">Deploy a gateway on Windows or Linux for hello connected factory preconfigured solution</span></span>](iot-suite-connected-factory-gateway-deployment.md)

[connected-factory-logical]:media/iot-suite-connected-factory-walkthrough/cf-logical-architecture.png

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-IoT Hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-OPC-UA-NET-Standard]:https://github.com/OPCFoundation/UA-.NETStandardLibrary
[lnk-Azure-IoT-Gateway]: https://github.com/azure/iot-edge
[lnk-permissions]: iot-suite-permissions.md
