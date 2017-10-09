---
title: "tamanho da pasta TEMP aaaDefault é demasiado pequeno para uma função | Microsoft Docs"
description: "Uma função de serviço de nuvem tem uma quantidade limitada de espaço para a pasta do Olá TEMP. Este artigo fornece algumas sugestões sobre como tooavoid a ficar sem espaço."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="38d50-104">Tamanho da pasta predefinida TEMP é demasiado pequeno numa função de web/trabalho do serviço de nuvem</span><span class="sxs-lookup"><span data-stu-id="38d50-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="38d50-105">predefinição de Olá diretório temporário de uma função de trabalho ou da web de serviço do cloud tem um tamanho máximo de 100 MB, que podem tornar-se completa, a determinada altura.</span><span class="sxs-lookup"><span data-stu-id="38d50-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="38d50-106">Este artigo descreve como tooavoid a ficar sem espaço para o diretório temporário Olá.</span><span class="sxs-lookup"><span data-stu-id="38d50-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="38d50-107">Por que motivo ficar sem espaço em?</span><span class="sxs-lookup"><span data-stu-id="38d50-107">Why do I run out of space?</span></span>
<span data-ttu-id="38d50-108">Olá padrão Windows variáveis de ambiente TEMP e TMP são toocode disponível que está a ser executado na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="38d50-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="38d50-109">TEMP e TMP tooa ponto único diretório que tem um tamanho máximo de 100 MB.</span><span class="sxs-lookup"><span data-stu-id="38d50-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="38d50-110">Todos os dados são armazenados neste diretório não são continuados em Olá ciclo de vida do serviço de nuvem Olá; Se forem recicladas instâncias de função Olá num serviço em nuvem, o diretório de Olá limpos.</span><span class="sxs-lookup"><span data-stu-id="38d50-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="38d50-111">Problema de Olá toofix de sugestão</span><span class="sxs-lookup"><span data-stu-id="38d50-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="38d50-112">Implemente uma das Olá alternativas os seguintes:</span><span class="sxs-lookup"><span data-stu-id="38d50-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="38d50-113">Configurar um recurso de armazenamento local e estão acessíveis diretamente em vez de utilizar TEMP ou TMP.</span><span class="sxs-lookup"><span data-stu-id="38d50-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="38d50-114">tooaccess um recurso de armazenamento local a partir do código está em execução na sua aplicação, chamada Olá [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="38d50-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="38d50-115">Configurar um recurso de armazenamento local e do ponto de Olá TEMP e TMP diretórios toopoint toohello caminho recursos de armazenamento local Olá.</span><span class="sxs-lookup"><span data-stu-id="38d50-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="38d50-116">Esta modificação deve ser efetuada dentro de Olá [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="38d50-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="38d50-117">Olá exemplo de código seguinte mostra como toomodify Olá diretórios de destino para TEMP e TMP de dentro do método OnStart de Olá:</span><span class="sxs-lookup"><span data-stu-id="38d50-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="38d50-118">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="38d50-118">Next steps</span></span>
<span data-ttu-id="38d50-119">Ler um blogue que descreve [como tooincrease Olá tamanho da pasta temporária do Azure Web função ASP.NET de Olá](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="38d50-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="38d50-120">Ver mais [artigos de resolução de problemas](/?tag=top-support-issue&product=cloud-services) para serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="38d50-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="38d50-121">toolearn como função de serviço de nuvem tootroubleshoot problemas através da utilização de dados de diagnóstico do computador de Azure PaaS, ver [série de blogues de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="38d50-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
