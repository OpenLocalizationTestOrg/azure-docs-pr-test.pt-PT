---
title: "Segurança de cluster do Service Fabric: funções do cliente | Microsoft Docs"
description: "Este artigo descreve as funções de cliente de dois Olá e permissões de Olá fornecidas toohello funções."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Controlo de acesso baseado em funções para clientes de Service Fabric
Azure Service Fabric suportam dois tipos de controlo de acesso diferentes para clientes que estejam ligados tooa cluster do Service Fabric: administrador e utilizador. Controlo de acesso permite Olá administrador toolimit acesso toocertain cluster operações de cluster para diferentes grupos de utilizadores, tornando o cluster de Olá mais segura.  

**Os administradores** têm acesso total toomanagement capacidades (incluindo as capacidades de leitura/escrita). Por predefinição, **utilizadores** apenas tem acesso de leitura toomanagement capacidades (por exemplo, capacidades de consulta) e os serviços e aplicações de tooresolve Olá capacidade.

Especifique funções do cliente Olá dois (administrador e cliente) momento Olá da criação do cluster ao fornecer certificados separados para cada. Consulte [segurança de cluster do Service Fabric](service-fabric-cluster-security.md) para obter detalhes sobre como configurar um cluster do Service Fabric seguro.

## <a name="default-access-control-settings"></a>Definições de controlo de acesso predefinida
tipo de controlo de acesso de administrador Olá tem Olá tooall de acesso total FabricClient APIs. Pode efetuar qualquer leituras e escritas no cluster do Service Fabric Olá, incluindo Olá seguintes operações:

### <a name="application-and-service-operations"></a>Operações de serviço e aplicação
* **CreateService**: a criação do serviço                             
* **CreateServiceFromTemplate**: a criação do modelo do serviço                             
* **UpdateService**: atualizações de serviço                             
* **DeleteService**: eliminação de serviço                             
* **ProvisionApplicationType**: aprovisionamento de tipo de aplicação                             
* **CreateApplication**: criação de aplicações                               
* **DeleteApplication**: eliminação de aplicação                             
* **UpgradeApplication**: a iniciar ou interromper as atualizações de aplicações                             
* **UnprovisionApplicationType**: tipo aplicação de anulação de aprovisionamento                             
* **MoveNextUpgradeDomain**: a retomar as atualizações de aplicações com um domínio de atualização explícita                             
* **ReportUpgradeHealth**: a retomar as atualizações de aplicações com o progresso da atualização atual Olá                             
* **ReportHealth**: relatório de estado de funcionamento                             
* **PredeployPackageToNode**: API de pré-implementação                            
* **CodePackageControl**: reiniciar pacotes de código                             
* **RecoverPartition**: recuperação de uma partição                             
* **RecoverPartitions**: recuperar partições                             
* **RecoverServicePartitions**: recuperar partições de serviço                             
* **RecoverSystemPartitions**: recuperar as partições de serviço do sistema                             

### <a name="cluster-operations"></a>Operações de cluster
* **ProvisionFabric**: cluster / MSI manifesto aprovisionamento                             
* **UpgradeFabric**: a iniciar as atualizações de cluster                             
* **UnprovisionFabric**: cluster / MSI manifesto anulação de aprovisionamento                         
* **MoveNextFabricUpgradeDomain**: a retomar a atualizações de cluster com um domínio de atualização explícita                             
* **ReportFabricUpgradeHealth**: a retomar a atualizações de cluster com o progresso da atualização atual Olá                             
* **StartInfrastructureTask**: iniciar tarefas de infraestrutura                             
* **FinishInfrastructureTask**: concluir tarefas de infraestrutura                             
* **InvokeInfrastructureCommand**: comandos de gestão de tarefas de infraestrutura                              
* **ActivateNode**: ativar um nó                             
* **DeactivateNode**: desativar um nó                             
* **DeactivateNodesBatch**: desativar vários nós                             
* **RemoveNodeDeactivations**: desativação de reversão em vários nós                             
* **GetNodeDeactivationStatus**: a verificar o estado de Desativação                             
* **NodeStateRemoved**: relatório de estado do nó removido                             
* **ReportFault**: relatório de falhas                             
* **FileContent**: a imagem de transferência de ficheiros de cliente de arquivo (toocluster externa)                             
* **FileDownload**: o início de transferência de ficheiro do arquivo de cliente (toocluster externa) da imagem                             
* **InternalList**: a imagem de arquivo de ficheiro lista a operação de cliente (interno)                             
* **Eliminar**: a imagem de operação de eliminação do arquivo de cliente                              
* **Carregar**: a operação de carregamento de cliente de arquivo de imagem                             
* **NodeControl**: a iniciar, parar e reiniciar nós                             
* **MoveReplicaControl**: mover as réplicas de um nó tooanother                             

### <a name="miscellaneous-operations"></a>Operações diversas
* **Ping**: pings de cliente                             
* **Consulta**: todas as consultas permitidas
* **NameExists**: verificações de existência de URI de nomenclatura                             

tipo de controlo de acesso de utilizador Olá está, por predefinição, toohello limitado seguintes operações: 

* **EnumerateSubnames**: atribuição de nomes de enumeração de URI                             
* **EnumerateProperties**: atribuição de nomes de enumeração da propriedade                             
* **PropertyReadBatch**: operações de leitura de atribuição de nome de propriedade                             
* **GetServiceDescription**: descrições de serviço de notificações de serviço de inquérito longo e leitura                             
* **ResolveService**: Resolução de serviço com base em conformidade                             
* **ResolveNameOwner**: Resolução proprietário URI de nomenclatura                             
* **ResolvePartition**: resolver serviços do sistema                             
* **ServiceNotifications**: notificações de serviço com base em eventos                             
* **GetUpgradeStatus**: consulta o estado de atualização da aplicação                             
* **GetFabricUpgradeStatus**: consulta o estado de atualização de cluster                             
* **InvokeInfrastructureQuery**: consultar as tarefas de infraestrutura                             
* **Lista**: operação de lista de ficheiros de cliente de arquivo de imagem                             
* **ResetPartitionLoad**: repor a carga de uma unidade de ativação pós-falha                             
* **ToggleVerboseServicePlacementHealthReporting**: ativando ou desativando a relatórios de estado de funcionamento de posicionamento do serviço verboso                             

controlo de acesso de administrador Olá tem também toohello acesso precedente operações.

## <a name="changing-default-settings-for-client-roles"></a>Alterar as predefinições para as funções do cliente
Ficheiro de manifesto cluster Olá, pode fornecer o cliente de toohello capacidades de administrador, se for necessário. Pode alterar as predefinições de Olá vai toohello **definições de recursos de infraestrutura** opção durante [criação de cluster](service-fabric-cluster-creation-via-portal.md)e fornecer Olá precedente definições no Olá **nome**, **admin**, **utilizador**, e **valor** campos.

## <a name="next-steps"></a>Passos seguintes
[Segurança de cluster do Service Fabric](service-fabric-cluster-security.md)

[Criação de cluster do Service Fabric](service-fabric-cluster-creation-via-portal.md)

