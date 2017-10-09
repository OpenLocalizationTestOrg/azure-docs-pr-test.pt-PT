---
title: "inspeção aaaPacket com observador de rede do Azure | Microsoft Docs"
description: "Este artigo descreve como toouse inspeção de pacotes aprofundada do observador de rede tooperform recolhidos a partir de uma VM"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b907d00-9c35-40f5-a61e-beb7b782276f
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4aeddcd482edc4df3d63e87b5c4b0788c540850b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="packet-inspection-with-azure-network-watcher"></a><span data-ttu-id="2e974-103">Inspeção de pacotes com observador de rede do Azure</span><span class="sxs-lookup"><span data-stu-id="2e974-103">Packet inspection with Azure Network Watcher</span></span>

<span data-ttu-id="2e974-104">Utilizar a funcionalidade de captura de pacotes hello do observador de rede, pode iniciar e gerir sessões de capturas nas suas VMs do Azure a partir do portal Olá, PowerShell CLI e através de programação através de Olá SDK e a REST API.</span><span class="sxs-lookup"><span data-stu-id="2e974-104">Using hello packet capture feature of Network Watcher, you can initiate and manage captures sessions on your Azure VMs from hello portal, PowerShell, CLI, and programmatically through hello SDK and REST API.</span></span> <span data-ttu-id="2e974-105">Captura de pacotes permite-lhe tooaddress cenários que necessitam de dados ao nível do pacote, fornecendo informações Olá num formato prontamente utilizável.</span><span class="sxs-lookup"><span data-stu-id="2e974-105">Packet capture allows you tooaddress scenarios that require packet level data by providing hello information in a readily usable format.</span></span> <span data-ttu-id="2e974-106">Tirar partido dos dados de Olá tooinspect de ferramentas livremente disponíveis, pode examinar comunicações enviadas tooand do seu VMs e obter informações sobre o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="2e974-106">Leveraging freely available tools tooinspect hello data, you can examine communications sent tooand from your VMs and gain insights into your network traffic.</span></span> <span data-ttu-id="2e974-107">Incluem algumas utilizações de exemplo de dados de captura de pacotes: investigar problemas de rede ou aplicação, detetar tentativas de utilização indevida e intrusão de rede ou manter a conformidade regulamentar.</span><span class="sxs-lookup"><span data-stu-id="2e974-107">Some example uses of packet capture data include: investigating network or application issues, detecting network misuse and intrusion attempts, or maintaining regulatory compliance.</span></span> <span data-ttu-id="2e974-108">Neste artigo, mostramos como tooopen um ficheiro de captura de pacotes fornecido por observador de rede utilizando uma ferramenta open source para populares.</span><span class="sxs-lookup"><span data-stu-id="2e974-108">In this article, we show how tooopen a packet capture file provided by Network Watcher using a popular open source tool.</span></span> <span data-ttu-id="2e974-109">Fornecemos também exemplos que mostra como identificar tráfego anormal toocalculate uma latência de ligação e examine as estatísticas de rede.</span><span class="sxs-lookup"><span data-stu-id="2e974-109">We will also provide examples showing how toocalculate a connection latency, identify abnormal traffic, and examine networking statistics.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2e974-110">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2e974-110">Before you begin</span></span>

