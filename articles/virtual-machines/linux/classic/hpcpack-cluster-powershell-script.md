---
title: aaaPowerShell script toodeploy cluster HPC do Linux | Microsoft Docs
description: "Executar um toodeploy de script do PowerShell de um cluster do Linux HPC Pack 2012 R2 em máquinas virtuais do Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Criar um cluster de computação de alto desempenho (HPC) do Linux com script de implementação de HPC Pack IaaS Olá
Execute toodeploy de script do PowerShell de implementação do Olá HPC Pack IaaS um cluster HPC Pack 2012 R2 completado para cargas de trabalho do Linux em máquinas virtuais do Azure. cluster de Olá é composta por um nó principal associados ao Active Directory com o Windows Server e o Microsoft HPC Pack e nós de computação que execute um dos Olá distribuições Linux suportadas pelo pacote HPC. Se quiser toodeploy um cluster HPC Pack em cargas de trabalho do Azure para Windows, consulte [criar um cluster Windows HPC com Olá script de implementação de HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Também pode utilizar um toodeploy de modelo do Azure Resource Manager um cluster HPC Pack. Por exemplo, consulte [criar um cluster HPC connosco de computação do Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Olá script do PowerShell descrito neste artigo cria um cluster do Microsoft HPC Pack 2012 R2 no Azure utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.
> Além disso, o script Olá descrito neste artigo não suporta o HPC Pack 2016.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Ficheiro de configuração de exemplo
Olá seguinte ficheiro de configuração cria um controlador de domínio e floresta de domínio e implementa um cluster HPC Pack que tem um nó principal com bases de dados locais e 10 nós de computação do Linux. Todos os serviços de cloud Olá são criados diretamente no Oriental como localização Olá. Olá nós de computação do Linux são criados em dois serviços de nuvem e duas contas de armazenamento (ou seja, *MyLnxCN-0001 e* para *MyLnxCN 0005* no *MyLnxCNService01* e *mylnxstorage01*, e *MyLnxCN 0006* para *MyLnxCN 0010* no *MyLnxCNService02* e *mylnxstorage02* ). nós de computação Olá são criados a partir de uma imagem de Linux do OpenLogic CentOS versão 7.0. 

Substitua os seus próprios valores para o nome da subscrição e os nomes de conta e o serviço de Olá.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>Resolução de problemas
* **Erro "Não existe VNet"**. Se executar toodeploy de script de implementação de HPC Pack IaaS Olá vários clusters no Azure em simultâneo com uma subscrição, uma ou mais implementações podem falhar com o erro de Olá "VNet *VNet\_nome* não existe".
  Se este erro ocorrer, volte a executar script de Olá Olá falha na implementação.
* **Problema ao aceder ao hello Internet da rede virtual do Azure de Olá**. Se criar um cluster HPC Pack com um novo controlador de domínio utilizando o script de implementação hello, ou manualmente promover um controlador de toodomain VM de nó principal, podem ocorrer problemas de ligação Olá VMs na rede virtual do Azure de Olá toohello Internet. Isto pode ocorrer se um servidor DNS do reencaminhador é automaticamente configurado no controlador de domínio Olá, e este servidor DNS do reencaminhador não resolve corretamente.
  
    toowork em torno este problema, inicie sessão no controlador de domínio de toohello e a definição de configuração do reencaminhador de Olá remover ou configurar um servidor DNS do reencaminhador válido. toodo, clique no Gestor de servidor **ferramentas** > **DNS** tooopen Gestor de DNS e, em seguida, faça duplo clique **reencaminhadores**.

## <a name="next-steps"></a>Passos seguintes
* Consulte [começar connosco de computação do Linux num cluster HPC Pack no Azure](hpcpack-cluster.md) para obter informações sobre as distribuições Linux suportadas, mover dados e a submissão de cluster HPC Pack de tooan de tarefas com o Linux nós de computação.
* Para tutoriais que utilizam Olá script toocreate um cluster e executam uma carga de trabalho do Linux HPC, consulte:
  * [Executar NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-namd.md)
  * [Executar OpenFOAM com o Microsoft HPC Pack em nós de computação do Linux no Azure](hpcpack-cluster-openfoam.md)
  * [Executar ESTRELA-CCM + com o Microsoft HPC Pack no Linux nós de computação no Azure](hpcpack-cluster-starccm.md)

