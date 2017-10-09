---
title: "aaaConfigure um serviço de escuta externo para grupos de disponibilidade Always | Microsoft Docs"
description: "Este tutorial explica-lhe como Olá passos de criação de um sempre na disponibilidade escuta do grupo no Azure que está acessível externamente utilizando o endereço Virtual IP público do Olá o serviço de nuvem associada."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Configurar um serviço de escuta externo para grupos de disponibilidade Always no Azure
> [!div class="op_single_selector"]
> * [Serviço de escuta interno](../classic/ps-sql-int-listener.md)
> * [Serviço de escuta externo](../classic/ps-sql-ext-listener.md)
> 
> 

Este tópico mostra como tooconfigure um serviço de escuta para sempre no grupo de disponibilidade que está externamente acessível na Olá internet. Isto é possibilitado pela associação do serviço em nuvem Olá **IP Virtual público (VIP)** endereço com o serviço de escuta de Olá.

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

O grupo de disponibilidade pode conter réplicas que estão no local só, Azure apenas, ou span no local e o Azure para configurações híbridas. As réplicas do Azure podem residir no Olá mesma região ou em várias regiões com várias redes virtuais (VNets). passos de Olá abaixo partem do princípio de que já tem [configurado um grupo de disponibilidade](../classic/portal-sql-alwayson-availability-groups.md) , mas não tiver configurado um serviço de escuta.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Diretrizes e limitações para as escutas de externas
Tenha em atenção Olá seguir as diretrizes sobre a escuta do grupo de disponibilidade Olá no Azure, quando estiver a implementar utilizando o endereço de VIP Olá nuvem serviço pubic:

