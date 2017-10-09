---
title: webhooks de registo do contentor aaaAzure | Microsoft Docs
description: Webhooks de registo de contentor do Azure
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acr, azure-container-registry
keywords: Docker, contentores, ACR
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/06/2017
ms.author: nepeters
ms.openlocfilehash: adc2afec486007e2d54cd689e6f7ef8b1098db06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-container-registry-webhooks---azure-portal"></a><span data-ttu-id="8f466-104">Utilizar webhooks de registo de contentor do Azure - portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-104">Using Azure Container Registry webhooks - Azure portal</span></span>

<span data-ttu-id="8f466-105">Um registo de contentor do Azure armazena e gere a imagens de contentor de Docker privadas, forma toohello semelhante Docker Hub armazena públicas imagens de Docker.</span><span class="sxs-lookup"><span data-stu-id="8f466-105">An Azure container registry stores and manages private Docker container images, similar toohello way Docker Hub stores public Docker images.</span></span> <span data-ttu-id="8f466-106">Utilize webhooks tootrigger eventos quando determinadas ações ocorrer dos seus repositórios de registo.</span><span class="sxs-lookup"><span data-stu-id="8f466-106">You use webhooks tootrigger events when certain actions take place in one of your registry repositories.</span></span> <span data-ttu-id="8f466-107">Webhooks pode responder tooevents ao nível de registo Olá ou podem ser confinados para baixo tooa etiquetas de repositório específico.</span><span class="sxs-lookup"><span data-stu-id="8f466-107">Webhooks can respond tooevents at hello registry level or they can be scoped down tooa specific repository tag.</span></span> 

