---
title: "as políticas de acesso do aaaData informações de séries de tempo do Azure | Microsoft Docs"
description: "Neste tutorial, aprende toomanage políticas de acesso de dados no Insights de séries de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="4e714-103">Conceder acesso tooa Insights de séries de tempo ambiente do dados através do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4e714-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="4e714-104">Os ambientes do Time Series Insights têm dois tipos de políticas de acesso independentes:</span><span class="sxs-lookup"><span data-stu-id="4e714-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="4e714-105">Políticas de acesso de gestão</span><span class="sxs-lookup"><span data-stu-id="4e714-105">Management access policies</span></span>
* <span data-ttu-id="4e714-106">Políticas de acesso a dados</span><span class="sxs-lookup"><span data-stu-id="4e714-106">Data access policies</span></span>

<span data-ttu-id="4e714-107">Ambas as políticas concedem aos principais (utilizadores e aplicações) do Azure Active Directory várias permissões num determinado ambiente.</span><span class="sxs-lookup"><span data-stu-id="4e714-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="4e714-108">Olá principais (utilizadores e aplicações) têm de pertencer toohello active directory (ou "Inquilino do Azure") associado à subscrição Olá que contém o ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e714-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="4e714-109">Políticas de gestão de acesso conceder configuração toohello relacionados de permissões de ambiente de Olá, tais como</span><span class="sxs-lookup"><span data-stu-id="4e714-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="4e714-110">Criação e eliminação do ambiente de Olá, origens de eventos, referenciam conjuntos de dados, e</span><span class="sxs-lookup"><span data-stu-id="4e714-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="4e714-111">Gestão de políticas de acesso de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e714-111">Management of hello data access policies.</span></span>

<span data-ttu-id="4e714-112">Políticas de acesso de dados conceder permissões tooissue as consultas de dados, manipular dados de referência no ambiente de Olá e partilham consultas guardadas e perspetivas associadas Olá ambiente.</span><span class="sxs-lookup"><span data-stu-id="4e714-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="4e714-113">dois tipos de Olá das políticas permitem clara separação entre a gestão de toohello de acesso de ambiente de Olá e aceder a dados toohello Olá ambiente.</span><span class="sxs-lookup"><span data-stu-id="4e714-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="4e714-114">Por exemplo, é possível toosetup um ambiente que Olá proprietário/criador de ambiente de Olá é removido do acesso a dados Olá.</span><span class="sxs-lookup"><span data-stu-id="4e714-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="4e714-115">Bem como os utilizadores e serviços que são permitidos dados tooread do ambiente de Olá não pode ser concedido nenhuma configuração de toohello de acesso de ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e714-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="4e714-116">Conceder acesso a dados</span><span class="sxs-lookup"><span data-stu-id="4e714-116">Grant data access</span></span>
<span data-ttu-id="4e714-117">Olá passos seguintes mostram como toogrant de acesso aos dados para um principal de utilizador:</span><span class="sxs-lookup"><span data-stu-id="4e714-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="4e714-118">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e714-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="4e714-119">Clique em "Todos os recursos" no menu de Olá no lado esquerdo do Olá da Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e714-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="4e714-120">Selecione o seu ambiente do Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="4e714-120">Select your Time Series Insights environment.</span></span>

  ![Gerir a origem de informações de séries de tempo de Olá - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="4e714-122">Selecione "Acesso do Plano de Dados", clique em "Adicionar"</span><span class="sxs-lookup"><span data-stu-id="4e714-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Gerir a origem de informações de séries de tempo de Olá – adicionar](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="4e714-124">Clique em "Selecionar utilizador".</span><span class="sxs-lookup"><span data-stu-id="4e714-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="4e714-125">Procure e selecione o utilizador por correio eletrónico de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e714-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="4e714-126">Clique em “Selecionar”, no painel “Selecionar Utilizador”.</span><span class="sxs-lookup"><span data-stu-id="4e714-126">Click “Select” in “Select User” blade.</span></span>

  ![Gerir a origem de informações de séries de tempo de Olá - selecionar utilizador](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="4e714-128">Clique em “Selecionar função”.</span><span class="sxs-lookup"><span data-stu-id="4e714-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="4e714-129">Se pretender que os dados de referência do tooallow utilizador toochange e partilhar consultas guardadas e perspetivas com outros utilizadores do ambiente de Olá, selecione "Contribuinte".</span><span class="sxs-lookup"><span data-stu-id="4e714-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="4e714-130">Caso contrário, selecione "Leitor" tooallow utilizador consultar os dados no ambiente de Olá e guarde consultas de (não partilhadas) pessoais no ambiente de Olá.</span><span class="sxs-lookup"><span data-stu-id="4e714-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="4e714-131">Clique em "Ok" no painel do Olá "Selecionar função".</span><span class="sxs-lookup"><span data-stu-id="4e714-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Gerir a origem de informações de séries de tempo de Olá - selecionar função](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="4e714-133">Clique em "Ok" no painel do Olá "Selecionar função de utilizador".</span><span class="sxs-lookup"><span data-stu-id="4e714-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="4e714-134">Deverá ver:</span><span class="sxs-lookup"><span data-stu-id="4e714-134">You should see:</span></span>

  ![Gerir a origem de informações de séries de tempo de Olá - resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="4e714-136">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4e714-136">Next steps</span></span>

* [<span data-ttu-id="4e714-137">Criar uma origem de eventos</span><span class="sxs-lookup"><span data-stu-id="4e714-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="4e714-138">[Enviar eventos](time-series-insights-send-events.md) toohello origem de evento</span><span class="sxs-lookup"><span data-stu-id="4e714-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="4e714-139">Ver o seu ambiente no [Portal do Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4e714-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
