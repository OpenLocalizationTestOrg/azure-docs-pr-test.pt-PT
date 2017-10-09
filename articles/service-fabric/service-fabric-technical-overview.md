---
title: aaaLearn terminologia do Azure Service Fabric | Microsoft Docs
description: "Uma descrição geral de terminologia do Service Fabric. Descreve os conceitos de terminologia-chave e termos utilizados no rest Olá documentação Olá."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Descrição geral de terminologia do Service Fabric
Service Fabric é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implementar e gerir micro-serviços escaláveis e fiáveis. Este terminologia de Olá de detalhes tópico utilizada pelo Service Fabric toounderstand Olá termos utilizados na documentação de Olá.

Olá conceitos indicados nesta secção são também apresentados Olá seguir vídeos do Microsoft Virtual Academy: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">principais conceitos</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">conceitos do momento da conceção</a>, e <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">conceitos de tempo de execução</a>.

## <a name="infrastructure-concepts"></a>Conceitos de infraestrutura
**Cluster**: um conjunto de ligados à rede de máquinas virtuais ou físicos para o qual os micro-serviços são implementados e geridos.  Clusters podem Dimensionar toothousands de máquinas.

**Nó**: um computador ou a VM que faz parte de um cluster denomina-se um nó. Cada nó é atribuído um nome de nó (uma cadeia). Os nós têm características como propriedades de colocação. Cada computador ou a VM tem um serviço de início automático do Windows, `FabricHost.exe`, que inicia a executar após o arranque e, em seguida, inicia duas executáveis: `Fabric.exe` e `FabricGateway.exe`. Estes dois executáveis constituem nó Olá. Para cenários de teste, pode alojar vários nós num único computador ou VM ao executar várias instâncias do `Fabric.exe` e `FabricGateway.exe`.

## <a name="application-concepts"></a>Conceitos da aplicação
**Tipo de aplicação**: Olá nome/versão atribuído tooa coleção de tipos de serviço. Definidos num `ApplicationManifest.xml` ficheiro, incorporado um diretório do pacote de aplicação, que é, em seguida, copiado o arquivo de imagens do cluster do Service Fabric toohello. Em seguida, pode criar uma aplicação com o nome deste tipo de aplicação no cluster de Olá.

Olá leitura [modelo de aplicação](service-fabric-application-model.md) artigo para obter mais informações.

**Pacote de aplicação**: um diretório de disco que contém o tipo de aplicação a Olá `ApplicationManifest.xml` ficheiro. Referências Olá pacotes de serviços para cada tipo de serviço que constitui o tipo de aplicação Olá. ficheiros de Olá no diretório de pacote de aplicação Olá estão arquivo de imagens do cluster de recursos de infraestrutura tooService copiado. Por exemplo, um pacote de aplicação de um tipo de aplicação de e-mail pode conter o pacote de serviço de fila de tooa referências, um pacote de serviço de front-end e um pacote de serviço de base de dados.

**Com o nome de aplicação**: depois de um pacote de aplicação é copiado toohello arquivo de imagens, criar uma instância da aplicação Olá num cluster de Olá especificando um tipo de aplicação do pacote de aplicação Olá (utilizando o respetivo nome/versão). Cada instância de tipo de aplicação é atribuída um nome URI que se assemelha: `"fabric:/MyNamedApp"`. Num cluster, pode criar várias aplicações com o nome de um tipo de aplicação único. Também pode criar aplicações com o nome dos tipos de aplicação diferente. Cada aplicação nomeada é gerido e com a versão independentemente.      

**O tipo de serviço**: Olá. o nome/versão atribuído do serviço de tooa código pacotes, pacotes de dados e pacotes de configuração. Definidos num `ServiceManifest.xml` ficheiro, incorporado num diretório de pacote de serviço e diretório de pacote de serviço Olá, em seguida, é referenciado por um pacote de aplicação `ApplicationManifest.xml` ficheiro. Dentro do cluster de Olá, depois de criar uma aplicação com nome, pode criar um serviço com nome de um dos Olá tipos de serviço do tipo de aplicação. Olá, tipo de serviço `ServiceManifest.xml` ficheiro descreve serviço Olá.

Olá leitura [modelo de aplicação](service-fabric-application-model.md) artigo para obter mais informações.

Existem dois tipos de serviços:

