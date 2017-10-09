---
title: "tooAzure de VMware/físico de falhas de proteção aaaTroubleshoot | Microsoft Docs"
description: "Este artigo descreve falhas de replicação de máquina Olá comuns VMware e como tootroubleshoot-las"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Resolver problemas de replicação do servidor de VMware/físico no local
Poderá receber uma mensagem de erro específico ao proteger as máquinas virtuais VMware ou servidores físicos, utilizando o Azure Site Recovery. Detalhes deste artigo Olá algumas das mensagens de erro mais comuns encontradas, juntamente com tooresolve passos de resolução de problemas-los.


## <a name="initial-replication-is-stuck-at-0"></a>A replicação inicial está encravada % 0
A maioria das falhas de replicação inicial de Olá que estamos a encontrar no suporte são devido a problemas de tooconnectivity entre o servidor de processo do servidor de origem ou processo servidor para o Azure.
Para a maioria dos casos, pode Self-resolver estes problemas, seguindo os passos de Olá listados abaixo.

###<a name="check-hello-following-on-source-machine"></a>Verifique o seguinte Olá na máquina de origem
* A partir de linha de comandos de máquina do servidor de origem, utilize Telnet tooping Olá servidor de processos com a porta https (predefinição 9443) conforme mostrado abaixo toosee se existem quaisquer problemas de conectividade de rede ou a porta de firewall a bloquear problemas.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Utilizar o Telnet, não utilize a conectividade de tootest PING.  Se o Telnet não estiver instalado, siga a lista de passos Olá [aqui](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Se não é possível tooconnect, permitir que a porta de entrada 9443 no servidor de processos de Olá e verifique se o hello problema ainda sai. Foi alguns casos em que o servidor de processos foi atrás de rede de Perímetro, o qual foi fazendo com que este problema.

* Verificar estado Olá de serviço `InMage Scout VX Agent – Sentinel/OutpostStart` se não estiver em execução e verifique se o problema de Olá ainda existe.   
 
###<a name="check-hello-following-on-process-server"></a>Verifique Olá seguinte no servidor de processos

* **Verifique se o servidor de processos é enviar ativamente tooAzure de dados** 

A partir da máquina do servidor de processos, abra Olá Gestor de tarefas (prima Ctrl-Shift-Esc). Aceda toohello separador de desempenho e clique em ligação de 'Abra Monitor de recursos'. No Gestor de recursos, visite tooNetwork separador. Verifique se cbengine.exe em 'Processos com a atividade de rede' está a enviar ativamente grande volume (em MB) de dados.

![Ativar a replicação](./media/site-recovery-protection-common-errors/cbengine.png)

Se não siga os passos de Olá listados abaixo:

* **Verifique se o servidor de processos é capaz de tooconnect Blob do Azure**: selecione e verifique cbengine.exe tooview Olá 'Ligações TCP' toosee se existir conectividade do servidor de processo tooAzure URL de blob de armazenamento.

![Ativar a replicação](./media/site-recovery-protection-common-errors/rmonitor.png)

Se não for, em seguida, aceda tooControl painel > serviços, verifique se Olá os seguintes serviços está em execução:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Inicie a qualquer serviço que não está em execução e verifique se o problema de Olá ainda existe.

* **Verifique se o servidor de processos está endereço de IP público tooconnect capaz de tooAzure através da porta 443**

Abra Olá CBEngineCurr.errlog mais recente do `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` e procure: 443 e ligação tentativa falhada.

![Ativar a replicação](./media/site-recovery-protection-common-errors/logdetails1.png)

Se existirem problemas, em seguida, a partir de linha de comandos do servidor de processos, utilize telnet tooping seu endereço de IP público do Azure (mascarado nos acima imagem) foi encontrado no Olá CBEngineCurr.currLog através da porta 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Se forem tooconnect não é possível, em seguida, verifique se o problema de acesso de Olá for devido toofirewall ou Proxy, tal como descrito no passo seguinte.


* **Verifique se firewall de baseadas no endereço IP no servidor de processos não estão a bloquear o acesso**: Se estiver a utilizar um regras de firewall baseadas no endereço IP no servidor de Olá, em seguida, transferir a lista completa de Olá do Microsoft Azure Datacenter intervalos de IP do [aqui ](https://www.microsoft.com/download/details.aspx?id=41653) e adicioná-los tooensure de configuração de firewall de tooyour permitem comunicação tooAzure (e Olá porta HTTPS (443)).  Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).

* **Verifique se firewall baseada no URL no servidor de processos não está a bloquear o acesso**: Se estiver a utilizar as regras de firewall um URL com base no servidor de Olá, certifique-se de Olá os seguintes URLs é adicionado toofirewall configuração. 
     
  `*.accesscontrol.windows.net:` Utilizado para controlo de acesso e gestão de identidades

  `*.backup.windowsazure.com:` Utilizado para transferência de dados de replicação e orquestração

  `*.blob.core.windows.net:`Utilizado para acesso toohello conta de armazenamento que armazena os dados replicados

  `*.hypervrecoverymanager.windowsazure.com:` Utilizado para operações e gestão de replicação e orquestração

  `time.nist.gov`e `time.windows.com`: utilizar a sincronização de hora toocheck entre sistema e a hora global.

URLs para **Cloud do Azure Government**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Verifique se as definições de Proxy no servidor de processos não estão a bloquear o acesso**.  Se estiver a utilizar um servidor Proxy, certifique-se de que está a resolver nome do servidor proxy Olá pelo servidor DNS Olá.
toocheck tiver sido fornecido no momento de Olá do programa de configuração do servidor de configuração. Aceda a chave de tooregistry

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Certifique-se que Olá as mesmas definições estão a ser utilizadas os dados de toosend de agente do Azure Site Recovery.
Cópia de segurança do Microsoft Azure Search 

![Ativar a replicação](./media/site-recovery-protection-common-errors/mab.png)

Abra-o e clique na ação > alterar propriedades. No separador de configuração de Proxy, deverá ver o endereço de proxy de Olá, que deve ser a mesmo, conforme ilustrado pelas definições de registo Olá. Se não estiver, altere-toohello mesmo endereço.

![Ativar a replicação](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Verifique se a largura de banda de limitação não é restrita no servidor de processos**: aumentar Olá largura de banda e verifique se o problema de Olá ainda existe.

##<a name="next-steps"></a>Passos seguintes
Se precisar de mais ajuda, em seguida, após a sua consulta demasiado[fórum de ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). Temos uma Comunidade de Active Directory e um dos nossos engenheiros será capaz de tooassist.
