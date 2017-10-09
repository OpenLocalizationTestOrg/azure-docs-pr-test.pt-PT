---
title: "aaaPlan capacidade e dimensionamento para tooAzure de replicação do servidor físico com o Azure Site Recovery | Microsoft Docs"
description: "Utilizar esta capacidade de tooplan artigo e escala quando replicar tooAzure de servidores físicos Windows/Linux com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 209980963c07d13e15802a5da44769ac559217d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-tooazure-replication"></a>Passo 3: Planear a capacidade e Dimensionar para replicação do servidor físico tooAzure

Utilize este toofigure artigo saída capacidade e dimensionamento, quando está a replicar no local tooAzure de servidores físicos Windows/Linux com [do Azure Site Recovery](site-recovery-overview.md).

Publique comentários e perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="plan-deployment-capacity"></a>Planear a capacidade de implementação

1. Leia este [artigo](site-recovery-plan-capacity-vmware.md) toolearn sobre estimar os requisitos de replicação e orientações para dimensionamento componentes da recuperação de Site.
2. Ler considerações Olá abaixo toolearn sobre servidores de componente de dimensionamento e controlar a largura de banda máquina replicada.

## <a name="replication-considerations"></a>Considerações sobre replicação

Utilize estas toofigure considerações sobre os requisitos do servidor replicadas.

**Componente** | **Detalhes** 
--- | --- 
**Replicação** | **A velocidade máxima da alteração diária:** uma máquina protegida só pode utilizar um servidor de processos e um servidor de processos único pode processar uma taxa de alteração diária segurança too2 TB. Se, portanto, 2 TB Olá diária dados alterar velocidade que é suportada para uma máquina protegida.<br/><br/> **Débito máximo:** uma máquina replicada pode pertencer a conta de armazenamento tooone no Azure. Uma conta de armazenamento standard pode processar um máximo de 20 000 pedidos por segundo e recomendamos que mantenha o número de Olá de operações de entrada/saída por segundo (IOPS) entre um too20 da máquina de origem, 000. Por exemplo, se tiver uma máquina de origem com 5 discos e cada disco gera 120 IOPS (tamanho de 8K) na máquina de origem Olá, em seguida, será dentro Olá do Azure por limite IOPS de disco de 500. (o número de Olá de contas de armazenamento necessária é máquina de origem total de toohello igual IOPS, dividida pelo 20.000.)

## <a name="configuration-server-capacity"></a>Capacidade do servidor de configuração

servidor de configuração de Olá deve ser a capacidade de taxa de alteração diárias do toohandle capaz de Olá em todas as cargas de trabalho em execução nas máquinas protegidas e tem de toocontinuously de largura de banda suficiente replicar dados tooAzure armazenamento.

Como melhor prática, localize o servidor de configuração de Olá no Olá mesma rede e o segmento de LAN como Olá máquinas que pretende tooprotect. Este pode estar localizado numa rede diferente, mas as máquinas que pretende tooprotect deve ter tooit de visibilidade de rede 3 camada.

## <a name="sizing-recommendations"></a>Recomendações de dimensionamento

tabela de Olá resume recomendações de dimensionamento, com base na CPU.

**CPU** | **Memória** | **Tamanho da cache do disco** | **Taxa de alteração de dados** | **Máquinas protegidas**
--- | --- | --- | --- | ---
8 vCPUs (2 sockets * 4 núcleos @ gigahertz 2,5 [GHz]) | 16 GB | 300 GB | 500 GB ou inferior | Replicar máquinas inferior a 100.
12 vCPUs (2 sockets * 6 núcleos @ 2,5 GHz) | 18 GB | 600 GB | 500 GB too1 TB | Replicar entre 100 150 máquinas.
16 vCPUs (2 sockets * 8 núcleos @ 2,5 GHz) | 32 GB | 1 TB | 1 TB too2 TB | Replicar entre 150 200 máquinas.
Implementar a outro servidor de processos | | | > 2 TB | Implemente servidores de processos adicionais se está a replicar mais de 200 máquinas ou, se alterar dados diários Olá taxa excede 2 TB.

Em que:

* Cada máquina de origem está configurada com 3 discos de 100 GB.
* Utilizámos o direcionamento de caminhos de armazenamento de 8 unidades SAS de 10 mil RPM, com RAID 10, de medidas de disco de cache.

## <a name="process-server-capacity"></a>Capacidade do servidor de processos


servidor de processos de Olá recebe dados de replicação de máquinas protegidas e otimiza-as com colocação em cache, compressão e encriptação. Em seguida, envia Olá tooAzure de dados.

