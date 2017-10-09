---
title: "aaaPlan capacidade e dimensionamento para tooAzure de replicação de VMware com o Azure Site Recovery | Microsoft Docs"
description: Utilizar esta capacidade de tooplan artigo e escala quando replicar VMs de VMware tooAzure com o Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 7ca9147d1b4611f6b4a67c3de3f27fb9878f4c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a>Planear a capacidade e o dimensionamento para replicação de VMware com o Azure Site Recovery

Utilize este toofigure do artigo planear a capacidade e dimensionamento, quando replicar VMs de VMware no local e servidores físicos tooAzure com [do Azure Site Recovery](site-recovery-overview.md).

## <a name="how-do-i-start-capacity-planning"></a>Como começar a planear a capacidade?

Recolha informações sobre o ambiente de replicação executando Olá [Planeador de implementação do Azure Site Recovery](https://aka.ms/asr-deployment-planner-doc) para replicação de VMware. [Saiba mais](site-recovery-deployment-planner.md) sobre esta ferramenta. Irá recolher informações sobre compatíveis e incompatíveis VMs, discos por VM, e dados churn por disco. ferramenta Olá também abrange os requisitos de largura de banda de rede e Olá necessária para ativação pós-falha com êxito de replicação e teste de infraestrutura do Azure.

## <a name="capacity-considerations"></a>Considerações sobre a capacidade

**Componente** | **Detalhes** |
--- | --- | ---
**Replicação** | **A velocidade máxima da alteração diária:** uma máquina protegida só pode utilizar um servidor de processos e um servidor de processos único pode processar uma taxa de alteração diária segurança too2 TB. Se, portanto, 2 TB Olá diária dados alterar velocidade que é suportada para uma máquina protegida.<br/><br/> **Débito máximo:** uma máquina replicada pode pertencer a conta de armazenamento tooone no Azure. Uma conta de armazenamento standard pode processar um máximo de 20 000 pedidos por segundo e recomendamos que mantenha o número de Olá de operações de entrada/saída por segundo (IOPS) entre um too20 da máquina de origem, 000. Por exemplo, se tiver uma máquina de origem com 5 discos e cada disco gera 120 IOPS (tamanho de 8K) na máquina de origem Olá, em seguida, será dentro Olá do Azure por limite IOPS de disco de 500. (o número de Olá de contas de armazenamento necessária é máquina de origem total de toohello igual IOPS, dividida pelo 20.000.)
**Servidor de configuração** | servidor de configuração de Olá deve ser a capacidade de taxa de alteração diárias do toohandle capaz de Olá em todas as cargas de trabalho em execução nas máquinas protegidas e tem de toocontinuously de largura de banda suficiente replicar dados tooAzure armazenamento.<br/><br/> Como melhor prática, localize o servidor de configuração de Olá no Olá mesma rede e o segmento de LAN como Olá máquinas que pretende tooprotect. Este pode estar localizado numa rede diferente, mas as máquinas que pretende tooprotect deve ter tooit de visibilidade de rede 3 camada.<br/><br/> Recomendações de tamanho para o servidor de configuração de Olá estão resumidas na tabela de Olá no Olá secção a seguir.
**Servidor de processos** | servidor de processos primeiro Olá é instalado por predefinição no servidor de configuração de Olá. Pode implementar processos adicionais servidores tooscale seu ambiente. <br/><br/> servidor de processos de Olá recebe dados de replicação de máquinas protegidas e otimiza-as com colocação em cache, compressão e encriptação. Em seguida, envia Olá tooAzure de dados. máquina do servidor de processos de Olá deve ter tooperform de recursos suficientes estas tarefas.<br/><br/> servidor de processos de Olá utiliza uma cache com base em disco. Utilize um disco separado de cache de 600 GB ou mais toohandle alterações aos dados armazenadas no evento Olá de um estrangulamento de rede ou uma interrupção.

## <a name="size-recommendations-for-hello-configuration-server"></a>Recomendações de tamanho para o servidor de configuração de Olá

**CPU** | **Memória** | **Tamanho da cache do disco** | **Taxa de alteração de dados** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPUs (2 sockets * 4 núcleos @ gigahertz 2,5 [GHz]) | 16 GB | 300 GB | 500 GB ou inferior | Replicar máquinas inferior a 100.
12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz) | 18 GB | 600 GB | 500 GB too1 TB | Replicar entre 100 150 máquinas.
16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replicar entre 150 200 máquinas.
Implementar a outro servidor de processos | | | > 2 TB | Implemente servidores de processos adicionais se está a replicar mais de 200 máquinas ou, se alterar dados diários Olá taxa excede 2 TB.

