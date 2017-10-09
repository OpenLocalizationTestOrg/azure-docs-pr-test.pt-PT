---
title: "problemas de implementação de serviço de nuvem aaaTroubleshoot | Microsoft Docs"
description: "Existem alguns problemas comuns que poderá ter quando implementar um tooAzure do serviço de nuvem. Este artigo fornece soluções toosome deles."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Resolver problemas de implementação do serviço de nuvem
Quando implementa um tooAzure de pacote de aplicação de serviço de nuvem, pode obter informações sobre a implementação de Olá de Olá **propriedades** painel Olá portal do Azure. Pode utilizar os detalhes de Olá no toohelp neste painel, resolver problemas relacionados com o serviço em nuvem Olá e pode fornecer esta tooAzure informações de suporte ao abrir um novo pedido de suporte.

Pode encontrar Olá **propriedades** painel da seguinte forma:

* No portal do Azure de Olá, clique implementação Olá do seu serviço de nuvem, clique **todas as definições**e, em seguida, clique em **propriedades**.
* No portal clássico do Azure de Olá, clique implementação Olá do seu serviço de nuvem, clique **DASHBOARD**, localizada no canto inferior direito de Olá da página Olá (em **leitura rápida**). Lembre-se de que não há qualquer etiqueta "Propriedades" neste painel.

> [!NOTE]
> Pode copiar o conteúdo Olá Olá **propriedades** área de transferência do painel toohello clicando Olá ícone no canto superior direito de Olá do painel de Olá.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Problema: não é possível aceder a minha Web site, mas os meus implementação ser iniciada e todas as instâncias de função, estará pronto
ligação de URL de Web site Olá apresentada no portal de Olá não inclui porta Olá. porta predefinida de Olá para Web sites é 80. Se a aplicação for toorun configurada uma porta diferente, tem de adicionar Olá porta correta número toohello URL ao aceder ao Web site de Olá.

1. No portal do Azure Olá, clique em implementação Olá do seu serviço de nuvem.
2. No Olá **propriedades** portas Olá Olá as instâncias de função de verificação do painel do portal do Azure, de Olá (em **pontos finais de entrada**).
3. Se a porta de Olá não 80, adicione Olá porta correta valor toohello URL ao aceder a aplicação Olá. toospecify uma porta não predefinido, escreva o URL de Olá, seguido de dois pontos (:), seguido pelo número de porta de Olá, sem espaços.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Problema: Meu instâncias de função recicladas sem enviar-me fazer nada
Serviço autorrecuperação ocorre automaticamente quando o Azure Deteta nós de problema e, por conseguinte, move os nós de toonew de instâncias de função. Se isto ocorre, poderá ver as instâncias da função Reciclagem automaticamente. toofind enviados se serviço autorrecuperação ocorreu:

1. No portal do Azure Olá, clique em implementação Olá do seu serviço de nuvem.
2. No Olá **propriedades** painel do Olá portal do Azure, reveja as informações de Olá e determinar se autorrecuperação do serviço ocorreu durante a hora de Olá observados funções Olá Reciclagem.

Funções também reciclará aproximadamente uma vez por mês durante SO do anfitrião e atualizações de SO convidado.  
Para obter mais informações, consulte a mensagem de blogue de Olá [função instância reinicia devida tooOS atualizações](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Problema: Posso não é possível fazer uma alternância de VIP e receber um erro
Uma alternância de VIP não é permitida se uma atualização da implementação estiver em curso. Atualizações de implementação podem ocorrer automaticamente quando:

* Um novo sistema de operativo convidado está disponível e estão configurados para atualizações automáticas.
* Ocorre a autorrecuperação do serviço.

toofind enviados se atualizar um automático está a impedir a efetuar uma alternância de VIP:

1. No portal do Azure Olá, clique em implementação Olá do seu serviço de nuvem.
2. No Olá **propriedades** painel do Olá portal do Azure, observe o valor Olá **estado**. Se for **pronto**, em seguida, verifique **última operação** toosee se um recentemente ocorrido que poderá impedir a troca de Olá VIP.
3. Repita os passos 1 e 2 para a implementação de produção Olá.
4. Se uma atualização automática está em curso, aguarde pela respetiva toofinish antes de tentar alternância de VIP de Olá toodo.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Problema: Uma instância de função é ciclo entre iniciado, inicialização, ocupado e parado
Esta condição poderá indicar um problema com o código, o pacote ou o ficheiro de configuração da aplicação. Nesse caso, deve ser o estado de Olá toosee capaz de alteração em alguns minutos e hello portal do Azure poderá ser algo semelhante ao seguinte **Reciclagem**, **ocupado**, ou **Initializing**. Isto indica que existe algo errado com a aplicação Olá que consiste em manter instância de função Olá a execução.

Para obter mais informações sobre como tootroubleshoot para este problema, consulte a mensagem de blogue de Olá [dados de diagnóstico de computação do Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) e [comuns emite toorecycle de funções que causa](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Problema: A minha aplicação deixou de funcionar
1. No portal do Azure Olá, clique em instância de função Olá.
2. No Olá **propriedades** painel do Olá portal do Azure, considere Olá seguintes condições tooresolve o problema:
   * Se a instância de função Olá recentemente parou (pode verificar o valor Olá **abortar contagem**), foi possível atualizar a implementação de Olá. Aguarde toosee se a instância de função Olá retoma a funcionar no seu próprio.
   * Se for a instância de função Olá **ocupado**, verifique a sua toosee de código da aplicação se hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) evento é processado. Poderá ter tooadd ou corrigir alguns códigos que processa este evento.
   * Cenários de mensagem de blogue Olá de resolução de problemas e passar por dados de diagnóstico Olá [dados de diagnóstico de computação do Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Se reciclar o seu serviço em nuvem, repor Olá as propriedades de implementação de Olá, eficazmente apagar informações de Olá para problema original Olá.
>
>

## <a name="next-steps"></a>Passos seguintes
Ver mais [artigos de resolução de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para serviços em nuvem.

toolearn como função de serviço de nuvem tootroubleshoot problemas através da utilização de dados de diagnóstico do Azure PaaS computadores, consulte [série de blogues de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
