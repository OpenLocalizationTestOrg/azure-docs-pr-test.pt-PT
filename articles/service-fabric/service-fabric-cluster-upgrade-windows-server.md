---
title: "aaaUpgrade autónoma Azure Service Fabric de cluster no Windows Server | Microsoft Docs"
description: "Atualize o código de Azure Service Fabric Olá e/ou de configuração que executa um cluster do Service Fabric autónomo, incluindo a definição do modo de atualização de cluster Olá."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Atualizar o seu autónomo Azure Service Fabric no cluster do Windows Server
> [!div class="op_single_selector"]
> * [Cluster do Azure](service-fabric-cluster-upgrade.md)
> * [Cluster autónomo](service-fabric-cluster-upgrade-windows-server.md)
>
>

Para qualquer sistema moderno, Olá capacidade tooupgrade é um sucesso de longo prazo toohello chave do produto. Um cluster do Service Fabric do Azure é um recurso que é proprietário. Este artigo descreve como pode garantir que esse cluster Olá executa sempre as versões suportadas do código de Service Fabric e configurações.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Versão de Service Fabric Olá do controlo que é executado no seu cluster
tooset atualiza o toodownload de cluster do Service Fabric quando a Microsoft disponibiliza uma nova versão, conjunto Olá **fabricClusterAutoupgradeEnabled** tootrue de configuração de cluster. tooselect uma versão suportada do Service Fabric que pretende que o seu toobe de cluster no conjunto Olá **fabricClusterAutoupgradeEnabled** toofalse de configuração de cluster.

> [!NOTE]
> Certifique-se de que o cluster é sempre executada uma versão suportada do Service Fabric. Quando a Microsoft announces versão Olá de uma nova versão de Service Fabric, versão anterior do Olá está marcado para fim de suporte após um mínimo de 60 dias a partir da data de Olá de anúncio de Olá. Novos lançamentos sejam anunciados [no blogue de equipa do Service Fabric Olá](https://blogs.msdn.microsoft.com/azureservicefabric/). nova versão de Olá é toochoose disponível nesse momento.
>
>

Pode atualizar a versão nova do cluster toohello apenas se estiver a utilizar uma configuração de nó de estilo de produção, onde cada nó de Service Fabric está alocada numa máquina virtual ou físico separado. Se tiver um cluster de desenvolvimento, em que mais do que um nó de Service Fabric é numa única máquina física ou virtual, tem de voltar a criar cluster Olá com a versão nova Olá.

Dois fluxos de trabalho distintos podem atualizar a versão mais recente do cluster toohello ou uma versão suportada do Service Fabric. Um fluxo de trabalho destina-se a clusters que têm a versão mais recente do conectividade toodownload Olá automaticamente. Olá outro fluxo de trabalho é para os clusters que não têm a versão de Service Fabric conectividade toodownload Olá mais recente.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Atualizar clusters com o código mais recente do conectividade toodownload Olá e a configuração
Utilize estes passos tooupgrade a versão de tooa suportada do cluster se os nós do cluster tem conectividade Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).

