---
title: aaaReplicate VMs de Hyper-V com o PowerShell e do Azure Resource Manager | Microsoft Docs
description: "Automatizar a replicação de VMs de Hyper-V tooAzure Olá com o Azure Site Recovery com o PowerShell e do Azure Resource Manager."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Replicar entre máquinas de virtuais de Hyper-V no local e o Azure utilizando o PowerShell e o Azure Resource Manager
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell – Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portal Clássico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Descrição geral
O Azure Site Recovery contribui tooyour continuidade e desastre recuperação estratégia de negócios através da orquestração da replicação, ativação pós-falha e recuperação de máquinas virtuais num número de cenários de implementação. Para obter uma lista completa dos cenários de implementação, consulte Olá [descrição geral do Azure Site Recovery](site-recovery-overview.md).

O Azure PowerShell é um módulo que fornece toomanage de cmdlets do Azure através do Windows PowerShell. Poder funcionar com dois tipos de módulos: Olá módulo Azure perfil ou o módulo do Azure Resource Manager Olá.

Cmdlets do PowerShell da recuperação de site, disponíveis com o Azure PowerShell para o Azure Resource Manager, ajudar a proteger e recuperar os seus servidores no Azure.

Este artigo descreve como toouse Windows PowerShell, juntamente com o Azure Resource Manager, toodeploy tooconfigure de recuperação de sites e orquestrar tooAzure de proteção do servidor. exemplo de Olá utilizado neste artigo mostra-lhe como tooprotect, efetuar a ativação pós-falha e recuperar máquinas virtuais no tooAzure anfitrião Hyper-V, utilizando o Azure PowerShell com o Azure Resource Manager.

> [!NOTE]
> Olá cmdlets do PowerShell da recuperação de Site atualmente permitem-lhe Olá tooconfigure seguintes: uma tooanother de site do Virtual Machine Manager, um tooAzure de site do Virtual Machine Manager e um tooAzure de site Hyper-V.
>
>

Não precisa de toobe um toouse especialista de PowerShell neste artigo, mas é necessário toounderstand Olá conceitos básicos, tais como módulos, cmdlets e sessões. Para obter mais informações sobre o Windows PowerShell, veja a [Introdução ao Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).

