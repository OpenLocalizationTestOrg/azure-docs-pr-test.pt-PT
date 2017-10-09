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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>Tamanho da pasta predefinida TEMP é demasiado pequeno numa função de web/trabalho do serviço de nuvem
predefinição de Olá diretório temporário de uma função de trabalho ou da web de serviço do cloud tem um tamanho máximo de 100 MB, que podem tornar-se completa, a determinada altura. Este artigo descreve como tooavoid a ficar sem espaço para o diretório temporário Olá.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Por que motivo ficar sem espaço em?
Olá padrão Windows variáveis de ambiente TEMP e TMP são toocode disponível que está a ser executado na sua aplicação. TEMP e TMP tooa ponto único diretório que tem um tamanho máximo de 100 MB. Todos os dados são armazenados neste diretório não são continuados em Olá ciclo de vida do serviço de nuvem Olá; Se forem recicladas instâncias de função Olá num serviço em nuvem, o diretório de Olá limpos.

## <a name="suggestion-toofix-hello-problem"></a>Problema de Olá toofix de sugestão
Implemente uma das Olá alternativas os seguintes:

* Configurar um recurso de armazenamento local e estão acessíveis diretamente em vez de utilizar TEMP ou TMP. tooaccess um recurso de armazenamento local a partir do código está em execução na sua aplicação, chamada Olá [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) método.
* Configurar um recurso de armazenamento local e do ponto de Olá TEMP e TMP diretórios toopoint toohello caminho recursos de armazenamento local Olá. Esta modificação deve ser efetuada dentro de Olá [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) método.

Olá exemplo de código seguinte mostra como toomodify Olá diretórios de destino para TEMP e TMP de dentro do método OnStart de Olá:

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

## <a name="next-steps"></a>Passos seguintes
Ler um blogue que descreve [como tooincrease Olá tamanho da pasta temporária do Azure Web função ASP.NET de Olá](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Ver mais [artigos de resolução de problemas](/?tag=top-support-issue&product=cloud-services) para serviços em nuvem.

toolearn como função de serviço de nuvem tootroubleshoot problemas através da utilização de dados de diagnóstico do computador de Azure PaaS, ver [série de blogues de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
