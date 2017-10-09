---
title: "aaaConsume um serviço Web do Machine Learning a partir do Excel | Microsoft Docs"
description: "Consumir um serviço Web do Azure Machine Learning a partir do Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Consumir um serviço Web do Azure Machine Learning a partir do Excel
 Azure Machine Learning Studio facilita toocall fácil os serviços web diretamente a partir do Excel sem precisar de Olá toowrite qualquer código.

Se estiver a utilizar o Excel 2013 (ou posterior) ou o Excel Online, em seguida, recomendamos que utilize Olá Excel [suplemento do Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Passos
Publica um serviço web. [Esta página](machine-learning-walkthrough-5-publish-web-service.md) explica como toodo-lo. A funcionalidade de livro do Excel Olá só é suportada para os serviços de pedido/resposta com uma saída único (ou seja, uma classificação simples). 

Depois de ter um serviço web, clique em Olá **serviços WEB** secção esquerda Olá do studio Olá e, em seguida, selecione Olá web service tooconsume a partir do Excel.

**Serviço Web clássico**

1. No Olá **DASHBOARD** separador para o serviço web de Olá é uma linha para Olá **pedido/resposta** serviço. Se este serviço tinha de saída única, deverá ver Olá **Transferir livro do Excel** ligação nessa linha.
   
    ![][1]
2. Clique em **transferir o livro do Excel**.

**Novo serviço Web**

1. No portal do serviço Web do Azure Machine Learning Olá, selecione **Consume**.
2. Na página de Consume Olá, no Olá **Web opções de consumo do serviço** secção, clique em ícone do Excel Olá.

**Utilizar Olá livro**

1. Livro Olá aberta.
2. É apresentado um aviso de segurança; Clique em Olá **ativar editar** botão.
   
    ![][2]
3. É apresentado um aviso de segurança. Clique em Olá **ativar conteúdo** botão toorun macros no seu folha de cálculo.
   
    ![][3]
4. Depois de macros estiverem ativadas, é gerada uma tabela. As colunas na azul são necessárias como entrada para Olá serviço web RRS, ou **parâmetros**. Tenha em atenção resultado Olá Olá serviço RRS, **PREVER valores** verde. Quando todas as colunas para uma determinada linha estão preenchidas, Olá livro automaticamente chama Olá API de classificação e apresenta Olá classificada resultados.
   
    ![][4]
5. tooscore mais do que uma linha, a segunda linha da preenchimento Olá com dados e Olá prever valores são produzidos. Ainda pode colar linhas várias em simultâneo.

Pode utilizar qualquer uma das funcionalidades de Excel Olá (gráficos, mapa de energia, condicional formatação, etc.) com Olá prever valores toohelp visualizar dados de Olá.    

## <a name="sharing-your-workbook"></a>Partilhar o seu livro
Para Olá macros toowork, a chave de API têm de constar da folha de cálculo de Olá. Isto significa que devem partilhar o livro Olá apenas com entidades/indivíduos que confia.

## <a name="automatic-updates"></a>Atualizações automáticas
É efetuada uma chamada RRS nestas duas situações:

1. Olá pela primeira vez uma linha possui conteúdo em todos os respetivos **parâmetros**
2. Sempre que qualquer um dos Olá **parâmetros** alterações numa linha que tinha todos os respetivos **parâmetros** introduzido.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
