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
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Criar uma rede virtual com um modelo Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

O Azure tem dois modelos de implementação: a implementação do Azure Resource Manager e a implementação clássica. A Microsoft recomenda a criação de recursos através do modelo de implementação do Resource Manager Olá. mais informações sobre como toolearn Olá diferenças entre os modelos de Olá dois ler Olá [modelos de implementação do Azure compreender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.
 
Este artigo explica como toocreate uma VNet através da implementação do Resource Manager Olá modelo utilizando um modelo Azure Resource Manager. Também pode criar uma VNet através do Resource Manager utilizando outras ferramentas ou criar uma VNet através do modelo de implementação clássica Olá selecionando uma opção diferente de Olá lista a seguir:

> [!div class="op_single_selector"]
- [Portal](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [Modelo](virtual-networks-create-vnet-arm-template-click.md)
- [Portal (Clássico)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (Clássico)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI (Clássica)](virtual-networks-create-vnet-classic-cli.md)

Ficará a saber como toodownload e modificar existente modelo ARM a partir do GitHub e implementar a modelo de Olá a partir do GitHub, PowerShell e Olá CLI do Azure.

Se estiver a implementar modelo ARM Olá diretamente a partir do GitHub, sem quaisquer alterações, avance demasiado[implementar um modelo a partir do github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Transferir e compreender o modelo do Azure Resource Manager Olá
Pode transferir Olá modelo existente para criar uma VNet e duas sub-redes a partir do GitHub, efetuar quaisquer alterações que pretender e reutilizá-lo. por isso, de toodo concluir Olá os seguintes passos:

1. Navegue demasiado[página do modelo de exemplo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Clique em **azuredeploy.json** e em **RAW**.
3. Guarde Olá ficheiro tooa uma pasta local no seu computador.
4. Se estiver familiarizado com modelos, avance toostep 7.
5. Abra o ficheiro Olá que guardou e observe Olá conteúdo em **parâmetros** na linha 5. Os parâmetros do modelo ARM fornecem um marcador de posição para valores que podem ser preenchidos durante a implementação.
   
   | Parâmetro | Descrição |
   | --- | --- |
   | **localização** |Região do Azure onde será criada Olá VNet |
   | **vnetName** |Nome para Olá nova VNet |
   | **addressPrefix** |Espaço de endereços de Olá VNet, no formato CIDR |
   | **subnet1Name** |Nome para Olá primeira VNet |
   | **subnet1Prefix** |Bloco CIDR da sub-rede primeiro Olá |
   | **subnet2Name** |Nome para Olá segunda VNet |
   | **subnet2Prefix** |Bloco CIDR da sub-rede segundo Olá |
   
   > [!IMPORTANT]
   > Os modelos Azure Resource Manager mantidos no GitHub podem ser alterados ao longo do tempo. Certifique-se que verifique o modelo de Olá antes de o utilizar.
   > 
   > 
6. Verifique o conteúdo de Olá em **recursos** e tenha em atenção o seguinte Olá:
   
   * **tipo**. Tipo de recurso a ser criado pelo modelo de Olá. Neste caso, **Microsoft.Network/virtualNetworks**, que representa uma VNet.
   * **nome**. Nome do recurso de Olá. Utilização de Olá de aviso de **[parameters('vnetName')]**, que significa Olá será nome fornecido como entrada pelo utilizador Olá ou um ficheiro de parâmetros durante a implementação.
   * **propriedades**. Lista de propriedades para o recurso de Olá. Este modelo utiliza as propriedades de espaço e a sub-rede de endereços de Olá durante a criação da VNet.
7. Navegue para trás demasiado[página do modelo de exemplo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Clique em **azuredeploy-paremeters.json** e em **RAW**.
9. Guarde Olá ficheiro tooa uma pasta local no seu computador.
10. Abra o ficheiro Olá que guardou e edite Olá os valores de parâmetros de Olá. Utilize Olá valores abaixo toodeploy Olá VNet descrita no cenário de Olá os seguintes:

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

11. Guarde o ficheiro de Olá.


## <a name="deploy-hello-template-using-powershell"></a>Implementar a modelo Olá através do PowerShell

Conclua Olá seguir modelo Olá toodeploy de passos que transferiu com o PowerShell:

1. Instalar e configurar o Azure PowerShell, efetuando os passos de Olá Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. Execute Olá toocreate de comando a seguir um novo grupo de recursos:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    comando de Olá cria um grupo de recursos denominado *TestRG* no Olá *EUA Central* região do azure. Para obter mais informações sobre os grupos de recursos, veja [Descrição Geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    Resultado esperado:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Execute os seguintes comandos toodeploy Olá nova VNet com Olá parâmetros de modelo e os ficheiros que transferiu e alterou acima de Olá:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Resultado esperado:
   
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
4. Seguinte Olá executar comando Propriedades de Olá tooview de Olá nova VNet:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Resultado esperado:

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

## <a name="deploy-hello-template-using-click-to-deploy"></a>Implementar a modelo Olá utilizando clique para implementar

Pode reutilizar predefinido do Azure Resource Manager modelos tooa carregado repositório GitHub mantido pela Microsoft e da Comunidade de toohello aberta. Estes modelos podem ser implementados diretamente do GitHub ou transferidos e modificados toofit às suas necessidades. toodeploy um modelo que cria uma VNet com duas sub-redes, Olá concluir os seguintes passos:

1. Num browser, navegue demasiado[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Desloque para baixo a lista de Olá de modelos e clique em **101 vnet-two subnets**. Verifique Olá **README.md** ficheiro, como mostrado abaixo.

    ![Ficheiro READEME.md no github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Clique em **implementar tooAzure**. Se necessário, introduza as suas credenciais de início de sessão do Azure. 
4. No Olá **parâmetros** painel, introduza valores Olá pretende toouse toocreate sua nova VNet e, em seguida, clique em **OK**. Olá figura seguinte mostra os valores de Olá para o cenário de Olá:
   
    ![Parâmetros do modelo ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Clique em **grupo de recursos** e selecione um tooadd do grupo de recursos Olá VNet ou clique em **criar nova** tooadd Olá VNet tooa novo grupo de recursos. Olá figura seguinte mostra Olá recursos definições de grupo para um novo grupo de recursos chamado **TestRG**:

    ![Grupo de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Se necessário, altere Olá **subscrição** e **localização** definições para a sua VNet.
7. Se não quiser toosee Olá VNet como um mosaico no Olá **Startboard**, desativar **Pin tooStartboard**.
8. Clique em **termos legais**, Olá termos de licenciamento e clique em **comprar** tooagree. 
9. Clique em **criar** toocreate Olá VNet.
   
    ![Mosaico Submeter implementação no portal de pré-visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Após a conclusão da implementação de Olá, no Olá portal do Azure clique **mais serviços**, tipo *redes virtuais* na caixa de filtro de Olá que aparece, em seguida, clique em Painel de redes de Virtual de Olá toosee redes virtuais. No painel de Olá, clique em *TestVNet*. No Olá *TestVNet* painel, clique em **sub-redes** toosee Olá criada sub-redes, conforme mostrado no Olá seguinte imagem:
    
     ![Criar a VNet no portal de pré-visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Passos seguintes

Saiba como tooconnect:

- Uma rede virtual máquina virtual (VM) tooa por ler Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [criar uma VM com Linux](../virtual-machines/linux/quick-create-portal.md) artigos. Em vez de criar uma VNet e sub-rede nos passos de Olá dos artigos Olá, pode selecionar uma VNet existente e sub-rede tooconnect uma VM.
- Olá, redes virtuais de tooother de rede virtual através da leitura Olá [ligar VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.
- Olá rede virtual tooan rede no local através de um site para site rede privada virtual (VPN) ou um circuito ExpressRoute. Saiba como. o lendo Olá [ligar uma rede no local do VNet tooan usando uma VPN de site para site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [ligação tooan uma VNet circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.
