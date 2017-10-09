---
title: "aaaUse parâmetros de serviço Web do Azure Machine Learning | Microsoft Docs"
description: "Como toouse parâmetros de serviço Web do Azure Machine Learning toomodify Olá comportamento do modelo ao serviço web de Olá é acedido."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Utilizar Parâmetros do Serviço Web do Azure Machine Learning
Um serviço web Azure Machine Learning é criado através da publicação de uma experimentação que contém módulos com parâmetros configuráveis. Em alguns casos, poderá ser útil comportamento de módulo de Olá toochange enquanto o serviço web de Olá está em execução. *Os parâmetros do serviço de Web* permitem-lhe toodo esta tarefa. 

Um exemplo comum é configurar Olá [importar dados] [ reader] módulo para esse utilizador Olá de Olá publicados serviço web pode especificar uma origem de dados diferente quando o serviço web de Olá é acedido. Ou a configuração de Olá [exportar dados] [ writer] módulo para que pode ser especificado um destino diferente. Outros exemplos incluem a alteração do número de Olá de bits para Olá [funcionalidade hash] [ feature-hashing] módulo ou Olá várias funcionalidades pretendidas para Olá [filtro com base na seleção de funcionalidades] [ filter-based-feature-selection] módulo. 

Pode definir os parâmetros do serviço Web e associá-las com um ou mais parâmetros do módulo na sua experimentação e pode especificar se estão necessária ou opcional. utilizador Olá do serviço web de Olá, em seguida, pode fornecer valores para estes parâmetros quando chamar o serviço web de Olá. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Como tooset e utilize parâmetros de serviço Web
Definir um parâmetro de serviço Web, clicando em Olá ícone seguinte toohello parâmetro um módulo e selecionando "Definir como parâmetro de serviço web". Esta ação cria um novo parâmetro do serviço Web e liga toothat parâmetro de módulo. Em seguida, quando está a aceder ao serviço de web de Olá, utilizador de Olá pode especificar um valor de parâmetro de serviço Web de Olá e é aplicado toohello módulo parâmetro.

Depois de definir um parâmetro de serviço Web, é tooany disponível outros parâmetros do módulo na experimentação de Olá. Se definir um parâmetro de serviço Web associada um parâmetro para um módulo, pode utilizar esse mesmo parâmetro de serviço Web para qualquer outro módulo, desde que o parâmetro de Olá espera Olá mesmo tipo de valor. Por exemplo, se Olá parâmetro de serviço Web é um valor numérico, em seguida, pode apenas ser utilizado para os parâmetros do módulo que esperam um valor numérico. Quando o utilizador Olá define um valor de parâmetro de serviço Web de Olá, serão aplicados tooall associado módulo parâmetros.

Pode decidir se tooprovide uma predefinição de valor para Olá parâmetro de serviço Web. Se, em seguida, Olá parâmetro é opcional para o utilizador Olá do serviço web de Olá. Se não fornecer um valor predefinido, em seguida, Olá o utilizador está tooenter necessário um valor quando o serviço web de Olá é acedido.

Olá documentação da API para o serviço web de Olá inclui informações de utilizador de serviço web de Olá em como toospecify Olá parâmetro de serviço Web através de programação ao aceder ao serviço web de Olá.

> [!NOTE]
> Olá documentação da API para um serviço web clássico é fornecido através de Olá **página de ajuda de API** ligação no serviço web de Olá **DASHBOARD** no Machine Learning Studio. Olá documentação da API para um novo serviço web é fornecido através de Olá [serviços Web do Azure Machine Learning](https://services.azureml.net/Quickstart) portal no Olá **Consume** e **API do Swagger** páginas para o serviço Web.
> 
> 

## <a name="example"></a>Exemplo
Por exemplo, vamos supor que temos uma experimentação com um [exportar dados] [ writer] módulo envia o armazenamento de BLOBs de tooAzure de informações. Iremos definir um parâmetro de serviço Web com o nome "Caminho do Blob" que permite Olá web service utilizador toochange Olá caminho toohello armazenamento de BLOBs, quando o serviço de Olá é acedido.

1. No Machine Learning Studio, clique em Olá [exportar dados] [ writer] módulo tooselect-lo. Olá propriedades painel toohello à direita da tela de experimentação Olá são apresentadas as respetivas propriedades.
2. Especifique o tipo de armazenamento Olá:
   
   * Em **especifique o destino de dados**, selecione "Blob Storage do Azure".
   * Em **especifique o tipo de autenticação**, selecione "Conta".
   * Introduza as informações de conta de Olá para Olá blob storage do Azure. 
     <p />
3.Clique em Olá ícone toohello à direita dos Olá **caminho tooblob que começa com o parâmetro de contentor**. Este aspeto:
   
   ![Ícone de parâmetro de serviço Web][icon]
   
   Selecione "Definir como parâmetro de serviço web".
   
   Uma entrada é adicionada em **parâmetros de serviço Web** em Olá parte inferior do painel de propriedades de Olá com Olá nome "caminho tooblob que começa com o contentor". Este é Olá parâmetro de serviço Web que está agora associada a este [exportar dados] [ writer] parâmetro do módulo.
4. toorename Olá parâmetro de serviço Web, clique no nome de Olá, introduza "Caminho do Blob" e prima Olá **Enter** chave. 
5. tooprovide um valor predefinido para Olá parâmetro do serviço Web, clique em Olá ícone toohello à direita do nome de Olá, selecione "Fornecer o valor predefinido", introduza um valor (por exemplo, "container1/output1.csv") e prima Olá **Enter** chave.
   
   ![Parâmetro de serviço Web][parameter]
6. Clique em **Executar**. 
7. Clique em **implementar serviço Web** e selecione **implementar o serviço Web [clássico]** ou **implementar o serviço Web do [New]** serviço web do toodeploy Olá.

> [!NOTE] 
> um novo serviço web tem de ter permissões suficientes no Olá subscrição toowhich que implementar o serviço web de Olá toodeploy. Para obter mais informações, consulte [gerir um serviço Web utilizando o portal de serviços Web do Azure Machine Learning Olá](machine-learning-manage-new-webservice.md). 

utilizador Olá do serviço web de Olá agora pode especificar um novo destino para Olá [exportar dados] [ writer] módulo ao aceder ao serviço web de Olá.

## <a name="more-information"></a>Mais informações
Para obter um exemplo mais detalhado, consulte Olá [parâmetros de serviço Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entrada no Olá [blogue do Machine Learning](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Para obter mais informações sobre aceder a um serviço web do Machine Learning, consulte [como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

