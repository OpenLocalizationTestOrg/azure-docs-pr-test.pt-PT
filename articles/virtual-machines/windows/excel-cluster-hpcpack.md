---
title: aaaHPC pacote do cluster para o Excel e SOA | Microsoft Docs
description: "Começar a executar cargas de trabalho em grande escala Excel e SOA num cluster HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Introdução ao executar cargas de trabalho do Excel e SOA num cluster HPC Pack no Azure
Este artigo mostra como toodeploy Microsoft HPC Pack 2012 R2 do cluster em máquinas virtuais do Azure, utilizando um modelo de início rápido do Azure ou, opcionalmente, um script de implementação do Azure PowerShell. cluster de Olá utiliza VM do Azure Marketplace imagens concebidas toorun Microsoft Excel ou cargas de trabalho de arquitetura orientada para serviços (SOA) com o HPC Pack. Pode utilizar serviços SOA partir de um computador de cliente no local e Olá toorun de cluster HPC de Excel. os serviços de Excel HPC Olá incluem descarregamento de livros do Excel e funções definidas pelo utilizador do Excel ou UDFs.

> [!IMPORTANT] 
> Este artigo baseia-se nas funcionalidades, modelos e scripts para HPC Pack 2012 R2. Este cenário não é atualmente suportado HPC Pack 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Um nível elevado, hello diagrama seguinte mostra cluster HPC Pack de Olá que cria.

![Cluster HPC connosco executar cargas de trabalho do Excel][scenario]

