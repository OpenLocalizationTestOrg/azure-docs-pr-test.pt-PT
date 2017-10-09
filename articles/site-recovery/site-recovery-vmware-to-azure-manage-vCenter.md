---
title: " Gerir um servidor VMware vCenter no Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como adicionar e gerir o VMware vCenter no Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 5be995f137d0c0efaf3050b5366a107098cae15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-vmware-vcenter-server-in-azure-site-recovery"></a>Gerir o VMware vCenter Server no Azure Site Recovery
Este artigo aborda Olá várias operações de recuperação de sites que podem ser executadas no VMware vCenter.

## <a name="prerequisites"></a>Pré-requisitos

**Suporta o VMware vCenter e VMware vSphere anfitrião do ESX** | **Detalhes** |
|--- | --- |
|**Servidores do VMware no local** | Um ou mais VMware vSphere servidores, com 6.0, 5.5, 5.1 com as atualizações mais recentes. Servidores devem estar localizados em Olá mesmo de rede como servidor de configuração de Olá (ou servidor de processo separado).<br/><br/> Recomendamos um vCenter anfitriões de toomanage de servidor, com as atualizações mais recentes do Olá 6.0 ou 5.5. Apenas as funcionalidades que estão disponíveis no 5.5 são suportadas quando implementar a versão 6.0.|

## <a name="prepare-an-account-for-automatic-discovery"></a>Preparar uma conta de deteção automática
Recuperação de sites tem acesso tooVMware para tooautomatically de servidor de processo Olá detetar máquinas virtuais e ativação pós-falha e a reativação pós-falha de máquinas virtuais.

* **Migrar**: Se pretender que apenas toomigrate tooAzure de máquinas virtuais de VMware, sem nunca voltar a falhá-los, pode utilizar uma conta do VMware com uma função só de leitura. Este tipo uma função pode executar a ativação pós-falha, mas não é possível encerrar máquinas de origem protegida. Não é necessário para a migração.
* **Replicar/recuperar**: Se pretender que a conta de Olá de replicação completo (replicar ativação pós-falha, a reativação pós-falha) toodeploy tem de ser capaz de toorun operações, tais como criar e remoção de discos, a ligar a máquina virtual.
* **A deteção automática**: é necessária, pelo menos, uma conta de só de leitura.


|**Tarefas** | **Conta/função necessários** | **Permissões** | **Detalhes**|
|--- | --- | --- | ---|
|**Servidor de processos Deteta automaticamente máquinas virtuais VMware** | Precisa de, pelo menos, um utilizador só de leitura | Objeto de centro de dados –> Propagate tooChild objeto, função = só de leitura | Utilizador atribuído ao nível do datacenter e tem acesso tooall Olá objetos no Centro de dados de Olá.<br/><br/> acesso de toorestrict, atribuir Olá **sem acesso** função com Olá **propagar toochild** objeto, objetos de subordinados toohello (anfitriões vSphere, datastores, máquinas virtuais e redes).|
|**Ativação pós-falha** | Precisa de, pelo menos, um utilizador só de leitura | Objeto de centro de dados –> Propagate tooChild objeto, função = só de leitura | Utilizador atribuído ao nível do datacenter e tem acesso tooall Olá objetos no Centro de dados de Olá.<br/><br/> acesso de toorestrict, atribuir Olá **sem acesso** função com Olá **propagar toochild** objeto toohello objetos de subordinados (anfitriões vSphere, datastores, máquinas virtuais e redes).<br/><br/> Útil para fins de migração, mas não completa replicação, ativação pós-falha, reativação pós-falha.|
|**Ativação pós-falha e a reativação pós-falha** | Sugerimos que cria uma função (AzureSiteRecoveryRole) com permissões de Olá necessário e, em seguida, atribuir Olá função tooa VMware utilizador ou grupo | Objeto de centro de dados –> Propagate tooChild objeto, função = AzureSiteRecoveryRole<br/><br/> Arquivo de dados -> atribuir espaço em, procurar o arquivo de dados, as operações de baixo nível de ficheiro, remova o ficheiro, atualizar ficheiros de máquina virtual<br/><br/> Rede -> atribuição de rede<br/><br/> Recursos -> o conjunto de tooresource atribuir VM, migrar alimentado desligar a VM, migrar alimentado na VM<br/><br/> Tarefas -> tarefas de criação, a tarefa de atualização<br/><br/> Configuração -> de máquina virtual<br/><br/> Máquina virtual -> interagir -> pergunta de resposta, a ligação de dispositivos, configurar suporte de dados do CD, configurar o suporte de dados de disquetes, desligar, ligar, instalação de ferramentas do VMware<br/><br/> Máquina virtual -> inventário -> criar, registar, anular o registo<br/><br/> Máquina virtual -> aprovisionamento -> Permitir transferências de máquina virtual, permitem carregar ficheiros de máquina virtual<br/><br/> Máquina virtual -> instantâneos -> Remover instantâneos | Utilizador atribuído ao nível do datacenter e tem acesso tooall Olá objetos no Centro de dados de Olá.<br/><br/> acesso de toorestrict, atribuir Olá **sem acesso** função com Olá **propagar toochild** objeto, objetos de subordinados toohello (anfitriões vSphere, datastores, máquinas virtuais e redes).|

