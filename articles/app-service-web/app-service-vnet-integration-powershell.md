---
title: "aaaConnect aplicação tooyour rede virtual com o PowerShell"
description: "Instruções sobre como tooconnect tooand trabalhar com redes virtuais utilizando o PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Ligar a sua rede virtual de tooyour de aplicação utilizando o PowerShell
## <a name="overview"></a>Descrição geral
No App Service do Azure, pode ligar-se a aplicação (web, móveis ou API) tooan rede virtual do Azure (VNet) na sua subscrição. Esta funcionalidade é denominada a integração de VNet. a funcionalidade de integração de VNet Olá não deve ser confundida com funcionalidade de ambiente de serviço de aplicações de Olá, permitindo-lhe toorun uma instância do App Service do Azure na sua rede virtual.

a funcionalidade de integração de VNet Olá tem uma interface de utilizador (IU) do novo portal de Olá que pode utilizar toointegrate com redes virtuais que são implementadas utilizando o modelo de implementação clássica Olá ou modelo de implementação Azure Resource Manager Olá. Se pretender toolearn mais informações sobre a funcionalidade de Olá, veja [integrar a sua aplicação com uma Azure virtual network](web-sites-integrate-with-vnet.md).

Este artigo é não sobre como toouse Olá IU mas em vez disso, sobre como tooenable integração com o PowerShell. Porque os comandos de Olá para cada modelo de implementação forem diferentes, este artigo tem uma secção para cada modelo de implementação.  

Antes de continuar com este artigo, certifique-se de que tem:

* Olá que Azure PowerShell SDK mais recente instalada. Pode instalá-lo com Olá instalador de plataforma Web.
* Uma aplicação no serviço de aplicações do Azure em execução num padrão ou Premium SKU.

## <a name="classic-virtual-networks"></a>Redes virtuais clássicas
Esta secção explica três tarefas para as redes virtuais que utilizam o modelo de implementação clássica Olá:

1. Ligar a sua aplicação tooa pré-existentes rede virtual que tem um gateway e está configurado para a conetividade ponto a site.
2. Atualize as informações de integração de rede virtual para a sua aplicação.
3. Desligue a sua aplicação da sua rede virtual.

### <a name="connect-an-app-tooa-classic-vnet"></a>Ligar uma aplicação tooa VNet clássica
tooconnect uma aplicação tooa rede virtual, siga estes três passos:

1. Declare toohello web aplicação que irá associar uma rede virtual específico. aplicação Olá irá gerar um certificado que irá receber toohello de rede virtual para a conetividade ponto a site.
2. Carregar Olá web app certificado toohello rede virtual e, em seguida, obter o pacote de VPN de ponto a site Olá URI.
3. Atualize a ligação de rede virtual da aplicação web Olá com o URI do pacote de ponto a site Olá.

Olá primeiro e terceiro passos são totalmente passível de ter scripts, mas o segundo passo de Olá requer uma ação única, manual através do portal Olá ou acesso tooperform **colocar** ou **PATCH** ações na rede virtual Olá Ponto final do Gestor de recursos do Azure. Contacte o suporte do Azure toohave esta opção ativada. Antes de começar, certifique-se de que tem uma rede virtual clássica que tem conetividade ponto a site já ativada e um gateway implementado. toocreate Olá gateway e ativar ponto a site conectividade, tem de portal de Olá toouse conforme descrito em [criar um gateway VPN][createvpngateway].

Olá clássico rede virtual tem de toobe Olá mesma subscrição que o serviço de aplicações planear essa aplicação Olá contém que está a integrar.

##### <a name="set-up-azure-powershell-sdk"></a>Configurar o Azure PowerShell SDK
Abra uma janela do PowerShell e configurar a sua conta do Azure e subscrição utilizando:

    Login-AzureRmAccount

Esse comando irá abrir uma linha de comandos tooget as suas credenciais do Azure. Depois de iniciar sessão, tem de utilizar uma das Olá subscrição Olá tooselect de comandos que pretende que o toouse a seguir. Certifique-se de que está a utilizar subscrição Olá destinadas a sua rede virtual e o plano de serviço aplicacional no.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

ou

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variáveis utilizadas neste artigo
os comandos toosimplify, iremos irá definir um **$Configuration** variável do PowerShell com uma configuração especial Olá.

Defina uma variável da seguinte forma no PowerShell com Olá os seguintes parâmetros:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

localização da aplicação Olá deve ser uma localização de Olá sem quaisquer espaços. Por exemplo, EUA oeste é westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

Olá o item seguinte é onde o certificado de Olá deve ser escrito. Deve ser um caminho gravável no seu computador local. Certifique-se de que tooinclude. cer no fim de Olá.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee que definir, tipo **$Configuration**.

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

