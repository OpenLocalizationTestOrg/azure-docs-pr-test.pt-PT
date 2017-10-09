---
title: "aaaDeploy e atualizar micro-serviços do Azure localmente | Microsoft Docs"
description: "Saiba como implementar um tooit de aplicação existentes tooset configurar um cluster do Service Fabric local e, em seguida, atualizar essa aplicação."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Introdução à implementação e atualização de aplicações no seu cluster local
Olá SDK de Service Fabric do Azure inclui um ambiente de desenvolvimento local completo que pode utilizar tooquickly introdução à implementação e gestão de aplicações num local cluster. Neste artigo, criar um cluster local, implementar um tooit aplicação existente e, em seguida, atualizar essa aplicação tooa nova versão, tudo a partir do Windows PowerShell.

> [!NOTE]
> Este artigo assume que já [configurou o seu ambiente de desenvolvimento](service-fabric-get-started.md).
> 
> 

## <a name="create-a-local-cluster"></a>Criar um cluster local
Um cluster de Service Fabric representa um conjunto de recursos de hardware em que pode implementar aplicações. Normalmente, um cluster é constituído por qualquer ponto de cinco toomany milhares de máquinas. No entanto, Olá SDK de Service Fabric inclui uma configuração de cluster que pode ser executadas num único computador.

É importante toounderstand Olá cluster do Service Fabric local não é um emulador ou simulador. Este é executado Olá mesmo código de plataforma que se encontra nos clusters de várias máquinas. Step-by-Olá única diferença é que os processos de plataforma de Olá que normalmente estão dispersos por cinco máquinas num computador que executa.

Olá SDK fornece duas formas tooset configurar um cluster local: um Windows PowerShell script e Olá Gestor de clusters locais aplicação de tabuleiro sistema. Neste tutorial, utilizamos o script do PowerShell Olá.

> [!NOTE]
> Se já criou um cluster local quando implementou uma aplicação do Visual Studio, pode ignorar esta secção.
> 
> 

1. Inicie uma nova janela do PowerShell como administrador.
2. Execute script de configuração de cluster Olá a partir da pasta SDK Olá:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    A configuração do cluster demora alguns minutos. Após a conclusão do programa de configuração, deverá ver resultados semelhantes ao seguinte:
   
    ![Saída do programa de configuração do cluster][cluster-setup-success]
   
    Agora, está pronto tootry implementar um cluster de tooyour de aplicação.

