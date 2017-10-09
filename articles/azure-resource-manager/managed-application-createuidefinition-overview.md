---
title: "aaaUnderstand Criar definição de IU para aplicações geridas do Azure | Microsoft Docs"
description: "Descreve como toocreate definições de IU para aplicações geridas do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="19c76-103">Introdução ao CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="19c76-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="19c76-104">Este documento apresenta alguns conceitos de núcleos de Olá de um CreateUiDefinition, que é utilizada pela interface de utilizador de Olá do Olá toogenerate portal do Azure para criar uma aplicação gerida.</span><span class="sxs-lookup"><span data-stu-id="19c76-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="19c76-105">Um CreateUiDefinition sempre contém três propriedades:</span><span class="sxs-lookup"><span data-stu-id="19c76-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="19c76-106">processador</span><span class="sxs-lookup"><span data-stu-id="19c76-106">handler</span></span>
* <span data-ttu-id="19c76-107">Versão</span><span class="sxs-lookup"><span data-stu-id="19c76-107">version</span></span>
* <span data-ttu-id="19c76-108">parâmetros</span><span class="sxs-lookup"><span data-stu-id="19c76-108">parameters</span></span>

<span data-ttu-id="19c76-109">Para aplicações geridas, o processador deve ser sempre `Microsoft.Compute.MultiVm`, e a versão de Olá mais recente suportado é `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="19c76-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="19c76-110">esquema de Olá da propriedade de parâmetros de Olá depende da combinação de Olá de processador especificado Olá e versão.</span><span class="sxs-lookup"><span data-stu-id="19c76-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="19c76-111">Para aplicações geridas, propriedades Olá suportado são `basics`, `steps`, e `outputs`.</span><span class="sxs-lookup"><span data-stu-id="19c76-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="19c76-112">Olá propriedades as noções básicas e passos contenham Olá _elementos_ , como as caixas de texto e as dropdowns - toobe apresentado no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="19c76-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="19c76-113">saídas Olá propriedade é utilizada toomap Olá saída valores de Olá especificado de elementos toohello parâmetros do modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="19c76-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="19c76-114">Incluindo `$schema` é recomendada, mas opcionais.</span><span class="sxs-lookup"><span data-stu-id="19c76-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="19c76-115">Se for especificado, Olá valor para `version` tem de corresponder à versão de Olá dentro Olá `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="19c76-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="19c76-116">Noções básicas</span><span class="sxs-lookup"><span data-stu-id="19c76-116">Basics</span></span>
<span data-ttu-id="19c76-117">passo Noções básicas de Olá é sempre Olá primeiro passo assistente Olá gerado ao hello do portal do Azure analisa um CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="19c76-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="19c76-118">Além disso elementos de Olá toodisplaying especificado no `basics`, portal Olá injects elementos para a subscrição do utilizadores toochoose Olá, grupo de recursos e localização para a implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="19c76-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="19c76-119">Geralmente, os elementos de consulta para os parâmetros de toda a implementação, como o nome de Olá de credenciais de administrador ou de cluster, devem passar neste passo.</span><span class="sxs-lookup"><span data-stu-id="19c76-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="19c76-120">Se o comportamento de um elemento depende da subscrição, o grupo de recursos ou localização do utilizador Olá, em seguida, que o elemento não é possível utilizar Noções básicas.</span><span class="sxs-lookup"><span data-stu-id="19c76-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="19c76-121">Por exemplo, **Microsoft.Compute.SizeSelector** depende subscrição e localização toodetermine Olá lista do utilizador Olá de tamanhos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="19c76-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="19c76-122">Por conseguinte, **Microsoft.Compute.SizeSelector** só pode ser utilizada nos passos.</span><span class="sxs-lookup"><span data-stu-id="19c76-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="19c76-123">Geralmente, apenas os elementos da Olá **Microsoft.Common** espaço de nomes pode ser utilizado no Noções básicas.</span><span class="sxs-lookup"><span data-stu-id="19c76-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="19c76-124">Embora alguns elementos em outros espaços de nomes (como **Microsoft.Compute.Credentials**) que não dependem do contexto do utilizador Olá, ainda são permitidas.</span><span class="sxs-lookup"><span data-stu-id="19c76-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="19c76-125">Passos</span><span class="sxs-lookup"><span data-stu-id="19c76-125">Steps</span></span>
<span data-ttu-id="19c76-126">propriedade de passos de Olá pode conter zero ou mais toodisplay de passos adicionais após Noções básicas, cada um dos quais contém um ou mais elementos.</span><span class="sxs-lookup"><span data-stu-id="19c76-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="19c76-127">Considere adicionar passos por função ou a camada da aplicação Olá a ser implementada.</span><span class="sxs-lookup"><span data-stu-id="19c76-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="19c76-128">Por exemplo, adicione um passo para entradas de nós principais Olá e um passo para nós de trabalho de Olá num cluster.</span><span class="sxs-lookup"><span data-stu-id="19c76-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="19c76-129">saídas</span><span class="sxs-lookup"><span data-stu-id="19c76-129">Outputs</span></span>
<span data-ttu-id="19c76-130">Olá portal do Azure utiliza Olá `outputs` elementos da propriedade toomap de `basics` e `steps` toohello parâmetros do modelo de implementação Azure Resource Manager Olá.</span><span class="sxs-lookup"><span data-stu-id="19c76-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="19c76-131">chaves de Olá deste dicionário estão nomes Olá Olá dos parâmetros do modelo e valores de Olá são propriedades dos objetos de resultado Olá de elementos de Olá referenciado.</span><span class="sxs-lookup"><span data-stu-id="19c76-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="19c76-132">Funções</span><span class="sxs-lookup"><span data-stu-id="19c76-132">Functions</span></span>
<span data-ttu-id="19c76-133">Semelhante demasiado[funções de modelo](resource-group-template-functions.md) no Azure Resource Manager (tanto no como sintaxe funcionalidade), CreateUiDefinition fornece funções para trabalhar com dos elementos entradas e saídas, bem como as funcionalidades, tais como conditionals.</span><span class="sxs-lookup"><span data-stu-id="19c76-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19c76-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="19c76-134">Next steps</span></span>
<span data-ttu-id="19c76-135">CreateUiDefinition próprio tem um esquema simple.</span><span class="sxs-lookup"><span data-stu-id="19c76-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="19c76-136">profundidade real de Olá-provém de todos os elementos de Olá suportada e as funções, que Olá seguintes documentos descrevem wondrous detalhadamente:</span><span class="sxs-lookup"><span data-stu-id="19c76-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="19c76-137">Elementos</span><span class="sxs-lookup"><span data-stu-id="19c76-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="19c76-138">Funções</span><span class="sxs-lookup"><span data-stu-id="19c76-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="19c76-139">Está aqui disponível atual do esquema JSON para CreateUiDefinition: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="19c76-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="19c76-140">Versões posteriores estará disponíveis em Olá mesma localização.</span><span class="sxs-lookup"><span data-stu-id="19c76-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="19c76-141">Substitua Olá `0.1.2-preview` parte do URL de Olá e Olá `version` valor com o identificador da versão Olá tenciona toouse.</span><span class="sxs-lookup"><span data-stu-id="19c76-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="19c76-142">identificadores de versão Olá atualmente suportado são `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, e `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="19c76-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
