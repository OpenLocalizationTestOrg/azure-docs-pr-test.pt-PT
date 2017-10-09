---
title: aaaPublish-WebApplicationWebSite (script do Windows PowerShell) | Microsoft Docs
description: "Saiba como toopublish uma web projeto tooan Web site Azure. Este script cria recursos Olá necessária na sua subscrição do Azure, caso não existam."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="81ae4-104">Publicar-WebApplicationWebSite (script do Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="81ae4-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="81ae4-105">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="81ae4-105">Syntax</span></span>
<span data-ttu-id="81ae4-106">Publica um tooan de projeto do web site do Azure.</span><span class="sxs-lookup"><span data-stu-id="81ae4-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="81ae4-107">o script de Olá cria recursos Olá necessária na sua subscrição do Azure, caso não existam.</span><span class="sxs-lookup"><span data-stu-id="81ae4-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="81ae4-108">Configuração</span><span class="sxs-lookup"><span data-stu-id="81ae4-108">Configuration</span></span>
<span data-ttu-id="81ae4-109">Olá caminho toohello ficheiro de configuração JSON que descreve os detalhes de Olá da implementação de Olá.</span><span class="sxs-lookup"><span data-stu-id="81ae4-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="81ae4-110">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81ae4-110">Parameter</span></span> | <span data-ttu-id="81ae4-111">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="81ae4-112">Aliases</span><span class="sxs-lookup"><span data-stu-id="81ae4-112">Aliases</span></span> |<span data-ttu-id="81ae4-113">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-113">none</span></span> |
| <span data-ttu-id="81ae4-114">Necessário?</span><span class="sxs-lookup"><span data-stu-id="81ae4-114">Required?</span></span> |<span data-ttu-id="81ae4-115">VERDADEIRO</span><span class="sxs-lookup"><span data-stu-id="81ae4-115">true</span></span> |
| <span data-ttu-id="81ae4-116">Posição</span><span class="sxs-lookup"><span data-stu-id="81ae4-116">Position</span></span> |<span data-ttu-id="81ae4-117">com o nome</span><span class="sxs-lookup"><span data-stu-id="81ae4-117">named</span></span> |
| <span data-ttu-id="81ae4-118">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-118">Default value</span></span> |<span data-ttu-id="81ae4-119">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-119">none</span></span> |
| <span data-ttu-id="81ae4-120">Aceitar entrada de pipeline?</span><span class="sxs-lookup"><span data-stu-id="81ae4-120">Accept pipeline input?</span></span> |<span data-ttu-id="81ae4-121">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-121">false</span></span> |
| <span data-ttu-id="81ae4-122">Aceitar carateres universais?</span><span class="sxs-lookup"><span data-stu-id="81ae4-122">Accept wildcard characters?</span></span> |<span data-ttu-id="81ae4-123">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="81ae4-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="81ae4-124">SubscriptionName</span></span>
<span data-ttu-id="81ae4-125">nome de Olá do Olá subscrição do Azure que pretende o Web site de Olá toocreate no.</span><span class="sxs-lookup"><span data-stu-id="81ae4-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="81ae4-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81ae4-126">Parameter</span></span> | <span data-ttu-id="81ae4-127">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="81ae4-128">Aliases</span><span class="sxs-lookup"><span data-stu-id="81ae4-128">Aliases</span></span> |<span data-ttu-id="81ae4-129">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-129">none</span></span> |
| <span data-ttu-id="81ae4-130">Necessário?</span><span class="sxs-lookup"><span data-stu-id="81ae4-130">Required?</span></span> |<span data-ttu-id="81ae4-131">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-131">false</span></span> |
| <span data-ttu-id="81ae4-132">Posição</span><span class="sxs-lookup"><span data-stu-id="81ae4-132">Position</span></span> |<span data-ttu-id="81ae4-133">com o nome</span><span class="sxs-lookup"><span data-stu-id="81ae4-133">named</span></span> |
| <span data-ttu-id="81ae4-134">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-134">Default value</span></span> |<span data-ttu-id="81ae4-135">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-135">none</span></span> |
| <span data-ttu-id="81ae4-136">Aceitar entrada de pipeline?</span><span class="sxs-lookup"><span data-stu-id="81ae4-136">Accept pipeline input?</span></span> |<span data-ttu-id="81ae4-137">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-137">false</span></span> |
| <span data-ttu-id="81ae4-138">Aceitar carateres universais?</span><span class="sxs-lookup"><span data-stu-id="81ae4-138">Accept wildcard characters?</span></span> |<span data-ttu-id="81ae4-139">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="81ae4-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="81ae4-140">WebDeployPackage</span></span>
<span data-ttu-id="81ae4-141">Olá caminho toohello implementação pacote toopublish toohello site web.</span><span class="sxs-lookup"><span data-stu-id="81ae4-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="81ae4-142">Pode criar este pacote utilizando o Assistente de publicar Web Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="81ae4-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="81ae4-143">Para obter mais informações, consulte [introdução ao Cloud Services do Azure e ao ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="81ae4-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="81ae4-144">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81ae4-144">Parameter</span></span> | <span data-ttu-id="81ae4-145">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="81ae4-146">Aliases</span><span class="sxs-lookup"><span data-stu-id="81ae4-146">Aliases</span></span> |<span data-ttu-id="81ae4-147">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-147">none</span></span> |
| <span data-ttu-id="81ae4-148">Necessário?</span><span class="sxs-lookup"><span data-stu-id="81ae4-148">Required?</span></span> |<span data-ttu-id="81ae4-149">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-149">false</span></span> |
| <span data-ttu-id="81ae4-150">Posição</span><span class="sxs-lookup"><span data-stu-id="81ae4-150">Position</span></span> |<span data-ttu-id="81ae4-151">com o nome</span><span class="sxs-lookup"><span data-stu-id="81ae4-151">named</span></span> |
| <span data-ttu-id="81ae4-152">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-152">Default value</span></span> |<span data-ttu-id="81ae4-153">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-153">none</span></span> |
| <span data-ttu-id="81ae4-154">Aceitar entrada de pipeline?</span><span class="sxs-lookup"><span data-stu-id="81ae4-154">Accept pipeline input?</span></span> |<span data-ttu-id="81ae4-155">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-155">false</span></span> |
| <span data-ttu-id="81ae4-156">Aceitar carateres universais?</span><span class="sxs-lookup"><span data-stu-id="81ae4-156">Accept wildcard characters?</span></span> |<span data-ttu-id="81ae4-157">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="81ae4-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="81ae4-158">DatabaseServerPassword</span></span>
<span data-ttu-id="81ae4-159">Olá nome de utilizador e palavra-passe para Olá SQL da base de dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="81ae4-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="81ae4-160">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81ae4-160">Parameter</span></span> | <span data-ttu-id="81ae4-161">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="81ae4-162">Aliases</span><span class="sxs-lookup"><span data-stu-id="81ae4-162">Aliases</span></span> |<span data-ttu-id="81ae4-163">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-163">none</span></span> |
| <span data-ttu-id="81ae4-164">Necessário?</span><span class="sxs-lookup"><span data-stu-id="81ae4-164">Required?</span></span> |<span data-ttu-id="81ae4-165">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-165">false</span></span> |
| <span data-ttu-id="81ae4-166">Posição</span><span class="sxs-lookup"><span data-stu-id="81ae4-166">Position</span></span> |<span data-ttu-id="81ae4-167">com o nome</span><span class="sxs-lookup"><span data-stu-id="81ae4-167">named</span></span> |
| <span data-ttu-id="81ae4-168">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-168">Default value</span></span> |<span data-ttu-id="81ae4-169">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-169">none</span></span> |
| <span data-ttu-id="81ae4-170">Aceitar entrada de pipeline?</span><span class="sxs-lookup"><span data-stu-id="81ae4-170">Accept pipeline input?</span></span> |<span data-ttu-id="81ae4-171">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-171">false</span></span> |
| <span data-ttu-id="81ae4-172">Aceitar carateres universais?</span><span class="sxs-lookup"><span data-stu-id="81ae4-172">Accept wildcard characters?</span></span> |<span data-ttu-id="81ae4-173">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="81ae4-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="81ae4-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="81ae4-175">Se for VERDADEIRO, mensagens de impressão de Olá script toohello fluxo de saída.</span><span class="sxs-lookup"><span data-stu-id="81ae4-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="81ae4-176">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="81ae4-176">Parameter</span></span> | <span data-ttu-id="81ae4-177">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="81ae4-178">Aliases</span><span class="sxs-lookup"><span data-stu-id="81ae4-178">Aliases</span></span> |<span data-ttu-id="81ae4-179">Nenhum</span><span class="sxs-lookup"><span data-stu-id="81ae4-179">none</span></span> |
| <span data-ttu-id="81ae4-180">Necessário?</span><span class="sxs-lookup"><span data-stu-id="81ae4-180">Required?</span></span> |<span data-ttu-id="81ae4-181">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-181">false</span></span> |
| <span data-ttu-id="81ae4-182">Posição</span><span class="sxs-lookup"><span data-stu-id="81ae4-182">Position</span></span> |<span data-ttu-id="81ae4-183">com o nome</span><span class="sxs-lookup"><span data-stu-id="81ae4-183">named</span></span> |
| <span data-ttu-id="81ae4-184">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="81ae4-184">Default value</span></span> |<span data-ttu-id="81ae4-185">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-185">false</span></span> |
| <span data-ttu-id="81ae4-186">Aceitar entrada de pipeline?</span><span class="sxs-lookup"><span data-stu-id="81ae4-186">Accept pipeline input?</span></span> |<span data-ttu-id="81ae4-187">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-187">false</span></span> |
| <span data-ttu-id="81ae4-188">Aceitar carateres universais?</span><span class="sxs-lookup"><span data-stu-id="81ae4-188">Accept wildcard characters?</span></span> |<span data-ttu-id="81ae4-189">FALSO</span><span class="sxs-lookup"><span data-stu-id="81ae4-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="81ae4-190">Observações</span><span class="sxs-lookup"><span data-stu-id="81ae4-190">Remarks</span></span>
<span data-ttu-id="81ae4-191">Para obter uma explicação completa do como toouse Olá script toocreate Dev e ambientes de teste, consulte [utilizando Scripts do Windows PowerShell tooPublish tooDev e ambientes de teste](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="81ae4-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="81ae4-192">ficheiro de configuração JSON Olá Especifica os detalhes de Olá que é toobe implementado.</span><span class="sxs-lookup"><span data-stu-id="81ae4-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="81ae4-193">Inclui informações de Olá que especificou quando criou o projeto de Olá, como o nome de Olá e nome de utilizador para o Web site Olá.</span><span class="sxs-lookup"><span data-stu-id="81ae4-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="81ae4-194">Também inclui Olá tooprovision de base de dados, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="81ae4-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="81ae4-195">Olá código a seguir mostra um ficheiro de configuração do JSON de exemplo:</span><span class="sxs-lookup"><span data-stu-id="81ae4-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="81ae4-196">Pode editar Olá JSON configuração ficheiro toochange o que é implementado.</span><span class="sxs-lookup"><span data-stu-id="81ae4-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="81ae4-197">Não é necessária uma secção de Web site, mas a secção de base de dados de Olá é opcional.</span><span class="sxs-lookup"><span data-stu-id="81ae4-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81ae4-198">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="81ae4-198">Next steps</span></span>
<span data-ttu-id="81ae4-199">Para obter mais informações, consulte [publicar-WebApplicationVM (script do Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="81ae4-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

