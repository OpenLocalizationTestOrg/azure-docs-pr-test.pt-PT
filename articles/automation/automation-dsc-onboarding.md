---
title: "aaaOnboarding máquinas para gestão pelo Automation DSC do Azure | Microsoft Docs"
description: "Como toosetup máquinas para gestão com o Automation DSC do Azure"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Máquinas de integração de gestão do Automation DSC do Azure

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Por que motivo gerir máquinas com o Automation DSC do Azure?

Como [configuração de estado pretendido do PowerShell](https://technet.microsoft.com/library/dn249912.aspx), a configuração de estado pretendido do Azure Automation é um serviço de gestão de configuração de simples, mas poderosa, para nós de DSC (máquinas virtuais e físicas) no Centro de dados qualquer nuvem ou no local. Permite que escalabilidade entre milhares de máquinas forma rápida e fácil de uma localização central e segura. Pode carregar facilmente máquinas, atribua-as configurações declarativas e ver relatórios, que mostra cada computador do que especificou o estado de compatibilidade toohello assim o desejar. camada de gestão do Azure Automation DSC Olá é tooDSC camada de gestão de automatização do Azure que Olá é tooPowerShell scripting. Por outras palavras, de Olá mesma maneira que a automatização do Azure ajuda-o a gerir os scripts do PowerShell, também o ajuda a gerir configurações de DSC. toolearn mais informações sobre os benefícios de Olá da utilização do Automation DSC do Azure, consulte [descrição geral do Azure Automation DSC](automation-dsc-overview.md).

Automation DSC do Azure pode ser utilizado toomanage uma variedade de máquinas:

* Máquinas virtuais do Azure (clássica)
* Máquinas virtuais do Azure
* Máquinas virtuais Amazon Web Services (AWS)
* Windows físico virtual máquinas no local, ou numa nuvem diferente do Azure/AWS
* Linux físico virtual máquinas no local, no Azure ou numa nuvem diferente do Azure

Além disso, se não estiver pronta toomanage configuração da máquina da nuvem Olá, DSC de automatização do Azure também pode ser utilizado como um ponto final só de relatório. Isto permite configuração pretendida do tooset (emitir) através do DSC no local e ver detalhes relatórios avançados de conformidade de nó com Olá pretendido estado na automatização do Azure.

Olá seguintes secções descrevem como pode carregar cada tipo de máquina tooAzure DSC de automatização.

## <a name="azure-virtual-machines-classic"></a>Máquinas virtuais do Azure (clássica)

Com o DSC de automatização do Azure, pode facilmente carregar virtual machines do Azure (clássica) para gestão de configuração utilizando o Olá portal do Azure ou o PowerShell. Em definições avançadas de Olá e sem um administrador ter tooremote para Olá VM, Olá extensão de configuração de estado pretendido do Azure VM regista Olá VM no Automation DSC do Azure. Uma vez que Olá extensão de configuração de estado pretendido do Azure VM é executado no modo assíncrono, passos tootrack progresso dela ou resolver problemas são fornecidos na Olá [ **integração de máquina virtual do Azure de resolução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)secção abaixo.

### <a name="azure-portal"></a>Portal do Azure

No Olá [portal do Azure](http://portal.azure.com/), clique em **procurar** -> **máquinas virtuais (clássicas)**. Selecione Olá VM do Windows que pretende tooonboard. No painel de dashboard da máquina virtual Olá, clique em **todas as definições** -> **extensões** -> **adicionar**  ->   **Automation DSC do Azure** -> **criar**. Introduza Olá [valores de Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para o caso de utilização, chave de registo da sua conta de automatização e URL de registo e, opcionalmente, um toohello de tooassign de configuração de nó VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

URL de registo de Olá toofind e a chave para a máquina Olá tooonboard de conta de automatização de Olá, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Máquinas virtuais do Azure

Automation DSC do Azure permite carregar facilmente máquinas virtuais do Azure para a gestão de configuração, utilizando o portal do Azure de Olá, modelos Azure Resource Manager ou PowerShell. Em definições avançadas de Olá e sem um administrador ter tooremote para Olá VM, Olá extensão de configuração de estado pretendido do Azure VM regista Olá VM no Automation DSC do Azure. Uma vez que Olá extensão de configuração de estado pretendido do Azure VM é executado no modo assíncrono, passos tootrack progresso dela ou resolver problemas são fornecidos na Olá [ **integração de máquina virtual do Azure de resolução de problemas** ](#troubleshooting-azure-virtual-machine-onboarding)secção abaixo.

### <a name="azure-portal"></a>Portal do Azure

No Olá [portal do Azure](https://portal.azure.com/), navegue até toohello conta de automatização do Azure onde pretende que as máquinas virtuais de tooonboard. No painel de conta de automatização de Olá, clique em **nós de DSC** -> **adicionar a VM do Azure**.

Em **selecionar máquinas virtuais tooonboard**, selecione um ou mais Azure virtual máquinas tooonboard.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

Em **configurar dados de registo**, introduza Olá [valores de Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) necessários para o caso de utilização e opcionalmente um toohello de tooassign de configuração de nó VM.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Modelos do Azure Resource Manager

Máquinas virtuais do Azure pode ser implementadas e simplificar tooAzure Automation DSC através de modelos Azure Resource Manager. Consulte [configurar uma VM através de extensão de DSC e Automation DSC do Azure](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) para um modelo de exemplo que onboards um tooAzure VM existente DSC de automatização. toofind Olá chave e o registo do URL de registo tomada como entrada neste modelo, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.

### <a name="powershell"></a>PowerShell

Olá [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet pode ser utilizado tooonboard máquinas virtuais Olá portal do Azure através do PowerShell.

## <a name="amazon-web-services-aws-virtual-machines"></a>Máquinas virtuais Amazon Web Services (AWS)

Pode carregar facilmente máquinas de virtuais Amazon Web Services para a gestão de configuração ao utilizar Olá AWS DSC Toolkit de Automation DSC do Azure. Pode saber mais sobre o toolkit de Olá [aqui](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Windows físico virtual máquinas no local, ou numa nuvem diferente do Azure/AWS

Máquinas do Windows no local e as máquinas do Windows em nuvens não do Azure (por exemplo, Amazon Web Services) também podem ser integrado tooAzure DSC de automatização, desde que têm acesso de saída toohello à internet, através de alguns passos simples:

1. Certifique-se de que versão mais recente de Olá do [WMF 5](http://aka.ms/wmf5latest) está instalado em máquinas de Olá pretende tooonboard tooAzure DSC de automatização.
2. Siga as indicações Olá secção [ **gerar DSC metaconfigurations** ](#generating-dsc-metaconfigurations) abaixo toogenerate uma pasta que contém Olá necessário metaconfigurations de DSC.
3. Aplica remotamente Olá PowerShell DSC configuração meta toohello as máquinas que pretende tooonboard. **Este comando é executado a partir de máquina de Olá tem de ter a versão mais recente do Olá do [WMF 5](http://aka.ms/wmf5latest) instalado**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Se não é possível aplicar Olá PowerShell DSC metaconfigurations remotamente, copie a pasta de metaconfigurations de Olá do passo 2 para cada máquina tooonboard. Em seguida, chame **conjunto DscLocalConfigurationManager** localmente em cada máquina tooonboard.
5. Utilizar Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora aparecem como nós de DSC registado na sua conta de automatização do Azure.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Linux físico virtual máquinas no local, no Azure ou numa nuvem diferente do Azure

As máquinas no local Linux, computadores Linux no Azure, e computadores Linux no Azure não nuvens também podem ser integrado tooAzure DSC de automatização, desde que têm acesso de saída toohello à internet, através de alguns passos simples:

1. Certifique-se de que versão mais recente de Olá do [PowerShell configuração de estado pretendido para Linux](https://github.com/Microsoft/PowerShell-DSC-for-Linux) está instalado em máquinas de Olá pretende tooonboard tooAzure DSC de automatização.
2. Se Olá [predefinições do Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) corresponder ao seu caso de utilização e pretender tooonboard máquinas tais que estes **ambos** solicitar a partir e comunicar tooAzure DSC de automatização:

   + Na máquina tooonboard tooAzure Automation DSC cada Linux, utilize tooonboard Register.py Olá predefinições do Gestor de configuração Local do PowerShell DSC a utilizar:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind Olá chave e o registo do URL de registo para a sua conta de automatização, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.

     Se hello predefinições do Gestor de configuração Local do PowerShell DSC **fazer** **não** corresponder ao seu caso de utilização ou se quiser tooonboard máquinas de forma a que estes apenas comunicam tooAzure DSC de automatização, mas não solicitar a configuração ou de módulos do PowerShell a partir do mesmo, siga os passos 3 a 6. Caso contrário, avance diretamente toostep 6.

3. Siga as indicações de Olá Olá [ **gerar DSC metaconfigurations** ](#generating-dsc-metaconfigurations) secção abaixo toogenerate uma pasta que contém Olá necessário metaconfigurations de DSC.
4. Aplicar remotamente Olá PowerShell DSC configuração meta toohello as máquinas que pretende tooonboard:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

Este comando é executado a partir de máquina de Olá tem de ter a versão mais recente do Olá do [WMF 5](http://aka.ms/wmf5latest) instalado.

1. Se não é possível aplicar Olá PowerShell DSC metaconfigurations remotamente, tooonboard cada computador Linux, copie a máquina de toothat correspondente do Olá configuração meta da pasta de Olá no passo 5 na máquina de Linux Olá. Em seguida, chame `SetDscLocalConfigurationManager.py` localmente em cada computador Linux que pretende tooonboard tooAzure DSC de automatização:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Utilizar Olá portal do Azure ou os cmdlets, verifique se Olá máquinas tooonboard agora aparecem como nós de DSC registado na sua conta de automatização do Azure.

## <a name="generating-dsc-metaconfigurations"></a>Gerar DSC metaconfigurations

toogenerically carregar qualquer máquina tooAzure DSC de automatização, um [configuração meta do DSC](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) pode ser gerada que, quando aplicada, diz ao agente Olá DSC no Olá máquina toopull de e/ou relatório tooAzure DSC de automatização. DSC metaconfigurations para Automation DSC do Azure pode ser gerada através de uma configuração de DSC do PowerShell, ou Olá cmdlets do PowerShell de automatização do Azure.

> [!NOTE]
> DSC metaconfigurations conter Olá segredos necessários tooonboard uma conta de automatização para a gestão de tooan máquina. Certifique-se de que tooproperly proteger qualquer metaconfigurations DSC que criar ou eliminá-los após a utilização.

### <a name="using-a-dsc-configuration"></a>Utilizar uma configuração de DSC

1. Abra Olá ISE do PowerShell como administrador num computador do ambiente local. máquina Olá tem de ter a versão mais recente do Olá do [WMF 5](http://aka.ms/wmf5latest) instalado.
2. Copie Olá seguir o script localmente. Este script contém uma configuração de DSC do PowerShell para criar metaconfigurations e tookick um comando desativar a criação de configuração meta Olá.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Preencha chave de registo Olá e o URL para a sua conta de automatização, bem como os nomes de Olá de Olá máquinas tooonboard. Todos os outros parâmetros são opcionais. toofind Olá chave e o registo do URL de registo para a sua conta de automatização, consulte Olá [ **Secure registo** ](#secure-registration) secção abaixo.
4. Se pretender Olá máquinas tooreport DSC Estado informações tooAzure DSC de automatização, mas não solicitar a configuração ou de módulos do PowerShell, defina Olá **ReportOnly** tootrue de parâmetro.
5. Execute script de Olá. Agora, deve ter uma pasta denominada **DscMetaConfigs** no seu diretório de trabalho, que contém Olá PowerShell DSC metaconfigurations para Olá máquinas tooonboard (como administrador):

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Utilizar cmdlets de automatização do Azure Olá

Se as predefinições do Gestor de configuração Local do PowerShell DSC de Olá corresponder ao seu caso de utilização e pretende tooonboard máquinas para que possam tanto solicitar a partir e comunicam tooAzure DSC de automatização, Olá cmdlets de automatização do Azure fornecem um método simplificado de gerar Olá DSC metaconfigurations necessário:

1. Abra a consola do PowerShell Olá ou o ISE do PowerShell como administrador numa máquina no seu ambiente local.
2. Ligar através do Gestor de recursos de tooAzure **Add-AzureRmAccount**
3. Transferir Olá PowerShell DSC metaconfigurations para máquinas de Olá pretende tooonboard de Olá automatização conta toowhich pretende tooonboard nós:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. Agora, deve ter uma pasta denominada ***DscMetaConfigs***, que contém Olá PowerShell DSC metaconfigurations para Olá máquinas tooonboard (como administrador):
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Registo seguro

Máquinas podem integrar com segurança tooan conta de automatização do Azure através do protocolo de registo do Olá WMF 5 DSC, que permite que um nó tooauthenticate tooa PowerShell DSC V2 solicitar ou relatórios servidor DSC (incluindo o Automation DSC do Azure). nó Olá regista o servidor de toohello num **URL de registo**, autenticação utilizando um **chave de registo**. Durante o registo no nó de Olá DSC e servidor de solicitação do DSC/relatórios negociar um certificado exclusivo para este toouse do nó para autenticação toohello pós-o registo do servidor. Este processo impede que nós de integrado de representar um que outro, por exemplo, se um nó for comprometido e comportam de forma maliciosa. Após o registo, a chave de registo Olá não é utilizado para autenticação novamente e é eliminado do nó de Olá.

Pode obter informações de Olá necessárias para o protocolo de registo de Olá DSC de Olá **gerir chaves** painel no portal de pré-visualização do Azure Olá. Abrir este painel clicando no ícone chave Olá no Olá **Essentials** painel para Olá conta de automatização.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* URL de registo é o campo de URL de Olá no painel de gerir chaves de Olá.
* Chave de registo é Olá chave de acesso primária ou secundária a chave de acesso no painel de gerir chaves de Olá. A chave pode ser utilizada.

Para segurança adicional, chaves de acesso primária e secundária Olá de uma conta de automatização podem ser novamente geradas em qualquer altura (no Olá **gerir chaves** painel) registos de nó futuras tooprevent utilizando chaves anteriores.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Resolução de problemas de integração da máquina virtual do Azure

Automation DSC do Azure permite-lhe facilmente Windows VMs do Azure para gestão de configuração. Definições avançadas de Olá, Olá extensão de configuração de estado pretendido do Azure VM é utilizada tooregister Olá VM com o Automation DSC do Azure. Uma vez que Olá extensão de configuração de estado pretendido do Azure VM é executado no modo assíncrono, ao controlar o progresso e a execução de resolução de problemas podem ser importantes.

> [!NOTE]
> Qualquer método de integração tooAzure uma VM do Windows Azure Automation DSC que utiliza a extensão de configuração de estado pretendido do Azure VM Olá pode demorar até tooan hora para Olá nó tooshow cópias de segurança, tal como registado na automatização do Azure. Isto acontece devido toohello instalação do Windows Management Framework 5.0 Olá VM pela extensão de DSC da VM do Azure Olá, que é necessário tooonboard Olá VM tooAzure DSC de automatização.

Estado de Olá tootroubleshoot ou de vista de Olá extensão de configuração de estado pretendido do Azure VM, no portal do Azure de Olá navegue toohello VM que está a ser integrado, em seguida, clique em->- **todas as definições** -> **extensões**   ->  **DSC**. Para obter mais detalhes, pode clicar em **ver o estado detalhado**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Expiração do certificado e o novo registo

Depois de registar uma máquina como um nó de DSC no Automation DSC do Azure, existem vários motivos por que razão poderá ser necessário tooreregister esse nó Olá futura:

* Depois de registar, cada nó negoceia automaticamente um certificado exclusivo para a autenticação expira após um ano. Atualmente, Olá protocolo de registo do PowerShell DSC não é possível renovar automaticamente certificados quando estes estão prestes a expirar, por isso terá de nós de Olá tooreregister após o tempo de um ano. Antes de ao registar novamente, certifique-se de que cada nó está a executar Windows Management Framework 5.0 RTM. Se o certificado de autenticação de um nó expira e nó Olá não é reregistered, nó Olá toocommunicate não é possível com a automatização do Azure e será marcado como 'Unresponsive.' O novo registo efetuada 90 dias ou menor da hora de expiração do certificado hello, ou em qualquer momento após a hora de expiração do certificado de Olá, irá resultar num novo certificado a ser gerado e utilizado.
* toochange qualquer [valores de Gestor de configuração Local do PowerShell DSC](https://msdn.microsoft.com/powershell/dsc/metaconfig4) que foram definidas durante o registo inicial do nó de Olá, tais como ConfigurationMode. Atualmente, estes valores de agente do DSC só podem ser alterados através do novo registo. uma exceção de Olá é Olá configuração do nó atribuído nó toohello – Isto pode ser alterado no Automation DSC do Azure diretamente.

O novo registo pode ser efetuado no Olá mesma forma que registou nó Olá inicialmente, utilizando qualquer um dos métodos de integração de Olá descrita neste documento. Não é necessário toounregister um nó do DSC da automatização do Azure antes de ao registar novamente-lo.

## <a name="related-articles"></a>Artigos relacionados

* [Descrição geral do DSC da automatização do Azure](automation-dsc-overview.md)
* [Cmdlets do DSC da automatização do Azure](/powershell/module/azurerm.automation/#automation)
* [Preços do DSC da automatização do Azure](https://azure.microsoft.com/pricing/details/automation/)