* escuta do grupo de disponibilidade de hello é suportada no Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.
* aplicação de cliente Olá têm de residir num serviço cloud diferente que Olá que contém o grupo de disponibilidade VMs. O serviço em nuvem do Azure não suporta direta do servidor devolver com o cliente e servidor Olá mesmo.
* Por predefinição, os passos descritos neste artigo Olá mostram como o endereço de IP Virtual (VIP) do serviço de cloud de Olá de toouse tooconfigure um serviço de escuta. No entanto, é possível tooreserve e criar vários endereços de VIP do serviço em nuvem. Isto permite-lhe toouse passos Olá toocreate este artigo vários serviços de escuta que são cada um associado um VIP diferentes. Para obter informações sobre como toocreate vários endereços VIP, consulte o artigo [vários VIPs por serviço em nuvem](../../../load-balancer/load-balancer-multivip.md).
* Se estiver a criar um serviço de escuta para um ambiente híbrido, rede no local de Olá tem de ter conectividade toohello Internet pública na adição toohello VPN de site para site com Olá rede virtual do Azure. Quando Olá sub-rede do Azure, escuta do grupo de disponibilidade de Olá é acessível apenas por endereço IP público de Olá do serviço de nuvem respetivos Olá.
* Não é suportado um serviço de escuta externo Olá mesmo onde tem também um serviço de escuta interno utilizando o serviço em nuvem do toocreate Olá Balanceador de carga interno (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Determinar a acessibilidade de Olá do serviço de escuta de Olá
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Este artigo foca-se sobre a criação de um serviço de escuta que utiliza **balanceamento de carga externo**. Se pretender que um serviço de escuta de rede virtual privada tooyour, consulte a versão Olá deste artigo que fornece os passos para configurar um [serviço de escuta com o ILB](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Criar os pontos finais VM com balanceamento de carga com direta do servidor retorno
Balanceamento de carga externo utiliza o endereço de Virtual IP de público de Olá virtual do Olá do serviço em nuvem Olá que aloja as suas VMs. Por isso, não precisa de toocreate ou configurar o Balanceador de carga Olá neste caso.

Tem de criar um ponto final com balanceamento de carga para cada VM que aloja uma réplica do Azure. Se tiver réplicas em várias regiões, cada réplica para essa região tem de ser Olá mesmo serviço de nuvem Olá mesma VNet. As réplicas do grupo de disponibilidade de criação que abrangem várias regiões do Azure necessita de configurar várias VNets. Para obter mais informações sobre como configurar a conectividade de VNet cruzada, consulte [Configure VNet tooVNet conectividade](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. No portal do Azure Olá, navegue até tooeach VM que aloja uma réplica e ver os detalhes de Olá.
2. Clique em Olá **pontos finais** separador para cada uma das VMs Olá.
3. Certifique-se de que Olá **nome** e **Porta pública** do ponto final de serviço de escuta de Olá pretende toouse não está já em utilização. Exemplo de Olá abaixo, o nome de Olá é "MyEndpoint" e porta de Olá é "1433".
4. No seu cliente local, transfira e instale [módulo do PowerShell mais recente Olá](https://azure.microsoft.com/downloads/).
5. Iniciar **o Azure PowerShell**. Um novo PowerShell sessão está aberta com Olá módulos administrativos do Azure carregados.
6. Executar **Get-AzurePublishSettingsFile**. Este cmdlet direciona toodownload de browser tooa um publicar definições ficheiro tooa diretório local. Poderão ser-lhe solicitadas as credenciais de início de sessão para a sua subscrição do Azure.
7. Executar Olá **importação AzurePublishSettingsFile** comando com o caminho de Olá de Olá publicar o ficheiro de definições que transferiu a:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Depois de publicar Olá importado do ficheiro de definições, pode gerir a sua subscrição do Azure numa sessão do PowerShell de Olá.
    
1. Copie o script do PowerShell Olá abaixo para um editor de texto e defina Olá valores das variáveis toosuit ambiente (as predefinições foram fornecidas para alguns parâmetros). Tenha em atenção que se o grupo de disponibilidade abranger regiões do Azure, tem de executar o script de Olá uma vez cada centro de dados para o serviço em nuvem Olá e nós que residem em que Centro de dados.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Assim que tiver definido as variáveis de Olá, Olá de cópia do script do editor de texto Olá no seu toorun de sessão do PowerShell do Azure-lo. Se a linha de Olá continua a mostrar >>, escreva novamente ENTER toomake script de Olá se entra em execução.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>Certifique-se de que KB2854082 está instalado, se necessário
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Abrir portas de firewall de Olá em nós do grupo de disponibilidade
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Criar a escuta do grupo de disponibilidade de Olá

Crie a escuta do grupo de disponibilidade de Olá em dois passos. Em primeiro lugar, crie o recurso de cluster de ponto de acesso de cliente de Olá e configurar as dependências. Segundo, configure os recursos do cluster Olá com o PowerShell.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Criar ponto de acesso de cliente Olá e configurar as dependências de cluster Olá
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>Configurar recursos de cluster Olá no PowerShell
1. Balanceamento de carga externa, tem de obter o endereço IP virtual público por Olá do serviço em nuvem Olá que contém as réplicas. Inicie sessão no Olá portal do Azure. Navegue toohello o serviço em nuvem que contém o grupo de disponibilidade VM. Abra Olá **Dashboard** vista.
2. Tenha em atenção endereço Olá apresentado em **endereço IP Virtual público (VIP)**. Se a sua solução abrange VNets, repita este passo para cada serviço em nuvem que contenha uma VM que aloja uma réplica.
3. Dos Olá VMs, copie Olá script do PowerShell abaixo para um editor de texto e definir variáveis de Olá valores toohello que anotou anteriormente.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Uma vez que definiu as variáveis de Olá, abra uma janela elevada do Windows PowerShell, em seguida, copie o script de Olá do editor de texto de Olá e cole no seu toorun de sessão do PowerShell do Azure. Se a linha de Olá continua a mostrar >>, escreva novamente ENTER toomake script de Olá se entra em execução.
5. Repita esta em cada VM. Este script configura o recurso de endereço IP de Olá com o endereço IP Olá do serviço de nuvem Olá e define outros parâmetros, como a porta da sonda Olá. Quando Olá recursos de endereço IP seja colocado online, pode, em seguida, responder toohello consulta na porta de sonda de Olá do ponto final de balanceamento de carga do Olá criado anteriormente no tutorial.

## <a name="bring-hello-listener-online"></a>Coloque online serviço de escuta de Olá
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>Itens de seguimento
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Escuta do grupo de disponibilidade do teste Olá (dentro Olá mesmo VNet)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Escuta do grupo de disponibilidade do teste Olá (através de Olá internet)
Na ordem tooaccess Olá serviço de escuta de rede virtual externa Olá, tem de utilizar o balanceamento de carga de externo/público (descrito neste tópico) em vez do ILB, que é apenas accesible dentro Olá mesma VNet. Na cadeia de ligação de Olá, especifique o nome do serviço de nuvem de Olá. Por exemplo, se tiver um serviço em nuvem com o nome de Olá *mycloudservice*, instrução de sqlcmd Olá seria o seguinte:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

Ao contrário do exemplo anterior Olá, autenticação de SQL tem de ser utilizada, porque o emissor de Olá não é possível utilizar a autenticação do windows através de Olá internet. Para obter mais informações, consulte [sempre no grupo de disponibilidade na VM do Azure: cenários de conectividade do cliente](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx). Quando utilizar a autenticação do SQL Server, certifique-se que crie Olá mesmo início de sessão em ambas as réplicas. Para obter mais informações sobre resolução de problemas de inícios de sessão com grupos de disponibilidade, consulte [como toomap inícios de sessão ou utilize contidos SQL réplicas de tooother tooconnect de utilizador de base de dados e tooavailability bases de dados do mapa](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

Se Olá Always On réplicas estarem em sub-redes diferentes, os clientes têm de especificar **MultisubnetFailover = True** na cadeia de ligação de Olá. Isto resulta num tooreplicas de tentativas de ligação paralelas em sub-redes diferentes Olá. Tenha em atenção que este cenário inclui a uma implementação de sempre no grupo de disponibilidade por várias regiões.

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

