---
title: "aaaConfigure um serviço de escuta do ILB Always On para grupos de disponibilidade no Azure | Microsoft Docs"
description: "Este tutorial utiliza recursos criados no modelo de implementação clássica Olá e cria uma escuta do grupo Always On disponibilidade no Azure que utiliza um balanceador de carga interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Configurar um serviço de escuta do ILB para grupos de disponibilidade Always On no Azure
> [!div class="op_single_selector"]
> * [Serviço de escuta interno](../classic/ps-sql-int-listener.md)
> * [Serviço de escuta externo](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Descrição geral

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [do Azure Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange a utilização de Olá do modelo de implementação clássica Olá. Recomendamos que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

tooconfigure um serviço de escuta para um grupo de disponibilidade Always On no modelo do Resource Manager Olá, consulte [configurar um balanceador de carga para um grupo de disponibilidade Always On no Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

O grupo de disponibilidade pode conter réplicas que são apenas no local ou para o Azure apenas, ou que abrangem no local e o Azure para configurações híbridas. As réplicas do Azure podem residir no Olá mesma região ou em várias regiões que utilizem várias redes virtuais. Olá procedimentos neste artigo partem do princípio de que já tem [configurado um grupo de disponibilidade](../classic/portal-sql-alwayson-availability-groups.md) , mas ainda não tiver configurado um serviço de escuta.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Diretrizes e limitações para os serviços de escuta internas
utilização Olá um balanceador de carga interno (ILB) com um serviço de escuta do grupo de disponibilidade no Azure é toohello requerente seguintes diretrizes:

* escuta do grupo de disponibilidade de hello é suportada no Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* Apenas uma escuta do grupo de disponibilidade interno é suportada para cada serviço em nuvem, porque o serviço de escuta de Olá é configurado toohello ILB, e não existe apenas um ILB para cada serviço em nuvem. No entanto, é possível toocreate vários serviços de escuta externos. Para obter mais informações, consulte [configurar um serviço de escuta externo para grupos de disponibilidade Always On no Azure](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinar a acessibilidade de Olá do serviço de escuta de Olá
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Este artigo foca-se sobre a criação de um serviço de escuta que utiliza um ILB. Se precisar de um serviço de escuta público ou externo, consulte a versão de Olá deste artigo que descreve a definição de segurança de um [escuta externa](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Criar os pontos finais VM com balanceamento de carga com direta do servidor retorno
Cria um ILB pela primeira vez ao executar o script de Olá posteriormente nesta secção.

Crie um ponto final com balanceamento de carga para cada VM que aloja uma réplica do Azure. Se tiver réplicas em várias regiões, cada réplica para essa região tem de ser Olá mesmo serviço de nuvem Olá mesma rede virtual do Azure. Criação de réplicas do grupo que abrangem várias regiões do Azure de disponibilidade necessita de configurar várias redes virtuais. Para obter mais informações sobre como configurar cruzada conectividade de rede virtual, consulte [configurar a conectividade de rede de toovirtual de rede virtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. No portal do Azure Olá, visite tooeach VM que aloja um detalhes da réplica tooview Olá.

2. Clique em Olá **pontos finais** separador para cada VM.

3. Certifique-se de que Olá **nome** e **Porta pública** do ponto final de serviço de escuta de Olá que pretende que sejam toouse ainda não estiverem em utilização. Exemplo de Olá nesta secção, é o nome de Olá *MyEndpoint*, e é a porta de Olá *1433*.

4. No seu cliente local, transfira e instale os mais recentes Olá [módulo do PowerShell](https://azure.microsoft.com/downloads/).

5. Inicie o PowerShell do Azure.  
    Abre uma nova sessão do PowerShell, com Olá Azure administrativos módulos carregados.

6. Execute `Get-AzurePublishSettingsFile`. Este cmdlet direciona toodownload de browser tooa um publicar definições ficheiro tooa diretório local. Pode ser pedido para as credenciais de início de sessão para a sua subscrição do Azure.

7. Execute o seguinte de Olá `Import-AzurePublishSettingsFile` comando com o caminho de Olá de Olá publicar o ficheiro de definições que transferiu a:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Depois de publicar Olá importado do ficheiro de definições, pode gerir a sua subscrição do Azure numa sessão do PowerShell de Olá.

8. Para *ILB*, atribuir um endereço IP estático. Examine a configuração de rede virtual atual Olá executando Olá os seguintes comandos:

        (Get-AzureVNetConfig).XMLConfiguration
9. Olá nota *sub-rede* nome para a sub-rede de Olá que contenha VMs Olá que alojam as réplicas de Olá. Este nome é utilizado no parâmetro Olá $SubnetName no script de Olá.

10. Olá nota *VirtualNetworkSite* name e Olá iniciar *AddressPrefix* para sub-rede Olá que contenha VMs Olá que alojam as réplicas de Olá. Procurar um endereço IP disponível através da transmissão de ambos os valores toohello `Test-AzureStaticVNetIP` comando e, examinando Olá *AvailableAddresses*. Por exemplo, se hello rede virtual é denominada *MyVNet* e tem um intervalo de endereços de sub-rede que inicia no *172.16.0.128*, seguinte Olá comando seria lista endereços disponíveis:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Selecione um dos endereços disponíveis Olá e utilizá-lo no parâmetro Olá $ILBStaticIP do script Olá no passo seguinte Olá.

12. Copiar Olá seguir o editor de texto de tooa de script do PowerShell e defina Olá valores das variáveis toosuit seu ambiente. As predefinições foram fornecidas para alguns parâmetros.  

    As implementações existentes que utilizam grupos de afinidade não é possível adicionar um ILB. Para obter mais informações sobre os requisitos do ILB, consulte [descrição geral do Balanceador de carga interno](../../../load-balancer/load-balancer-internal-overview.md).

    Além disso, se o grupo de disponibilidade abranger regiões do Azure, tem de executar o script de Olá uma vez cada centro de dados para o serviço em nuvem Olá e nós que residem em que Centro de dados.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Após definir variáveis de Olá, Olá cópia script de Olá texto editor tooyour PowerShell sessão toorun-lo. Se a linha de Olá continua a mostrar  **>>** , prima Enter novamente o script de Olá se toomake entra em execução.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Certifique-se de que KB2854082 está instalado, se necessário
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Abrir portas de firewall de Olá em nós do grupo de disponibilidade
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Criar a escuta do grupo de disponibilidade de Olá

Crie a escuta do grupo de disponibilidade de Olá em dois passos. Em primeiro lugar, crie o recurso de cluster de ponto de acesso de cliente de Olá e configurar as dependências. Segundo, configure os recursos do cluster Olá no PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Criar ponto de acesso de cliente Olá e configurar as dependências de cluster Olá
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurar recursos de cluster Olá no PowerShell
1. Para o ILB, tem de utilizar o endereço IP Olá Olá ILB criado anteriormente. tooobtain este IP abordar no PowerShell, Olá de utilização seguintes script:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Dos Olá VMs, copie o script do PowerShell de Olá para o seu editor de texto de tooa do sistema operativo e, em seguida, definir variáveis de Olá valores toohello que anotou anteriormente.

    Para o Windows Server 2012 ou posterior, utilize Olá seguintes script:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Para o Windows Server 2008 R2, utilize Olá seguintes script:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Depois de ter as variáveis de Olá conjunto, abra uma janela elevada do Windows PowerShell, colar Olá script de editor de texto Olá no seu toorun de sessão do PowerShell-lo. Se a linha de Olá continua a mostrar  **>>** , prima Enter novamente toomake certificar-se de que o script de Olá entra em execução.

4. Repita Olá precedente passos para cada VM.  
    Este script configura o recurso de endereço IP de Olá com o endereço IP Olá do serviço de nuvem Olá e define outros parâmetros, tais como a porta da sonda Olá. Quando o recurso de endereço IP de Olá seja colocado online, pode responder toohello consulta na porta de sonda de Olá Olá com balanceamento de carga ponto final de que criou anteriormente.

## <a name="bring-hello-listener-online"></a>Coloque online serviço de escuta de Olá
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Itens de seguimento
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Escuta do grupo de disponibilidade do teste Olá (Olá da mesma rede virtual)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
