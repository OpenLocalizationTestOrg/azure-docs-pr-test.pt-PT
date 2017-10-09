---
title: "máquinas virtuais aaaReplicate Hyper-V em nuvens VMM utilizando o Azure Site Recovery e o PowerShell (Resource Manager) | Microsoft Docs"
description: "Replicar máquinas virtuais de Hyper-V em nuvens VMM utilizando o Azure Site Recovery e o PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Replicar máquinas virtuais de Hyper-V no VMM nuvens tooAzure com o PowerShell e do Azure Resource Manager
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portal Clássico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell – Clássica](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Descrição geral
O Azure Site Recovery contribui tooyour negócio continuidade e desastre (BCDR) estratégia de recuperação através da orquestração da replicação, ativação pós-falha e recuperação de máquinas virtuais num número de cenários de implementação. Para obter uma lista completa de implementação cenários Consulte Olá [descrição geral do Azure Site Recovery](site-recovery-overview.md).

Este artigo mostra como tarefas comuns do toouse PowerShell tooautomate precisa tooperform quando configurar máquinas virtuais de Hyper-V de tooreplicate do Azure Site Recovery no armazenamento de tooAzure de nuvens VMM do System Center.

Olá artigo inclui os pré-requisitos para o cenário de Olá e mostra-lhe

* Como tooset configurar um cofre dos serviços de recuperação
* Instalar Olá fornecedor do Azure Site Recovery no servidor do VMM de origem de Olá
* Registar o servidor de Olá no Cofre de Olá, adicione uma conta de armazenamento do Azure
* Instalar o agente de Azure Recovery Services Olá nos servidores de anfitrião do Hyper-V
* Configurar definições de proteção de nuvens do VMM, que serão aplicados tooall protegida máquinas virtuais
* Ative a proteção para as máquinas virtuais.
* Teste Olá toomake de ativação pós-falha se que tudo está a funcionar conforme esperado.

Caso se depare com problemas de configuração neste cenário, publique as suas perguntas nos Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação do Resource Manager Olá.
>
>

## <a name="before-you-start"></a>Antes de começar
Certifique-se de que tem os pré-requisitos:

### <a name="azure-prerequisites"></a>Pré-requisitos do Azure
* Precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/). Se não tiver uma, comece por um [conta gratuita](https://azure.microsoft.com/free). Além disso, pode ler sobre Olá [preços do Microsoft Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Irá precisar de uma subscrição do CSP se estiver a tentar terminar o cenário de subscrição do Olá replicação tooa CSP. Saiba mais sobre o programa CSP Olá no [como tooenroll no programa CSP Olá](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Irá precisar de um tooAzure de dados replicados toostore de conta de armazenamento (Resource Manager) de v2 do Azure. conta de Olá tem georreplicação ativada. Deve estar no Olá mesma região que Olá serviço Azure Site Recovery e estar associado a Olá mesma subscrição ou na subscrição do CSP Olá. toolearn mais informações sobre como configurar o armazenamento do Azure, consulte Olá [introdução tooMicrosoft Storage do Azure](../storage/common/storage-introduction.md) para referência.
* Terá de certificar-se de que as máquinas virtuais que pretende tooprotect cumprir Olá toomake [pré-requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> Atualmente, apenas operações ao nível de VM são possíveis através do Powershell. Suporte para operações de nível de plano de recuperação será feito em breve.  Por agora, está limitado tooperforming ativações pós-falha de datacenters apenas granularidade 'protected VM' e não um nível plano de recuperação.
>
>

### <a name="vmm-prerequisites"></a>Pré-requisitos do VMM
* Irá precisar de servidor do VMM em execução no System Center 2012 R2.
* Nenhum servidor VMM que contêm máquinas virtuais que pretende tooprotect tem de estar em execução Olá Azure Site Recovery Provider. Este é instalado durante Olá implementação do Azure Site Recovery.
* Irá precisar de pelo menos uma nuvem no Olá pretende tooprotect de servidor do VMM. Olá nuvem deve conter:
  * Um ou mais grupos de anfitriões VMM.
  * Um ou mais servidores anfitrião Hyper-V ou clusters em cada grupo anfitrião.
  * Um ou mais máquinas virtuais no servidor de Hyper-V de origem Olá.
* Saiba mais sobre como configurar as nuvens do VMM:
  * Saiba mais sobre nuvens privadas do VMM no [Novidades na nuvem privada com o System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) e na [nuvens VMM 2012 e Olá](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Saiba mais sobre [configurar Olá VMM recursos de infraestrutura de nuvem](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * Depois dos elementos de recursos de infraestrutura de nuvem estão assegurados saber sobre a criação de nuvens privadas em [criar uma nuvem privada no VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) e na [instruções: criar nuvens privadas com o VMM do System Center 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Pré-requisitos do Hyper-V
* Olá servidores anfitrião Hyper-V tem de estar em execução, pelo menos, **Windows Server 2012** com a função Hyper-V ou **Microsoft Hyper-V Server 2012** e ter Olá atualizações mais recentes instaladas.
* Se estiver a executar Hyper-V num cluster, tenha em atenção que o mediador de clusters não é criado automaticamente se tiver um cluster com base no endereço IP estático. Terá de Mediador de clusters de Olá tooconfigure manualmente. Para
* Para obter instruções, consulte [como tooConfigure Mediador de réplicas do Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Qualquer servidor de anfitrião do Hyper-V ou cluster do qual pretende toomanage proteção têm de ser incluído numa nuvem VMM.

### <a name="network-mapping-prerequisites"></a>Pré-requisitos de mapeamento da rede
Quando protege máquinas virtuais no Azure, o mapeamento da rede Olá mapeia redes de máquinas virtuais de Olá no servidor do VMM de origem de Olá e seguinte de Olá de tooenable de redes do Azure de destino:

* Todas as máquinas que efetuar a ativação pós-falha no Olá mesma rede pode ligar-se tooeach outro, independentemente do plano de recuperação onde se encontram no.
* Se um gateway de rede está configurado na rede do Azure de destino de Olá, as máquinas virtuais podem ligar tooother máquinas virtuais no local.
* Se não configurar o mapeamento da rede, Olá apenas máquinas virtuais com ativação pós-falha no Olá mesmo plano de recuperação será capaz de tooconnect tooeach outros após tooAzure de ativação pós-falha.

Se pretender que o mapeamento da rede toodeploy terá seguinte Olá:

* máquinas virtuais Olá pretende tooprotect no servidor do VMM de origem de Olá deve ser ligado tooa rede VM. Essa rede deve ser ligado tooa rede lógica que esteja associado Olá nuvem.
* Máquinas virtuais toowhich replicado uma rede do Azure podem ligar após a ativação pós-falha. Selecionará esta rede momento Olá da ativação pós-falha. rede de Olá deve estar no Olá mesma região que a sua subscrição do Azure Site Recovery.

Saiba mais sobre o mapeamento da rede no

* [Como tooconfigure redes lógicas no VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Como tooconfigure VM redes e gateways no VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Como tooconfigure e monitorizar redes virtuais no Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a>Pré-requisitos do PowerShell
Certifique-se de que tem toogo pronto do Azure PowerShell. Se já estiver a utilizar o PowerShell, terá de tooupgrade tooversion 0.8.10 ou posterior. Para informações sobre como configurar o PowerShell, consulte Olá [orientar tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs). Assim que tiver definido e configurado o PowerShell, pode ver todas Olá cmdlets disponíveis para o serviço de Olá [aqui](/powershell/azure/overview).

toolearn sobre sugestões que podem ajudar a utilizar os cmdlets de Olá, tais como a forma como os valores de parâmetros, entradas e saídas normalmente são processadas no Azure PowerShell, consulte Olá [guia tooget iniciado com Cmdlets do Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Passo 1: Conjunto Olá subscrição
1. A partir do powershell do Azure, o início de sessão tooyour conta do Azure: Olá os seguintes cmdlets a utilizar

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Obter uma lista das suas subscrições. Isto também irá listar Olá subscriptionIDs para cada uma das subscrições de Olá. Anotar Olá subscriptionID da subscrição Olá no qual pretende o Cofre de serviços de recuperação de Olá toocreate

        Get-AzureRmSubscription
3. Subscrição de Olá conjunto no qual Olá cofre dos serviços de recuperação é toobe criado pelo mentioning Olá ID de subscrição

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Passo 2: crie um cofre dos Serviços de Recuperação
1. Criar um grupo de recursos no Gestor de recursos do Azure se ainda não tiver um

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Crie um novo cofre de serviços de recuperação e guarde Olá criada o objeto de Cofre de ASR numa variável (serão utilizados mais tarde). Também pode obter Olá ASR cofre após criar o objeto utilizando o cmdlet Get-AzureRMRecoveryServicesVault de Olá:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Passo 3: Definir o contexto do Cofre de serviços de recuperação de Olá

Definir o contexto de cofre Olá executando Olá comando abaixo.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Passo 4: Instalar Olá Azure Site Recovery Provider
1. Na máquina do VMM de Olá, crie um diretório, executando Olá os seguintes comandos:

       New-Item c:\ASR -type directory
2. Extraia os ficheiros de Olá utilizando o fornecedor de Olá transferido através da execução Olá comando a seguir

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Instale o fornecedor de Olá utilizando Olá os seguintes comandos:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Aguarde Olá toofinish de instalação.
4. Registe o servidor de Olá no cofre Olá utilizando Olá os seguintes comandos:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a>Passo 5: Criar uma conta de armazenamento do Azure

Se não tiver uma conta de armazenamento do Azure, criar uma conta de georreplicação ativada na Olá mesma geografia que Olá cofre executando Olá os seguintes comandos:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Tenha em atenção que conta de armazenamento Olá tem de ser no Olá mesma região que o serviço do Azure Site Recovery Olá e associado Olá mesma subscrição.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Passo 6: Instalar Olá Azure Recovery Services Agent
1. Transferir o agente de serviços de recuperação do Azure Olá em [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) e instale-lo em cada servidor de anfitrião de Hyper-V localizado em Olá VMM nuvens pretende tooprotect.
2. Execute os seguintes comandos em todos os anfitriões VMM de Olá:

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Passo 7: Configurar a nuvem as definições de proteção
1. Crie um tooAzure de política de replicação através da execução Olá os seguintes comandos:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Obtenha um contentor de proteção através da execução Olá os seguintes comandos:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Obter a variável de tooa de detalhes do Olá política utilizando a tarefa de Olá que foi criada e mentioning nome amigável de política de Olá:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Inicie associação Olá do contentor de proteção de Olá com a política de replicação de Olá:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. Depois de concluir a tarefa de Olá, execute Olá os seguintes comandos:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. Depois da tarefa de Olá terminou o processamento, execute Olá os seguintes comandos:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

conclusão de Olá toocheck operação Olá, siga os passos Olá [monitorizar a atividade](#monitor).

## <a name="step-8-configure-network-mapping"></a>Passo 8: Configurar o mapeamento da rede
Antes de começar mapeamento da rede Verifique se as máquinas virtuais no servidor do VMM de origem de Olá tooa ligado rede VM. Além disso, crie um ou mais redes virtuais do Azure.

Saiba mais sobre como toocreate a virtual rede utilizando o Azure Resource Manager e o PowerShell, no [criar uma rede virtual com uma ligação de VPN de site para site com o Azure Resource Manager e o PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Tenha em atenção que várias redes de Máquina Virtual podem ser mapeado tooa única rede Azure. Se a rede de destino Olá tem várias sub-redes e uma dessas sub-redes tem Olá mesmo nome de sub-rede na máquina virtual de origem que Olá está localizado, em seguida, Olá máquina virtual de réplica será ligada toothat sub-rede de destino após a ativação pós-falha. Se não existir nenhuma sub-rede de destino com um nome correspondente, Olá máquina de virtual será ligado toohello primeira sub-rede Olá rede.

1. Step-by-Olá primeiro comando obtém servidores para o Cofre de recuperação de sites do Azure atual Olá. comando de Olá armazena os servidores do Microsoft Azure Site Recovery de Olá na variável de matriz Olá $Servers.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Step-by-Olá segundo comando obtém a rede de recuperação de site Olá para o servidor primeiro Olá na matriz de Olá $Servers. comando Olá armazena redes Olá na variável Olá $Networks.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. comando terceiro Olá obtém redes virtuais do Azure e, em seguida, esse valor variável Olá $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. cmdlet final Olá cria um mapeamento entre a rede principal Olá e rede de máquina virtual do Azure Olá. Olá cmdlet Especifica uma rede principal Olá como primeiro elemento de Olá de $Networks. cmdlet de Olá Especifica uma rede de máquina virtual como primeiro elemento de Olá de $AzureVmNetworks.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Passo 9: Ativar a proteção para máquinas virtuais
Depois de servidores de Olá, nuvens e as redes estão configurados corretamente, pode ativar a proteção para máquinas virtuais na nuvem de Olá.

 Tenha em atenção o seguinte Olá:

* Máquinas virtuais têm de cumprir os requisitos do Azure. Verifique estes na [pré-requisitos e suporte](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) no guia de planeamento de Olá.
* proteção de tooenable, sistema de operativo Olá e propriedades de disco do sistema operativo tem de ser definidas para a máquina virtual de Olá. Quando cria uma máquina virtual no VMM utilizando um modelo de máquina virtual pode definir a propriedade de Olá. Também pode definir estas propriedades de máquinas virtuais existentes nos Olá **geral** e **configuração de Hardware** separadores de propriedades da máquina virtual Olá. Se não definir estas propriedades no VMM será capaz de tooconfigure-las no portal do Azure Site Recovery Olá.

1. proteção de tooenable, execute Olá contentor de proteção do comando tooget Olá os seguintes:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Obter a entidade de proteção Olá (VM) executando Olá os seguintes comandos:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Ative Olá DR para Olá VM executando Olá os seguintes comandos:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Testar a implementação
tootest a implementação pode executar um teste de ativação pós-falha para uma única máquina virtual, ou criar um plano de recuperação consiste em várias máquinas virtuais e executar uma teste de ativação pós-falha para o plano de Olá. Pós-falha de teste simula o mecanismo de ativação pós-falha e recuperação numa rede isolada. Tenha em atenção que:

* Se quiser tooconnect toohello corresponde uma máquina virtual no Azure utilizando o ambiente de trabalho remoto após a ativação pós-falha Olá, ative a ligação ao ambiente de trabalho remoto na máquina virtual de Olá antes de executar a ativação pós-falha de teste de Olá.
* Após a ativação pós-falha, utilizará uma pública IP endereço tooconnect toohello máquina virtual no Azure utilizando o ambiente de trabalho remoto. Se quiser toodo isto, certifique-se de que não tem quaisquer políticas de domínio que impedem que a máquina virtual ao ligar tooa, utilizando um endereço público.

conclusão de Olá toocheck operação Olá, siga os passos Olá [monitorizar a atividade](#monitor).

### <a name="run-a-test-failover"></a>Executar uma ativação pós-falha de teste
- Inicie ativação pós-falha de teste de Olá executando Olá os seguintes comandos:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Executar uma ativação pós-falha planeada
- Olá de iniciar a ativação pós-falha planeada, executando Olá os seguintes comandos:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Executar uma ativação pós-falha não planeada
- Iniciar Olá ativação pós-falha não planeada executando Olá os seguintes comandos:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <a name=monitor></a>Monitorizar a atividade
Utilize Olá atividade de Olá toomonitor de comandos a seguir. Tenha em atenção que tem toowait entre tarefas de Olá toofinish de processamento.

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Passos seguintes
[Leia mais](/powershell/module/azurerm.recoveryservices.backup/#recovery) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.
