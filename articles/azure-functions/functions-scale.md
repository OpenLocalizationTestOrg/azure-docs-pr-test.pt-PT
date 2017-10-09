---
title: "planos de consumo de funções e o serviço de aplicações aaaAzure | Microsoft Docs"
description: "Compreenda a forma como as funções do Azure dimensiona necessidades de Olá toomeet das cargas de trabalho condicionada por eventos."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Planos de consumo de funções e o serviço de aplicações do Azure 

## <a name="introduction"></a>Introdução

Pode executar as funções do Azure em dois modos diferentes: plano de consumo e o plano do App Service do Azure. plano de consumo Olá atribui automaticamente a capacidade de computação quando o código está em execução, aumenta horizontalmente de forma como a carga de toohandle necessário e dimensiona quando o código não está em execução. Por isso, não tem toopay para VMs Inativas e não tem capacidade de tooreserve antecipadamente. Este artigo incida no plano de consumo Olá. Para obter mais informações sobre como funciona o Olá plano do App Service, consulte Olá [descrição geral dos planos do App Service do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Se não estiver familiarizado com as funções do Azure, consulte Olá [descrição geral das funções do Azure](functions-overview.md).

Quando criar uma aplicação de função, tem de configurar um plano de alojamento para funções essa aplicação Olá contém. O modo, uma instância de Olá *anfitrião das funções do Azure* executa funções Olá. tipo de Olá dos controlos de plano:

* Como são ampliar instâncias de anfitrião.
* recursos de Olá que estão disponíveis tooeach anfitrião.

Atualmente, tem de escolher tipo de plano Olá durante a criação de Olá de aplicação de função Olá. Não é possível alterá-la mais tarde. 

Pode dimensionar entre camadas de Olá plano do App Service. Plano de consumo de Olá, das funções do Azure processa automaticamente todos os alocação de recursos.

## <a name="consumption-plan"></a>Plano de consumo

Quando estiver a utilizar um plano de consumo, instâncias de anfitrião de funções do Azure Olá dinamicamente serão adicionadas e removidas com base no número de Olá dos eventos recebidos. Este plano dimensiona automaticamente e são-lhe cobrados os recursos de computação apenas quando as suas funções estão em execução. Um plano de consumo, pode executar uma função para um máximo de 10 minutos. 

> [!NOTE]
> tempo limite predefinido de Olá para funções de um plano de consumo é de 5 minutos. valor de Olá pode ser aumentada too10 minutos para Olá aplicação de função alterando a propriedade Olá `functionTimeout` no [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Faturação é com base no tempo de execução e de memória utilizada e é agregado em todas as funções dentro de uma aplicação de função. Para obter mais informações, consulte Olá [das funções do Azure a página de preços].

plano de consumo Olá Olá predefinido e oferece Olá seguintes vantagens:
- Paga apenas quando as suas funções estão em execução.
- Aumentar horizontalmente automaticamente, mesmo durante períodos de alta carregar.

## <a name="app-service-plan"></a>Plano do App Service

Planear Olá do serviço de aplicações, as suas aplicações de função executam em VMs dedicadas em básicas, Standard e Premium SKUs, tooWeb aplicações semelhante. VMs dedicadas são alocados tooyour aplicações de serviço de aplicações, o que significa anfitrião de funções de Olá está sempre em execução.

Tenha em consideração um plano de serviço aplicacional Olá seguintes casos:
- Tem as VMs existentes, subutilizadas que já estejam a executar outras instâncias de serviço de aplicações.
- Esperar toorun de aplicações a função continuamente ou quase continuamente.
- Precisa de mais opções de CPU ou memória ao que é fornecido no plano de consumo Olá.
- É necessário toorun superior Olá tempo de execução máximo permitido no plano de consumo Olá.

Uma VM desassocia custo de tamanho de memória e tempo de execução. Como resultado, não será paga mais do que o custo de Olá de instância de VM de Olá que alocar. Para obter mais informações sobre como funciona o Olá plano do App Service, consulte Olá [descrição geral dos planos do App Service do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Com um plano de serviço de aplicações, pode manualmente aumentar horizontalmente adicionando mais instâncias VM ou, pode ativar o dimensionamento automático. Para obter mais informações, consulte [dimensionar a contagem de instâncias manual ou automaticamente](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). Também pode aumentar verticalmente ao escolher um plano de serviço aplicacional diferente. Para obter mais informações, consulte [aumentar verticalmente a uma aplicação no Azure](../app-service-web/web-sites-scale.md). Se estiver a planear funções de JavaScript toorun um plano de serviço de aplicações, deve escolher um plano que tenha menos núcleos. Para obter mais informações, consulte Olá [referência de JavaScript para funções](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###Always On

Se executar um plano de serviço de aplicações, deve ativar Olá **Always On** definição para que a aplicação de função é executada corretamente. Um plano de serviço de aplicações, tempo de execução de funções de Olá passa inativo após alguns minutos de inatividade, pelo que só acionadores HTTP "reativará" as suas funções. Isto é semelhante toohow que webjobs tem de ter Always On ativado. 

Always On só está disponível no plano de serviço aplicacional. Um plano de consumo plataforma Olá ativa a função aplicações automaticamente.

## <a name="storage-account-requirements"></a>Requisitos de conta de armazenamento

Um plano de consumo ou um plano do App Service, uma aplicação de função necessita de uma conta de armazenamento do Azure que suporta o armazenamento de tabela, fila e Blob do Azure. Internamente, as funções do Azure utiliza o armazenamento do Azure para operações como a gestão de acionadores e execuções de função de registo. Algumas contas de armazenamento não suportam as filas e tabelas, tais como contas de armazenamento apenas de BLOBs (incluindo o armazenamento premium) e contas de armazenamento para fins gerais com a replicação de armazenamento com redundância de zona. Estas contas são filtradas de Olá **conta de armazenamento** painel quando estiver a criar uma aplicação de função.

toolearn mais informações sobre tipos de conta de armazenamento, consulte [introdução dos serviços de armazenamento do Azure Olá](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Como funciona o plano de consumo Olá

plano de consumo Olá dimensiona automaticamente recursos de CPU e memória adicionando instâncias adicionais de anfitrião de funções de Olá, com base no número de Olá dos eventos que as funções são acionadas no. Cada instância de anfitrião de funções de Olá é limitado too1.5 GB de memória.

Quando utiliza Olá consumo plano de alojamento, ficheiros de código de função são armazenados em partilhas de ficheiros do Azure numa conta de armazenamento principal Olá. Ao eliminar a conta de armazenamento principal Olá, este conteúdo é eliminado e não pode ser recuperado.

> [!NOTE]
> Quando estiver a utilizar um acionador de blob um plano de consumo, podem existir se o atraso de 10 minutos tooa processar novos blobs, se uma aplicação de função tornou-se inativo. Depois de executa a aplicação de função Olá, blobs são processados imediatamente. tooavoid neste inicial atrasar, considere uma das seguintes opções de Olá:
> - Utilize um plano de serviço de aplicações com Always On ativado.
> - Utilize o blob de Olá tootrigger outro mecanismo processar, tais como uma mensagem de fila que contém o nome do blob Olá. Por exemplo, consulte [enlace de entrada de Acionador de fila com o blob](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Dimensionamento de tempo de execução

As funções do Azure utiliza um componente denominado Olá *controlador escala* toomonitor Olá taxa de eventos e determinar se tooscale out ou reduzir verticalmente. controlador de escala Olá utiliza a heurística para cada tipo de Acionador. Por exemplo, quando estiver a utilizar um acionador de armazenamento de filas do Azure, dimensiona com base no comprimento da fila Olá e idade Olá de mensagem de fila Olá mais antiga.

unidade de Olá da escala é Olá aplicação de função. Quando a aplicação de função Olá é ampliada, mais recursos são atribuídos toorun várias instâncias do anfitrião do Olá das funções do Azure. Por outro lado, como a computação a pedido é reduzida, o controlador de escala Olá remove instâncias de anfitrião de função. o número de instâncias Olá, eventualmente, é dimensionado para baixo toozero quando não funciona em execução dentro de uma aplicação de função.

![Controlador de escala eventos de monitorização e criação de instâncias](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Modelo de faturação

Faturação do plano de consumo Olá é descrito detalhadamente no Olá [das funções do Azure a página de preços]. Utilização é agregada ao nível de aplicação de função Olá e contagens apenas o tempo de Olá que está a executar o código de função. Olá, são unidades de faturação: 
* **Consumo de recursos em segundos de gigabyte (GB-s)**. Calculada como uma combinação de tamanho de memória e tempo de execução para todas as funções dentro de uma aplicação de função. 
* **Execuções**. Contados sempre que uma função for executada no evento de tooan de resposta, acionado por um enlace.

[das funções do Azure a página de preços]: https://azure.microsoft.com/pricing/details/functions
