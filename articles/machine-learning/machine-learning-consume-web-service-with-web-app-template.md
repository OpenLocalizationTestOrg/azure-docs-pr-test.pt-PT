---
title: "aaaConsume um serviço web do Machine Learning com um modelo de aplicação web | Microsoft Docs"
description: "Utilize um modelo de aplicação web no Azure Marketplace tooconsume um serviço web preditiva no Azure Machine Learning."
keywords: "serviço Web, operationalization, REST API, machine learning"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Consumir um serviço Web do Azure Machine Learning com um modelo de aplicação Web

Uma vez que já desenvolveu o seu modelo preditivo e implementado como um serviço web do Azure utilizando o Machine Learning Studio, ou utilizando ferramentas como R ou Python, pode aceder ao modelo operacionalizado Olá utilizando uma API REST.

Existem várias formas tooconsume Olá REST API e acesso Olá serviço web. Por exemplo, pode escrever uma aplicação em c#, R, ou código gerado quando implementou o serviço web de Olá de exemplo do Python com Olá (disponível no Olá [Portal de serviços Web do Machine Learning](https://services.azureml.net/quickstart) ou no dashboard de serviço web Olá no O Machine Learning Studio). Ou pode utilizar o livro do Microsoft Excel exemplo Olá criado por si em Olá mesmo tempo.

