---
title: "aaaContinuous implementação com a aplicação de Web do Azure no Linux | Microsoft Docs"
description: "Como toosetup a implementação contínua na aplicação de Web do Azure no Linux."
keywords: "serviço de aplicações do Azure, linux, oss, acr"
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="57706-104">Implementação contínua com a aplicação de Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="57706-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="57706-105">Neste tutorial, configura a implementação contínua para uma imagem personalizada contentor de gerido [registo de contentor do Azure](https://azure.microsoft.com/en-us/services/container-registry/) repositórios ou [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="57706-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="57706-106">Passo 1 - tooAzure de início de sessão</span><span class="sxs-lookup"><span data-stu-id="57706-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="57706-107">A iniciar sessão toohello do portal do Azure em http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="57706-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="57706-108">Passo 2 - funcionalidade de implementação contínua de contentor de ativação</span><span class="sxs-lookup"><span data-stu-id="57706-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="57706-109">Pode ativar através da funcionalidade de implementação contínua de Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e Olá os seguintes comandos a executar</span><span class="sxs-lookup"><span data-stu-id="57706-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="57706-110">No Olá  **[portal do Azure](https://portal.azure.com/)**, clique em Olá **do serviço de aplicações** opção esquerda Olá da página Olá.</span><span class="sxs-lookup"><span data-stu-id="57706-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="57706-111">Clique no nome de Olá da sua aplicação que pretende que sejam tooconfigure Docker Hub a implementação contínua para.</span><span class="sxs-lookup"><span data-stu-id="57706-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="57706-112">No Olá **as definições de aplicação**, adicionar uma aplicação definição chamado `DOCKER_ENABLE_CI` com o valor de Olá `true`.</span><span class="sxs-lookup"><span data-stu-id="57706-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![Inserir uma imagem de definição de aplicação](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="57706-114">Passo 3 – Preparar o URL do Webhook</span><span class="sxs-lookup"><span data-stu-id="57706-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="57706-115">Pode obter utilizando o URL do Webhook Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e Olá os seguintes comandos a executar</span><span class="sxs-lookup"><span data-stu-id="57706-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="57706-116">Para o URL do Webhook Olá, terá de Olá toohave seguinte ponto final: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="57706-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="57706-117">Pode obter o `publishingusername` e `publishingpwd` ao transferir a aplicação web de Olá publicar perfis com Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="57706-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![Inserir uma imagem de adição de webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="57706-119">Passo 4 – adicionar um hook de web</span><span class="sxs-lookup"><span data-stu-id="57706-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="57706-120">Registo de Contentores do Azure</span><span class="sxs-lookup"><span data-stu-id="57706-120">Azure Container Registry</span></span>

<span data-ttu-id="57706-121">No seu painel do portal de registo, clique em **Webhooks**, criar um novo webhook clicando **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="57706-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="57706-122">No Olá **criar o webhook** painel, dê um nome do webhook.</span><span class="sxs-lookup"><span data-stu-id="57706-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="57706-123">Para o URI de Webhook Olá, terá de tooprovide Olá URL obtido a partir do **passo 3**</span><span class="sxs-lookup"><span data-stu-id="57706-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="57706-124">Certifique-se de que definir âmbito de Olá como Olá repositório que contém a imagem de contentor.</span><span class="sxs-lookup"><span data-stu-id="57706-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![Inserir uma imagem do webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="57706-126">Quando a imagem de Olá for atualizada, aplicação web de Olá for atualizado automaticamente com a nova imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="57706-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="57706-127">Hub de docker</span><span class="sxs-lookup"><span data-stu-id="57706-127">Docker Hub</span></span>

<span data-ttu-id="57706-128">Na página do seu Hub de Docker, clique em **Webhooks**, em seguida, **WEBHOOK de A criar**.</span><span class="sxs-lookup"><span data-stu-id="57706-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![Inserir uma imagem de adição de webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="57706-130">Para o URL do Webhook Olá, terá de tooprovide Olá URL obtida **passo 3**</span><span class="sxs-lookup"><span data-stu-id="57706-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![Inserir uma imagem de adição de webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="57706-132">Quando a imagem de Olá for atualizada, aplicação web de Olá for atualizado automaticamente com a nova imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="57706-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57706-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="57706-133">Next steps</span></span>
* [<span data-ttu-id="57706-134">O que é a aplicação de Web do Azure no Linux?</span><span class="sxs-lookup"><span data-stu-id="57706-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="57706-135">Registo de contentor do Azure</span><span class="sxs-lookup"><span data-stu-id="57706-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="57706-136">Utilizar a configuração de PM2 para Node.js na aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="57706-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="57706-137">Utilizando o .NET Core na aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="57706-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="57706-138">Utilizar Ruby na aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="57706-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="57706-139">Como toouse um Docker personalizado imagem para a aplicação de Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="57706-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="57706-140">Aplicação de Web do App Service do Azure no Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="57706-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="57706-141">Gerir a aplicação Web no Linux utilizando o Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="57706-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



