---
title: "aaaAzure pacote autónoma de recursos de infraestrutura de serviço para o Windows Server | Microsoft Docs"
description: "Descrição e o conteúdo do pacote do Azure Service Fabric Standalone Olá para o Windows Server."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Conteúdo do pacote de serviço Fabric autónoma para o Windows Server
No Olá [transferido](http://go.microsoft.com/fwlink/?LinkId=730690) pacote autónoma do Service Fabric, encontrará Olá os seguintes ficheiros:

| **Nome de ficheiro** | **Breve descrição** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Um script do PowerShell que cria o cluster de Olá utilizando as definições de Olá em Clusterconfig. |
| RemoveServiceFabricCluster.ps1 |Um script do PowerShell que remove um cluster utilizando as definições de Olá em Clusterconfig. |
| AddNode.ps1 |Um script do PowerShell para adicionar um tooan de nó existentes implementadas cluster na máquina atual Olá. |
| RemoveNode.ps1 |Um script do PowerShell para remover um nó do existente implementada cluster da máquina atual Olá. |
| CleanFabric.ps1 |Um script do PowerShell para a instalação do Service Fabric desativar máquina atual Olá autónoma de limpeza. Instalações anteriores do MSI devem ser removidas utilizando os seus próprios uninstallers associados. |
| TestConfiguration.ps1 |Um script do PowerShell para analisar a infraestrutura de Olá conforme especificado no Olá Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Um script do PowerShell utilizado para transferir o pacote em tempo de execução mais recente Olá fora de banda, para cenários onde Olá implementar a máquina não está ligado toohello internet. |
| DeploymentComponentsAutoextractor.exe |Extração arquivo que contenha os componentes de implementação automática ser utilizado por Olá scripts de pacote autónomo. |
| EULA_ENU.txt |utilizam termos de licenciamento de Olá para Olá do pacote do Microsoft Azure Service Fabric autónomo do Windows Server. Pode [transferir uma cópia do Olá EULA](http://go.microsoft.com/fwlink/?LinkID=733084) agora. |
| Readme.txt |Uma ligação toohello notas de versão e as instruções de instalação básico. É um subconjunto de instruções de Olá neste documento. |
| ThirdPartyNotice.rtf |Aviso de software de terceiros que se encontra num pacote de Olá. |
| Tools\Microsoft.Azure.ServiceFabric.Windowsserver.SupportPackage.zip |StandaloneLogCollector.exe qual é executado no rastreio de pedido toocollect e carregar registos tooMicrosoft para fins de suporte. |
| Tools\ServiceFabricUpdateService.zip |Uma ferramenta utilizadas atualização de código tooenable automática em clusters que não têm acesso à internet. Pode encontrar mais detalhes sobre [aqui](service-fabric-cluster-upgrade-windows-server.md)|

**Modelos** 
| **Nome de ficheiro** | **Breve descrição** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Um ficheiro de exemplo de configuração do cluster contém Olá as definições para um protegida, três nós, máquina único (ou máquina virtual) cluster de desenvolvimento, incluindo informações de Olá para cada nó no cluster de Olá. |
| ClusterConfig.Unsecure.MultiMachine.json |Um ficheiro de exemplo de configuração do cluster contém Olá definições para um cluster não segura, multi máquina (ou máquina virtual), incluindo informações de Olá para cada máquina no cluster de Olá. |
| ClusterConfig.Windows.DevCluster.json |Um ficheiro de exemplo de configuração do cluster contém cluster todos os de desenvolvimento do definições para um único-máquina seguro e três nós, (ou máquina virtual) Olá, incluindo informações de Olá para cada nó que esteja num cluster de Olá. cluster de Olá é protegida pela utilização [identidades Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Um ficheiro de exemplo de configuração do cluster contém todas as definições de Olá para um cluster de máquina multi (ou máquina virtual) segura, utilizar a segurança do Windows, incluindo informações de Olá para cada máquina que esteja num cluster segura Olá. cluster de Olá é protegida pela utilização [identidades Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Um ficheiro de exemplo de configuração do cluster contém todas as definições Olá seguro e três nós, máquina único (ou máquina virtual) desenvolvimento cluster, incluindo informações de Olá para cada nó no cluster de Olá. Olá cluster está protegido por x509 certificados. |
| ClusterConfig.x509.MultiMachine.json |Proteger um ficheiro de exemplo de configuração de cluster que contém todas as definições Olá Olá, cluster máquina multi (ou máquina virtual), incluindo informações de Olá para cada nó no cluster segura Olá. Olá cluster está protegido por x509 certificados. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Proteger um ficheiro de exemplo de configuração de cluster que contém todas as definições Olá Olá, cluster máquina multi (ou máquina virtual), incluindo informações de Olá para cada nó no cluster segura Olá. Olá cluster está protegido por [contas de serviço geridas de grupo](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Exemplos de configuração de cluster
Versões mais recentes dos modelos de configuração do cluster podem ser encontradas na página do GitHub Olá: [exemplos de configuração de Cluster autónomo](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Pacote de tempo de execução independente
pacote de tempo de execução mais recente Olá é transferido automaticamente durante a implementação de cluster do [hiperligação Transferir - tempo de execução do serviço de recursos de infraestrutura - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Relacionado
* [Criar um cluster do Azure Service Fabric autónomo](service-fabric-cluster-creation-for-windows-server.md)
* [Cenários de segurança de cluster do Service Fabric](service-fabric-windows-cluster-windows-security.md)
