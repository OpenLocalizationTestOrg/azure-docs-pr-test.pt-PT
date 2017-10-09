---
title: "aaaReplicate tooAzure de VMs de Hyper-V no portal clássico Olá | Microsoft Docs"
description: "Este artigo descreve como tooreplicate virtual do Hyper-V máquinas tooAzure quando máquinas não são geridas em nuvens VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Replicar entre máquinas de virtuais de Hyper-V no local e o Azure (sem VMM) com o Azure Site Recovery
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portal Clássico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Este artigo descreve como tooreplicate no local tooAzure de máquinas virtuais de Hyper-V, utilizando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço, na Olá portal do Azure. Neste cenário, os servidores Hyper-V não são geridos em nuvens VMM.

Depois de ler este artigo, publique quaisquer comentários na parte inferior do hello, ou coloque questões técnicas no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Recuperação de sites no Olá portal do Azure

O Azure tem dois [modelos de implementação](../resource-manager-deployment-model.md) diferentes para criar e trabalhar com recursos – o Azure Resource Manager e o clássico. O Azure também tem dois portais – Olá portal clássico do Azure e Olá portal do Azure.

Este artigo descreve como toodeploy no portal clássico Olá. portal clássico Olá pode ser cofres existente toomaintain utilizados. Não é possível criar novos cofres através do portal clássico Olá.

## <a name="site-recovery-in-your-business"></a>Site Recovery na sua empresa

As organizações necessitam de uma estratégia BCDR que determina a forma como as aplicações e dados continuam em execução e disponíveis durante o período de indisponibilidade planeado e imprevisto e a recuperar as condições de trabalho toonormal logo que possível. Eis o que o Site Recovery pode fazer:

* Proteção fora do local para aplicações empresariais em execução em VMs de Hyper-V.
* Tooset uma única localização, gerir e monitorizar a replicação, ativação pós-falha e recuperação.
* Ativação pós-falha simples tooAzure e reativações pós-falha (recuperação) dos servidores de anfitrião do Azure tooHyper-V no seu site no local.
* Planos de recuperação que incluem várias VMs, para que a ativação pós-falha das cargas de trabalho de aplicações em camadas seja feita em conjunto.