Em que:

* Cada máquina de origem está configurada com 3 discos de 100 GB.
* Utilizámos o direcionamento de caminhos de armazenamento de 8 unidades SAS de 10 mil RPM, com RAID 10, de medidas de disco de cache.

## <a name="size-recommendations-for-hello-process-server"></a>Recomendações de tamanho para o servidor de processos de Olá

Se precisar mais de 200 máquinas tooprotect ou taxa de alteração diária Olá é maior do que 2 TB, pode adicionar o processo servidores toohandle Olá replicação carga. tooscale terminar, pode:

* Aumente o número de Olá de servidores de configuração. Por exemplo, pode proteger a segurança de máquinas de too400 com dois servidores de configuração.
* Adicionar mais servidores de processos e utilizar o servidor de configuração destes toohandle tráfego em vez de (ou além de) Olá.

Olá, a tabela seguinte descreve um cenário em que:

* Não está a planear o servidor de configuração de Olá toouse como um servidor de processos.
* Configurou um servidor de processos adicionais.
* Configurou o servidor de processos adicionais de Olá de toouse de máquinas virtuais protegidas.
* Cada máquina de origem protegida está configurada com três discos de 100 GB.

**Servidor de configuração** | **Servidor de processos adicionais** | **Tamanho da cache do disco** | **Taxa de alteração de dados** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPUs (2 sockets * 4 núcleos @ GHz 2,5), 16 GB de memória | 4 vCPUs (2 sockets * 2 núcleos @ GHz 2,5), 8 GB de memória | 300 GB | 250 GB ou inferior | Replicar máquinas 85 ou menos.
8 vCPUs (2 sockets * 4 núcleos @ GHz 2,5), 16 GB de memória | 8 vCPUs (2 sockets * 4 núcleos @ GHz 2,5), 12 GB de memória | 600 GB | 250 GB too1 TB | Replicar entre 85 150 máquinas.
12 vCPUs (2 sockets * 6 núcleos @ GHz 2,5), 18 GB de memória | 12 vCPUs (2 sockets * 6 núcleos @ GHz 2,5) 24 GB de memória | 1 TB | 1 TB too2 TB | Replicar entre 150 225 máquinas.

dimensionar os servidores de forma de Olá depende da sua preferência para um modelo de vertical ou Escalamento horizontal.  Aumentar verticalmente ao implementar alguns configuração de gama alta de classe e servidores de processos, ou aumentar horizontalmente ao implementar mais servidores com menos recursos. Por exemplo, se tiver 220 máquinas tooprotect, pode efetuar uma das seguintes Olá:

* Configure o servidor de configuração de Olá com 12 vCPU, 18 GB de memória e um servidor de processos adicionais com 12 vCPU, 24 GB de memória. Configure máquinas protegidas toouse Olá processo suplementar apenas o servidor.
* Configure dois servidores de configuração (2, 8 vCPU, 16 GB de RAM) e dois servidores de processos adicionais (1 x 8 vCPU e 4 vCPU x 1 toohandle 135 + 85 [220] máquinas). Configure máquinas protegidas toouse Olá mais servidores de processos apenas.


## <a name="control-network-bandwidth"></a>Largura de banda de rede de controlo

Depois de utilizou Olá [ferramenta de implementação Planner Olá](site-recovery-deployment-planner.md) largura de banda do toocalculate Olá que precisa para a replicação (replicação inicial Olá e, em seguida, delta), pode controlar a quantidade de Olá de largura de banda utilizada na replicação através de alguns das opções:

* **Limitar largura de banda**: tráfego do VMware que replica tooAzure passa através de um servidor de processo específico. Pode limitar a largura de banda em máquinas de Olá em execução como servidores de processos.
* **Influenciar a largura de banda**: pode influenciar a largura de banda Olá utilizada na replicação através da utilização de um par de chaves de registo de:
  * Olá **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** valor de registo Especifica o número de Olá de threads que são utilizados para a transferência de dados (replicação inicial ou delta) de um disco. Um valor mais alto aumenta a largura de banda de Olá utilizada para replicação.
  * Olá **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** Especifica Olá número de threads utilizados para a transferência de dados durante a reativação pós-falha.

### <a name="throttle-bandwidth"></a>Limitar largura de banda

