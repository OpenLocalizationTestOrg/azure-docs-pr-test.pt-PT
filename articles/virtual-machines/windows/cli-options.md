---
title: "Olá aaaUsing CLI do Azure no Windows | Microsoft Docs"
description: "Utilizar Olá CLI do Azure no Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a><span data-ttu-id="c17ee-103">Utilizar Olá CLI do Azure no Windows</span><span class="sxs-lookup"><span data-stu-id="c17ee-103">Using hello Azure CLI on Windows</span></span>

<span data-ttu-id="c17ee-104">Olá Interface de linha de comandos do Azure (CLI) fornece uma linha de comandos e o ambiente de script para criar e gerir recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c17ee-104">hello Azure Command Line Interface (CLI) provides a command line and scripting environment for creating and managing Azure resources.</span></span> <span data-ttu-id="c17ee-105">Olá CLI do Azure está disponível para macOS, Linux e sistemas operativos Windows.</span><span class="sxs-lookup"><span data-stu-id="c17ee-105">hello Azure CLI is available for macOS, Linux, and Windows operating systems.</span></span> <span data-ttu-id="c17ee-106">Entre estes sistemas operativos, comandos da CLI Olá são idênticos, no entanto, a sintaxe de scripting específicos de sistema operativo pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="c17ee-106">Across these operating systems, hello CLI commands are identical, however operating system specific scripting syntax can differ.</span></span>