* **Stateless:** utilizar um serviço sem monitorização de estado quando o estado persistente do serviço de Olá é armazenado num serviço armazenamento externo, como o Storage do Azure, SQL Database do Azure ou do Azure Cosmos DB. Utilize um serviço sem estado ao serviço Olá não tem nenhum armazenamento persistente de todo. Por exemplo, um Calculadora serviço onde os valores são transmitidos toohello serviço, a computação é efetuada utilizando estes valores e é devolvido um resultado.
* **Monitorização de estado:** utilizar um serviço com estado quando quiser toomanage de Service Fabric estado do serviço através das suas coleções fiável ou Reliable Actors modelos de programação. Especifique quantos partições pretende toospread o estado de ativação pós-falha (para escalabilidade) quando criar um serviço com nome. Também especificar quantas vezes tooreplicate o estado em nós (para fiabilidade). Cada serviço com nome tem uma única réplica primária e várias réplicas secundárias. Modificar o estado do serviço com nome escrevendo toohello de réplica primária. Em seguida, o Service Fabric replica este estado tooall Olá réplicas secundárias manter o estado sincronizado. Service Fabric Deteta automaticamente quando uma réplica primária falha e promove uma existente réplica primária de tooa de réplica secundária. Service Fabric, em seguida, cria uma nova réplica secundária.  

**Pacote de serviço**: um diretório de disco que contém o tipo de serviço a Olá `ServiceManifest.xml` ficheiro. Este ficheiro referencia código Olá, dados estáticos e pacotes de configuração para o tipo de serviço Olá. ficheiros de Olá no diretório de pacote de serviço Olá são referenciados por tipo de aplicação a Olá `ApplicationManifest.xml` ficheiro. Por exemplo, um pacote de serviço foi Consulte toohello código, dados estáticos e pacotes de configuração que compõem um serviço de base de dados.

**Com o nome de serviço**: depois de criar uma aplicação com nome, pode criar uma instância de um dos respetivos tipos de serviço no cluster de Olá especificando um tipo de serviço Olá (utilizando o respetivo nome/versão). Cada instância de tipo de serviço é atribuída um nome URI em URI da sua aplicação com o nome de âmbito. Por exemplo, se criar um serviço dentro de uma aplicação com o nome "MyNamedApp" com o nome "MyDatabase", Olá URI aspeto: `"fabric:/MyNamedApp/MyDatabase"`. Dentro de uma aplicação com nome, pode criar vários serviços com nome. Cada serviço com o nome pode ter o seu próprio esquema de partição e réplica/instância contagens.

**Pacote de código**: um diretório de disco que contém os ficheiros executáveis de tipo de serviço a Olá (normalmente, os ficheiros. EXE/DLL). ficheiros de Olá no diretório de pacote do código Olá são referenciados por tipo de serviço a Olá `ServiceManifest.xml` ficheiro. Quando é criado um serviço com nome, o pacote do código Olá é nó toohello copiado ou Olá toorun selecionado de nós com o nome de serviço. Em seguida, o código de Olá entra em execução. Existem dois tipos de executáveis de pacote do código:

* **Executáveis convidado**: executáveis que são executados como-no sistema de operativo de anfitrião Olá (Windows ou Linux). Ou seja, estes executáveis não referência de tooor de ligação não quaisquer ficheiros de tempo de execução do Service Fabric e, por conseguinte, não utilizem os modelos de programação do Service Fabric. Estes executáveis são toouse não é possível que algumas funcionalidades do Service Fabric, tais como Olá a atribuição de nomes de serviço para a deteção de ponto final. Executáveis convidado não podem reportar a instância de serviço de tooeach específico de métricas de carga.
* **Serviço de anfitrião executáveis**: executáveis que utilizam o Service Fabric programming modelos ao ligar os ficheiros de runtime de recursos de infraestrutura tooService, ativar funcionalidades do Service Fabric. Por exemplo, uma instância de serviço com o nome pode registar os pontos finais Naming Service do Service Fabric e também pode comunicar métricas de carga.      

**Pacote de dados**: um diretório de disco que contém ficheiros de dados estático só de leitura de tipo de serviço a Olá (normalmente, fotografias, som, vídeo ficheiros e). ficheiros de Olá no diretório de pacote de dados de Olá são referenciados por tipo de serviço a Olá `ServiceManifest.xml` ficheiro. Quando é criado um serviço com nome, o pacote de dados de Olá está toohello copiados nó ou Olá toorun selecionado de nós com o nome de serviço.  código de Olá entra em execução e pode agora aceder aos ficheiros de dados de Olá.

**Pacote de configuração**: um diretório de disco que contém estático do tipo de serviço Olá, ficheiros de configuração de só de leitura (normalmente, ficheiros de texto). ficheiros de Olá no diretório de pacote de configuração de Olá são referenciados por tipo de serviço a Olá `ServiceManifest.xml` ficheiro. Quando é criado um serviço com nome, ficheiros de Olá no pacote de configuração de Olá estão copiado toohello um ou mais Olá de toorun selecionado de nós com o nome do serviço. Em seguida, o código de Olá entra em execução e pode agora aceder aos ficheiros de configuração de Olá.

**Contentores**: por predefinição, o Service Fabric implementa e ativa serviços como processos. Serviço de recursos de infraestrutura também pode implementar serviços nas imagens de contentor. Contentores são uma tecnologia de Virtualização que Virtualiza o sistema operativo subjacente Olá de aplicações. Uma aplicação e respetivos bibliotecas de tempo de execução, dependências e do sistema executam dentro de um contentor com a vista de contentor próprio isolada toohello acesso completo, privada das construções de sistema operativo. Service Fabric suporta contentores de Docker em contentores de Linux e Windows Server.  Para obter mais informações, leia o artigo [Service Fabric e contentores](service-fabric-containers-overview.md).

