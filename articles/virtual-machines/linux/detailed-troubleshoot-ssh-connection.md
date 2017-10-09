---
title: "a resolução de SSH aaaDetailed para uma VM do Azure | Microsoft Docs"
description: "Mais passos para ligar tooan máquina virtual do Azure de problemas de resolução de problemas de SSH"
keywords: "SSH ligação recusada, ssh erro, azure ssh, ligação SSH falhou"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>SSH detalhada passos para ligar tooa VM com Linux no Azure de problemas de resolução de problemas
Existem muitos motivos possíveis que o cliente SSH Olá poderá não ser capaz de tooreach Olá SSH serviço Olá VM. Se seguiu através de Olá mais [SSH geral passos de resolução de problemas](troubleshoot-ssh-connection.md), terá de toofurther resolver o problema de ligação de Olá. Este artigo orienta-o toodetermine de passos de resolução de problemas detalhada onde está a falhar Olá ligação SSH e como tooresolve-lo.

## <a name="take-preliminary-steps"></a>Siga os passos preliminares
Olá diagrama seguinte mostra os componentes de Olá envolvidos.

![Diagrama que mostra os componentes do serviço SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

Olá passos seguintes ajudá-lo isolar origem Olá de falha de Olá e descobrir soluções ou soluções.

1. Verifique o estado de Olá de Olá VM no portal de Olá.
   No Olá [portal do Azure](https://portal.azure.com), selecione **máquinas virtuais** > *nome da VM*.

   Olá painel de estado para Olá VM deve mostrar **executar**. Desloque para baixo tooshow atividade recente para computação, armazenamento e recursos de rede.

2. Selecione **definições** tooexamine pontos finais, endereços IP, grupos de segurança de rede e outras definições.

   Olá VM deve ter um ponto final definido para o tráfego SSH que pode ver na **pontos finais** ou  **[grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md)**. Pontos finais em VMs que foram criadas utilizando o Gestor de recursos são armazenados num grupo de segurança de rede. Além disso, certifique-se de que as regras de Olá tem sido aplicados toohello grupo de segurança de rede e que está a referenciados na sub-rede Olá.

conectividade de rede tooverify, verifique pontos finais de Olá configurado e ver se pode aceder Olá VM através de outro protocolo, tal como HTTP ou outro serviço.

Após estes passos, tente Olá SSH a ligação de novo.

## <a name="find-hello-source-of-hello-issue"></a>Localizar Olá origem do problema Olá
cliente SSH Olá no seu computador poderão falhar tooreach Olá SSH serviço Olá VM do Azure devido tooissues ou configurações incorretas nas Olá seguintes áreas:

* [Computador de cliente SSH](#source-1-ssh-client-computer)
* [Dispositivo de limite de organização](#source-2-organization-edge-device)
* [Ponto final do serviço em nuvem e de acesso (ACL) de lista de controlo](#source-3-cloud-service-endpoint-and-acl)
* [Grupos de segurança de rede](#source-4-network-security-groups)
* [VM do Azure baseados em Linux](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>Origem de 1: SSH computador cliente
tooeliminate o computador como origem de Olá de falha de Olá, certifique-se de que pode tornar a SSH ligações tooanother no local, computador baseado em Linux.

![Diagrama realça os componentes de computador do cliente SSH](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Se falhar a ligação de Olá, verifique a existência de Olá os seguintes problemas no seu computador:

* Uma definição de local firewall que está a bloquear o tráfego SSH de entrada ou de saída (TCP 22)
* Instalado localmente o software de proxy do cliente que está a impedir ligações SSH
* Localmente instalado software que está a impedir ligações SSH da monitorização de rede
* Outros tipos de software de segurança que monitorizar o tráfego ou permitirem/não permitir tipos específicos de tráfego

Se uma das seguintes condições aplicam-se, temporariamente desative o software de Olá e tente um computador toofind do SSH ligação tooan no local, causa Olá ligação Olá está a ser bloqueada no seu computador. Em seguida, trabalhe com o seu administrador toocorrect Olá software definições tooallow SSH ligações de rede.

Se estiver a utilizar a autenticação de certificado, certifique-se de que tem estes pasta do permissões toohello. SSH no seu diretório raiz:

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*pub
* Chmod 600 ~/.ssh/id_rsa (ou outros ficheiros que tenham as chaves privadas armazenadas nelas)
* Chmod 644 ~/.ssh/known_hosts (contém anfitriões que tenha ligado toovia SSH)

## <a name="source-2-organization-edge-device"></a>Origem 2: Dispositivo de limite de organização
tooeliminate o dispositivo de limite de organização como origem de Olá de falha de Olá, certifique-se de que um computador que tenha diretamente ligado toohello Internet pode efetuar a SSH ligações tooyour VM do Azure. Se estiver a aceder Olá VM através de uma VPN de site para site ou uma ligação ExpressRoute do Azure, ignore demasiado[origem 4: grupos de segurança de rede](#nsg).

![Diagrama realça o dispositivo de limite de organização](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

Se não tiver um computador que seja toohello diretamente ligado à Internet, crie uma nova VM do Azure no seu próprio serviço de nuvem ou grupo de recursos e utilizá-lo. Para obter mais informações, consulte [criar uma máquina virtual com Linux no Azure](quick-create-cli.md). Elimine o serviço de grupo ou a VM e a nuvem de recursos de Olá quando tiver terminado com os seus testes.

Se é possível criar uma ligação SSH com um computador que tenha diretamente ligado toohello Internet, verifique o seu dispositivo de limite de organização para:

* Uma firewall interno que está a bloquear o tráfego SSH com Olá Internet
* Um servidor proxy que está a impedir ligações SSH
* Deteção de intrusões ou software em execução em dispositivos na sua rede de limite que está a impedir ligações SSH de monitorização de rede

Trabalhar com o seu administrador toocorrect Olá as definições de rede da organização edge dispositivos tooallow SSH tráfego com Olá Internet.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>Origem 3: Ponto final do serviço de nuvem e a ACL
> [!NOTE]
> Esta origem de aplica-se apenas tooVMs que foram criadas utilizando o modelo de implementação clássica Olá. Para VMs que foram criadas utilizando o Gestor de recursos, ignorar demasiado[origem 4: grupos de segurança de rede](#nsg).

ponto final do serviço de nuvem de Olá do tooeliminate e ACL como origem de Olá de falha de Olá, certifique-se de que Olá outra VM do Azure na mesma rede virtual pode efetuar a SSH ligações tooyour VM.

![Diagrama realça o ponto final do serviço de nuvem e ACL](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

Se não tiver outra VM na Olá mesma rede virtual, pode facilmente criar uma. Para obter mais informações, consulte [criar uma VM com Linux no Azure utilizando Olá CLI](quick-create-cli.md). Eliminar Olá VM adicional quando tiver terminado com os seus testes.

Olá mesmo virtual se pode criar uma ligação SSH com uma VM na rede, verifique Olá seguintes áreas:

* **configuração de ponto final de Olá para o tráfego SSH no destino Olá VM.** porta TCP privada Olá do ponto final de Olá deve corresponder no qual Olá SSH serviço no Olá VM está a escutar a porta TCP Olá. (a porta predefinida de Olá é 22). Verifique o número de porta de SSH TCP Olá na Olá portal do Azure ao selecionar **máquinas virtuais** > *nome da VM* > **definições**  >  **Pontos finais**.
* **Olá ACL para o ponto final do tráfego SSH Olá no Olá máquina virtual de destino.** Uma ACL permite-lhe toospecify permitido ou negado o tráfego de entrada de Olá Internet, com base no respetivo endereço IP de origem. ACLs mal configuradas podem impedir que a entrada ponto final do toohello de tráfego SSH. Verifique a sua tooensure de ACLs de tráfego de entrada de endereços IP públicos Olá do seu proxy ou de outro servidor edge é permitido. Para obter mais informações, consulte [sobre o acesso de rede (ACLs) de listas de controlo](../../virtual-network/virtual-networks-acl.md).

ponto final de Olá tooeliminate como uma origem do problema Olá, remova o ponto final atual do Olá, criar outro ponto final e especifique Olá SSH (a porta TCP 22 por número de porta pública e privada Olá). Para obter mais informações, consulte [configurar pontos finais numa máquina virtual no Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>Origem 4: Grupos de segurança de rede
Grupos de segurança de rede, permitem-lhe toohave controlo mais granular sobre o tráfego de entrada e saída permitido. Pode criar regras que abrangem sub-redes e serviços em nuvem na uma rede virtual do Azure. Verifique a sua tooensure de regras de grupo de segurança de rede que tooand de tráfego SSH de Olá que Internet é permitida.
Para obter mais informações, consulte [sobre grupos de segurança de rede](../../virtual-network/virtual-networks-nsg.md).

Também pode utilizar a configuração de NSG de Olá toovalidate Certifique-se de IP. Para obter mais informações, consulte [descrição geral da monitorização de rede do Azure](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview). 

## <a name="source-5-linux-based-azure-virtual-machine"></a>Origem 5: Baseado em Linux máquina virtual do Azure
Olá origem último informações sobre problemas possíveis é Olá máquina virtual do Azure em si.

![Diagrama realça baseado em Linux máquina virtual do Azure](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

Se não tiver o feito, siga as instruções de Olá [tooreset uma palavra-passe ou SSH para máquinas virtuais baseadas em Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

Tente ligar novamente a partir do seu computador. Se continuar a falhar, Olá são apresentados alguns dos problemas possíveis Olá:

* Olá serviço SSH não está em execução na máquina de virtual de destino Olá.
* Olá serviço SSH não está a escutar na porta TCP 22. tootest, instalar um cliente telnet no seu computador local e execute "telnet *cloudServiceName*. cloudapp.net 22". Este passo determina se a máquina virtual de Olá permite ponto final de SSH de toohello de comunicação de entrada e saída.
* a Olá firewall local na máquina de virtual de destino Olá tem regras que estão a impedir o tráfego SSH de entrada ou de saída.
* Deteção de intrusões ou software que está em execução no Olá máquina virtual do Azure de monitorização de rede está a impedir ligações SSH.

## <a name="additional-resources"></a>Recursos adicionais
Para obter mais informações sobre resolução de problemas de acesso de aplicação, consulte [aplicação tooan acesso de resolução de problemas em execução numa máquina virtual do Azure](troubleshoot-app-connection.md)
