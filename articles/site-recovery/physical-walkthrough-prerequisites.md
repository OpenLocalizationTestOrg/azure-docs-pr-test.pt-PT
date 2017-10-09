---
title: "aaaPrerequisites para replicação do servidor físico tooAzure utilizando o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá pré-requisitos para replicar as cargas de trabalho em execução no tooAzure de servidores físico Windows/Linux, utilizando o serviço do Azure Site Recovery Olá."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: b0ed53a143079877a2ad21ee17aae5510e0dc058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-physical-server-tooazure-replication"></a>Passo 2: Consultar Olá pré-requisitos para a replicação do servidor físico tooAzure

Reveja os pré-requisitos de Olá resumidos na tabela de Olá.


**Pré-requisito** | **Detalhes**
--- | ---
**Azure** | Saiba mais sobre [requisitos do Azure](site-recovery-prereq.md#azure-requirements)
**Servidor de configuração no local** | Precisa de um servidor físico (ou VM do VMware) com o Windows Server 2012 R2 ou posterior. Configurar este servidor durante a implementação da recuperação de Site.<br/><br/> Processo de Olá predefinido o servidor e o servidor de destino principal também estão instalados neste computador. Ao aumentar verticalmente, poderá ser necessário um servidor de processo separado. Se o fizer, tem Olá mesmos requisitos como servidor de configuração de Olá.<br/><br/> [Saiba mais](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**VMs no local** | As máquinas que pretende tooreplicate devem estar a executar um [sistema operativo suportado](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e estar em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URLs** | servidor de configuração de Olá necessita de acesso toothese URLs:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se tiver regras de firewall baseadas no endereço IP, certifique-se de que permitem comunicação tooAzure.<br/></br> Permitir Olá [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e Olá porta HTTPS (443).<br/></br> Permita intervalos de endereços IP para Olá região do Azure da sua subscrição e para EUA oeste (utilizado para gestão de identidade e controlo de acesso).<br/><br/> Permitir que este URL para transferência de MySQL Olá: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Serviço de mobilidade** | Instalado em cada servidor replicada.




## <a name="limitations"></a>Limitações

Tenha em atenção as limitações de Olá resumidas na tabela de Olá antes de implementar.

**Limitação** | **Detalhes**
--- | ---
**Azure** | Contas de armazenamento e rede tem de constar Olá mesma região que Olá Cofre<br/><br/> Se utilizar uma conta de armazenamento premium, terá também uma norma armazenar os registos de replicação de toostore de conta<br/><br/> Não é possível replicar toopremium contas no centro e sul da Índia.
**Servidor de configuração no local** | Se utilizar uma VM de VMware como máquina do servidor de configuração de Olá, Olá o tipo de adaptador de VM de VMware deve ser VMXNET3. Se não estiver, [instalar esta atualização](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1)<br/><br/> Para uma VM de VMware vSphere PowerCLI 6.0 deve ser instalado.<br/><br> máquina Olá não deve ser um controlador de domínio.<br/><br/> máquina Olá deve ter um endereço IP estático.<br/><br/> nome de anfitrião de Olá deve ter 15 carateres ou menos e sistema operativo deve estar em inglês.
**Replicar máquinas** | Certifique-se [limitações de VM do Azure](site-recovery-prereq.md#azure-requirements)<br/><br/> Não é possível replicar as VMs com discos encriptados ou VMs com o arranque UEFI/EFI.<br/><br> Partilhada não são suportados clusters de disco. Se a VM de origem Olá tem o agrupamento NIC, é convertido tooa único NIC após a ativação pós-falha.<br/><br/> Se as VMs têm um disco iSCSI, a recuperação de sites converte-o ficheiro VHD tooa após a ativação pós-falha. Se o destino de iSCSI Olá pode ser acedido por Olá VM do Azure, liga tooit e vê-lo tanto Olá VHD. Se isto acontecer, desligar o destino de iSCSI Olá.<br/><br/> Se pretender que o tooenable a consistência multi VM, que permite que as VMs com Olá recuperado mesmo toobe de carga de trabalho tooa em conjunto de dados consistente ponto, abra a porta 20004 no Olá VM.<br/><br/> Windows tem de estar instalado na unidade de Olá C. disco do SO Olá deve ser básicas e não dinâmica. o disco de dados de Olá pode ser dinâmico.<br/><br/> Linux /etc/hosts ficheiros em VMs devem conter entradas que mapeiam Olá anfitrião local nome tooIP endereços associados a todos os adaptadores de rede. Olá, nome de anfitrião, pontos de montagem, nome do dispositivo, os caminhos de sistema e os nomes de ficheiros (/ etc; /usr) deve ser apenas em inglês.<br/><br/> Tipos específicos de [Linux armazenamento](site-recovery-support-matrix-to-azure.md#support-for-storage) são suportados.<br/><br/>Criar ou definir **disk.enableUUID=true** nas definições de VM Olá. Esta opção fornece um toohello UUID consistente VMDK, para que monta corretamente e assegura que as alterações de delta apenas são transferido back tooon local durante a reativação pós-falha, sem replicação completa.


## <a name="next-steps"></a>Passos seguintes

- Se estiver a fazer uma implementação completa, aceda demasiado[passo 3: planear a capacidade](physical-walkthrough-capacity.md)
- Se estiver a fazer uma implementação de teste simples, aceda demasiado[passo 4: planear o funcionamento em rede](physical-walkthrough-network.md).
