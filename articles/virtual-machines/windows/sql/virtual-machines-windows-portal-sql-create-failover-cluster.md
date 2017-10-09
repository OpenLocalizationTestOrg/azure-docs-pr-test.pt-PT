---
title: aaaSQL FCI Servidor - Virtual Machines do Azure | Microsoft Docs
description: "Este artigo explica como toocreate instância de Cluster de ativação pós-falha do SQL Server em Azure Virtual Machines."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>Configurar a instância de Cluster de ativação pós-falha do SQL Server em Virtual Machines do Azure

Este artigo explica como toocreate uma SQL Server Cluster de ativação pós-falha (FCI) de instância em máquinas virtuais do Azure no modelo do Resource Manager. Esta solução usa [edição Datacenter do Windows Server 2016 espaços de armazenamento direto \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) como uma SAN de virtual baseado em software que sincroniza o armazenamento de Olá (discos de dados) entre Olá nós (as VMs do Azure) um Cluster do Windows. S2D é nova no Windows Server 2016.

Olá diagrama seguinte mostra solução completa de Olá em máquinas virtuais do Azure:

![Grupo de disponibilidade](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Olá precedente diagrama mostra:

- Dois virtual machines do Azure num cluster de ativação pós-falha do Windows. Quando uma máquina virtual está num cluster de ativação pós-falha também é denominado um *o nó de cluster*, ou *nós*.
- Cada máquina virtual tem dois ou mais discos de dados.
- S2D sincroniza os dados de Olá no disco de dados de Olá e apresenta Olá sincronizado armazenamento como um agrupamento de armazenamento.
- agrupamento de armazenamento Olá apresenta um cluster de ativação pós-falha do cluster (CSV) de volume partilhado toohello.
- função de cluster do SQL Server FCI Olá utiliza Olá CSV para Olá unidades de dados.
- Um carga do Azure balanceador toohold Olá endereço IP para Olá SQL Server FCI.
- Um conjunto de disponibilidade do Azure retém todos os recursos de Olá.

   >[!NOTE]
   >Todos os recursos do Azure estão no diagrama de Olá em Olá mesmo grupo de recursos.

Para obter detalhes sobre S2D, consulte [edição Datacenter do Windows Server 2016 espaços de armazenamento direto \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

S2D suportam dois tipos de arquiteturas - convergidas e hiperconvergida. arquitetura de Olá neste documento é hiperconvergida. Um infraestrutura hiperconvergida locais Olá armazenamento Olá mesmos servidores essa aplicação Olá em cluster do anfitrião. Nesta arquitetura, o armazenamento de Olá é em cada nó do SQL Server FCI.

### <a name="example-azure-template"></a>Exemplo modelo do Azure

Pode criar solução completa de Olá no Azure a partir de um modelo. Um exemplo de um modelo está disponível no Olá GitHub [modelos de início rápido do Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Este exemplo não concebido ou não está testado para qualquer carga de trabalho específica. Pode executar Olá modelo toocreate um FCI do SQL Server com o domínio de tooyour ligado de armazenamento S2D. Pode avaliar modelo Olá e modificá-lo para os fins pretendidos.

## <a name="before-you-begin"></a>Antes de começar

Existem algumas coisas que precisa de tooknow e algumas coisas que precisa no local antes de continuar.

### <a name="what-tooknow"></a>Que tooknow
Deve ter uma compreensão operacional das seguintes tecnologias de Olá:

- [Tecnologias de cluster do Windows](http://technet.microsoft.com/library/hh831579.aspx)
-  [Instâncias de Cluster de ativação pós-falha do SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).

Além disso, deve ter uma compreensão das seguintes tecnologias de Olá geral:

- [Solução convergida Hyper utilizando direta de espaços de armazenamento no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Grupos de recursos do Azure](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Que toohave

Antes de seguir as instruções de Olá neste artigo, já deverá ter:

- Uma subscrição do Microsoft Azure.
- Um domínio do Windows em máquinas virtuais do Azure.
- Uma conta com objetos de toocreate permissão na Olá máquina virtual do Azure.
- Uma rede virtual do Azure e a sub-rede com o espaço de endereços IP suficiente para Olá os seguintes componentes:
   - Ambas as máquinas virtuais.
   - endereço IP do cluster de ativação pós-falha do Olá.
   - Um endereço IP para cada FCI.
- DNS configurado no Olá rede do Azure, os controladores de domínio toohello a apontar.

Com estas pré-requisitos no local, pode continuar com a criação do cluster de ativação pós-falha. Step-by-Olá primeiro passo é Olá toocreate máquinas virtuais.

## <a name="step-1-create-virtual-machines"></a>Passo 1: Criar máquinas virtuais

1. Inicie sessão no toohello [portal do Azure](http://portal.azure.com) com a sua subscrição.

1. [Criar um conjunto de disponibilidade do Azure](../tutorial-availability-sets.md).

   disponibilidade de Olá definir grupos máquinas de virtuais em vários domínios de falhas e domínios de atualização. conjunto de disponibilidade de Olá certifica-se de que a aplicação não é afetada por pontos únicos de falha, como o comutador de rede Olá ou unidade de energia Olá de um bastidor de servidores.

   Se não tiver criado o grupo de recursos de Olá para as máquinas virtuais, fazê-lo ao criar um conjunto de disponibilidade do Azure. Se estiver a utilizar o conjunto de disponibilidade do Olá toocreate portal do Azure Olá, Olá os seguintes passos:

   - No portal do Azure Olá, clique em  **+**  tooopen Olá Azure Marketplace. Procurar **do conjunto de disponibilidade**.
   - Clique em **do conjunto de disponibilidade**.
   - Clique em **Criar**.
   - No Olá **criar conjunto de disponibilidade** painel, Olá de conjunto de valores a seguir:
      - **Nome**: um nome para o conjunto de disponibilidade de Olá.
      - **Subscrição**: subscrição do Azure.
      - **Grupo de recursos**: Se pretender toouse um grupo existente, clique em **utilizar existente** e selecione Olá grupo de Olá na lista pendente. Caso contrário, escolha **criar novo** e escreva um nome para o grupo de Olá.
      - **Localização**: Definir localização do olá onde planeia toocreate as máquinas virtuais.
      - **Domínios de falha**: utilizar a predefinição de Olá (3).
      - **Domínios de atualização**: utilizar a predefinição de Olá (5).
   - Clique em **criar** conjunto de disponibilidade de Olá toocreate.

1. Crie máquinas virtuais Olá no conjunto de disponibilidade de Olá.

   Aprovisione duas máquinas virtuais do SQL Server no conjunto de disponibilidade do Azure Olá. Para obter instruções, consulte [aprovisionar uma máquina virtual do SQL Server no portal do Azure de Olá](virtual-machines-windows-portal-sql-server-provision.md).

   Coloca as duas máquinas virtuais:

   - Nas Olá mesmo grupo de recursos do Azure que definir a sua disponibilidade está a ser.
   - No Olá mesmo que o controlador de domínio de rede.
   - Numa sub-rede com suficiente espaço de endereços IP para máquinas virtuais e todas as FCIs que poderão, eventualmente, utilizar neste cluster.
   - Olá conjunto de disponibilidade do Azure.   

      >[!IMPORTANT]
      >Não é possível definir ou alterar conjunto depois de criar uma máquina virtual de disponibilidade.

   Escolha uma imagem do Olá Azure Marketplace. Pode utilizar um mercado imagem com o que inclui o Windows Server e SQL Server ou Olá apenas Windows Server. Para obter mais informações, consulte [descrição geral do SQL Server em Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)

   imagens do SQL Server oficiais Olá no Olá galeria do Azure incluem uma instância do SQL Server instalada, plus software de instalação do SQL Server Olá e Olá necessária uma chave.

   Escolha imagem direita Olá de acordo com toohow que pretende toopay de licença do SQL Server Olá:

   - **Pagar por utilização licenciamento**: um custo por minuto Olá destas imagens inclui Olá de licenciamento do SQL Server:
      - **SQL Server 2016 Enterprise no Datacenter do Windows Server 2016**
      - **SQL Server 2016 padrão no Datacenter do Windows Server 2016**
      - **SQL Server 2016 Programador no Datacenter do Windows Server 2016**

   - **Bring-your-proprietário-licença (BYOL)**

      - **{BYOL} SQL Server 2016 Enterprise no Datacenter do Windows Server 2016**
      - **{BYOL} SQL Server 2016 padrão no Datacenter do Windows Server 2016**

   >[!IMPORTANT]
   >Depois de criar a máquina virtual de Olá, remova a instância de SQL Server do Olá autónomo pré-instaladas. Irá utilizar Olá pré-instaladas SQL multimédia toocreate hello do servidor SQL Server FCI depois de configurar o cluster de ativação pós-falha Olá e S2D.

   Em alternativa, pode utilizar imagens do Azure Marketplace com sistema de operativo apenas Olá. Escolha um **Datacenter do Windows Server 2016** imagem e instalar Olá SQL Server FCI depois de configurar o cluster de ativação pós-falha Olá e S2D. Esta imagem não contém suporte de instalação do SQL Server. Coloque o suporte de dados de instalação de Olá numa localização onde é possível executar a instalação do SQL Server Olá para cada servidor.

1. Depois do Azure cria as máquinas virtuais, ligar máquinas de virtuais tooeach com RDP.

   Quando liga pela primeira vez tooa máquinas com RDP, o computador de Olá pede-lhe se pretende tooallow toobe este PC detetável na rede de Olá. Clique em **Sim**.

1. Se estiver a utilizar uma das imagens da máquina virtual baseada no SQL Server de Olá, remova a instância do SQL Server de Olá.

   - No **programas e funcionalidades**, faça duplo clique **Microsoft SQL Server 2016 (64-bit)** e clique em **desinstalar/alterar**.
   - Clique em **remover**.
   - Selecione a instância predefinida de Olá.
   - Remova todas as funcionalidades em **serviços de motor de base de dados**. Não remova **partilhado funcionalidades**. Consulte Olá seguinte imagem:

      ![Remover funcionalidades](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Clique em **seguinte**e, em seguida, clique em **remover**.

1. <a name="ports"></a>Abrir portas de firewall de Olá.

   Em cada máquina virtual, abra Olá seguindo as portas do Olá Firewall do Windows.

   | Objetivo | A porta TCP | Notas
   | ------ | ------ | ------
   | SQL Server | 1433 | Porta normal para instâncias predefinida do SQL Server. Se utilizou uma imagem da Galeria de Olá, esta porta é automaticamente aberta.
   | Sonda de estado de funcionamento | 59999 | Abra qualquer porta TCP. Num passo posterior, configure o Balanceador de carga Olá [sonda do Estado de funcionamento](#probe) e Olá cluster toouse esta porta.  

1. Adicione armazenamento toohello máquina. Para obter informações detalhadas, consulte [adicionar armazenamento](../../../storage/common/storage-premium-storage.md).

   Ambas as máquinas virtuais precisa de discos de dados, pelo menos, dois.

   Anexe discos em bruto - não NTFS formatado discos.
      >[!NOTE]
      >Se anexar formatada com NTFS discos, só pode ativar S2D com verificação de elegibilidade sem disco.  

   Anexe um mínimo de dois Premium Storage (discos SSD) tooeach VM. Recomendamos que, pelo menos, P30 discos (1 TB).

   Anfitrião de conjunto de colocação em cache demasiado**só de leitura**.

   capacidade de armazenamento de Olá que utilizar em ambientes de produção depende da sua carga de trabalho. os valores de Olá descritos neste artigo são de demonstração e teste.

1. [Adicionar Olá máquinas virtuais tooyour pré-existente domínio](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Depois de Olá máquinas de virtuais são criadas e configuradas, pode configurar o cluster de ativação pós-falha Olá.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>Passo 2: Configurar Olá Cluster de ativação pós-falha do Windows com S2D

Olá passo seguinte consiste em cluster de ativação pós-falha de Olá tooconfigure com S2D. Neste passo, irá fazer Olá seguintes substeps:

1. Adicionar a funcionalidade de Clustering de ativação pós-falha do Windows
1. Validar cluster Olá
1. Criar cluster de ativação pós-falha de Olá
1. Criar o testemunho de nuvem Olá
1. Adicionar armazenamento

### <a name="add-windows-failover-clustering-feature"></a>Adicionar a funcionalidade de Clustering de ativação pós-falha do Windows

1. toobegin, ligar toohello primeira máquina de virtual com RDP utilizando uma conta de domínio que é um membro dos administradores locais e tem objetos de toocreate permissões no Active Directory. Utilize esta conta para o resto Olá configuração Olá.

1. [Adicionar a máquina virtual do tooeach funcionalidade Clustering de ativação pós-falha](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   funcionalidade de Clustering de ativação pós-falha tooinstall de Olá IU, Olá os seguintes passos em ambas as máquinas virtuais.
   - No **Gestor de servidor**, clique em **gerir**e, em seguida, clique em **para adicionar funções e funcionalidades**.
   - No **Assistente Adicionar funções e funcionalidades**, clique em **seguinte** quando obtiver demasiado**selecionar funcionalidades**.
   - No **selecionar funcionalidades**, clique em **Clustering de ativação pós-falha**. Inclua todas as funcionalidades necessárias e ferramentas de gestão de Olá. Clique em **adicionar funcionalidades**.
   - Clique em **seguinte** e, em seguida, clique em **concluir** funcionalidades de Olá tooinstall.

   tooinstall Olá Clustering de ativação pós-falha funcionalidade com o PowerShell, execute Olá seguinte script a partir de uma sessão do PowerShell de administrador dos Olá máquinas de virtuais.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Para referência, passos Olá Siga instruções de Olá no passo 3 de [convergida Hyper solução utilizando direta de espaços de armazenamento no Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Validar cluster Olá

Este guia refere-se tooinstructions em [validar cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Valide cluster Olá Olá IU ou com o PowerShell.

cluster de Olá toovalidate com Olá IU, Olá seguindo os passos de uma das máquinas virtuais Olá.

1. No **Gestor de servidor**, clique em **ferramentas**, em seguida, clique em **Gestor de clusters de ativação pós-falha**.
1. No **Gestor de clusters de ativação pós-falha**, clique em **ação**, em seguida, clique em **validar configuração...** .
1. Clique em **Seguinte**.
1. No **selecionar servidores ou um Cluster**, nome do tipo Olá de ambas as máquinas virtuais.
1. No **opções de teste**, escolha **executar apenas os testes selecionados**. Clique em **Seguinte**.
1. No **testar seleção**, incluir todos os testes, exceto **armazenamento**. Consulte Olá seguinte imagem:

   ![Validar testes](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. Clique em **Seguinte**.
1. No **confirmação**, clique em **seguinte**.

Olá **validar um Assistente de configuração** executa Olá testes de validação.

cluster de Olá toovalidate com o PowerShell, execute Olá seguinte script a partir de uma sessão do PowerShell de administrador dos Olá máquinas de virtuais.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Depois de validar cluster Olá, crie o cluster de ativação pós-falha de Olá.

### <a name="create-hello-failover-cluster"></a>Criar cluster de ativação pós-falha de Olá

Este guia refere-se demasiado[Criar cluster de ativação pós-falha de Olá](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

cluster de ativação pós-falha do toocreate Olá, tem de:
- nomes de Olá das máquinas virtuais Olá que fique Olá nós de cluster.
- Um nome para o cluster de ativação pós-falha Olá
- Um endereço IP para o cluster de ativação pós-falha de Olá. Pode utilizar um endereço IP que não seja utilizado Olá mesma rede virtual do Azure e como Olá nós de cluster.

Olá PowerShell a seguir cria um cluster de ativação pós-falha. Atualizar o script de Olá com nomes de Olá de nós de Olá (nomes de máquina virtual Olá) e um endereço IP disponível do Olá VNET do Azure:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Criar um testemunho de nuvem

Testemunho de nuvem é um novo tipo de testemunho de quórum do cluster armazenado num Blob de armazenamento do Azure. Esta ação remove a necessidade de Olá de uma VM separada que aloja uma partilha de testemunho.

1. [Criar um testemunho de nuvem para o cluster de ativação pós-falha de Olá](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Crie um contentor de blob.

1. Guarde as chaves de acesso de Olá e o URL do contentor Olá.

1. Configure o testemunho de quórum de cluster de cluster de ativação pós-falha de Olá. Ver, [configurar testemunho de quórum de Olá na interface de utilizador Olá]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) no Olá IU.

### <a name="add-storage"></a>Adicionar armazenamento

discos Olá S2D necessário toobe vazio e sem partições ou outros dados. Siga tooclean discos [Olá passos neste guia](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Ativar loja direta de espaços \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   Olá seguir PowerShell permite direta de espaços de armazenamento.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   No **Gestor de clusters de ativação pós-falha**, agora, pode ver o agrupamento de armazenamento Olá.

1. [Criar um volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Uma das funcionalidades de Olá de S2D é que este cria automaticamente um agrupamento de armazenamento se a ativar. Agora, está pronto toocreate um volume. Olá PowerShell commandlet `New-Volume` automatiza o processo de criação do volume Olá, incluindo formatação, adicionar toohello cluster e criar um volume partilhado de cluster (CSV). Olá seguinte exemplo cria um 800 gigabyte (GB) CSV.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Depois de concluída este comando, um volume de 800 GB está montado como um recurso de cluster. é volume Olá `C:\ClusterStorage\Volume1\`.

   Olá diagrama a seguir mostra um volume partilhado de cluster com S2D:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>Passo 3: Testar a ativação pós-falha de cluster de ativação pós-falha

No Gestor de clusters de ativação pós-falha, certifique-se de que é possível mover toohello de recursos de armazenamento Olá outro nó de cluster. Se pode ligar cluster de ativação pós-falha de toohello com **Gestor de clusters de ativação pós-falha** e mover o armazenamento de Olá de um nó toohello outros, está pronto tooconfigure Olá FCI.

## <a name="step-4-create-sql-server-fci"></a>Passo 4: Criar do SQL Server FCI

Depois de ter configurado o cluster de ativação pós-falha de Olá e todos os componentes de cluster, incluindo o armazenamento, pode criar Olá SQL Server FCI.

1. Ligar toohello primeira máquina de virtual com RDP.

1. No **Gestor de clusters de ativação pós-falha**, certifique-se todos os recursos principais do cluster estão na máquina de virtual primeiro Olá. Se necessário, mova todas as máquinas de toothis recursos.

1. Localize o suporte de dados de instalação de Olá. Se a máquina virtual de Olá utiliza uma das imagens de Azure Marketplace Olá, suporte de dados de Olá está localizado em `C:\SQLServer_<version number>_Full`. Clique em **configuração**.

1. No Olá **Centro de instalação do SQL Server**, clique em **instalação**.

1. Clique em **instalação de cluster de ativação pós-falha do novo SQL Server**. Siga as instruções de Olá Olá de tooinstall Olá assistente SQL Server FCI.

   diretórios de dados FCI Olá necessário toobe no armazenamento em cluster. Com S2D, não é um disco partilhado, mas um volume de tooa de ponto de montagem em cada servidor. S2D sincroniza volume Olá entre ambos os nós. volume de Olá é apresentada toohello cluster como volume partilhado de cluster. Utilize o ponto de montagem CSV Olá para diretórios de dados de Olá.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Depois de concluir o Assistente de Olá, a configuração irá instalar um FCI do SQL Server no primeiro nó de Olá.

1. Depois do programa de configuração instala com êxito Olá FCI no primeiro nó de Olá, ligar toohello segundo nó com RDP.

1. Abra Olá **Centro de instalação do SQL Server**. Clique em **instalação**.

1. Clique em **cluster de ativação pós-falha do SQL Server do adicionar nó tooa**. Siga as instruções de Olá no SQL server do Olá assistente tooinstall e adicione toohello este servidor FCI.

   >[!NOTE]
   >Se utilizou uma imagem de galeria do Azure Marketplace com o SQL Server, ferramentas do SQL Server foram incluídas com Olá imagem. Se não utilizou esta imagem, instale o ferramentas do SQL Server de Olá separadamente. Consulte [transferir SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>Passo 5: Criar Balanceador de carga do Azure

Nas máquinas virtuais do Azure, clusters, utilize um toohold de Balanceador de carga um endereço IP que tem toobe num nó de cluster de cada vez. Nesta solução, o Balanceador de carga Olá detém do endereço IP Olá Olá SQL Server FCI.

[Criar e configurar um balanceador de carga do Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Criar Balanceador de carga Olá no Olá portal do Azure

Balanceador de carga de Olá toocreate:

1. No portal do Azure Olá, visite toohello grupo de recursos com Olá máquinas de virtuais.

1. Clique em **+ adicionar**. Olá pesquisa Marketplace para **Balanceador de carga**. Clique em **Balanceador de carga**.

1. Clique em **Criar**.

1. Configure o Balanceador de carga Olá com:

   - **Nome**: um nome que identifique o Balanceador de carga Olá.
   - **Tipo**: Balanceador de carga Olá pode ser públicas ou privadas. Um balanceador de carga privada pode ser acedido a partir do Olá mesma VNET. Aplicações mais Azure podem utilizar um balanceador de carga privada. Se a aplicação tem acesso tooSQL servidor diretamente através da Internet de Olá, utilize um balanceador de carga público.
   - **Rede virtual**: Olá mesmo como máquinas de virtuais Olá de rede.
   - **Sub-rede**: Olá mesma sub-rede que Olá máquinas de virtuais.
   - **Endereço IP privado**: Olá mesmo endereço IP que atribuídos recursos de rede de cluster do toohello SQL Server FCI.
   - **subscrição**: subscrição do Azure.
   - **Grupo de recursos**: Utilize Olá mesmo grupo de recursos como as máquinas virtuais.
   - **Localização**: Utilize Olá mesma localização do Azure que as máquinas virtuais.
   Consulte Olá seguinte imagem:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Configurar o conjunto de back-end de Balanceador de carga Olá

1. Devolver toohello grupo de recursos do Azure com as máquinas virtuais de Olá e localize o Balanceador de carga novo Olá. Poderá ter vista de Olá toorefresh no Olá grupo de recursos. Clique em Balanceador de carga Olá.

1. No painel de Balanceador de carga Olá, clique em **conjuntos back-end**.

1. Clique em **+ adicionar** tooadd um conjunto de back-end.

1. Escreva um nome para o conjunto de back-end Olá.

1. Clique em **adicionar uma máquina virtual**.

1. No Olá **escolher as máquinas virtuais** painel, clique em **escolher um conjunto de disponibilidade**.

1. Escolha o conjunto de disponibilidade de Olá que colocou Olá do SQL Server máquinas virtuais.

1. No Olá **escolher as máquinas virtuais** painel, clique em **escolher máquinas de virtuais Olá**.

   O portal do Azure deve aspeto Olá seguinte imagem:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Clique em **selecione** no Olá **escolher as máquinas virtuais** painel.

1. Clique em **OK** duas vezes.

### <a name="configure-a-load-balancer-health-probe"></a>Configurar uma sonda de estado de funcionamento do Balanceador de carga

1. No painel de Balanceador de carga Olá, clique em **sondas de estado de funcionamento**.

1. Clique em **+ adicionar**.

1. No Olá **sonda do Estado de funcionamento de adicionar** painel, <a name="probe"> </a>definir parâmetros de pesquisa de estado de funcionamento de Olá:

   - **Nome**: um nome para a sonda de estado de funcionamento de Olá.
   - **Protocolo**: TCP.
   - **Porta**: Definir tooan porta TCP disponível. Esta porta necessita de uma porta de firewall aberta. Olá utilize [mesma porta](#ports) definido para a sonda de estado de funcionamento de Olá na firewall de Olá.
   - **Intervalo**: 5 segundos.
   - **Limiar de mau estado de funcionamento**: 2 falhas consecutivas.

1. Clique em OK.

### <a name="set-load-balancing-rules"></a>Definir regras de balanceamento de carga

1. No painel de Balanceador de carga Olá, clique em **as regras de balanceamento de carga**.

1. Clique em **+ adicionar**.

1. Definir os parâmetros de regras de balanceamento de carga de Olá:

   - **Nome**: um nome para as regras de balanceamento de carga de Olá.
   - **Endereço IP de front-end**: Utilize um endereço IP Olá para Olá recurso de rede de cluster do SQL Server FCI.
   - **Porta**: definir para Olá a porta TCP do SQL Server FCI. porta de instância Olá predefinida é 1433.
   - **Porta de back-end**: este valor utiliza Olá a mesma porta como Olá **porta** valor quando ativar **IP flutuante (devolução direta do servidor)**.
   - **Conjunto back-end**: nome conjunto de back-end de Olá de utilização que configurou anteriormente.
   - **Sonda de estado de funcionamento**: sonda de estado de funcionamento de Olá utilização que configurou anteriormente.
   - **Persistência da sessão**: nenhuma.
   - **Tempo limite (minutos) de inatividade**: 4.
   - **Vírgula flutuante (devolução direta do servidor) de IP**: ativado

1. Clique em **OK**.

## <a name="step-6-configure-cluster-for-probe"></a>Passo 6: Configurar o cluster para a sonda

Definir o parâmetro de porta de sonda de cluster Olá no PowerShell.

tooset Olá parâmetro de porta de sonda de cluster, Atualize as variáveis no Olá seguinte script do seu ambiente.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>Passo 7: Testar a ativação pós-falha da FCI

Testar a ativação pós-falha de Olá a funcionalidade de cluster toovalidate FCI. Olá os seguintes passos:

1. Ligar tooone de nós de cluster do SQL Server FCI Olá com RDP.

1. Abra **Gestor de clusters de ativação pós-falha**. Clique em **funções**. Aviso de nó que possui a função de SQL Server FCI Olá.

1. Clique com botão direito função do SQL Server FCI Olá.

1. Clique em **mover** e clique em **melhor nó possível**.

**Gestor de clusters de ativação pós-falha** mostra Olá função e respetivos recursos fique offline. Olá recursos, em seguida, mover e ficar online Olá no outro nó.

### <a name="test-connectivity"></a>Testar conectividade

conectividade tootest, registo na máquina virtual tooanother Olá mesma rede virtual. Abra **SQL Server Management Studio** e ligar o nome do SQL Server FCI toohello.

>[!NOTE]
>Se necessário, pode [transferir SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Limitações
Máquinas virtuais do Azure, coordenador de transações distribuídas ' (DTC) da Microsoft não é suportada em FCIs porque Olá porta RPC não é suportado pelo balanceador de carga Olá.

## <a name="see-also"></a>Veja Também

[A configuração S2D com o ambiente de trabalho remoto (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Hyper-convergido solução com espaços de armazenamento diretos](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Descrição geral direta do espaço de armazenamento](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[Suporte do SQL Server para S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