- máquina do servidor de processos de Olá deve ter tooperform de recursos suficientes estas tarefas.
- servidor de processos primeiro Olá é instalado por predefinição no servidor de configuração de Olá. Pode implementar processos adicionais servidores tooscale seu ambiente.
- servidor de processos de Olá utiliza uma cache com base em disco. Utilize um disco separado de cache de 600 GB ou mais toohandle alterações aos dados armazenadas no evento Olá de um estrangulamento de rede ou uma interrupção.
- Se precisar mais de 200 máquinas tooprotect ou taxa de alteração diária Olá é maior do que 2 TB, pode adicionar o processo servidores toohandle Olá replicação carga. tooscale terminar, pode:
    - Aumente o número de Olá de servidores de configuração. Por exemplo, pode proteger a segurança de máquinas de too400 com dois servidores de configuração.
    - Adicionar mais servidores de processos e utilizar o servidor de configuração destes toohandle tráfego em vez de (ou além de) Olá.


### <a name="example-process-server-scaling"></a>Servidor de processos de exemplo da receção

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

## <a name="deploy-additional-process-servers"></a>Implementar servidores de processos adicionais

1. Siga [estas instruções](site-recovery-vmware-setup-azure-ps-resource-manager.md) tooset configurar um servidor de processos adicionais.
2. Se não tiver o frase de acesso de Olá, execute **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** no tooget de servidor de configuração de Olá-lo.
3. Depois de configurar o servidor de processos de Olá, migrar toouse de máquinas de origem-lo.

    1. No **definições** > **servidores do Site Recovery**, clique em servidor de configuração de Olá > **processar servidores**.
    2. Servidor de processos do contexto Olá atualmente em utilização > **comutador**.
    3. No **servidor de processos de destino selecione**, selecione esse servidor Olá do servidor de processos de Olá que pretende toouse e selecione Olá VMs irá processar.
    4. Clique Olá ícone de informações. toohelp que tomar decisões de carga, Olá espaço médio que necessários tooreplicate cada selecionado VM toohello novo servidor de processos é apresentado.
    5. Clique em Olá marca de verificação toostart replicação toohello novo servidor de processos.

## <a name="control-network-bandwidth"></a>Largura de banda de rede de controlo

Depois de executar [ferramenta de implementação Planner Olá](site-recovery-deployment-planner.md) largura de banda do toocalculate Olá que precisa para a replicação (replicação inicial Olá e, em seguida, delta), pode controlar a quantidade de Olá de largura de banda utilizada na replicação através de duas opções:

* **Limitar largura de banda**: tráfego do VMware que replica tooAzure passa através de um servidor de processo específico. Pode limitar a largura de banda em máquinas de Olá em execução como servidores de processos.
* **Influenciar a largura de banda**: pode influenciar a largura de banda Olá utilizada na replicação através da utilização de um par de chaves de registo de:
  * Olá **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** valor de registo Especifica o número de Olá de threads que são utilizados para a transferência de dados (replicação inicial ou delta) de um disco. Um valor mais alto aumenta a largura de banda de Olá utilizada para replicação.
  * Olá **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** Especifica Olá número de threads utilizados para a transferência de dados durante a reativação pós-falha.

### <a name="throttle-bandwidth"></a>Limitar largura de banda

1. Abra Olá snap-in MMC de cópia de segurança do Azure no agir de máquina Olá como servidor de processos de Olá. Por predefinição, um atalho para cópia de segurança está disponível no ambiente de trabalho hello, ou em Olá seguinte pasta: c:\Programas\Microsoft c:\Programas\Microsoft Azure Recovery Services agent\bin\wabadmin..
2. No snap-in Olá, clique em **alterar propriedades**.
3. No Olá **limitação** separador, selecione **ativar a limitação para operações de cópia de segurança de utilização de largura de banda de internet**.
4. Definir limites de Olá para o trabalho e de descanso horas. Intervalos válidos são de Kbps 512 too102 Mbps, por segundo.

    ![Limitação](./media/physical-walkthrough-capacity/throttle2.png)

Também pode utilizar Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitação. Exemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que não é necessária nenhuma limitação.

### <a name="influence-network-bandwidth-for-a-vm"></a>Influenciar a largura de banda de rede para uma VM

1. No registo de Olá VM, aceda demasiado**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tráfego de largura de banda de Olá tooinfluence num disco replicação, modifique o valor de Olá do **UploadThreadsPerVM**, ou crie a chave de Olá, se não existir.
   * largura de banda do tooinfluence Olá para tráfego de reativação pós-falha a partir do Azure, modifique o valor de Olá do **DownloadThreadsPerVM**.
2. valor predefinido de Olá é 4. Numa rede sobreaprovisionada, estas chaves do registo devem ser modificadas. Olá máximo é 32. Monitorizar o valor de Olá toooptimize de tráfego.




## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 4: planear o funcionamento em rede](physical-walkthrough-network.md).
