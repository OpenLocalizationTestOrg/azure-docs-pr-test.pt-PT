---
title: "funcionalidades de Shell de nuvem (pré-visualização) aaaAzure | Microsoft Docs"
description: "Descrição geral das funcionalidades de Shell de nuvem do Azure"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a><span data-ttu-id="0bfcb-103">Funcionalidades e ferramentas para a Shell de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="0bfcb-103">Features and Tools for Azure Cloud Shell</span></span>
<span data-ttu-id="0bfcb-104">Shell de nuvem do Azure é um toomanage de experiência de shell baseada no browser e desenvolver recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-104">Azure Cloud Shell is a browser-based shell experience toomanage and develop Azure resources.</span></span>

<span data-ttu-id="0bfcb-105">Shell de nuvem oferece um browser acessível, pré-configurados experiência de shell para gerir recursos do Azure sem a sobrecarga Olá de instalar, controlo de versões e manutenção de uma máquina por si.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-105">Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without hello overhead of installing, versioning, and maintaining a machine yourself.</span></span>

<span data-ttu-id="0bfcb-106">Shell de nuvem Aprovisiona máquinas numa base por pedido e como resultado o estado da máquina não serão mantidas entre sessões.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-106">Cloud Shell provisions machines on a per-request basis and as a result machine state will not persist across sessions.</span></span> <span data-ttu-id="0bfcb-107">Uma vez que a Shell de nuvem é criada para sessões interativas, shells terminam automaticamente após 20 minutos de inatividade de shell.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-107">Since Cloud Shell is built for interactive sessions, shells automatically terminate after 20 minutes of shell inactivity.</span></span>

