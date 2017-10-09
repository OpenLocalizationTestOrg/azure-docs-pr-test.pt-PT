---
title: "aaaConnect tooa serviço Web do Machine Learning | Microsoft Docs"
description: "Com c# ou Python, ligar tooan serviço Web do Azure Machine Learning utilizando uma chave de autorização."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Ligar tooan serviço Web do Azure Machine Learning
Olá experiência de programação do Azure Machine Learning é um predições do Web service API toomake de dados de entrada em tempo real ou no modo de batch. Utilizar predições toocreate do Azure Machine Learning Studio e implementar um serviço Web do Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

toolearn sobre como toocreate e implementar um serviço Web do Machine Learning com Machine Learning Studio:

* Para um tutorial sobre como toocreate uma experimentação no Machine Learning Studio, consulte o artigo [criar a sua primeira experimentação](machine-learning-create-experiment.md).
* Para obter detalhes sobre como toodeploy um serviço Web, consulte [implementar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Para obter mais informações sobre o Machine Learning em geral, visite Olá [Centro de documentação do Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

## <a name="azure-machine-learning-web-service"></a>Serviço Web do Machine Learning do Azure
Com o serviço Web do Azure Machine Learning Olá, uma aplicação externa comunica com um modelo de pontuação de fluxo de trabalho de Machine Learning em tempo real. Uma chamada de serviço Web do Machine Learning devolve resultados de predição aplicação externa tooan. toomake uma chamada de serviço Web do Machine Learning, passa uma chave de API que foi criada quando implementou uma predição. Olá serviço Web do Machine Learning é baseado em REST, uma opção de arquitetura popular para projetos de programação web.

O Azure Machine Learning tem dois tipos de serviços:

* O serviço de resposta-pedido (RRS) – A latência baixa, o serviço altamente dimensionável, que fornece uma interface toohello modelos sem monitorização de estado criados e implementados a partir de Olá Machine Learning Studio.
* Execução serviço batch (BES) – um assíncrono que pontua um lote de registos de dados do serviço.

Para obter mais informações sobre os serviços Web do Machine Learning, consulte [implementar um serviço Web do Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Obter uma chave de autorização do Azure Machine Learning
Ao implementar a sua experimentação, chaves de API são geradas para Olá serviço Web. Pode obter chaves Olá de várias localizações.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>No portal de serviços Web do Microsoft Azure Machine Learning Olá
Inicie sessão no toohello [serviços Web do Microsoft Azure Machine Learning](https://services.azureml.net) portal.

chave de Olá API tooretrieve para um serviço Web de aprendizagem máquina novo:

1. No portal de serviços Web do Azure Machine Learning Olá, clique em **serviços Web** menu superior Olá.
2. Clique em serviço Web de Olá para o qual pretende chave de Olá tooretrieve.
3. No menu superior Olá, clique em **Consume**.
4. Copie e guarde Olá **chave primária**.

chave de API de Olá tooretrieve para um serviço Web de aprendizagem máquina clássico:

1. No portal de serviços Web do Azure Machine Learning Olá, clique em **serviços Web clássicos** menu superior Olá.
2. Clique em serviço Web de Olá com a qual está a trabalhar.
3. Clique em ponto final de Olá para o qual pretende chave de Olá tooretrieve.
4. No menu superior Olá, clique em **Consume**.
5. Copie e guarde Olá **chave primária**.

### <a name="classic-web-service"></a>Serviço Web clássico
 Também pode obter uma chave para um serviço Web clássico de Machine Learning Studio ou Olá portal clássico do Azure.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. No Machine Learning Studio, clique em **serviços WEB** Olá esquerda.
2. Clique num serviço Web. Olá **chave de API** no Olá **DASHBOARD** separador.

#### <a name="azure-classic-portal"></a>Portal Clássico do Azure
1. Clique em **MACHINE LEARNING** Olá esquerda.
2. Clique em área de trabalho Olá em que se encontra o seu serviço Web.
3. Clique em **serviços WEB**.
4. Clique num serviço Web.
5. Clique num ponto final. Olá "Chave de API" está inativo em Olá inferior direita.

## <a id="connect"></a>Ligar o serviço de Machine Learning Web tooa
Pode ligar tooa serviço Web do Machine Learning utilizando qualquer linguagem de programação que suporte o HTTP de pedido e resposta. Pode ver exemplos em c#, Python e R de uma página de ajuda do serviço Web do Machine Learning.

**Ajuda da API de aprendizagem do computador** ajuda de API do Machine Learning é criada quando implementar um serviço Web. Consulte [instruções de aprendizagem do Azure - implementar o serviço Web](machine-learning-walkthrough-5-publish-web-service.md).
Olá ajuda de API do Machine Learning contém detalhes sobre uma predição do serviço Web.

1. Clique em serviço Web de Olá com a qual está a trabalhar.
2. Clique em ponto final de Olá para o qual pretende tooview Olá página de ajuda de API.
3. No menu superior Olá, clique em **Consume**.
4. Clique em **página de ajuda de API** em Olá pedido-resposta ou pontos finais de execução de lote.

**ajudar a API do Machine Learning tooview para um serviço Web de novo**

No Portal de serviços Web do Azure Machine Learning Olá:

1. Clique em **serviços WEB** no menu superior Olá.
2. Clique em serviço Web de Olá para o qual pretende chave de Olá tooretrieve.

Clique em **Consume** tooget hello URIs para Olá Reposonse pedido e o código de exemplo e serviços de execução do Batch em c#, R e Python.

Clique em **API do Swagger** tooget Swagger baseada em documentação para Olá APIs chamada a partir de Olá fornecido URIs.

### <a name="c-sample"></a>Exemplo do c#
tooconnect tooa serviço Web do Machine Learning, utilize um **HttpClient** transmitir ScoreData. ScoreData contém um FeatureVector, um vetor n dimensional das funcionalidades numéricos que representa Olá ScoreData. Autenticar o serviço de Machine Learning toohello com uma chave de API.

Olá tooconnect tooa serviço Web do Machine Learning, **Microsoft.AspNet.WebApi.Client** pacote NuGet tem de estar instalado.

**Instalar Microsoft.AspNet.WebApi.Client NuGet no Visual Studio**

1. Publicar o conjunto de dados de transferência de Olá de UCI: conjunto de dados de classe para adultos 2 serviço Web.
2. clique em **Ferramentas** > **Gestor de Pacotes NuGet** > **Consola de Gestor de Pacotes**.
3. Escolha **Install-Package Microsoft.AspNet.WebApi.Client**.

**exemplo de código toorun Olá**

1. Publicar "exemplo 1: Transferir o conjunto de dados a partir de UCI: o conjunto de dados do adulto 2 classe" experimentação, parte Olá coleção de exemplo do Machine Learning.
2. Atribua apiKey com a chave de Olá um serviço Web. Consulte **obter uma chave de autorização do Azure Machine Learning** acima.
3. Atribua serviceUri com Olá URI do pedido.

### <a name="python-sample"></a>Exemplo de Python
tooconnect tooa serviço Web do Machine Learning, utilize Olá **urllib2** biblioteca transmitir ScoreData. ScoreData contém um FeatureVector, um vetor n dimensional das funcionalidades numéricos que representa Olá ScoreData. Autenticar o serviço de Machine Learning toohello com uma chave de API.

**exemplo de código toorun Olá**

1. Implementar "exemplo 1: Transferir o conjunto de dados a partir de UCI: o conjunto de dados do adulto 2 classe" experimentação, parte Olá coleção de exemplo do Machine Learning.
2. Atribua apiKey com a chave de Olá um serviço Web. Consulte Olá **obter uma chave de autorização do Azure Machine Learning** secção quase início Olá deste artigo.
3. Atribua serviceUri com Olá URI do pedido.

