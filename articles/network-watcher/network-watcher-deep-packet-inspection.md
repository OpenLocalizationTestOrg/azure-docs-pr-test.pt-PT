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
# <a name="packet-inspection-with-azure-network-watcher"></a>Inspeção de pacotes com observador de rede do Azure

Utilizar a funcionalidade de captura de pacotes hello do observador de rede, pode iniciar e gerir sessões de capturas nas suas VMs do Azure a partir do portal Olá, PowerShell CLI e através de programação através de Olá SDK e a REST API. Captura de pacotes permite-lhe tooaddress cenários que necessitam de dados ao nível do pacote, fornecendo informações Olá num formato prontamente utilizável. Tirar partido dos dados de Olá tooinspect de ferramentas livremente disponíveis, pode examinar comunicações enviadas tooand do seu VMs e obter informações sobre o tráfego de rede. Incluem algumas utilizações de exemplo de dados de captura de pacotes: investigar problemas de rede ou aplicação, detetar tentativas de utilização indevida e intrusão de rede ou manter a conformidade regulamentar. Neste artigo, mostramos como tooopen um ficheiro de captura de pacotes fornecido por observador de rede utilizando uma ferramenta open source para populares. Fornecemos também exemplos que mostra como identificar tráfego anormal toocalculate uma latência de ligação e examine as estatísticas de rede.

## <a name="before-you-begin"></a>Antes de começar

