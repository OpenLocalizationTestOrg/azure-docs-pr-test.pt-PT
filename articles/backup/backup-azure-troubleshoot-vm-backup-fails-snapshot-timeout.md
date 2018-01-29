---
title: "Resolver problemas de falhas de cópia de segurança do Azure: Estado do agente convidado indisponível | Microsoft Docs"
description: "Sintomas, causas e soluções de falhas de cópia de segurança do Azure relacionados com o agente, a extensão, discos"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
keywords: "Cópia de segurança do Azure; Agente da VM; Conectividade de rede"
ms.assetid: 4b02ffa4-c48e-45f6-8363-73d536be4639
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 01/09/2018
ms.author: genli;markgal;sogup;
ms.openlocfilehash: 0be2391268e11593802cb0f455e8c4553f0d4731
ms.sourcegitcommit: 1fbaa2ccda2fb826c74755d42a31835d9d30e05f
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/22/2018
---
# <a name="troubleshoot-azure-backup-failure-issues-with-agent-andor-extension"></a>Resolver problemas de falhas de cópia de segurança do Azure: problemas com agentes e/ou extensão

Este artigo fornece os passos de resolução de problemas para o ajudar a resolver falhas de cópia de segurança relacionado com problemas de comunicação com o agente da VM e a extensão.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="vm-agent-unable-to-communicate-with-azure-backup"></a>Agente de VM não é possível comunicar com o Backup do Azure

