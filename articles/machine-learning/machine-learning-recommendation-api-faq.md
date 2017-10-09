---
title: "aaaSet cópias de segurança e a utilização Olá recomendações API do Machine Learning | Microsoft Docs"
description: "Microsoft recomendações de API criada com o Azure Machine Learning FAQ"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 1ffc3c16-e040-4225-9d72-105129938dfa
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 980bf1a36f3291275d9ef0fee9b4446f7e0cbecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-and-using-machine-learning-recommendations-api-faq"></a>FAQ sobre a configuração e utilização da API de Recomendações do Machine Learning
**O que é recomendações?**

> [!NOTE]
> Deve começar a utilizar Olá recomendações API cognitivos serviço em vez de nesta versão. Olá serviço cognitivos recomendações irá substituir este serviço e todas as novas funcionalidades de Olá irão ser desenvolvidas não existe. Tem novas capacidades, como a criação de batches de suporte, melhor Explorador de API, uma experiência de inscrição/faturação superfície, mais consistente de API limpeza, etc.
> Saiba mais sobre [migrar toohello novo serviço cognitivos](http://aka.ms/recomigrate)
> 
> 

Para as organizações e empresas que se baseiam em recomendações toocross-vende e vende dos produtos e os serviços tootheir clientes, as recomendações no Azure Machine Learning fornece um motor de recomendações self-service. É uma implementação de filtragem de colaboração que utiliza factorization matriz como o algoritmo de núcleos. Os programadores de aplicações podem aceder recomendações utilizando REST APIs. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

**O que posso fazer com base em recomendações?**

RECOMENDAÇÕES aceita como entrada de um item ou um conjunto de itens e devolve uma lista de recomendações relevantes. Por exemplo: um cliente de um revendedor online clica um produto. revendedor online Olá envia o produto como entrada tooRECOMMENDATIONS, obtém uma lista dos produtos em return e decide que estes produtos serão apresentados toohello cliente. Pode pretender toouse recomendações toooptimize sua loja online ou mesmo tooinform seu interior center departamento ou chamada de venda.

**Existem algumas limitações de utilização?**

Recomendações tem Olá seguintes limitações de utilização:

* Número máximo de modelos por subscrição: 10
* Número máximo de itens que pode conter um catálogo: 100 000
* número máximo de Olá de pontos de utilização que são mantidos é ~ 5,000,000. Olá mais antigo será eliminado se novos serão carregados ou comunicados.
* Tamanho máximo de dados que podem ser enviados por correio eletrónico (por exemplo, importar dados do catálogo, importar dados de utilização) é 200 MB
* Número de transações por segundo (TPS) para uma compilação de modelo de recomendações que não está ativa é TPS ~ 2. Uma compilação de modelo de recomendações que Active Directory pode manter cópias de segurança too20 TPS.

## <a name="purchase-and-billing"></a>Compra e Faturação
**Quanto custo recomendações durante o período de início de Olá?**

Recomendações é um serviço baseado na subscrição. Charging baseia-se no volume de transações por mês. Pode verificar Olá [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) no Microsoft Azure Marketplace para obter informações sobre preços.

**Existem quaisquer custos associados com recomendações a ter controlam e armazenam a atividade do utilizador para mim?**

Não momento Olá.

**A recomendações tem uma versão de avaliação gratuita?**

Não há um registo livre que é restrita too10, 000 transações por mês.

**Quando será posso faturado por recomendações?**

Uma subscrição paga é nenhuma subscrição para o qual é uma taxa mensal. Ao adquirir uma subscrição paga, são-lhe imediatamente cobrados para Olá primeiro utilizar do mês. São-lhe cobrados quantidade Olá que está associada a oferta de Olá na página de subscrição de Olá (além de taxas aplicáveis). Este encargos mensais é efetuado cada mês no Olá mesmo calendário data como compra original até cancelar Olá subscrição. 

**Como atualizar o serviço de camada superior tooa?**

Pode comprar ou atualizar a sua subscrição do Olá [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations) página no Microsoft Azure Marketplace.

Quando atualiza uma subscrição:

* Transações que são restantes na sua subscrição antiga não foram adicionadas tooyour nova subscrição. 
* Paga completo preços nova subscrição de Olá, apesar de a ter transações não utilizadas na sua subscrição antiga.

Uma subscrição do processo tooupgrade:

* Nevigate toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).
* Inicie sessão no toohello Marketplace se já não são iniciou sessão.
* No painel direito Olá, são listados todos os planos disponíveis de Olá. Clique no botão de opção Olá para o plano de Olá que pretende tooupgrade para.
* Se quiser tooupgrade, clique em **OK**. Se não pretender tooupgrade, clique em **Cancelar**.