1. Abra Olá snap-in MMC de cópia de segurança do Azure no agir de máquina Olá como servidor de processos de Olá. Por predefinição, um atalho para cópia de segurança está disponível no ambiente de trabalho hello, ou em Olá seguinte pasta: c:\Programas\Microsoft c:\Programas\Microsoft Azure Recovery Services agent\bin\wabadmin..
2. No snap-in Olá, clique em **alterar propriedades**.

    ![Propriedades de toochange do snap-in da opção de captura de ecrã da MMC de cópia de segurança do Azure](./media/site-recovery-vmware-to-azure/throttle1.png)
3. No Olá **limitação** separador, selecione **ativar a limitação para operações de cópia de segurança de utilização de largura de banda de internet**. Definir limites de Olá para o trabalho e de descanso horas. Intervalos válidos são de Kbps 512 too102 Mbps, por segundo.

    ![Caixa de diálogo de captura de ecrã de propriedades de cópia de segurança do Azure](./media/site-recovery-vmware-to-azure/throttle2.png)

Também pode utilizar Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que não é necessária nenhuma limitação.

### <a name="influence-network-bandwidth-for-a-vm"></a>Influenciar a largura de banda de rede para uma VM

1. No registo da VM Olá, navegue até demasiado**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de Olá tooinfluence num disco replicação, modifique o valor de Olá do **UploadThreadsPerVM**, ou crie a chave de Olá, se não existir.
   * largura de banda do tooinfluence Olá para tráfego de reativação pós-falha a partir do Azure, modifique o valor de Olá do **DownloadThreadsPerVM**.
2. valor predefinido de Olá é 4. Numa rede "sobreaprovisionada", estas chaves do registo devem ser Olá valores predefinidos alteradas. Olá máximo é 32. Monitorizar o valor de Olá toooptimize de tráfego.


## <a name="deploy-additional-process-servers"></a>Implementar servidores de processos adicionais

Se tiver tooscale fora da sua implementação, para além de 200 máquinas de origem ou tem um total diariamente churn taxa de mais do que 2 TB, é necessário o volume de tráfego do processo suplementar servidores toohandle Olá. Siga tooset estas instruções se o servidor de processos de Olá. Depois de configurar o servidor de Olá, migrar toouse de máquinas de origem-lo.

1. No **servidores do Site Recovery**, clique o servidor de configuração de Olá e, em seguida, clique em **servidor de processos**.

    ![Captura de ecrã de recuperação de sites servidores opção tooadd um servidor de processos](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. No **tipo de servidor**, clique em **(no local) do servidor de processos**.

    ![Caixa de diálogo de captura de ecrã do servidor de processos](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. Transferir o ficheiro de configuração do Site Recovery Unified Olá e execute-o servidor de processos de Olá tooinstall. Isto também regista-no Cofre de Olá.
4. No **antes de começar**, selecione **adicionar tooscale de servidores de processos adicionais saída implementação**.
5. Assistente de Olá completa no Olá mesma forma que fez quando [configurar](#step-2-set-up-the-source-environment) servidor de configuração de Olá.

    ![Assistente de captura de ecrã de configuração Azure Site Recovery unificada](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. No **detalhes do servidor de configuração**, especifique o endereço IP de hello do servidor de configuração de Olá e Olá o frase de acesso. tooobtain Olá frase de acesso, execute **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** no servidor de configuração de Olá.

    ![Página de detalhes do servidor captura de ecrã de configuração](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Migrar máquinas toouse Olá novo servidor de processos
1. No **definições** > **servidores do Site Recovery**, clique o servidor de configuração de Olá e, em seguida, expanda **processar servidores**.

    ![Caixa de diálogo de captura de ecrã do servidor de processos](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. Clique no servidor de processos de Olá atualmente em utilização e clique em **comutador**.

    ![Caixa de diálogo de servidor de captura de ecrã de configuração](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. No **servidor de processos de destino selecione**, selecione Olá novo servidor de processos que pretende toouse e, em seguida, selecione as máquinas virtuais de Olá nesse servidor Olá irá processar. Clique em informações tooget de ícone de informações do Olá sobre hello do servidor. toohelp que tomar decisões de carga, Olá espaço médio que necessários tooreplicate cada máquina virtual selecionada toohello novo servidor de processos é apresentado. Clique em Olá marca de verificação toostart replicar toohello novo servidor de processos.


## <a name="next-steps"></a>Passos seguintes

Transferir e executar Olá [Planeador de implementação do Azure Site Recovery](https://aka.ms/asr-deployment-planner)