<span data-ttu-id="2e974-111">Este artigo passa através de alguns cenários previamente configurados uma captura de pacotes que foi anteriormente executada com êxito.</span><span class="sxs-lookup"><span data-stu-id="2e974-111">This article goes through some pre-configured scenarios on a packet capture that was run previously.</span></span> <span data-ttu-id="2e974-112">Estes cenários mostram capacidades que podem ser acedidas ao rever uma captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="2e974-112">These scenarios illustrate capabilities that can be accessed by reviewing a packet capture.</span></span> <span data-ttu-id="2e974-113">Este cenário utiliza [WireShark](https://www.wireshark.org/) captura de pacotes de Olá tooinspect.</span><span class="sxs-lookup"><span data-stu-id="2e974-113">This scenario uses [WireShark](https://www.wireshark.org/) tooinspect hello packet capture.</span></span>

<span data-ttu-id="2e974-114">Este cenário pressupõe que já tenha sido executada uma captura de pacotes numa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e974-114">This scenario assumes you already ran a packet capture on a virtual machine.</span></span> <span data-ttu-id="2e974-115">toolearn como toocreate uma captura de pacotes visite [capturas de pacotes de gerir com o portal de Olá](network-watcher-packet-capture-manage-portal.md) ou com REST, visitando [gerir capturas de pacotes com a REST API](network-watcher-packet-capture-manage-rest.md).</span><span class="sxs-lookup"><span data-stu-id="2e974-115">toolearn how toocreate a packet capture visit [Manage packet captures with hello portal](network-watcher-packet-capture-manage-portal.md) or with REST by visiting [Managing Packet Captures with REST API](network-watcher-packet-capture-manage-rest.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="2e974-116">Cenário</span><span class="sxs-lookup"><span data-stu-id="2e974-116">Scenario</span></span>

<span data-ttu-id="2e974-117">Neste cenário, poderá:</span><span class="sxs-lookup"><span data-stu-id="2e974-117">In this scenario, you:</span></span>

* <span data-ttu-id="2e974-118">Reveja uma captura de pacotes</span><span class="sxs-lookup"><span data-stu-id="2e974-118">Review a packet capture</span></span>

## <a name="calculate-network-latency"></a><span data-ttu-id="2e974-119">Calcular a latência de rede</span><span class="sxs-lookup"><span data-stu-id="2e974-119">Calculate network latency</span></span>

<span data-ttu-id="2e974-120">Neste cenário, mostramos como tooview Olá tempo de ida e volta inicial (RTT) de uma conversação de protocolo de controlo de transmissão (TCP) ocorrer entre dois pontos finais.</span><span class="sxs-lookup"><span data-stu-id="2e974-120">In this scenario, we show how tooview hello initial Round Trip Time (RTT) of a Transmission Control Protocol (TCP) conversation occurring between two endpoints.</span></span>

<span data-ttu-id="2e974-121">Quando é estabelecida uma ligação de TCP, hello três primeiros pacotes enviados na ligação de Olá siga um handshake de três vias padrão geralmente referida tooas Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-121">When a TCP connection is established, hello first three packets sent in hello connection follow a pattern commonly referred tooas hello three-way handshake.</span></span> <span data-ttu-id="2e974-122">Ao examinar Olá primeiro dois pacotes enviados neste handshake, um pedido de cliente de Olá inicial e uma resposta do servidor de Olá, iremos pode calcular a latência de Olá quando esta ligação foi estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2e974-122">By examining hello first two packets sent in this handshake, an initial request from hello client and a response from hello server, we can calculate hello latency when this connection was established.</span></span> <span data-ttu-id="2e974-123">Esta latência é referenciado tooas Olá tempo de ida e volta (RTT).</span><span class="sxs-lookup"><span data-stu-id="2e974-123">This latency is referred tooas hello Round Trip Time (RTT).</span></span> <span data-ttu-id="2e974-124">Para obter mais informações sobre o protocolo TCP Olá e handshake de três vias Olá Consulte toohello os seguintes recursos.</span><span class="sxs-lookup"><span data-stu-id="2e974-124">For more information on hello TCP protocol and hello three-way handshake refer toohello following resource.</span></span> <span data-ttu-id="2e974-125">https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-Three-Way-Handshake-via-TCP-IP</span><span class="sxs-lookup"><span data-stu-id="2e974-125">https://support.microsoft.com/en-us/help/172983/explanation-of-the-three-way-handshake-via-tcp-ip</span></span>

### <a name="step-1"></a><span data-ttu-id="2e974-126">Passo 1</span><span class="sxs-lookup"><span data-stu-id="2e974-126">Step 1</span></span>

<span data-ttu-id="2e974-127">Inicie o WireShark</span><span class="sxs-lookup"><span data-stu-id="2e974-127">Launch WireShark</span></span>

### <a name="step-2"></a><span data-ttu-id="2e974-128">Passo 2</span><span class="sxs-lookup"><span data-stu-id="2e974-128">Step 2</span></span>

<span data-ttu-id="2e974-129">Olá carga **.cap** ficheiro a partir do seu captura de pacotes.</span><span class="sxs-lookup"><span data-stu-id="2e974-129">Load hello **.cap** file from your packet capture.</span></span> <span data-ttu-id="2e974-130">Este ficheiro pode ser encontrado no blob Olá foi guardada na nossa localmente na máquina de virtual Olá, dependendo de como tiver configurado.</span><span class="sxs-lookup"><span data-stu-id="2e974-130">This file can be found in hello blob it was saved in our locally on hello virtual machine, depending on how you configured it.</span></span>

### <a name="step-3"></a><span data-ttu-id="2e974-131">Passo 3</span><span class="sxs-lookup"><span data-stu-id="2e974-131">Step 3</span></span>

<span data-ttu-id="2e974-132">tooview Olá tempo de ida e volta inicial (RTT) no conversações de TCP, iremos será apenas possível observar pacotes hello a duas primeiras envolvidas no handshake TCP Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-132">tooview hello initial Round Trip Time (RTT) in TCP conversations, we will only be looking at hello first two packets involved in hello TCP handshake.</span></span> <span data-ttu-id="2e974-133">Vamos utilizar dois pacotes hello no handshake de três vias Olá, que são Olá [SIN], [SIN, ACK] pacotes.</span><span class="sxs-lookup"><span data-stu-id="2e974-133">We will be using hello first two packets in hello three-way handshake, which are hello [SYN], [SYN, ACK] packets.</span></span> <span data-ttu-id="2e974-134">Estes são denominados para sinalizadores definidas no cabeçalho TCP Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-134">They are named for flags set in hello TCP header.</span></span> <span data-ttu-id="2e974-135">pacote de último Olá no handshake de Olá, pacote Olá [ACK], não será utilizada neste cenário.</span><span class="sxs-lookup"><span data-stu-id="2e974-135">hello last packet in hello handshake, hello [ACK] packet, will not be used in this scenario.</span></span> <span data-ttu-id="2e974-136">pacote de Olá [SIN] é enviado pelo cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-136">hello [SYN] packet is sent by hello client.</span></span> <span data-ttu-id="2e974-137">Quando é recebido o servidor de Olá envia pacotes hello [ACK] como uma confirmação de receção Olá SIN de cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-137">Once it is received hello server sends hello [ACK] packet as an acknowledgement of receiving hello SYN from hello client.</span></span> <span data-ttu-id="2e974-138">Tirar partido das facto Olá que a resposta do servidor de Olá requer overhead muito pouco, iremos calcular Olá RTT ao subtrair tempo Olá pacotes hello [SIN, ACK] foi recebido pelo cliente de Olá pelo pacote de tempo [SIN] Olá foi enviada pelo cliente de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-138">Leveraging hello fact that hello server’s response requires very little overhead, we calculate hello RTT by subtracting hello time hello [SYN, ACK] packet was received by hello client by hello time [SYN] packet was sent by hello client.</span></span>

<span data-ttu-id="2e974-139">Este valor com o WireShark é calculado para-nos.</span><span class="sxs-lookup"><span data-stu-id="2e974-139">Using WireShark this value is calculated for us.</span></span>

<span data-ttu-id="2e974-140">toomore visualizar facilmente pacotes hello a duas primeiras no handshake de três vias TCP Olá, iremos irá utilizar Olá filtragem capacidade fornecida pelo WireShark.</span><span class="sxs-lookup"><span data-stu-id="2e974-140">toomore easily view hello first two packets in hello TCP three-way handshake, we will utilize hello filtering capability provided by WireShark.</span></span>

<span data-ttu-id="2e974-141">filtro de Olá tooapply em WireShark, expanda Olá segmento de "Protocolo de controlo de transmissão" de um pacote de [SIN] no seu captura e examinar os sinalizadores de Olá definidos no cabeçalho TCP Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-141">tooapply hello filter in WireShark, expand hello “Transmission Control Protocol” Segment of a [SYN] packet in your capture and examine hello flags set in hello TCP header.</span></span>

<span data-ttu-id="2e974-142">Uma vez que vamos procura toofilter em todos os [SIN] e [SIN, ACK] pacotes, sob sinalizadores cofirm que Olá sin bit do estiver definido too1, em seguida, clique direito em bits de sin Olá -> aplicar como filtro -> selecionados.</span><span class="sxs-lookup"><span data-stu-id="2e974-142">Since we are looking toofilter on all [SYN] and [SYN, ACK] packets, under flags cofirm that hello Syn bit is set too1, then right click on hello Syn bit -> Apply as Filter -> Selected.</span></span>

![figura 7][7]

### <a name="step-4"></a><span data-ttu-id="2e974-144">Passo 4</span><span class="sxs-lookup"><span data-stu-id="2e974-144">Step 4</span></span>

<span data-ttu-id="2e974-145">Agora que tem filtrado pacotes hello a janela tooonly Consulte com o bit de Olá [SIN] definido, pode selecionar facilmente conversações estiver interessado em tooview Olá RTT inicial.</span><span class="sxs-lookup"><span data-stu-id="2e974-145">Now that you have filtered hello window tooonly see packets with hello [SYN] bit set, you can easily select conversations you are interested in tooview hello initial RTT.</span></span> <span data-ttu-id="2e974-146">Olá de tooview uma forma simples RTT no WireShark basta clicar em dropdown Olá marcado analysis "SEQ/ACK".</span><span class="sxs-lookup"><span data-stu-id="2e974-146">A simple way tooview hello RTT in WireShark simply click hello dropdown marked “SEQ/ACK” analysis.</span></span> <span data-ttu-id="2e974-147">Em seguida, verá Olá que RTT apresentado.</span><span class="sxs-lookup"><span data-stu-id="2e974-147">You will then see hello RTT displayed.</span></span> <span data-ttu-id="2e974-148">Neste caso, Olá RTT foi 0.0022114 segundos ou 2.211 ms.</span><span class="sxs-lookup"><span data-stu-id="2e974-148">In this case, hello RTT was 0.0022114 seconds, or 2.211 ms.</span></span>

![figura 8][8]

## <a name="unwanted-protocols"></a><span data-ttu-id="2e974-150">Protocolos indesejáveis</span><span class="sxs-lookup"><span data-stu-id="2e974-150">Unwanted protocols</span></span>

<span data-ttu-id="2e974-151">Pode ter várias aplicações em execução numa instância de máquina virtual que implementou no Azure.</span><span class="sxs-lookup"><span data-stu-id="2e974-151">You can have many applications running on a virtual machine instance you have deployed in Azure.</span></span> <span data-ttu-id="2e974-152">Muitas destas aplicações comunicam através de rede de Olá, talvez sem a sua permissão explícita.</span><span class="sxs-lookup"><span data-stu-id="2e974-152">Many of these applications communicate over hello network, perhaps without your explicit permission.</span></span> <span data-ttu-id="2e974-153">Utilizar a comunicação de rede de toostore de captura de pacotes, iremos pode investigar como aplicações estão a comunicar na rede de Olá e procure eventuais problemas.</span><span class="sxs-lookup"><span data-stu-id="2e974-153">Using packet capture toostore network communication, we can investigate how application are talking on hello network and look for any issues.</span></span>

<span data-ttu-id="2e974-154">Neste exemplo, vamos rever anterior foi executada a captura de pacotes indesejável protocolos que possam indicar a comunicação não autorizada de uma aplicação em execução no seu computador.</span><span class="sxs-lookup"><span data-stu-id="2e974-154">In this example, we review a previous ran packet capture for unwanted protocols that may indicate unauthorized communication from an application running on your machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="2e974-155">Passo 1</span><span class="sxs-lookup"><span data-stu-id="2e974-155">Step 1</span></span>

<span data-ttu-id="2e974-156">Utilizar Olá mesma captura no Olá anterior cenário, clique em **estatísticas** > **hierarquia de protocolo**</span><span class="sxs-lookup"><span data-stu-id="2e974-156">Using hello same capture in hello previous scenario click **Statistics** > **Protocol Hierarchy**</span></span>

![menu de hierarquia de protocolo][2]

<span data-ttu-id="2e974-158">Surge a janela de hierarquia de protocolo de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-158">hello protocol hierarchy window appears.</span></span> <span data-ttu-id="2e974-159">Esta vista fornece uma lista de todos os protocolos de Olá que estavam a ser utilizadas durante a sessão de captura Olá e número de Olá de pacotes transmitidos e recebidos através de protocolos de Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-159">This view provides a list of all hello protocols that were in use during hello capture session and hello number of packets transmitted and received using hello protocols.</span></span> <span data-ttu-id="2e974-160">Esta vista pode ser útil para localizar indesejável tráfego de rede na sua rede ou de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2e974-160">This view can be useful for finding unwanted network traffic on your virtual machines or network.</span></span>

![hierachy protocolo aberta][3]

<span data-ttu-id="2e974-162">Como pode ver na seguinte captura de ecrã de Olá, ocorreu tráfego através do protocolo de BitTorrent Olá, que é utilizado para a partilha de ficheiros do toopeer de ponto a ponto.</span><span class="sxs-lookup"><span data-stu-id="2e974-162">As you can see in hello following screen capture, there was traffic using hello BitTorrent protocol, which is used for peer toopeer file sharing.</span></span> <span data-ttu-id="2e974-163">Como um administrador não espere toosee BitTorrent tráfego nas específico máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="2e974-163">As an administrator you do not expect toosee BitTorrent traffic on this particular virtual machines.</span></span> <span data-ttu-id="2e974-164">Agora tem em consideração este tráfego, pode remover Olá ponto a ponto toopeer software que instalado nesta máquina virtual ou Olá de bloco através de uma Firewall ou grupos de segurança de rede de tráfego.</span><span class="sxs-lookup"><span data-stu-id="2e974-164">Now you aware of this traffic, you can remove hello peer toopeer software that installed on this virtual machine, or block hello traffic using Network Security Groups or a Firewall.</span></span> <span data-ttu-id="2e974-165">Além disso, pode elecionar toorun capturas de pacotes com base numa agenda, pelo que pode rever Olá protocolo utilizar nas suas máquinas virtuais regularmente.</span><span class="sxs-lookup"><span data-stu-id="2e974-165">Additionally, you may elect toorun packet captures on a schedule, so you can review hello protocol use on your virtual machines regularly.</span></span> <span data-ttu-id="2e974-166">Para obter um exemplo sobre como rede de tooautomate tarefas no azure visite [monitorizem os recursos de rede com a automatização do azure](network-watcher-monitor-with-azure-automation.md)</span><span class="sxs-lookup"><span data-stu-id="2e974-166">For an example on how tooautomate network tasks in azure visit [Monitor network resources with azure automation](network-watcher-monitor-with-azure-automation.md)</span></span>

## <a name="finding-top-destinations-and-ports"></a><span data-ttu-id="2e974-167">Localizar destinos principais e portas</span><span class="sxs-lookup"><span data-stu-id="2e974-167">Finding top destinations and ports</span></span>

<span data-ttu-id="2e974-168">Compreender os tipos de tráfego Olá, Olá pontos finais e comunicadas através de portas de Olá é um importante quando monitorização ou a resolução de problemas de aplicações e recursos na sua rede.</span><span class="sxs-lookup"><span data-stu-id="2e974-168">Understanding hello types of traffic, hello endpoints, and hello ports communicated over is an important when monitoring or troubleshooting applications and resources on your network.</span></span> <span data-ttu-id="2e974-169">Utilizar um ficheiro de captura de pacotes de acima, podemos pode rapidamente saber Olá superior os destinos nosso VM está a comunicar com e Olá portas a ser utilizadas.</span><span class="sxs-lookup"><span data-stu-id="2e974-169">Utilizing a packet capture file from above, we can quickly learn hello top destinations our VM is communicating with and hello ports being utilized.</span></span>

### <a name="step-1"></a><span data-ttu-id="2e974-170">Passo 1</span><span class="sxs-lookup"><span data-stu-id="2e974-170">Step 1</span></span>

<span data-ttu-id="2e974-171">Utilizar Olá mesma captura no Olá anterior cenário, clique em **estatísticas** > **estatísticas de IPv4** > **destinos e portas**</span><span class="sxs-lookup"><span data-stu-id="2e974-171">Using hello same capture in hello previous scenario click **Statistics** > **IPv4 Statistics** > **Destinations and Ports**</span></span>

![janela de captura de pacotes][4]

### <a name="step-2"></a><span data-ttu-id="2e974-173">Passo 2</span><span class="sxs-lookup"><span data-stu-id="2e974-173">Step 2</span></span>

<span data-ttu-id="2e974-174">Como podemos examine os resultados de Olá representa uma linha de, existem várias ligações na porta 111.</span><span class="sxs-lookup"><span data-stu-id="2e974-174">As we look through hello results a line stands out, there were multiple connections on port 111.</span></span> <span data-ttu-id="2e974-175">porta Olá mais utilizado foi 3389, que é o ambiente de trabalho remoto e Olá restantes são portas dinâmicas de RPC.</span><span class="sxs-lookup"><span data-stu-id="2e974-175">hello most used port was 3389, which is remote desktop, and hello remaining are RPC dynamic ports.</span></span>

<span data-ttu-id="2e974-176">Apesar deste tráfego pode significar que nada, é uma porta que foi utilizada para várias ligações e é administrador toohello desconhecido.</span><span class="sxs-lookup"><span data-stu-id="2e974-176">While this traffic may mean nothing, it is a port that was used for many connections and is unknown toohello administrator.</span></span>

![figura 5][5]

### <a name="step-3"></a><span data-ttu-id="2e974-178">Passo 3</span><span class="sxs-lookup"><span data-stu-id="2e974-178">Step 3</span></span>

<span data-ttu-id="2e974-179">Agora que Determinámos uma saída da porta local, pode filtrar a nossa captura com base na porta Olá.</span><span class="sxs-lookup"><span data-stu-id="2e974-179">Now that we have determined an out of place port we can filter our capture based on hello port.</span></span>

<span data-ttu-id="2e974-180">filtro de Olá neste cenário seria:</span><span class="sxs-lookup"><span data-stu-id="2e974-180">hello filter in this scenario would be:</span></span>

```
tcp.port == 111
```

<span data-ttu-id="2e974-181">Iremos introduzir o texto de filtro de Olá de acima na caixa de texto de filtro de Olá e clique em enter.</span><span class="sxs-lookup"><span data-stu-id="2e974-181">We enter hello filter text from above in hello filter textbox and hit enter.</span></span>

![figura 6][6]

<span data-ttu-id="2e974-183">De resultados de Olá, é possível ver todo o tráfego Olá for proveniente de uma máquina virtual local no Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="2e974-183">From hello results, we can see all hello traffic is coming from a local virtual machine on hello same subnet.</span></span> <span data-ttu-id="2e974-184">Se ainda não compreendemos por que motivo está a ocorrer este tráfego, mais iremos pode inspecionar Olá pacotes toodetermine por que motivo que é efetuar estas chamadas na porta 111.</span><span class="sxs-lookup"><span data-stu-id="2e974-184">If we still don’t understand why this traffic is occurring, we can further inspect hello packets toodetermine why it is making these calls on port 111.</span></span> <span data-ttu-id="2e974-185">Com esta informação é pode ação Olá adequado.</span><span class="sxs-lookup"><span data-stu-id="2e974-185">With this information we can take hello appropriate action.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e974-186">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2e974-186">Next steps</span></span>

<span data-ttu-id="2e974-187">Saiba mais sobre Olá outras funcionalidades de diagnóstico do observador de rede, visitando [descrição geral da monitorização de rede do Azure](network-watcher-monitoring-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2e974-187">Learn about hello other diagnostic features of Network Watcher by visiting [Azure network monitoring overview](network-watcher-monitoring-overview.md)</span></span>

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













