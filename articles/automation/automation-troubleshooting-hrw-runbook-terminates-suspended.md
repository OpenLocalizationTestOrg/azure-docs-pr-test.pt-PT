---
title: "Trabalho de Runbook híbrida: Termina o uma tarefa de runbook com o estado suspenso | Microsoft Docs"
description: "Causas sintomas e resoluções para erro de terminação de tarefa do Runbook Worker híbrido."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Função de Trabalho de Runbook Híbrida: uma tarefa de runbook termina com o estado suspenso
## <a name="summary"></a>Resumo
O runbook está suspenso pouco tempo depois tentar tooexecute que três vezes. Existem condições que poderão interromper o runbook Olá a conclusão com êxito e mensagem de erro relacionados Olá não inclui qualquer informação adicional que indica o motivo. Este artigo fornece os passos de resolução de problemas para problemas relacionados toohello Runbook Worker híbrido runbook execução falhas.

Se o problema do Azure não esteja endereçado neste artigo, visite Olá fóruns do Azure no [MSDN e Olá Stack Overflow](https://azure.microsoft.com/support/forums/). Pode publicar o seu problema nestes fóruns ou demasiado[ @AzureSupport no Twitter](https://twitter.com/AzureSupport). Além disso, pode ficheiro um pedido de suporte do Azure ao selecionar **obter suporte** no Olá [suporte do Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptom"></a>Sintoma
Falha de execução do Runbook e erro Olá devolvido é, "Olá ação de tarefa 'Ativar' não é possível executar, porque o processo de Olá parou inesperadamente. ação de tarefa Olá foi tentada 3 vezes."

## <a name="cause"></a>Causa
Existem várias causas possíveis para erro de Olá: 

1. função de trabalho híbrida Olá estiver atrás de um proxy ou firewall
2. Olá computador Olá de trabalho híbrida está em execução no possui inferior que mínimos de hardware Olá [requisitos](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Olá runbooks não é possível autenticar com recursos locais

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Causa 1: O Runbook Worker híbrido é atrás de proxy ou firewall
Olá de computador Olá que está a executar o Runbook Worker híbrido no está atrás de um servidor de firewall ou proxy e acesso de rede de saída não pode ser permitido ou configurado corretamente.

### <a name="solution"></a>Solução
Certifique-se de que o computador de Olá tem acesso de saída too*.cloudapp .net em portas 443, 9354 e 30000 30199. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Causa 2: O computador tiver menos de mínimos de hardware
Computadores com Olá Runbook Worker híbrido deve cumprir Olá requisitos mínimos de hardware antes de indicar-toohost esta funcionalidade. Caso contrário, consoante a utilização de recursos de Olá de outros processos em segundo plano e a contenção causado por runbooks durante a execução, computador Olá irá ficar sobrecarregado e provocar atrasos de tarefa de runbook ou tempos limite. 

### <a name="solution"></a>Solução
Confirme primeiro computador Olá designado a funcionalidade de Runbook Worker híbrido toorun Olá cumpre os requisitos mínimos de hardware de Olá.  Se existir, monitorize toodetermine de utilização de CPU e memória qualquer correlação entre desempenho Olá dos processos de trabalho de Runbook híbrida e o Windows.  Se existir memória ou pressão de CPU, isto pode indicar Olá necessidade tooupgrade ou adicione processadores adicionais, ou aumento memória tooaddress Olá congestionamento do recurso e resolva o erro de Olá. Em alternativa, selecione um recurso de computação diferentes que pode suportar os requisitos mínimos de Olá e dimensionar quando a carga de trabalho exigências indicam que um aumento é necessário.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Causa 3: Não é possível autenticar Runbooks com recursos locais
### <a name="solution"></a>Solução
Verifique Olá **Microsoft SMA** registo de eventos para um evento correspondente com a descrição *Win32 processo abortado com o código [4294967295]*.  causa Olá deste erro é que ainda não configurada a autenticação nos runbooks ou especificado Olá credenciais Run as para o grupo de trabalho híbridas Olá.  Reveja [Runbook permissões](automation-hybrid-runbook-worker.md#runbook-permissions) tooconfirm configurou corretamente a autenticação para os runbooks.  

