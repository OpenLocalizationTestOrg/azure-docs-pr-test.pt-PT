---
title: "Do Azure serviços Web Machine Learning: Implementação e o consumo | Microsoft Docs"
description: "Recursos para implementar e utilizar os serviços web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Serviços Web do Azure Machine Learning: implementação e consumo
Pode utilizar o Azure Machine Learning a fluxos de trabalho de machine-learning do toodeploy e modelos como serviços web. Estes serviços web, em seguida, podem ser utilizados toocall Olá machine-learning modelos de aplicações por predições do Olá Internet toodo em tempo real ou no modo de batch. Dado que os serviços web Olá RESTful, pode chamá-los de vários idiomas e plataformas, tal como .NET e Java, programação e de aplicações, como o Excel.

secções Olá fornecem ligações toowalkthroughs, códigos e documentação toohelp começar.

## <a name="deploy-a-web-service"></a>Implementar serviços Web
### <a name="with-azure-machine-learning-studio"></a>Com o Azure Machine Learning Studio
Machine Learning Studio e o portal de serviços Web do Microsoft Azure Machine Learning Olá ajudam a implementar e gerir um serviço web sem escrever código.

Olá ligações seguintes fornecem informações gerais sobre como toodeploy um novo serviço web:

* Para obter uma descrição geral sobre como toodeploy um novo serviço web que é baseado no Azure Resource Manager, consulte o artigo [implementar um novo serviço web](machine-learning-webservice-deploy-a-web-service.md).
* Para obter instruções sobre como toodeploy um serviço web, consulte [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Para obter instruções completas sobre como toocreate e implementar um serviço web, consulte [instruções passo 1: criar uma área de trabalho do Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md).
* Para obter exemplos específicos que implementar um serviço web, consulte:

  * [Instruções passo 5: Implementar o serviço de web do Azure Machine Learning Olá](machine-learning-walkthrough-5-publish-web-service.md)
  * [Como toodeploy uma web service toomultiple regiões](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>Com o fornecedor de recursos de serviços web APIs (APIs do Azure Resource Manager)
fornecedor de recursos do Azure Machine Learning Olá para serviços web permite a implementação e gestão de serviços web através de chamadas da REST API. Para obter mais detalhes, consulte o [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) referência.

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>Com os cmdlets do PowerShell
Fornecedor de recursos do Azure Machine Learning para serviços web permite a implementação e gestão de serviços web utilizando cmdlets do PowerShell.

toouse Olá cmdlets, tem primeiro de iniciar sessão tooyour conta do Azure a partir do ambiente de PowerShell Olá utilizando Olá [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet. Se não estiver familiarizado com como toocall PowerShell comandos que são baseadas no Resource Manager, consulte [utilizar o Azure PowerShell com o Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport experimentar, utilize o preditiva [este código de exemplo](https://github.com/ritwik20/AzureML-WebServices). Depois de criar o ficheiro de .exe Olá a partir do código Olá, pode escrever:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Execução da aplicação Olá cria um modelo de JSON do serviço web. toouse Olá modelo toodeploy um serviço web, tem de adicionar Olá seguintes informações:

* Nome da conta de armazenamento e a chave

    Pode obter o nome de conta do storage Olá e a chave de qualquer um dos Olá [portal do Azure](https://portal.azure.com/) ou Olá [portal clássico do Azure](http://manage.windowsazure.com/).
* ID de plano de compromisso

    Pode obter o ID de plano Olá de Olá [serviços Web do Azure Machine Learning](https://services.azureml.net) portal, iniciando sessão e clicar em nome do plano.

Adicionar modelo JSON toohello como elementos subordinados do Olá *propriedades* nó na Olá mesmo nível como Olá *MachineLearningWorkspace* nós.

Eis um exemplo:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

Consulte Olá seguintes artigos e dar exemplos de código para obter detalhes adicionais:

* [Cmdlets do Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt767952.aspx) na MSDN
* Exemplo [instruções](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) no GitHub

## <a name="consume-hello-web-services"></a>Consumir os serviços web de Olá
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>De Olá Azure Machine Learning serviços IU da Web (teste)
Pode testar o seu serviço web do portal de serviços Web do Azure Machine Learning Olá. Isto inclui a testar o serviço de resposta-pedido Olá (RRS) e interfaces de serviço de execução de lote (BES).

* [Implementar um serviço Web novo](machine-learning-webservice-deploy-a-web-service.md)
* [Implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* [Instruções passo 5: Implementar o serviço de web do Azure Machine Learning Olá](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>A partir do Excel
Pode transferir um modelo do Excel que consome o serviço web de Olá:

* [Consumir um serviço web do Azure Machine Learning a partir do Excel](machine-learning-consuming-from-excel.md)
* [Suplemento do Excel para serviços Web do Azure Machine Learning](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>De um cliente baseado em REST
Serviços Web do Azure Machine Learning são RESTful APIs. Pode consumir estas APIs de várias plataformas, tais como .NET, Python, R, Java, Olá etc. **Consume** página para o seu serviço web no Olá [portal de serviços Web do Microsoft Azure Machine Learning](https://services.azureml.net) tem de exemplo Introdução ao código que pode ajudá-lo. Para obter mais informações, consulte [como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md).
