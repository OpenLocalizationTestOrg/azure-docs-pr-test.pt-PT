---
title: "aaaLinux computação VMs num cluster HPC Pack | Microsoft Docs"
description: "Saiba como toocreate e utilizar um pacote HPC cluster no Azure para Linux elevado desempenho informática cargas de trabalho (HPC)"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Introdução aos nós de computação do Linux num cluster HPC Pack no Azure
Configurar um [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) com uma distribuição Linux suportada de nós de computação de cluster no Azure que contém um nó principal com o Windows Server e várias. Explore os dados de toomove de opções entre os nós do Linux Olá e nó principal de Windows hello do cluster de Olá. Saiba como toosubmit Linux HPC tarefas toohello cluster.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Um nível elevado, hello diagrama seguinte mostra cluster HPC Pack de Olá criar e trabalhar com.

![Cluster de pacote HPC connosco do Linux][scenario]

Para outra opções toorun Linux HPC cargas de trabalho no Azure, consulte [recursos técnicos para batch e computação de alto desempenho](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Implementar um cluster de pacote HPC connosco de computação do Linux
Este artigo mostra duas opções toodeploy um cluster HPC Pack no Azure connosco de computação do Linux. Ambos os métodos de utilizam uma imagem do Marketplace do Windows Server com o nó principal do HPC Pack toocreate Olá. 

* **Modelo Azure Resource Manager** -utilizar um modelo a partir do Olá Azure Marketplace ou um modelo de início rápido da Comunidade Olá, tooautomate a criação do cluster de Olá no modelo de implementação do Resource Manager Olá. Por exemplo, Olá [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no Olá Azure Marketplace cria uma infraestrutura de cluster HPC Pack concluída para o Linux HPC cargas de trabalho.
* **Script do PowerShell** -Olá utilize [script de implementação do Microsoft HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate uma implementação completa do cluster no modelo de implementação clássica Olá. Este script do PowerShell do Azure utiliza uma imagem de VM de pacote HPC no Olá Azure Marketplace para a implementação rápida e fornece um conjunto abrangente de toodeploy de parâmetros de configuração de nós de computação do Linux.

Para obter mais informações sobre as opções de implementação de cluster HPC Pack no Azure, consulte [opções toocreate e gerir um cluster de computação de alto desempenho (HPC) no Azure com o Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Pré-requisitos
* **Subscrição do Azure** -pode utilizar uma subscrição em qualquer um dos Olá serviço Global do Azure ou do Azure China. Se não tiver uma conta, pode criar um [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
* **Quota de núcleos** -poderá ter de quota de Olá tooincrease de núcleos, especialmente se optar por toodeploy vários nós do cluster sem especializados tamanhos de VM. tooincrease uma quota, abra um pedido de suporte online do cliente, sem encargos.
* **As distribuições do Linux** -atualmente HPC Pack suporta Olá seguir as distribuições do Linux para nós de computação. Pode utilizar Marketplace as versões destes distribuições, quando disponíveis, ou forneça o seu próprio.
  
  * **Com base em centOS**: 6.5 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6.8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12 SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 para HPC, SLES 12 para HPC (Premium)
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > rede de Azure RDMA Olá toouse com um dos tamanhos de VM Olá com capacidade RDMA, especifique uma imagem do SUSE Linux Enterprise Server 12 HPC ou baseada em CentOS HPC de Olá Azure Marketplace. Para obter mais informações, consulte [tamanhos de VM de computação de elevado desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Pré-requisitos adicionais toodeploy Olá cluster utilizando o script de implementação de HPC Pack IaaS Olá:

* **Computador cliente** -precisa de um script de implementação do cliente baseada em Windows computador toorun Olá cluster.
* **O Azure PowerShell** - [instalar e configurar o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.
* **Script de implementação de HPC Pack IaaS** - transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Pode verificar a versão de Olá do script Olá executando `.\New-HPCIaaSCluster.ps1 –Version`. Este artigo baseia-se numa versão 4.4.1 ou posterior do script de Olá.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Opção de implementação 1. Utilizar um modelo do Resource Manager
1. Aceda toohello [cluster HPC Pack para cargas de trabalho do Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) modelo no Olá Azure Marketplace e clique em **implementar**.
2. No Olá portal do Azure, reveja as informações de Olá e, em seguida, clique em **criar**.
   
    ![Criação do portal][portal]
3. No Olá **Noções básicas** painel, introduza um nome para o cluster Olá, que também os nomes de nó principal do Olá VM. Pode escolher um grupo de recursos existente ou crie um grupo para implementação de Olá numa localização que seja tooyou disponível. Olá localização afeta a disponibilidade de Olá de determinados tamanhos de VM e outros serviços do Azure (consulte [produtos disponíveis por região](https://azure.microsoft.com/regions/services/)).
4. No Olá **aceda a definições de nó** painel, para uma primeira implementação, pode aceitar geralmente as predefinições de Olá. 
   
   > [!NOTE]
   > Olá **URL de scripts pós-configuração** é opcional definição toospecify um script do Windows PowerShell publicamente disponível que pretende que toorun no nó principal do Olá VM depois de se encontra em execução. 
   > 
   > 
5. No Olá **definições de nó de computação** painel, selecione um padrão de nomenclatura para nós de Olá, o número de Olá e o tamanho de nós de Olá e Olá toodeploy de distribuição de Linux.
6. No Olá **as definições de infraestrutura** painel, introduza os nomes de rede virtual Olá e do Active Directory domínio, domínio e credenciais de administrador da VM e um padrão de nomenclatura Olá contas do storage.
   
   > [!NOTE]
   > Pacote HPC utiliza Olá do Active Directory tooauthenticate cluster aos utilizadores de domínio. 
   > 
   > 
7. Depois de executar testes de validação de Olá e reveja os termos de Olá de utilização, clique em **Compra**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Opção de implementação 2. Utilizar script de implementação de IaaS Olá
Seguem-se cluster de Olá toodeploy de pré-requisitos adicionais utilizando o script de implementação de HPC Pack IaaS Olá:

* **Computador cliente** -precisa de um script de implementação do cliente baseada em Windows computador toorun Olá cluster.
* **O Azure PowerShell** - [instalar e configurar o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.
* **Script de implementação de HPC Pack IaaS** - transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Pode verificar a versão de Olá do script Olá executando `.\New-HPCIaaSCluster.ps1 –Version`. Este artigo baseia-se numa versão 4.4.1 ou posterior do script de Olá.

**Ficheiro de configuração XML**

Olá HPC Pack IaaS script de implementação utiliza um ficheiro de configuração XML, como cluster HPC Olá toodescribe de entrada. Olá seguinte ficheiro de configuração de exemplo Especifica um cluster pequeno constituída por um nó principal do HPC Pack e dois nós de computação do Linux do A7 CentOS 7.0 de tamanho. 

Modificar o ficheiro de Olá conforme necessário para o seu ambiente e a configuração de cluster pretendido e guarde-o com um nome, como HPCDemoConfig.xml. Por exemplo, terá de toosupply nome da sua subscrição e um nome de conta de armazenamento exclusivas e o nome do serviço em nuvem. Além disso, poderá toochoose outro suportado Linux imagem Olá nós de computação. Para obter mais informações sobre elementos Olá no ficheiro de configuração de Olá, consulte o ficheiro de Manual.rtf de Olá na pasta de script de Olá e [criar um cluster HPC com Olá script de implementação de HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**Olá toorun script de implementação do IaaS do HPC Pack**

1. Abra o Windows PowerShell no computador de cliente Olá como administrador.
2. Alterar pasta do toohello diretório onde está o script de Olá instalado (E:\IaaSClusterScript neste exemplo).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Execute Olá cluster HPC Pack do comando toodeploy Olá a seguir. Este exemplo assume que o ficheiro configuração Olá está localizado na E:\HPCDemoConfig.xml
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Porque Olá **AdminPassword** não está especificado no Olá precedente comandos, é pedido tooenter Olá palavra-passe utilizador *MyAdminName*.
   
    b. script de Olá, em seguida, inicia o ficheiro de configuração de Olá toovalidate. Pode demorar até tooseveral minutos dependendo da ligação de rede Olá.
   
    ![Validação][validate]
   
    c. Depois de passaram validações, o script Olá lista toocreate de recursos de cluster Olá. Introduza *Y* toocontinue.
   
    ![Recursos][resources]
   
    d. script de Olá inicia toodeploy Olá HPC Pack cluster e concluir a configuração de Olá sem mais passos manuais. Pode executar o script de Olá durante vários minutos.
   
    ![Implementação][deploy]
   
   > [!NOTE]
   > Neste exemplo, o script de Olá gera um ficheiro de registo automaticamente o desde Olá **- LogFile** parâmetro não está especificado. Olá registos não são escritos em tempo real, mas são recolhidos no fim de Olá de validação de Olá e implementação de Olá. Se Olá PowerShell processo for interrompido enquanto está a executar o script de Olá, alguns registos serão perdidos.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Ligar o nó principal toohello
Depois de implementar um cluster HPC Pack de Olá no Azure, [estabelecer ligação ao ambiente de trabalho remoto](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) através de VM de nó principal do toohello Olá credenciais de domínio que forneceu quando implementou o cluster de Olá (por exemplo, *hpc\\ clusteradmin*). Gerir o cluster de Olá do nó principal Olá.

No nó principal Olá, inicie o Gestor de clusters HPC toocheck Estado Olá cluster HPC Pack de Olá. Pode gerir e monitorizar nós de computação do Linux hello mesma forma que trabalha com o Windows nós de computação. Por exemplo, consulte nós do Linux Olá listados no **gestão de recursos** (estes nós são implementados com Olá **LinuxNode** modelo).

![Gestão de nó][management]

Consulte também nós Linux Olá Olá **mapa térmico** vista.

![Mapa térmico][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Como toomove dados num cluster connosco do Linux
Tem vários dados de toomove escolhas entre os nós do Linux e o nó principal de Windows hello do cluster de Olá. Seguem-se três métodos comuns, descritos com maior detalhe em Olá seguintes secções:

* **Ficheiros do Azure** -expõe um gerido toostore dados do SMB ficheiro partilha de ficheiros no armazenamento do Azure. Nós do Windows e nós do Linux podem montar uma partilha de ficheiros do Azure como uma unidade ou pasta no Olá mesmo tempo, mesmo que está a ser implementados em redes virtuais diferentes.
* **Nó principal SMB partilhar** -monta uma pasta partilhada de Windows padrão de nó principal Olá em nós do Linux.
* **O servidor NFS do head nó** -fornece uma solução de partilha de ficheiros para um ambiente misto do Windows e Linux.

### <a name="azure-file-storage"></a>File storage do Azure
Olá [ficheiros do Azure](https://azure.microsoft.com/services/storage/files/) serviço expõe partilhas de ficheiros utilizando o protocolo SMB 2.1 padrão do Olá. Serviços de nuvem e as VMs do Azure podem partilhar dados de ficheiros entre componentes da aplicação através de partilhas montadas e as aplicações no local podem aceder a dados de ficheiros numa partilha através de Olá API do armazenamento de ficheiros. 

Para obter passos detalhados toocreate um ficheiro de Azure partilhar e montá-la no nó principal Olá, consulte [introdução ao File storage do Azure no Windows](../../../storage/files/storage-how-to-use-files-windows.md). partilha de ficheiros de Azure Olá toomount nós do Linux Olá, consulte [como toouse File storage do Azure com o Linux](../../../storage/files/storage-how-to-use-files-linux.md). tooset cópias de segurança persistentes ligações, consulte [Persisting ligações tooMicrosoft ficheiros do Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

No seguinte exemplo de Olá, crie uma partilha de ficheiros do Azure numa conta de armazenamento. Olá toomount partilha em Olá nó principal, abra uma linha de comandos e introduza Olá os seguintes comandos:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

Neste exemplo, allvhdsje é o nome da sua conta de armazenamento, storageaccountkey é a chave de conta de armazenamento e rdma é Olá nome da partilha de ficheiros do Azure. partilha de ficheiros do Azure Olá está montada como z no nó principal Olá.

partilha de ficheiros de Azure Olá toomount nós do Linux, execute um **clusrun** comando no nó principal Olá. **[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  é uma ferramenta toocarry útil do HPC Pack realizar tarefas administrativas em vários nós. (Consulte também [Clusrun para nós do Linux](#Clusrun-for-Linux-nodes) neste artigo.)

Abra uma janela do Windows PowerShell e introduza Olá os seguintes comandos:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

comando primeiro Olá cria uma pasta denominada /rdma em todos os nós no grupo de LinuxNodes Olá. segundo comando de Olá monta Olá ficheiros do Azure partilha allvhdsjw.file.core.windows.net/rdma numa pasta de /rdma Olá com dir e ficheiro too777 de conjunto de bits de modo. No segundo comando Olá, allvhdsje é o nome da sua conta de armazenamento e storageaccountkey é a chave de conta de armazenamento.

> [!NOTE]
> Olá "\`" símbolo segundo comando de Olá é um símbolo de escape para o PowerShell. "\`,"significa que Olá"," (vírgulas caráter) é uma parte do comando de Olá.
> 
> 

### <a name="head-node-share"></a>Partilha de nó principal
Em alternativa, monte uma pasta partilhada de nó principal Olá em nós do Linux. Fornece de uma partilha de ficheiros de tooshare de forma mais simples Olá, mas o nó principal Olá e todos os nós do Linux tem de ser implementados numa Olá mesma rede virtual. Seguem-se passos de Olá.

1. Crie uma pasta no nó principal Olá e partilhe-tooEveryone com permissões de leitura/escrita. Por exemplo, partilhar D:\OpenFOAM no nó principal do Olá como \\CentOS7RDMA HN\OpenFOAM. Aqui CentOS7RDMA HN é Olá nome de anfitrião do nó principal Olá.
   
    ![Permissões de partilha de ficheiros][fileshareperms]
   
    ![Partilha de ficheiros][filesharing]
2. Abra uma janela do Windows PowerShell e execute Olá os seguintes comandos:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

comando primeiro Olá cria uma pasta denominada /openfoam em todos os nós no grupo de LinuxNodes Olá. segundo comando de Olá monta Olá partilhado pasta //CentOS7RDMA-HN/OpenFOAM numa pasta Olá com dir e ficheiro too777 de conjunto de bits de modo. Olá nome de utilizador e palavra-passe no comando Olá devem ser Olá nome de utilizador e palavra-passe de um utilizador de cluster no nó principal Olá. (Consulte [adicionar ou remover utilizadores de cluster](https://technet.microsoft.com/library/ff919330.aspx).)

> [!NOTE]
> Olá "\`" símbolo segundo comando de Olá é um símbolo de escape para o PowerShell. "\`,"significa que Olá"," (vírgulas caráter) é uma parte do comando de Olá.
> 
> 

### <a name="nfs-server"></a>Servidor NFS
Olá serviço NFS permite-lhe tooshare e migra ficheiros entre computadores que executam o sistema de operativo Olá Windows Server 2012 utilizando o protocolo SMB de Olá e os computadores baseados em Linux através do protocolo NFS de Olá. Olá servidor NFS e todos os outros nós têm toobe implementado na Olá mesma rede virtual. Proporciona uma melhoria da compatibilidade com os nós do Linux comparada a uma partilha SMB. Por exemplo, suporta ligações de ficheiro.

1. tooinstall e configurar um servidor NFS, siga os passos Olá [servidor para a partilha primeiro do sistema de ficheiros de rede ponto a ponto](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Por exemplo, crie uma partilha NFS com o nome nfs com Olá seguintes propriedades:
   
    ![Autorização de NFS][nfsauth]
   
    ![Permissões de partilha NFS][nfsshare]
   
    ![Permissões NTFS de NFS][nfsperm]
   
    ![Propriedades de gestão de NFS][nfsmanage]
2. Abra uma janela do Windows PowerShell e execute Olá os seguintes comandos:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   comando primeiro Olá cria uma pasta denominada /nfsshared em todos os nós no grupo de LinuxNodes Olá. Olá segundo comando monta Olá NFS partilhar CentOS7RDMA HN: / nfs para Olá pasta. Aqui CentOS7RDMA HN: / nfs é o caminho de remoto Olá da sua partilha NFS.

## <a name="how-toosubmit-jobs"></a>Como toosubmit tarefas
Existem várias formas toosubmit tarefas toohello HPC Pack cluster:

* Gestor de clusters HPC ou GUI de Gestor de tarefas HPC
* HPC web portal
* API REST

Submissão de tarefa toohello cluster no Azure através do portal web do Olá HPC e ferramentas de HPC Pack GUI são Olá iguais a nós de computação do Windows. Consulte [Gestor de tarefas HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) e [como toosubmit tarefas a partir de um computador de cliente no local](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

tarefas de toosubmit através de Olá REST API, consulte demasiado[criar e submeter tarefas ao utilizar Olá API de REST no Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). toosubmit tarefas de um cliente Linux, consulte também o exemplo de Python toohello no Olá [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Clusrun para nós do Linux
Olá HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) ferramenta pode ser utilizado tooexecute comandos em nós do Linux ou através de uma linha de comandos ou o Gestor de clusters HPC. Seguem-se alguns exemplos básicos.

* Mostra os nomes de utilizador atual em todos os nós no cluster de Olá.
  
    ```command
    clusrun whoami
    ```
* Instalar Olá **gdb** ferramenta de depurador com **yum** em todos os nós Olá linuxnodes grupo e, em seguida, reinicie nós Olá após 10 minutos.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Criar um script de shell que apresenta cada número entre 1 e 10 para um segundo em cada nó de Linux num cluster de Olá, executá-la e mostrar um resultado de nós de Olá imediatamente.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Poderá ser necessário toouse determinados carateres de escape **clusrun** comandos. Como é mostrado neste exemplo, utilize ^ no Olá de tooescape linha de comandos ">" símbolo.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* Tente como aumentar verticalmente Olá cluster tooa grande número de nós, ou tentar executar uma carga de trabalho do Linux no cluster de Olá. Por exemplo, consulte [NAMD executar com o Microsoft HPC Pack no Linux nós de computação em Azure](hpcpack-cluster-namd.md).
* Tente um cluster com [VMs com capacidade RDMA, de computação intensiva](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI as cargas de trabalho. Por exemplo, consulte [cluster OpenFOAM executar com o Microsoft HPC Pack num RDMA Linux no Azure](hpcpack-cluster-openfoam.md).
* Se estiver interessado em trabalhar com Linux nós num cluster HPC Pack no local, consulte Olá [TechNet orientações](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
