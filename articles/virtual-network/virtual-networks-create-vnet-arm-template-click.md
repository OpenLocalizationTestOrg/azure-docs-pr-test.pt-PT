---
title: aaaCreate uma rede virtual | Modelo Azure Resource Manager | Microsoft Docs
description: Saiba como toocreate a virtual rede utilizando um modelo Azure Resource Manager.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="ac6ae-103">Criar uma rede virtual com um modelo Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ac6ae-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="ac6ae-104">O Azure tem dois modelos de implementação: a implementação do Azure Resource Manager e a implementação clássica.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ac6ae-105">A Microsoft recomenda a criação de recursos através do modelo de implementação do Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="ac6ae-106">mais informações sobre como toolearn Olá diferenças entre os modelos de Olá dois ler Olá [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="ac6ae-107">Este artigo explica como toocreate uma VNet através da implementação do Resource Manager Olá modelo utilizando um modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="ac6ae-108">Também pode criar uma VNet através do Resource Manager utilizando outras ferramentas ou criar uma VNet através do modelo de implementação clássica Olá selecionando uma opção diferente de Olá lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="ac6ae-109">Portal</span><span class="sxs-lookup"><span data-stu-id="ac6ae-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="ac6ae-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac6ae-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="ac6ae-111">CLI</span><span class="sxs-lookup"><span data-stu-id="ac6ae-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="ac6ae-112">Modelo</span><span class="sxs-lookup"><span data-stu-id="ac6ae-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="ac6ae-113">Portal (Clássico)</span><span class="sxs-lookup"><span data-stu-id="ac6ae-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="ac6ae-114">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="ac6ae-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="ac6ae-115">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="ac6ae-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="ac6ae-116">Ficará a saber como toodownload e modificar existente modelo ARM a partir do GitHub e implementar a modelo de Olá a partir do GitHub, PowerShell e Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="ac6ae-117">Se estiver a implementar modelo ARM Olá diretamente a partir do GitHub, sem quaisquer alterações, avance demasiado[implementar um modelo a partir do github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="ac6ae-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="ac6ae-118">Transferir e compreender o modelo do Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="ac6ae-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="ac6ae-119">Pode transferir Olá modelo existente para criar uma VNet e duas sub-redes a partir do GitHub, efetuar quaisquer alterações que pretender e reutilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="ac6ae-120">por isso, de toodo concluir Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="ac6ae-121">Navegue demasiado[página do modelo de exemplo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="ac6ae-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="ac6ae-122">Clique em **azuredeploy.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="ac6ae-123">Guarde Olá ficheiro tooa uma pasta local no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="ac6ae-124">Se estiver familiarizado com modelos, avance toostep 7.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="ac6ae-125">Abra o ficheiro Olá que guardou e observe Olá conteúdo em **parâmetros** na linha 5.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="ac6ae-126">Os parâmetros do modelo ARM fornecem um marcador de posição para valores que podem ser preenchidos durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="ac6ae-127">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="ac6ae-127">Parameter</span></span> | <span data-ttu-id="ac6ae-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac6ae-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="ac6ae-129">**localização**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-129">**location**</span></span> |<span data-ttu-id="ac6ae-130">Região do Azure onde será criada Olá VNet</span><span class="sxs-lookup"><span data-stu-id="ac6ae-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="ac6ae-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-131">**vnetName**</span></span> |<span data-ttu-id="ac6ae-132">Nome para Olá nova VNet</span><span class="sxs-lookup"><span data-stu-id="ac6ae-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="ac6ae-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-133">**addressPrefix**</span></span> |<span data-ttu-id="ac6ae-134">Espaço de endereços de Olá VNet, no formato CIDR</span><span class="sxs-lookup"><span data-stu-id="ac6ae-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="ac6ae-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-135">**subnet1Name**</span></span> |<span data-ttu-id="ac6ae-136">Nome para Olá primeira VNet</span><span class="sxs-lookup"><span data-stu-id="ac6ae-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="ac6ae-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-137">**subnet1Prefix**</span></span> |<span data-ttu-id="ac6ae-138">Bloco CIDR da sub-rede primeiro Olá</span><span class="sxs-lookup"><span data-stu-id="ac6ae-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="ac6ae-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-139">**subnet2Name**</span></span> |<span data-ttu-id="ac6ae-140">Nome para Olá segunda VNet</span><span class="sxs-lookup"><span data-stu-id="ac6ae-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="ac6ae-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="ac6ae-141">**subnet2Prefix**</span></span> |<span data-ttu-id="ac6ae-142">Bloco CIDR da sub-rede segundo Olá</span><span class="sxs-lookup"><span data-stu-id="ac6ae-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="ac6ae-143">Os modelos Azure Resource Manager mantidos no GitHub podem ser alterados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="ac6ae-144">Certifique-se que verifique o modelo de Olá antes de o utilizar.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="ac6ae-145">Verifique o conteúdo de Olá em **recursos** e tenha em atenção o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="ac6ae-146">**tipo**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-146">**type**.</span></span> <span data-ttu-id="ac6ae-147">Tipo de recurso a ser criado pelo modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="ac6ae-148">Neste caso, **Microsoft.Network/virtualNetworks**, que representa uma VNet.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="ac6ae-149">**nome**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-149">**name**.</span></span> <span data-ttu-id="ac6ae-150">Nome do recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-150">Name for hello resource.</span></span> <span data-ttu-id="ac6ae-151">Utilização de Olá de aviso de **[parameters('vnetName')]**, que significa Olá será nome fornecido como entrada pelo utilizador Olá ou um ficheiro de parâmetros durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="ac6ae-152">**propriedades**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-152">**properties**.</span></span> <span data-ttu-id="ac6ae-153">Lista de propriedades para o recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-153">List of properties for hello resource.</span></span> <span data-ttu-id="ac6ae-154">Este modelo utiliza as propriedades de espaço e a sub-rede de endereços de Olá durante a criação da VNet.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="ac6ae-155">Navegue para trás demasiado[página do modelo de exemplo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="ac6ae-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="ac6ae-156">Clique em **azuredeploy-paremeters.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="ac6ae-157">Guarde Olá ficheiro tooa uma pasta local no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="ac6ae-158">Abra o ficheiro Olá que guardou e edite Olá os valores de parâmetros de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="ac6ae-159">Utilize Olá valores abaixo toodeploy Olá VNet descrita no cenário de Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="ac6ae-160">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="ac6ae-161">Implementar a modelo Olá através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac6ae-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="ac6ae-162">Conclua Olá seguir modelo Olá toodeploy de passos que transferiu com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="ac6ae-163">Instalar e configurar o Azure PowerShell, efetuando os passos de Olá Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="ac6ae-164">Execute Olá toocreate de comando a seguir um novo grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="ac6ae-165">comando de Olá cria um grupo de recursos denominado *TestRG* no Olá *EUA Central* região do azure.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="ac6ae-166">Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac6ae-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="ac6ae-167">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="ac6ae-168">Execute os seguintes comandos toodeploy Olá nova VNet com Olá parâmetros de modelo e os ficheiros que transferiu e alterou acima de Olá:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="ac6ae-169">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="ac6ae-170">Seguinte Olá executar comando Propriedades de Olá tooview de Olá nova VNet:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="ac6ae-171">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="ac6ae-172">Implementar a modelo Olá utilizando clique para implementar</span><span class="sxs-lookup"><span data-stu-id="ac6ae-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="ac6ae-173">Pode reutilizar predefinido do Azure Resource Manager modelos tooa carregado repositório GitHub mantido pela Microsoft e da Comunidade de toohello aberta.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="ac6ae-174">Estes modelos podem ser implementados diretamente do GitHub ou transferidos e modificados toofit às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="ac6ae-175">toodeploy um modelo que cria uma VNet com duas sub-redes, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="ac6ae-176">Num browser, navegue demasiado[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="ac6ae-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="ac6ae-177">Desloque para baixo a lista de Olá de modelos e clique em **101 vnet-two subnets**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="ac6ae-178">Verifique Olá **README.md** ficheiro, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-178">Check hello **README.md** file, as shown below.</span></span>

    ![Ficheiro READEME.md no github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="ac6ae-180">Clique em **implementar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="ac6ae-181">Se necessário, introduza as suas credenciais de início de sessão do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="ac6ae-182">No Olá **parâmetros** painel, introduza valores Olá pretende toouse toocreate sua nova VNet e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="ac6ae-183">Olá figura seguinte mostra os valores de Olá para o cenário de Olá:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Parâmetros do modelo ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="ac6ae-185">Clique em **grupo de recursos** e selecione um tooadd do grupo de recursos Olá VNet ou clique em **criar nova** tooadd Olá VNet tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="ac6ae-186">Olá figura seguinte mostra Olá recursos definições de grupo para um novo grupo de recursos chamado **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Grupo de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="ac6ae-188">Se necessário, altere Olá **subscrição** e **localização** definições para a sua VNet.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="ac6ae-189">Se não quiser toosee Olá VNet como um mosaico no Olá **Startboard**, desativar **Pin tooStartboard**.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="ac6ae-190">Clique em **termos legais**, Olá termos de licenciamento e clique em **comprar** tooagree.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="ac6ae-191">Clique em **criar** toocreate Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Mosaico Submeter implementação no portal de pré-visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="ac6ae-193">Após a conclusão da implementação de Olá, no Olá portal do Azure clique **mais serviços**, tipo *redes virtuais* na caixa de filtro de Olá que aparece, em seguida, clique em Painel de redes de Virtual de Olá toosee redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="ac6ae-194">No painel de Olá, clique em *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="ac6ae-195">No Olá *TestVNet* painel, clique em **sub-redes** toosee Olá criada sub-redes, conforme mostrado no Olá seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Criar a VNet no portal de pré-visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="ac6ae-197">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ac6ae-197">Next steps</span></span>

<span data-ttu-id="ac6ae-198">Saiba como tooconnect:</span><span class="sxs-lookup"><span data-stu-id="ac6ae-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="ac6ae-199">Uma rede virtual máquina virtual (VM) tooa por ler Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [criar uma VM com Linux](../virtual-machines/linux/quick-create-portal.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="ac6ae-200">Em vez de criar uma VNet e sub-rede nos passos de Olá dos artigos Olá, pode selecionar uma VNet existente e sub-rede tooconnect uma VM.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="ac6ae-201">Olá, redes virtuais de tooother de rede virtual através da leitura Olá [ligar VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="ac6ae-202">Olá rede virtual tooan rede no local através de um site para site rede privada virtual (VPN) ou um circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="ac6ae-203">Saiba como. o lendo Olá [ligar uma rede no local do VNet tooan usando uma VPN de site para site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [ligação tooan uma VNet circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="ac6ae-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
