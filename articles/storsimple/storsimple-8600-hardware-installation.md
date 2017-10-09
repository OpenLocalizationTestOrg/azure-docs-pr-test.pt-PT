---
title: dispositivo aaaInstall 8600 do Microsoft Azure StorSimple | Microsoft Docs
description: "Descreve como toounpack, montar em bastidor e instalar os cabos do dispositivo StorSimple 8600 antes de implementar e configurar o software de Olá."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3d82ba5f-3e34-40dc-9c33-50f952bc6be8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 10/24/2016
ms.author: alkohli
ms.openlocfilehash: 0fc0ddf076725fededdde33a260b950b72edc8db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="unpack-rack-mount-and-cable-your-storsimple-8600-device"></a>Descompactar, montar em bastidor e instalar os cabos do dispositivo StorSimple 8600
## <a name="overview"></a>Descrição geral
Os cabos do 8600 Microsoft Azure StorSimple é um dispositivo duplo bastidor e é composta por um site primário e um bastidor EBOD. Este tutorial explica como toounpack, montar em bastidor e instalar os cabos Olá de hardware do dispositivo StorSimple 8600 antes de configurar o software do Olá StorSimple.

## <a name="unpack-your-storsimple-8600-device"></a>Descompacte o dispositivo StorSimple 8600
Olá passos seguintes fornecem limpar, instruções detalhadas sobre como toounpack o dispositivo de armazenamento StorSimple 8600. Este dispositivo está incluído em duas caixas, para inclusão principal Olá e outra para Olá bastidor EBOD. Estas duas caixas, em seguida, são colocadas numa única caixa.

### <a name="prepare-toounpack-your-device"></a>Preparar o seu dispositivo toounpack
Antes de Descompacte o seu dispositivo, reveja Olá informações a seguir.

![Ícone de aviso](./media/storsimple-safety/IC740879.png)![ícone de ponderação pesada](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **aviso!**

1. Certifique-se de que tem duas pessoas toomanage disponíveis Olá peso de dispositivo Olá se são processamento manualmente. Um bastidor totalmente configurado pode pesar segurança too32 kg (70 lbs.).
2. Coloque caixa Olá na superfície simples, nível.

Em seguida, conclua Olá toounpack passos a seguir o dispositivo.

#### <a name="toounpack-your-device"></a>toounpack o dispositivo
1. Inspecione caixa Olá e foam de empacotamento de Olá crushes, cuts, máximo danos ou quaisquer outros danos óbvios. Se a caixa de Olá ou empacotamento gravemente está danificado, não abra a caixa de Olá. . [Contacte a Microsoft Support](storsimple-contact-microsoft-support.md) toohelp avaliar se o dispositivo de Olá está por ordem bom funcionamento.
2. Abrir a caixa externa Olá e, em seguida, remova Olá dois as caixas correspondentes tooprimary e inclusões EBOD. Agora pode descompactar Olá primário e inclusões EBOD. Olá figura a seguir mostra a vista de Olá descompactado de uma das caixas de Olá.
   
    ![Descompacte o seu dispositivo de armazenamento](./media/storsimple-8600-hardware-installation/HCSUnpackyour4Udevice.png)
   
    **Vista descompactada do seu dispositivo de armazenamento**
   
   | Etiqueta | Descrição |
   | --- | --- |
   |   1 |Caixa de mais |
   |   2 |Cabos SAS (no tabuleiro acessórios e cabos) |
   |   3 |Foam inferior |
   |   4 |Dispositivo |
   |   5 |Foam superior |
   |   6 |Caixa acessórios |
3. Após unpacking caixas Olá dois, certifique-se de que tem:
   
   * 1 inclusão principal (inclusão principal Olá e inclusão EBOD são nas duas caixas separadas)
   * Inclusão EBOD 1
   * 4 cabos, 2 em cada caixa de energia
   * 2 cabos SAS (tooconnect Olá inclusão principal tooEBOD a inclusão de bastidor)
   * 1 cruzado cabo de Ethernet
   * 2 cabos de consola de série
   * 1 USB de série conversor para acesso de série
   * 4 QSFP-para-SFP + adaptadores para utilização com as interfaces de rede de 10 GbE
   * 2 em Bastidor kits de montagem (o 4 rails de lado com montar hardware, 2 para inclusão principal Olá e inclusão EBOD), 1 em cada caixa
   * Obter a documentação de introdução
     
     Se não recebeu qualquer um dos itens de Olá listados acima, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md).  

