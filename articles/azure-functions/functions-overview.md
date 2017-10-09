---
title: "Descrição geral das funções de aaaAzure | Microsoft Docs"
description: "Compreender como toouse das funções do Azure toooptimize cargas de trabalho assíncronas em minutos."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 01d6ca9f-ca3f-44fa-b0b9-7ffee115acd4
ms.service: functions
ms.devlang: multiple
ms.topic: overview
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 668f9055a007fee662a4c7ec774d3c0a1d847800
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-tooazure-functions"></a>Uma introdução tooAzure funciona  
As funções do Azure é uma solução para uma fácil execução de pequenos blocos de código, ou "funções", na nuvem de Olá. Pode escrever o código de Olá apenas que necessita para o problema de Olá em questão, sem se preocupar toorun de infraestrutura completa de aplicações ou Olá-lo. As funções podem tornar o desenvolvimento ainda mais produtivo, e podem utilizar uma linguagem de desenvolvimento à sua escolha, tal como C#, F#, Node.js, Python ou PHP. Só paga pelos tempo Olá que seu código é executado e confiar tooscale do Azure, conforme necessário. As Funções do Azure permitem desenvolver aplicações sem servidor no Microsoft Azure.

Este tópico fornece uma descrição geral de alto nível das Funções do Azure. Se pretender toojump direita em e começar a utilizar com as funções do Azure, comece por [criar a sua primeira função do Azure](functions-create-first-azure-function.md). Se estiver à procura de mais informações técnicas acerca das funções, consulte Olá [referência para programadores](functions-reference.md).

## <a name="features"></a>Funcionalidades
Seguem-se algumas funcionalidades-chave das Funções do Azure:

* **Escolha de idioma** - escreva funções com C#, F#, Node.js, Python, PHP, batch, bash ou qualquer executável.
* **Modelo de preços pagamento por utilização** - pague apenas para Olá o tempo despendido a executar o seu código. Consulte o alojamento de consumo de Olá planear opção na Olá [secção de preços](#pricing).  
* **Traga as suas próprias dependências** - As funções são compatíveis com NuGet e NPM, pelo que pode utilizar as suas bibliotecas favoritas.  
* **Segurança integrada** - Proteja as funções acionadas por HTTP com fornecedores de OAuth, como o Azure Active Directory, Facebook, Google, Twitter e Conta Microsoft.  
* **Integração simplificada** - Tire facilmente partido dos serviços do Azure e ofertas de software como serviço (SaaS). Consulte Olá [secção integrações](#integrations) para alguns exemplos.  
* **Desenvolvimento flexível** - Code o direito de funções no portal de Olá ou configurar a integração contínua e implemente o seu código através do GitHub, Visual Studio Team Services e de outras [ferramentas de programação suportadas](../app-service-web/web-sites-deploy.md#deploy-using-an-ide).  
* **Open source** -Olá funções runtime é open source e [está disponível no GitHub](https://github.com/azure/azure-webjobs-sdk-script).  

## <a name="what-can-i-do-with-functions"></a>O que posso fazer com as Funções?
As funções do Azure é uma excelente solução para processar dados, integrar sistemas, trabalhar com Olá internet das coisas (IoT) e a criação de API simples e micro-serviços. Considere utilizar as funções para tarefas como imagem ou processamento de ordem, manutenção de ficheiros ou para todas as tarefas que pretende que o toorun com base numa agenda. 

Funções fornece tooget modelos iniciado com cenários-chave, incluindo Olá seguinte:

* **BlobTrigger** -blobs de armazenamento do Azure de processo quando são adicionados toocontainers. Pode utilizar esta função para redimensionar a imagem.
* **EventHubTrigger** -responder tooevents entregar tooan Hub de eventos do Azure. É especialmente útil em cenários de instrumentação de aplicações, experiência do utilizador ou processamento de fluxo de trabalho e Internet das Coisas (IoT).
* **Webhook genérico** - Processar os pedidos de webhook HTTP a partir de qualquer serviço que suporte webhooks.
* **GitHub webhook** -tooevents respondeu que ocorrem nos seus repositórios do GitHub. Por exemplo, consulte o artigo [Criar um webhook ou uma função de API](functions-create-a-web-hook-or-api-function.md).
* **HTTPTrigger** -acionar a execução de Olá do seu código através da utilização de um pedido de HTTP.
* **QueueTrigger** -responder toomessages à medida que chegam numa fila de armazenamento do Azure. Por exemplo, consulte [criar uma função do Azure que está vinculado tooan serviço do Azure](functions-create-an-azure-connected-function.md).
* **ServiceBusQueueTrigger** -ligar o seu tooother código dos serviços do Azure ou serviços no local pelo serviço de escuta toomessage filas. 
* **Servicebusqueuetrigger** -ligar o seu tooother código dos serviços do Azure ou serviços no local ao subscrever tootopics. 
* **TimerTrigger** - Executar tarefas de limpeza ou outras tarefas de lote numa agenda predefinida. Por exemplo, consulte o artigo [Criar uma função de processamento de eventos](functions-create-an-event-processing-function.md).

Funções do Azure suporta *acionadores*, que são formas toostart execução do seu código, e *enlaces*, que é formas toosimplify codificação de dados de entrada e de saída. Para obter uma descrição detalhada dos acionadores Olá e enlaces das funções do Azure fornece, consulte [referência de para programadores de acionadores e enlaces das funções do Azure](functions-triggers-bindings.md).

## <a name="integrations"></a>ntegrações
Funções do Azure integra-se com vários serviços do Azure e de terceiros. Estes serviços podem acionar a sua função e iniciar a execução ou podem servir como entrada e saída para o seu código. Olá seguintes integrações de serviço é suportada funções do Azure. 

* Azure Cosmos DB
* Azure Event Hubs 
* Azure Mobile Apps (tabelas)
* Azure Notification Hubs
* Azure Service Bus (filas e tópicos)
* Armazenamento do Azure (blob, filas e tabelas) 
* GitHub (webhooks)
* No local (utilizando o Service Bus)
* Twilio (mensagens SMS)

## <a name="pricing"></a>Quanto custam as Funções?
As funções do Azure tem dois tipos de planos de preços, escolha Olá um que melhor se adequa às suas necessidades: 

* **Plano de consumo** - quando a função é executada, o Azure fornece todos os recursos informáticos necessários de Olá. Não tem tooworry sobre gestão de recursos, paga apenas para o tempo de Olá que executa o seu código. 
* **Plano do App Service** - Executar as suas funções, como aplicações da Web, telemóveis e API. Quando já estiver a utilizar o App Service para outras aplicações, pode executar as suas funções no Olá mesmo plano sem custos adicionais. 

Preços estão disponíveis no Olá [preços das funções](https://azure.microsoft.com/pricing/details/functions/). Para obter mais informações sobre como dimensionar as suas funções, consulte [como tooscale das funções do Azure](functions-scale.md).

## <a name="next-steps"></a>Passos Seguintes
* [Criar a sua primeira Função do Azure](functions-create-first-azure-function.md)  
  Avançar diretamente e criar a sua primeira função com o guia de introdução do Olá das funções do Azure. 
* [Referência para programadores das Funções do Azure](functions-reference.md)  
  Fornece mais informações técnicas sobre o tempo de execução do Olá das funções do Azure e uma referência para as funções de codificação e definição de acionadores e enlaces.
* [Testar as Funções do Azure](functions-test-a-function.md)  
  Descreve várias ferramentas e técnicas para testar as suas funções.
* [Como tooscale das funções do Azure](functions-scale.md)  
  Aborda os planos de serviço disponíveis com as funções do Azure, incluindo o plano de alojamento de consumo de Olá e como toochoose Olá plano adequado. 
* [Saiba mais sobre o Azure App Service](../app-service/app-service-value-prop-what-is.md)  
  As funções do Azure tira partido da plataforma do App Service do Azure Olá para funcionalidades essenciais como implementações, variáveis de ambiente e diagnósticos. 