rest Olá desta secção assume que tem uma variável criada como descrito apenas.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Declarar Olá rede virtual toohello aplicação
Utilize Olá seguir comando tootell Olá aplicação que irá utilizar esta rede virtual específico. Isto fará com que Olá aplicação toogenerate certificados necessários:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Se este comando for bem sucedida, **$vnet** deve ter um **propriedades** variável na mesma. Olá **propriedades** variável deve conter ambos um certificado thumbprint e Olá dados do certificado.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Carregar Olá web app certificado toohello rede virtual
Uma manual, único passo é necessário para cada subscrição e a combinação de rede virtual. Ou seja, se estiver a ligar aplicações na subscrição A tooVirtual rede A, terá de toodo este passo apenas assim, independentemente da forma como muitas aplicações que configurar. Se estiver a adicionar uma nova rede virtual de tooanother de aplicação, terá de voltar toodo. motivo de Olá para isto é que um conjunto de certificados é gerado um nível de subscrição no App Service do Azure e o conjunto de Olá é gerado uma vez para cada rede virtual que Olá aplicações estabelecerão ligação ao.

Olá certificados serão já foram definidos se seguido estes passos ou se integrado Olá mesma rede virtual com portal Olá.

Step-by-Olá primeiro passo é o ficheiro do toogenerate Olá. cer. Step-by-Olá segundo passo é tooupload Olá. cer ficheiro tooyour rede virtual. ficheiro. cer de Olá de toogenerate da chamada de API de Olá no Olá passo anterior, execute os seguintes comandos de Olá.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

certificado de Olá irá ser encontrado na localização de Olá que **$Configuration.GeneratedCertificatePath** especifica.

certificado de Olá tooupload manualmente, utilize Olá [portal do Azure] [ azureportal] e **procurar (Virtual Network clássica)** > **deligaçõesdeVPN**  >  **Ponto a site** > **gerir certificados**. Aqui, carregue o certificado.

##### <a name="get-hello-point-to-site-package"></a>Obter o pacote do ponto a site Olá
Olá próximo passo como configurar uma ligação de rede virtual numa aplicação web é tooget Olá ponto a site pacote e fornecê-lo tooyour web app.

Guarde Olá seguintes modelo tooa ficheiro chamado GetNetworkPackageUri.json algures no seu computador, por exemplo, C:\Azure\Templates\GetNetworkPackageUri.json.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


Definir os parâmetros de entrada:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Chamada Olá script:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


variável de Olá **$output. Outputs.packageUri** agora irá conter Olá pacote URI toobe fornecido tooyour web app.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Carregar Olá ponto a site pacote tooyour aplicação
passo final Olá é tooprovide Olá aplicação com este pacote. Basta executar o comando seguinte Olá:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Se uma mensagem pede-lhe tooconfirm que estiver a substituir um recurso existente, certifique-se de que tooallow-lo.

Depois deste comando for bem sucedida, a aplicação deve ser ligado toohello rede virtual. sucesso tooconfirm, aceda a consola de aplicação tooyour e escreva Olá seguinte:

    SET WEBSITE_

Se existir uma variável de ambiente chamada WEBSITE_VNETNAME que tem um valor que corresponde ao nome de Olá da rede virtual de destino Olá, todas as configurações de êxito.

### <a name="update-classic-vnet-integration-information"></a>Atualizar informações de integração de VNet clássicas
tooupdate ou ressincronizar as suas informações, basta repetir os passos de Olá que seguiu quando criou a integração de Olá assegurados primeiro Olá. Esses passos são:

1. Defina as informações de configuração.
2. Declare Olá rede virtual toohello aplicação.
3. Obter o pacote de ponto a site Olá.
4. Carregar Olá ponto a site pacote tooyour aplicação.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Desligue a aplicação uma VNet clássica
toodisconnect Olá aplicação, precisa de informações de configuração de Olá que foi definidas durante a integração de rede virtual. Utilizar essas informações, há, em seguida, de um comando toodisconnect a aplicação da sua rede virtual.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Redes virtuais do Gestor de recursos
Redes virtuais do Gestor de recursos tem APIs do Azure Resource Manager, que simplificar algumas processos quando comparados com redes virtuais clássicas. Temos um script que irá ajudar a concluir Olá seguintes tarefas:

* Criar uma rede virtual do Gestor de recursos e integrar a sua aplicação com o mesmo.
* Criar um gateway, configure a conetividade ponto a site numa rede virtual do Resource Manager pré-existentes e, em seguida, integrar a sua aplicação com o mesmo.
* Integre a aplicação com uma pré-existentes rede virtual do Gestor de recursos que tem um gateway e ativar a conetividade ponto a site.
* Desligue a sua aplicação da sua rede virtual.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script de integração de serviço de aplicações de VNet do Resource Manager
Copie Olá seguinte script e guarde-o ficheiro de tooa. Se não quiser que o script de Olá toouse, sentir toolearn livre do mesmo toosee como coisas tooset cópias de segurança com uma rede virtual do Gestor de recursos.

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