passo seguinte Olá é toorack montagem seu dispositivo.

## <a name="rack-mount-your-storsimple-8600-device"></a>Montar em Bastidor o dispositivo StorSimple 8600
Siga Olá seguinte passos tooinstall o dispositivo de armazenamento StorSimple 8600 num bastidor 19 polegadas padrão com front-end e rear publicações. Este dispositivo é fornecida com dois inclusões: um bastidor primário e um bastidor EBOD. Ambos têm toobe eletrodomésticos montados.

instalação de Olá é composta por vários passos, cada um dos quais é abordada em Olá os seguintes procedimentos.

> [!IMPORTANT]
> Dispositivos StorSimple tem de ser eletrodomésticos montados para um funcionamento correto.
> 
> 

### <a name="site-preparation"></a>Preparação do site
inclusões de Olá tem de ser instalados num bastidor 19 polegadas padrão que tenha o front-end e rear publicações. Utilize Olá seguir o procedimento tooprepare para a instalação de bastidor.

#### <a name="tooprepare-hello-site-for-rack-installation"></a>site de Olá tooprepare para a instalação de bastidor
1. Certifique-se de que Olá primário e inclusões EBOD são resting em segurança numa superfície de trabalho simples, estável e nível (ou semelhante).
2. Certifique-se esse site olá onde pretende tooset cópias de segurança tem de AC padrão de ativação de uma origem independente ou um bastidor de unidade de distribuição de energia (PDU) com um de alimentação ininterrupta (UPS).
3. Certifique-se que ranhura de (2U de X 2) um 4U disponível no bastidor Olá no qual pretende inclusões de Olá toomount.

![Ícone de aviso](./media/storsimple-safety/IC740879.png)![ícone de ponderação pesada](./media/storsimple-8600-hardware-installation/HCS_HeavyWeight_Icon.png) **aviso!**

 Certifique-se de que tem duas peso da Olá pessoas toomanage disponível se estiver a processar a configuração de dispositivo Olá manualmente. Um bastidor totalmente configurado pode pesar segurança too32 kg (70 lbs.).

### <a name="rack-prerequisites"></a>Pré-requisitos de bastidor
inclusões de Olá foram concebidos para instalação num bastidor 19 polegadas padrão cab com:

* Profundidade mínima de polegadas 27.84 de bastidor publique toopost
* Ponderação máxima de 32 kg para dispositivo Olá
* Pressão de back-máximo de 5 Pascal (0.5 mm máximo medidor)

### <a name="rack-mounting-rail-kit"></a>Kit de lado de montagem de bastidor
Um conjunto de montar rails será fornecido para utilização com o ficheiro CAB de bastidor 19 polegadas Olá. rails Olá foram testadas ponderação do toohandle Olá bastidor máximo. Estes rails também irão permitir a instalação de múltiplas inclusões sem perda de espaço no bastidor Olá. Instale a inclusão EBOD Olá primeiro.

#### <a name="tooinstall-hello-ebod-enclosure-on-hello-rails"></a>Olá tooinstall bastidor EBOD no rails Olá
1. Execute este passo apenas se rails internas não estão instalados no seu dispositivo. Normalmente, rails interna Olá são instalados na fábrica de Olá. Se rails não estiver instalados, instale os lados de toohello Olá slides lado esquerdo e do lado direito de chassis de inclusão de Olá. Se anexar utilizando seis screws métricas em cada lado. toohelp com orientação, lado Olá slides estão marcados **LH – frente** e **RH – frente**, e de fim Olá que é affixed para rear Olá de inclusão de Olá tem um fim tapered.
   
    ![Anexar lado slides tooenclosure chassis](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoEnclosureChassis.png)
   
    **Anexar lado slides toohello lados de inclusão de Olá**
   
   | Etiqueta | Descrição |
   | --- | --- |
   |  1 |M, 3, 4 screws head do botão |
   |  2 |Slides de chassis |
