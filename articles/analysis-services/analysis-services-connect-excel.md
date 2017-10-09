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
# <a name="connect-with-excel"></a><span data-ttu-id="8636c-103">Ligar com o Excel</span><span class="sxs-lookup"><span data-stu-id="8636c-103">Connect with Excel</span></span>

<span data-ttu-id="8636c-104">Assim que tiver criado um servidor no Azure e implementar um modelo em tabela tooit, está pronto tooconnect e começar a explorar os dados.</span><span class="sxs-lookup"><span data-stu-id="8636c-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="8636c-105">Ligar no Excel</span><span class="sxs-lookup"><span data-stu-id="8636c-105">Connect in Excel</span></span>

<span data-ttu-id="8636c-106">Ligar o servidor de tooa no Excel é suportada utilizando obter dados no Excel 2016.</span><span class="sxs-lookup"><span data-stu-id="8636c-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="8636c-107">A ligação utilizando Olá Assistente de importação de tabelas do Power Pivot não é suportada.</span><span class="sxs-lookup"><span data-stu-id="8636c-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="8636c-108">**tooconnect no Excel 2016**</span><span class="sxs-lookup"><span data-stu-id="8636c-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="8636c-109">Excel 2016, no Olá **dados** do Friso, clique em **obter dados externos** > **de outras origens** > **do Analysis Services** .</span><span class="sxs-lookup"><span data-stu-id="8636c-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="8636c-110">No Assistente de ligação de dados, de Olá no **nome do servidor**, introduza nome do servidor Olá, incluindo o protocolo e o URI.</span><span class="sxs-lookup"><span data-stu-id="8636c-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="8636c-111">Em seguida, no **credenciais de início de sessão**, selecione **Olá de utilização seguintes nome de utilizador e palavra-passe**e, em seguida, escreva o nome de utilizador organizacional Olá, por exemplo nancy@adventureworks.come a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="8636c-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Ligar a partir do início de sessão de Excel](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="8636c-113">No **selecionar base de dados e tabela**, selecione a base de dados de Olá e o modelo ou perspetiva e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="8636c-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Ligar a partir de modelo selecione do Excel](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="8636c-115">Consultar também</span><span class="sxs-lookup"><span data-stu-id="8636c-115">See also</span></span>
<span data-ttu-id="8636c-116">[Bibliotecas de cliente](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="8636c-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="8636c-117">Gerir o seu servidor</span><span class="sxs-lookup"><span data-stu-id="8636c-117">Manage your server</span></span>](analysis-services-manage.md)     