> [!NOTE]
> Se as cópias de segurança de VM do Linux do Azure começado a falhar com este erro nesta ou após 4º de Janeiro de 2018, execute o seguinte comando nas VMs afetadas e repita as cópias de segurança

    sudo rm -f /var/lib/waagent/*.[0-9]*.xml

Depois de registar e agendar uma VM para o serviço de cópia de segurança do Azure, a cópia de segurança inicia a tarefa ao comunicar com o agente VM para criar um instantâneo de ponto no tempo. Qualquer uma das seguintes condições poderá impedir o instantâneo de que está a ser acionado, o que por sua vez, pode levar a falhas de cópia de segurança. Siga abaixo passos pela ordem indicada de resolução de problemas e repita a operação.

##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [a VM possui sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [o agente está instalado na VM, mas não responde (para VMs do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [o agente instalado na VM está desatualizado (para VMs com Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [não é possível obter o estado de instantâneo ou não pode ser obtido um instantâneo](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [a extensão de cópia de segurança não consegue atualizar ou carregar](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-6-azure-classic-vms-may-require-additional-step-to-complete-registrationazure-classic-vms-may-require-additional-step-to-complete-registration"></a>Causa 6: [VMs clássicas do Azure pode necessitar de um passo adicional para concluir o registo](#azure-classic-vms-may-require-additional-step-to-complete-registration)

## <a name="snapshot-operation-failed-due-to-no-network-connectivity-on-the-virtual-machine"></a>Operação de instantâneos falhou devido a sem conectividade de rede na máquina virtual
Depois de registar e agendar uma VM para o serviço de cópia de segurança do Azure, a cópia de segurança inicia a tarefa ao comunicar com a extensão de cópia de segurança de VM para criar um instantâneo de ponto no tempo. Qualquer uma das seguintes condições poderá impedir o instantâneo de que está a ser acionado, o que por sua vez, pode levar a falhas de cópia de segurança. Siga abaixo passos pela ordem indicada de resolução de problemas e repita a operação.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [a VM possui sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 2: [não é possível obter o estado de instantâneo ou não pode ser obtido um instantâneo](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-3-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 3: [a extensão de cópia de segurança não consegue atualizar ou carregar](#the-backup-extension-fails-to-update-or-load)

## <a name="vmsnapshot-extension-operation-failed"></a>Falha na operação de extensão VMSnapshot

Depois de registar e agendar uma VM para o serviço de cópia de segurança do Azure, a cópia de segurança inicia a tarefa ao comunicar com a extensão de cópia de segurança de VM para criar um instantâneo de ponto no tempo. Qualquer uma das seguintes condições poderá impedir o instantâneo de que está a ser acionado, o que por sua vez, pode levar a falhas de cópia de segurança. Siga abaixo passos pela ordem indicada de resolução de problemas e repita a operação.
##### <a name="cause-1-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 1: [não é possível obter o estado de instantâneo ou não pode ser obtido um instantâneo](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-2-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 2: [a extensão de cópia de segurança não consegue atualizar ou carregar](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-3-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [a VM possui sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-4-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 4: [o agente está instalado na VM, mas não responde (para VMs do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-5-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 5: [o agente instalado na VM está desatualizado (para VMs com Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)

## <a name="unable-to-perform-the-operation-as-the-vm-agent-is-not-responsive"></a>Não é possível efetuar a operação dado que o agente da VM não está a responder

Depois de registar e agendar uma VM para o serviço de cópia de segurança do Azure, a cópia de segurança inicia a tarefa ao comunicar com a extensão de cópia de segurança de VM para criar um instantâneo de ponto no tempo. Qualquer uma das seguintes condições poderá impedir o instantâneo de que está a ser acionado, o que por sua vez, pode levar a falhas de cópia de segurança. Siga abaixo passos pela ordem indicada de resolução de problemas e repita a operação.
##### <a name="cause-1-the-agent-is-installed-in-the-vm-but-is-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 1: [o agente está instalado na VM, mas não responde (para VMs do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-2-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 2: [o agente instalado na VM está desatualizado (para VMs com Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-3-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 3: [a VM possui sem acesso à Internet](#the-vm-has-no-internet-access)

## <a name="backup-failed-with-an-internal-error---please-retry-the-operation-in-a-few-minutes"></a>Falha de cópia de segurança com um erro interno -. Repita a operação dentro de alguns minutos

Depois de registar e agendar uma VM para o serviço de cópia de segurança do Azure, a cópia de segurança inicia a tarefa ao comunicar com a extensão de cópia de segurança de VM para criar um instantâneo de ponto no tempo. Qualquer uma das seguintes condições poderá impedir o instantâneo de que está a ser acionado, o que por sua vez, pode levar a falhas de cópia de segurança. Siga abaixo passos pela ordem indicada de resolução de problemas e repita a operação.
##### <a name="cause-1-the-vm-has-no-internet-accessthe-vm-has-no-internet-access"></a>Causa 1: [a VM possui sem acesso à Internet](#the-vm-has-no-internet-access)
##### <a name="cause-2-the-agent-installed-in-the-vm-but-unresponsive-for-windows-vmsthe-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>Causa 2: [o agente instalado na VM, mas não responde (para VMs do Windows)](#the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms)
##### <a name="cause-3-the-agent-installed-in-the-vm-is-out-of-date-for-linux-vmsthe-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>Causa 3: [o agente instalado na VM está desatualizado (para VMs com Linux)](#the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms)
##### <a name="cause-4-the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-takenthe-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Causa 4: [não é possível obter o estado de instantâneo ou não pode ser obtido um instantâneo](#the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken)
##### <a name="cause-5-the-backup-extension-fails-to-update-or-loadthe-backup-extension-fails-to-update-or-load"></a>Causa 5: [a extensão de cópia de segurança não consegue atualizar ou carregar](#the-backup-extension-fails-to-update-or-load)
##### <a name="cause-6-backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lockbackup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock"></a>Causa 6: [serviço de cópia de segurança não tem permissão para eliminar os pontos de restauro antigos devido a bloqueio de grupo de recursos](#backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock)

## <a name="the-specified-disk-configuration-is-not-supported"></a>A configuração de disco especificada não é suportada

> [!NOTE]
> Temos uma versão de pré-visualização privada para suportar cópias de segurança para VMs com > discos de 1TB. Para obter detalhes, consulte [pré-visualização privada para o suporte de cópia de segurança de VM de disco grande](https://gallery.technet.microsoft.com/Instant-recovery-point-and-25fe398a)
>
>

Cópia de segurança do Azure não suporta atualmente os tamanhos de disco [superior a 1023GB](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms-prepare#limitations-when-backing-up-and-restoring-a-vm). 
- Se tiver discos superiores a 1 TB, [ligue novos discos](https://docs.microsoft.com/azure/virtual-machines/windows/attach-managed-disk-portal) que sejam inferiores a 1 TB <br>
- Em seguida, copie os dados do disco superior a 1 TB para o disco ou discos que acabou de criar com um tamanho inferior a 1 TB. <br>
- Certifique-se de que copiou todos os dados e remova os discos superiores a 1 TB
- Iniciar a cópia de segurança

## <a name="causes-and-solutions"></a>Causas e soluções

### <a name="the-vm-has-no-internet-access"></a>A VM possui sem acesso à Internet
Pelo requisito de implementação, a VM possui sem acesso à Internet, ou tem restrições no local que impedem o acesso à infraestrutura do Azure.

Para funcionar corretamente, a extensão de cópia de segurança necessita de conectividade para os endereços IP públicos do Azure. A extensão envia comandos para um ponto final de armazenamento do Azure (URL de HTTP) para gerir os instantâneos da VM. Se a extensão não tem acesso à Internet pública, cópia de segurança eventualmente falha.

####  <a name="solution"></a>Solução
Para resolver o problema, experimente um dos métodos listados aqui.
##### <a name="allow-access-to-the-azure-storage-corresponding-to-the-region"></a>Permitir o acesso ao armazenamento do Azure correspondente à região

Pode permitir que as ligações para o armazenamento da região específica utilizando [etiquetas de serviço](../virtual-network/security-overview.md#service-tags). Certifique-se de que a regra que permite o acesso à conta de armazenamento tem prioridade mais alta do que a regra que bloqueia o acesso à internet. 

![NSG com etiquetas de armazenamento para uma região](./media/backup-azure-arm-vms-prepare/storage-tags-with-nsg.png)

> [!WARNING]
> As etiquetas de serviço de armazenamento estão disponíveis apenas em regiões específicas e estão em pré-visualização. Para obter uma lista de regiões, consulte [etiquetas de serviço para o armazenamento](../virtual-network/security-overview.md#service-tags).

##### <a name="create-a-path-for-http-traffic-to-flow"></a>Criar um caminho para o tráfego HTTP para o fluxo

1. Se tiver de restrições de rede no local (por exemplo, um grupo de segurança de rede), implemente um servidor de proxy HTTP para encaminhar o tráfego.
2. Para permitir o acesso à Internet do servidor de proxy de HTTP, adicione regras para o grupo de segurança de rede, se tiver uma.

Para saber como configurar um proxy HTTP para cópias de segurança VM, consulte [preparar o ambiente para fazer cópias de segurança de máquinas virtuais do Azure](backup-azure-arm-vms-prepare.md#establish-network-connectivity).

No caso de estiver a utilizar discos geridos, poderá ter uma porta adicional (8443) abrir nas firewalls.

### <a name="the-agent-installed-in-the-vm-but-unresponsive-for-windows-vms"></a>O agente instalado na VM, mas não responde (para VMs do Windows)

#### <a name="solution"></a>Solução
O agente de VM poderá ter sido danificado ou o serviço poderá foram parado. Reinstalar o agente da VM iria ajudar a obter a versão mais recente e reinicie a comunicação.

1. Verifique se o serviço de agente de convidados do Windows em execução nos serviços (services.msc) da Máquina Virtual. Tente reiniciar o serviço de agente de convidados do Windows e iniciar a cópia de segurança<br>
2. Se não estiver visível na serviços, certifique-se em programas e funcionalidades se o serviço do agente convidado do Windows está instalado.
4. Se conseguir ver em programas e funcionalidades de desinstalar o agente de convidados do Windows.
5. Transfira e instale o [versão mais recente do MSI do agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Precisa de privilégios de Administrador para concluir a instalação.
6. Em seguida, deve ser capaz de ver os serviços do agente de convidados do Windows nos serviços
7. Tente executar uma cópia de segurança no-a pedido/adhoc clicando em "cópia de segurança agora' de no portal.

Verifique também se a Máquina Virtual possui  **[.NET 4.5 instalados no sistema](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed)**. É necessário para o agente da VM comunicar com o serviço

### <a name="the-agent-installed-in-the-vm-is-out-of-date-for-linux-vms"></a>O agente instalado na VM está desatualizado (para VMs com Linux)

#### <a name="solution"></a>Solução
Mais relacionados com o agente relacionadas com a extensão de falhas de ou para VMs com Linux são causadas por problemas que afetam um agente VM desatualizado. Para resolver este problema, siga estas Diretrizes gerais:

1. Siga as instruções para [atualizar o agente da VM com Linux](../virtual-machines/linux/update-agent.md).

 >[!NOTE]
 >Iremos *vivamente recomendável* que Atualize o agente apenas através de um repositório de distribuição. Não é recomendada a transferir o código de agente diretamente a partir do GitHub e atualizá-la. Se o agente mais recente está disponível para a distribuição, contacte o suporte de distribuição para obter instruções sobre como o instalar. Para verificar se o agente mais recente, vá para o [agente Linux do Windows Azure](https://github.com/Azure/WALinuxAgent/releases) página no repositório GitHub.

2. Certifique-se de que o agente do Azure está em execução a VM, executando o seguinte comando:`ps -e`

 Se o processo de mensagens em fila não está em execução, reinicie-o utilizando os seguintes comandos:

 * Para Ubuntu:`service walinuxagent start`
 * Para outras distribuições:`service waagent start`

3. [Configurar o agente de reinício automático](https://github.com/Azure/WALinuxAgent/wiki/Known-Issues#mitigate_agent_crash).
4. Execute uma nova cópia de segurança de teste. Se a falha persistir, recolha os seguintes registos de VM do cliente:

   * /var/lib/waagent/*.xml
   * /var/log/waagent.log
   * /var/log/azure/*

Se é necessário o registo verboso para waagent, siga estes passos:

1. No ficheiro /etc/waagent.conf, localize a seguinte linha: **ativar registo verboso (y | n)**
2. Alterar o **Logs.Verbose** valor a partir da  *n*  para *y*.
3. Guardar a alteração e, em seguida, reinicie waagent seguindo os passos nesta secção anteriores.

### <a name="the-snapshot-status-cannot-be-retrieved-or-a-snapshot-cannot-be-taken"></a>Não é possível obter o estado de instantâneo ou não pode ser obtido um instantâneo
A cópia de segurança VM depende de emitir um comando de instantâneo para a conta de armazenamento subjacente. Pode efetuar a cópia de segurança porque este não tem acesso à conta de armazenamento ou porque a execução da tarefa de instantâneo é atrasada.

#### <a name="solution"></a>Solução
As seguintes condições podem causar a falha de tarefa de instantâneo:

| Causa | Solução |
| --- | --- |
| A VM possui uma cópia de segurança do SQL Server configurada. | Por predefinição, a cópia de segurança VM é executado um VSS cópia de segurança completa em VMs do Windows. Em VMs que estejam a executar servidores baseados no SQL Server e no qual o SQL Server está configurada a cópia de segurança, podem ocorrer atrasos de execução do instantâneo.<br><br>Se estão a experienciar uma falha de cópia de segurança devido a um problema de instantâneo, defina a seguinte chave de registo:<br><br>**[HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\BCDRAGENT] "USEVSSCOPYBACKUP"="TRUE"** |
| O estado VM é comunicado incorretamente porque a VM seja encerrada RDP. | Se desligar a VM no protocolo de ambiente de trabalho remoto (RDP), consulte o portal para determinar se o estado da VM está correto. Se não estiver correto, encerre a VM no portal utilizando o **encerramento** opção no dashboard VM. |
| A VM não é possível obter o endereço do anfitrião/recursos de infraestrutura do DHCP. | DHCP deve ser ativado no computador convidado para a cópia de segurança de VM do IaaS funcione.  Se a VM não é possível obter o endereço do anfitrião/recursos de infraestrutura da resposta DHCP 245, não é possível transferir ou executar quaisquer extensões. Se precisar de um IP privado estático, deve configurá-lo através da plataforma. A opção de DHCP dentro da VM deve ser ativada à esquerda. Para obter mais informações, consulte [definir um IP estático de privada interna](../virtual-network/virtual-networks-reserved-private-ip.md). |

### <a name="the-backup-extension-fails-to-update-or-load"></a>A extensão de cópia de segurança não consegue atualizar ou carregar
Se não não possível carregar as extensões, a cópia de segurança falha porque não pode ser obtido um instantâneo.

#### <a name="solution"></a>Solução

**Para os convidados do Windows:** Certifique-se de que o serviço de iaasvmprovider está ativado e tem um tipo de arranque de *automática*. Se o serviço não está configurado desta forma, ativá-la determinar se a próxima cópia de segurança é concluída com êxito.

**Para convidados de Linux:** verificar a versão mais recente do VMSnapshot para Linux (a extensão utilizada pela cópia de segurança) é 1.0.91.0.<br>


Se a extensão de cópia de segurança ainda não conseguir atualizar ou carregar, pode forçar a extensão de VMSnapshot recarregar por desinstalar a extensão. A tentativa de cópia de segurança seguinte irá recarregar a extensão.

Para desinstalar a extensão, efetue o seguinte:

1. Aceda ao [Portal do Azure](https://portal.azure.com/).
2. Localize a VM tem problemas de cópia de segurança.
3. Clique em **definições**.
4. Clique em **extensões**.
5. Clique em **Vmsnapshot extensão**.
6. Clique em **desinstalar**.

Este procedimento faz com que a extensão de ser reinstalado durante a próxima cópia de segurança.

### <a name="backup-service-does-not-have-permission-to-delete-the-old-restore-points-due-to-resource-group-lock"></a>Serviço de cópia de segurança não tem permissão para eliminar os pontos de restauro antigos devido a bloqueio de grupo de recursos
Este problema é específico para VMs gerido onde o utilizador bloqueia o grupo de recursos e o serviço de cópia de segurança não é possível eliminar os pontos de restauro mais antigos. Devido a esta novas cópias de segurança começam a falhar, há um limite de pontos de restauro 18 máxima imposta de back-end.

#### <a name="solution"></a>Solução

Para resolver o problema, utilize os seguintes passos para remover a recolha de ponto de restauro: <br>
 
1. Remova o grupo de recursos de bloqueio no qual a VM reside 
     
2. Instalar ARMClient utilizando Chocolatey <br>
   https://github.com/projectkudu/ARMClient
     
3. Início de sessão para ARMClient <br>
             `.\armclient.exe login`
         
4. Coleção de ponto de restauro Get correspondente para a VM <br>
    `.\armclient.exe get https://management.azure.com/subscriptions/<SubscriptionId>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Compute/restorepointcollections/AzureBackup_<VM-Name>?api-version=2017-03-30`

    Exemplo:`.\armclient.exe get https://management.azure.com/subscriptions/f2edfd5d-5496-4683-b94f-b3588c579006/resourceGroups/winvaultrg/providers/Microsoft.Compute/restorepointcollections/AzureBackup_winmanagedvm?api-version=2017-03-30`
             
5. Elimine a coleção de ponto de restauro <br>
            `.\armclient.exe delete https://management.azure.com/subscriptions/<SubscriptionId>/resourceGroups/<ResourceGroupName>/providers/Microsoft.Compute/restorepointcollections/AzureBackup_<VM-Name>?api-version=2017-03-30` 
 
6. Cópia de segurança agendada seguinte irá criar automaticamente novos pontos de restauro e recolha de ponto de restauro 
 
7. O problema voltar será apresentada se bloquear o grupo de recursos novamente como é apenas um limite de 18 pontos de restauro após o qual as cópias de segurança começam a falhar 