2. Anexe o lado esquerdo Olá e lado direito assemblagens toohello bastidor cab vertical membros. Retos Olá estão marcados **LH**, **RH**, e **este lado segurança** tooguide que sentido correcto.
3. Localize os pins de lado de Olá em frente Olá e rear da assemblagem de lado de Olá. Expandir Olá lado toofit entre Olá bastidor publicações e inserir pins Olá holes de membro vertical Olá front e rear bastidor post. Lembre-se de que a assemblagem de lado de Olá ser nível.
4. Proteja Olá bastidor toohello assemblagem de lado membros verticais utilizando dois screws métrica Olá fornecidos. Utilize um screw em frente Olá e um rear Olá.
5. Repita estes passos para Olá outra assemblagem lado.
   
     ![Anexar lado slides toorack Cab](./media/storsimple-8600-hardware-installation/HCSAttachingRailSlidestoRackCabinet.png)
   
    **A anexar o bastidor de toohello de assemblagens lado**
   
   | Etiqueta | Descrição |
   | --- | --- |
   |   1 |Clamping screw |
   |   2 |Bastidor quadrada hole de front-post screw |
   |   3 |À esquerda pins de localização de lado de front- |
   |   4 |Clamping screw |
   |   5 |Pins de localização do lado esquerdo de rear |

### <a name="mounting-hello-ebod-enclosure-in-hello-rack"></a>Montar a inclusão EBOD Olá num bastidor Olá
Utilizando rails de bastidor Olá que apenas foram instaladas, execute Olá os seguintes passos toomount Olá EBOD a inclusão de bastidor num bastidor Olá.

#### <a name="toomount-hello-ebod-enclosure"></a>Olá toomount bastidor EBOD
1. Com um assistente, bastidor Olá de comparação de precisão e alinhá-lo com rails de bastidor Olá.
2. Cuidadosamente inserir bastidor Olá rails Olá e, em seguida, enviá-lo completamente no bastidor Olá Cab.
   
    ![A inserir o dispositivo num bastidor Olá](./media/storsimple-8600-hardware-installation/HCSInsertingDeviceintheRack.png)
   
    **Montar a inclusão de Olá num bastidor Olá**
3. Remova Olá esquerda e caps flange direito front ao extrair caps Olá livres. caps de flange Olá simplesmente snap no Olá flanges.
4. Proteja o bastidor Olá em Bastidor Olá instalando um screw Phillips head fornecido através de cada flange, esquerda e da direita.
5. Instale o caps de flange Olá ao premi-los numa posição e ajuste-los no local.
   
     ![Instalar a funcionalidade caps de flange](./media/storsimple-8600-hardware-installation/HCSInstallingFlangeCaps.png)
   
    **Instalar a funcionalidade caps de flange Olá**
   
   | Etiqueta | Descrição |
   | --- | --- |
   |   1 |Screw fastening de inclusão |

### <a name="mounting-hello-primary-enclosure-in-hello-rack"></a>Montar a inclusão principal do Olá num bastidor Olá
Depois de concluída a montar a inclusão EBOD Olá, terá de inclusão principal do toomount Olá seguinte Olá mesmos passos.

> [!NOTE]
> * É possível toohave alguns ranhuras vazias no Olá em Bastidor entre inclusão principal Olá e inclusão EBOD Olá.
> * Utilize Olá fornecido 2m SAS cabo tooconnect Olá inclusão principal toohello EBOD inclusão.
> * Não existem sem restrições de posicionamento relativo de Olá de Olá head unidade toohello EBOD unidade. Por conseguinte, bastidor primário Olá pode ser colocado na ranhura superior Olá e inclusão EBOD Olá abaixo — ou vice-versa.
> 
> 

passo seguinte Olá é toocable o dispositivo de alimentação, rede e acesso de série.