## <a name="create-an-account-tooconnect-toovmware-vcenter-server-vmware-vsphere-exsi-host"></a>Criar um servidor conta tooconnect tooVMware vCenter / anfitrião do VMware vSphere EXSi
1. Inicie sessão em Olá configuração servidor e inicie Olá cspsconfigtool.exe utilizando o atalho Olá colocado Olá ambiente de trabalho.
2. Clique em **adicionar conta** no Olá **gerir conta** separador.

  ![adicionar a conta](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Forneça detalhes da conta Olá e clique em OK tooadd Olá conta. a conta de Olá deve ter privilégios de Olá listados no Olá [preparar uma conta de deteção automática](#prepare-an-account-for-automatic-discovery) secção.

  >[!NOTE]
  Demora cerca de 15 minutos para as informações de conta do Olá toobe sincronizadas cópias de segurança com o serviço de recuperação de sites Olá.


## <a name="associate-a-vmware-vcenter-vmware-vsphere-esx-host-add-vcenter"></a>Associar um VMware vCenter / ESX do VMware vSphere alojar (adicionar vCenter)
* No portal do Azure de Olá, navegue demasiado*YourRecoveryServicesVault* > **infraestrutura de recuperação de Site** > **servidores de configuração**  >  *ConfigurationServer*
* Na página de detalhes do servidor de configuração Olá clique Olá + vCenter botão.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]

## <a name="modify-credentials-used-tooconnect-toohello-vcenter-server-vsphere-esxi-host"></a>Modificar as credenciais utilizadas tooconnect toohello vCenter server / vSphere ESXi anfitrião

1. Início de sessão para Olá configuração servidor e inicie Olá cspsconfigtool.exe
2. Clique em **adicionar conta** no Olá **gerir conta** separador.

  ![adicionar a conta](./media/site-recovery-vmware-to-azure-manage-vcenter/addaccount.png)
3. Forneça detalhes da conta nova Olá e clique em OK tooadd Olá conta. a conta de Olá deve ter privilégios de Olá listados no Olá [preparar uma conta de deteção automática](#prepare-an-account-for-automatic-discovery) secção.
4. No portal do Azure de Olá, navegue demasiado*YourRecoveryServicesVault* > **infraestrutura de recuperação de Site** > **servidores de configuração**  >  *ConfigurationServer*
5. Na página de detalhes do servidor de configuração Olá clique Olá **atualização do servidor** botão.
6. Uma vez concluída a tarefa de servidor de atualização de Olá, selecione Olá vCenter Server tooopen Olá vCenter página de resumo.
7. Selecione Olá recém-adicionada conta no Olá **conta de anfitriões vSphere/servidor vCenter** campo e clique em Olá **guardar** botão.

  ![conta modificar](./media/site-recovery-vmware-to-azure-manage-vcenter/modify-vcente-creds.png)

## <a name="delete-a-vcenter-in-azure-site-recovery"></a>Eliminar um vCenter no Azure Site Recovery
1. No portal do Azure de Olá, navegue demasiado*YourRecoveryServicesVault* > **infraestrutura de recuperação de Site** > **servidores de configuração**  >  *ConfigurationServer*
2. Na página de detalhes do servidor de configuração Olá selecione Olá vCenter Server tooopen Olá vCenter página de resumo.
3. Clique em Olá **eliminar** botão toodelete Olá vCenter

  ![eliminar conta](./media/site-recovery-vmware-to-azure-manage-vcenter/delete-vcenter.png)

> [!NOTE]
Se precisar de toomodify Olá vCenters endereço de IP/FQDN, detalhes da porta tem de toodelete Olá vCenter Server e adicioná-lo novamente novamente.
