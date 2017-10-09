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
# <a name="using-azure-container-registry-webhooks---azure-portal"></a>Utilizar webhooks de registo de contentor do Azure - portal do Azure

Um registo de contentor do Azure armazena e gere a imagens de contentor de Docker privadas, forma toohello semelhante Docker Hub armazena públicas imagens de Docker. Utilize webhooks tootrigger eventos quando determinadas ações ocorrer dos seus repositórios de registo. Webhooks pode responder tooevents ao nível de registo Olá ou podem ser confinados para baixo tooa etiquetas de repositório específico. 

Para obter mais em segundo plano e conceitos, consulte Olá [descrição geral](./container-registry-intro.md).

## <a name="prerequisites"></a>Pré-requisitos 

- O contentor do Azure gerida registo - criar um registo de contentor geridos na sua subscrição do Azure. Por exemplo, utilize Olá portal do Azure ou Olá Azure CLI 2.0. 
- Docker CLI - tooset cópia de segurança do computador local como uma Docker anfitrião e acesso Olá CLI do Docker comandos, instale o motor de Docker. 

## <a name="create-webhook-azure-portal"></a>Criar o webhook portal do Azure

1. Inicie sessão no toohello portal do Azure e navegue até o registo de toohello em que pretende toocreate webhooks. 

2. No painel do contentor de Olá, selecione o separador de "Webhooks" Olá. 

3. Selecione "Adicionar" na barra de ferramentas do Olá webhook painel. 

4. Olá concluída *criar o Webhook* formulário com Olá seguintes informações:

| Valor | Descrição |
|---|---|
| Nome | nome de Olá pretende toogive toohello webhook. Só pode conter letras minúsculas e números e entre 5 e 50 carateres. |
| URI do serviço | Olá URI onde Olá webhook deve enviar notificações de POST. |
| Cabeçalhos personalizados | Cabeçalhos que pretende toopass juntamente com o pedido POST Olá. Devem ser na "chave: valor" formato. |
| Ações de Acionador | Ações que acionam Olá webhook. Atualmente webhooks pode ser acionada por push e/ou eliminar ações tooan imagem. |
| Estado | Estado de Olá do webhook Olá depois de criado. Está ativada por predefinição. |
| Âmbito | âmbito de Olá no que funciona de webhook Olá. Por predefinição, o âmbito de Olá é para todos os eventos no registo de Olá. Pode ser especificado para um repositório ou uma tag utilizando o formato de Olá "repositório: tag". |

Formulário de webhook de exemplo:

![IU DCOS](./media/container-registry-webhook/webhook.png)

## <a name="create-webhook-azure-cli"></a>Criar o webhook CLI do Azure

toocreate utilizando um webhook Olá CLI do Azure, utilize Olá [az acr webhook criar](/cli/azure/acr/webhook#create) comando.

```azurecli-interactive
az acr webhook create --registry mycontainerregistry --name myacrwebhook01 --actions delete --uri http://webhookuri.com
```

## <a name="test-webhook"></a>Webhook de teste

### <a name="azure-portal"></a>Portal do Azure

Toousing anterior Olá webhook no contentor de push de imagem e eliminar ações, pode ser testada com Olá **Ping** botão. Quando utilizado, Olá Ping envia que um toohello de pedido de post genérico especificado ponto final e registos Olá resposta. Esta ação é útil tooverify Olá webhook foi configurado corretamente.

1. Selecione o webhook Olá pretende tootest. 
2. Na barra de ferramentas superior de Olá, selecione a ação de "um Ping" Olá. 
3. Verifique Olá pedido e resposta.

### <a name="azure-cli"></a>CLI do Azure

tootest um webhook ACR com Olá CLI do Azure, utilize Olá [ping de webhook az acr](/cli/azure/acr/webhook#ping) comando.

```azurecli-interactive
az acr webhook ping --registry mycontainerregistry --name myacrwebhook01
```

resultados de Olá toosee, utilize Olá [az acr webhook lista-eventos](/cli/azure/acr/webhook#list-events) comando. 

```azurecli-interactive
az acr webhook list-events --registry mycontainerregistry08 --name myacrwebhook01
```

## <a name="delete-webhook"></a>Eliminar o webhook

### <a name="azure-portal"></a>Portal do Azure

Cada webhook pode ser eliminado, selecionando Olá webhook e, em seguida, o botão para eliminar Olá no Olá portal do Azure.

### <a name="azure-cli"></a>CLI do Azure

```azurecli-interactive
az acr webhook delete --registry mycontainerregistry --name myacrwebhook01
```