## <a name="cable-your-storsimple-8600-device"></a>Instalar os cabos do dispositivo StorSimple 8600
Olá procedimentos seguintes explicam como toocable dispositivo StorSimple 8600 de alimentação, rede e ligações de série.

### <a name="prerequisites"></a>Pré-requisitos
Antes de começar toocable do seu dispositivo, terá de:

* A inclusão principal e a inclusão EBOD Olá, completamente descompactado
* 4 cabos de energia (2 cada para Olá primário e Olá bastidor EBOD) fornecido com o seu dispositivo
* 2 cabos SAS fornecido com Olá do Olá dispositivo tooconnect inclusão principal do EBOD bastidor toohello
* Acesso too2 energia unidades de distribuição (PDUs) (recomendado)
* Cabos de rede
* Fornecido cabos de série
* Conversor de USB de série com o controlador adequado Olá instalado no seu PC (se necessário)
* Fornecido 4 QSFP-para-SFP + adaptadores para utilização com as interfaces de rede de 10 GbE
* [Hardware suportado para interfaces de rede Olá 10 GbE no dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)

### <a name="sas-and-power-cabling"></a>SAS e de cabos de energia
O dispositivo tem um bastidor primário e um bastidor EBOD. Isto requer Olá unidades toobe instalou os cabos em conjunto para conectividade Serial Attached SCSI (SAS) e de energia.

Quando configurar este dispositivo para Olá pela primeira vez, execute os passos de Olá para SAS cablagem pela primeira vez e Olá, em seguida, concluir os passos para power cablagem.

