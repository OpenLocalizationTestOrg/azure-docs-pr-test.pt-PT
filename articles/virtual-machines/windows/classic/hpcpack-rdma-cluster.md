---
title: "aaaSet das aplicações de MPI Windows RDMA cluster toorun | Microsoft Docs"
description: "Saiba como toocreate um cluster Windows HPC Pack com tamanho H16r, H16mr, A8 ou A9 VMs toouse Olá Azure RDMA rede toorun MPI aplicações."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>Configurar um cluster do Windows RDMA com aplicações de MPI toorun HPC Pack
Configurar um cluster do Windows RDMA no Azure com [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) e [tamanhos de VM de computação de elevado desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun aplicações de Interface de passagem de mensagens (MPI) paralelas. Quando configurar com capacidade RDMA, baseado no Windows Server nós num cluster HPC Pack, aplicações MPI comunicam forma eficiente através de uma baixa latência, a rede de alto débito no Azure baseia-se na tecnologia de (RDMA) de acesso remoto direto à memória.

Se pretender toorun cargas de trabalho MPI em VMs do Linux essa rede de Azure RDMA acesso Olá, veja [configurar um Linux RDMA cluster toorun MPI aplicações](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>Opções de implementação de cluster HPC Pack
Pacote HPC da Microsoft é uma ferramenta fornecido no toocreate sem custos adicionais HPC clusters no local ou no Azure toorun Windows ou aplicações de Linux HPC. Pacote HPC inclui um ambiente de tempo de execução para a implementação Microsoft de Olá de Olá mensagem passar na Interface do Windows (MS-MPI). Quando utilizado com instâncias com capacidade RDMA a executar o sistema operativo Windows Server suportado, o HPC Pack fornece aplicações de Windows MPI uma opção eficiente toorun essa rede de Azure RDMA Olá acesso. 

Este artigo apresenta dois cenários e liga toodetailed orientações tooset configurar um cluster do Windows RDMA com o Microsoft HPC Pack. 

* Cenário 1. Implementar instâncias de função de trabalho de computação intensiva (PaaS)
* Cenário 2. Implementar nós de computação de computação intensiva VMs (IaaS)

Para instâncias de computação intensivas de toouse de pré-requisitos gerais com o Windows, consulte [tamanhos de VM de computação de elevado desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Cenário 1: Implementar instâncias de função de trabalho de computação intensiva (PaaS)
De um cluster HPC Pack existente, adicione recursos de computação adicional em instâncias de função de trabalho do Azure (nós do Azure) em execução num serviço cloud (PaaS). Esta funcionalidade, também designado por "rajada tooAzure" do pacote HPC, suporta uma variedade de tamanhos de instâncias de função de trabalho Olá. Quando adicionar hello nós do Azure, tem de especificar um dos tamanhos de Olá com capacidade RDMA.

Seguem-se passos e considerações sobre tooburst com capacidade tooRDMA instâncias do Azure existente de um (normalmente, no local) cluster. Utilize semelhante procedimentos tooadd trabalho função instâncias tooan HPC Pack nó principal que está implementada numa VM do Azure.

> [!NOTE]
> Para um tooAzure tutorial tooburst com o HPC Pack, consulte [configurar um cluster de híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Tenha em atenção considerações Olá Olá seguindo os passos que se aplicam especificamente tooRDMA com capacidade para nós do Azure.
> 
> 

![Impulsar tooAzure][burst]

### <a name="steps"></a>Passos
1. **Implementar e configurar um nó principal do HPC Pack 2012 R2**
   
    Transferir o pacote de instalação do HPC Pack mais recente Olá de Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Para requisitos e instruções tooprepare para uma implementação de rajada do Azure, consulte [Impulsar tooAzure instâncias de trabalho com o Microsoft HPC Pack](https://technet.microsoft.com/library/gg481749.aspx).
2. **Configurar um certificado de gestão no Olá subscrição do Azure**
   
    Configure uma ligação de Olá toosecure de certificado entre o nó principal Olá e o Azure. Para opções e procedimentos, consulte [Olá de tooConfigure cenários certificado de gestão do Azure para HPC Pack](http://technet.microsoft.com/library/gg481759.aspx). Para implementações de teste, HPC Pack instala um predefinido Microsoft HPC Azure certificado de gestão pode carregar rapidamente tooyour subscrição do Azure.
3. **Criar um novo serviço de nuvem e de uma conta de armazenamento**
   
    Utilize Olá toocreate portal do Azure para um serviço em nuvem e de uma conta de armazenamento para a implementação de Olá numa região onde estão disponíveis as instâncias de Olá com capacidade RDMA.
4. **Criar um modelo de nó do Azure**
   
    Utilize Olá Assistente para criar o modelo nó no Gestor de clusters HPC. Para obter os passos, consulte [criar um modelo do Azure nó](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) nos "Passos tooDeploy nós do Azure com o Microsoft HPC Pack".
   
    Para testes iniciais, sugerimos que configurar uma política de disponibilidade manual no modelo de Olá.
5. **Adicionar nós toohello cluster**
   
    Utilize Olá adicionar nó assistente no Gestor de clusters HPC. Para obter mais informações, consulte [toohello adicionar nós do Azure Windows HPC Cluster](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Quando especificar o tamanho de nós de Olá Olá, selecione um dos tamanhos de instância com capacidade RDMA Olá.
   
   > [!NOTE]
   > Cada implementação de tooAzure rajada com instâncias de computação intensiva Olá, HPC Pack implementa automaticamente um mínimo de duas instâncias com capacidade RDMA (por exemplo, A8) como nós de proxy, além disso toohello instâncias de função de trabalho do Azure especifica. os nós de proxy de Olá utilizam núcleos que são atribuídos toohello subscrição e pagar juntamente com instâncias de função de trabalho do Azure Olá.
   > 
   > 
6. **Inicie nós de Olá (aprovisionar) e colocá-los online toorun tarefas**
   
    Selecione nós de Olá e utilize Olá **iniciar** ação no Gestor de clusters HPC. Quando o aprovisionamento estiver concluído, selecione Olá nós e utilize Olá **colocar Online** ação no Gestor de clusters HPC. nós de Olá são tarefas toorun pronto.
7. **Submeter cluster toohello de tarefas**
   
   Utilize tarefas de cluster de toorun de ferramentas submissão tarefa HPC Pack. Consulte [pacote HPC da Microsoft: gestão de tarefas](http://technet.microsoft.com/library/jj899585.aspx).
8. **Parar de nós de Olá (deprovision)**
   
   Quando tiver terminado de tarefas em execução, colocar nós Olá offline e utilizar Olá **parar** ação no Gestor de clusters HPC.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Cenário 2: Implementar nós de computação intensiva VMs (IaaS) de computação
Neste cenário, implementar nó principal do HPC Pack Olá e nós de computação de cluster em VMs de uma rede virtual do Azure. Pacote HPC fornece vários [opções de implementação em VMs do Azure](../../linux/hpcpack-cluster-options.md), incluindo scripts de implementação automática e modelos de início rápido do Azure. Por exemplo, Olá seguintes considerações e passos guiá-lo toouse Olá [script de implementação de HPC Pack IaaS](hpcpack-cluster-powershell-script.md) para automatizar a implementação de Olá de um cluster HPC Pack 2012 R2 no Azure.

![Cluster em VMs do Azure][iaas]

### <a name="steps"></a>Passos
1. **Criar um nó principal do cluster e as VMs do nó de computação, executando o script de implementação de HPC Pack IaaS Olá num computador cliente**
   
    Transferir o pacote de Script de implementação do HPC Pack IaaS Olá do Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    computador de cliente do tooprepare Olá, criar o ficheiro de configuração do script Olá e Olá executar script, consulte [criar um Cluster HPC com Olá script de implementação de HPC Pack IaaS](hpcpack-cluster-powershell-script.md). 
   
    nós de computação toodeploy com capacidade RDMA, Olá nota seguintes considerações adicionais:
   
   * **Rede virtual**: Especifique uma nova rede virtual numa região na qual Olá rdma e tamanho da instância que pretende toouse está disponível.
   * **Sistema operativo Windows Server**: toosupport conectividade RDMA, especifique um sistema operativo Windows Server 2012 R2 ou Windows Server 2012 para o nó de computação de Olá VMs.
   * **Serviços em nuvem**: Recomendamos a implementação do nó principal no serviço de uma nuvem e os nós de computação num serviço cloud diferente.
   * **Tamanho de nó de HEAD**: para este cenário, considere um tamanho de, pelo menos, A4 (Extra grande) para o nó principal Olá.
   * **Extensão de HpcVmDrivers**: script de implementação de Olá instala Olá agente da VM do Azure e Olá HpcVmDrivers extensão automaticamente quando implementar nós de computação de A8 ou A9 tamanho com um sistema operativo Windows Server. HpcVmDrivers instala controladores no nó de computação Olá VMs, pelo que se possam ligar a rede RDMA toohello. Em VMs de série de H com capacidade RDMA, tem de instalar manualmente a extensão de HpcVmDrivers Olá. Consulte [tamanhos de VM de computação de elevado desempenho](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Configuração de rede de cluster**: script de implementação de Olá configura automaticamente o cluster HPC Pack Olá topologia 5 (todos os nós numa rede de Enterprise Olá). Esta topologia é necessária para todas as implementações de cluster HPC Pack em VMs. Não altere a topologia de rede de cluster hello mais tarde.
2. **Colocar nós de computação Olá tarefas online toorun**
   
    Selecione nós de Olá e utilize Olá **colocar Online** ação no Gestor de clusters HPC. nós de Olá são tarefas toorun pronto.
3. **Submeter cluster toohello de tarefas**
   
    Ligar as tarefas de toosubmit do nó principal toohello ou configurar um toodo de computador local isto. Para informações, consulte [cluster tooan submeter tarefas HPC no Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Tome Olá nós offline e parar (desalocar)-las**
   
    Quando tiver terminado de tarefas em execução, colocar offline nós de Olá no Gestor de clusters HPC. Em seguida, utilize tooshut de ferramentas de gestão do Azure-las para baixo.

## <a name="run-mpi-applications-on-hello-cluster"></a>Executar aplicações MPI no cluster de Olá
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Exemplo: Executar mpipingpong num cluster HPC Pack
tooverify uma implementação de pacote HPC de instâncias de Olá com capacidade RDMA, execute Olá HPC Pack **mpipingpong** comando no cluster de Olá. **mpipingpong** envia pacotes de dados entre os nós emparelhado repetidamente toocalculate medidas de latência e débito e as estatísticas de rede de Olá de aplicações com capacidade RDMA. Este exemplo mostra um padrão normal para executar uma tarefa MPI (neste caso, **mpipingpong**) utilizando o cluster de Olá **mpiexec** comando.

Este exemplo assume que adicionou nós do Azure numa configuração de "impulsar tooAzure" ([cenário 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). Se tiver implementado o HPC Pack num cluster de VMs do Azure, irá precisar toomodify Olá comando sintaxe toospecify um grupo de outro nó e definir a rede RDMA ao toohello do tráfego de rede adicionais ambiente variáveis toodirect.

toorun mpipingpong no cluster de Olá:

1. No nó principal Olá ou num computador cliente está corretamente configurada, abra uma linha de comandos.
2. Latência de tooestimate entre pares de nós numa implementação do Azure rajada de quatro nós, Olá tipo comando toosubmit mpipingpong de toorun uma tarefa com um tamanho de pacotes pequenos e número de iterações a seguir:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    comando de Olá devolve Olá ID da tarefa de Olá submetido.
   
    Se implementou o cluster de HPC Pack Olá implementado em VMs do Azure, especifique um grupo de nó que contenha implementadas num serviço em nuvem única de VMs de nó de computação e modificar Olá **mpiexec** comando da seguinte forma:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Quando tiver concluído a tarefa de Olá, tooview Olá saída (neste caso, resultado Olá tarefa 1 da tarefa de Olá), Olá tipo seguintes
   
    ```Command
    task view <JobID>.1
    ```
   
    onde &lt; *JobID* &gt; Olá ID da tarefa de Olá que foi submetida.
   
    saída de Olá inclui seguinte de toohello semelhante do latência resultados.
   
    ![Latência de pong de ping][pingpong1]
4. débito tooestimate entre pares de Azure burst nós, seguinte de Olá do tipo de comando de toosubmit toorun uma tarefa **mpipingpong** com um tamanho de pacote e alguns iterações:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    comando de Olá devolve Olá ID da tarefa de Olá submetido.
   
    Num cluster HPC Pack implementado em VMs do Azure, modifique o comando de Olá conforme indicado no passo 2.
5. Quando tiver concluído a tarefa de Olá, tooview Olá saída (neste caso, resultado Olá tarefa 1 da tarefa de Olá), Olá tipo seguintes:
   
    ```Command
    task view <JobID>.1
    ```
   
   saída de Olá inclui seguinte de toohello semelhante do débito resultados.
   
   ![Débito de pong de ping][pingpong2]

### <a name="mpi-application-considerations"></a>Considerações de aplicação de MPI
Seguem-se considerações para executar aplicações MPI com o HPC Pack no Azure. Algumas aplicam-se apenas toodeployments de nós do Azure (instâncias de função de trabalho adicionadas numa configuração de "rajada tooAzure").

* Instâncias de função de trabalho num serviço em nuvem são periodicamente reaprovisionadas sem aviso prévio pelo Azure (por exemplo, para manutenção do sistema ou no caso de que falha de uma instância). Se uma instância é reaprovisionada enquanto estiver em execução uma tarefa MPI, instância de Olá perde os dados e devolve o estado de toohello quando esta foi implementada pela primeira vez, que pode provocar Olá MPI tarefa toofail. Hello mais nós que utiliza para uma única tarefa MPI e Olá já hello tarefa é executada, Olá mais provável que uma das instâncias de Olá reaprovisionada enquanto uma tarefa está em execução. Considere também a esta se designar um único nó numa implementação de Olá como um servidor de ficheiros.
* trabalhos MPI toorun no Azure, não tiver toouse Olá com capacidade RDMA instâncias. Pode utilizar qualquer tamanho da instância que é suportado pelo pacote HPC. No entanto, as instâncias com capacidade RDMA Olá são recomendadas para executar tarefas MPI relativamente em grande escala que estão a latência de toohello confidenciais e Olá largura de banda da rede de Olá que liga nós de Olá. Se utilizar outros trabalhos MPI tamanhos toorun sensíveis à latência e largura de banda, recomendamos a execução de tarefas pequenas, na qual uma única tarefa é executada em apenas alguns nós.
* As aplicações implementadas tooAzure instâncias são toohello requerente associados à aplicação Olá dos termos de licenciamento. Verificar junto do fornecedor de Olá de qualquer aplicação comercial para licenciamento ou de outras restrições para ser executada nas nuvens Olá. Nem todos os fornecedores oferecem licenciamento pay as you go.
* Instâncias do Azure tem de configurar mais nós no local de tooaccess, partilhas e servidores de licenças. Por exemplo, tooenable Olá nós do Azure tooaccess um servidor de licenças no local, pode configurar uma rede virtual do Azure do site para site.
* aplicações de MPI toorun nas instâncias do Azure, registar cada aplicação de MPI Firewall do Windows em instâncias de Olá executando Olá **hpcfwutil** comando. Isto permite MPI comunicações tootake local uma porta que é atribuída dinamicamente por firewall Olá.
  
  > [!NOTE]
  > Para implementações de tooAzure rajada, também pode configurar um toorun de comando de exceção de firewall automaticamente em todos os nós do Azure novos que são adicionados tooyour cluster. Depois de executar Olá **hpcfwutil** comando e certifique-se de que a aplicação funciona, adicione o script de arranque do Olá comando tooa para os nós do Azure. Para obter mais informações, consulte [utilizar um Script de arranque para nós do Azure](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* Pacote HPC utiliza Olá CCP_MPI_NETMASK cluster ambiente variável toospecify um intervalo de endereços aceitáveis para comunicação de MPI. A partir de HPC Pack 2012 R2, variável de ambiente de cluster CCP_MPI_NETMASK Olá afeta apenas a comunicação de MPI entre nós de computação de cluster associados a um domínio (no local ou em VMs do Azure). variável de Olá é ignorada por nós adicionados numa configuração tooAzure rajada.
* Não é possível executar tarefas MPI entre instâncias do Azure que são implementadas nos serviços de nuvem diferente (por exemplo, em implementações de tooAzure rajada com modelos de nó diferente ou nós de computação de VM do Azure implementados em múltiplos serviços em nuvem). Se tiver múltiplas implementações de nó do Azure são iniciadas com modelos de nó diferente, deve executar a tarefa MPI de Olá em apenas um conjunto de nós do Azure.
* Quando adicionar nós do Azure tooyour cluster e colocá-los Olá online, o serviço de agendador de tarefas HPC imediatamente tenta toostart tarefas em nós de Olá. Se apenas uma parte da sua carga de trabalho pode ser executado no Azure, certifique-se de que atualizar ou criar tarefa modelos toodefine que tarefa tipos podem ser executados no Azure. Por exemplo, tooensure que tarefas submetidas com um modelo de tarefa apenas serem executado em nós do Azure, adicionar o modelo de tarefa do Olá nó grupos propriedade toohello e selecione AzureNodes como Olá necessário valor. toocreate grupos personalizados para os nós do Azure, utilize o cmdlet do PowerShell de HPC HpcGroup adicionar de Olá.

## <a name="next-steps"></a>Passos seguintes
* Como uma alternativa toousing HPC Pack, desenvolva com toorun de serviço do Azure Batch Olá aplicações MPI no gerido conjuntos de nós de computação no Azure. Consulte [tarefas de várias instâncias de utilização toorun aplicações de Interface de passagem de mensagens (MPI) no Azure Batch](../../../batch/batch-mpi.md).
* Se quiser toorun Linux MPI aplicações que acedam à rede de Azure RDMA Olá, consulte [configurar um Linux RDMA cluster toorun MPI aplicações](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