Também pode ler mais sobre [utilizar o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Parceiros da Microsoft que fazem parte do programa de fornecedor de solução em nuvem (CSP) Olá podem configurar e gerir a proteção de servidores dos seus clientes respetivas CSP subscrições dos clientes tootheir (subscrições de inquilino).
>
>

## <a name="before-you-start"></a>Antes de começar
Certifique-se de que tem os pré-requisitos:

* A [Microsoft Azure](https://azure.microsoft.com/) conta. Pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). Além disso, pode ler sobre [preços do Microsoft Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Para obter informações sobre esta versão e como tooinstall-lo, consulte [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Olá [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) e [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) módulos. Pode obter versões mais recentes do Olá estes módulos do Olá [galeria do PowerShell](https://www.powershellgallery.com/)

Este artigo ilustra como toouse Azure Powershell com o Azure Resource Manager tooconfigure e gerir a proteção dos seus servidores. exemplo de Olá utilizado neste artigo mostra-lhe como tooprotect uma máquina virtual, em execução num anfitrião Hyper-V, tooAzure. Olá, os seguintes pré-requisitos é exemplo toothis específico. Para um conjunto mais completo de requisitos para Olá vários cenários de recuperação de sites, consulte a documentação de toohello relativas toothat cenário.

* Um anfitrião de Hyper-V com Windows Server 2012 R2 ou Microsoft Hyper-V Server 2012 R2 que contém uma ou mais máquinas virtuais.
* Servidores de Hyper-V ligados toohello Internet, diretamente ou através de um proxy.
* Olá máquinas virtuais que pretende tooprotect deve estar em conformidade com [pré-requisitos de Máquina Virtual](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Passo 1: Iniciar sessão tooyour conta do Azure
1. Abra uma consola do PowerShell e execute este comando toosign no tooyour conta do Azure. cmdlet de Olá aparece uma página web que irá pedir que introduza as credenciais da conta.

        Login-AzureRmAccount

    Em alternativa, também pode incluir as credenciais da conta como um parâmetro toohello `Login-AzureRmAccount` cmdlet, utilizando Olá `-Credential` parâmetro.

    Se estiver a trabalhar em nome de um inquilino de parceiro CSP, especificar cliente Olá como um inquilino, utilizando o respetivo nome de domínio primário tenantID ou inquilino.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Uma conta pode ter várias subscrições, pelo que deve associar subscrição Olá pretende toouse com a conta de Olá.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Certifique-se de que a sua subscrição está registada toouse hello fornecedores do Azure para os serviços de recuperação e de recuperação de Site, utilizando Olá os seguintes comandos:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   No resultado Olá estes comandos, se hello **RegistrationState** estiver definido demasiado**registada**, pode avançar tooStep 2. Caso contrário, deve registar o fornecedor em falta Olá na sua subscrição.

   tooregister hello o fornecedor do Azure para a recuperação de sites e serviços de recuperação, execute Olá os seguintes comandos:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Certifique-se de que os fornecedores de Olá registado com êxito utilizando Olá os seguintes comandos: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` e `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Passo 2: Configurar Olá que cofre dos serviços de recuperação
1. Crie um grupo de recursos do Azure Resource Manager, nos quais irá criar cofre Olá ou utilizar um grupo de recursos existente. Pode criar um novo grupo de recursos utilizando Olá os seguintes comandos:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    em que a variável de Olá $ResourceGroupName contém o nome de Olá Olá do grupo de recursos que pretende toocreate e variável Olá $Geo contém Olá Azure região em que grupo de recursos de Olá toocreate (por exemplo, "sul do Brasil").

    Pode obter uma lista de grupos de recursos na sua subscrição utilizando Olá `Get-AzureRmResourceGroup` cmdlet.
2. Crie um novo cofre de serviços de recuperação do Azure da seguinte forma:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Pode obter uma lista de cofres existentes utilizando Olá `Get-AzureRmRecoveryServicesVault` cmdlet.

> [!NOTE]
> Se desejar operações tooperform cofres de recuperação de Site criados utilizando o portal clássico Olá ou o módulo de gestão de serviço do Azure PowerShell Olá, pode obter uma lista de cofres de tais utilizando Olá `Get-AzureRmSiteRecoveryVault` cmdlet. Deve criar um novo cofre de serviços de recuperação para todas as operações de novo. cofres de recuperação de Site Olá que criou anteriormente são suportadas, mas não tem funcionalidades mais recentes Olá.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Passo 3: Definir Olá contexto do Cofre de serviços de recuperação
1. Definir o contexto de cofre Olá executando Olá os seguintes comandos:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Passo 4: Criar um site de Hyper-V e gerar uma nova chave de registo do cofre para o site de Olá.
1. Crie um novo site de Hyper-V da seguinte forma:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Este cmdlet é iniciado um site de Olá de toocreate de tarefa de recuperação de sites e devolve um objeto de tarefa de recuperação de sites. Aguarde Olá tarefa toocomplete e certifique-se de que essa tarefa Olá foi concluída com êxito.

    Pode obter o objeto da tarefa Olá e, deste modo, verifique o estado atual do Olá da tarefa de Olá, utilizando o cmdlet Get-AzureRmSiteRecoveryJob de Olá.
2. Gerar e transferir uma chave de registo para o site de Olá, da seguinte forma:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Olá cópia transferido toohello chave Hyper-V anfitrião. Terá de site de toohello Olá tooregister chave Olá Hyper-V anfitrião.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Passo 5: Instalar o fornecedor do Azure Site Recovery Olá e Azure Recovery Services Agent no seu anfitrião de Hyper-V
1. Transferir o instalador Olá para a versão mais recente do Olá do fornecedor de Olá de [Microsoft](https://aka.ms/downloaddra).
2. Instalador de Olá execução no anfitrião do Hyper-V e no fim de Olá da instalação de Olá continuar passo de registo toohello.
3. Quando solicitado, forneça Olá transferir chave de registo do site e conclua o registo do site de toohello de anfitrião de Hyper-V Olá.
4. Certifique-se de que alojam Olá Hyper-V é site toohello registado utilizando Olá os seguintes comandos:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Passo 6: Criar uma política de replicação e associe-o contentor de proteção de Olá
1. Crie uma política de replicação da seguinte forma:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Olá de verificação devolvido tooensure de tarefa que a criação de política de replicação de Olá for bem sucedida.

   > [!IMPORTANT]
   > Olá conta de armazenamento especificada deve estar na mesma região do Azure como o seu Cofre de serviços de recuperação de Olá e deve ter o georreplicação ativada.
   >
   > * Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (clássica).
   > * Se Olá especificada a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Azure Resource Manager), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (Azure Resource Manager).
   >
   >
2. Obter Olá proteção contentor correspondente toohello site, da seguinte forma:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Inicie associação Olá do contentor de proteção de Olá com a política de replicação de Olá, da seguinte forma:

     $Policy = get-AzureRmSiteRecoveryPolicy - FriendlyName $PolicyName $associationJob = Start AzureRmSiteRecoveryPolicyAssociationJob-política $Policy - PrimaryProtectionContainer $protectionContainer

   Aguarde Olá associação tarefa toocomplete e certifique-se de que foi concluída com êxito.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Passo 7: Ativar a proteção para máquinas virtuais
1. Obter Olá proteção entidade correspondente toohello VM pretende tooprotect, da seguinte forma:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Começar a proteger a máquina virtual de Olá, da seguinte forma:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Olá conta de armazenamento especificada deve estar na mesma região do Azure como o seu Cofre de serviços de recuperação de Olá e deve ter o georreplicação ativada.
   >
   > * Se Olá especificado recuperação de conta de armazenamento é do tipo de armazenamento do Azure (clássica), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (clássica).
   > * Se Olá especificada a conta de armazenamento de recuperação é do tipo de armazenamento do Azure (Azure Resource Manager), a ativação pós-falha de Olá protegido máquinas recuperar Olá máquina tooAzure IaaS (Azure Resource Manager).
   >
   > Se Olá VM estiver a proteger tem mais de um disco tooit anexado, especifique o disco do sistema operativo Olá utilizando Olá *OSDiskName* parâmetro.
   >
   >
3. Aguarde Olá tooreach de máquinas virtuais num estado protegido após a replicação inicial Olá. Isto pode demorar algum tempo, dependendo de fatores como a quantidade de Olá de toobe dados replicado e Olá tooAzure de largura de banda disponível e a montante. Estado da tarefa Olá e StateDescription são atualizados da seguinte forma após Olá VM atingir um estado protegido.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Atualize propriedades de recuperação, tais como Olá tamanho de função da VM e rede interface cartões tooupon ativação pós-falha Olá rede Azure tooattach Olá da máquina virtual.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Passo 8: Executar uma ativação pós-falha de teste
1. Execute uma tarefa de ativação pós-falha de teste, da seguinte forma:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Certifique-se que teste Olá que é criada a VM no Azure. (tarefa de ativação pós-falha de teste de Olá estiver suspenso, depois de criar a VM de teste de Olá no Azure. tarefa de Olá conclui a limpeza artefacts Olá criado após retomar a tarefa de Olá, conforme ilustrado no passo seguinte Olá.)
3. Olá completa de teste de ativação pós-falha, da seguinte forma:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Passos Seguintes
[Leia mais](https://msdn.microsoft.com/library/azure/mt637930.aspx) sobre o Azure Site Recovery com cmdlets do PowerShell do Azure Resource Manager.
