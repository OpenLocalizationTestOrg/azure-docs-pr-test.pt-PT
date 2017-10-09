---
title: "aaaSet segurança elevada disponibilidade para as VMs do Azure Resource Manager | Microsoft Docs"
description: "Este tutorial mostra como toocreate um disponibilidade Always On agrupar com máquinas virtuais do Azure no modo Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Configurar grupos de disponibilidade Always On em Azure Virtual Machines automaticamente: o Gestor de recursos

Este tutorial mostra como toocreate uma disponibilidade do SQL Server grupo que utiliza máquinas de virtuais do Azure Resource Manager. tutorial de Olá utiliza os painéis do Azure tooconfigure um modelo. Pode rever as definições predefinidas da Olá, escreva as definições necessárias e atualizar os painéis de Olá no portal de Olá como percorrer neste tutorial.

tutorial de conclusão de Olá cria um grupo de disponibilidade do SQL Server em Virtual Machines do Azure que incluem Olá seguintes elementos:

* Uma rede virtual que tem várias sub-redes, incluindo um front-end e uma sub-rede de back-end
* Dois controladores de domínio que tenha um domínio do Active Directory
* Duas máquinas virtuais que executam o SQL Server e que são implementadas toohello sub-rede de back-end e toohello associados a um domínio de Active Directory
* Um cluster de ativação pós-falha de três nós com o modelo de quórum maioria de nós de Olá
* Um grupo de disponibilidade que tem duas réplicas com consolidação síncrona de uma base de dados de disponibilidade

Olá seguinte ilustração representa a solução completa de Olá.

