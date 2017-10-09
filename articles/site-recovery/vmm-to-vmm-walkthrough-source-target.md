---
title: "aaaSet segurança Olá origem e de destino para o site secundário do tooa de replicação de Hyper-V com o Azure Site Recovery | Microsoft Docs"
description: "Descreve como tooset origem Olá de segurança e de destino quando replicar VMs Hyper-V toosecondary VMM do site com o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Passo 6: Configurar a origem de replicação de Olá e de destino


Depois de criar dos serviços de recuperação cofre para Hyper-V replicação tooa site VMM secundário com [do Azure Site Recovery](site-recovery-overview.md), utilize este artigo tooset segurança origem Olá e localizações de replicação de destino. 

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Configurar o ambiente de origem Olá

Instalar Olá fornecedor do Azure Site Recovery nos servidores do VMM, detetar e registar os servidores no Cofre de Olá.

1. Clique em **passo 1: preparar infraestrutura** > **origem**.

    ![Configurar a origem](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. No **preparar a origem**, clique em **+ VMM** tooadd um servidor do VMM.

    ![Configurar a origem](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. No **Adicionar servidor**, verifique se **servidor VMM do System Center** aparece no **tipo de servidor** e esse servidor do VMM Olá cumpre Olá [pré-requisitos](#prerequisites).
4. Transfira o ficheiro de instalação do fornecedor do Azure Site Recovery Olá.
5. Transfira a chave de registo de Olá. Precisará disto quando executar a configuração. chave de Olá é válido durante cinco dias depois de gerá-la.

    ![Configurar a origem](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Instale Olá fornecedor do Azure Site Recovery no servidor do VMM Olá. Não precisa de tooexplicitly instala nada nos servidores de anfitrião do Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Instalar Olá Azure Site Recovery Provider

1. Execute o ficheiro de configuração do fornecedor de Olá em cada servidor VMM. Se o VMM for implementado num cluster, efetue Olá seguir Olá pela primeira vez que instala:
    -  Instale o fornecedor de Olá num nó ativo e concluir o servidor do Olá instalação tooregister Olá VMM no Cofre de Olá.
    - Em seguida, instale o Olá fornecedor no Olá outros nós. Os nós do cluster devem executar todos os Olá mesma versão do fornecedor de Olá.
2. A configuração executa algumas verificações de pré-requisitos e os pedidos de serviço do VMM permissão toostop Olá. Olá serviço VMM será reiniciado automaticamente após a conclusão do programa de configuração. Se instalar num VMM cluster, está a função de Cluster de Olá toostop pedido.
3. No **Microsoft Update**, pode optar toospecify que as atualizações do fornecedor são instaladas de acordo com a política do Microsoft Update.
4. No **instalação**, aceite ou modifique a localização de instalação predefinida de Olá e clique em **instalar**.

    ![Localização de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Depois de concluída a instalação, clique em **registar** tooregister servidor Olá cofre Olá.

    ![Localização de instalação](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. No **nome do cofre**, verifique o nome de Olá do Cofre de Olá no qual Olá servidor será registado. Clique em *Seguinte*.

    ![Registo do servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. No **ligação à Internet**, especifique como o fornecedor de Olá em execução no servidor do VMM Olá se liga a tooAzure.

    ![Definições da Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Pode especificar esse fornecedor Olá deve ligar diretamente toohello internet, ou através de um proxy.
   - Especifique as definições de proxy, se necessário.
   - Se utilizar um proxy, uma conta RunAs do VMM (DRAProxyAccount) é automaticamente criada utilizando Olá especificada credenciais de proxy. Configure o servidor de proxy de Olá, para que esta conta pode autenticar com êxito. Olá definições de conta RunAs podem ser modificadas na consola do VMM Olá > **definições** > **segurança** > **contas Run as**. Reinicie Olá VMM serviço tooupdate é alterada.
8. No **chave de registo**, selecione chave Olá que transferido a partir do Azure Site Recovery e copiou toohello o servidor do VMM.
9. definição de encriptação de Olá só é utilizada quando replicar VMs Hyper-V no tooAzure de nuvens do VMM. Se estiver a replicar tooa site secundário não é utilizado.
10. No **nome do servidor**, especifique o servidor de nome amigável tooidentify Olá VMM no Cofre de Olá. Numa configuração de cluster especifique o nome de função de cluster do Olá VMM.
11. No **sincronizar metadados da nuvem**, selecione se pretende toosynchronize metadados para todas as nuvens no servidor do VMM Olá Vault Olá. Esta ação só deverá toohappen uma vez em cada servidor. Se não quiser toosynchronize todas as nuvens, pode deixar esta definição desmarcada e sincronizar cada nuvem individualmente nas propriedades de nuvem de Olá na consola do VMM Olá.
12. Clique em **seguinte** processo de Olá toocomplete. Após o registo, os metadados hello do servidor do VMM são obtidos pelo Azure Site Recovery. servidor de Olá é apresentado no Olá **servidores VMM** separador Olá **servidores** página no Olá cofre.

    ![Servidor](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Depois do servidor de Olá está disponível na consola da recuperação de sites de Olá, no **origem** > **preparar a origem** selecionar servidor do VMM Olá e nuvem de Olá selecione em que Olá Hyper-V anfitrião se encontra. Em seguida, clique em **OK**.

Também pode instalar o fornecedor de Olá Olá linha de comandos:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurar o ambiente de destino Olá

Selecione o servidor do VMM de destino de Olá e na nuvem:

1. Clique em **preparar a infraestrutura** > **destino**e o servidor VMM de destino selecione Olá pretende toouse.
2. Serão apresentadas nuvens no servidor de Olá que são sincronizadas com a recuperação de sites. Selecione a nuvem de destino Olá.

   ![destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Passos seguintes

Aceda demasiado[passo 7: configurar o mapeamento da rede](vmm-to-vmm-walkthrough-network-mapping.md).
