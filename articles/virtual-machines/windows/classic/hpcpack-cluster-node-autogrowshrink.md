---
title: "nós de cluster HPC Pack aaaAutoscale | Microsoft Docs"
description: "Automaticamente aumentar e diminuir o número de Olá de nós de computação de cluster HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a>Automaticamente aumentar e diminuir a recursos de cluster HPC Pack Olá no Azure de acordo com a carga de trabalho de cluster de toohello
Se implementar nós do Azure "rajada" no seu cluster HPC Pack ou criar um cluster HPC Pack em VMs do Azure, poderá pretender uma forma de automaticamente aumentar ou diminuir os recursos do cluster Olá como nós ou núcleos de acordo com a carga de trabalho Olá no cluster de Olá. Dimensionar os recursos do cluster Olá desta forma permite-lhe toouse os recursos do Azure de forma mais eficiente e controlar os custos.

Este artigo mostra-lhe duas formas de HPC Pack fornece recursos de computação tooautoscale:

* Olá propriedade de cluster HPC Pack **AutoGrowShrink**

* Olá **AzureAutoGrowShrink.ps1** script do HPC PowerShell

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Atualmente só automaticamente pode aumentar e diminuir a nós de computação de HPC Pack que estejam a executar um sistema operativo Windows Server.


## <a name="set-hello-autogrowshrink-cluster-property"></a>Definir a propriedade de cluster Olá AutoGrowShrink
### <a name="prerequisites"></a>Pré-requisitos

