---
title: "aaaHow tooincrease simultaneidade de um serviço web Azure Machine Learning | Microsoft Docs"
description: "Saiba como tooincrease simultaneidade de um Azure Machine Learning serviço web adicionando os pontos finais adicionais."
services: machine-learning
documentationcenter: 
author: neerajkh
manager: srikants
editor: cgronlun
keywords: "do Azure machine learning, serviços web, operationalization, dimensionamento, ponto final, concorrência"
ms.assetid: c2c51d7f-fd2d-4f03-bc51-bf47e6969296
ms.service: machine-learning
ms.devlang: NA
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/23/2017
ms.author: neerajkh
ms.openlocfilehash: e2ad16ec766820a64f36c31232f6a33a79196af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-an-azure-machine-learning-web-service-by-adding-additional-endpoints"></a><span data-ttu-id="42d40-104">Dimensionar um serviço web Azure Machine Learning adicionando os pontos finais adicionais</span><span class="sxs-lookup"><span data-stu-id="42d40-104">Scaling an Azure Machine Learning web service by adding additional endpoints</span></span>
> [!NOTE]
> <span data-ttu-id="42d40-105">Este tópico descreve tooa aplicável técnicas **clássico** serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="42d40-105">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span> 
> 
> 

<span data-ttu-id="42d40-106">Por predefinição, cada serviço Web publicado é configurado toosupport 20 pedidos em simultâneo e pode ser tão elevado como 200 pedidos em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="42d40-106">By default, each published Web service is configured toosupport 20 concurrent requests and can be as high as 200 concurrent requests.</span></span> <span data-ttu-id="42d40-107">Enquanto Olá portal clássico do Azure fornece uma forma tooset este valor, do Azure Machine Learning automaticamente otimiza Olá definição tooprovide Olá melhor desempenho para o seu serviço web e valor portal Olá é ignorado.</span><span class="sxs-lookup"><span data-stu-id="42d40-107">While hello Azure classic portal provides a way tooset this value, Azure Machine Learning automatically optimizes hello setting tooprovide hello best performance for your web service and hello portal value is ignored.</span></span> 

<span data-ttu-id="42d40-108">Se planear toocall Olá API com uma carga maior do que um valor de número máximo de chamadas em simultâneo de 200 irá suportar, deve criar vários pontos finais no Olá mesmo serviço Web.</span><span class="sxs-lookup"><span data-stu-id="42d40-108">If you plan toocall hello API with a higher load than a Max Concurrent Calls value of 200 will support, you should create multiple endpoints on hello same Web service.</span></span> <span data-ttu-id="42d40-109">Em seguida, pode distribuir aleatoriamente a carga em todos eles.</span><span class="sxs-lookup"><span data-stu-id="42d40-109">You can then randomly distribute your load across all of them.</span></span>

<span data-ttu-id="42d40-110">Olá dimensionamento de um serviço Web é uma tarefa comuns.</span><span class="sxs-lookup"><span data-stu-id="42d40-110">hello scaling of a Web service is a common task.</span></span> <span data-ttu-id="42d40-111">Algumas razões tooscale são toosupport mais de 200 pedidos em simultâneo, aumentar a disponibilidade através de vários pontos finais ou forneça pontos finais separados para o serviço web de Olá.</span><span class="sxs-lookup"><span data-stu-id="42d40-111">Some reasons tooscale are toosupport more than 200 concurrent requests, increase availability through multiple endpoints, or provide separate endpoints for hello web service.</span></span> <span data-ttu-id="42d40-112">Pode aumentar a escala de Olá adicionando os pontos finais adicionais para Olá mesmo serviço Web através de [portal clássico do Azure](https://manage.windowsazure.com/) ou Olá [serviço Web do Azure Machine Learning](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="42d40-112">You can increase hello scale by adding additional endpoints for hello same Web service through [Azure classic portal](https://manage.windowsazure.com/) or hello [Azure Machine Learning Web Service](https://services.azureml.net/) portal.</span></span>

<span data-ttu-id="42d40-113">Para obter mais informações sobre como adicionar novos pontos finais, consulte [criação de pontos finais](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="42d40-113">For more information on adding new endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span>

<span data-ttu-id="42d40-114">Tenha em atenção que o com uma contagem de concorrência elevado pode ser detrimental se não estiver a chamar Olá API com uma taxa elevada de proporcionalmente.</span><span class="sxs-lookup"><span data-stu-id="42d40-114">Keep in mind that using a high concurrency count can be detrimental if you're not calling hello API with a correspondingly high rate.</span></span> <span data-ttu-id="42d40-115">Poderá ver esporádicas tempos limite e/ou picos de latência de Olá se colocar uma carga relativamente baixa numa API configurada para elevada carga.</span><span class="sxs-lookup"><span data-stu-id="42d40-115">You might see sporadic timeouts and/or spikes in hello latency if you put a relatively low load on an API configured for high load.</span></span>

<span data-ttu-id="42d40-116">Olá que APIs síncronas são normalmente utilizadas em situações em que uma baixa latência for pretendida.</span><span class="sxs-lookup"><span data-stu-id="42d40-116">hello synchronous APIs are typically used in situations where a low latency is desired.</span></span> <span data-ttu-id="42d40-117">Latência aqui implica tempo Olá Olá API toocomplete um pedido leva e não uma conta para qualquer atrasos de rede.</span><span class="sxs-lookup"><span data-stu-id="42d40-117">Latency here implies hello time it takes for hello API toocomplete one request, and doesn't account for any network delays.</span></span> <span data-ttu-id="42d40-118">Imaginemos que tem uma API com uma latência de 50-ms.</span><span class="sxs-lookup"><span data-stu-id="42d40-118">Let's say you have an API with a 50-ms latency.</span></span> <span data-ttu-id="42d40-119">toofully consumir capacidade disponível do Olá com um nível elevado de limitação e máx. de chamadas em simultâneo = 20, terá de toocall esta API 20 * 1000 / 50 = 400 vezes por segundo.</span><span class="sxs-lookup"><span data-stu-id="42d40-119">toofully consume hello available capacity with throttle level High and Max Concurrent Calls = 20, you need toocall this API 20 * 1000 / 50 = 400 times per second.</span></span> <span data-ttu-id="42d40-120">Expandir ainda mais este, um máximo de chamadas em simultâneo de 200 permite-lhe toocall Olá API 4000 vezes por segundo, partindo do princípio de uma latência de 50-ms.</span><span class="sxs-lookup"><span data-stu-id="42d40-120">Extending this further, a Max Concurrent Calls of 200 allows you toocall hello API 4000 times per second, assuming a 50-ms latency.</span></span>

<!--Image references-->
[1]: ./media/machine-learning-scaling-webservice/machlearn-1.png
[2]: ./media/machine-learning-scaling-webservice/machlearn-2.png