Este artigo passa através de alguns cenários previamente configurados uma captura de pacotes que foi anteriormente executada com êxito. Estes cenários mostram capacidades que podem ser acedidas ao rever uma captura de pacotes. Este cenário utiliza [WireShark](https://www.wireshark.org/) captura de pacotes de Olá tooinspect.

Este cenário pressupõe que já tenha sido executada uma captura de pacotes numa máquina virtual. toolearn como toocreate uma captura de pacotes visite [capturas de pacotes de gerir com o portal de Olá](network-watcher-packet-capture-manage-portal.md) ou com REST, visitando [gerir capturas de pacotes com a REST API](network-watcher-packet-capture-manage-rest.md).

## <a name="scenario"></a>Cenário

Neste cenário, poderá:

* Reveja uma captura de pacotes

## <a name="calculate-network-latency"></a>Calcular a latência de rede

Neste cenário, mostramos como tooview Olá tempo de ida e volta inicial (RTT) de uma conversação de protocolo de controlo de transmissão (TCP) ocorrer entre dois pontos finais.

Quando é estabelecida uma ligação de TCP, hello três primeiros pacotes enviados na ligação de Olá siga um handshake de três vias padrão geralmente referida tooas Olá. Ao examinar Olá primeiro dois pacotes enviados neste handshake, um pedido de cliente de Olá inicial e uma resposta do servidor de Olá, iremos pode calcular a latência de Olá quando esta ligação foi estabelecida. Esta latência é referenciado tooas Olá tempo de ida e volta (RTT). Para obter mais informações sobre o protocolo TCP Olá e handshake de três vias Olá Consulte toohello os seguintes recursos. https://support.microsoft.com/en-US/Help/172983/Explanation-of-the-Three-Way-Handshake-via-TCP-IP

### <a name="step-1"></a>Passo 1

Inicie o WireShark

### <a name="step-2"></a>Passo 2

Olá carga **.cap** ficheiro a partir do seu captura de pacotes. Este ficheiro pode ser encontrado no blob Olá foi guardada na nossa localmente na máquina de virtual Olá, dependendo de como tiver configurado.

### <a name="step-3"></a>Passo 3

tooview Olá tempo de ida e volta inicial (RTT) no conversações de TCP, iremos será apenas possível observar pacotes hello a duas primeiras envolvidas no handshake TCP Olá. Vamos utilizar dois pacotes hello no handshake de três vias Olá, que são Olá [SIN], [SIN, ACK] pacotes. Estes são denominados para sinalizadores definidas no cabeçalho TCP Olá. pacote de último Olá no handshake de Olá, pacote Olá [ACK], não será utilizada neste cenário. pacote de Olá [SIN] é enviado pelo cliente de Olá. Quando é recebido o servidor de Olá envia pacotes hello [ACK] como uma confirmação de receção Olá SIN de cliente de Olá. Tirar partido das facto Olá que a resposta do servidor de Olá requer overhead muito pouco, iremos calcular Olá RTT ao subtrair tempo Olá pacotes hello [SIN, ACK] foi recebido pelo cliente de Olá pelo pacote de tempo [SIN] Olá foi enviada pelo cliente de Olá.

Este valor com o WireShark é calculado para-nos.

toomore visualizar facilmente pacotes hello a duas primeiras no handshake de três vias TCP Olá, iremos irá utilizar Olá filtragem capacidade fornecida pelo WireShark.

filtro de Olá tooapply em WireShark, expanda Olá segmento de "Protocolo de controlo de transmissão" de um pacote de [SIN] no seu captura e examinar os sinalizadores de Olá definidos no cabeçalho TCP Olá.

Uma vez que vamos procura toofilter em todos os [SIN] e [SIN, ACK] pacotes, sob sinalizadores cofirm que Olá sin bit do estiver definido too1, em seguida, clique direito em bits de sin Olá -> aplicar como filtro -> selecionados.

![figura 7][7]

### <a name="step-4"></a>Passo 4

Agora que tem filtrado pacotes hello a janela tooonly Consulte com o bit de Olá [SIN] definido, pode selecionar facilmente conversações estiver interessado em tooview Olá RTT inicial. Olá de tooview uma forma simples RTT no WireShark basta clicar em dropdown Olá marcado analysis "SEQ/ACK". Em seguida, verá Olá que RTT apresentado. Neste caso, Olá RTT foi 0.0022114 segundos ou 2.211 ms.

![figura 8][8]

## <a name="unwanted-protocols"></a>Protocolos indesejáveis

Pode ter várias aplicações em execução numa instância de máquina virtual que implementou no Azure. Muitas destas aplicações comunicam através de rede de Olá, talvez sem a sua permissão explícita. Utilizar a comunicação de rede de toostore de captura de pacotes, iremos pode investigar como aplicações estão a comunicar na rede de Olá e procure eventuais problemas.

Neste exemplo, vamos rever anterior foi executada a captura de pacotes indesejável protocolos que possam indicar a comunicação não autorizada de uma aplicação em execução no seu computador.

### <a name="step-1"></a>Passo 1

Utilizar Olá mesma captura no Olá anterior cenário, clique em **estatísticas** > **hierarquia de protocolo**

![menu de hierarquia de protocolo][2]

Surge a janela de hierarquia de protocolo de Olá. Esta vista fornece uma lista de todos os protocolos de Olá que estavam a ser utilizadas durante a sessão de captura Olá e número de Olá de pacotes transmitidos e recebidos através de protocolos de Olá. Esta vista pode ser útil para localizar indesejável tráfego de rede na sua rede ou de máquinas virtuais.

![hierachy protocolo aberta][3]

Como pode ver na seguinte captura de ecrã de Olá, ocorreu tráfego através do protocolo de BitTorrent Olá, que é utilizado para a partilha de ficheiros do toopeer de ponto a ponto. Como um administrador não espere toosee BitTorrent tráfego nas específico máquinas virtuais. Agora tem em consideração este tráfego, pode remover Olá ponto a ponto toopeer software que instalado nesta máquina virtual ou Olá de bloco através de uma Firewall ou grupos de segurança de rede de tráfego. Além disso, pode elecionar toorun capturas de pacotes com base numa agenda, pelo que pode rever Olá protocolo utilizar nas suas máquinas virtuais regularmente. Para obter um exemplo sobre como rede de tooautomate tarefas no azure visite [monitorizem os recursos de rede com a automatização do azure](network-watcher-monitor-with-azure-automation.md)

## <a name="finding-top-destinations-and-ports"></a>Localizar destinos principais e portas

Compreender os tipos de tráfego Olá, Olá pontos finais e comunicadas através de portas de Olá é um importante quando monitorização ou a resolução de problemas de aplicações e recursos na sua rede. Utilizar um ficheiro de captura de pacotes de acima, podemos pode rapidamente saber Olá superior os destinos nosso VM está a comunicar com e Olá portas a ser utilizadas.

### <a name="step-1"></a>Passo 1

Utilizar Olá mesma captura no Olá anterior cenário, clique em **estatísticas** > **estatísticas de IPv4** > **destinos e portas**

![janela de captura de pacotes][4]

### <a name="step-2"></a>Passo 2

Como podemos examine os resultados de Olá representa uma linha de, existem várias ligações na porta 111. porta Olá mais utilizado foi 3389, que é o ambiente de trabalho remoto e Olá restantes são portas dinâmicas de RPC.

Apesar deste tráfego pode significar que nada, é uma porta que foi utilizada para várias ligações e é administrador toohello desconhecido.

![figura 5][5]

### <a name="step-3"></a>Passo 3

Agora que Determinámos uma saída da porta local, pode filtrar a nossa captura com base na porta Olá.

filtro de Olá neste cenário seria:

```
tcp.port == 111
```

Iremos introduzir o texto de filtro de Olá de acima na caixa de texto de filtro de Olá e clique em enter.

![figura 6][6]

De resultados de Olá, é possível ver todo o tráfego Olá for proveniente de uma máquina virtual local no Olá mesma sub-rede. Se ainda não compreendemos por que motivo está a ocorrer este tráfego, mais iremos pode inspecionar Olá pacotes toodetermine por que motivo que é efetuar estas chamadas na porta 111. Com esta informação é pode ação Olá adequado.

## <a name="next-steps"></a>Passos seguintes

Saiba mais sobre Olá outras funcionalidades de diagnóstico do observador de rede, visitando [descrição geral da monitorização de rede do Azure](network-watcher-monitoring-overview.md)

[1]: ./media/network-watcher-deep-packet-inspection/figure1.png
[2]: ./media/network-watcher-deep-packet-inspection/figure2.png
[3]: ./media/network-watcher-deep-packet-inspection/figure3.png
[4]: ./media/network-watcher-deep-packet-inspection/figure4.png
[5]: ./media/network-watcher-deep-packet-inspection/figure5.png
[6]: ./media/network-watcher-deep-packet-inspection/figure6.png
[7]: ./media/network-watcher-deep-packet-inspection/figure7.png
[8]: ./media/network-watcher-deep-packet-inspection/figure8.png