Para clusters com conectividade demasiado[http://download.microsoft.com](http://download.microsoft.com), Microsoft verifica periodicamente a existência de disponibilidade de Olá de novas versões de Service Fabric.

Quando estiver disponível uma nova versão de Service Fabric, Olá pacote é transferido localmente toohello cluster e aprovisionado para atualização. Além disso, cliente de Olá tooinform esta nova versão, o sistema Olá mostra um aviso de estado de funcionamento de explícita de cluster que é semelhante toohello seguintes:

"o suporte da versão [versão #] cluster atual Olá termina [Date]".

Depois do cluster de Olá está a executar a versão mais recente do Olá, aviso Olá passa ausente.

#### <a name="cluster-upgrade-workflow"></a>Fluxo de trabalho de atualização de cluster
Depois de ver o aviso de estado de funcionamento do cluster Olá, Olá a seguir:

1. Ligar toohello cluster a partir de qualquer computador que tenha máquinas Olá de tooall de acesso de administrador que estão listadas como nós num cluster de Olá. Olá que este script é executado no não ter toobe parte do cluster de Olá.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Obter a lista de Olá das versões de Service Fabric que pode atualizar para o.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Pode ser obtido um toothis semelhante de saída:

    ![obter versões de recursos de infraestrutura][getfabversions]
3. Inicie uma versão disponível de tooan de atualização de cluster utilizando o [início ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) cmd do PowerShell.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   progresso de Olá toomonitor da atualização de Olá, pode utilizar o Service Fabric Explorer ou Olá executar seguinte comando do Windows PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Se não forem satisfeitas as políticas de estado de funcionamento do cluster Olá, atualização Olá é revertida. políticas de estado de funcionamento personalizado toospecify para Olá **início ServiceFabricClusterUpgrade** comando, consulte a documentação para [início ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Depois de corrigir os problemas de Olá que resultaram numa reversão Olá, inicie novamente a atualização Olá pelo seguinte Olá mesmos passos conforme descritos anteriormente.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Atualizar clusters que tenham <U>sem conectividade</u> código mais recente do toodownload Olá e a configuração
Utilize estes passos tooupgrade a versão de tooa suportada do cluster se os nós do cluster não tem conectividade Internet demasiado[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Se estiver a executar um cluster que não é toohello ligado à Internet, terá toomonitor toolearn de blogue da equipa de Service Fabric de Olá sobre uma nova versão. sistema de Olá não mostra um tooalert de aviso do Estado de funcionamento de cluster de uma nova versão.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Vs de aprovisionamento automático de aprovisionamento Manual
transferência automática de tooenable e o registo para a versão de código mais recente Olá, configurar o serviço de atualização do serviço de recursos de infraestrutura. Consulte toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt dentro Olá [autónomo pacote](service-fabric-cluster-standalone-package-contents.md) para obter instruções.
Para o processo manual, siga as instruções de Olá abaixo.

Modificar o Olá tooset do cluster configuração seguinte propriedade toofalse antes de iniciar uma atualização da configuração.

        "fabricClusterAutoupgradeEnabled": false,

Consulte demasiado[início ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) para detalhes de utilização. Certifique-se de que tooupdate 'clusterConfigurationVersion' no seu JSON antes de iniciar a atualização da configuração de Olá.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Fluxo de trabalho de atualização de cluster

1. Execute Get-ServiceFabricClusterUpgrade a partir de um de nós de Olá no cluster de Olá e tenha em atenção Olá TargetCodeVersion.
2. Seguinte Olá execução de um toolist de computador ligado à internet atualizar todas as versões compatíveis com a versão atual do Olá e transferir Olá correspondente do pacote de ligações de transferência associados Olá.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Ligar toohello cluster a partir de qualquer computador que tenha máquinas Olá de tooall de acesso de administrador que estão listadas como nós num cluster de Olá. máquina Olá que este script é executado no não tem toobe parte do cluster de Olá

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Copie o pacote de Olá transferido para o arquivo de imagens do cluster Olá.

5. Registe o pacote de Olá copiado.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Inicie uma versão disponível de tooan atualização do cluster.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer, ou pode executar Olá seguinte comando do PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Se não forem satisfeitas as políticas de estado de funcionamento do cluster Olá, atualização Olá é revertida. políticas de estado de funcionamento personalizado toospecify para Olá **início ServiceFabricClusterUpgrade** comando, consulte a documentação de Olá para [início ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Depois de corrigir os problemas de Olá que resultaram numa reversão Olá, inicie novamente a atualização Olá pelo seguinte Olá mesmos passos conforme descritos anteriormente.


## <a name="upgrade-hello-cluster-configuration"></a>Atualizar a configuração de cluster Olá
Antes de iniciar a atualização da configuração de Olá, pode testar a sua nova json de configuração de cluster executando o script do powershell Olá no pacote de autónomo Olá.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
ou

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Algumas configurações não podem ser atualizado, como pontos finais, nome do cluster, IP de nó, etc. Isto irá testar Olá novo cluster configuração json contra Olá antigo e gerar erros na janela do Powershell Olá, se existir qualquer problema.

atualização de configuração de cluster de Olá tooupgrade, execute **início ServiceFabricClusterConfigurationUpgrade**. atualização da configuração de Olá é processado domínio de atualização por domínio de atualização.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Atualização de configuração do certificado de cluster  
Certificado de cluster é utilizado para autenticação entre nós de cluster, para que o rollover de certificado Olá devem ser efetuadas com cuidado extra porque falha irá bloquear a comunicação de Olá entre nós de cluster.  
Tecnicamente, são suportadas três opções:  

1. Atualização do certificado único: é o caminho de atualização de Olá ' certificado de um site (primário) -> B do certificado (primário) -> certificado C (primário) ->... '.   
2. Duplo atualização do certificado: é o caminho de atualização de Olá ' certificado de um site (primário) -> certificado (principal) e B (secundário) -> B do certificado (primário) -> B do certificado (principal) e C (secundário) -> certificado C (primário) ->... '.
3. Atualização do tipo de certificado: baseado na Thumbprint do certificado <> - certificado com base em CommonName configuração. Por exemplo, o Thumbprint do certificado (principal) e Thumbprint B (secundário)-C. CommonName do certificado >


## <a name="next-steps"></a>Passos seguintes
* Saiba como toocustomize algumas [definições de cluster do Service Fabric](service-fabric-cluster-fabric-settings.md).
* Saiba como demasiado[reduzir e ampliar o seu cluster](service-fabric-cluster-scale-up-down.md).
* Saiba mais sobre [as atualizações de aplicações](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