## <a name="bash-in-cloud-shell"></a><span data-ttu-id="0bfcb-108">Bash na Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="0bfcb-108">Bash in Cloud Shell</span></span>
### <a name="tools"></a><span data-ttu-id="0bfcb-109">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="0bfcb-109">Tools</span></span>
|<span data-ttu-id="0bfcb-110">Categoria</span><span class="sxs-lookup"><span data-stu-id="0bfcb-110">Category</span></span>   |<span data-ttu-id="0bfcb-111">Nome</span><span class="sxs-lookup"><span data-stu-id="0bfcb-111">Name</span></span>   |
|---|---|
|<span data-ttu-id="0bfcb-112">Interpretador de shell do Linux</span><span class="sxs-lookup"><span data-stu-id="0bfcb-112">Linux shell interpreter</span></span>|<span data-ttu-id="0bfcb-113">Bash</span><span class="sxs-lookup"><span data-stu-id="0bfcb-113">Bash</span></span><br> <span data-ttu-id="0bfcb-114">partilhar</span><span class="sxs-lookup"><span data-stu-id="0bfcb-114">sh</span></span>               |
|<span data-ttu-id="0bfcb-115">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="0bfcb-115">Azure tools</span></span>            |<span data-ttu-id="0bfcb-116">[CLI do Azure 2.0](https://github.com/Azure/azure-cli) e [1.0](https://github.com/Azure/azure-xplat-cli)</span><span class="sxs-lookup"><span data-stu-id="0bfcb-116">[Azure CLI 2.0](https://github.com/Azure/azure-cli) and [1.0](https://github.com/Azure/azure-xplat-cli)</span></span><br> [<span data-ttu-id="0bfcb-117">AZCopy</span><span class="sxs-lookup"><span data-stu-id="0bfcb-117">AzCopy</span></span>](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [<span data-ttu-id="0bfcb-118">Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="0bfcb-118">Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)     |
|<span data-ttu-id="0bfcb-119">Editores de texto</span><span class="sxs-lookup"><span data-stu-id="0bfcb-119">Text editors</span></span>           |<span data-ttu-id="0bfcb-120">VIM</span><span class="sxs-lookup"><span data-stu-id="0bfcb-120">vim</span></span><br> <span data-ttu-id="0bfcb-121">Nano</span><span class="sxs-lookup"><span data-stu-id="0bfcb-121">nano</span></span><br> <span data-ttu-id="0bfcb-122">emacs</span><span class="sxs-lookup"><span data-stu-id="0bfcb-122">emacs</span></span>       |
|<span data-ttu-id="0bfcb-123">Controlo de código fonte</span><span class="sxs-lookup"><span data-stu-id="0bfcb-123">Source control</span></span>         |<span data-ttu-id="0bfcb-124">Git</span><span class="sxs-lookup"><span data-stu-id="0bfcb-124">git</span></span>                    |
|<span data-ttu-id="0bfcb-125">Ferramentas de compilação</span><span class="sxs-lookup"><span data-stu-id="0bfcb-125">Build tools</span></span>            |<span data-ttu-id="0bfcb-126">Certifique-</span><span class="sxs-lookup"><span data-stu-id="0bfcb-126">make</span></span><br> <span data-ttu-id="0bfcb-127">maven</span><span class="sxs-lookup"><span data-stu-id="0bfcb-127">maven</span></span><br> <span data-ttu-id="0bfcb-128">npm</span><span class="sxs-lookup"><span data-stu-id="0bfcb-128">npm</span></span><br> <span data-ttu-id="0bfcb-129">PIP</span><span class="sxs-lookup"><span data-stu-id="0bfcb-129">pip</span></span>         |
|<span data-ttu-id="0bfcb-130">Contentores</span><span class="sxs-lookup"><span data-stu-id="0bfcb-130">Containers</span></span>             |<span data-ttu-id="0bfcb-131">[CLI do docker](https://github.com/docker/cli)/[Docker máquina](https://github.com/docker/machine)</span><span class="sxs-lookup"><span data-stu-id="0bfcb-131">[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)</span></span><br> [<span data-ttu-id="0bfcb-132">Kubectl</span><span class="sxs-lookup"><span data-stu-id="0bfcb-132">Kubectl</span></span>](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [<span data-ttu-id="0bfcb-133">Rascunho</span><span class="sxs-lookup"><span data-stu-id="0bfcb-133">Draft</span></span>](https://github.com/Azure/draft)<br> [<span data-ttu-id="0bfcb-134">CLI DE DC/SO</span><span class="sxs-lookup"><span data-stu-id="0bfcb-134">DC/OS CLI</span></span>](https://github.com/dcos/dcos-cli)         |
|<span data-ttu-id="0bfcb-135">Bases de Dados</span><span class="sxs-lookup"><span data-stu-id="0bfcb-135">Databases</span></span>              |<span data-ttu-id="0bfcb-136">Cliente de MySQL</span><span class="sxs-lookup"><span data-stu-id="0bfcb-136">MySQL client</span></span><br> <span data-ttu-id="0bfcb-137">Cliente PostgreSql</span><span class="sxs-lookup"><span data-stu-id="0bfcb-137">PostgreSql client</span></span><br> [<span data-ttu-id="0bfcb-138">SQLCMD utilitário</span><span class="sxs-lookup"><span data-stu-id="0bfcb-138">sqlcmd Utility</span></span>](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [<span data-ttu-id="0bfcb-139">MSSQL scripter</span><span class="sxs-lookup"><span data-stu-id="0bfcb-139">mssql-scripter</span></span>](https://github.com/Microsoft/sql-xplat-cli) |
|<span data-ttu-id="0bfcb-140">Outros</span><span class="sxs-lookup"><span data-stu-id="0bfcb-140">Other</span></span>                  |<span data-ttu-id="0bfcb-141">iPython cliente</span><span class="sxs-lookup"><span data-stu-id="0bfcb-141">iPython Client</span></span><br> [<span data-ttu-id="0bfcb-142">Nuvem Foundry CLI</span><span class="sxs-lookup"><span data-stu-id="0bfcb-142">Cloud Foundry CLI</span></span>](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a><span data-ttu-id="0bfcb-143">Suporte de idiomas</span><span class="sxs-lookup"><span data-stu-id="0bfcb-143">Language support</span></span>
|<span data-ttu-id="0bfcb-144">Idioma</span><span class="sxs-lookup"><span data-stu-id="0bfcb-144">Language</span></span>   |<span data-ttu-id="0bfcb-145">Versão</span><span class="sxs-lookup"><span data-stu-id="0bfcb-145">Version</span></span>   |
|---|---|
|<span data-ttu-id="0bfcb-146">.NET</span><span class="sxs-lookup"><span data-stu-id="0bfcb-146">.NET</span></span>       |<span data-ttu-id="0bfcb-147">1.01</span><span class="sxs-lookup"><span data-stu-id="0bfcb-147">1.01</span></span>       |
|<span data-ttu-id="0bfcb-148">Ir</span><span class="sxs-lookup"><span data-stu-id="0bfcb-148">Go</span></span>         |<span data-ttu-id="0bfcb-149">1.7</span><span class="sxs-lookup"><span data-stu-id="0bfcb-149">1.7</span></span>        |
|<span data-ttu-id="0bfcb-150">Java</span><span class="sxs-lookup"><span data-stu-id="0bfcb-150">Java</span></span>       |<span data-ttu-id="0bfcb-151">1.8</span><span class="sxs-lookup"><span data-stu-id="0bfcb-151">1.8</span></span>        |
|<span data-ttu-id="0bfcb-152">Node.js</span><span class="sxs-lookup"><span data-stu-id="0bfcb-152">Node.js</span></span>    |<span data-ttu-id="0bfcb-153">6.9.4</span><span class="sxs-lookup"><span data-stu-id="0bfcb-153">6.9.4</span></span>      |
|<span data-ttu-id="0bfcb-154">Python</span><span class="sxs-lookup"><span data-stu-id="0bfcb-154">Python</span></span>     |<span data-ttu-id="0bfcb-155">2.7 e 3.5 (predefinição)</span><span class="sxs-lookup"><span data-stu-id="0bfcb-155">2.7 and 3.5 (default)</span></span>|

## <a name="secure-automatic-authentication"></a><span data-ttu-id="0bfcb-156">Autenticação automática segura</span><span class="sxs-lookup"><span data-stu-id="0bfcb-156">Secure automatic authentication</span></span>
<span data-ttu-id="0bfcb-157">Shell de nuvem e em segurança os automaticamente autentica o acesso de conta para Olá Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-157">Cloud Shell securely and automatically authenticates account access for hello Azure CLI 2.0.</span></span>

## <a name="azure-files-persistence"></a><span data-ttu-id="0bfcb-158">Persistência de ficheiros do Azure</span><span class="sxs-lookup"><span data-stu-id="0bfcb-158">Azure Files persistence</span></span>
<span data-ttu-id="0bfcb-159">Uma vez que a Shell de nuvem é atribuído numa base por pedido através de uma máquina temporária, ficheiros fora do Estado de $Home e a máquina não são mantidos entre sessões.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-159">Since Cloud Shell is allocated on a per-request basis using a temporary machine, files outside of your $Home and machine state are not persisted across sessions.</span></span>
<span data-ttu-id="0bfcb-160">ficheiros de toopersist entre sessões, Shell da nuvem explica como anexar um ficheiro do Azure através de partilha na primeira execução.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-160">toopersist files across sessions, Cloud Shell walks you through attaching an Azure file share on first launch.</span></span>
<span data-ttu-id="0bfcb-161">Uma vez concluída nuvem Shell ligará automaticamente o armazenamento para todas as futuras sessões.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-161">Once completed Cloud Shell will automatically attach your storage for all future sessions.</span></span>

[<span data-ttu-id="0bfcb-162">Saiba mais sobre a ligação de partilhas de ficheiros do Azure tooCloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0bfcb-162">Learn more about attaching Azure file shares tooCloud Shell.</span></span>](persisting-shell-storage.md)

## <a name="next-steps"></a><span data-ttu-id="0bfcb-163">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0bfcb-163">Next steps</span></span>
[<span data-ttu-id="0bfcb-164">Início rápido de Shell de nuvem</span><span class="sxs-lookup"><span data-stu-id="0bfcb-164">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="0bfcb-165">
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="0bfcb-165">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br>