## <a name="azure-prerequisites"></a>Pré-requisitos do Azure
* Necessita de uma conta do [Microsoft Azure](https://azure.microsoft.com/). Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* É necessário um toostore replicado dados da conta de armazenamento do Azure. conta de Olá tem georreplicação ativada. Deve estar no Olá mesma região que o cofre do Azure Site Recovery Olá e associado Olá mesma subscrição. [Saiba mais sobre o storage do Azure](../storage/common/storage-introduction.md). Tenha em atenção que não suportamos as contas de armazenamento criadas utilizando Olá [novo portal do Azure](../storage/common/storage-create-storage-account.md) entre grupos de recursos.
* Irá precisar de uma rede virtual do Azure para que as máquinas virtuais do Azure será ligado tooa rede quando efetuar a ativação pós-falha do seu site primário.

## <a name="hyper-v-prerequisites"></a>Pré-requisitos do Hyper-V
* No site do Olá origem no local, terá de um ou mais servidores que executam **Windows Server 2012 R2** com função Olá Hyper-V instalada ou **Microsoft Hyper-V Server 2012 R2**. Este servidor deve:
* Contém uma ou mais máquinas virtuais.
* Ser toohello ligado à Internet, diretamente ou através de um proxy.
* Estar em execução correções Olá descritas no artigo KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Pré-requisitos de máquina virtual
Máquinas virtuais que pretende tooprotect deve estar em conformidade com [requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Pré-requisitos de fornecedor e agente
Como parte da implementação do Azure Site Recovery irá instalar Olá Azure Site Recovery Provider e Olá Azure Recovery Services Agent em cada servidor de Hyper-V. Tenha em atenção que:

* Recomendamos que são sempre executadas versões mais recentes do Olá das Olá fornecedor e o agente. Estes estão disponíveis no portal de recuperação de Site Olá.
* Todos os servidores de Hyper-V num cofre deve ter Olá mesmo as versões de Olá fornecedor e agente.
* Olá fornecedor em execução no servidor de Olá liga tooSite recuperação através de Olá internet. Pode fazê-sem um proxy, com definições de proxy de Olá atualmente configuradas no servidor de Hyper-V hello, ou com definições de proxy personalizado que configurou durante a instalação do fornecedor. Terá de se esse servidor de proxy de Olá pretende toouse pode aceder estes URLs Olá para ligar tooAzure toomake:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Além disso, permitir endereços IP Olá descritos em [intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/details.aspx?id=41653) e o protocolo HTTPS (443). Tem de intervalos de IP de Olá tooallow da Olá região do Azure que planeia toouse e de EUA oeste.

Este gráfico mostra canais de comunicação diferente Olá e portas utilizadas pela recuperação de sites para replicação e de orquestração

![Topologia de B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Passo 1: Criar um cofre
1. Inicie sessão no toohello [Portal de gestão](https://portal.azure.com).
2. Expanda **serviços de dados** > **dos serviços de recuperação** e clique em **Cofre de recuperação de Site**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. No **nome**, introduza um cofre de Olá tooidentify nome amigável.
5. No **região**, selecione Olá região geográfica do Cofre de Olá. regiões toocheck suportada veja disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Clique em **Criar cofre**.

    ![Novo cofre](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Verifique tooconfirm de barra de estado de Olá Olá cofre foi criado com êxito. Olá cofre será listado como **Active Directory** na página do Olá principal dos serviços de recuperação.

## <a name="step-2-create-a-hyper-v-site"></a>Passo 2: Criar um site de Hyper-V
1. Na página de serviços de recuperação Olá, clique a página de início rápido Olá cofre tooopen Olá. Início rápido também pode ser aberto em qualquer altura utilizando o ícone de Olá.

    ![Guia de Introdução](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. Na lista pendente de Olá, selecione **entre um site de Hyper-V no local e o Azure**.

    ![Cenário de site Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. No **criar um Site de Hyper-V** clique **site Hyper-V criar**. Especifique um nome de site e guardar.

    ![Site Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Passo 3: Instalar Olá fornecedor e agente
Instale Olá fornecedor e agente em cada servidor de Hyper-V que tem as VMs que pretende tooprotect.

Se estiver a instalar num cluster de Hyper-V, efetua os passos 5-11 em cada nó no cluster de ativação pós-falha Olá. Depois de todos os nós estão registados e ativar a proteção, irá ser protegidas máquinas virtuais, mesmo que o se migrar entre nós no cluster de Olá.

1. No **servidores Hyper-V preparar**, clique em **transferir uma chave de registo** ficheiro.
2. No Olá **transferir chave de registo** página, clique em **transferir** site toohello seguinte. Transferir Olá tooa chave localização segura que pode facilmente ser acedida pelo servidor Olá Hyper-V. chave de Olá é válido durante 5 dias após ser gerado.

    ![Chave de registo](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Clique em **transferência Olá fornecedor** versão mais recente do tooobtain Olá.
4. Execute Olá ficheiro em cada servidor de Hyper-V que pretende tooregister no Cofre de Olá. ficheiro de Olá instala dois componentes:
   * **Fornecedor do Azure Site Recovery**— processa orquestração entre o servidor de Olá Hyper-V e o portal do Azure Site Recovery Olá e de comunicação.
   * **Azure Recovery Services Agent**— processa o transporte de dados entre máquinas virtuais em execução no servidor de Hyper-V de origem de Olá e de armazenamento do Azure.
5. Em **Microsoft Update** pode optar por atualizações. Com esta definição ativada, as atualizações do fornecedor e agente serão instaladas tooyour política do Microsoft Update de acordo com.

    ![Atualizações da Microsoft](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. No **instalação** especifique onde pretende tooinstall Olá fornecedor e agente Olá servidor Hyper-V.

    ![Localização de instalação](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Depois de concluída a instalação continuar o servidor de Olá de tooregister do programa de configuração no Cofre de Olá.
8. No Olá **as definições do cofre** página, clique em **procurar** o ficheiro de chave do tooselect Olá. Especifique a subscrição do Azure Site Recovery Olá, nome do cofre Olá, e Olá Hyper-V site toowhich Olá Hyper-V servidor pertence.

    ![Registo do servidor](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. No Olá **ligação à Internet** página especificar a forma como Olá fornecedor estabelece ligação tooAzure recuperação de sites. Selecione **utilizar definições de proxy do sistema predefinidas** toouse Olá Internet ligação predefinições configuradas no servidor de Olá. Se não especificar uma predefinição de Olá valor definições serão utilizadas.

   ![Definições da Internet](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. Registo inicia o servidor de Olá tooregister no Cofre de Olá.

    ![Registo do servidor](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Após a conclusão de registo, os metadados de Olá Hyper-V server é obtido pelo Azure Site Recovery e o servidor de Olá é apresentado no Olá **Sites Hyper-V** separador Olá **servidores** página no Olá cofre.

### <a name="install-hello-provider-from-hello-command-line"></a>Instalar Olá fornecedor Olá linha de comandos
Como alternativa, pode instalar Olá Azure Site Recovery Provider Olá linha de comandos. Deve utilizar este método se pretender que o fornecedor do tooinstall Olá num computador com o Windows Server Core 2012 R2. Execute Olá linha de comandos da seguinte forma:

1. Transferir Olá fornecedor e o registo do ficheiro de chave tooa pasta de instalação. Por exemplo: C:\ASR.
2. Execute uma linha de comandos como um administrador e escreva:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Em seguida, instale Olá fornecedor executando:

        C:\ASR> setupdr.exe /i
4. Execute Olá toocomplete registo os seguintes:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Onde os parâmetros incluem:

* **/Credentials**: especificar Olá localização da chave de registo de Olá que transferiu.
* **/ FriendlyName**: especificar um servidor de anfitrião do nome tooidentify Olá Hyper-V. Este nome será apresentado no portal de Olá
* **/ EncryptionEnabled**: opcional. Especifique se pretende que as máquinas de virtuais de réplica do tooencrypt no Azure (na encriptação de Inativos).
* **/proxyAddress**; **/proxyaddress**; **/proxyUsername**; **/proxyPassword**: opcional. Especifique parâmetros de proxy se pretende que toouse um proxy personalizado, ou o seu proxy existente requer autenticação.

## <a name="step-4-create-an-azure-storage-account"></a>Passo 4: Criar uma conta de armazenamento do Azure
* No **preparar os recursos** selecione **criar conta de armazenamento** toocreate uma conta de armazenamento do Azure se não tiver uma. conta de Olá deve ter georreplicação ativada. Deve estar no Olá mesma região que o cofre do Azure Site Recovery Olá e associado Olá mesma subscrição.

    ![Criar conta de armazenamento](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. Não é proporcionado suporte mover Olá de contas de armazenamento criada utilizando Olá [novo portal do Azure](../storage/common/storage-create-storage-account.md) entre grupos de recursos.
> 2. [Migração de contas do storage](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá mesma subscrição ou nas subscrições não é suportada para contas de armazenamento utilizadas para implementar a recuperação de sites.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Passo 5: Criar e configurar grupos de proteção
Grupos de proteção são agrupamentos lógicos de máquinas virtuais que pretende utilizar tooprotect Olá mesmas definições de proteção. Aplicar o grupo de proteção de tooa de definições de proteção e essas definições são aplicados tooall máquinas de virtuais que adicione toohello grupo.

1. No **criar e configurar grupos de proteção** clique **criar um grupo de proteção**. Se qualquer um dos pré-requisitos não está no local é emitida uma mensagem e pode clicar em **ver detalhes** para obter mais informações.
2. No Olá **grupos de proteção** separador, adicione um grupo de proteção. Especifique um nome, o site de origem Hyper-V de Olá, o destino Olá **Azure**, o nome da subscrição do Azure Site Recovery e Olá conta do storage do Azure.

    ![Grupo de proteção](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. No **as definições de replicação** conjunto Olá **copiar frequência** toospecify frequência delta de dados de Olá deve ser sincronizado entre Olá origem e de destino. Pode definir too30 segundos, 5 minutos ou 15 minutos.
4. No **manter pontos de recuperação** especificar quantos horas do histórico de recuperação devem ser armazenadas.
5. No **frequência de instantâneos consistentes com aplicações** pode especificar se tootake instantâneos que utilizam o serviço de cópia de sombra de Volume (VSS) tooensure que aplicações estão num estado consistente quando se obtém o instantâneo de Olá. Por predefinição, estas não são executadas. Certifique-se de que este valor é definido tooless ao número de Olá de pontos de recuperação adicionais que configura. Só é suportada se a máquina virtual de Olá está a executar um sistema operativo Windows.
6. No **hora de início da replicação inicial** especificar quando a replicação inicial das máquinas virtuais no grupo de proteção de Olá deve ser enviada tooAzure.

    ![Grupo de proteção](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Passo 6: Ativar a proteção da máquina virtual
Adicione proteção tooenable grupo de proteção de tooa de máquinas virtuais para os mesmos.

> [!NOTE]
> Não é suportada a proteção de VMs que executam Linux com um endereço IP estático.
>
>

1. No Olá **máquinas** separador Olá grupo de proteção, clique em * * Adicionar máquinas virtuais tooprotection grupos tooenable proteção * *.
2. No Olá **ativar a proteção da Máquina Virtual** página Olá selecione máquinas que pretende tooprotect.

    ![Ativar a proteção da máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    as tarefas de ativar a proteção de Olá começa. Pode controlar o progresso no Olá **tarefas** separador. Após a tarefa finalizar proteção de Olá executa Olá máquina está preparada para ativação pós-falha.
3. Após a proteção está a configurar pode:

   * Ver as máquinas virtuais no **itens protegidos** > **grupos de proteção** > *protectiongroup_name*  >  **Máquinas virtuais** pode desagregar toomachine detalhes no Olá **propriedades** separador …
   * Configurar propriedades de ativação pós-falha de Olá para uma máquinas virtuais no **itens protegidos** > **grupos de proteção** > *protectiongroup_name*  >  **Máquinas virtuais** *virtual_machine_name* > **configurar**. Pode configurar:

     * **Nome**: nome de Olá da máquina virtual de Olá no Azure.
     * **Tamanho**: Olá tamanho de destino da máquina virtual Olá com ativação pós-falha.

       ![Configurar propriedades de máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Configurar as definições de máquina virtual adicional no *itens protegidos** > **grupos de proteção** > *protectiongroup_name*  >   **Máquinas virtuais** *virtual_machine_name* > **configurar**, incluindo:

     * **Adaptadores de rede**: número de Olá dos adaptadores de rede é ditado pelo tamanho Olá que especificar para Olá máquina virtual de destino. Verifique [especificações de tamanho de máquina virtual](../virtual-machines/linux/sizes.md) para o número de Olá de nics suportados pelo tamanho da máquina virtual de Olá.

       Quando modificar o tamanho de Olá para uma máquina virtual e guardar as definições de Olá, o número de Olá do adaptador de rede será alterado quando abrir **configurar** Olá página próxima vez. Olá o número de adaptadores de rede de máquinas virtuais de destino é mínimo do número de Olá de adaptadores de rede na máquina virtual de origem e o número máximo de adaptadores de rede suportados pelo tamanho Olá da máquina virtual de Olá escolhido. Este é explicado abaixo:

       * Se o número de Olá de adaptadores de rede na máquina de origem Olá é menor ou igual toohello número de adaptadores de permitido para o tamanho da máquina de destino Olá, em seguida, terá de destino Olá Olá o mesmo número de adaptadores que origem Olá.
       * Se o número de Olá de adaptadores Olá máquina virtual de origem excede o número de Olá permitido para o tamanho de destino Olá, o tamanho máximo de destino Olá será utilizado.
       * Por exemplo, se uma máquina de origem tiver dois adaptadores de rede e tamanho da máquina Olá destino suporta quatro, a máquina de destino Olá terá dois adaptadores. Se Olá máquina de origem tiver dois adaptadores, mas hello tamanho de destino só suporta um computador de destino Olá terá apenas um adaptador.

     * **Rede Azure**: especificar Olá rede toowhich Olá máquina deve efetuar a ativação pós-falha. Se a máquina virtual de Olá tem vários adaptadores de rede de todos os adaptadores de deve toohello ligada mesma rede do Azure.
     * **Sub-rede** para cada adaptador de rede na máquina virtual de Olá, sub-rede Olá selecione na máquina de Olá Olá rede Azure toowhich deve ligar após a ativação pós-falha.
     * **Endereço IP de destino**: se o adaptador de rede Olá de máquina virtual de origem é configurado toouse estático de um IP endereços, em seguida, pode especificar o endereço IP Olá para tooensure de máquina virtual de destino Olá Olá máquina tem Olá mesmo endereço IP, após a ativação pós-falha .  Se não especificar um endereço IP será atribuído qualquer endereço disponível no momento de Olá de ativação pós-falha. Se especificar um endereço que está a ser utilizado irão falhar a ativação pós-falha.

     > [!NOTE]
     > [Migração de redes](../azure-resource-manager/resource-group-move-resources.md) em recursos grupos dentro Olá mesma subscrição ou nas subscrições não é suportada para redes utilizadas para implementar a recuperação de sites.
     >

     ![Configurar propriedades de máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Passo 7: Criar um plano de recuperação
Na implementação de Olá tootest de ordem, pode executar uma ativação pós-falha de teste para uma única máquina virtual ou um plano de recuperação que contém uma ou mais máquinas virtuais. [Saiba mais](site-recovery-create-recovery-plans.md) sobre como criar um plano de recuperação.

## <a name="step-8-test-hello-deployment"></a>Passo 8: Testar a implementação de Olá
Existem duas formas toorun um tooAzure de ativação pós-falha de teste.

* **Testar a ativação pós-falha sem uma rede Azure**— este tipo de ativação pós-falha de teste verifica que a máquina virtual Olá é apresentada corretamente no Azure. máquina virtual de Olá será ligado tooany rede Azure após a ativação pós-falha.
* **Testar a ativação pós-falha com uma rede Azure**— este tipo de verificações de ativação pós-falha que Olá ambiente de replicação completo é mostrado conforme esperado e a ativação pós-falha máquinas de virtuais Olá ligar toohello de rede do Azure de destino especificada. Tenha em atenção que para ativação pós-falha de teste sub-rede Olá de Olá máquina virtual de teste irá ser figured com base na sub-rede Olá Olá virtual da máquina de réplica. Esta é a replicação de diferentes tooregular quando de sub-rede Olá de uma máquina virtual de réplica se baseia na sub-rede Olá Olá virtual da máquina de origem.

Se quiser toorun uma ativação pós-falha de teste sem especificar uma rede do Azure não precisa de tooprepare nada.

toorun uma ativação pós-falha de teste com um destino de rede do Azure, terá de toocreate uma nova rede Azure que está isolada da sua rede de produção do Azure (comportamento predefinido quando cria uma nova rede no Azure). Leitura [executar uma ativação pós-falha de teste](site-recovery-failover.md) para obter mais detalhes.

toofully teste a implementação de replicação e da rede, terá tooset segurança infraestrutura Olá, por isso que Olá replicados toowork de máquina virtual conforme esperado. Uma forma de efetuar esta tootooset de uma máquina virtual como controlador de domínio com DNS e replicar-tooAzure utilizando toocreate de recuperação de Site, no teste de Olá de rede ao executar uma ativação pós-falha de teste.  [Leia mais](site-recovery-active-directory.md#test-failover-considerations) sobre considerações de ativação pós-falha de teste para o Active Directory.

Execute a ativação pós-falha de teste de Olá da seguinte forma:

> [!NOTE]
> tooget Olá melhor desempenho quando fizer uma tooAzure de ativação pós-falha, certifique-se de que tem instalado Olá agente do Azure na máquina de Olá protegido. Este procedimento ajuda a arrancar mais rapidamente e também ajuda a realizar o diagnóstico em caso de problemas. O agente Linux pode ser encontrado [aqui](https://github.com/Azure/WALinuxAgent) – e o agente do Windows pode ser encontrado [aqui](http://go.microsoft.com/fwlink/?LinkID=394789)
>
>

1. No Olá **planos de recuperação** separador, selecione o plano de Olá e clique em **ativação pós-falha de teste**.
2. No Olá **confirmar ativação pós-falha de teste** página selecionar **nenhum** ou uma rede de Azure específica.  Tenha em atenção que se selecionar **nenhum** Olá ativação pós-falha de teste irá verificar que a máquina virtual Olá replicou corretamente tooAzure mas não verifique a configuração de rede de replicação.

    ![Ativação pós-falha de teste](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. No Olá **tarefas** separador pode controlar o progresso de ativação pós-falha. Também deve ser capaz de toosee réplica de teste de máquina virtual Olá no Olá portal do Azure. Se estiver a configurar máquinas de virtuais tooaccess da sua rede no local, pode iniciar uma máquina virtual de toohello de ligação de ambiente de trabalho remoto.
4. Quando a ativação pós-falha de Olá atinge Olá **concluir teste** fase, clique em **concluir teste** toofinish Olá ativação pós-falha de teste. Pode desagregar toohello **tarefa** separador tootrack progresso de ativação pós-falha e estado e tooperform todas as ações que são necessárias.
5. Após a ativação pós-falha será toosee capaz de réplica de teste de máquina virtual Olá no Olá portal do Azure. Se estiver a configurar máquinas de virtuais tooaccess da sua rede no local, pode iniciar uma máquina virtual de toohello de ligação de ambiente de trabalho remoto.

   1. Certifique-se de que as máquinas virtuais de Olá iniciar com êxito.
   2. Se quiser tooconnect toohello corresponde uma máquina virtual no Azure utilizando o ambiente de trabalho remoto após a ativação pós-falha de Olá, ative a ligação de ambiente de trabalho remoto na máquina virtual de Olá antes de executar a ativação pós-falha de teste de Olá. Também terá de tooadd um ponto final RDP na máquina virtual de Olá. Pode tirar partido uma [runbook de automatização do Azure](site-recovery-runbook-automation.md) toodo que.
   3. Depois de ativação pós-falha se utiliza uma pública IP endereço tooconnect toohello máquina virtual no Azure utilizando o ambiente de trabalho remoto, certifique-se não tiver quaisquer políticas de domínio a impedem a ligação de máquina virtual de tooa utilizando um endereço público.
6. Depois de concluída a testar Olá Olá a seguir:

   * Clique em **Olá ativação pós-falha de teste está concluída**. Limpar Olá energia tooautomatically de ambiente de teste desativar e eliminar Olá máquinas virtuais de teste.
   * Clique em **notas** toorecord e guardar todas as observações associadas à ativação pós-falha de teste de Olá.
7. Quando a ativação pós-falha de Olá atinge Olá **concluir teste** fase concluir a verificação de Olá da seguinte forma:
   1. Vista Olá máquina virtual de réplica no Olá portal do Azure. Certifique-se de que a máquina virtual Olá é iniciado com êxito.
   2. Se estiver a configurar máquinas de virtuais tooaccess da sua rede no local, pode iniciar uma máquina virtual de toohello de ligação de ambiente de trabalho remoto.
   3. Clique em **teste concluída Olá** toofinish-lo.
   4. Clique em **notas** toorecord e guardar todas as observações associadas à ativação pós-falha de teste de Olá.
   5. Clique em **Olá ativação pós-falha de teste está concluída**. Limpar Olá energia tooautomatically de ambiente de teste desativar e eliminar Olá máquina virtual de teste.

## <a name="next-steps"></a>Passos seguintes
Depois de a implementação estar instalada e em execução, [saiba mais](site-recovery-failover.md) sobre a ativação pós-falha.
