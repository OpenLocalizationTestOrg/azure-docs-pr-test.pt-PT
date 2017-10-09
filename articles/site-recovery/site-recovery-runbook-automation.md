---
title: "planos toorecovery de runbooks de automatização do Azure do aaaAdd no Azure Site Recovery | Microsoft Docs"
description: "Saiba como do Azure Site Recovery pode ajudá-lo expandir planos de recuperação através da automatização do Azure. Saiba como toocomplete complexas tarefas durante a recuperação tooAzure."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: ecece14d-5f92-4596-bbaf-5204addb95c2
ms.service: site-recovery
ms.devlang: powershell
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: ruturajd@microsoft.com
ms.openlocfilehash: 90d517200cec5527e98a0d00da466bace587b70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-automation-runbooks-toorecovery-plans"></a>Adicionar planos de toorecovery runbooks de automatização do Azure
Neste artigo, vamos descrever como o Azure Site Recovery integra toohelp de automatização do Azure expandir os planos de recuperação. Planos de recuperação podem orquestrar a recuperação de VMs que estão protegidos com a recuperação de Site. Funcionam planos de recuperação para a nuvem de secundária de tooa de replicação tanto para tooAzure de replicação. Planos de recuperação também ajudam a efetuar a recuperação de Olá **consistentemente exata**, **repetíveis**, e **automatizada**. Se falhar a tooAzure VMs, integração com a automatização do Azure expande os planos de recuperação. Pode utilizá-la tooexecute runbooks, que oferece tarefas de automatização de elevado desempenho.

