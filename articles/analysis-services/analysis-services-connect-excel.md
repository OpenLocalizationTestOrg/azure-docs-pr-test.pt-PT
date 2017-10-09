---
title: aaaConnect tooAzure Analysis Services com o Excel | Microsoft Docs
description: Saiba como tooconnect tooan do Azure Analysis Services server utilizando o Excel.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a>Ligar com o Excel

Assim que tiver criado um servidor no Azure e implementar um modelo em tabela tooit, está pronto tooconnect e começar a explorar os dados.


## <a name="connect-in-excel"></a>Ligar no Excel

Ligar o servidor de tooa no Excel é suportada utilizando obter dados no Excel 2016. A ligação utilizando Olá Assistente de importação de tabelas do Power Pivot não é suportada. 

**tooconnect no Excel 2016**

1. Excel 2016, no Olá **dados** do Friso, clique em **obter dados externos** > **de outras origens** > **do Analysis Services** .

2. No Assistente de ligação de dados, de Olá no **nome do servidor**, introduza nome do servidor Olá, incluindo o protocolo e o URI. Em seguida, no **credenciais de início de sessão**, selecione **Olá de utilização seguintes nome de utilizador e palavra-passe**e, em seguida, escreva o nome de utilizador organizacional Olá, por exemplo nancy@adventureworks.come a palavra-passe.

    ![Ligar a partir do início de sessão de Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. No **selecionar base de dados e tabela**, selecione a base de dados de Olá e o modelo ou perspetiva e, em seguida, clique em **concluir**.
   
    ![Ligar a partir de modelo selecione do Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a>Consultar também
[Bibliotecas de cliente](analysis-services-data-providers.md)   
[Gerir o seu servidor](analysis-services-manage.md)     