Guarde uma cópia do script Olá. Neste artigo, é denominado V2VnetAllinOne.ps1, mas pode utilizar outro nome. Não existem sem argumentos para este script. Pode simplesmente executá-la. Olá primeiro thing script Olá executará está a solicitar-lhe toosign no. Depois de iniciar sessão, o script de Olá obtém os detalhes sobre a sua conta e devolve uma lista de subscrições. Sem contar pedido Olá as suas credenciais, execução de script inicial Olá este aspeto:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Demonstração de subscrição (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) Teste MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Subscrição de demonstração roxa (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Escolher uma opção: 3

    Conta: ccompy@microsoft.com ambiente: subscrição AzureCloud: inquilino 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d: 722278f-fef1-499f-91ab-2323d011db47

    Introduza Olá grupo de recursos da sua aplicação: hcdemo rg introduza Olá nome da sua aplicação: v2vnetpowershell o que fazer pretende toodo?

    1) Adicionar uma aplicação de tooan nova rede Virtual
    2) Adicionar uma aplicação de tooan de rede Virtual existente
    3) Remover uma rede Virtual a partir de uma aplicação

Olá resto esta secção explica cada uma dessas três opções.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Criar uma VNet do Resource Manager e integrar com o mesmo
Selecione uma nova rede virtual que utiliza Olá modelo de implementação do Resource Manager e integrá-lo com a sua aplicação, de toocreate **1) adicionar uma nova rede Virtual de tooan aplicação**. Esta ação irá solicitar-nome Olá da rede virtual Olá. A minha caso, como pode ver no Olá definições, os seguintes utilizei nome Olá, v2pshell.

script de Olá fornece detalhes de Olá sobre Olá de rede virtual está a ser criada. Se as pretendo, pode alterar qualquer um dos valores de Olá Na execução deste exemplo, criar uma rede virtual que tenha Olá seguintes definições:

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

Se quiser toochange qualquer um dos valores de Olá, escreva **Y** e efetuar alterações de Olá. Quando estiver satisfeito com as definições de rede virtual Olá, escreva **N** ou simplesmente prima Enter quando lhe for pedido sobre como alterar as definições de Olá. A partir daí no até conclusão, o script de Olá informará alguns dos qual it' i's fazer antes de iniciar o gateway de rede virtual toocreate Olá. Esse passo pode demorar até tooan hora. Não existe nenhum indicador de progresso durante esta fase, mas script Olá irá informá-lo a quando gateway Olá foi criado.

Quando termina o script de Olá, irá indicar **concluído**. Neste momento, terá de uma rede virtual do Gestor de recursos com o nome de Olá e definições que selecionou. Esta nova rede virtual também será integrada com a sua aplicação.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Integrar a sua aplicação com uma VNet do Resource Manager pré-existentes
Quando estiver a integrar uma rede virtual preexistentes, se fornecer uma Gestor de recursos de rede virtual não tem um gateway ou a conetividade ponto a site, Olá será definido o script que cópias de segurança. Se Olá VNET já essas ações configurar, o script de Olá fica toohello direitas integração de aplicações. toostart este processo, basta selecionar **2) adicione tooan uma rede Virtual existente aplicação**.

Esta opção só funciona se tiver uma pré-existentes rede virtual do Gestor de recursos que está a ser Olá mesma subscrição que a sua aplicação. Depois de selecionar a opção de Olá, será apresentada uma lista de redes virtuais do Resource Manager.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Escolher uma opção: 5

Selecione simplesmente Olá de rede virtual pretende toointegrate com. Se já tiver um gateway que tem conetividade ponto a site ativada, o script de Olá simplesmente integrar a aplicação com a sua rede virtual. Se não tiver um gateway, terá de sub-rede do gateway toospecify Olá. A sub-rede do gateway tem de estar no seu espaço de endereços de rede virtual e não pode ser qualquer outra sub-rede. Se tiver uma rede virtual sem um gateway e execute este passo, coisas este aspeto:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

Neste exemplo, criar um gateway de rede virtual que tenha Olá seguintes definições:

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

Se quiser toochange qualquer um dessas definições, pode fazê. Caso contrário, prima Enter e script Olá irá criar o gateway e anexar a rede virtual do tooyour de aplicação. hora de criação do gateway Olá ainda é uma hora, embora, por isso, certifique-se de que que tenha em atenção. Quando tudo estiver concluído, o script de Olá indicará **concluído**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Desligar a aplicação a partir de uma VNet do Resource Manager
A aplicação da sua rede virtual não tirá gateway Olá ou desativar a conetividade ponto a site. Pode, após todos os, estar a utilizar, de outra coisa. -Também não desligue-o de todas as outras aplicações que não sejam Olá um fornecida. tooperform esta ação, selecione **3) remover uma rede Virtual a partir de uma aplicação**. Quando o fizer, verá algo semelhante ao seguinte:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Embora o script de Olá indica eliminar, não elimina a rede virtual Olá. Apenas é a remoção integração Olá. Depois de confirmar que este é o que pretende toodo, o comando de Olá é processado bastante rapidamente e indica **verdadeiro** quando é efetuada.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