## <a name="deploy-an-application"></a>Implementar uma aplicação
Olá SDK de Service Fabric inclui um conjunto avançado de estruturas e ferramentas para programadores para criar aplicações. Se estiver interessado no learning como toocreate aplicações no Visual Studio, consulte [criar a primeira aplicação de Service Fabric no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

Neste tutorial, a utilização de uma aplicação de exemplo existente (denominada WordCount) para poder concentrar nos aspetos de gestão de Olá da plataforma de Olá: implementação, monitorização e a atualização.

1. Inicie uma nova janela do PowerShell como administrador.
2. Importe o módulo do PowerShell de SDK do Service Fabric de Olá.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Crie uma aplicação Olá toostore de diretório que transferir e implementar, tais como C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Transferir a aplicação de WordCount Olá](http://aka.ms/servicefabric-wordcountapp) toohello localização criada.  Nota: o browser Microsoft Edge de Olá guarda o ficheiro de Olá com um *. zip* extensão.  Alterar a extensão de ficheiro Olá demasiado*. sfpkg*.
5. Ligue o toohello local cluster:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Crie uma nova aplicação utilizando o comando de implementação do SDK Olá com um nome e um pacote de aplicação toohello do caminho.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Se tudo correr bem, deverá ver Olá seguinte saída:
   
    ![Implementar um cluster local de toohello de aplicação][deploy-app-to-local-cluster]
7. aplicação de Olá toosee em ação, inicie Olá navegador e navegue demasiado[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html). Deverá ver:
   
    ![Interface do utilizador da aplicação implementada][deployed-app-ui]
   
    Olá aplicação WordCount é simple. Inclui o lado do cliente JavaScript código toogenerate aleatórios cinco carateres "palavras", que são, em seguida, retransmitidas toohello aplicação através da API Web do ASP.NET. Um serviço com estado controla o número de Olá de palavras contadas. Criam-se partições com base no primeiro caráter de Olá do word Olá. Pode encontrar o código de origem Olá para a aplicação de WordCount Olá no Olá [clássico exemplos de introdução](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    aplicação Olá que foi implementada contém quatro partições. Para que as palavras que começam de À G são armazenadas na partição primeiro Olá, palavras de h a N são armazenadas na segunda partição de Olá e assim sucessivamente.

## <a name="view-application-details-and-status"></a>Ver detalhes e estado da aplicação
Agora que Implementámos a aplicação Olá, vamos ver alguns dos detalhes da aplicação Olá no PowerShell.

1. Consulta todas as aplicações implementadas no cluster de Olá:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Partindo do princípio que só implementou a aplicação de WordCount Olá, verá algo semelhante a:
   
    ![Consultar todas as aplicações implementadas no PowerShell][ps-getsfapp]
2. Aceda toohello próximo nível consultando o conjunto de Olá de serviços que estão incluídos na aplicação de WordCount Olá.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista de serviços para aplicação Olá no PowerShell][ps-getsfsvc]
   
    aplicação Olá é constituída por dois serviços, o front-end Olá web e o serviço de monitorização de estado Olá que gere palavras Olá.
3. Por fim, observe lista Olá de partições para WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Ver Olá partições de serviço no PowerShell][ps-getsfpartitions]
   
    Olá, conjunto de comandos que utilizou como todos os comandos do PowerShell de Service Fabric, estão disponíveis para qualquer cluster a que poderá ligar, local ou remoto.
   
    Para um toointeract de forma mais visual com o cluster de Olá, pode utilizar a ferramenta de Service Fabric Explorer baseado na web Olá navegando demasiado[http://localhost:19080/Explorer](http://localhost:19080/Explorer) no browser Olá.
   
    ![Ver detalhes da aplicação no Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > toolearn mais acerca do Service Fabric Explorer, consulte [visualizar o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Atualizar uma aplicação
O Service Fabric fornece atualizações sem tempo de indisponibilidade através da monitorização de estado de funcionamento de Olá da aplicação Olá, que implementa no cluster Olá. Efetue uma atualização de Olá aplicação WordCount.

nova versão de Olá da aplicação Olá agora conta apenas as palavras que começam por uma vogal. Como Olá atualização se faz, vemos duas alterações de comportamento da aplicação Olá. Em primeiro lugar, taxa de Olá que aumenta a contagem de Olá mais lenta, uma vez que estão a ser contadas menos palavras. Segundo, uma vez que a primeira partição de Olá tem duas vogais (A e E) e todas as outras partições contêm apenas uma, a contagem deverá finalmente deve começar toooutpace Olá outras pessoas.

1. [Transferir o pacote de versão 2 do WordCount Olá](http://aka.ms/servicefabric-wordcountappv2) toohello mesma localização onde transferiu o pacote de versão 1 olá.
2. Devolver a janela do PowerShell tooyour e utilize o comando de atualização do SDK de Olá tooregister Olá nova versão no cluster de Olá. Em seguida, comece a atualizar a infraestrutura de Olá: / aplicação WordCount.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Deverá ver a seguinte Olá saída no PowerShell, como Olá atualização começa.
   
    ![Progresso da atualização do PowerShell][ps-appupgradeprogress]
3. Enquanto Olá atualização está a decorrer, pode encontrá-lo mais fácil toomonitor o estado do Service Fabric Explorer. Inicie uma janela do browser e navegue demasiado[http://localhost:19080/Explorer](http://localhost:19080/Explorer). Expanda **aplicações** na árvore de Olá Olá esquerda, em seguida, escolha **WordCount**e, finalmente, **fabric: / WordCount**. No separador de essentials Olá, ver estado Olá da atualização de Olá como medida que avança nos domínios de atualização do cluster Olá.
   
    ![Parar um nó no Service Fabric Explorer][sfx-upgradeprogress]
   
    Como as prossegue atualização Olá através de cada domínio, verificações de estado de funcionamento são executada tooensure que aplicação Olá está a comportar corretamente.
4. Se voltar a executar Olá anteriormente consultar do conjunto de Olá de serviços nos recursos de infraestrutura Olá: / WordCount aplicação, tenha em atenção que a versão do wordcountservice foi alterada de Olá mas Olá versão do WordCountWebService não:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar os serviços de aplicações após atualização][ps-getsfsvc-postupgrade]
   
    Este exemplo realça como o Service Fabric gere as atualizações de aplicações. Toca apenas Olá conjunto de serviços (ou pacotes de código/configuração dentro desses serviços) que tenham sido alterados, tornando o processo de Olá de atualização mais rápido e mais fiável.
5. Por último, regresse toohello browser tooobserve Olá comportamento nova versão da aplicação Olá. Conforme esperado, Olá contagem avança-ser mais lentamente e Olá primeira partição termina com um pouco mais de volume Olá.
   
    ![Nova versão da vista Olá da aplicação Olá no browser Olá][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Limpeza
Antes de concluir, é importante tooremember Olá local cluster é real. As aplicações continuam toorun em segundo plano de Olá até que remova-os.  Dependendo da natureza Olá das suas aplicações, uma aplicação em execução pode consumir recursos significativos no seu computador. Tem várias aplicações de toomanage opções e cluster Olá:

1. tooremove uma aplicação individual e todos os-lo da dados, execute Olá os seguintes comandos:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Ou, elimine a aplicação Olá da Olá Service Fabric Explorer **AÇÕES** menu ou o menu de contexto de Olá na vista de lista do lado esquerdo da aplicação Olá.
   
    ![Eliminar uma aplicação no Service Fabric Explorer][sfe-delete-application]
2. Depois de eliminar aplicação Olá do cluster de Olá, anular o registo das versões 1.0.0 e 2.0.0 do Olá tipo de aplicação de WordCount. Eliminação remove pacotes de aplicações de Olá, incluindo o código de Olá e a configuração, do cluster Olá arquivo de imagens.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Ou, no Service Fabric Explorer, escolha **tipo de não aprovisionamento** para aplicação Olá.
3. tooshut baixo cluster Olá, mas manter dados da aplicação Olá e rastreios, clique em **parar Cluster Local** na aplicação de tabuleiro de sistema Olá.
4. cluster de Olá toodelete totalmente, clique em **remover Cluster Local** na aplicação de tabuleiro de sistema Olá. Esta opção resultará na outra Olá de implementação lenta próxima vez que premir F5 no Visual Studio. Remova cluster local Olá apenas se não tenciona toouse-la para algum tempo ou se necessitar de tooreclaim recursos.

## <a name="one-node-and-five-node-cluster-mode"></a>Modo do cluster de cinco nós e um nó
Ao desenvolver aplicações, irá frequentemente fazer iterações rápidas de escrita de código, depuração e alteração de código. toohelp otimizar este processo, o cluster local Olá pode executar em dois modos: um nó ou cinco nós. Ambos os modos de cluster têm as suas vantagens. Modo de cluster de cinco nós permite-lhe toowork com um cluster real. Pode testar cenários de ativação pós-falha, trabalhar com mais instâncias e réplicas dos seus serviços. O modo de um nó de cluster é toodo otimizada de implementação rápida e o registo dos serviços, toohelp rapidamente validar o código utilizando o tempo de execução do Olá Service Fabric.

Os modos do cluster de um nó e de cinco nós não são um emulador ou simulador. cluster de desenvolvimento local Olá executa Olá mesmo código de plataforma que se encontra nos clusters de várias máquinas.

> [!WARNING]
> Quando alterar o modo de cluster de Olá, o cluster atual Olá é removido do sistema e é criado um novo cluster. dados de Olá armazenados Olá cluster são eliminados quando alterar o modo de cluster.
> 
> 

toochange Olá modo tooone cluster de nó, selecione **comutador Cluster modo** no Olá Gestor de clusters locais do serviço de recursos de infraestrutura.

![Alternar o modo do cluster][switch-cluster-mode]

Em alternativa, alterar o modo de cluster Olá através do PowerShell:

1. Inicie uma nova janela do PowerShell como administrador.
2. Execute script de configuração de cluster Olá a partir da pasta SDK Olá:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    A configuração do cluster demora alguns minutos. Após a conclusão do programa de configuração, deverá ver resultados semelhantes ao seguinte:
   
    ![Saída do programa de configuração do cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a>Passos seguintes
* Agora que implementou e atualizou algumas aplicações pré-criadas, pode [tentar criar a sua no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Todas as ações de Olá executadas no cluster local Olá este artigo podem ser efetuadas num [cluster do Azure](service-fabric-cluster-creation-via-portal.md) bem.
* atualização de Olá que efetuámos neste artigo foi básica. Consulte Olá [documentação de atualização](service-fabric-application-upgrade.md) toolearn mais informações sobre a capacidade de Olá e a flexibilidade das atualizações do Service Fabric.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
