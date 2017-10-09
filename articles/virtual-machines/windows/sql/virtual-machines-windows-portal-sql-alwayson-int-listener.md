---
title: aaaCreate uma escuta do grupo de disponibilidade do SQL Server em virtual machines do Azure | Microsoft Docs
description: "Instruções passo a passo para criar um serviço de escuta para um grupo de disponibilidade Always On para o SQL Server em virtual machines do Azure"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Configurar um balanceador de carga para um grupo de disponibilidade Always On no Azure
Este artigo explica como toocreate um balanceador de carga para um grupo de disponibilidade SQL Server Always On no Azure virtual máquinas estão em execução com o Azure Resource Manager. Um grupo de disponibilidade necessita de um balanceador de carga quando são instâncias do SQL Server Olá em máquinas virtuais do Azure. Balanceador de carga Olá armazena do endereço IP Olá escuta do grupo de disponibilidade de Olá. Se um grupo de disponibilidade abranger várias regiões, cada região necessita de um balanceador de carga.

toocomplete nesta tarefa, terá de toohave implementado num grupo de disponibilidade do SQL Server em virtual machines do Azure que estejam a executar com o Resource Manager. Máquinas virtuais do SQL Server tem de pertencer toohello mesmo conjunto de disponibilidade. Pode utilizar Olá [modelo Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically criar grupo de disponibilidade de Olá no Gestor de recursos. Este modelo cria automaticamente um balanceador de carga interno para si. 

Se preferir, pode [configurar manualmente a um grupo de disponibilidade](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Este artigo requer que os grupos de disponibilidade já estão configurados.  

Tópicos relacionados incluem:

* [Configurar grupos de disponibilidade Always On na VM do Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configurar uma ligação VNet a VNet através do Azure Resource Manager e o PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

Orientando através deste artigo, pode criar e configurar um balanceador de carga no Olá portal do Azure. Após a conclusão do processo de Olá, pode configura Olá toouse Olá endereço IP do Balanceador de carga Olá para escuta do grupo de disponibilidade de Olá.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Criar e configurar o Balanceador de carga Olá no Olá portal do Azure
Nesta parte da tarefa de Olá, Olá seguintes:

1. No portal do Azure Olá, criar Balanceador de carga Olá e configurar o endereço IP Olá.
2. Configure o conjunto de back-end Olá.
3. Crie a sonda de Olá. 
4. Definir regras de balanceamento de carga Olá.

> [!NOTE]
> Se as instâncias do SQL Server de Olá estiverem em vários grupos de recursos e regiões, execute cada passo duas vezes, uma vez em cada grupo de recursos.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Passo 1: Criar Balanceador de carga Olá e configurar o endereço IP Olá
Em primeiro lugar, crie o Balanceador de carga Olá. 

1. No portal do Azure Olá, abra o grupo de recursos de Olá contém Olá máquinas virtuais do SQL Server. 

2. No grupo de recursos de Olá, clique em **adicionar**.

3. Procurar **Balanceador de carga** e, em seguida, nos resultados de pesquisa de Olá, selecione **Load Balancer**, que é publicada pelo **Microsoft**.

4. No Olá **Balanceador de carga** painel, clique em **criar**.

5. No Olá **criar Balanceador de carga** diálogo caixa, configure o Balanceador de carga Olá da seguinte forma:

   | Definição | Valor |
   | --- | --- |
   | **Nome** |Um nome de texto que representa o Balanceador de carga Olá. Por exemplo, **sqlLB**. |
   | **Tipo** |**Interno**: maioria das implementações de utilizar um balanceador de carga interno, que permite que aplicações Olá dentro do mesmo grupo de disponibilidade do toohello tooconnect rede virtual.  </br> **Externo**: permite que o grupo de disponibilidade do aplicações tooconnect toohello através de uma ligação à Internet pública. |
   | **Rede virtual** |Selecione a rede virtual Olá que Olá intances de SQL Server estão em. |
   | **Sub-rede** |Selecione a sub-rede de Olá que são instâncias do SQL Server Olá no. |
   | **Atribuição de endereços IP** |**Estática** |
   | **Endereço IP privado** |Especifique um endereço IP disponível da sub-rede Olá. Utilize este endereço IP quando criar um serviço de escuta no cluster de Olá. Num script do PowerShell, neste artigo, utilize este endereço de Olá `$ILBIP` variável. |
   | **Subscrição** |Se tiver várias subscrições, poderá ser apresentado este campo. Selecione a subscrição de Olá que pretende que o tooassociate com este recurso. É normalmente Olá mesma subscrição, todos os recursos de Olá Olá grupo de disponibilidade. |
   | **Grupo de recursos** |Selecione o grupo de recursos de Olá que são instâncias do SQL Server Olá no. |
   | **Localização** |Selecione Olá localização do Azure que são instâncias do SQL Server Olá no. |

6. Clique em **Criar**. 

O Azure cria Balanceador de carga Olá. Balanceador de carga Olá pertence tooa de rede específicas, sub-rede, grupo de recursos e localização. Depois de Azure concluir a tarefa de Olá, verifique as definições do Balanceador de carga Olá no Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Passo 2: Configurar o conjunto de back-end Olá
Conjunto de endereços de back-end Olá, Azure chamadas *conjunto back-end*. Neste caso, o conjunto de back-end Olá é endereços Olá de instâncias do SQL Server dois Olá no seu grupo de disponibilidade. 

1. No seu grupo de recursos, clique em Balanceador de carga Olá que criou. 

2. No **definições**, clique em **conjuntos back-end**.

3. No **conjuntos back-end**, clique em **adicionar** toocreate um conjunto de endereços de back-end. 

4. No **adicionar conjunto back-end**, em **nome**, escreva um nome para o conjunto de back-end Olá.

5. Em **máquinas virtuais**, clique em **adicionar uma máquina virtual**. 

6. Em **escolher as máquinas virtuais**, clique em **escolher um conjunto de disponibilidade**e, em seguida, especifique o conjunto de disponibilidade de Olá que as máquinas virtuais do SQL Server Olá pertence ao.

7. Depois de escolher o conjunto de disponibilidade de Olá, clique em **escolher máquinas de virtuais Olá**, selecione Olá duas máquinas virtuais que alojem instâncias do SQL Server Olá no grupo de disponibilidade de Olá e, em seguida, clique em **selecione**. 

8. Clique em **OK** painéis de Olá tooclose para **escolher as máquinas virtuais**, e **adicionar conjunto back-end**. 

Azure atualiza as definições de Olá para o conjunto de endereços de back-end de Olá. O conjunto de disponibilidade tem agora um agrupamento de duas instâncias do SQL Server.

### <a name="step-3-create-a-probe"></a>Passo 3: Criar uma sonda
sonda de Olá define a forma como o Azure verifica que instâncias do SQL Server Olá atualmente, possui escuta do grupo de disponibilidade de Olá. Serviço de Olá com base no endereço IP Olá numa porta que definem quando criar a sonda de Olá as sondas do Azure.

1. Balanceador de carga no Olá **definições** painel, clique em **sondas de estado de funcionamento**. 

2. No Olá **sondas de estado de funcionamento** painel, clique em **adicionar**.

3. Configurar a sonda de Olá no Olá **adicionar sonda** painel. Os seguintes valores tooconfigure Olá sonda Olá de utilização:

   | Definição | Valor |
   | --- | --- |
   | **Nome** |Um nome de texto que representa a sonda de Olá. Por exemplo, **SQLAlwaysOnEndPointProbe**. |
   | **Protocolo** |**TCP** |
   | **Porta** |Pode utilizar qualquer porta disponível. Por exemplo, *59999*. |
   | **Intervalo** |*5* |
   | **Limiar de mau estado de funcionamento** |*2* |

4.  Clique em **OK**. 

> [!NOTE]
> Certifique-se de que a porta de Olá que especificar está aberta na firewall de Olá de ambas as instâncias do SQL Server. Ambas as instâncias requerem uma regra de entrada para Olá a porta TCP que utiliza. Para obter mais informações, consulte [adicionar ou Editar regra de Firewall](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure cria Olá pesquisa e, em seguida, utiliza-o tootest que instância do SQL Server tem o serviço de escuta de Olá Olá grupo de disponibilidade.

### <a name="step-4-set-hello-load-balancing-rules"></a>Passo 4: Definir regras de balanceamento de carga Olá
regras de balanceamento de carga Olá configurar como Olá load balancer encaminha instâncias do tráfego toohello do SQL Server. Para este Balanceador de carga, ativar a devolução direta do servidor porque apenas uma das duas instâncias de SQL Server Olá possui o recurso de serviço de escuta do grupo de disponibilidade de Olá cada vez.

1. Balanceador de carga no Olá **definições** painel, clique em **as regras de balanceamento de carga**. 

2. No Olá **as regras de balanceamento de carga** painel, clique em **adicionar**.

3. No Olá **as regras de balanceamento de carga de adicionar** painel, configurar a regra de balanceamento de carga Olá. Utilize Olá seguintes definições: 

   | Definição | Valor |
   | --- | --- |
   | **Nome** |Um nome de texto que representa as regras de balanceamento de carga Olá. Por exemplo, **SQLAlwaysOnEndPointListener**. |
   | **Protocolo** |**TCP** |
   | **Porta** |*1433* |
   | **Porta de back-end** |*1433*. Este valor é ignorado porque esta regra utiliza **IP flutuante (devolução direta do servidor)**. |
   | **Sonda** |Utilize o nome de Olá da sonda de Olá que criou para este Balanceador de carga. |
   | **Persistência da sessão** |**Nenhum** |
   | **Tempo limite de inatividade (minutos)** |*4* |
   | **Vírgula flutuante (devolução direta do servidor) de IP** |**Ativado** |

   > [!NOTE]
   > Poderá ter tooscroll baixo Olá painel tooview todas as definições de Olá.
   > 

4. Clique em **OK**. 
5. Azure configura a regra de balanceamento de carga de Olá. Balanceador de carga Olá está agora configurado tooroute tráfego toohello SQL instância do servidor que aloja o serviço de escuta de Olá Olá grupo de disponibilidade. 

Neste momento, o grupo de recursos de Olá tem um balanceador de carga que liga tooboth máquinas de SQL Server. Balanceador de carga Olá também contém um endereço IP para Olá SQL Server Always On escuta do grupo disponibilidade, para que a máquina pode responder toorequests Olá para grupos de disponibilidade.

> [!NOTE]
> Se as instâncias do SQL Server estão em duas regiões separadas, repita os passos de Olá Olá outra região. Cada região necessita de um balanceador de carga. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Configurar toouse de cluster de Olá Olá endereço IP de Balanceador de carga
passo seguinte Olá tooconfigure Olá escuta no cluster de Olá e coloque online serviço de escuta de Olá. Olá seguintes: 

1. Crie a escuta do grupo de disponibilidade de Olá Olá cluster de ativação pós-falha. 

2. Coloque online serviço de escuta de Olá.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Passo 5: Criar a escuta do grupo de disponibilidade de Olá Olá cluster de ativação pós-falha
Neste passo, cria manualmente escuta do grupo de disponibilidade Olá no Gestor de clusters de ativação pós-falha e o SQL Server Management Studio.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Verifique a configuração de Olá do serviço de escuta de Olá

Se os recursos do cluster Olá e as dependências se encontram corretamente configuradas, deve ser capaz de tooview Olá serviço de escuta de SQL Server Management Studio. tooset Olá porta do serviço de escuta, Olá a seguir:

1. Inicie o SQL Server Management Studio e, em seguida, ligue toohello de réplica primária.

2. Aceda demasiado**elevada disponibilidade do AlwaysOn** > **grupos de disponibilidade** > **escuta do grupo de disponibilidade**.  
    Deverá ver agora o nome do serviço de escuta de Olá que criou no Gestor de clusters de ativação pós-falha. 

3. Clique no nome do serviço de escuta de Olá e, em seguida, clique em **propriedades**.

4. No Olá **porta** caixa, especifique o número de porta de escuta do grupo de disponibilidade de Olá Olá utilizando Olá $EndpointPort que utilizou anteriormente (1433 foi predefinido Olá) e, em seguida, clique em **OK**.

Tem agora um grupo de disponibilidade em máquinas virtuais do Azure em execução no modo Resource Manager. 

## <a name="test-hello-connection-toohello-listener"></a>O serviço de escuta do teste Olá ligação toohello
Testar a ligação de Olá, Olá seguinte:

1. Instância do SQL Server do RDP tooa que está a ser Olá mesmo virtual de rede, mas não réplica Olá próprio. Este servidor pode ser Olá outra instância do SQL Server em cluster Olá.

2. Utilize **sqlcmd** ligação do utilitário tootest Olá. Por exemplo, o seguinte script de Olá estabelece uma **sqlcmd** réplica primária de toohello ligação através do serviço de escuta de Olá com autenticação do Windows:
   
        sqlcmd -S <listenerName> -E

Olá ligação SQLCMD liga automaticamente toohello instância de SQL Server que aloja a réplica primária Olá. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Criar um endereço IP para um grupo de disponibilidade adicionais

Cada grupo de disponibilidade utiliza um serviço de escuta separado. Cada serviço de escuta possui o seu próprio endereço IP. Utilize Olá mesmo endereço IP de Olá de toohold de Balanceador de carga para as escutas de adicionais. Depois de criar um grupo de disponibilidade, adicionar balanceador de carga de toohello de endereço IP Olá e, em seguida, configure o serviço de escuta de Olá.

tooadd um balanceador de carga do tooa de endereço IP com Olá portal do Azure, Olá seguintes:

1. No portal do Azure Olá, abra o grupo de recursos de Olá que contém o Balanceador de carga Olá e, em seguida, clique em Balanceador de carga Olá. 

2. Em **definições**, clique em **conjunto IP de front-end**e, em seguida, clique em **adicionar**. 

3. Em **adicionar endereço IP de front-end**, atribua um nome para o front-end de Olá. 

4. Certifique-se de que Olá **rede Virtual** e Olá **sub-rede** são Olá igual ao hello instâncias do SQL Server.

5. Definir o endereço IP de Olá para serviço de escuta de Olá. 
   
   >[!TIP]
   >Pode definir toostatic de endereço IP de Olá e escreva um endereço que não é atualmente utilizado na sub-rede Olá. Em alternativa, pode definir toodynamic de endereço IP de Olá e guardar o conjunto IP de front-end novo de Olá. Se o fizer, Olá portal do Azure atribui automaticamente disponível toohello conjunto de endereços IP. Pode, em seguida, volte a abrir o conjunto IP Front-end Olá e alterar Olá toostatic de atribuição. 

6. Guarde o endereço IP Olá para serviço de escuta de Olá. 

7. Adicione uma pesquisa de estado de funcionamento utilizando Olá seguintes definições:

   |Definição |Valor
   |:-----|:----
   |**Nome** |Sonda de Olá tooidentify um nome.
   |**Protocolo** |TCP
   |**Porta** |Uma porta não utilizada TCP, que tem de estar disponível em todas as máquinas virtuais. Não pode ser utilizado para qualquer outra finalidade. Não existem dois serviços de escuta podem utilizar Olá mesmo sonda a porta. 
   |**Intervalo** |tenta Olá período de tempo entre a pesquisa. Utilize predefinição de Olá (5).
   |**Limiar de mau estado de funcionamento** |número de Olá de limiares consecutivos que devem falhar antes de uma máquina virtual é considerada em mau estado de funcionamento.

8. Clique em **OK** sonda de Olá toosave. 

9. Crie uma regra de balanceamento de carga. Clique em **as regras de balanceamento de carga**e, em seguida, clique em **adicionar**.

10. Configure Olá novo de balanceamento de carga regra ao utilizar Olá seguintes definições:

   |Definição |Valor
   |:-----|:----
   |**Nome** |Olá de tooidentify um nome de regra de balanceamento de carga. 
   |**Endereço IP de front-end** |Selecione o endereço IP Olá que criou. 
   |**Protocolo** |TCP
   |**Porta** |Utilize a porta de Olá que instâncias do SQL Server Olá estão a utilizar. Uma instância predefinida utiliza a porta 1433, a menos que o alterado. 
   |**Porta de back-end** |Olá utilize mesmo valor como **porta**.
   |**Conjunto back-end** |conjunto de Olá que contém máquinas virtuais de Olá com instâncias de SQL Server Olá. 
   |**Sonda de estado de funcionamento** |Escolha sonda Olá que criou.
   |**Persistência da sessão** |Nenhuma
   |**Tempo limite de inatividade (minutos)** |Predefinição (4)
   |**Vírgula flutuante (devolução direta do servidor) de IP** | Ativado

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Configurar Olá disponibilidade grupo toouse Olá novo endereço IP

toofinish configurar cluster Olá, os passos de repetições Olá que seguiu quando efetuado primeiro grupo de disponibilidade Olá. Ou seja, configura Olá [toouse Olá novo endereço IP do cluster](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Depois de ter adicionado um endereço IP para o serviço de escuta de Olá, configure o grupo de disponibilidade adicionais de Olá, Olá seguinte: 

1. Certifique-se de que a porta da sonda Olá para o novo endereço IP Olá está aberta em ambas as máquinas virtuais do SQL Server. 

2. [No Gestor de clusters, adicionar o ponto de acesso de cliente Olá](#addcap).

3. [Configurar o recurso IP Olá para o grupo de disponibilidade de Olá](#congroup).

   >[!IMPORTANT]
   >Quando cria o endereço IP Olá, utilize o endereço IP de Olá que adicionou toohello Balanceador de carga.  

4. [Tornar o recurso do grupo de disponibilidade do SQL Server Olá depende de ponto de acesso de cliente Olá](#dependencyGroup).

5. [Se o acesso de cliente Olá ponto recursos dependentes no endereço IP Olá](#listname).
 
6. [Definir os parâmetros de cluster Olá no PowerShell](#setparam).

Depois de configurar Olá disponibilidade grupo toouse Olá novo endereço IP, configure o serviço de escuta do Olá ligação toohello. 

## <a name="next-steps"></a>Passos seguintes

- [Configurar um grupo de disponibilidade SQL Server Always On em máquinas virtuais do Azure em regiões diferentes](virtual-machines-windows-portal-sql-availability-group-dr.md)