**Importante** caixa de diálogo Olá leia cuidadosamente antes de atualizar porque existem implicações de faturação e de utilização.

**Quando terminará tooRecommendations a minha subscrição?**

A subscrição terminará quando cancelá-lo. Se quiser toocancel as suas subscrições, consulte Olá seguir instruções.

**Como cancelar a minha subscrição recomendações?**

toocancel a sua subscrição, Olá utilize os seguintes passos. Se a sua subscrição atual é uma subscrição paga, a subscrição continua em vigor até fim Olá Olá atual de período de faturação. Se precisar de hello cancelamento toobe em vigor imediatamente, contacte-nos [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

**Tenha em atenção** não reembolso é dado se cancelar antes do final de Olá de um período de faturação ou de transações não utilizadas num período de faturação.

* Navegue toohello [oferecem página](https://datamarket.azure.com/dataset/amla/recommendations).
* Inicie sessão no toohello Marketplace se já não são iniciou sessão.
* Clique em **Cancelar** toohello direita do nome do conjunto de dados de Olá e o estado. Pode utilizar esta subscrição até Olá de Olá atual período ou o limite de transação de faturação é foi atingido um fim (que ocorrer primeiro).

Se quiser toocancel a sua subscrição imediatamente, por isso, pode comprar uma nova subscrição, um ticket ao [Microsoft Support](https://support.microsoft.com/oas/default.aspx?gprid=17024&st=1&wfxredirect=1&sd=gn).

## <a name="getting-started-with-recommendations"></a>Introdução ao recomendações
**É recomendações para mim?** 

Recomendações no Machine Learning é para as organizações e empresas que se baseiam em recomendações toocross vende e cópia de segurança vende produtos ou serviços tootheir clientes. Se tiver um Web site orientado para o cliente, uma força de venda, um interior vendedores ou de um centro de atendimento telefónico, e se oferecer um catálogo de mais do que alguns dozen produtos ou serviços, a linha na parte inferior pode beneficiar da utilização recomendações. 

Conseguirmos uma com base em recomendações é concebida toobe bastante simples. versão de API com base em atual Olá requer competências de programação básicas. Se necessitar de assistência, contacte o fornecedor de Olá que desenvolveu o seu Web site. Se tiver um departamento de TI interno ou um programador interna, devem ser capaz de tooget recomendações toowork por si. 

**Quais são Olá pré-requisitos para configurar as recomendações?**

Recomendações requer que tem um registo das opções de utilizador no que respeita tooyour catálogo. Se não tiver um registo de tal e tiver um Web site com acesso de cliente, recomendações podem recolher a atividade do utilizador para si. 

Recomendações também requer um catálogo dos seus produtos ou serviços. Se não tiver catálogo Olá, recomendações podem utilizar dados de utilização do cliente real Olá e distill um catálogo. Um catálogo implícito não irá incluir itens que não foram reportados como parte de transações de utilizador.

**Como posso configurar recomendações para Olá pela primeira vez?**

Depois de [subscrição](https://datamarket.azure.com/dataset/amla/recommendations) tooRecommendations, deve utilizar documentação Olá API no Olá [recomendações no Azure Machine Learning - Guia Rápido](machine-learning-recommendation-api-quick-start-guide.md) tooset serviço Olá.

**Onde posso encontrar a documentação da API?** 

Olá documentação da API é [Azure Machine Learning recomendações-Guia Rápido](machine-learning-recommendation-api-quick-start-guide.md).

**O que fazem opções tenho tooRecommendations de dados de utilização e de catálogo tooupload?**

Tem duas opções para carregar os dados de utilização e de catálogo: pode exportar os dados de Olá do seu sistema CRM ou outros registos e carregá-la tooRecommendations ou pode adicionar Web site do tooyour etiquetas que irá monitorizar atividades de utilizador. Se utilizar o método última Olá, Olá dados serão armazenados no Azure.

## <a name="maintenance-and-support"></a>Suporte e manutenção
**Grande como podem os meus conjunto de dados ser?**

Cada conjunto de dados pode conter segurança too100, 000 itens de catálogo e cópia de segurança too2048 MB de dados de utilização.
Além disso, pode conter uma subscrição de cópia de segurança too10 conjuntos de dados (modelos).

**Onde posso obter suporte técnico para obter recomendações de?**

O suporte técnico está disponível no Olá [suporte do Microsoft Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=MachineLearning) site.

**Onde posso encontrar termos Olá de utilização?**

[Microsoft Azure Machine Learning recomendações API termos de serviço](https://datamarket.azure.com/dataset/amla/recommendations#terms).