<span data-ttu-id="c17ee-107">Estes documento detalhes Olá formas Olá CLI do Azure podem ser instaladas e executadas no Windows detalhes syntactical as considerações de e para cada.</span><span class="sxs-lookup"><span data-stu-id="c17ee-107">This document details hello ways that hello Azure CLI can be installed and run on Windows and details syntactical considerations for each.</span></span> <span data-ttu-id="c17ee-108">Para aprofundada CLI do Azure documentação, consulte [documentação da CLI do Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c17ee-108">For in-depth Azure CLI documentation see, [Azure CLI documentation]( https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="windows-subsystem-for-linux"></a><span data-ttu-id="c17ee-109">Subsistema Windows para Linux</span><span class="sxs-lookup"><span data-stu-id="c17ee-109">Windows Subsystem for Linux</span></span>

<span data-ttu-id="c17ee-110">Olá subsistema Windows para Linux (WSL) fornece um ambiente de Ubuntu Linux aniversário do Windows 10 e edições posteriores.</span><span class="sxs-lookup"><span data-stu-id="c17ee-110">hello Windows Subsystem for Linux (WSL) provides an Ubuntu Linux environment on Windows 10 Anniversary and later editions.</span></span> <span data-ttu-id="c17ee-111">Quando ativada, WSL fornece uma experiência de Bash nativa, o que pode ser utilizada para criar e executar scripts da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c17ee-111">When enabled, WSL provides a native Bash experience, which can be used for creating and running Azure CLI scripts.</span></span> <span data-ttu-id="c17ee-112">Porque WSL fornece uma experiência de Bash nativa, os scripts da CLI do Azure podem ser partilhados entre macOS, Linux e Windows sem modificação.</span><span class="sxs-lookup"><span data-stu-id="c17ee-112">Because WSL provides a native Bash experience, Azure CLI scripts can be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="c17ee-113">toouse Olá CLI do Azure no WSL, conclua os seguintes Olá.</span><span class="sxs-lookup"><span data-stu-id="c17ee-113">toouse hello Azure CLI in WSL, complete hello following.</span></span>

|<span data-ttu-id="c17ee-114">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c17ee-114">Task</span></span> | <span data-ttu-id="c17ee-115">Instruções</span><span class="sxs-lookup"><span data-stu-id="c17ee-115">Instructions</span></span> |
|---|---|
| <span data-ttu-id="c17ee-116">Ativar WSL</span><span class="sxs-lookup"><span data-stu-id="c17ee-116">Enable WSL</span></span> | [<span data-ttu-id="c17ee-117">Instalar documentação WSL</span><span class="sxs-lookup"><span data-stu-id="c17ee-117">Install WSL documentation </span></span>](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| <span data-ttu-id="c17ee-118">Instalar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c17ee-118">Install hello Azure CLI</span></span> |[<span data-ttu-id="c17ee-119">Instalar Olá CLI no WSL/Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="c17ee-119">Install hello CLI on WSL/Ubuntu 14.04</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a><span data-ttu-id="c17ee-120">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c17ee-120">PowerShell</span></span>

<span data-ttu-id="c17ee-121">Olá CLI do Azure pode ser executada nativamente no Windows.</span><span class="sxs-lookup"><span data-stu-id="c17ee-121">hello Azure CLI can be run natively in Windows.</span></span> <span data-ttu-id="c17ee-122">Nesta configuração, pacote da CLI do Azure de Olá está instalado no sistema de operativo do Windows hello e comandos podem ser executados a partir do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c17ee-122">In this configuration, hello Azure CLI package is installed on hello Windows operating system, and commands can be run from PowerShell.</span></span> <span data-ttu-id="c17ee-123">Nesta configuração, scripts e comandos da CLI do Azure podem ser executados em qualquer versão suportada do Windows, no entanto, não é necessária sintaxe de scripting específicas de plataforma.</span><span class="sxs-lookup"><span data-stu-id="c17ee-123">In this configuration, Azure CLI commands and scripts can be run on any supported version of Windows, however platform specific scripting syntax is required.</span></span> <span data-ttu-id="c17ee-124">Por este motivo, scripts não não necessariamente ser partilhados entre macOS, Linux e Windows sem modificação.</span><span class="sxs-lookup"><span data-stu-id="c17ee-124">Because of this, scripts cannot necessarily be shared between macOS, Linux, and Windows without modification.</span></span>

<span data-ttu-id="c17ee-125">Olá toouse CLI do Azure no Windows, instale o pacote de Olá utilizar estas instruções, [instalação Olá CLI no Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span><span class="sxs-lookup"><span data-stu-id="c17ee-125">toouse hello Azure CLI on Windows, install hello package using these instructions, [Install hello CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).</span></span>

## <a name="docker-image"></a><span data-ttu-id="c17ee-126">Imagem de docker</span><span class="sxs-lookup"><span data-stu-id="c17ee-126">Docker Image</span></span>

<span data-ttu-id="c17ee-127">Ao utilizar o Docker para Windows, pode ser iniciada uma imagem de Docker que inclui Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c17ee-127">When using Docker for Windows, a Docker image can be started that includes hello Azure CLI.</span></span> <span data-ttu-id="c17ee-128">Esta imagem baseia-se remotas Linux e inclui uma experiência nativa do Bash.</span><span class="sxs-lookup"><span data-stu-id="c17ee-128">This image is based off of Linux, and includes a native Bash experience.</span></span>  <span data-ttu-id="c17ee-129">Ao utilizar o Docker para Windows e a imagem da CLI do Azure de Olá, toobe scripts partilhado entre macOS, Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="c17ee-129">When using Docker for Windows and hello Azure CLI image, scripts toobe shared between macOS, Linux, and Windows.</span></span> 

<span data-ttu-id="c17ee-130">Olá toouse CLI do Azure no Docker para Windows, certifique-se de que Docker para Windows está em execução e execute Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="c17ee-130">toouse hello Azure CLI on Docker for Windows, ensure that Docker for Windows is running and run hello following command.</span></span>

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

<span data-ttu-id="c17ee-131">Depois de concluído, um Bash será de início de sessão que é pré-carregado com ferramentas da CLI do Azure de Olá.</span><span class="sxs-lookup"><span data-stu-id="c17ee-131">Once completed, a Bash session will start that is preloaded with hello Azure CLI tools.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c17ee-132">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="c17ee-132">Next Steps</span></span>

[<span data-ttu-id="c17ee-133">Exemplo CLI para máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="c17ee-133">CLI sample for Azure virtual machines</span></span>](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="c17ee-134">Exemplos da CLI para Web Apps do Azure</span><span class="sxs-lookup"><span data-stu-id="c17ee-134">CLI samples for Azure Web Apps</span></span>](../../app-service-web/app-service-cli-samples.md)

[<span data-ttu-id="c17ee-135">Exemplos da CLI para SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="c17ee-135">CLI samples for Azure SQL</span></span>](../../sql-database/sql-database-cli-samples.md)