Mas Olá tooaccess de forma mais rápida e mais fácil é o serviço web através de modelos de aplicação de Web de Olá disponíveis no Olá [Azure Marketplace de aplicação Web](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Olá modelos de aplicação Web do Azure Machine Learning
modelos de aplicação de web de Olá disponíveis no Azure Marketplace de Olá podem criar uma aplicação web personalizada que sabe o seu serviço web dados de entrada e resultados esperados. Tudo o que precisa toodo é a fornecer serviço web de tooyour acesso Olá web app e os dados e modelo Olá Olá rest.

Estão disponíveis dois modelos:

* [Modelo de aplicação do Azure ML resposta-pedido serviço Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [Modelo de aplicação de Web de serviço de execução de lote do Azure ML](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Cada modelo cria uma aplicação de ASP.NET de exemplo, através de Olá URI de API e a chave para o seu serviço web e implementa-o como um tooAzure de web site. modelo de serviço de resposta-pedido (RRS) Olá cria uma aplicação web que permite-lhe toosend uma única linha de dados toohello web service tooget um resultado único. modelo de serviço de execução de lote (BES) Olá cria uma aplicação web que permite-lhe toosend número de linhas de dados tooget vários resultados.

Sem codificação é necessária toouse estes modelos. Forneça apenas o Olá chave de API e o URI e modelo Olá baseia-se a aplicação Olá por si.

chave de API de Olá tooget e URI de pedido para um serviço web:

1. No Olá [Portal de serviços Web](https://services.azureml.net/quickstart), para um novo serviço web, clique em **serviços Web** na parte superior do Olá. Ou de um clique de serviço web clássico **serviços Web clássicos**.
2. Clique em Olá web serviço tooaccess.
3. Para um serviço web clássico, clique em ponto final de Olá pretende tooaccess.
4. Clique em **Consume** na parte superior do Olá.
5. Olá cópia **primário** ou **chave secundária** e guardá-lo.
6. Se estiver a criar um modelo de serviço de resposta-pedido (RRS), copiar Olá **pedido-resposta** URI e guardá-lo. Se estiver a criar um modelo de serviço de execução de lote (BES), copiar Olá **pedidos de Batch** URI e guardá-lo.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Como toouse Olá modelo de serviço de resposta-pedido (RRS)
Siga estes passos toouse Olá RRS web modelo de aplicação, conforme mostrado no Olá diagrama a seguir.

![Modelo do processo toouse RRS web][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Aceda toohello [portal do Azure](https://portal.azure.com), **início de sessão**, clique em **novo**, procure e selecione **do Azure ML resposta-pedido Web do App Service**, em seguida, clique em **Criar**. 
   
   * Dê um nome exclusivo da aplicação web. URL de Olá da aplicação web de Olá será este nome seguido `.azurewebsites.net.` por exemplo,`http://carprediction.azurewebsites.net.`
   * Selecione Olá subscrição do Azure e serviços em que o seu serviço web está em execução.
   * Clique em **Criar**.
     
     ![Criar aplicação Web][image5]

4. Quando o Azure foi concluída a implementação de aplicação web de Olá, clique em Olá **URL** no Olá página de definições de aplicação web no Azure, ou introduza o URL de Olá num web browser. Por exemplo, `http://carprediction.azurewebsites.net.`
5. Quando Olá execuções de primeiro de aplicação de web que irá pedir-lhe Olá **API Post URL** e **chave de API**.
   Introduza os valores de Olá guardou anteriormente (**URI pedido** e **chave de API**, respetivamente).
     
     Clique em **submeter**.
     
     ![Introduza o Post URI e chave de API][image6]

6. Olá apresenta de aplicação web respetivo **configuração de aplicação Web** página com definições de serviço web de Olá atuais. Aqui pode efetuar alterações definições toohello utilizadas pela aplicação de web de Olá.
   
   > [!NOTE]
   > Alterar as definições de Olá aqui apenas altera-los para esta aplicação web. Não altera as definições predefinidas da Olá do seu serviço web. Por exemplo, se alterar Olá **Descrição** aqui não altera descrição Olá apresentada no dashboard de serviço web Olá no Machine Learning Studio.
   > 
   > 
   
    Quando tiver terminado, clique em **guardar alterações**e, em seguida, clique em **aceda tooHome página**.

7. Página inicial, que pode introduzir valores de serviço web do toosend tooyour de Olá. Clique em **submeter** quando tiver terminado e Olá resultado será devolvido.

Se quiser tooreturn toohello **configuração** página, visite toohello `setting.aspx` página da aplicação web de Olá. Por exemplo: `http://carprediction.azurewebsites.net/setting.aspx.` será chave de API de Olá tooenter pedido novamente - é necessário que tooaccess Olá página e atualizar as definições de Olá.

Pode parar, reiniciar ou eliminar a aplicação web de Olá no Olá portal do Azure como qualquer outra aplicação web. Enquanto estiver em execução pode procurar o endereço da web raiz toohello e introduza novos valores.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Como toouse Olá modelo de serviço de execução de lote (BES)
Pode utilizar Olá BES modelo de aplicação web no Olá mesma forma como o modelo de RRS Olá, exceto essa aplicação web Olá criado permitirá toosubmit várias linhas de dados e de receber vários resultados.

os valores de entrada Olá para um serviço de web de execução do batch podem provenientes de armazenamento do Azure ou um ficheiro local; resultados de Olá são armazenados no contentor de armazenamento do Azure.
Por isso, irá precisa de um toohold do contentor de armazenamento do Azure Olá resultados devolvidos pela aplicação de web de Olá, e terá tooget os dados de entrada pronto.

![Processar toouse BES modelo web][image2]

1. Siga Olá mesmo Olá toocreate do procedimento BES web app para o modelo RRS Olá, exceto aceda demasiado[modelo de aplicação ao Web do serviço de execução do Azure ML Batch](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen Olá modelo BES no Azure Marketplace e clique em **Criar aplicação da Web** .

2. toospecify onde pretende que os resultados de Olá armazenados, introduza as informações do contentor de destino Olá na home page do Olá web app. Também pode especificar onde a aplicação web de Olá pode obter Olá os valores de entrada, a um ficheiro local ou um contentor de armazenamento do Azure.
   Clique em **submeter**.
   
    ![Informações de armazenamento][image7]

aplicação web de Olá apresentará uma página com o estado da tarefa.
Quando concluir a tarefa de Olá irá ser indicado localização Olá dos resultados de Olá no armazenamento de Blobs do Azure. Tem também a opção de Olá de transferência de ficheiros locais do Olá resultados tooa.

## <a name="for-more-information"></a>Para obter mais informações
toolearn mais informações sobre...

* criar uma experimentação de aprendizagem com Machine Learning Studio, consulte [criar a sua primeira experimentação no Azure Machine Learning Studio](machine-learning-create-experiment.md)
* como ver toodeploy sua aprendizagem experimentação como um serviço web, [implementar um serviço web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md)
* outras formas tooaccess seu serviço web, consulte [como tooconsume um serviço Web do Azure Machine Learning](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
