---
title: "nível de compatibilidade do modelo de aaaData no Azure Analysis Services | Microsoft Docs"
description: "Compreender o nível de compatibilidade do modelo de dados de tabela."
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
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="e476a-103">Nível de compatibilidade para modelos em tabela do Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e476a-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="e476a-104">*Nível de compatibilidade* refere-se comportamentos toorelease específico no motor do Analysis Services Olá.</span><span class="sxs-lookup"><span data-stu-id="e476a-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="e476a-105">Nível de compatibilidade de toohello de alterações, normalmente, a operação com as versões principais do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e476a-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="e476a-106">Estas alterações também são implementadas no paridade de toomaintain Azure Analysis Services entre ambas as plataformas.</span><span class="sxs-lookup"><span data-stu-id="e476a-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="e476a-107">Alterações de nível de compatibilidade também afetam as funcionalidades disponíveis nos seus modelos em tabela.</span><span class="sxs-lookup"><span data-stu-id="e476a-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="e476a-108">Por exemplo, DirectQuery e de metadados do objeto de tabela tem implementações diferentes, dependendo do nível de compatibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="e476a-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="e476a-109">Serviços de análise do Azure suporta modelos em tabela níveis de compatibilidade de Olá 1200 e 1400.</span><span class="sxs-lookup"><span data-stu-id="e476a-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="e476a-110">nível de compatibilidade mais recente Olá é 1400.</span><span class="sxs-lookup"><span data-stu-id="e476a-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="e476a-111">Este nível coincide com o SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="e476a-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="e476a-112">Nível de compatibilidade de 1400 Olá principais funcionalidades incluem:</span><span class="sxs-lookup"><span data-stu-id="e476a-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="e476a-113">Nova infraestrutura para conectividade de dados e importação para modelos em tabela com suporte para personalizada APIs e TMSL scripting.</span><span class="sxs-lookup"><span data-stu-id="e476a-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="e476a-114">Esta nova funcionalidade permite suporte para origens de dados adicionais, como o armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e476a-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="e476a-115">Transformação de dados e as capacidades de aplicação híbrida de dados através de expressões de obter dados e o M.</span><span class="sxs-lookup"><span data-stu-id="e476a-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="e476a-116">Medidas suportam uma propriedade de linhas de detalhe com uma expressão DAX.</span><span class="sxs-lookup"><span data-stu-id="e476a-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="e476a-117">Esta propriedade permite que as ferramentas de cliente, como o Microsoft Excel toodrill baixo toodetailed dados a partir de um relatório agregado.</span><span class="sxs-lookup"><span data-stu-id="e476a-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="e476a-118">Por exemplo, quando os utilizadores visualizar vendas totais para uma região e o mês, podem visualizar os detalhes da encomenda Olá associado.</span><span class="sxs-lookup"><span data-stu-id="e476a-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="e476a-119">Segurança ao nível do objeto de tabela e coluna de nomes, além disso toohello dados nelas.</span><span class="sxs-lookup"><span data-stu-id="e476a-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="e476a-120">Suporte melhorado para hierarquias desalinhadas.</span><span class="sxs-lookup"><span data-stu-id="e476a-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="e476a-121">Monitorização de desempenho e melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="e476a-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="e476a-122">Nível de compatibilidade de conjunto</span><span class="sxs-lookup"><span data-stu-id="e476a-122">Set compatibility level</span></span> 
 <span data-ttu-id="e476a-123">Quando criar um novo projeto de modelo em tabela no SSDT, pode especificar o nível de compatibilidade de Olá no Olá **estruturador de modelos em tabela** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e476a-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="e476a-125">Se selecionar Olá **não mostrar esta mensagem novamente** opção, todos os projetos subsequentes utilizam o nível de compatibilidade de Olá especificado como predefinição de Olá.</span><span class="sxs-lookup"><span data-stu-id="e476a-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="e476a-126">Pode alterar o nível de compatibilidade predefinido Olá no SSDT no **ferramentas** > **opções**.</span><span class="sxs-lookup"><span data-stu-id="e476a-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="e476a-127">tooupgrade um projeto de modelo em tabela existente no SSDT, conjunto Olá **nível de compatibilidade** propriedade no modelo de Olá **propriedades** janela.</span><span class="sxs-lookup"><span data-stu-id="e476a-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="e476a-128">Tenha em atenção, atualizar o nível de compatibilidade de Olá é irreversível.</span><span class="sxs-lookup"><span data-stu-id="e476a-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="e476a-129">Verifique o nível de compatibilidade para uma base de dados do modelo em tabela no SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="e476a-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="e476a-130">No SSMS, clique no nome da base de dados de Olá > **propriedades** > **nível de compatibilidade**.</span><span class="sxs-lookup"><span data-stu-id="e476a-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="e476a-131">Verifique o nível de compatibilidade suportado para um servidor no SSMS</span><span class="sxs-lookup"><span data-stu-id="e476a-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="e476a-132">No SSMS, clique no nome do servidor Olá > **propriedades** > **nível de compatibilidade suportado**.</span><span class="sxs-lookup"><span data-stu-id="e476a-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="e476a-133">Esta propriedade especifica Olá mais elevado nível de compatibilidade de uma base de dados que será executado no servidor de Olá (excluindo pré-visualização).</span><span class="sxs-lookup"><span data-stu-id="e476a-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="e476a-134">Não é possível alterar o nível de compatibilidade de Olá suportado.</span><span class="sxs-lookup"><span data-stu-id="e476a-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e476a-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e476a-135">Next steps</span></span>
  <span data-ttu-id="e476a-136">[Criar um modelo no portal do Azure](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="e476a-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="e476a-137">Gerir do Analysis Services</span><span class="sxs-lookup"><span data-stu-id="e476a-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
