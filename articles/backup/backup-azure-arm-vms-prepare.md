---
title: "Cópia de segurança do Azure: Preparar tooback segurança das máquinas virtuais | Microsoft Docs"
description: "Certifique-se de que o seu ambiente está preparado para fazer uma cópia de segurança de máquinas virtuais no Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "cópias de segurança; cópia de segurança;"
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Preparar o seu tooback de ambiente de segurança das máquinas de virtuais implementadas no Resource Manager
> [!div class="op_single_selector"]
> * [Modelo do Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modelo clássico](backup-azure-vms-prepare.md)
>
>

Este artigo fornece os passos de Olá para preparar o seu tooback de ambiente de uma máquina de virtual (VM) implementadas no Resource Manager. Olá passos apresentados nos procedimentos de Olá utilizam Olá portal do Azure.  

Olá serviço de cópia de segurança do Azure tem dois tipos de cofres (uma cópia de segurança cofres e os cofres dos serviços de recuperação) para proteger as suas VMs. Um cofre de cópia de segurança protege VMs implementadas utilizando o modelo de implementação clássica Olá. Protege um cofre dos serviços de recuperação **VMs ambos implementadas clássico ou implementadas no Resource Manager**. Tem de utilizar um tooprotect do Cofre de serviços de recuperação uma VM implementadas no Resource Manager.

> [!NOTE]
> O Azure tem dois modelos de implementação para criar e trabalhar com recursos: [Resource Manager e Clássico](../azure-resource-manager/resource-manager-deployment-model.md). Consulte [preparar o seu tooback ambiente máquinas virtuais do Azure](backup-azure-vms-prepare.md) para obter detalhes sobre como trabalhar com a implementação clássica modelo VMs.
>
>

Antes de poder proteger ou fazer uma cópia de segurança de uma máquina de virtual (VM) implementadas no Resource Manager, certifique-se que estes pré-requisitos existem:

