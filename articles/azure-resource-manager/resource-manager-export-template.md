---
title: modelo do Azure Resource Manager aaaExport | Microsoft Docs
description: Utilize o Azure Resource Manager tooexport um modelo a partir de um grupo de recursos existente.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="33582-103">Exportar um modelo do Azure Resource Manager a partir de recursos existentes</span><span class="sxs-lookup"><span data-stu-id="33582-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="33582-104">Neste artigo, saiba como tooexport um modelo do Resource Manager a partir dos recursos existentes na sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="33582-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="33582-105">Pode utilizar esse modelo gerado de toogain uma melhor compreensão da sintaxe do modelo.</span><span class="sxs-lookup"><span data-stu-id="33582-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="33582-106">Existem duas formas tooexport um modelo:</span><span class="sxs-lookup"><span data-stu-id="33582-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="33582-107">Pode exportar Olá **modelo utilizado para a implementação**.</span><span class="sxs-lookup"><span data-stu-id="33582-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="33582-108">modelo exportado Olá inclui todos os parâmetros de Olá e variáveis exatamente como estes apareceu no modelo original Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="33582-109">Esta abordagem é útil quando tiver implementado recursos através do portal de Olá e pretende toosee Olá modelo toocreate esses recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="33582-110">Este modelo pode ser utilizado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="33582-110">This template is readily usable.</span></span> 
* <span data-ttu-id="33582-111">Pode exportar um **gerou modelo que representa o estado atual do Olá Olá do grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="33582-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="33582-112">modelo exportado Olá não é baseado em qualquer modelo que utilizou para a implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="33582-113">Em vez disso, cria um modelo que é um instantâneo Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="33582-114">modelo exportado Olá tem muitos valores codificados e provavelmente não tantos parâmetros como normalmente seriam definidos.</span><span class="sxs-lookup"><span data-stu-id="33582-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="33582-115">Esta abordagem é útil quando modificar grupo de recursos de Olá após a implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="33582-116">Normalmente, este modelo requer modificações antes de poder ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="33582-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="33582-117">Este tópico mostra ambas as abordagens através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="33582-118">Implementar recursos</span><span class="sxs-lookup"><span data-stu-id="33582-118">Deploy resources</span></span>
<span data-ttu-id="33582-119">Vamos começar por implementar tooAzure de recursos que pode utilizar para exportar como um modelo.</span><span class="sxs-lookup"><span data-stu-id="33582-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="33582-120">Se já tiver um grupo de recursos na sua subscrição que pretende que o modelo de tooa tooexport, pode ignorar esta secção.</span><span class="sxs-lookup"><span data-stu-id="33582-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="33582-121">resto Olá deste artigo parte do princípio de que implementou Olá web app e a solução de base de dados do SQL Server apresentados nesta secção.</span><span class="sxs-lookup"><span data-stu-id="33582-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="33582-122">Se utilizar uma solução diferente, a sua experiência poderá ser ligeiramente diferente, mas passos Olá tooexport um modelo são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="33582-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="33582-123">No Olá [portal do Azure](https://portal.azure.com), selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="33582-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![selecionar novo](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="33582-125">Procurar **aplicação web + SQL** e selecione-a partir das opções disponíveis Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![procurar aplicação Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="33582-127">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="33582-127">Select **Create**.</span></span>

      ![selecione criar](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="33582-129">Fornece valores de Olá necessário para Olá web app e a base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="33582-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="33582-130">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="33582-130">Select **Create**.</span></span>

      ![forneça o valor da aplicação Web e do SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="33582-132">a implementação de Olá pode demorar um minuto.</span><span class="sxs-lookup"><span data-stu-id="33582-132">hello deployment may take a minute.</span></span> <span data-ttu-id="33582-133">Após a conclusão da implementação de Olá, a sua subscrição contém a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="33582-134">Ver o modelo no histórico de implementações</span><span class="sxs-lookup"><span data-stu-id="33582-134">View template from deployment history</span></span>
1. <span data-ttu-id="33582-135">Aceda toohello painel do grupo de recursos para o novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="33582-136">Tenha em atenção que painel Olá mostra o resultado de Olá da última implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="33582-137">Selecione essa ligação.</span><span class="sxs-lookup"><span data-stu-id="33582-137">Select this link.</span></span>
   
      ![painel do grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="33582-139">Pode ver um histórico de implementações de grupo Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="33582-140">No seu caso, o painel de Olá provavelmente lista apenas uma implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="33582-141">Selecione essa implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-141">Select this deployment.</span></span>
   
     ![última implementação](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="33582-143">Painel Olá mostra um resumo da implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="33582-144">Olá resumo inclui o estado de Olá da implementação de Olá e respetivas operações e a valores de Olá que fornecido para os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="33582-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="33582-145">modelo de Olá toosee que utilizou para a implementação de Olá, selecione **ver modelo**.</span><span class="sxs-lookup"><span data-stu-id="33582-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![ver resumo da implementação](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="33582-147">O Resource Manager obtém Olá sete ficheiros para os seguintes:</span><span class="sxs-lookup"><span data-stu-id="33582-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="33582-148">**Modelo** -modelo Olá que define a infraestrutura de Olá para a sua solução.</span><span class="sxs-lookup"><span data-stu-id="33582-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="33582-149">Quando criou a conta de armazenamento Olá através do portal Olá, o Gestor de recursos utilizados toodeploy um modelo e guardou esse modelo para consulta futura.</span><span class="sxs-lookup"><span data-stu-id="33582-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="33582-150">**Os parâmetros** -um ficheiro de parâmetros que pode utilizar toopass valores durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="33582-151">Contém Olá valores que indicou durante a primeira implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="33582-152">Pode alterar qualquer um destes valores quando implementar novamente o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="33582-153">**CLI** -Azure uma interface de linha comandos (CLI) ficheiro do script que pode utilizar o modelo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33582-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="33582-154">**CLI 2.0** -Azure uma interface de linha comandos (CLI) ficheiro do script que pode utilizar o modelo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33582-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="33582-155">**PowerShell** -ficheiro de script de um Azure PowerShell que pode utilizar o modelo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33582-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="33582-156">**.NET** -uma classe .NET que pode utilizar o modelo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33582-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="33582-157">**Ruby** -classe A Ruby que pode utilizar o modelo de Olá toodeploy.</span><span class="sxs-lookup"><span data-stu-id="33582-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="33582-158">ficheiros de Olá estão disponíveis através de ligações no painel de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="33582-159">Por predefinição, o painel de Olá apresenta modelo Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-159">By default, hello blade displays hello template.</span></span>
      
       ![ver modelo](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="33582-161">Este modelo é utilizar o modelo real Olá toocreate a aplicação web e a base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="33582-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="33582-162">Tenha em atenção que contém os parâmetros que lhe permitem valores diferentes de tooprovide durante a implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="33582-163">toolearn mais informações sobre a estrutura de Olá de um modelo, consulte [modelos Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="33582-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="33582-164">Exportar o modelo de Olá do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="33582-164">Export hello template from resource group</span></span>
<span data-ttu-id="33582-165">Se tiver alterado os recursos ou adicionou recursos nas implementações de vários manualmente, a obtenção de um modelo do histórico de implementação de Olá não reflete o estado atual do Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="33582-166">Esta secção mostra como tooexport um modelo que reflete Olá estado atual do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="33582-167">Não pode exportar um modelo para um grupo de recursos que tenha mais de 200 recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="33582-168">modelo de Olá tooview para um grupo de recursos, selecione **scripts de automatização**.</span><span class="sxs-lookup"><span data-stu-id="33582-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="33582-170">Gestor de recursos avalia Olá recursos no grupo de recursos de Olá e gera um modelo para esses recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="33582-171">Nem todos os tipos de recursos suportam a função de modelo de exportação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="33582-172">Poderá ver um erro a indicar que existe um problema com a exportação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="33582-173">Saiba a forma como a toohandle os problemas na Olá [corrigir problemas de exportação](#fix-export-issues) secção.</span><span class="sxs-lookup"><span data-stu-id="33582-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="33582-174">Verá novamente os ficheiros de seis Olá que pode utilizar a solução de Olá tooredeploy.</span><span class="sxs-lookup"><span data-stu-id="33582-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="33582-175">No entanto, este modelo de Olá tempo é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="33582-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="33582-176">Tenha em atenção que Olá modelo gerado contém parâmetros menos do que o modelo de Olá na secção anterior.</span><span class="sxs-lookup"><span data-stu-id="33582-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="33582-177">Além disso, muitos dos valores de Olá (como a localização e valores SKU) estão hard-coded neste modelo, em vez de aceitar um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="33582-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="33582-178">Antes de a reutilizar este modelo, pode querer tooedit Olá modelo toomake melhor utilização de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="33582-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="33582-179">Tem duas opções para continuar a toowork com este modelo.</span><span class="sxs-lookup"><span data-stu-id="33582-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="33582-180">Pode transferir o modelo de Olá e trabalhar no mesmo localmente com um editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="33582-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="33582-181">Em alternativa, pode guardar a biblioteca de tooyour Olá modelos e trabalhar no mesmo através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="33582-182">Se estiver familiarizado com um editor de JSON como [VS Code](https://code.visualstudio.com/) ou [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), poderá preferir transferir modelo de Olá localmente e utilizar essa editor.</span><span class="sxs-lookup"><span data-stu-id="33582-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="33582-183">toowork localmente, selecione **transferir**.</span><span class="sxs-lookup"><span data-stu-id="33582-183">toowork locally, select **Download**.</span></span>
   
      ![transferir modelo](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="33582-185">Se não estiverem definidas cópias de segurança com um editor de JSON, poderá preferir editar Olá modelo através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="33582-186">resto Olá deste tópico parte do princípio de que foi guardado com biblioteca de tooyour Olá modelos no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="33582-187">No entanto, se a mesma Olá sintaxe alterações toohello modelo se trabalhar localmente com um editor de JSON ou através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="33582-188">Selecione toowork através do portal Olá, **adicionar toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="33582-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![Adicionar toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="33582-190">Ao adicionar uma biblioteca de modelos de toohello, dê o modelo de Olá um nome e descrição.</span><span class="sxs-lookup"><span data-stu-id="33582-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="33582-191">Em seguida, selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="33582-191">Then, select **Save**.</span></span>
   
     ![definir os valores do modelo](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="33582-193">tooview um modelo guardado na biblioteca, selecione **mais serviços**, tipo **modelos** toofilter resultados, selecionados **modelos**.</span><span class="sxs-lookup"><span data-stu-id="33582-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![localizar modelos](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="33582-195">Selecione o modelo de Olá com o nome de Olá guardou.</span><span class="sxs-lookup"><span data-stu-id="33582-195">Select hello template with hello name you saved.</span></span>
   
      ![selecionar modelo](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="33582-197">Personalizar o modelo de Olá</span><span class="sxs-lookup"><span data-stu-id="33582-197">Customize hello template</span></span>
<span data-ttu-id="33582-198">Olá exportada modelo funciona bem que se quiser toocreate Olá mesmo web app e a base de dados SQL para todas as implementações.</span><span class="sxs-lookup"><span data-stu-id="33582-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="33582-199">No entanto, o Resource Manager fornece opções para que possa implementar modelos com uma flexibilidade muito maior.</span><span class="sxs-lookup"><span data-stu-id="33582-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="33582-200">Este artigo mostra como parâmetros de tooadd para Olá da base de dados nome administrador e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="33582-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="33582-201">Pode utilizar este mesmo tooadd de abordagem mais flexibilidade para outros valores no modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="33582-202">modelo do toocustomize Olá, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="33582-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![mostrar modelo](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="33582-204">Selecione o modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-204">Select hello template.</span></span>
   
     ![editar modelo](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="33582-206">valores de Olá toopass capaz de toobe que poderá ser útil toospecify durante a implementação, adicionar Olá seguir dois parâmetros toohello **parâmetros** secção no modelo de Olá:</span><span class="sxs-lookup"><span data-stu-id="33582-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="33582-207">toouse Olá novos parâmetros, substitua a definição do servidor SQL Olá no Olá **recursos** secção.</span><span class="sxs-lookup"><span data-stu-id="33582-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="33582-208">Repare que **administratorLogin** e **administratorLoginPassword** utilizam agora os valores dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="33582-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="33582-209">Selecione **OK** quando tiver concluído a edição de modelo de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="33582-210">Selecione **guardar** modelo de toohello toosave Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="33582-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![guardar modelo](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="33582-212">modelo de Olá atualizado tooredeploy, selecione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="33582-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![implementar modelo](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="33582-214">Fornecer valores de parâmetros e selecione um recurso grupo toodeploy Olá recursos.</span><span class="sxs-lookup"><span data-stu-id="33582-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="33582-215">Corrigir problemas de exportação</span><span class="sxs-lookup"><span data-stu-id="33582-215">Fix export issues</span></span>
<span data-ttu-id="33582-216">Nem todos os tipos de recursos suportam a função de modelo de exportação de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="33582-217">tooresolve este problema, manualmente adicionar recursos em falta Olá no seu modelo.</span><span class="sxs-lookup"><span data-stu-id="33582-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="33582-218">mensagem de erro de saudação inclui tipos de recursos de Olá que não não possível exportar.</span><span class="sxs-lookup"><span data-stu-id="33582-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="33582-219">Localize o tipo de recurso na [Referência a modelos](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="33582-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="33582-220">Por exemplo, toomanually adicionar um gateway de rede virtual, consulte [referência ao modelo Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="33582-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="33582-221">Só encontra problemas de exportação se exportar a partir de um grupo de recursos em vez do seu histórico de implementação.</span><span class="sxs-lookup"><span data-stu-id="33582-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="33582-222">Se a última implementação representar com precisão o estado atual do Olá Olá do grupo de recursos, deve exportar modelo Olá do histórico de implementação de Olá, em vez do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="33582-223">Só deve exporte de um grupo de recursos quando efetuou um grupo de recursos de toohello alterações que não estão definidas num único modelo.</span><span class="sxs-lookup"><span data-stu-id="33582-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="33582-224">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="33582-224">Next steps</span></span>
<span data-ttu-id="33582-225">Aprendeu como tooexport um modelo a partir dos recursos que criou no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="33582-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="33582-226">Pode implementar um modelo através do [PowerShell](resource-group-template-deploy.md), do [CLI do Azure](resource-group-template-deploy-cli.md) ou da [API REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="33582-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="33582-227">toosee como tooexport um modelo através do PowerShell, consulte [utilizar o Azure PowerShell com o Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="33582-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="33582-228">toosee como tooexport um modelo através da CLI do Azure, consulte [Olá utilize CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="33582-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

