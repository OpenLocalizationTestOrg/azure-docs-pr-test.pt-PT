---
title: "janela do aaaUsing Olá Shell de nuvem do Azure (pré-visualização) | Microsoft Docs"
description: "Janela de Shell de nuvem do Azure Olá de instruções."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="67d83-103">Utilizando Olá janela da Shell de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="67d83-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="67d83-104">Este documento explica como toouse Olá janela da Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="67d83-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="67d83-105">Sessões simultâneas</span><span class="sxs-lookup"><span data-stu-id="67d83-105">Concurrent sessions</span></span>
<span data-ttu-id="67d83-106">Shell de nuvem permite várias sessões em simultâneo em separadores de browser, permitindo tooexist cada sessão como um processo de Bash separado.</span><span class="sxs-lookup"><span data-stu-id="67d83-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="67d83-107">Se sair com uma sessão, não se esqueça de tooexit cada janela de sessão como cada processo é executado independentemente embora são executadas em Olá mesma máquina.</span><span class="sxs-lookup"><span data-stu-id="67d83-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="67d83-108">Reiniciar o Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="67d83-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="67d83-109">Reiniciar o Shell de nuvem irá repor o estado da máquina e todos os ficheiros não persistentes ao seu ficheiro partilha serão perdida.</span><span class="sxs-lookup"><span data-stu-id="67d83-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="67d83-110">Clique Olá reinício ícone na barra de ferramentas de Olá tooreceive um novo ambiente de nuvem Shell.</span><span class="sxs-lookup"><span data-stu-id="67d83-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="67d83-111">Minimizar & maximize a janela da Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="67d83-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="67d83-112">Clique em Olá minimizar ícone na Olá principais direita da Olá janela toohide-lo.</span><span class="sxs-lookup"><span data-stu-id="67d83-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="67d83-113">Clique novamente Olá ícone de nuvem Shell toounhide.</span><span class="sxs-lookup"><span data-stu-id="67d83-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="67d83-114">Clique em Olá maximizar a altura do ícone tooset janela toomax.</span><span class="sxs-lookup"><span data-stu-id="67d83-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="67d83-115">toorestore janela tooprevious tamanho, clique em restaurar.</span><span class="sxs-lookup"><span data-stu-id="67d83-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="67d83-116">Copiar e colar</span><span class="sxs-lookup"><span data-stu-id="67d83-116">Copy and paste</span></span>
* <span data-ttu-id="67d83-117">Windows: `Ctrl-insert` toocopy e `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="67d83-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="67d83-118">Contexto pendente, também pode ativar copiar/colar.</span><span class="sxs-lookup"><span data-stu-id="67d83-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="67d83-119">FireFox/IE podem não suportar corretamente as permissões da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="67d83-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="67d83-120">Mac OS: `Cmd-c` toocopy e `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="67d83-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="67d83-121">Contexto pendente, também pode ativar copiar/colar.</span><span class="sxs-lookup"><span data-stu-id="67d83-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="67d83-122">Redimensionar a janela da Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="67d83-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="67d83-123">Clique e arraste o limite superior de Olá da barra de ferramentas Olá ou reduzir verticalmente a janela do tooresize Olá Shell da nuvem.</span><span class="sxs-lookup"><span data-stu-id="67d83-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="67d83-124">Deslocamento apresentação de texto</span><span class="sxs-lookup"><span data-stu-id="67d83-124">Scrolling text display</span></span>
* <span data-ttu-id="67d83-125">Desloque-se com o rato ou touchpad toomove terminal texto a.</span><span class="sxs-lookup"><span data-stu-id="67d83-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="67d83-126">Comando de saída</span><span class="sxs-lookup"><span data-stu-id="67d83-126">Exit command</span></span>
<span data-ttu-id="67d83-127">Executar `exit` termina a sessão ativa de Olá.</span><span class="sxs-lookup"><span data-stu-id="67d83-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="67d83-128">Este comportamento ocorre por predefinição, passados 20 minutos, sem interação do.</span><span class="sxs-lookup"><span data-stu-id="67d83-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67d83-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="67d83-129">Next steps</span></span>
[<span data-ttu-id="67d83-130">Início rápido de Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="67d83-130">Cloud Shell Quickstart</span></span>](quickstart.md)
