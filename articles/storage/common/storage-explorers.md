---
title: aaaTools para trabalhar com o Storage do Azure | Microsoft Docs
description: Uma lista das ferramentas que permitem-lhe tooview/interagir com os seus dados de armazenamento do Azure.
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 3308de2153099a05a676ab1d76426bd932e8a96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="ac5b4-103">Ferramentas de Cliente do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ac5b4-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="ac5b4-104">Os utilizadores do Storage do Azure com frequência pretendem toobe capaz de tooview/interagir com os dados utilizando uma ferramenta de cliente do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-104">Users of Azure Storage frequently want toobe able tooview/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="ac5b4-105">Nas tabelas de Olá abaixo, iremos lista várias ferramentas que permitem-lhe toodo isto.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-105">In hello tables below, we list a number of tools that allow you toodo this.</span></span> <span data-ttu-id="ac5b4-106">Vamos colocar um "X" em cada bloco se fornece a capacidade de Olá tooeither enumerar e/ou aceder a abstração do Olá dados.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-106">We put an "X" in each block if it provides hello ability tooeither enumerate and/or access hello data abstraction.</span></span> <span data-ttu-id="ac5b4-107">tabela de Olá também mostra as ferramentas de Olá estiver livre ou não.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-107">hello table also shows if hello tools is free or not.</span></span> <span data-ttu-id="ac5b4-108">"Versão de avaliação" indica que existe uma versão de avaliação gratuita, mas completa do produto Olá não é gratuita.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-108">"Trial" indicates that there is a free trial, but hello full product is not free.</span></span> <span data-ttu-id="ac5b4-109">"Y/N" indica que está disponível uma versão gratuitamente, enquanto está disponível para comprar uma versão diferente.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="ac5b4-110">Só fornecemos um instantâneo de ferramentas de cliente de armazenamento do Azure Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-110">We've only provided a snapshot of hello available Azure Storage client tools.</span></span> <span data-ttu-id="ac5b4-111">Estas ferramentas podem continuar tooevolve e aumentar a funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-111">These tools may continue tooevolve and grow in functionality.</span></span> <span data-ttu-id="ac5b4-112">Se existirem atualizações ou correções, deixe uma toolet comentário-nos.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-112">If there are corrections or updates, please leave a comment toolet us know.</span></span> <span data-ttu-id="ac5b4-113">Olá mesmo se aplica se sabe das ferramentas que aparece aqui toobe - teria de ser satisfeito tooadd-los.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-113">hello same is true if you know of tools that ought toobe here - we'd be happy tooadd them.</span></span>