[!INCLUDE [storsimple-cable-8600-for-SAS](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

### <a name="network-cabling"></a>Cabos de rede
O seu dispositivo é uma configuração de modo de espera ativo: em qualquer momento, um módulo de controlador está ativo e processar todas as operações de disco e da rede ao hello outro módulo controlador está no modo de espera. Se ocorrer uma falha de controlador, controlador de reserva dinâmica Olá ativa imediatamente e continua a todas as operações de disco e de rede de Olá.

toosupport esta ativação pós-falha controlador redundante, terá de toocable o dispositivo de rede conforme mostrado no Olá os seguintes passos.

#### <a name="toocable-for-network-connection"></a>toocable para ligação de rede
1. O dispositivo tem seis interfaces de rede em cada controlador: quatro 1 Gbps e 10 de duas portas Gbps Ethernet. Consulte toohello seguindo as portas de dados do ilustração tooidentify Olá do Olá backplane do seu dispositivo.
   
     ![Backplane do dispositivo 8600](./media/storsimple-8600-hardware-installation/HCSBackplaneof2UDevicewithPortsLabeled.jpg)
   
    **Efetue uma cópia do seu dispositivo que mostra o Olá portas de dados**
   
   | Etiqueta | Descrição |
   | --- | --- |
   |   0,1,4,5 |Interfaces de rede de 1 GbE |
   |   2,3 |Interfaces de rede de 10 GbE |
   |   6 |Portas série |
2. Consulte Olá seguinte diagrama de cabos de rede. (a configuração de rede mínimas Olá é apresentada por linhas azuis sólidas. Para elevada disponibilidade e desempenho, necessária configuração adicional é apresentada por linhas ponteada.)

![Instalar os cabos do dispositivo de rede 4U](./media/storsimple-8600-hardware-installation/HCSCableYour4UDeviceforNetwork.png)

**Cablagem para o seu dispositivo de rede**

| Etiqueta | Descrição |
| --- | --- |
| A |LAN com acesso à Internet |
| B |Controlador 0 |
| C |PCM 0 |
| D |Controlador 1 |
| I |PCM 1 |
| F |Controlador EBOD 0 |
| G |Controlador EBOD 1 |
| H, POSSO |Anfitriões (por exemplo, servidores de ficheiros) |
| 0-5 |Interfaces de rede |
| 6 |Inclusão principal |
| 7 |Inclusão EBOD |

Quando cablagem dispositivo Olá, a configuração mínima de Olá necessita:

* Pelo menos duas interfaces de rede ligados em cada controlador com um para acesso à nuvem e outro para iSCSI. Olá dados 0 a porta é automaticamente ativada e configurada através da consola de série de Olá do dispositivo Olá. Para além dos dados 0, outra porta de dados também tem de toobe configurada por meio de Olá portal clássico do Azure. Neste caso, ligar dados 0 porta toohello primário LAN (rede com acesso à Internet). Olá outros dados portas podem ser ligados segmento de LAN (VLAN) tooSAN/iSCSI da rede Olá, dependendo da função de Olá pretendido.
* Interfaces idênticas em cada controlador ligado toohello mesmo rede tooensure disponibilidade se ocorrer uma ativação pós-falha de controlador. Por exemplo, se escolher tooconnect dados 0 e 3 de dados para um dos controladores de Olá, terá de Olá tooconnect correspondente dados 0 e dados 3 no Olá outro controlador.

Tenha em consideração para elevada disponibilidade e desempenho:

* Sempre que possível, configure um par de interface de rede para acesso à nuvem (de 1 GbE) e outro par de iSCSI (10 GbE recomendado) em cada controlador.
* Sempre que possível, ligar interfaces de rede de cada tootwo diferentes comutadores tooensure disponibilidade do controlador de contra uma falha de comutador. a figura Olá ilustra Olá dois 10 GbE interfaces de rede, dados 2 e dados 3, de cada controlador ligado tootwo diferentes comutadores. Para obter mais informações, consulte toohello **interfaces de rede** em Olá [requisitos de elevada disponibilidade para o dispositivo StorSimple](storsimple-system-requirements.md#high-availability-requirements-for-storsimple).

> [!NOTE]
> Se utilizar SFP + transcetores com as interfaces de rede 10 GbE, utilize Olá fornecido QSFP-SFP + adaptadores. Para mais informações, visite demasiado[hardware suportado para interfaces de rede Olá 10 GbE no dispositivo StorSimple](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
> 
> 

### <a name="serial-port-cabling"></a>Cablagem de porta série
Efetue Olá toocable passos a seguir a porta série.

#### <a name="toocable-for-serial-connection"></a>toocable para ligação de série
1. O dispositivo tem uma porta série em cada controlador de que é identificado por um ícone de chave inglesa. toolocate a portas série de Olá, consulte toohello ilustração que mostra as portas de dados de Olá no Olá back of o seu dispositivo.
2. Identifique o controlador de Olá Active Directory no seu backplane do dispositivo. Um LED azul intermitente indica que desse controlador Olá está ativo.
3. Utilize o cabo de série de Olá fornecido (se necessário, conversor de Olá USB de série para o seu computador portátil) e ligar o seu computador ou a consola (com o dispositivo de toohello de emulação do terminal) de porta série toohello controlador ativo Olá.
4. Instale controladores USB de série de Olá (vem incluídos no dispositivo Olá) no seu computador.
5. Configure a ligação de série de Olá da seguinte forma:
   
   * 115,200 transmissão.
   * bits de 8 dados
   * bits de 1 paragem
   * Não existem paridade
   * Controlo de fluxo definido demasiado**None**
6. Certifique-se de que a ligação de Olá está a funcionar, premindo Enter na consola de Olá. Um menu da consola de série deve aparecer.

> [!NOTE]
> **Gestão de KVM:** quando o dispositivo de Olá é instalado num centro de dados remoto ou uma sala de computador com acesso limitado, certifique-se que os controladores de tooboth de ligações série Olá sempre comutador da consola de série de tooa ligado ou equipamento semelhante. Isto permite o controlo remoto de fora de banda e as operações de suporte em caso de interrupção de rede ou falhas inesperadas.
> 
> 

Concluiu o dispositivo para poder de acesso à rede, de cablagem e connection.hello série próximo passo é o software de Olá tooconfigure no seu dispositivo.

## <a name="next-steps"></a>Passos seguintes
Agora, está pronto demasiado[implementar e configurar o dispositivo StorSimple no local](storsimple-deployment-walkthrough-u2.md).

