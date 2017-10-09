---
title: "aaaConnect tooa Máquina Virtual do servidor SQL no Azure (clássica) | Microsoft Docs"
description: "Saiba como tooconnect tooSQL servidor em execução numa máquina Virtual no Azure. Este tópico utiliza o modelo de implementação clássica Olá. cenários de Olá diferem consoante a configuração da rede Olá e a localização de hello do cliente de Olá."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Ligar tooa Máquina Virtual do servidor SQL no Azure (implementação clássica)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-connect.md)
> * [Clássico](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Descrição geral
Este tópico descreve como tooconnect tooyour do SQL Server de instância em execução numa máquina virtual do Azure. Abrange alguns [cenários de conectividade](#connection-scenarios) e, em seguida, fornece [detalhadas os passos para configurar a conectividade do SQL Server numa VM do Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá. Se estiver a utilizar as VMs do Gestor de recursos, consulte o artigo [ligar tooa Máquina Virtual do servidor SQL no Azure com o Resource Manager](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Cenários de ligação
a forma de Olá um cliente liga-se tooSQL servidor em execução numa máquina Virtual difere dependendo da localização de Olá hello do cliente do e configuração de máquina/redes Olá. Estes cenários incluem:

* [Ligar tooSQL servidor no Olá mesmo serviço em nuvem](#connect-to-sql-server-in-the-same-cloud-service)
* [Ligar tooSQL servidor através de Olá internet](#connect-to-sql-server-over-the-internet)
* [Ligar tooSQL servidor no Olá mesma rede virtual](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Antes de ligar com qualquer um destes métodos, tem de seguir Olá [os passos na conectividade de tooconfigure artigo](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Ligar tooSQL servidor no Olá mesmo serviço em nuvem
Várias máquinas virtuais podem ser criadas na Olá mesmo serviço em nuvem. máquinas de toounderstand virtual neste cenário, consulte [como máquinas de virtuais tooconnect com um serviço de nuvem ou de rede virtual](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Este cenário ocorre quando um cliente na máquina virtual de um tenta a execução de servidor tooconnect tooSQL noutra máquina virtual no Olá mesmo serviço em nuvem.

Neste cenário, pode estabelecer ligação utilizando Olá VM **nome** (também são mostradas como **nome do computador** ou **hostname** no portal de Olá). Este é o nome de Olá fornecido para Olá VM durante a criação. Por exemplo, se denominar a VM do SQL Server **mysqlvm**, um cliente VM Olá poderia utilizar o mesmo serviço em nuvem Olá seguir tooconnect de cadeia de ligação:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Ligar tooSQL servidor através de Olá Internet
Se pretender que o motor de base de dados do tooconnect tooyour do SQL Server de Olá Internet, tem de criar um ponto final da máquina virtual para comunicação de TCP recebidas. Este passo de configuração do Azure, direciona entrada TCP porta tráfego tooa a porta TCP que seja acessível toohello máquina.

Olá, tooconnect através de internet, tem de utilizar DNS nome e Olá VM endpoint número da porta da VM Olá (configurado neste artigo). Olá toofind nome DNS, navegue toohello Azure portal e selecione **máquinas virtuais (clássicas)**. Em seguida, selecione a máquina virtual. Olá **nome DNS** é apresentado na Olá **descrição geral** secção.

Por exemplo, considere uma máquina virtual clássica chamada **mysqlvm** com um nome de DNS de **mysqlvm7777.cloudapp.net** e um ponto final de VM de **57500**. Partindo do princípio de conectividade corretamente configurada, Olá seguinte cadeia de ligação foi ser tooaccess utilizados Olá máquina virtual de partir de qualquer lugar no Olá internet:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Apesar de isto ativa a conectividade de clientes através de Olá internet, isto implica que qualquer pessoa pode ligar tooyour do SQL Server. Os clientes exteriores tem correto toohello de nome de utilizador e palavra-passe. Para segurança adicional, não utilize a porta conhecidos Olá 1433 para o ponto final do Olá pública máquina virtual. E, se possível, considere adicionar uma ACL num ponto final toorestrict tráfego toohello apenas clientes que é permitir. Para obter instruções sobre a utilização de ACLs com pontos finais, consulte [gerir Olá ACL num ponto final](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> É importante toonote quando utilizar esta técnica toocommunicate com o SQL Server, todos os dados de saída de Olá datacenter do Azure é requerente toonormal [preços em transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Ligar tooSQL servidor no Olá mesma rede virtual
[Rede virtual](../../../virtual-network/virtual-networks-overview.md) permite cenários adicionais. Pode ligar as VMs na mesma rede virtual, mesmo que essas VMs existe nos serviços de nuvem diferente de Olá. E com um [VPN site a site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), pode criar uma arquitetura de híbridos que liga as VMs com redes no local e as máquinas.

Redes virtuais também permite toojoin o domínio de tooa VMs do Azure. Este é Olá apenas forma toouse autenticação do Windows tooSQL servidor. Olá outros cenários de ligação exigem autenticação de SQL com os nomes de utilizador e palavras-passe.

Se pretender tooconfigure num ambiente de domínio e a autenticação do Windows, não é necessário toouse Olá passos neste artigo tooconfigure Olá públicas do ponto final ou Olá autenticação do SQL Server e inícios de sessão. Neste cenário, pode ligar a instância do SQL Server tooyour especificando o nome da VM do SQL Server Olá na cadeia de ligação de Olá. Olá seguinte o exemplo assume que também tenha sido configurada a autenticação do Windows e esse utilizador Olá tiver sido concedido a instância do acesso toohello do SQL Server.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Passos para configurar a conectividade do SQL Server numa VM do Azure
Olá, os passos seguintes demonstram como instância de SQL Server toohello tooconnect através de Olá internet com o SQL Server Management Studio (SSMS). No entanto, hello mesmos passos aplicam-se toomaking máquina virtual do SQL Server acessível para as suas aplicações, em execução no local e no Azure.

Antes de poder ligar toohello instância do SQL Server a partir de outra VM ou Olá internet, tem de concluir Olá seguintes tarefas, conforme descrito nas secções Olá que se seguem:

* [Criar um ponto final TCP para a máquina virtual de Olá](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Portas TCP abertas na firewall do Windows hello](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Configurar o SQL Server toolisten no Olá protocolo TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Configurar o SQL Server para a autenticação de modo misto](#configure-sql-server-for-mixed-mode-authentication)
* [Criar inícios de sessão de autenticação de SQL Server](#create-sql-server-authentication-logins)
* [Determinar o nome DNS Olá da máquina virtual de Olá](#determine-the-dns-name-of-the-virtual-machine)
* [Ligar toohello motor de base de dados a partir de outro computador](#connect-to-the-database-engine-from-another-computer)

caminho de ligação de Olá é resumido por Olá diagrama a seguir:

![Ligar a máquina de virtual tooa do SQL Server](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Passos Seguintes
Se também estiver a planear grupos de Disponibilidade AlwaysOn toouse para elevada disponibilidade e recuperação após desastre, deve considerar implementar um serviço de escuta. Os clientes de base de dados ligam o serviço de escuta do toohello em vez de diretamente tooone de instâncias do SQL Server de Olá. Olá escuta rotas clientes toohello réplica primária do grupo de disponibilidade de Olá. Para obter mais informações, consulte [configurar um serviço de escuta do ILB para grupos de Disponibilidade AlwaysOn no Azure](../classic/ps-sql-int-listener.md).

É importante tooreview todas segurança Olá melhores práticas para o SQL Server em execução numa máquina virtual do Azure. Para obter mais informações, veja [Security Considerations for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md) (Considerações de segurança para o SQL Server em Máquinas Virtuais do Azure).

[Explorar o percurso de aprendizagem do Olá](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) para SQL Server em virtual machines do Azure. 

Para outros tópicos relacionados com toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