<span data-ttu-id="8f466-108">Para obter mais em segundo plano e conceitos, consulte Olá [descrição geral](./container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8f466-108">For more background and concepts, see hello [overview](./container-registry-intro.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f466-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f466-109">Prerequisites</span></span> 

- <span data-ttu-id="8f466-110">O contentor do Azure gerida registo - criar um registo de contentor geridos na sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f466-110">Azure container managed registry - Create a managed container registry in your Azure subscription.</span></span> <span data-ttu-id="8f466-111">Por exemplo, utilize Olá portal do Azure ou Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="8f466-111">For example, use hello Azure portal or hello Azure CLI 2.0.</span></span> 
- <span data-ttu-id="8f466-112">Docker CLI - tooset cópia de segurança do computador local como uma Docker anfitrião e acesso Olá CLI do Docker comandos, instale o motor de Docker.</span><span class="sxs-lookup"><span data-stu-id="8f466-112">Docker CLI - tooset up your local computer as a Docker host and access hello Docker CLI commands, install Docker Engine.</span></span> 

## <a name="create-webhook-azure-portal"></a><span data-ttu-id="8f466-113">Criar o webhook portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-113">Create webhook Azure portal</span></span>

1. <span data-ttu-id="8f466-114">Inicie sessão no toohello portal do Azure e navegue até o registo de toohello em que pretende toocreate webhooks.</span><span class="sxs-lookup"><span data-stu-id="8f466-114">Log in toohello Azure portal and navigate toohello registry in which you want toocreate webhooks.</span></span> 

2. <span data-ttu-id="8f466-115">No painel do contentor de Olá, selecione o separador de "Webhooks" Olá.</span><span class="sxs-lookup"><span data-stu-id="8f466-115">In hello container blade, select hello "Webhooks" tab.</span></span> 

3. <span data-ttu-id="8f466-116">Selecione "Adicionar" na barra de ferramentas do Olá webhook painel.</span><span class="sxs-lookup"><span data-stu-id="8f466-116">Select "Add" from hello webhook blade toolbar.</span></span> 

4. <span data-ttu-id="8f466-117">Olá concluída *criar o Webhook* formulário com Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="8f466-117">Complete hello *Create Webhook* form with hello following information:</span></span>

| <span data-ttu-id="8f466-118">Valor</span><span class="sxs-lookup"><span data-stu-id="8f466-118">Value</span></span> | <span data-ttu-id="8f466-119">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f466-119">Description</span></span> |
|---|---|
| <span data-ttu-id="8f466-120">Nome</span><span class="sxs-lookup"><span data-stu-id="8f466-120">Name</span></span> | <span data-ttu-id="8f466-121">nome de Olá pretende toogive toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="8f466-121">hello name you want toogive toohello webhook.</span></span> <span data-ttu-id="8f466-122">Só pode conter letras minúsculas e números e entre 5 e 50 carateres.</span><span class="sxs-lookup"><span data-stu-id="8f466-122">It can only contain lowercase letters and numbers and between 5-50 characters.</span></span> |
| <span data-ttu-id="8f466-123">URI do serviço</span><span class="sxs-lookup"><span data-stu-id="8f466-123">Service URI</span></span> | <span data-ttu-id="8f466-124">Olá URI onde Olá webhook deve enviar notificações de POST.</span><span class="sxs-lookup"><span data-stu-id="8f466-124">hello URI where hello webhook should send POST notifications.</span></span> |
| <span data-ttu-id="8f466-125">Cabeçalhos personalizados</span><span class="sxs-lookup"><span data-stu-id="8f466-125">Custom headers</span></span> | <span data-ttu-id="8f466-126">Cabeçalhos que pretende toopass juntamente com o pedido POST Olá.</span><span class="sxs-lookup"><span data-stu-id="8f466-126">Headers you want toopass along with hello POST request.</span></span> <span data-ttu-id="8f466-127">Devem ser na "chave: valor" formato.</span><span class="sxs-lookup"><span data-stu-id="8f466-127">They should be in "key: value" format.</span></span> |
| <span data-ttu-id="8f466-128">Ações de Acionador</span><span class="sxs-lookup"><span data-stu-id="8f466-128">Trigger actions</span></span> | <span data-ttu-id="8f466-129">Ações que acionam Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="8f466-129">Actions that trigger hello webhook.</span></span> <span data-ttu-id="8f466-130">Atualmente webhooks pode ser acionada por push e/ou eliminar ações tooan imagem.</span><span class="sxs-lookup"><span data-stu-id="8f466-130">Currently webhooks can be triggered by push and/or delete actions tooan image.</span></span> |
| <span data-ttu-id="8f466-131">Estado</span><span class="sxs-lookup"><span data-stu-id="8f466-131">Status</span></span> | <span data-ttu-id="8f466-132">Estado de Olá do webhook Olá depois de criado.</span><span class="sxs-lookup"><span data-stu-id="8f466-132">hello status for hello webhook after it's created.</span></span> <span data-ttu-id="8f466-133">Está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="8f466-133">It's enabled by default.</span></span> |
| <span data-ttu-id="8f466-134">Âmbito</span><span class="sxs-lookup"><span data-stu-id="8f466-134">Scope</span></span> | <span data-ttu-id="8f466-135">âmbito de Olá no que funciona de webhook Olá.</span><span class="sxs-lookup"><span data-stu-id="8f466-135">hello scope at which hello webhook works.</span></span> <span data-ttu-id="8f466-136">Por predefinição, o âmbito de Olá é para todos os eventos no registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="8f466-136">By default hello scope is for all events in hello registry.</span></span> <span data-ttu-id="8f466-137">Pode ser especificado para um repositório ou uma tag utilizando o formato de Olá "repositório: tag".</span><span class="sxs-lookup"><span data-stu-id="8f466-137">It can be specified for a repository or a tag by using hello format "repository: tag".</span></span> |

<span data-ttu-id="8f466-138">Formulário de webhook de exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f466-138">Example webhook form:</span></span>

![IU DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a><span data-ttu-id="8f466-140">Criar o webhook CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-140">Create webhook Azure CLI</span></span>

<span data-ttu-id="8f466-141">toocreate utilizando um webhook Olá CLI do Azure, utilize Olá [az acr webhook criar](/cli/azure/acr/webhook#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8f466-141">toocreate a webhook using hello Azure CLI, use hello [az acr webhook create](/cli/azure/acr/webhook#create) command.</span></span>

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a><span data-ttu-id="8f466-142">Webhook de teste</span><span class="sxs-lookup"><span data-stu-id="8f466-142">Test webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8f466-143">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-143">Azure portal</span></span>

<span data-ttu-id="8f466-144">Toousing anterior Olá webhook no contentor de push de imagem e eliminar ações, pode ser testada com Olá **Ping** botão.</span><span class="sxs-lookup"><span data-stu-id="8f466-144">Prior toousing hello webhook on container image push and delete actions, it can be tested using hello **Ping** button.</span></span> <span data-ttu-id="8f466-145">Quando utilizado, Olá Ping envia que um toohello de pedido de post genérico especificado ponto final e registos Olá resposta.</span><span class="sxs-lookup"><span data-stu-id="8f466-145">When used, hello Ping sends a generic post request toohello specified endpoint and logs hello response.</span></span> <span data-ttu-id="8f466-146">Esta ação é útil tooverify Olá webhook foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="8f466-146">This is helpful tooverify that hello webhook has been set up correctly.</span></span>

1. <span data-ttu-id="8f466-147">Selecione o webhook Olá pretende tootest.</span><span class="sxs-lookup"><span data-stu-id="8f466-147">Select hello webhook you want tootest.</span></span> 
2. <span data-ttu-id="8f466-148">Na barra de ferramentas superior de Olá, selecione a ação de "um Ping" Olá.</span><span class="sxs-lookup"><span data-stu-id="8f466-148">In hello top toolbar, select hello "Ping" action.</span></span> 
3. <span data-ttu-id="8f466-149">Verifique Olá pedido e resposta.</span><span class="sxs-lookup"><span data-stu-id="8f466-149">Check hello request and response.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="8f466-150">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-150">Azure CLI</span></span>

<span data-ttu-id="8f466-151">tootest um webhook ACR com Olá CLI do Azure, utilize Olá [ping de webhook az acr](/cli/azure/acr/webhook#ping) comando.</span><span class="sxs-lookup"><span data-stu-id="8f466-151">tootest an ACR webhook with hello Azure CLI, use hello [az acr webhook ping](/cli/azure/acr/webhook#ping) command.</span></span>

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

<span data-ttu-id="8f466-152">resultados de Olá toosee, utilize Olá [az acr webhook lista-eventos](/cli/azure/acr/webhook#list-events) comando.</span><span class="sxs-lookup"><span data-stu-id="8f466-152">toosee hello results, use hello [az acr webhook list-events](/cli/azure/acr/webhook#list-events) command.</span></span> 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a><span data-ttu-id="8f466-153">Eliminar o webhook</span><span class="sxs-lookup"><span data-stu-id="8f466-153">Delete webhook</span></span>

### <a name="azure-portal"></a><span data-ttu-id="8f466-154">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-154">Azure portal</span></span>

<span data-ttu-id="8f466-155">Cada webhook pode ser eliminado, selecionando Olá webhook e, em seguida, o botão para eliminar Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f466-155">Each webhook can be deleted by selecting hello webhook and then hello delete button on hello Azure portal.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="8f466-156">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8f466-156">Azure CLI</span></span>

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```