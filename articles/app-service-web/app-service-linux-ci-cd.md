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
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a>Implementação contínua com a aplicação de Web do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Neste tutorial, configura a implementação contínua para uma imagem personalizada contentor de gerido [registo de contentor do Azure](https://azure.microsoft.com/en-us/services/container-registry/) repositórios ou [Docker Hub](https://hub.docker.com).

## <a name="step-1---sign-in-tooazure"></a>Passo 1 - tooAzure de início de sessão

A iniciar sessão toohello do portal do Azure em http://portal.azure.com

## <a name="step-2---enable-container-continuous-deployment-feature"></a>Passo 2 - funcionalidade de implementação contínua de contentor de ativação

Pode ativar através da funcionalidade de implementação contínua de Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e Olá os seguintes comandos a executar

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

No Olá  **[portal do Azure](https://portal.azure.com/)**, clique em Olá **do serviço de aplicações** opção esquerda Olá da página Olá.

Clique no nome de Olá da sua aplicação que pretende que sejam tooconfigure Docker Hub a implementação contínua para.

No Olá **as definições de aplicação**, adicionar uma aplicação definição chamado `DOCKER_ENABLE_CI` com o valor de Olá `true`.

![Inserir uma imagem de definição de aplicação](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a>Passo 3 – Preparar o URL do Webhook

Pode obter utilizando o URL do Webhook Olá [CLI do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) e Olá os seguintes comandos a executar

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

Para o URL do Webhook Olá, terá de Olá toohave seguinte ponto final: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.

Pode obter o `publishingusername` e `publishingpwd` ao transferir a aplicação web de Olá publicar perfis com Olá portal do Azure.

![Inserir uma imagem de adição de webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a>Passo 4 – adicionar um hook de web

### <a name="azure-container-registry"></a>Registo de Contentores do Azure

No seu painel do portal de registo, clique em **Webhooks**, criar um novo webhook clicando **adicionar**. No Olá **criar o webhook** painel, dê um nome do webhook. Para o URI de Webhook Olá, terá de tooprovide Olá URL obtido a partir do **passo 3**

Certifique-se de que definir âmbito de Olá como Olá repositório que contém a imagem de contentor.

![Inserir uma imagem do webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

Quando a imagem de Olá for atualizada, aplicação web de Olá for atualizado automaticamente com a nova imagem de Olá.

### <a name="docker-hub"></a>Hub de docker

Na página do seu Hub de Docker, clique em **Webhooks**, em seguida, **WEBHOOK de A criar**.

![Inserir uma imagem de adição de webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

Para o URL do Webhook Olá, terá de tooprovide Olá URL obtida **passo 3**

![Inserir uma imagem de adição de webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

Quando a imagem de Olá for atualizada, aplicação web de Olá for atualizado automaticamente com a nova imagem de Olá.

## <a name="next-steps"></a>Passos seguintes
* [O que é a aplicação de Web do Azure no Linux?](./app-service-linux-intro.md)
* [Registo de contentor do Azure](https://azure.microsoft.com/en-us/services/container-registry/)
* [Utilizar a configuração de PM2 para Node.js na aplicação Web do Azure no Linux](app-service-linux-using-nodejs-pm2.md)
* [Utilizando o .NET Core na aplicação Web do Azure no Linux](app-service-linux-using-dotnetcore.md)
* [Utilizar Ruby na aplicação Web do Azure no Linux](app-service-linux-ruby-get-started.md)
* [Como toouse um Docker personalizado imagem para a aplicação de Web do Azure no Linux](./app-service-linux-using-custom-docker-image.md)
* [Aplicação de Web do App Service do Azure no Linux FAQ](./app-service-linux-faq.md) 
* [Gerir a aplicação Web no Linux utilizando o Azure CLI 2.0](./app-service-linux-cli.md)