<span data-ttu-id="ac5b4-114">**Ferramentas de cliente de armazenamento do Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="ac5b4-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="ac5b4-115">Ferramenta de cliente do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="ac5b4-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-116">Blob de bloco</span><span class="sxs-lookup"><span data-stu-id="ac5b4-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-117">Blob de página</span><span class="sxs-lookup"><span data-stu-id="ac5b4-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-118">Blob de acréscimo</span><span class="sxs-lookup"><span data-stu-id="ac5b4-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-119">Tabelas</span><span class="sxs-lookup"><span data-stu-id="ac5b4-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-120">Filas</span><span class="sxs-lookup"><span data-stu-id="ac5b4-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-121">Ficheiros</span><span class="sxs-lookup"><span data-stu-id="ac5b4-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-122">Gratuito</span><span class="sxs-lookup"><span data-stu-id="ac5b4-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="ac5b4-123">Plataforma</span><span class="sxs-lookup"><span data-stu-id="ac5b4-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-124">Web</span><span class="sxs-lookup"><span data-stu-id="ac5b4-124">Web</span></span></td>
    <td><span data-ttu-id="ac5b4-125">Windows</span><span class="sxs-lookup"><span data-stu-id="ac5b4-125">Windows</span></span></td>
    <td><span data-ttu-id="ac5b4-126">OSX</span><span class="sxs-lookup"><span data-stu-id="ac5b4-126">OSX</span></span></td>
    <td><span data-ttu-id="ac5b4-127">Linux</span><span class="sxs-lookup"><span data-stu-id="ac5b4-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-128"><a href="https://azure.microsoft.com/features/azure-portal/">Portal do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="ac5b4-129">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-129">X</span></span></td>
    <td><span data-ttu-id="ac5b4-130">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-130">X</span></span></td>
    <td><span data-ttu-id="ac5b4-131">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-131">X</span></span></td>
    <td><span data-ttu-id="ac5b4-132">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-132">X</span></span></td>
    <td><span data-ttu-id="ac5b4-133">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-133">X</span></span></td>
    <td><span data-ttu-id="ac5b4-134">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-134">X</span></span></td>
    <td><span data-ttu-id="ac5b4-135">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-135">Y</span></span></td>
    <td><span data-ttu-id="ac5b4-136">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-137"><a href="http://storageexplorer.com/">Explorador de Armazenamento do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-138">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-138">X</span></span></td>
    <td><span data-ttu-id="ac5b4-139">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-139">X</span></span></td>
    <td><span data-ttu-id="ac5b4-140">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-140">X</span></span></td>
    <td><span data-ttu-id="ac5b4-141">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-141">X</span></span></td>
    <td><span data-ttu-id="ac5b4-142">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-142">X</span></span></td>
    <td><span data-ttu-id="ac5b4-143">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-143">X</span></span></td>
    <td><span data-ttu-id="ac5b4-144">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-145">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-145">X</span></span></td>
    <td><span data-ttu-id="ac5b4-146">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-146">X</span></span></td>
    <td><span data-ttu-id="ac5b4-147">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Explorador de servidores do Microsoft Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-149">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-149">X</span></span></td>
    <td><span data-ttu-id="ac5b4-150">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-150">X</span></span></td>
    <td><span data-ttu-id="ac5b4-151">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-151">X</span></span></td>
    <td><span data-ttu-id="ac5b4-152">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-152">X</span></span></td>
    <td><span data-ttu-id="ac5b4-153">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-154">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-155">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="ac5b4-156">**Ferramentas de cliente do Storage do Azure de terceiros**</span><span class="sxs-lookup"><span data-stu-id="ac5b4-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="ac5b4-157">Não tiver verificado a funcionalidade de Olá ou qualidade reivindicados pelo Olá seguintes ferramentas de terceiros e as respetivas listagem não implica um endossamento pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ac5b4-157">We have not verified hello functionality or quality claimed by hello following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="ac5b4-158">Ferramenta de cliente do Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="ac5b4-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-159">Blob de bloco</span><span class="sxs-lookup"><span data-stu-id="ac5b4-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-160">Blob de página</span><span class="sxs-lookup"><span data-stu-id="ac5b4-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-161">Blob de acréscimo</span><span class="sxs-lookup"><span data-stu-id="ac5b4-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-162">Tabelas</span><span class="sxs-lookup"><span data-stu-id="ac5b4-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-163">Filas</span><span class="sxs-lookup"><span data-stu-id="ac5b4-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-164">Ficheiros</span><span class="sxs-lookup"><span data-stu-id="ac5b4-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="ac5b4-165">Gratuito</span><span class="sxs-lookup"><span data-stu-id="ac5b4-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="ac5b4-166">Plataforma</span><span class="sxs-lookup"><span data-stu-id="ac5b4-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-167">Web</span><span class="sxs-lookup"><span data-stu-id="ac5b4-167">Web</span></span></td>
    <td><span data-ttu-id="ac5b4-168">Windows</span><span class="sxs-lookup"><span data-stu-id="ac5b4-168">Windows</span></span></td>
    <td><span data-ttu-id="ac5b4-169">OSX</span><span class="sxs-lookup"><span data-stu-id="ac5b4-169">OSX</span></span></td>
    <td><span data-ttu-id="ac5b4-170">Linux</span><span class="sxs-lookup"><span data-stu-id="ac5b4-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-171"><a href="http://www.cloudportam.com/">Portam de nuvem</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="ac5b4-172">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-172">X</span></span></td>
    <td><span data-ttu-id="ac5b4-173">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-173">X</span></span></td>
    <td><span data-ttu-id="ac5b4-174">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-174">X</span></span></td>
    <td><span data-ttu-id="ac5b4-175">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-175">X</span></span></td>
    <td><span data-ttu-id="ac5b4-176">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-176">X</span></span></td>
    <td><span data-ttu-id="ac5b4-177">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-177">X</span></span></td>
    <td><span data-ttu-id="ac5b4-178">Avaliação</span><span class="sxs-lookup"><span data-stu-id="ac5b4-178">Trial</span></span></td>
    <td><span data-ttu-id="ac5b4-179">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: O Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="ac5b4-181">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-181">X</span></span></td>
    <td><span data-ttu-id="ac5b4-182">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-182">X</span></span></td>
    <td><span data-ttu-id="ac5b4-183">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-183">X</span></span></td>
    <td><span data-ttu-id="ac5b4-184">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-184">X</span></span></td>
    <td><span data-ttu-id="ac5b4-185">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-185">X</span></span></td>
    <td><span data-ttu-id="ac5b4-186">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-186">X</span></span></td>
    <td><span data-ttu-id="ac5b4-187">Avaliação</span><span class="sxs-lookup"><span data-stu-id="ac5b4-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-188">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Explorador do Azure</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-190">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-190">X</span></span></td>
    <td><span data-ttu-id="ac5b4-191">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-191">X</span></span></td>
    <td><span data-ttu-id="ac5b4-192">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-193">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-193">X</span></span></td>
    <td><span data-ttu-id="ac5b4-194">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-195">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Explorador do Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-197">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-197">X</span></span></td>
    <td><span data-ttu-id="ac5b4-198">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-199">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-199">X</span></span></td>
    <td><span data-ttu-id="ac5b4-200">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-201">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-202">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">Explorador de cloudBerry</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-204">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-204">X</span></span></td>
    <td><span data-ttu-id="ac5b4-205">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-206">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-206">X</span></span></td>
    <td><span data-ttu-id="ac5b4-207">Y/N</span><span class="sxs-lookup"><span data-stu-id="ac5b4-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-208">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-209"><a href="http://www.gapotchenko.com/cloudcombine">Combinação de nuvem</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="ac5b4-210">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-210">X</span></span></td>
    <td><span data-ttu-id="ac5b4-211">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-212">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-212">X</span></span></td>
    <td><span data-ttu-id="ac5b4-213">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-214">Avaliação</span><span class="sxs-lookup"><span data-stu-id="ac5b4-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-215">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-217">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-217">X</span></span></td>
    <td><span data-ttu-id="ac5b4-218">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-218">X</span></span></td>
    <td><span data-ttu-id="ac5b4-219">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-219">X</span></span></td>
    <td><span data-ttu-id="ac5b4-220">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-220">X</span></span></td>
    <td><span data-ttu-id="ac5b4-221">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-221">X</span></span></td>
    <td><span data-ttu-id="ac5b4-222">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-222">X</span></span></td>
    <td><span data-ttu-id="ac5b4-223">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-224">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Nuvem Gladinet</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="ac5b4-226">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-227">Avaliação</span><span class="sxs-lookup"><span data-stu-id="ac5b4-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-228">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-229"><a href="http://storageexplorer.codeplex.com/">Explorador de armazenamento da Web do Azure</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="ac5b4-230">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-230">X</span></span></td>
    <td><span data-ttu-id="ac5b4-231">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-232">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-232">X</span></span></td>
    <td><span data-ttu-id="ac5b4-233">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-234">S</span><span class="sxs-lookup"><span data-stu-id="ac5b4-234">Y</span></span></td>
    <td><span data-ttu-id="ac5b4-235">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ac5b4-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="ac5b4-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="ac5b4-237">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-237">X</span></span></td>
    <td><span data-ttu-id="ac5b4-238">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ac5b4-239">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-239">X</span></span></td>
    <td><span data-ttu-id="ac5b4-240">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-240">X</span></span></td>
    <td><span data-ttu-id="ac5b4-241">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-241">X</span></span></td>
    <td><span data-ttu-id="ac5b4-242">Avaliação</span><span class="sxs-lookup"><span data-stu-id="ac5b4-242">Trial</span></span></td>
    <td><span data-ttu-id="ac5b4-243">X</span><span class="sxs-lookup"><span data-stu-id="ac5b4-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
