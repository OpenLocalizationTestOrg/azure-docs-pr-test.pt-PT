---
title: aaaCreate um novo recurso do Azure Application Insights | Microsoft Docs
description: "Configure manualmente monitorização do Application Insights para uma nova aplicação em direto."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Criar um recurso do Application Insights
Azure Application Insights apresenta dados sobre a sua aplicação num Microsoft Azure *recursos*. Criar um novo recurso, por conseguinte, faz parte de [como configurar o Application Insights toomonitor uma nova aplicação][start]. Em muitos casos, criação de um recurso pode ser efetuado automaticamente Olá IDE. Mas em alguns casos, crie um recurso manualmente - por exemplo, toohave recursos separados para programação e produção baseia-se da sua aplicação.

Depois de ter criado os recursos de Olá, obter a chave de instrumentação e utilizar essa Olá tooconfigure SDK na aplicação Olá. ligações de chaves de recurso de Olá Olá recursos toohello de telemetria.

## <a name="sign-up-toomicrosoft-azure"></a>Inscrever-se tooMicrosoft do Azure
Se ainda não recebeu um [Microsoft conta, crie uma agora](http://live.com). (Se utilizar serviços como o Outlook.com, OneDrive, Windows Phone ou XBox Live, já tiver uma conta Microsoft.)

Também precisa de uma subscrição demasiado[Microsoft Azure](http://azure.com). Se a sua equipa ou organização tiver uma subscrição do Azure, Olá proprietário pode adicioná-tooit, utilizando o ID do Windows em direto. Apenas a cobrado o que utiliza. plano de básico Olá predefinido permite a uma determinada quantidade de utilização experimental gratuitamente.

Quando já tem acesso tooa subscrição, inicie sessão no tooApplication Insights em [http://portal.azure.com](https://portal.azure.com)e utilizar o toologin Live ID.

## <a name="create-an-application-insights-resource"></a>Criar um recurso do Application Insights
No Olá [portal.azure.com](https://portal.azure.com), adicione um recurso do Application Insights:

![Clicar em Novo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **Tipo de aplicação** afeta o que vê no painel de descrição geral de Olá e propriedades de Olá disponíveis no [explorer métrica][metrics]. Se não vir o seu tipo de aplicação, escolha geral.
* **Subscrição** é a sua conta de pagamento no Azure.
* **Grupo de recursos** está para efeitos práticos para a gestão de propriedades, como o controlo de acesso. Se já tiver criado outros recursos do Azure, pode escolher tooput este novo recurso Olá mesmo grupo.
* **Localização** é onde iremos manter os seus dados.
* **PIN toodashboard** coloca um mosaico de acesso de leitura rápida para o seu recurso na sua página de home page do Azure. Recomendado.

Quando a aplicação tiver sido criada, um novo painel abre. Este painel é onde ver os dados de utilização de desempenho e sobre a sua aplicação. 

tooget back tooit próxima vez que iniciar sessão na tooAzure, procure o mosaico de início rápido da sua aplicação no Olá Iniciar quadro (home ecrã). Ou clique em Procurar toofind-lo.

## <a name="copy-hello-instrumentation-key"></a>Copie a chave de instrumentação Olá
chave de instrumentação Olá identifica recursos de Olá que criou. Precisa toogive toohello SDK.

![Clique em Essentials, clique em Olá chave de instrumentação, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Instalar Olá SDK na sua aplicação
Instale Olá Application Insights SDK na sua aplicação. Este passo depende descontos elevados Olá tipo da sua aplicação. 

Utilizar tooconfigure de chave de instrumentação Olá [Olá SDK que instalou na sua aplicação][start].

Olá SDK inclui módulos padrão que enviam telemetria sem ter toowrite qualquer código. as ações do utilizador tootrack ou diagnosticar problemas em mais detalhe, [utilizar Olá API] [ api] toosend sua própria telemetria.

## <a name="monitor"></a>Ver dados de telemetria
Fechar Olá rápido iniciar o painel de aplicações do painel tooreturn tooyour Olá portal do Azure.

Clique em Olá pesquisa mosaico toosee [pesquisa de diagnóstico][diagnostic], onde são apresentados eventos primeiro Olá. 

Se está à espera de mais dados, clique em **atualizar** após alguns segundos.

## <a name="creating-a-resource-automatically"></a>Criação de um recurso automaticamente
Pode escrever um [script do PowerShell](app-insights-powershell.md) toocreate um recurso automaticamente.

## <a name="next-steps"></a>Passos seguintes
* [Criar um dashboard](app-insights-dashboards.md)
* [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md)
* [Explorar métricas](app-insights-metrics-explorer.md)
* [Escrever consultas da Análise](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