* **HPC Pack 2012 R2 Update 2 ou posterior cluster** -nó principal do cluster Olá pode ser implementado no local ou numa VM do Azure. Consulte [configurar um cluster de híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget começar a utilizar um nó principal no local e nós do Azure "rajada". Consulte Olá [script de implementação de HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly implementar um cluster HPC Pack em VMs do Azure.

* **Para um cluster com um nó principal no Azure (modelo de implementação do Resource Manager)** - a partir de HPC Pack 2016, autenticação de certificado de uma aplicação do Azure Active Directory é utilizada para a crescer automaticamente e reduzir o cluster VMs implementadas utilizando O Azure Resource Manager. Configure um certificado da seguinte forma:

  1. Após a implementação de cluster, se liguem ao nó principal do ambiente de trabalho remoto tooone.

  2. Carregar o nó principal do Olá certificado (formato PFX com chave privada) tooeach e instale tooCert:\LocalMachine\My e Cert: \LocalMachine\Root.

  3. Inicie o Azure PowerShell como administrador e execute Olá os seguintes comandos num nó principal:

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    Se a sua conta está em mais do que um inquilino do Azure Active Directory ou a subscrição do Azure, pode executar o seguinte Olá comando inquilino correto do tooselect Olá e de subscrição:
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    Executar Olá os seguintes comandos tooview Olá atualmente selecionadas inquilino e de subscrição:
    
    ```powershell
        Get-AzureRMContext
    ```

  4. Execute o seguinte script de Olá

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    onde

    **DisplayName** -nome de apresentação da aplicação Active Directory do Azure. Se a aplicação Olá não existir, será criado no Azure Active Directory.

    **Home page** -Olá home page da aplicação Olá. Pode configurar um URL fictício, tal como em Olá anterior exemplo.

    **IdentifierUri** -identificador da aplicação Olá. Pode configurar um URL fictício, tal como em Olá anterior exemplo.

    **CertificateThumbprint** -Thumbprint do certificado de Olá instalado no nó principal do Olá no passo 1.

    **TenantId** -ID do seu Azure Active Directory de inquilino. Pode obter Olá ID do inquilino a partir do portal do Azure Active Directory Olá **propriedades** página.

    Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.


* **Para um cluster com um nó principal no Azure (modelo de implementação clássica)** - se utilizar o cluster Olá de toocreate script Olá HPC Pack IaaS implementação no modelo de implementação clássica Olá, ativar Olá **AutoGrowShrink** cluster propriedade definindo a opção de AutoGrowShrink Olá no ficheiro de configuração de cluster Olá. Para obter mais informações, consulte a documentação de Olá que acompanha Olá [transferências de script](https://www.microsoft.com/download/details.aspx?id=44949).

    Em alternativa, ativar Olá **AutoGrowShrink** propriedade cluster depois de implementar o cluster de Olá utilizando o HPC PowerShell comandos descrito Olá secção a seguir. tooprepare para tal, primeiro Olá concluir os seguintes passos:

  1. Configure um certificado de gestão do Azure no nó principal Olá e nas Olá subscrição do Azure. Para uma implementação de teste, pode utilizar Olá predefinido Microsoft HPC Azure certificado autoassinado que instala o pacote HPC no nó principal Olá e, em seguida, carregue esse tooyour certificado de subscrição do Azure. Para opções e passos, consulte Olá [orientações de biblioteca do TechNet](https://technet.microsoft.com/library/gg481759.aspx).

  2. Executar **regedit** no nó principal Olá, aceda tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e adicione um valor de cadeia. Definir o nome do valor Olá demasiado "ThumbPrint" e valor dados toohello thumbprint do certificado de Olá no passo 1.

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a>Propriedade do HPC PowerShell comandos tooset Olá AutoGrowShrink
Seguem-se tooset de comandos do HPC PowerShell exemplo **AutoGrowShrink** e tootune respetivo comportamento com parâmetros adicionais. Consulte [AutoGrowShrink parâmetros](#AutoGrowShrink-parameters) posteriormente neste artigo para a lista completa de Olá das definições.

toorun estes comandos, inicie o HPC PowerShell no nó principal do cluster Olá como administrador.

**Olá tooenable AutoGrowShrink propriedade**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

**Olá toodisable AutoGrowShrink propriedade**

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

**Olá toochange aumente o intervalo em minutos**

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

**Olá toochange diminuir o intervalo em minutos**

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

**configuração de atual Olá tooview de AutoGrowShrink**

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

**grupos de nó tooexclude do AutoGrowShrink**

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> Este parâmetro é suportado a partir de 2016 do HPC Pack
>

### <a name="autogrowshrink-parameters"></a>Parâmetros de AutoGrowShrink
Olá seguem-se AutoGrowShrink parâmetros que pode modificar utilizando Olá **conjunto HpcClusterProperty** comando.

* **EnableGrowShrink** - mudar tooenable ou desativar Olá **AutoGrowShrink** propriedade.
* **ParamSweepTasksPerCore** -número de varrimento paramétrico tarefas toogrow um núcleo. predefinição de Olá é toogrow um núcleo por tarefa.

  > [!NOTE]
  > Alterações de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** demasiado**TasksPerResourceUnit**. -Baseia-se no tipo de recurso de tarefa Olá e pode ser nó, socket ou core.
  >
  >
* **GrowThreshold** -limiar de aumento automático do tootrigger tarefas em fila. predefinição de Olá é 1, o que significa que o se existirem 1 ou mais tarefas no Olá em fila de estado, aumentar automaticamente nós.
* **GrowInterval** -intervalo de aumento automático do tootrigger minutos. intervalo de Olá predefinido é 5 minutos.
* **ShrinkInterval** -intervalo em minutos tootrigger automática reduzir. intervalo de predefinido de Olá é de 5 minutos. |
* **ShrinkIdleTimes** -número de nós de Olá verificações contínua tooshrink tooindicate está inativo. predefinição de Olá é 3 vezes. Por exemplo, se hello **ShrinkInterval** é de 5 minutos, HPC Pack verifica se o nó de Olá está inativo a cada 5 minutos. Se nós de Olá num estado inativo Olá depois 3 contínua verifica (15 minutos), pacote HPC diminui nesse nó.
* **ExtraNodesGrowRatio** -percentagem adicional de nós toogrow para tarefas de Interface de passagem de mensagens (MPI). valor predefinido de Olá é 1, o que significa que o pacote HPC cresce nós % 1 para tarefas MPI.
* **GrowByMin** -se a política de aumento automático Olá baseia-se nos recursos de Olá mínimo necessários para a tarefa de Olá tooindicate de comutador. Olá predefinição é false, o que significa que o pacote HPC cresce nós para as tarefas com base nos recursos de máximo de Olá necessários para as tarefas de Olá.
* **SoaJobGrowThreshold** -limiar de entrada SOA pedidos tootrigger Olá automática aumentar o processo. valor predefinido de Olá é 50000.

  > [!NOTE]
  > Este parâmetro é suportado a partir de HPC Pack 2012 R2 Update 3.
  >
  >
* **SoaRequestsPerCore** -número de SOA recebido pedidos toogrow um núcleo. valor predefinido de Olá é de 20000.

  > [!NOTE]
  > Este parâmetro é suportado a partir de HPC Pack 2012 R2 Update 3.
  >
* **ExcludeNodeGroups** – especificado de nós no Olá grupos de nó automaticamente aumentar e diminuir.
  
  > [!NOTE]
  > Este parâmetro é suportado a partir de HPC Pack 2016.
  >

### <a name="mpi-example"></a>Exemplo MPI
Por predefinição HPC Pack crescimentos de 1% nós adicionais para os trabalhos MPI (**ExtraNodesGrowRatio** está definido too1). motivo Olá é que MPI pode necessitar de vários nós e tarefa Olá só pode ser executada quando todos os nós estão prontos. Quando Azure é iniciado nós, ocasionalmente, um nó pode ter mais tempo toostart que outros, fazendo com que outras toobe nós inativo enquanto aguardam que tooget esse nó pronto. Incrementando nós adicionais, HPC Pack reduz o tempo de espera este recurso e, potencialmente, guarda os custos. percentagem de Olá tooincrease de nós adicionais para trabalhos MPI (por exemplo, too10%), execute um comando semelhante ao

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a>Exemplo SOA
Por predefinição, **SoaJobGrowThreshold** está definido too50000 e **SoaRequestsPerCore** está definido too200000. Se submeter uma tarefa SOA com 70000 pedidos, existe uma tarefa em fila e os pedidos recebidos são 70000. Neste caso, o HPC Pack cresce 1 núcleo Olá colocados em fila de tarefas e para pedidos recebidos, cresce (70000 50000) / core 20000 = 1, no total crescimentos de 2 núcleos para esta tarefa SOA.

## <a name="run-hello-azureautogrowshrinkps1-script"></a>Executar script de AzureAutoGrowShrink.ps1 Olá
### <a name="prerequisites"></a>Pré-requisitos

* **HPC Pack 2012 R2 Update 1 ou posterior cluster** - hello **AzureAutoGrowShrink.ps1** script está instalado na pasta bin Olá % CCP_HOME %. nó principal do cluster Olá pode ser implementado no local ou numa VM do Azure. Consulte [configurar um cluster de híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget começar a utilizar um nó principal no local e nós do Azure "rajada". Consulte Olá [script de implementação de HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly implementar um cluster HPC Pack em VMs do Azure ou utilize um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).
* **O Azure PowerShell 1.4.0** -script Olá depende atualmente esta versão específica do Azure PowerShell.
* **Para um cluster com o Azure burst nós** -executar script de Olá num computador cliente onde o HPC Pack está instalado, ou no nó principal Olá. Se em execução num computador cliente, certifique-se de que definiu Olá $env variável: nó principal do CCP_SCHEDULER toopoint toohello. Olá do Azure "rajada" nós têm de ser adicionados toohello cluster, mas podem estar a ser Olá Estado não implementadas.
* **Para um cluster implementado em VMs do Azure (modelo de implementação do Resource Manager)** -num cluster de VMs do Azure implementadas no modelo de implementação do Resource Manager Olá, o script de Olá suporta dois métodos de autenticação do Azure: a iniciar sessão tooyour conta do Azure script de Olá toorun sempre (executando `Login-AzureRmAccount`, ou configurar um tooauthenticate principal de serviço com um certificado. Pacote HPC fornece o script de Olá **ConfigARMAutoGrowShrinkCert.ps** toocreate um principal de serviço com o certificado. script de Olá cria uma aplicação do Azure Active Directory (Azure AD) e um principal de serviço e atribui o principal de serviço de toohello de função de contribuinte de Olá. script de Olá toorun, inicie o Azure PowerShell como administrador e execute Olá os seguintes comandos:

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,

* **Para um cluster implementado em VMs do Azure (modelo de implementação clássica)** -execute o script de Olá no nó principal do Olá VM, porque depende de Olá **início HpcIaaSNode.ps1** e **Stop-HpcIaaSNode.ps1**scripts que são instaladas não existe. Esses scripts adicionalmente requerem um certificado de gestão do Azure ou publicar o ficheiro de definições (consulte [cluster de nós de computação de gerir num pacote HPC no Azure](hpcpack-cluster-node-manage.md)). Certifique-se de que todos os Olá nó VMs terá já foram adicionadas toohello cluster de computação. Estes poderão Olá estado parado.



### <a name="syntax"></a>Sintaxe
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a>Parâmetros
* **NodeTemplates** -nomes de Olá nó modelos toodefine Olá âmbito Olá nós toogrow e diminuir. Se não for especificado (valor predefinido de Olá é @()), todos os nós no Olá **AzureNodes** grupo de nós estão no âmbito quando **NodeType** tem um valor de AzureNodes e todos os nós no Olá **ComputeNodes** grupo de nós estão no âmbito quando **NodeType** tem um valor de ComputeNodes.
* **JobTemplates** -nomes de Olá âmbito de Olá toodefine modelos para Olá nós toogrow da tarefa.
* **NodeType** - Olá o tipo de nó toogrow e diminuir. Os valores suportados são:

  * **AzureNodes** – para nós do Azure PaaS (rajada) no local ou cluster do IaaS do Azure.
  * **ComputeNodes** – para o nó de computação VMs apenas um cluster do IaaS do Azure.

* **NumOfQueuedJobsPerNodeToGrow** -número de tarefas em fila necessários toogrow um nó.
* **NumOfQueuedJobsToGrowThreshold** -Olá limiar diversas Olá toostart de tarefas em fila aumentar o processo.
* **NumOfActiveQueuedTasksPerNodeToGrow** -número de Olá das tarefas em fila Active Directory necessários toogrow um nó. Se **NumOfQueuedJobsPerNodeToGrow** for especificado com um valor maior que 0, este parâmetro será ignorado.
* **NumOfActiveQueuedTasksToGrowThreshold** -Olá limiar diversas Olá do Active Directory tarefas em fila toostart aumentar o processo.
* **NumOfInitialNodesToGrow** - hello inicial número mínimo de nós toogrow se todos os nós de Olá no âmbito são **implementadas não** ou **parado (Deallocated)**.
* **GrowCheckIntervalMins** -intervalo de Olá em minutos entre verifica toogrow.
* **ShrinkCheckIntervalMins** -intervalo de Olá em minutos entre verifica tooshrink.
* **ShrinkCheckIdleTimes** -Olá número de verificações de operação de encolhimento contínua (separados por **ShrinkCheckIntervalMins**) nós de Olá tooindicate estão inativos.
* **UseLastConfigurations** -Olá configurações anteriores guardadas no ficheiro de argumento Olá.
* **ArgFile**- Olá nome Olá argumento ficheiro utilizado toosave e atualizar o script de Olá Olá configurações toorun.
* **LogFilePrefix** -nome de prefixo Olá Olá do ficheiro de registo. Pode especificar um caminho. Por predefinição o registo Olá é escrito toohello atual diretório de trabalho.

### <a name="example-1"></a>Exemplo 1
Olá exemplo a seguir configura Olá Azure burst nós implementados com o modelo predefinido de AzureNode toogrow e reduzir automaticamente. Se todos os nós inicialmente no Olá **implementadas não** Estado, pelo menos 3 nós são iniciados. Se o número de Olá de tarefas em fila exceder 8, o script Olá inicia nós até que o respetivo número excede o rácio de Olá de tarefas em fila a **NumOfQueuedJobsPerNodeToGrow**. Se um nó for encontrado toobe inativo em 3 vezes consecutivas de inatividade, está parado.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a>Exemplo 2
Olá exemplo a seguir configura Olá Azure implementadas com Olá modelo predefinido de ComputeNode toogrow de VMs de nó de computação e reduzir automaticamente.
tarefas de Olá configuradas pelo modelo de tarefa Olá predefinido definem âmbito de Olá da carga de trabalho no cluster de Olá. Se todos os nós de Olá inicialmente são parados, pelo menos 5 nós são iniciados. Se o número de Olá do Active Directory tarefas em fila exceder 15, o script Olá inicia nós até que o respetivo número excede rácio Olá do Active Directory tarefas em fila demasiado**NumOfActiveQueuedTasksPerNodeToGrow**. Se um nó for encontrado toobe inativo em 10 vezes consecutivas de inatividade, está parado.

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