## <a name="prerequisites"></a>Pré-requisitos
* **Computador cliente** -precisa de um cliente baseado no Windows computador toosubmit exemplo Excel e SOA tarefas toohello cluster. Também precisa de um Olá de toorun de computador Windows script de implementação de cluster do Azure PowerShell (se escolher que método de implementação).
* **Subscrição do Azure** -se não tiver uma subscrição do Azure, pode criar um [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.
* **Quota de núcleos** -poderá ter de quota de Olá tooincrease de núcleos, especialmente se implementar vários nós do cluster sem especializados tamanhos de VM. Se estiver a utilizar um modelo de início rápido do Azure, a quota de núcleos de Olá no Gestor de recursos é por região do Azure. Nesse caso, poderá ter de quota de Olá tooincrease numa região específica. Consulte [limites de subscrição do Azure, quotas e restrições](../../azure-subscription-service-limits.md). tooincrease uma quota [abrir um pedido de suporte ao cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) , sem encargos.
* **Licença do Microsoft Office** - se implementar computação nós utilizando uma imagem de VM do Marketplace HPC Pack 2012 R2 com o Microsoft Excel, está instalada uma versão de avaliação de 30 dias do Microsoft Excel Professional Plus 2013. Após o período de avaliação de Olá, terá de tooprovide uma válido Microsoft Office licença tooactivate Excel toocontinue toorun cargas de trabalho. Consulte [Excel ativação](#excel-activation) posteriormente neste artigo. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Passo 1. Configurar um cluster HPC Pack no Azure
Vamos mostrar duas opções tooset segurança cluster HPC Pack 2012 R2 de Olá: primeiro, utilizando um modelo de início rápido do Azure e Olá portal do Azure; e o segundo, utilizando um script de implementação do Azure PowerShell.

### <a name="option-1-use-a-quickstart-template"></a>Opção 1. Utilize um modelo de início rápido
Utilize um tooquickly de modelo de início rápido do Azure implementar um cluster HPC Pack Olá portal do Azure. Quando abrir o modelo de Olá no portal de Olá, obtenha uma IU simple em que introduza as definições de Olá para o cluster. Seguem-se passos de Olá. 

> [!TIP]
> Se quiser, utilize um [modelo do Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que cria um cluster semelhante especificamente para cargas de trabalho do Excel. passos de Olá diferirem ligeiramente do seguinte Olá.
> 
> 

1. Visite Olá [página do modelo criar Cluster HPC no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Se quiser, rever as informações sobre o modelo de Olá e código de origem Olá.
2. Clique em **implementar tooAzure** toostart uma implementação com modelo Olá Olá portal do Azure.
   
   ![Implementar a modelo tooAzure][github]
3. No portal de Olá, siga estes passos tooenter Olá parâmetros modelo de cluster HPC Olá.
   
   a. No Olá **parâmetros** página, introduza ou modificar os valores de parâmetros de modelo Olá. (Clique Olá ícone tooeach as definições seguintes para obter informações de ajuda.) Valores de exemplo são apresentados na Olá ecrã a seguir. Este exemplo cria um cluster com o nome *hpc01* no Olá *hpc.local* nós de computação de domínio constituída por um nó principal e 2. nós de computação Olá são criados a partir de uma imagem de VM de pacote HPC inclui o Microsoft Excel.
   
   ![Introduza os parâmetros][parameters-new-portal]
   
   > [!NOTE]
   > nó principal Olá VM é criada automaticamente a partir Olá [mais recente imagem do Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) do HPC Pack 2012 R2 no Windows Server 2012 R2. Atualmente imagem Olá baseia-se no HPC Pack 2012 R2 Update 3.
   > 
   > VMs de nó de computação são criadas a partir da imagem mais recente do Olá da família de nó de computação Olá selecionado. Selecione Olá **ComputeNodeWithExcel** opção Olá mais recente HPC Pack computação nó imagem que inclui uma versão de avaliação do Microsoft Excel Professional Plus 2013. toodeploy um cluster para sessões SOA gerais ou para descarregamento de UDF do Excel, escolha Olá **ComputeNode** opção (sem Excel instalado).
   > 
   > 
   
   b. Escolha Olá subscrição.
   
   c. Criar um grupo de recursos do cluster de Olá, tais como *hpc01RG*.
   
   d. Escolha uma localização para o grupo de recursos de Olá, como EUA Central.
   
   e. No Olá **termos legais** , reveja os termos de Olá. Se concordar, clique em **Compra**. Quando tiver terminado a definir valores de Olá para o modelo de Olá, clique em **criar**.
4. Quando concluir a implementação de Olá (que normalmente demora cerca de 30 minutos), Exportar ficheiro de certificado de cluster Olá Olá principal do nó do cluster. Num passo posterior, pode importa este certificado público no Olá tooprovide Olá do lado do servidor autenticação do computador cliente para enlace de HTTP seguro.
   
   a. No portal do Azure Olá, aceda toohello dashboard, o nó principal selecione Olá e clique em **Connect** , Olá parte superior do Olá página tooconnect utilizando o ambiente de trabalho remoto.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Utilize procedimentos padrão no certificado de nó principal do Gestor de certificados tooexport Olá (localizado em Cert: \LocalMachine\My) sem chave privada Olá. Neste exemplo, exportar *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Exportar o certificado de Olá][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Opção 2. Utilizar script de implementação de IaaS do pacote HPC Olá
Olá script de implementação de HPC Pack IaaS proporciona outra forma versátil toodeploy um cluster HPC Pack. Cria um cluster no modelo de implementação clássica Olá, enquanto que o modelo de Olá utiliza o modelo de implementação Azure Resource Manager Olá. Além disso, o script de Olá é compatível com uma subscrição no Olá Global do Azure ou o serviço de Azure China.

**Pré-requisitos adicionais**

* **O Azure PowerShell** - [instalar e configurar o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.
* **Script de implementação de HPC Pack IaaS** - transferir e Descompacte a versão mais recente do Olá do script de Olá no Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Verificar a versão de Olá do script Olá executando `New-HPCIaaSCluster.ps1 –Version`. Este artigo baseia-se numa versão 4.5.0 ou posterior do script de Olá.

**Criar ficheiro de configuração de Olá**

 Olá HPC Pack IaaS script de implementação utiliza um ficheiro de configuração XML, como entrada descreve Olá da infraestrutura de cluster HPC de Olá. toodeploy nós criados a partir da imagem do nó de computação Olá que inclui o Microsoft Excel, de computação de um cluster constituída por um nó principal e 18 substitua os valores para o seu ambiente para o seguinte ficheiro de configuração de exemplo de Olá. Para mais informações sobre o ficheiro de configuração de Olá, consulte o ficheiro de Manual.rtf de Olá na pasta de script de Olá e [criar um cluster HPC com Olá script de implementação de HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Notas sobre o ficheiro de configuração de Olá**

* Olá **VMName** de nó principal Olá **tem** ser Olá mesmo como Olá **ServiceName**, ou tarefas SOA falharem toorun.
* Certifique-se de que especifica **EnableWebPortal** para que hello certificado do nó principal é gerado e exportado.
* ficheiro de Olá Especifica um script do PowerShell pós-configuração PostConfig.ps1 que é executado no nó principal Olá. Olá script de exemplo a seguir configura a cadeia de ligação de armazenamento do Azure Olá, remove a função de nó de computação Olá do nó principal Olá e coloca todos os nós online quando estão implementadas. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Executar script de Olá**

1. Abra a consola do PowerShell de Olá no computador de cliente Olá como administrador.
2. Alterar pasta do script do diretório toohello (E:\IaaSClusterScript neste exemplo).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. toodeploy Olá HPC Pack cluster, execute Olá os seguintes comandos. Este exemplo assume que esse ficheiro de configuração Olá está localizado na E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Olá script de implementação de pacote HPC estiver em execução durante algum tempo. Um script de Olá coisa que faz é tooexport e transferir o certificado de cluster Olá e guardá-lo na pasta de documentos do utilizador atual Olá no computador de cliente Olá. script de Olá gera um mensagem semelhante toohello seguintes procedimentos. Um passo seguinte, importar o certificado de Olá no arquivo de certificados adequada de Olá.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Passo 2. Descarregamento de livros do Excel e executar UDFs a partir de um cliente no local
### <a name="excel-activation"></a>Ativação do Excel
Quando utilizar Olá imagem de ComputeNodeWithExcel VM para cargas de trabalho de produção, terá de tooprovide uma válido Microsoft Office licença chave tooactivate Excel em nós de computação Olá. Caso contrário, versão de avaliação de Olá do Excel expira após 30 dias e em execução livros do Excel irá falhar com Olá COMException (0x800AC472). 

Pode rearmamento Excel por mais 30 dias da hora de avaliação: Inicie sessão no nó principal toohello e clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` no Excel todos os nós através do Gestor de Cluster HPC de computação. Pode rearmamento um máximo de duas vezes. Depois disso, tem de fornecer uma chave de licenciamento do Office válida.

Olá Office Professional Plus 2013 instalado numa imagem VM Olá é uma edição de volume com uma chave de licença do genérico Volume (GVLK). Pode ativá-lo através do serviço de gestão de chaves (KMS) / ativação baseada no Active Directory (AD BA) ou chave de ativação múltipla (MAK). 

    * toouse KMS/AD-BA, utilizar um servidor KMS existente ou configure um novo utilizando Olá pacote de licença de Volume do Microsoft Office 2013. (Se pretender, configurar Olá servidor no nó principal Olá.) Em seguida, ative chave de anfitrião KMS Olá através de Olá Internet ou por telefone. Em seguida, clusrun `ospp.vbs` tooset Olá e porta do servidor KMS e ativar o Office em todos os nós de computação de Excel Olá. 

    * toouse MAK, primeiro clusrun `ospp.vbs` tooinput Olá chave e, em seguida, ative todos os nós de computação de Excel Olá através de Olá Internet ou telefone. 

> [!NOTE]
> Não não possível utilizar chaves de produto de revenda para o Office Professional Plus 2013 com esta imagem de VM. Se tiver chaves válidas e de suporte de dados de instalação para o Office ou Excel edições que não sejam nesta edição de volume do Office Professional Plus 2013, pode utilizá-los em vez disso. Primeiro, desinstale nesta edição de volume e instalar a edição de Olá que tiver. Olá reinstalado Excel nó de computação pode ser capturada como um toouse de imagem VM personalizada numa implementação à escala.
> 
> 

### <a name="offload-excel-workbooks"></a>Descarregamento de livros do Excel
Siga estes toooffload passos um livro do Excel para que seja executado no cluster HPC Pack de Olá no Azure. toodo, tem de ter o Excel 2010 ou 2013 já instalado no computador de cliente Olá.

1. Utilize uma das opções de Olá no passo 1 toodeploy um cluster HPC Pack com Olá Excel imagem do nó de computação. Obter o ficheiro de certificado de cluster Olá (. cer) e cluster nome de utilizador e palavra-passe.
2. No computador de cliente Olá, importe o certificado de cluster de Olá em Cert: \CurrentUser\Root.
3. Certifique-se de que o Excel está instalado. Crie um ficheiro de Excel.exe.config com Olá seguir o conteúdo no Olá mesma pasta que Excel.exe no computador de cliente Olá. Este passo garante que Olá suplemento HPC Pack 2012 R2 Excel COM é carregado com êxito.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Configure Olá cliente toosubmit tarefas toohello HPC Pack cluster. Uma das alternativas consiste Olá toodownload completa [instalação do HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar o cliente de HPC Pack Olá. Em alternativa, transfira e instale Olá [utilitários de cliente do Microsoft HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e Olá adequado Visual C++ 2010 redistributable para o seu computador ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. Neste exemplo, utilizamos um livro do Excel de exemplo com o nome ConvertiblePricing_Complete.xlsb. Poderá transferi-lo [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Copie Olá Excel livro tooa a pasta de trabalho, tais como D:\Excel\Run.
7. Abra o livro do Excel Olá. No Olá **desenvolver** do Friso, clique em **suplementos COM** e confirme que Olá suplemento HPC Pack Excel COM carregada com êxito.
   
   ![Excel suplemento para HPC Pack][addin]
8. Editar Olá VBA macro HPCControlMacros no Excel alterando Olá comentado linhas, conforme mostrado no seguinte script de Olá. Substitua os valores apropriados para o seu ambiente.
   
   ![Macro Excel para HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Copie Olá Excel livro tooan carregamento diretório, tais como D:\Excel\Upload. Este diretório é especificado em constante de HPC_DependsFiles Olá na macro VBA Olá.
10. livro de Olá toorun no cluster de Olá no Azure, clique em Olá **Cluster** botão na folha de cálculo de Olá.

### <a name="run-excel-udfs"></a>Executar UDFs do Excel
toorun UDFs do Excel, siga Olá precedente passos 1 – 3 tooset. o computador de cliente Olá. Para UDFs do Excel, não precisa de aplicação de Excel toohave Olá instalada em nós de computação. Para que, quando criar o cluster de nós de computação, que pode escolher uma imagem do nó de computação normal em vez de Olá computação imagens de nó com o Excel.

> [!NOTE]
> Não há um limite de 34 caracteres no Olá Excel 2010 e a caixa de diálogo de conector de cluster de 2013. Utilize este cluster de Olá de toospecify da caixa de diálogo que é executado Olá UDFs. Se o nome do cluster completo de Olá é maior (por exemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), não se ajustar na caixa de diálogo Olá. Olá solução é tooset uma variável de toda a máquina como *CCP_IAASHN* com o valor de Olá do nome de cluster longo Olá. Em seguida, introduza *% CCP_IAASHN %* na caixa de diálogo de Olá como nome de nó principal do cluster Olá. 
> 
> 

Depois do cluster de Olá é implementado com êxito, prosseguir Olá toorun passos a seguir um incorporado de exemplo UDF do Excel. Para personalizado UDFs do Excel, consulte estes [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Olá XLLs e implementá-los num cluster de IaaS Olá.

1. Abra um novo livro do Excel. No Olá **desenvolver** do Friso, clique em **suplementos**. Em seguida, na caixa de diálogo Olá, clique em **procurar**, navegue toohello %CCP_HOME%Bin\XLL32 pastas e selecione o exemplo de Olá ClusterUDF32.xll. Se hello ClusterUDF32 não existe no computador de cliente Olá, copie-a partir da pasta %CCP_HOME%Bin\XLL32 Olá nó principal Olá.
   
   ![Selecione Olá UDF][udf]
2. Clique em **ficheiro** > **opções** > **avançadas**. Em **fórmulas**, verifique **permitir toorun de funções XLL definido pelo utilizador a um cluster de cálculo**. Em seguida, clique em **opções** e introduza o nome do cluster completo Olá no **nome de nó principal do Cluster**. (Que foram anotados anteriormente esta caixa de entrada está limitada too34 carateres, para que um nome de cluster longo não pode caber. É possível utilizar uma variável de toda a máquina aqui para um nome de cluster longo.)
   
   ![Configurar Olá UDF][options]
3. Olá toorun cálculo de UDF num cluster de Olá, clique em Olá célula com o valor =XllGetComputerNameC() e prima Enter. função de Olá apenas obtém Olá nome de nó de computação de Olá no qual Olá UDF é executada. Para Olá executar pela primeira vez, uma caixa de diálogo de credenciais pede-lhe Olá nome de utilizador e palavra-passe tooconnect toohello IaaS cluster.
   
   ![Executar UDF][run]
   
   Quando existem demasiadas células toocalculate, prima Alt-Shift-Ctrl + o cálculo de Olá F9 toorun em todas as células.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Passo 3. Executar uma carga de trabalho SOA a partir de um cliente no local
aplicações SOA gerais toorun no cluster de HPC Pack IaaS Olá, utilize um dos métodos de Olá pela primeira vez no cluster do passo 1 toodeploy Olá. Especifique uma imagem do nó de computação genérico neste caso, porque não é necessário o Excel em nós de computação Olá. Em seguida, siga estes passos.

1. Após a obtenção de certificado de cluster Olá, importe-o no computador de cliente Olá em Cert: \CurrentUser\Root.
2. Instalar Olá [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) e [utilitários de cliente do Microsoft HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923). Estas ferramentas permitem-lhe toodevelop e executem aplicações de cliente SOA.
3. Transferir Olá HelloWorldR2 [código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633). Abra Olá HelloWorldR2.sln no Visual Studio 2010 ou 2012. (Este exemplo não é atualmente compatível com versões mais recentes do Visual Studio).
4. Compilar o projeto de EchoService Olá primeiro. Em seguida, implemente o cluster de IaaS do Olá serviço toohello no Olá mesma forma que implementa tooan-local no cluster. Para obter passos detalhados, consulte Olá Readme.doc no HelloWordR2. Modificar e criar Olá HellWorldR2 e outros projetos, conforme descrito em Olá seguinte secção toogenerate Olá SOA aplicações cliente que são executados num cluster do IaaS do Azure.

### <a name="use-http-binding-with-azure-storage-queue"></a>Utilizar o enlace de Http com a fila de armazenamento do Azure
enlace de Http toouse com uma fila de armazenamento do Azure, efetue alterações alguns toohello código de exemplo.

* Nome do cluster de Olá de atualização.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Opcionalmente, utilize a predefinição de Olá TransportScheme SessionStartInfo ou explicitamente definido tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Utilize o enlace predefinido para Olá BrokerClient.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Ou defina explicitamente com Olá basicHttpBinding.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Opcionalmente, defina Olá UseAzureQueue sinalizador tootrue no SessionStartInfo. Se não for definido, será definido tootrue por predefinição quando o nome do cluster Olá tem sufixos de domínio do Azure e Olá TransportScheme é Http.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Utilizar o enlace de Http sem fila de armazenamento do Azure
enlace de Http toouse sem uma fila de armazenamento do Azure, explicitamente conjunto Olá UseAzureQueue sinalizador toofalse no Olá SessionStartInfo.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Utilizar o enlace de NetTcp
toouse NetTcp enlace, a configuração de Olá é cluster de no local de tooan tooconnecting semelhantes. É necessário tooopen alguns pontos finais no nó principal do Olá VM. Se utilizou o cluster de Olá de toocreate implementação script Olá HPC Pack IaaS, por exemplo, pontos finais de Olá do conjunto no Olá portal do Azure da seguinte forma.

1. Pare Olá VM.
2. Adicionar portas TCP de Olá 9090, 9087, 9091, 9094 para Olá sessão, mediador, Mediador de trabalho e os serviços de dados, respetivamente
   
    ![Configurar pontos finais][endpoint-new-portal]
3. Inicie Olá VM.

Olá aplicação de cliente SOA não necessita de alterações, exceto alterar Olá nome head toohello IaaS completa nome do cluster.

## <a name="next-steps"></a>Passos seguintes
* Consulte [estes recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para obter mais informações sobre como executar cargas de trabalho do Excel com o HPC Pack.
* Consulte [gerir serviços SOA no Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para obter mais informações sobre como implementar e gerir serviços SOA com o HPC Pack.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