* Criar um cofre dos serviços de recuperação (ou identificar um cofre de serviços de recuperação existente) *no Olá mesma localização que a VM*.
* Selecionar um cenário, definir a política de cópia de segurança de Olá e definir tooprotect de itens.
* Verifique a instalação de Olá do agente da VM na máquina virtual.
* Verifique a conectividade de rede
* Para VMs com Linux, no caso de pretender toocustomize o ambiente de cópia de segurança para cópias de segurança de aplicação siga Olá [tooconfigure passos previamente instantâneo e pós-instantâneo scripts](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Se souber estas condições já existem no seu ambiente, em seguida, avançar toohello [cópia de segurança do artigo VMs](backup-azure-vms.md). Se precisar de tooset cópias de segurança, ou consulte, qualquer um destes pré-requisitos, este artigo orienta-o através de Olá passos tooprepare desse pré-requisito.

##<a name="supported-operating-system-for-backup"></a>Sistema operativo suportado para cópia de segurança
 * **Linux**: o Azure Backup suporta [uma lista de distribuições apoiadas pelo Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), exceto Core OS Linux. _Outras Bring-Your-proprietário-as distribuições do Linux também podem funcionar desde que o agente VM de Olá está disponível na máquina virtual de Olá e suporte para o Python existe. No entanto, não podemos apoia esses distribuições para cópia de segurança._
 * **Windows Server**: não são suportadas as versões mais antigas do que o Windows Server 2008 R2.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitações ao fazer cópias de segurança e restauro de uma VM
Antes de preparar o seu ambiente,. compreenda as limitações de Olá.

* Não é suportada a cópia de segurança de máquinas virtuais com mais de 16 discos de dados.
* Não é suportada a cópia de segurança das máquinas virtuais com dados tamanhos de disco superiores a 1023GB.
* Não é suportada a cópia de segurança de máquinas virtuais com um endereço IP reservado e nenhum ponto final de definidos.
* Cópia de segurança de VMs encriptada utilizando apenas BEK não é suportada. Cópia de segurança de VMs com Linux encriptados utilizando a encriptação de LUKS não é suportada.
* Não é recomendada a cópia de segurança das VMs de escala terminar a configuração do servidor de ficheiros.
* Dados de cópia de segurança não incluem tooVM unidades anexadas de rede montada.
* A substituição de uma máquina virtual existente durante o restauro não é suportada. Se tentar toorestore Olá VM quando existe Olá VM, a operação de restauro Olá falha.
* Não são suportados por várias regiões cópia de segurança e restauro.
* Pode efetuar cópias de segurança de máquinas virtuais em todas as regiões públicas do Azure (consulte Olá [lista de verificação](https://azure.microsoft.com/regions/#services) de regiões suportadas). Se a região Olá que procura não é suportado atualmente, não irá aparecer na lista pendente de Olá durante a criação do cofre.
* Restaurar um controlador de domínio (DC) VM que faz parte de uma configuração de várias DC é suportada apenas através do PowerShell. Leia mais sobre [restaurar um controlador de domínio do DC várias](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Máquinas virtuais que possuem Olá seguintes configurações de rede especiais o restauro é suportado apenas através do PowerShell. VMs criadas utilizando o fluxo de trabalho de restauro de Olá no Olá IU não terá estas configurações de rede após a conclusão da operação de restauro Olá. toolearn mais, consulte [restaurar VMs com configurações de rede especiais](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Máquinas virtuais em configuração de Balanceador de carga (interna e externa)
  * Máquinas virtuais com vários endereços IP reservados
  * Máquinas virtuais com vários adaptadores de rede

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Criar um cofre dos Serviços de Recuperação para uma VM
Um cofre dos serviços de recuperação é uma entidade que armazena cópias de segurança de Olá e os pontos de recuperação que foram criados ao longo do tempo. Olá Cofre de serviços de recuperação também contém as políticas de cópia de segurança Olá associado às máquinas virtuais Olá protegido.

cofre dos serviços de toocreate uma recuperação:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. No menu do Hub de Olá, clique em **procurar** e, na lista de Olá de recursos, escreva **dos serviços de recuperação**. À medida que começa a escrever, irá filtrar a lista de Olá com base na sua entrada. Clique em **Cofre dos Serviços de Recuperação**.

    ![Clique no botão Procurar de Olá e o tipo dos serviços de recuperação. Quando vir Olá dos serviços de recuperação cofre opção, clique nela tooopen Olá dos serviços de recuperação Cofre Painel.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    é apresentada a lista de Olá de cofres dos serviços de recuperação.
3. No Olá **cofres dos serviços de recuperação** menu, clique em **adicionar**.

    ![Passo 2 da Criação do Cofre dos Serviços de Recuperação](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    é aberto o painel do cofre dos serviços de recuperação Olá que lhe pede tooprovide um **nome**, **subscrição**, **grupo de recursos**, e **localização**.

    ![Passo 5 da Criação do cofre dos Serviços de Recuperação](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Para **nome**, introduza um cofre de Olá tooidentify nome amigável. nome de Olá tem toobe exclusivo para Olá subscrição do Azure. Escreva um nome que contenha entre 2 e 50 carateres. Tem de começar com uma letra e pode conter apenas letras, números e hífenes.
5. Clique em **subscrição** toosee Olá lista de subscrições disponíveis. Se não tiver a certeza de que toouse de subscrição, utilize a predefinição de Olá (ou sugerida) subscrição. Apenas haverá várias escolhas se a sua conta organizacional estiver associada a várias subscrições do Azure.
6. Clique em **grupo de recursos** toosee Olá a lista de grupos de recursos disponíveis ou clique em **novo** toocreate um novo grupo de recursos. Para mais informações mais completas sobre os grupos de Recursos, veja [Descrição geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Clique em **localização** tooselect região geográfica do Olá para o Cofre de Olá. cofre Olá **tem** constar Olá mesma região que Olá máquinas que pretende que o tooprotect.

   > [!IMPORTANT]
   > Se não souber de localização de Olá na qual existe a VM, feche a caixa de diálogo de criação Olá cofre e aceda toohello lista de máquinas virtuais no portal de Olá. Se tiver máquinas virtuais em várias regiões, terá de toocreate um cofre dos serviços de recuperação em cada região. Crie o Cofre de Olá na localização primeiro Olá antes de avançar toohello de localização seguinte. Não existe nenhuma conta de armazenamento de toospecify necessidade de dados de cópia de segurança de Olá toostore – Cofre de serviços de recuperação de Olá e Olá serviço cópia de segurança do Azure processam isto automaticamente.
   >
   >

8. Clique em **Criar**. -Pode demorar algum tempo para Olá toobe criado do cofre dos serviços de recuperação. Monitorizar as notificações de estado Olá Olá área superior direita no portal de Olá. Assim que o Cofre for criado, aparece na lista de Olá de cofres dos serviços de recuperação. Se não vir o cofre, clique em **atualizar** para

    ![Lista de cofres de cópia de segurança](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Agora que criou o seu Cofre, saiba como tooset Olá replicação de armazenamento.

## <a name="set-storage-replication"></a>Definir Replicação de Armazenamento
opção de replicação de armazenamento Olá permite-lhe toochoose entre o armazenamento georredundante e localmente redundante. Por predefinição, o seu cofre tem um armazenamento georredundante. Deixe o armazenamento com redundância toogeo do conjunto de opção Olá se esta for a sua cópia de segurança primária. Escolha armazenamento localmente redundante se pretende uma opção mais barata que não é tão durável.

definição de replicação de armazenamento de Olá tooedit:

1. No Olá **cofres dos serviços de recuperação** painel, selecione o cofre.
    Ao clicar em seu Cofre, Olá painel Definições (*que tem Olá do Cofre de Olá na parte superior do Olá*) e cofre Olá é aberto o painel de detalhes.

    ![Escolha o Cofre Olá lista de cofres de cópia de segurança](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. No Olá **definições** painel, utilize Olá vertical do controlo de deslize tooscroll baixo toohello **gerir** secção. Clique em **infraestrutura de cópia de segurança** tooopen respetivo painel. No Olá **geral** secção clique **configuração de cópia de segurança** tooopen respetivo painel. No Olá **configuração de cópia de segurança** painel, escolha a opção de replicação de armazenamento Olá para o cofre. Por predefinição, o seu cofre tem um armazenamento georredundante. Se alterar o tipo de replicação de armazenamento Olá, clique em **guardar**.

    ![Lista de cofres de cópia de segurança](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Se estiver a utilizar o Azure como um ponto final de armazenamento de cópia de segurança primário, continue a utilizar o armazenamento georredundante. Se estiver a utilizar o Azure como um ponto final de armazenamento de cópia de segurança não primário, em seguida, escolha armazenamento localmente redundante. Leia mais sobre [georredundante](../storage/common/storage-redundancy.md#geo-redundant-storage) e [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opções de armazenamento Olá [descrição geral da replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).
    Depois de escolher a opção de armazenamento de Olá para o cofre, está pronto tooassociate Olá VM com o Cofre de Olá. associação de Olá toobegin, detete e registe Olá máquinas virtuais do Azure.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selecionar um objetivo de cópia de segurança, defina a política e definir tooprotect de itens
Antes de registar uma VM com um cofre, execute tooensure de processo de deteção de Olá que as novas máquinas virtuais que foram adicionadas toohello subscrição são identificadas. Olá processo consulta o Azure para Olá obter lista de máquinas virtuais na subscrição Olá, juntamente com informações adicionais, como o nome do serviço de nuvem de Olá e região Olá. No portal do Azure Olá, cenário refere-se toowhat vai tooput no Cofre de serviços de recuperação Olá. A política é agenda Olá frequência e quando são tirados pontos de recuperação. A política também inclui o período de retenção de Olá Olá pontos de recuperação.

1. Se já tiver um cofre dos serviços de recuperação, abra o, continuar toostep 2. Se não tiver um cofre dos serviços de recuperação, abrir, em seguida, abra Olá [portal do Azure](https://portal.azure.com/) e no menu do Hub de Olá, clique em **mais serviços**.

   * Na lista de Olá de recursos, escreva **dos serviços de recuperação**.
   * À medida que começa a escrever, irá filtrar a lista de Olá com base na sua entrada. Quando vir **Cofres dos Serviços de Recuperação**, clique no mesmo.

     ![Passo 1 da Criação de um Cofre dos Serviços de Recuperação](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     é apresentada a lista de Olá de cofres dos serviços de recuperação. Se não houver nenhuma cofres na sua subscrição, esta lista estará vazia.

    ![Lista de cofres dos vista de Olá dos serviços de recuperação](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * Na lista de Olá dos cofres dos serviços de recuperação, selecione um cofre tooopen seu dashboard.

     Painel de definições de Olá e Olá dashboard para o Cofre de Olá escolhido, abre-se do cofre.

     ![Abrir painel do cofre](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. No menu de dashboard do cofre Olá clique **cópia de segurança** painel de cópia de segurança de Olá tooopen.

    ![Abrir o painel Backup](./media/backup-azure-arm-vms-prepare/backup-button.png)

    painéis de cópia de segurança e o objetivo de cópia de segurança de Olá abrir.

    ![Abrir o painel Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. No painel de objetivo de cópia de segurança de Olá, defina **onde está a carga de trabalho em execução** tooAzure e **que itens pretende toobackup** tooVirtual máquina, em seguida, clique em **OK**.

    Este procedimento regista Olá extensão da VM com o Cofre de Olá. Olá objetivo de cópia de segurança fecha de painel e Olá **política de cópia de segurança** abre o painel.

    ![Abrir o painel Cenário](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. No painel de política de cópia de segurança de Olá, selecione a política de cópia de segurança Olá pretende tooapply toohello cofre.

    ![Selecionar política de cópia de segurança](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    detalhes de Olá da política predefinida do Olá estão listados na menu pendente de Olá. Se pretender toocreate uma nova política, selecione **criar novo** no menu de Olá pendente. Para obter instruções sobre como definir uma política de cópia de segurança, consulte o artigo [Definir uma política de cópia de segurança](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Clique em **OK** política de cópia de segurança Olá tooassociate Vault Olá.

    Olá fechar de painel de política de cópia de segurança e Olá **selecionar máquinas virtuais** abre o painel.
5. No Olá **selecionar máquinas virtuais** painel, escolha Olá tooassociate de máquinas virtuais com Olá especificado política e clique em **OK**.

    ![Selecionar a carga de trabalho](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    máquina virtual de Olá selecionado está validada. Se não vir máquinas de virtuais Olá que esperado toosee, certifique-se de que existam na Olá mesma localização do Azure Olá dos serviços de recuperação cofre e ainda não estiverem protegida num cofre do outro. localização de Olá de Olá que cofre dos serviços de recuperação é apresentada no dashboard do Cofre de Olá.

6. Agora que definiu todas as definições para o Cofre de Olá, no painel de cópia de segurança de Olá clique **ativar Backup**. Isto implementa o Cofre de toohello de política de Olá e Olá VMs. Isto não criar um ponto de recuperação inicial de Olá para a máquina virtual de Olá.

    ![Ativar Backup](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Depois de ativar a cópia de segurança de Olá com êxito, a política de cópia de segurança será executado numa agenda. Se gostaria de toogenerate tooback uma tarefa de cópia de segurança a pedido de segurança das máquinas virtuais de Olá agora, consulte o artigo [tarefa de cópia de segurança de Olá Triggering](./backup-azure-arm-vms.md#triggering-the-backup-job).

Se tiver problemas ao registar a máquina virtual de Olá, consulte Olá seguintes informações sobre como instalar Olá agente da VM e conectividade de rede. Provavelmente, não precisa de Olá seguintes informações se estiver a proteger máquinas virtuais criadas no Azure. No entanto se tiver migrado máquinas virtuais no Azure, não se esqueça de que corretamente instalou o agente da VM Olá e de que a máquina virtual pode comunicar com a rede virtual Olá.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar Olá agente da VM na máquina virtual de Olá
Olá agente da VM do Azure tem de estar instalado na máquina virtual do Azure para toowork de extensão de cópia de segurança de Olá de Olá. Se a VM foi criada a partir de Olá galeria do Azure, em seguida, Olá agente da VM já se encontra presente na máquina virtual de Olá. Esta informação é fornecida para situações olá onde são *não* através de uma VM criada a partir de Olá galeria do Azure - por exemplo migrou uma VM a partir de um datacenter no local. Nesse caso, Olá agente da VM tem toobe instalado na máquina virtual do ordem tooprotect Olá. Saiba mais sobre Olá [agente da VM](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Se tiver problemas a cópia de segurança Olá VM do Azure, verifique se Olá agente da VM do Azure está corretamente instalado na máquina virtual de Olá (consulte a tabela de Olá abaixo). Olá, a tabela seguinte fornece informações adicionais sobre o agente de VM Olá para Windows e VMs com Linux.

| **Operação** | **Windows** | **Linux** |
| --- | --- | --- |
| Instalar Olá agente da VM |Transfira e instale Olá [MSI do agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Terá de instalação de Olá de toocomplete de privilégios de administrador. |<li> Instale os mais recentes Olá [agente Linux](../virtual-machines/linux/agent-user-guide.md). Terá de instalação de Olá de toocomplete de privilégios de administrador. Recomendamos que instale o agente do seu repositório de distribuição. Iremos **não é recomendada a** instalar agente de VM com Linux diretamente a partir do github.  |
| Atualizar Olá agente da VM |Olá atualizar agente da VM é tão simple como reinstalar Olá [binários do agente da VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Certifique-se de que nenhuma operação de cópia de segurança está em execução enquanto o agente da VM Olá está a ser atualizado. |Siga as instruções de Olá no [atualizar Olá agente da VM com Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Recomendamos a atualizar o agente do seu repositório de distribuição. Iremos **não é recomendada a** atualizar agente de VM com Linux diretamente a partir do github.<br>Certifique-se de que nenhuma operação de cópia de segurança está em execução ao hello que agente VM está a ser atualizado. |
| A validar a instalação do agente de VM de Olá |<li>Navegue toohello *C:\WindowsAzure\Packages* pasta Olá VM do Azure. <li>Deverá considerar o ficheiro do Olá WaAppAgent.exe presente.<li> Clique no ficheiro de Olá, visite demasiado**propriedades**e, em seguida, selecione Olá **detalhes** campo de versão de produto do separador. Olá deve ser 2.6.1198.718 ou superior. |N/D |

### <a name="backup-extension"></a>Extensão da cópia de segurança
Uma vez Olá que agente VM está instalado na máquina virtual de Olá, Olá serviço cópia de segurança do Azure instala a extensão de cópia de segurança de Olá toohello agente da VM. Olá serviço cópia de segurança do Azure perfeitamente atualiza e patches extensão Olá de cópia de segurança.

extensão de cópia de segurança de Olá é instalada pelo serviço de cópia de segurança de Olá Olá VM está em execução ou não. Uma VM em execução fornece a maior possibilidade de Olá de obter um ponto de recuperação consistentes com aplicações. No entanto, Olá serviço de cópia de segurança do Azure continua tooback segurança Olá VM mesmo se está a ser desativada e não foi possível instalar a extensão de Olá. Este processo é conhecido como VM Offline. Neste caso, o ponto de recuperação Olá será *consistente com a falha*.

## <a name="network-connectivity"></a>Conectividade de rede
Instantâneos VM do ordem toomanage Olá, extensão de cópia de segurança de Olá necessita de conectividade toohello Azure endereços IP públicos. Sem ligação à Internet à direita do Olá, HTTP pedidos tempo limite e Olá operação cópia de segurança da máquina virtual Olá falhará. Se a sua implementação tem restrições de acesso no local (através de um grupo de segurança de rede (NSG), por exemplo), em seguida, escolha uma destas opções para fornecer um caminho de simples para o tráfego de cópia de segurança:

* [Intervalos IP do datacenter do Azure do lista branca Olá](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -consulte o artigo de Olá para obter instruções sobre como toowhitelist Olá de endereços IP.
* Implemente um servidor de proxy HTTP para o encaminhamento de tráfego.

Ao decidir qual toouse opção, são Olá trade-offs entre capacidade de gestão, o controlo granular e o custo.

| Opção | Vantagens | Desvantagens |
| --- | --- | --- |
| Intervalos de IP da lista branca |Sem custos adicionais.<br><br>Para abrir o acesso num NSG, utilize Olá <i>conjunto AzureNetworkSecurityRule</i> cmdlet. |Toomanage complexo como alterar os intervalos IP Olá afetado ao longo do tempo.<br><br>Fornece a totalidade de toohello de acesso do Azure e não apenas o armazenamento. |
| Proxy HTTP |Controlo granular no proxy Olá sobre o armazenamento de Olá URLs permitidos.<br>TooVMs de acesso único ponto da Internet.<br>Não requerente tooAzure alterações do endereço IP. |Custos adicionais para executar uma VM com o software de proxy de Olá. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Lista de permissões os intervalos de IP Olá datacenter do Azure
intervalos de IP do toowhitelist Olá datacenter do Azure, consulte Olá [Web site Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) para obter detalhes sobre os intervalos IP Olá e obter instruções.

### <a name="using-an-http-proxy-for-vm-backups"></a>Utilizar um proxy HTTP para cópias de segurança VM
Ao fazer cópias de segurança de uma VM, a extensão de cópia de segurança de Olá no Olá VM envia Olá instantâneo gestão comandos tooAzure Storage através de uma API de HTTPS. Encaminhar o tráfego de extensão de cópia de segurança de Olá através do proxy HTTP de Olá, uma vez que é o único componente de Olá configurado para acesso toohello Internet pública.

> [!NOTE]
> Não há nenhuma recomendação de software de proxy de Olá que deve ser utilizada. Certifique-se de que escolha um proxy que é compatível com passos de configuração de Olá abaixo.
>
>

imagem de exemplo de Olá abaixo mostra os passos de configuração três Olá toouse necessário um HTTP de proxy:

* Rotas de VM de aplicação que todo o tráfego HTTP vinculado a Olá Internet pública através do Proxy de VM.
* Proxy VM permite o tráfego de entrada de VMs na rede virtual Olá.
* Olá grupo da segurança de rede (NSG) com o nome de bloqueio NSF tem um segurança regra que permite saído tráfego de Internet de VM de Proxy.

![NSG com diagrama de implementação do proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse um HTTP proxy toocommunicating toohello Internet pública, siga estes passos:

#### <a name="step-1-configure-outgoing-network-connections"></a>Passo 1. Configurar ligações de rede de saída
###### <a name="for-windows-machines"></a>Para máquinas do Windows
Isto irá configurar a configuração do servidor proxy para a conta de sistema Local.

1. Transferir [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Execute o seguinte comando na linha de comandos elevada,

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Irá abrir a janela do internet explorer.
3. Aceda a tooTools -> Opções da Internet -> ligações -> definições de LAN.
4. Verifique as definições de proxy para a conta de sistema. Definir o IP de Proxy e a porta.
5. Feche o Internet Explorer.

Isto irá configurar uma configuração de proxy a nível de máquina e será utilizado para enviar tráfego HTTP/HTTPS.

Se tiver a configuração de um servidor proxy numa conta de utilizador atual (não uma conta de sistema Local), utilize Olá seguintes script tooapply-los tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Se observar "(407) a autenticação de Proxy necessário" no registo de servidor proxy, verifique a que sua autenticação está configurada corretamente.
>
>

###### <a name="for-linux-machines"></a>Para computadores Linux
Adicionar Olá seguinte linha toohello ```/etc/environment``` ficheiro:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Adicionar Olá seguintes linhas toohello ```/etc/waagent.conf``` ficheiro:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Passo 2. Permitir ligações de entrada no servidor de proxy de Olá:
1. No servidor de proxy de Olá, abra a Firewall do Windows. a Olá mais fácil forma tooaccess Olá firewall está toosearch Firewall do Windows com segurança avançada.

    ![Abrir Olá Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. Na caixa de diálogo de Firewall do Windows hello, faça duplo clique **regras de entrada** e clique em **nova regra...** .

    ![Criar uma nova regra](./media/backup-azure-vms-prepare/firewall-02.png)
3. No Olá **novo Assistente de regras de entrada**, escolha Olá **personalizada** opção para Olá **tipo de regra** e clique em **seguinte**.
4. No Olá de tooselect de página Olá **programa**, escolha **todos os programas** e clique em **seguinte**.
5. No Olá **protocolo e portas** página, introduza Olá seguintes informações e clique em **seguinte**:

    ![Criar uma nova regra](./media/backup-azure-vms-prepare/firewall-03.png)

   * para *tipo de protocolo* escolha *TCP*
   * para *Porta Local* escolha *portas específicas*, no campo de Olá abaixo especifique Olá ```<Proxy Port>``` que foi configurado.
   * para *portas remotas* selecione *todas as portas*

     Para rest Olá do Assistente de Olá, clique em todos os fim de toohello de forma Olá e atribua um nome esta regra.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Passo 3. Adicione um toohello de regra de exceção NSG:
Numa linha de comandos do Azure PowerShell, introduza Olá os seguintes comandos:

Olá comando a seguir adiciona uma exceção toohello NSG. Esta exceção permite tráfego TCP de qualquer porta no 10.0.0.5 tooany endereço Internet na porta 80 (HTTP) ou 443 (HTTPS). Se necessitar de uma porta específica na Olá Internet pública, ser tooadd se de que porta toohello ```-DestinationPortRange``` bem.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*Estes passos utilizam valores e nomes específicos para este exemplo. Utilize Olá nomes e valores para a sua implementação quando os introduzir, ou cortando e colando detalhes para o seu código.*

Agora que já sabe que tem conectividade de rede, está pronto tooback cópias de segurança a VM. Consulte [cópia de segurança VMs implementadas no Resource Manager](backup-azure-arm-vms.md).

## <a name="questions"></a>Tem dúvidas?
Se tiver dúvidas ou se não houver qualquer funcionalidade que gostaria de toosee incluído, [envie-nos comentários](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Passos seguintes
Agora que tem de preparar o ambiente para fazer cópias de segurança a VM, o próximo passo lógico é toocreate uma cópia de segurança. Olá planeamento artigo fornece informações mais detalhadas sobre a cópia de segurança de VMs.

* [Fazer uma cópia de segurança de máquinas virtuais](backup-azure-vms.md)
* [Planear a infraestrutura de cópia de segurança de VM](backup-azure-vms-introduction.md)
* [Gerir cópias de segurança da máquina virtual](backup-azure-manage-vms.md)
