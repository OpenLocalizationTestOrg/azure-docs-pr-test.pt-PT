---
title: "AAA(deprecated) FAQ – publicar e utilizar aplicações de Machine Learning no Azure Marketplace | Microsoft Docs"
description: "(preterido) Perguntas mais frequentes sobre a publicação de Machine Learning aplicações no Olá Azure Marketplace"
services: machine-learning
documentationcenter: 
author: bharaths
manager: jhubbard
editor: cgronlun
ms.assetid: 26b3a1e7-8b9a-4004-98bc-17456d4c25e8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: b3ae45dfff211fe9baccaf54faaf360a8309c780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publishing-and-using-machine-learning-apps-in-hello-azure-marketplace-faq"></a>(preterido) Publicação e utilização de aplicações de Machine Learning no Azure Marketplace de Olá: FAQ

> [!NOTE]
> Serviços de dados e DataMarket são vai ser reformados e subscrições existentes serão descontinuadas e cancelada iniciar 3/31/2017. Como resultado, está a ser preterido neste artigo. 
> 
> Como alternativa, pode publicar o toohello de experimentações de Machine Learning [galeria da Cortana Intelligence](https://gallery.cortanaintelligence.com/) para benefício Olá da Comunidade de ciência de dados de Olá. Para obter mais informações, consulte [partilha e detetar recursos na Olá galeria da Cortana Intelligence](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).


## <a name="questions-about-consuming-from-marketplace"></a>Perguntas sobre o consumo do Marketplace
**1. Por que motivo recebo Olá seguir a mensagem de erro depois de introduzo entrada para o serviço web de Olá:**

**pedido de Olá resultou num erro de back-end ou back-end tempo limite. equipa de Olá é investigar o problema de Olá. Estamos Pedimos desculpa pelo incómodo do Olá. (500)**

O parâmetro de entrada (s) poderá não estar em conformidade com toohello formato necessário para o serviço web específico de Olá. Consulte toohello correspondente documentação ligação toofind Olá formato correto para os parâmetros de entrada e limitações de Olá deste serviço web.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**2. Se copiar o ligação Olá API de Olá do serviço web que vejo no Olá "Explorar este conjunto de dados" página e cole-outra janela do browser, que credenciais deve posso utilizar resultados de Olá tooaccess e como posso vê-las?**

Deve utilizar a sua conta do Marketplace como Olá nome de utilizador e a chave de conta primária Olá como palavra-passe de Olá. chave de conta primária Olá pode ser encontrado no Olá **explorar este conjunto de dados** página de descrição de Olá do serviço web de Olá (clique Olá **mostrar** botão). resultado de Olá pode ser apresentado num browser de Olá ou poderá ser disponível demasiado transferência, consoante o browser estiver a utilizar.

**3. Por que motivo recebo Olá seguir a mensagem de erro depois de introduzo entrada Olá para o serviço web de Olá na página de "Explorar este conjunto de dados" Olá:** 

**Ocorreu um erro inesperado ao processar o pedido. Tente novamente.**

Um ou mais parâmetros de entrada do seu serviço web podem excedeu o limite de comprimento de Olá quando consumir o serviço web de Olá no marketplace Olá **explorar este conjunto de dados** página. Serviços de Olá podem ser chamados com um comprimento de entrada já utilizando métodos de HTTP POST. Para obter exemplos, consulte [soluções que utilizam o R no Machine Learning e publicada tooMarketplace de exemplo](machine-learning-r-csharp-web-service-examples.md).

**4. Por que motivo não vejo qualquer coisa na int Olá arquivo do "EXPLORADOR de API" separador Olá no Olá Portal clássico do Azure?** 

Este é um problema conhecido com Olá Marketplace Portal clássico do Azure. equipa de Olá está a funcionar tooresolve este problema. 

## <a name="questions-about-publishing-from-azure-machine-learning-on-marketplace"></a>Perguntas sobre a publicação do Azure Machine Learning no Marketplace
**1. Por que motivo o meu transações dos logótipos ou nas imagens não são atualizados para o meu serviço web?** 

Logótipos e imagens são colocadas em cache no portal de publicação Olá e pode demorar dias too10 para logótipo novo Olá ou tooupdate de imagem no portal de Olá.

**2. Por que motivo é o separador de "Detalhes" Olá do meu serviço web no Marketplace, que mostra uma mensagem de erro?**

Não há um problema conhecido do Marketplace ao ligar tooAzure Machine Learning para os detalhes do serviço. equipa de Olá está a funcionar tooresolve este problema.

**3. Por que motivo não Olá código de exemplo de R nos serviços de web do Azure Machine Learning Olá funciona para serviços da web Olá consumo Marketplace?**

sistemas de autenticação de Olá são diferentes quando ligar serviços de web do Machine Learning tooAzure diretamente comparado com serviços web de toothese de tooconnecting através de Olá Marketplace. Serviços de Olá no mercado são serviços OData e pode ser chamados com métodos GET ou POST. 

**4. Por que motivo se as ligações de suporte de Olá do meu serviço web oferece não atualizar corretamente para algumas das minhas ofertas?**

ligações de suporte de Olá são globais por publicador, não por oferta. 

**5. Como se publicar um serviço web com o modo de entrada do batch no Marketplace?**

modo de entrada de batch de Olá não é atualmente suportado em serviços web do Marketplace.

**6. Quem deve posso contacte tooget ajuda se tiver perguntas sobre se tornar um publicador de dados, ou se tiver problemas durante a publicação?**

Contacte a equipa do Azure Marketplace Olá, < mailto:datamarketbd@microsoft.com > para obter mais informações.

