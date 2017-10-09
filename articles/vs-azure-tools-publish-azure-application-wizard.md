---
title: "Olá aaaUsing Visual Studio publicar Assistente da aplicação Azure | Microsoft Docs"
description: "Saiba como tooconfigure Olá várias definições no Olá Visual Studio publicar Assistente da aplicação Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d8f1ac9-e439-47e0-a183-0642c4ea1920
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3f0b580d0054cc246372597660d8ae317d9b8686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-visual-studio-publish-azure-application-wizard"></a>Utilizar Olá Visual Studio publicar Assistente da aplicação Azure
Depois de desenvolver uma aplicação web no Visual Studio, pode publicar nessa tooan aplicação de serviço em nuvem do Azure utilizando Olá **publicar aplicação Azure** assistente. 

> [!NOTE]
> Este tópico é sobre a implementação de serviços de toocloud, não tooweb sites. Para obter informações sobre a implementação tooweb sites, consulte [como tooDeploy um Web Site do Azure](https://social.msdn.microsoft.com/Search/windowsazure?query=How%20to%20Deploy%20an%20Azure%20Web%20Site&Refinement=138&ac=4#refinementChanges=117&pageNumber=1&showMore=false).
> 
> 

## <a name="accessing-hello-publish-azure-application-wizard"></a>Aceder ao Assistente de Olá de publicar aplicações do Azure

Pode aceder ao Assistente de publicar aplicação Azure Olá de duas formas, dependendo do tipo de Olá de projeto do Visual Studio que tem.

**Se tiver um projeto de serviço em nuvem do Azure:**

1. Criar ou abrir um projeto de serviço em nuvem do Azure no Visual Studio.

1. No **Explorador de soluções**, clique no projeto Olá e, no menu de contexto de Olá, selecione **publicar**.

**Se tiver um projeto de aplicação web não está ativado para o Azure:**

1. Criar ou abrir um projeto de serviço em nuvem do Azure no Visual Studio.

1. No **Explorador de soluções**, clique no projeto Olá e, no menu de contexto de Olá, selecione **converter** > **converter tooAzure projeto de serviço em nuvem**. 

1. No **Explorador de soluções**, clique no projeto do Azure Olá recém-criado e, no menu de contexto de Olá, selecione **publicar**.

## <a name="sign-in-page"></a>Página de início de sessão

![Página de início de sessão](./media/vs-azure-tools-publish-azure-application-wizard/sign-in.png)

**Conta** - Selecione uma conta ou **adicionar uma conta** na lista de lista pendente de conta Olá.

**Escolha a sua subscrição** -escolha Olá toouse de subscrição para a sua implementação.
   
## <a name="settings-page---common-settings-tab"></a>Página de definições - separador de definições comuns   

![Definições comuns](./media/vs-azure-tools-publish-azure-application-wizard/settings-common-settings.png)

**O serviço em nuvem** -utilizar Olá pendente, selecione uma nuvem existente, serviço ou selecione  **&lt;criar novo >**e criar um serviço em nuvem. Centro de dados de Olá apresenta parênteses para cada serviço em nuvem. Recomenda-se que a localização de centro de dados de Olá para hello serviço em nuvem ser Olá mesmo como localização de centro de dados de Olá Olá conta de armazenamento (definições avançadas).  

**Ambiente** -selecione **produção** ou **transição**. Escolha Olá ambiente de teste, se quiser toodeploy a aplicação num ambiente de teste. 

**Criar configuração** -selecione **depurar** ou **versão**.

**A configuração do serviço** -selecione **nuvem** ou **Local**.
   
**Ativar o ambiente de trabalho remoto para todas as funções** -verificação esta opção se quiser toobe tooremotely de capaz de ligar o serviço de toohello. Esta opção é utilizada principalmente para resolução de problemas. Ao selecionar esta caixa de verificação, Olá **configuração do ambiente de trabalho remoto** é apresentada a caixa de diálogo. Escolha Olá **definições** configuração de Olá toochange de ligação.
   
**Ativar o Web Deploy para todos os web funções** -esta opção, a implementação na web para o serviço de Olá tooenable de verificação. Tem de selecionar Olá **ativar o ambiente de trabalho remoto para todas as funções** opção toouse esta funcionalidade. Para obter mais informações, consulte [ [publicação de um serviço em nuvem do Azure com o Visual Studio](https://msdn.microsoft.com/library/azure/ff683672.aspx)](https://msdn.microsoft.com/library/azure/ff683672.aspx). 

## <a name="settings-page---advanced-settings-tab"></a>Página de definições - avançada do separador Definições

![Definições avançadas](./media/vs-azure-tools-publish-azure-application-wizard/settings-advanced-settings.png)

**Etiqueta de implementação** -aceite o nome predefinido de hello, ou introduza um nome à sua escolha. etiqueta de implementação de toohello de data de Olá tooappend, caixa de verificação de Olá deixe selecionada. 
   
**Conta de armazenamento** - selecione Olá toouse de conta de armazenamento para esta implementação, * *&lt;criar novo > toocreate uma conta de armazenamento. Centro de dados de Olá apresenta parênteses para cada conta de armazenamento. Recomenda-se que a localização de centro de dados de Olá para hello conta do storage ser Olá mesmo como Olá a localização de centro de dados para o serviço de nuvem de Olá (definições comuns).  
   
Olá conta do storage do Azure armazena pacote Olá para implementação de aplicação Olá. Depois de implementar a aplicação Olá, pacote Olá é removido da conta de armazenamento de Olá.

**Eliminar a implementação em caso de falha** -Selecione esta implementação de Olá opção toohave eliminada se forem encontrados erros durante a publicação. Deverá ser desmarcada se quiser toomaintain um endereço IP virtual constante do serviço em nuvem.

**Atualização da implementação** -Selecione esta opção se pretender que toodeploy apenas os componentes atualizados. Este tipo de implementação pode ser mais rápido do que uma implementação completa. Isto deve ser verificado se quiser toomaintain um endereço IP virtual constante do serviço em nuvem. 

**Atualização da implementação - definições** -é utilizada nesta caixa de diálogo toofurther especificar como pretende que Olá funções toobe atualizado. Se optar por **atualização Incremental**, cada instância da sua aplicação é atualizada após a outra, para essa aplicação Olá está sempre disponível. Se optar por **atualização em simultâneo**, todas as instâncias da aplicação são atualizadas em Olá mesmo tempo. A atualização em simultâneo é mais rápida, mas o serviço poderá não estar disponível durante o processo de atualização de Olá. 

![Definições de implementação](./media/vs-azure-tools-publish-azure-application-wizard/deployment-settings.png)

**Ativar o IntelliTrace** -especificar se pretende tooenable IntelliTrace. Com IntelliTrace, que pode iniciar sessão extensas informações de depuração para uma instância de função quando for executada no Azure. Se precisar de causa de Olá toofind de um problema, pode utilizar toostep de registos do IntelliTrace Olá através do seu código a partir do Visual Studio, como se estivesse em execução no Azure. Para obter mais informações sobre como utilizar o IntelliTrace, consulte [depuração um serviço em nuvem do Azure publicadas com o Visual Studio e o IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md). 

**Ativar a criação de perfis** -especificar se pretende que o desempenho tooenable de criação de perfis. o gerador de perfis do Olá Visual Studio permite tooget uma análise aprofundada de aspetos computacional Olá como o seu serviço em nuvem é executado. Para obter mais informações sobre como utilizar o gerador de perfis do Olá Visual Studio, consulte [testar o desempenho de Olá de um serviço em nuvem do Azure](./vs-azure-tools-performance-profiling-cloud-services.md).

**Ativar o depurador remoto para todas as funções** -especificar se pretende que o tooenable a depuração remota. Para obter mais informações sobre a depuração serviços em nuvem com o Visual Studio, consulte [depuração um serviço em nuvem do Azure ou a máquina virtual no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md).

## <a name="diagnostics-settings-page"></a>Página de definições de diagnóstico

![Definições de diagnóstico](./media/vs-azure-tools-publish-azure-application-wizard/diagnostic-settings.png)

Diagnóstico permite-lhe tootroubleshoot um serviço em nuvem do Azure (ou máquina virtual do Azure). Para obter informações sobre diagnósticos, consulte [configurar diagnósticos para máquinas virtuais e serviços Cloud do Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). Para obter informações sobre o Application Insights, consulte [o que é Application Insights?](./application-insights/app-insights-overview.md).

## <a name="summary-page"></a>Página de resumo

![Resumo](./media/vs-azure-tools-publish-azure-application-wizard/summary.png)

**Perfil de destino** -toocreate pode escolher um perfil de publicação a partir das definições de Olá que escolheu. Por exemplo, poderá criar um perfil para um ambiente de teste e outra para a produção. toosave este perfil, escolha Olá **guardar** ícone. o Assistente de Olá cria o perfil de Olá e guarda-o no projeto do Visual Studio Olá. nome do perfil de toomodify Olá, abra Olá **destino perfil** lista e, em seguida, escolha **< gerir … >**.
   
   > [!NOTE]
   > perfil de publicação Olá é apresentada no Explorador de soluções no Visual Studio e definições de perfil Olá são escritos no ficheiro tooa com uma extensão de .azurePubxml. As definições são guardadas como atributos das etiquetas XML.
   > 
   > 

## <a name="publishing-your-application"></a>Publicação da sua aplicação

Depois de configurar todas as definições de Olá para a implementação do seu projeto, selecione **publicar** em Olá parte inferior da caixa de diálogo Olá. Pode monitorizar o estado do processo Olá no Olá **saída** janela no Visual Studio.

## <a name="next-steps"></a>Passos seguintes
- [Migrar e publicar uma aplicação Web de tooan serviço em nuvem do Azure a partir do Visual Studio](./vs-azure-tools-migrate-publish-web-app-to-cloud-service.md)
- [Saiba como o serviço em nuvem toouse Visual Studio toopublish do Azure](./vs-azure-tools-publishing-a-cloud-service.md)
- [A depuração de um serviço em nuvem do Azure publicadas com o Visual Studio e o IntelliTrace](./vs-azure-tools-intellitrace-debug-published-cloud-services.md)
- [Testar o desempenho de Olá de um serviço em nuvem do Azure](./vs-azure-tools-performance-profiling-cloud-services.md)
- [Configurar diagnósticos para máquinas virtuais e serviços em nuvem do Azure](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md). 
- [O que é o Application Insights?](./application-insights/app-insights-overview.md)