Se for novo tooAzure automatização, pode [inscrever](https://azure.microsoft.com/services/automation/) e [transfira scripts de exemplo](https://azure.microsoft.com/documentation/scripts/). Para obter mais informações e toolearn como tooorchestrate recuperação tooAzure utilizando [planos de recuperação](https://azure.microsoft.com/blog/?p=166264), consulte [do Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/).

Neste artigo, vamos descrever a forma como pode integrar os runbooks de automatização do Azure os planos de recuperação. Utilizamos exemplos tooautomate tarefas básicas que anteriormente necessitavam de intervenção manual. Podemos também descrevem como tooconvert tooa uma recuperação de vários passos clique único ação de recuperação.

## <a name="customize-hello-recovery-plan"></a>Personalizar o plano de recuperação Olá
1. Aceda toohello **recuperação de Site** painel de recursos do plano de recuperação. Neste exemplo, o plano de recuperação de Olá tem dois tooit de adicionada VMs, para recuperação. toobegin adição de um runbook, clique em Olá **personalizar** separador.

    ![Clique no botão de personalizar Olá](media/site-recovery-runbook-automation-new/essentials-rp.png)


2. Clique com botão direito **grupo 1: Iniciar**e, em seguida, selecione **post adicionar ação**.

    ![Contexto grupo 1: Iniciar e adicionar post ação](media/site-recovery-runbook-automation-new/customize-rp.png)

3. Clique em **escolher um script**.

4. No Olá **atualizar ação** painel, o script de Olá nome **Olá mundo**.

    ![Painel de ação de atualização de Olá](media/site-recovery-runbook-automation-new/update-rp.png)

5. Introduza um nome de conta de automatização.
    >[!NOTE]
    > Olá conta de automatização pode estar em qualquer região do Azure. conta de automatização de Olá tem de constar Olá mesma subscrição do cofre do Azure Site Recovery Olá.

6. Na sua conta de automatização, selecione um runbook. Este runbook é o script de Olá que é executado durante a execução de Olá Olá do plano de recuperação, após a recuperação de Olá do primeiro grupo de Olá.

7. script de Olá toosave, clique em **OK**. script de Olá é adicionada demasiado**grupo 1: pós-passos**.

    ![Grupo de pós-ação de 1:Start](media/site-recovery-runbook-automation-new/addedscript-rp.PNG)


## <a name="considerations-for-adding-a-script"></a>Considerações para adicionar um script

* Para as opções de demasiado**eliminar um passo** ou **atualizar o script de Olá**, faça duplo clique script Olá.
* Um script pode executar no Azure durante a ativação pós-falha de um tooAzure de máquina no local. -Também pode executar no Azure como um script de site principal antes de encerramento, durante a reativação pós-falha da máquina no local de tooan do Azure.
* Quando executa um script, injects um contexto de plano de recuperação. Olá seguinte exemplo mostra uma variável de contexto:

    ```
            {"RecoveryPlanName":"hrweb-recovery",

            "FailoverType":"Test",

            "FailoverDirection":"PrimaryToSecondary",

            "GroupId":"1",

            "VmMap":{"7a1069c6-c1d6-49c5-8c5d-33bfce8dd183":

                    { "SubscriptionId":"7a1111111-c1d6-49c5-8c5d-111ce8dd183",

                    "ResourceGroupName":"ContosoRG",

                    "CloudServiceName":"pod02hrweb-Chicago-test",

                    "RoleName":"Fabrikam-Hrweb-frontend-test",

                    "RecoveryPointId":"TimeStamp"}

                    }

            }
    ```

    Olá, a tabela seguinte lista Olá nome e uma descrição de cada variável no contexto de Olá.

    | **Nome da variável** | **Descrição** |
    | --- | --- |
    | RecoveryPlanName |nome de Olá do plano de Olá a ser executado. Esta variável ajuda a efetuar ações diferentes com base no nome do plano de recuperação Olá. Também pode reutilizar script Olá. |
    | FailoverType |Especifica se é um teste de ativação pós-falha de Olá, planeada ou não planeada. |
    | FailoverDirection |Especifica se a recuperação é o site primário ou secundário do tooa. |
    | GroupID |Identifica o número de grupo Olá no plano de recuperação Olá quando plano Olá está em execução. |
    | VmMap |Uma matriz de todas as VMs no grupo de Olá. |
    | Chave de VMMap |Uma chave exclusiva (GUID) para cada VM. De Olá igual Olá, Azure Virtual Machine Manager (VMM) ID Olá VM, onde for aplicável. |
    | SubscriptionId |Olá ID de subscrição do Azure na qual Olá VM foi criado. |
    | RoleName |nome de Olá do Olá VM do Azure que está a ser recuperada. |
    | CloudServiceName |nome do serviço em nuvem do Azure Olá que sob a qual Olá VM foi criada. |
    | resourceGroupName|nome do grupo de recursos do Azure Olá que sob a qual Olá VM foi criado. |
    | RecoveryPointId|Olá timestamp para quando Olá VM for recuperada. |

* Certifique-se de que a conta de automatização de Olá tem Olá seguintes módulos:
    * AzureRM.profile
    * AzureRM.Resources
    * AzureRM.Automation
    * AzureRM.Network
    * AzureRM.Compute

Todos os módulos devem ser das versões compatíveis. Tooensure uma forma fácil que todos os módulos são compatíveis é toouse versões mais recentes do Olá de todos os módulos de Olá.

### <a name="access-all-vms-of-hello-vmmap-in-a-loop"></a>Aceder a todas as VMs de Olá VMMap num ciclo
Utilize Olá seguir tooloop de código em todas as VMs de Olá Microsoft VMMap:

```
$VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
$vmMap = $RecoveryPlanContext.VmMap
 foreach($VMID in $VMinfo)
 {
     $VM = $vmMap.$VMID                
             if( !(($VM -eq $Null) -Or ($VM.ResourceGroupName -eq $Null) -Or ($VM.RoleName -eq $Null))) {
         #this check is tooensure that we skip when some data is not available else it will fail
 Write-output "Resource group name ", $VM.ResourceGroupName
 Write-output "Rolename " = $VM.RoleName
     }
 }

```

> [!NOTE]
> Olá recursos grupo e função de valores de nome estão vazios quando o script de Olá é um grupo de arranque de pré-ação tooa. valores de Olá são preenchidos apenas se Olá VM desse grupo for bem sucedida na ativação pós-falha. script de Olá é uma pós-ação de do grupo de arranque Olá.

## <a name="use-hello-same-automation-runbook-in-multiple-recovery-plans"></a>Utilize Olá mesmo runbook da automatização em vários planos de recuperação

Pode utilizar um script único nos vários planos de recuperação através da utilização de variáveis externas. Pode utilizar [variáveis da automatização do Azure](../automation/automation-variables.md) toostore parâmetros que podem passar para a recuperação de uma plano de execução. Ao adicionar o nome do plano de recuperação Olá como uma variável de toohello de prefixo, pode criar variáveis individuais para cada plano de recuperação. Em seguida, utilize variáveis de Olá como parâmetros. Pode alterar o parâmetro sem alterar o script de Olá, mas ainda alteração Olá Olá forma script funciona.

### <a name="use-a-simple-string-variable-in-a-runbook-script"></a>Utilizar uma variável de cadeia simples num runbook script

Neste exemplo, um script aceita entrada de Olá de um grupo de segurança de rede (NSG) e aplica-se de as VMs de toohello de um plano de recuperação.

Para Olá toodetect de script que plano de recuperação está em execução, utilize o contexto de plano de recuperação Olá:

```
workflow AddPublicIPAndNSG {
    param (
          [parameter(Mandatory=$false)]
          [Object]$RecoveryPlanContext
    )

    $RPName = $RecoveryPlanContext.RecoveryPlanName
```

tooapply um NSG existente, tem de saber nome NSG Olá e nome do grupo de recursos do Olá NSG. Utilize estas variáveis como entradas para os scripts de plano de recuperação. toodo isto, crie duas variáveis no Olá ativos de conta de automatização. Adicione nome Olá Olá do plano de recuperação que está a criar os parâmetros de Olá para como um nome de variável de toohello prefixo.

1. Crie um nome NSG Olá toostore variável. Adicione um nome de variável de toohello de prefixo utilizando o nome de Olá Olá do plano de recuperação.

    ![Criar uma variável de nome do NSG](media/site-recovery-runbook-automation-new/var1.png)

2. Crie o nome do grupo de recursos de uma variável toostore Olá NSG. Adicione um nome de variável de toohello de prefixo utilizando o nome de Olá Olá do plano de recuperação.

    ![Criar um nome de grupo de recursos do NSG](media/site-recovery-runbook-automation-new/var2.png)


3.  No script de Olá, utilize Olá referência código tooget Olá os valores das variáveis os seguintes:

    ```
    $NSGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSG"
    $NSGRGValue = $RecoveryPlanContext.RecoveryPlanName + "-NSGRG"

    $NSGnameVar = Get-AutomationVariable -Name $NSGValue
    $RGnameVar = Get-AutomationVariable -Name $NSGRGValue
    ```

4.  Utilize Olá variáveis no Olá runbook tooapply Olá NSG toohello interface de rede de Olá efetuada a ativação pós-falha VM:

    ```
    InlineScript {
    if (($Using:NSGname -ne $Null) -And ($Using:NSGRGname -ne $Null)) {
            $NSG = Get-AzureRmNetworkSecurityGroup -Name $Using:NSGname -ResourceGroupName $Using:NSGRGname
            Write-output $NSG.Id
            #Apply hello NSG tooa network interface
            #$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
            #Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
            #  -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $NSG
        }
    }
    ```

Para cada plano de recuperação, crie variáveis independentes, para que possa reutilizar o script de Olá. Adicione um prefixo com o nome do plano de recuperação Olá. Para um script completado, ponto a ponto para este cenário, consulte [adicionar um tooVMs IP e NSG público durante a ativação pós-falha de teste de um plano de recuperação do Site Recovery](https://gallery.technet.microsoft.com/Add-Public-IP-and-NSG-to-a6bb8fee).


### <a name="use-a-complex-variable-toostore-more-information"></a>Utilizar uma variável de complexas toostore obter mais informações

Considere um cenário em que pretende tooturn um script único num IP público em VMs específicos. Outro cenário, é aconselhável tooapply NSGs diferentes em diferentes VMs (e não em todas as VMs). Pode efetuar um script que é reutilizável para qualquer plano de recuperação. Cada plano de recuperação pode ter um número de VMs de variável. Por exemplo, uma recuperação do SharePoint tem dois front-ends. Uma aplicação básica linha de negócio (LOB) tem apenas um front-end. Não é possível criar variáveis separadas para cada plano de recuperação. 

No seguinte exemplo de Olá, iremos utilizar uma novo técnica e criar um [complexas variável](https://msdn.microsoft.com/library/dn913767.aspx?f=255&MSPPError=-2147217396) em recursos de conta de automatização do Azure Olá. Fazê-lo especificando valores múltiplos. Tem de utilizar o Azure PowerShell toocomplete Olá os seguintes passos:

1. No PowerShell, inicie sessão tooyour subscrição do Azure:

    ```
    login-azurermaccount
    $sub = Get-AzureRmSubscription -Name <SubscriptionName>
    $sub | Select-AzureRmSubscription
    ```

2. parâmetros de Olá toostore, criar Olá complexas variável utilizando o nome de Olá Olá do plano de recuperação:

    ```
    $VMDetails = @{"VMGUID"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"};"VMGUID2"=@{"ResourceGroupName"="RGNameOfNSG";"NSGName"="NameOfNSG"}}
        New-AzureRmAutomationVariable -ResourceGroupName <RG of Automation Account> -AutomationAccountName <AA Name> -Name <RecoveryPlanName> -Value $VMDetails -Encrypted $false
    ```

3. Nesta variável complexas, **VMDetails** é Olá ID de VM para Olá protegidas VM. ID de VM, do tooget Olá no portal do Azure, de Olá ver propriedades VM de Olá. Olá seguinte captura de ecrã mostra uma variável que armazena detalhes de Olá de duas VMs:

    ![Utilizar Olá ID de VM, como Olá GUID](media/site-recovery-runbook-automation-new/vmguid.png)

4. Utilize esta variável no runbook. Se Olá indicado que GUID da VM se encontra no contexto de plano de recuperação Olá, aplicar Olá NSG Olá VM:

    ```
    $VMDetailsObj = Get-AutomationVariable -Name $RecoveryPlanContext.RecoveryPlanName
    ```

4. No runbook, percorrer Olá VMs do contexto de plano de recuperação Olá. Verifique se Olá VM existe no **$VMDetailsObj**. Se existir, aceder às propriedades de Olá da Olá de variável tooapply Olá NSG:

    ```
        $VMinfo = $RecoveryPlanContext.VmMap | Get-Member | Where-Object MemberType -EQ NoteProperty | select -ExpandProperty Name
        $vmMap = $RecoveryPlanContext.VmMap

        foreach($VMID in $VMinfo) {
            Write-output $VMDetailsObj.value.$VMID

            if ($VMDetailsObj.value.$VMID -ne $Null) { #If hello VM exists in hello context, this will not b Null
                $VM = $vmMap.$VMID
                # Access hello properties of hello variable
                $NSGname = $VMDetailsObj.value.$VMID.'NSGName'
                $NSGRGname = $VMDetailsObj.value.$VMID.'NSGResourceGroupName'

                # Add code tooapply hello NSG properties toohello VM
            }
        }
    ```

Pode utilizar Olá mesmo script para planos de recuperação diferente. Introduza diferentes parâmetros armazenando valor Olá que corresponde ao plano de recuperação tooa em diferentes variáveis.

## <a name="sample-scripts"></a>Scripts de exemplo

tooyour de scripts de exemplo toodeploy conta de automatização, clique em Olá **implementar tooAzure** botão.

[![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

Para obter outro exemplo, consulte Olá seguir as vídeo. Demonstra como toorecover um tooAzure de aplicação do WordPress de duas camadas:


> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/One-click-failover-of-a-2-tier-WordPress-application-using-Azure-Site-Recovery/player]



## <a name="additional-resources"></a>Recursos adicionais
* [Conta do Azure Automation serviço Run As](../automation/automation-sec-configure-azure-runas-account.md)
* [Descrição geral de automatização do Azure](http://msdn.microsoft.com/library/azure/dn643629.aspx "descrição geral da automatização do Azure")
* [Scripts de exemplo de automatização do Azure](http://gallery.technet.microsoft.com/scriptcenter/site/search?f\[0\].Type=User&f\[0\].Value=SC%20Automation%20Product%20Team&f\[0\].Text=SC%20Automation%20Product%20Team "scripts de exemplo da automatização do Azure")
