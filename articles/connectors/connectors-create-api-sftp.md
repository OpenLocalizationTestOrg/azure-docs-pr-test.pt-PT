---
title: "aaaLearn como toouse Olá conector SFTP nas suas logic apps | Microsoft Docs"
description: "Crie aplicações lógicas com o App service do Azure. Ligue toosend tooSFTP API e receber ficheiros. Pode realizar várias operações, tais como criar, atualizar, obterem ou eliminar ficheiros."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="a21cb-105">Introdução ao conector do Olá SFTP</span><span class="sxs-lookup"><span data-stu-id="a21cb-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="a21cb-106">Utilize Olá SFTP conector tooaccess um SFTP conta toosend e receber ficheiros.</span><span class="sxs-lookup"><span data-stu-id="a21cb-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="a21cb-107">Pode realizar várias operações, tais como criar, atualizar, obterem ou eliminar ficheiros.</span><span class="sxs-lookup"><span data-stu-id="a21cb-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="a21cb-108">toouse [qualquer conector](apis-list.md), terá primeiro de toocreate uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="a21cb-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="a21cb-109">Pode começar a utilizar pelo [criar uma aplicação lógica agora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a21cb-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="a21cb-110">Ligar tooSFTP</span><span class="sxs-lookup"><span data-stu-id="a21cb-110">Connect tooSFTP</span></span>
<span data-ttu-id="a21cb-111">Antes da aplicação lógica pode aceder a qualquer serviço, terá primeiro de toocreate um *ligação* toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="a21cb-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="a21cb-112">A [ligação](connectors-overview.md) fornece conectividade entre uma aplicação lógica e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="a21cb-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="a21cb-113">Criar uma ligação tooSFTP</span><span class="sxs-lookup"><span data-stu-id="a21cb-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="a21cb-114">Utilizar um acionador SFTP</span><span class="sxs-lookup"><span data-stu-id="a21cb-114">Use an SFTP trigger</span></span>
<span data-ttu-id="a21cb-115">Um acionador é um evento que pode ser o fluxo de trabalho do Olá toostart utilizados definido numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="a21cb-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="a21cb-116">[Saiba mais sobre acionadores](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a21cb-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="a21cb-117">Neste exemplo, Olá **SFTP - quando um ficheiro é adicionado ou modificado** acionador é um fluxo de trabalho de aplicação de lógica de tooinitiate utilizado quando um ficheiro é adicionado ou modificado num servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="a21cb-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="a21cb-118">Também adicionar uma condição que verifica a existência de conteúdo de Olá do ficheiro de novos ou modificados Olá e faz com que um ficheiro de Olá tooextract decisão se o seu conteúdo indicarem que deve ser extraído antes de utilizar conteúdo Olá.</span><span class="sxs-lookup"><span data-stu-id="a21cb-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="a21cb-119">Por fim, adicionar uma ação tooextract Olá do conteúdo de um ficheiro e coloque o conteúdo de Olá extraído numa pasta no servidor SFTP Olá.</span><span class="sxs-lookup"><span data-stu-id="a21cb-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="a21cb-120">Um exemplo de empresa, pode utilizar este toomonitor acionador uma pasta SFTP para novos ficheiros que representam as ordens de cliente.</span><span class="sxs-lookup"><span data-stu-id="a21cb-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="a21cb-121">Pode, em seguida, utilizar uma ação de conector SFTP, tais como **obter o conteúdo do ficheiro**, conteúdo de Olá tooget da ordem de Olá para armazenamento numa base de dados ordens e processamento adicional.</span><span class="sxs-lookup"><span data-stu-id="a21cb-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="a21cb-122">Adicionar uma condição</span><span class="sxs-lookup"><span data-stu-id="a21cb-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="a21cb-123">Utilizar uma ação de SFTP</span><span class="sxs-lookup"><span data-stu-id="a21cb-123">Use an SFTP action</span></span>
<span data-ttu-id="a21cb-124">Uma ação é uma operação levada a cabo pelo fluxo de trabalho Olá definido numa aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="a21cb-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="a21cb-125">[Saiba mais sobre as ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a21cb-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="a21cb-126">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="a21cb-126">Connector-specific details</span></span>

<span data-ttu-id="a21cb-127">Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="a21cb-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="a21cb-128">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="a21cb-128">More connectors</span></span>
<span data-ttu-id="a21cb-129">Voltar atrás toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a21cb-129">Go back toohello [APIs list](apis-list.md).</span></span>
