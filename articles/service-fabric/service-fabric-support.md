---
title: "aaaLearn sobre as opções de suporte de recursos de infraestrutura de serviço do Azure | Microsoft Docs"
description: "Versões de cluster do Service Fabric do Azure suportada e liga toofile pedidos de suporte"
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Opções de suporte do Azure Service Fabric

carrega toodeliver Olá adequado o suporte para os clusters de Service Fabric que está a executar o trabalho de aplicação no, iremos configurar várias opções para si. Dependendo da Olá nível de suporte necessários e gravidade Olá problema Olá, receber toopick opções direita Olá. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Problemas de site em direto ou de produção de relatórios ou peça ao apoio pago do Azure

Para comunicar problemas de site em direto no cluster do Service Fabric implementado no Azure, abra um pedido de suporte profissional [no portal do Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) ou [portal de suporte da Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Saiba mais sobre:
 
- [Suporte profissional da Microsoft para o Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Suporte da Microsoft premier](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Comunicar problemas de site em direto ou de produção ou de pedido de suporte pago autónomo que clusters do Service Fabric

Para relatórios de problemas de site em direto no cluster do Service Fabric implementado no local ou outras nuvens, abra um pedido de suporte profissional no [portal de suporte da Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Saiba mais sobre:

- [Suporte profissional da Microsoft para on-premises](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Suporte da Microsoft premier](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Problemas de relatório do Azure Service Fabric 
Ter configuramos um repositório do GitHub para relatórios de problemas do Service Fabric.  Podemos também ativamente está a monitorizar Olá fóruns a seguir.

### <a name="github-repo"></a>Repositório do GitHub 
Comunicar problemas de recursos de infraestrutura de serviço do Azure no [repositório de git de problemas de recursos de infraestrutura de serviço](https://github.com/Azure/service-fabric-issues). Este repositório destina-se de relatórios e controlo problemas com o Azure Service Fabric e para efetuar pedidos de funcionalidades pequeno. **Utilize este tooreport live-site emite**.

### <a name="stackoverflow-and-msdn-forums"></a>Fóruns StackOverflow e MSDN

Olá [etiquetas de Service Fabric no StackOverflow] [ stackoverflow] e Olá [fórum de Service Fabric no MSDN] [ msdn-forum] são melhor utilizada para fazer perguntas sobre como funciona a plataforma de Olá e como pode realizar algumas tarefas com o mesmo.

### <a name="azure-feedback-forum"></a>Fórum de comentários do Azure

Olá [fórum de comentários do Azure para o Service Fabric] [ uservoice-forum] é Olá melhor local para submeter ideias grande funcionalidade tiver do produto Olá, vamos analisar pedidos mais populares Olá fazem parte do nosso toolong prazo médio planeamento. Aconselhamo-lo toorally suporte para as sugestões dentro da Comunidade de Olá.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Versões suportadas do Service Fabric.

Certifique-se de que o cluster sempre está em execução uma versão suportada do Service Fabric. Como e quando é anunciar o lançamento de Olá de uma nova versão de Service Fabric, versão anterior do Olá está marcado para fim de suporte após 60 dias dessa data, no mínimo. Olá novos lançamentos sejam anunciados [no blogue de equipa do Service Fabric Olá](https://blogs.msdn.microsoft.com/azureservicefabric/).

Consulte toohello seguintes documentos em obter detalhes sobre como tookeep cluster executar uma versão suportada do Service Fabric.

- [Atualizar a versão de Service Fabric num cluster do Azure](service-fabric-cluster-upgrade.md)
- [Atualizar a versão de Service Fabric num cluster de servidores windows autónomo](service-fabric-cluster-upgrade-windows-server.md)
 
Seguem-se a lista de Olá de versões de Service Fabric Olá que são suportadas e as respetivas datas de fim de suporte.

| **Cluster de tempo de execução do Service Fabric** | **SDK compatível / versões do pacote NuGet** | **Fim do suporte de data** |
| --- | --- | --- |
| Todos os too5.3.121 anterior de versões de cluster |Menor ou igual tooversion 2.3 |20 de Janeiro de 2017 |
| 5.3.* |Menor ou igual tooversion 2.3 |24 de Fevereiro de 2017 |
| 5.4.* |Menor ou igual tooversion 2.4 |Pode 10,2017     |
| 5.5.* |Menor ou igual tooversion 2,5 |Agosto 10,2017    |
| 5.6.* |Menor ou igual tooversion 2.6 |Outubro 13,2017    |
| 5.7.* |Menor ou igual tooversion 2.7 |Versão atual e, por isso, sem data de fim

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Versões de pré-visualização de recursos de infraestrutura do serviço - não suportadas para utilização em produção.
De tempo tootime, iremos lançamento de versões com funcionalidades significativas queremos comentários, que são lançadas como pré-visualizações. Estas versões de pré-visualização só devem ser utilizadas para fins de teste. O cluster de produção deve sempre ser em execução uma versão de Service Fabric suportada e estável. Uma versão de pré-visualização sempre começa com um número de versão principal e secundária de 255. Por exemplo, se vir uma versão 255.255.5703.949 do Service Fabric, essa versão é toobe apenas utilizado em clusters de teste e está em pré-visualização. Estas versões de pré-visualização também sejam anunciadas no Olá [blogue da equipa do Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric) e irá ter detalhes no Olá funcionalidades incluídas.

Não há nenhuma opção de suporte pago para estas versões de pré-visualização. Utilize uma das opções de Olá listadas na [relatório Azure Service Fabric emite](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) tooask questões ou comentários.

## <a name="next-steps"></a>Passos seguintes

- [Versão de recursos de infraestrutura de serviço de atualização num cluster do Azure](service-fabric-cluster-upgrade.md)
- [Atualizar a versão de Service Fabric num cluster de servidores windows autónomo](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