![Arquitetura de laboratório de teste para grupos de disponibilidade no Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Grupo de recursos única de tooa de pertencer todos os recursos nesta solução.

Antes de começar este tutorial, confirme o seguinte Olá:

* Já tem uma conta do Azure. Se não tiver uma, [inscrever-se para uma conta de avaliação](http://azure.microsoft.com/pricing/free-trial/).
* Já sabe como toouse Olá GUI tooprovision uma máquina virtual do SQL Server a partir da Galeria de máquina virtual de Olá. Para obter mais informações, consulte [aprovisionar uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).
* Já existe uma compreensão sólida dos grupos de disponibilidade. Para obter mais informações, consulte [Always On nos grupos de disponibilidade (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Se estiver interessado em utilizar grupos de disponibilidade com o SharePoint, consulte também [configurar SQL Server 2012 Always On grupos de disponibilidade para SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).
>
>

Neste tutorial, utilize Olá Azure portal para:

* Escolha Olá sempre no modelo do portal de Olá.
* Reveja as definições do modelo de Olá e atualizar algumas definições de configuração para o seu ambiente.
* Monitor do Azure à medida que cria todo o ambiente Olá.
* Liga o controlador de domínio tooa e, em seguida, tooa servidor que executa o SQL Server.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Cluster de Olá aprovisionar na Galeria de Olá
O Azure oferece uma imagem de galeria para a solução completa de Olá. modelo de Olá toolocate:

1. Inicie sessão toohello portal do Azure utilizando a sua conta.
2. No portal do Azure Olá, clique em **+ novo** tooopen Olá **novo** painel.
3. No Olá **novo** painel, procure **AlwaysOn**.
   ![Localizar o modelo de AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. Nos resultados de pesquisa de Olá, localize **Cluster do SQL Server AlwaysOn**.
   ![Modelo de AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. No **selecionar um modelo de implementação**, escolha **Resource Manager**.

### <a name="basics"></a>Noções básicas
Clique em **Noções básicas** e configurar Olá seguintes definições:

* **Nome de utilizador administrador** é uma conta de utilizador que tem permissões de administrador de domínio e é um membro da função de servidor fixa do Olá do SQL Server sysadmin no ambas as instâncias do SQL Server. Para este tutorial, utilize **DomainAdmin**.
* **Palavra-passe** é Olá palavra-passe da conta de administrador de domínio Olá. Utilize uma palavra-passe complexa. Confirme a palavra-passe de Olá.
* **Subscrição** Olá subscrição que Azure faturas toorun todos os implementado recursos Olá grupo de disponibilidade. Se a sua conta tiver várias subscrições, pode especificar uma subscrição diferente.
* **Grupo de recursos** é Olá nome Olá grupo toowhich pertencerem todos os recursos do Azure que são criados por este modelo. Para este tutorial, utilize **SQL-HA-RG**. Para obter mais informações, veja [Descrição geral do Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Localização** é Olá região do Azure onde o tutorial Olá cria recursos Olá. Escolha uma região do Azure.

Olá seguinte captura de ecrã é uma concluída **Noções básicas** painel:

![Noções básicas](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Clique em **OK**.

### <a name="domain-and-network-settings"></a>Definições de domínio e de rede
Este modelo de galeria do Azure cria um domínio e os controladores de domínio. Também cria uma rede e duas sub-redes. modelo de Olá não é possível criar servidores numa rede virtual ou domínio existente. passo seguinte Olá configura as definições de domínio e de rede de Olá.

No Olá **definições de domínio e de rede** painel, reveja os valores para definições de domínio e de rede Olá da configuração predefinida Olá:

* **Nome de domínio de raiz de floresta** é o nome de domínio de Olá para o domínio do Active Directory de Olá desse cluster de Olá anfitriões. Tutorial de Olá, utilize **contoso.com**.
* **Nome de rede virtual** é o nome de rede Olá para Olá rede virtual do Azure. Tutorial de Olá, utilize **autohaVNET**.
* **Nome de sub-rede de controlador de domínio** é o nome de Olá de uma parte da rede virtual Olá esse controlador de domínio de Olá de anfitriões. Utilize **sub-rede 1**. Esta sub-rede utiliza o prefixo de endereço **10.0.0.0/24**.
* **Nome da sub-rede do SQL Server** é Olá nome de uma parte da rede virtual Olá servidores de Olá de anfitriões que executam o SQL Server e o ficheiro de Olá testemunho de partilha. Utilize **sub-rede 2**. Esta sub-rede utiliza o prefixo de endereço **10.0.1.0/26**.

toolearn mais informações sobre redes virtuais no Azure, consulte [descrição geral de rede Virtual](../../../virtual-network/virtual-networks-overview.md).  

Olá **definições de domínio e de rede** deve aspeto Olá seguinte captura de ecrã:

![Definições de domínio e de rede](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Se necessário, pode alterar estes valores. Para este tutorial, utilize Olá valores da configuração predefinida.

Reveja as definições de Olá e, em seguida, clique em **OK**.

### <a name="availability-group-settings"></a>Definições do grupo de disponibilidade
No **das definições do grupo de disponibilidade**, reveja Olá valores Olá grupo de disponibilidade da configuração predefinida e Olá o serviço de escuta.

* **Nome do grupo de disponibilidade** é o nome de recurso em cluster Olá Olá grupo de disponibilidade. Para este tutorial, utilize **Contoso ag**.
* **Nome de serviço de escuta do grupo de disponibilidade** é utilizado pelo cluster Olá e Balanceador de carga interno Olá. Os clientes que ligam tooSQL servidor podem utilizar este nome tooconnect toohello adequado réplica da base de dados de Olá. Para este tutorial, utilize **serviço de escuta de Contoso**.
* **Porta de serviço de escuta do grupo de disponibilidade** Especifica a porta TCP Olá do serviço de escuta do Olá do SQL Server. Para este tutorial, utilizar a porta predefinida de Olá, **1433**.

Se necessário, pode alterar estes valores. Para este tutorial, utilize Olá valores da configuração predefinida.  

![Definições do grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Clique em **OK**.

### <a name="virtual-machine-size-storage-settings"></a>Tamanho da máquina virtual, as definições de armazenamento
No **tamanho da VM, as definições de armazenamento**, escolha um tamanho de máquina virtual do SQL Server e revisão Olá outras definições.

* **Tamanho da máquina virtual do SQL Server** é Olá tamanho para máquinas virtuais que executam o SQL Server. Escolha um tamanho de máquina virtual adequado para a carga de trabalho. Se está a criar este ambiente para o tutorial Olá, utilize **DS2**. Para cargas de trabalho de produção, escolha um tamanho de máquina virtual que pode suportar a carga de trabalho Olá. Muitas cargas de trabalho de produção requerem **DS4** ou superior. modelo de Olá cria duas máquinas virtuais deste tamanho e instala o SQL Server em cada um. Para obter mais informações, consulte [tamanhos das virtual machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> A instalação do Azure Olá edição Enterprise do SQL Server. custo de Olá depende da edição Olá e tamanho da máquina virtual Olá. Para obter informações detalhadas sobre os custos atuais, consulte [máquinas de virtuais preços](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Tamanho de máquina virtual do controlador de domínio** é o tamanho da máquina virtual Olá para Olá controladores de domínio. Para este tutorial utilização **D2**.
* **Tamanho da máquina virtual o testemunho da partilha de ficheiros** é o tamanho da máquina virtual Olá para Olá testemunho de partilha de ficheiros. Para este tutorial, utilize **A1**.
* **Conta de armazenamento de SQL** é Olá nome da conta de armazenamento de Olá que contém dados do SQL Server de Olá e discos de sistema operativo. Para este tutorial, utilize **alwaysonsql01**.
* **Conta de armazenamento de DC** é o nome de Olá Olá da conta de armazenamento para Olá controladores de domínio. Para este tutorial, utilize **alwaysondc01**.
* **Tamanho do disco de dados do SQL Server** TB é o tamanho do disco de dados do SQL Server Olá no TB Olá. Especifique um número entre 1 e 4. Para este tutorial, utilize **1**.
* **Otimização de armazenamento** define as definições de configuração de armazenamento específica para máquinas virtuais do SQL Server de Olá com base no tipo de carga de trabalho de Olá. Todas as máquinas virtuais do SQL Server neste cenário utilizar o armazenamento premium com a cache de anfitrião de disco do Azure definida apenas de tooread. Além disso, pode otimizar as definições de SQL Server para a carga de trabalho Olá escolhendo uma das três estas definições:

  * **Carga de trabalho geral** define sem definições de configuração específico.
  * **Processamento transacional** sinalizador 1117 e 1118 de rastreio de conjuntos.
  * **Armazenamento de dados** 1117 do sinalizador de rastreio de conjuntos e 610.

Para este tutorial, utilize **carga de trabalho geral**.

![Definições de armazenamento de tamanho VM](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Reveja as definições de Olá e, em seguida, clique em **OK**.

#### <a name="a-note-about-storage"></a>Nota sobre o armazenamento
Otimizações adicionais dependem de tamanho de Olá Olá do SQL Server de discos de dados. Para cada terabyte do disco de dados, o Azure adiciona um armazenamento adicional de premium 1 TB. Quando um servidor necessita de 2 TB ou mais, o modelo de Olá cria um agrupamento de armazenamento em cada máquina virtual do SQL Server. Um agrupamento de armazenamento é um formulário de Virtualização de armazenamento onde vários discos são tooprovide configurado maior capacidade, resiliência e desempenho.  modelo de Olá, em seguida, cria um espaço de armazenamento no agrupamento de armazenamento Olá e apresenta um sistema de operativo de toohello de disco de dados individual. modelo de Olá designa este disco como disco de dados de Olá para o SQL Server. modelo de Olá tunes agrupamento de armazenamento Olá para o SQL Server utilizando Olá seguintes definições:

* Tamanho do stripe é Olá definição para o disco virtual Olá de intercalação. Cargas de trabalho transacionais utilizam 64 KB. Cargas de trabalho de armazém de dados utilizam 256 KB.
* Resiliência é simple (sem resiliência).

> [!NOTE]
> Armazenamento premium do Azure é localmente redundante e mantém três cópias dos dados de Olá numa única região, pelo que não for necessária resiliência adicional no agrupamento de armazenamento Olá.
>
>

* Contagem de colunas é igual ao número de Olá dos discos no agrupamento de armazenamento Olá.

Para obter informações adicionais sobre o espaço de armazenamento e agrupamentos de armazenamento, consulte:

* [Descrição geral dos espaços de armazenamento](http://technet.microsoft.com/library/hh831739.aspx)
* [Cópia de segurança do Windows Server e agrupamentos de armazenamento](http://technet.microsoft.com/library/dn390929.aspx)

Para obter mais informações sobre os procedimentos de configuração do SQL Server, consulte [melhores práticas de desempenho para o SQL Server em virtual machines do Azure](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>Definições do SQL Server
No **definições do SQL Server**, reveja e modifique o prefixo de nome de máquina virtual do Olá do SQL Server, a versão do SQL Server, a conta de serviço do SQL Server e palavra-passe e Olá agenda de manutenção de aplicação de patches de automática SQL.

* **Prefixo de nome de servidor do SQL Server** é toocreate utilizado um nome para cada máquina virtual do SQL Server. Para este tutorial, utilize **sqlserver**. Olá modelo nomes Olá máquinas de virtuais do SQL Server *sqlserver-0* e *sqlserver-1*.
* **Versão do SQL Server** Olá versão do SQL Server. Para este tutorial utilização **SQL Server 2014**. Também pode optar por **SQL Server 2012** ou **SQL Server 2016**.
* **Nome de utilizador de conta de serviço do SQL Server** é o nome de conta de domínio Olá para Olá serviço do SQL Server. Para este tutorial, utilize **sqlservice**.
* **Palavra-passe** é Olá palavra-passe para Olá conta de serviço do SQL Server.  Utilize uma palavra-passe complexa. Confirme a palavra-passe de Olá.
* **Correção do SQL Server automática agenda de manutenção** identifica o dia de Olá da semana de Olá que Azure patches automaticamente Olá SQL Servers. Para este tutorial, escreva **Domingo**.
* **Hora de início de manutenção de correção do SQL Server automática** está na altura de Olá do dia para Olá região do Azure quando começa a aplicação de patches automática.

> [!NOTE]
> Olá aplicação de patches de janela para cada máquina virtual é escalonada por uma hora. Apenas uma máquina virtual é aplicada a uma interrupção de tooprevent tempo dos serviços.
>
>

![Definições do SQL Server](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Reveja as definições de Olá e, em seguida, clique em **OK**.

### <a name="summary"></a>Resumo
Na página de resumo de Olá, Azure valida as definições de Olá. Também pode transferir o modelo de Olá. Resumo de Olá de revisão. Clique em **OK**.

### <a name="buy"></a>Comprar
Este painel final contém **termos de utilização**, e **política de privacidade**. Reveja estas informações. Quando estiver pronto para máquinas virtuais do Azure toostart toocreate Olá e Olá todos os outros recursos necessários para o grupo de disponibilidade de Olá, clique em **criar**.

Olá portal do Azure cria o grupo de recursos de Olá e todos os recursos de Olá.

## <a name="monitor-deployment"></a>Implementação de monitor
Monitorizar o progresso da implementação Olá de Olá portal do Azure. Um ícone que representa a implementação de Olá é afixado automaticamente toohello dashboard do portal do Azure.

![Dashboard do Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Ligar tooSQL servidor
novas instâncias de Olá do SQL Server estão em execução em máquinas virtuais que tem ligação à internet endereços IP. Pode remoto ambiente de trabalho (RDP) diretamente tooeach do SQL Server máquina virtual.

tooRDP tooa SQL Server, siga estes passos:

1. De Olá dashboard do portal do Azure, certifique-se de que a implementação de Olá foi bem sucedida.
2. Clique em **recursos**.
3. No Olá **recursos** painel, clique em **sqlserver-0**, que é o nome do computador Olá de uma das máquinas virtuais Olá que está a executar o SQL Server.
4. No painel Olá **sqlserver-0**, clique em **Connect**. O browser pede-lhe se pretende tooopen ou guardar o objeto de ligação remota Olá. Clique em **abra**.
5. **Ligação de ambiente de trabalho remota** poderá avisá-lo nesse Olá não seja possível identificar o publicador desta ligação remota. Clique em **Ligar**.
6. Segurança do Windows pede ao utilizador tooenter seu endereço IP do credenciais tooconnect toohello do controlador de domínio primário Olá. Clique em **utilizar outra conta**. Para **nome de utilizador**, tipo **contoso\DomainAdmin**. Se configurou esta conta quando definir o nome de utilizador de administrador Olá no modelo de Olá. Utilize Olá palavra-passe complexa que escolheu quando configurou o modelo de Olá.
7. **Ambiente de trabalho remoto** poderá avisá-lo nesse computador remoto Olá não foi possível autenticar devido tooproblems com o seu certificado de segurança. Mostra nome do certificado de segurança de Olá. Se seguiu tutorial Olá, nome de Olá é **sqlserver 0.contoso.com**. Clique em **Sim**.

Está agora ligado com a máquina virtual do RDP toohello do SQL Server. Pode abrir o SQL Server Management Studio, ligue toohello predefinido instância do SQL Server e certifique-se de que esse grupo de disponibilidade Olá está configurado.