**Esquema de partição**: ao criar um serviço com nome, especifique um esquema de partição. Serviços com grandes quantidades de estado dividir dados Olá por partições, que se propaga Estado Olá entre os nós do cluster Olá. Isto permite tooscale de estado do serviço com nome. Dentro de uma partição, os serviços com nome sem monitorização de estado ter instâncias enquanto serviços nomeados com monitorização de estado têm as réplicas. Normalmente, sem monitorização de estado com nome serviços apenas alguma vez de ter uma partição, uma vez que não têm nenhum Estado interno. instâncias de partição Olá fornecem disponibilidade; Se uma instância falhar, outras instâncias continuar toooperate normalmente e, em seguida, o Service Fabric irá criar uma nova instância. Com monitorização de estado com o nome dos serviços de manter o respetivo estado dentro de réplicas e cada partição tem a respetiva réplica com todos os Estados de Olá que está a ser mantido sincronizado. Se uma réplica falhar, o Service Fabric cria uma nova réplica de réplicas existentes Olá.

Olá leitura [serviços fiáveis partição Service Fabric](service-fabric-concepts-partitioning.md) artigo para obter mais informações.

## <a name="system-services"></a>Serviços do sistema
Existem serviços do sistema que são criados em cada cluster que fornecem capacidades de plataforma Olá do Service Fabric.

**Serviço de nomenclatura**: cluster de cada Service Fabric tem um serviço de nomes, o qual resolve localização tooa de nomes de serviço no cluster de Olá. Gerir nomes de serviço Olá e propriedades, semelhante tooan internet serviço DNS (Domain Name) para o cluster de Olá. Os clientes comunicam de forma segura com qualquer nó no cluster de Olá Olá Naming Service tooresolve a utilizar um nome de serviço e a respetiva localização.  Mover as aplicações no cluster Olá, por exemplo, devido toofailures, balanceamento de recurso ou Olá redimensionamento de cluster Olá. Pode desenvolver serviços e os clientes que resolver a localização de rede atual Olá. Os clientes obter o endereço IP Olá máquina real e a porta em que está atualmente a ser executado.

Leitura [Communicate com serviços](service-fabric-connect-and-communicate-with-services.md) para obter mais informações sobre Olá cliente serviço de comunicação e APIs que funcionam com Olá Naming service.

**Serviço de arquivo de imagem**: cluster de cada Service Fabric tem um serviço de arquivo de imagens onde os pacotes de aplicações implementadas, com a versão são mantidos. Copie um toohello de pacote de aplicação arquivo de imagens e, em seguida, registar o tipo de aplicação Olá contido nesse pacote de aplicação. Depois do tipo de aplicação Olá é aprovisionado, criar uma aplicação com o nome do mesmo. Pode anular o registo de um tipo de aplicação do serviço de arquivo de imagens de Olá depois de todas as aplicações com nome tem sido eliminadas.

Leitura [compreender a definição de ImageStoreConnectionString Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre Olá serviço de arquivo de imagens.

Olá leitura [implementar uma aplicação](service-fabric-deploy-remove-applications.md) artigo para obter mais informações sobre como implementar o serviço de arquivo de imagens de toohello de aplicações.

## <a name="built-in-programming-models"></a>Modelos de programação incorporados
Modelos de programação do .NET Framework estão disponíveis para que os serviços do Service Fabric toobuild:

**Reliable Services**: uma API toobuild sem monitorização de estado e com monitorização de estado dos serviços. Serviço com estado armazenar o respetivo estado em coleções fiável (por exemplo, um dicionário ou uma fila). Também obter tooplug em vários pilhas de comunicação, tais como Web API e Windows Communication Foundation (WCF).

**Reliable Actors**: uma API toobuild sem monitorização de estado e com monitorização de estado objetos através de Olá virtual Ator modelo de programação. Este modelo pode ser útil quando tem muitas unidades independentes de cálculo/estado. Uma vez que este modelo utiliza um modelo de thread baseado em por sua vez, é melhor código tooavoid que chama a atenção ou serviços de atores tooother, uma vez que um ator individuais não é possível processar outros pedidos recebidos, até que concluíram todos os seus pedidos de saída.

Olá leitura [escolher um modelo de programação para o seu serviço](service-fabric-choose-framework.md) artigo para obter mais informações.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Passos seguintes
toolearn mais sobre o Service Fabric:

* [Descrição geral do Service Fabric](service-fabric-overview.md)
* [Por que motivo um micro-serviços abordar toobuilding aplicações?](service-fabric-overview-microservices.md)
* [Cenários de aplicações](service-fabric-application-scenarios.md)

