---
title: "aaaCreate o fluxo de trabalho primeiro entre aplicações em nuvem & serviços em nuvem - Azure Logic Apps | Microsoft Docs"
description: "Crie e execute fluxos de trabalho no Azure Logic Apps para automatizar processos empresariais para cenários de integração de sistemas e integração de aplicações empresariais (EAI)."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
keywords: "fluxo de trabalho, aplicações na cloud, serviços cloud, processos empresariais, integração de sistemas, integração de aplicações empresariais, EAI"
documentationcenter: 
ms.assetid: ce3582b5-9c58-4637-9379-75ff99878dcd
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/31/2017
ms.author: LADocs; jehollan; estfan
ms.openlocfilehash: 17ec589b1c8923b5ad3e6479fc856b6ac81754ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-logic-app-workflow-tooautomate-processes-between-cloud-apps-and-cloud-services"></a>Criar a sua primeira aplicação de lógica processos de tooautomate de fluxo de trabalho entre aplicações em nuvem e de serviços cloud

Sem que seja necessário escrever qualquer código, pode automatizar processos empresariais mais fácil e rapidamente se criar e executar fluxos de trabalho com o [Azure Logic Apps](logic-apps-what-are-logic-apps.md). Este primeiro exemplo mostra como toocreate um fluxo de trabalho de aplicação lógica básica que verifica um RSS feed para novo conteúdo num Web site. Quando novos itens de aparecem no feed do Web site Olá, a aplicação de lógica de Olá envia e-mail de uma conta do Outlook ou Gmail.

toocreate e execute uma aplicação lógica, terá destes itens:

* Uma subscrição do Azure. Se não tiver uma subscrição, pode [começar com uma conta do Azure gratuita](https://azure.microsoft.com/free/). Caso contrário, pode [inscrever-se numa subscrição Pay As You Go](https://azure.microsoft.com/pricing/purchase-options/).

  A subscrição do Azure é utilizada para faturar a utilização da aplicação lógica. Saiba como funciona a [medição da utilização](../logic-apps/logic-apps-pricing.md) e os [preços](https://azure.microsoft.com/pricing/details/logic-apps) no Azure Logic Apps.

Além disso, este exemplo requer os itens seguintes

* Uma conta do Outlook.com, do Office 365 Outlook ou do Gmail

    > [!TIP]
    > Se tiver uma [conta Microsoft](https://account.microsoft.com/account) pessoal, também tem uma conta do Outlook.com. Caso contrário, se tiver uma conta escolar ou profissional do Azure, tem uma conta do **Office 365 Outlook**.

* Um tooa de ligação do feed RSS do Web site. Este exemplo utiliza Olá [RSS para stories superiores do feed do Web site de CNN.com Olá](http://rss.cnn.com/rss/cnn_topstories.rss):`http://rss.cnn.com/rss/cnn_topstories.rss`

## <a name="add-a-trigger-that-starts-your-workflow"></a>Adicionar um acionador que inicia o fluxo de trabalho

A [ *acionador* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia o fluxo de trabalho de aplicação de lógica e é o primeiro item de Olá que necessita da sua aplicação lógica.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure").

2. No menu à esquerda Olá, escolha **novo** > **integração empresarial com** > **aplicação lógica** conforme mostrado aqui:

     ![Portal do Azure, Novo, Integração Empresarial, Aplicação Lógica](media/logic-apps-create-a-logic-app/azure-portal-create-logic-app.png)

   > [!TIP]
   > Também pode optar por **novo**, em seguida, na caixa de pesquisa de Olá, escreva `logic app`, e prima Enter. Em seguida, escolha **Aplicação Lógica** > **Criar**.

3. Dê um nome à aplicação lógica e selecione a sua subscrição do Azure. Agora, crie ou selecione um grupo de recursos do Azure, que o ajuda a organizar e gerir recursos do Azure relacionados. Por fim, selecione a localização do Centro de dados de Olá para alojar a sua aplicação lógica. Quando estiver pronto, selecione **Pin toodashboard** e, em seguida, **criar**.

     ![Detalhes da aplicação lógica](media/logic-apps-create-a-logic-app/logic-app-settings.png)

   > [!NOTE]
   > Quando seleciona **Pin toodashboard**, a aplicação lógica aparece no Olá dashboard do Azure após a implementação e abre-se automaticamente. Se a sua aplicação lógica não aparece no dashboard de Olá, no Olá **todos os recursos** mosaico, escolha **Consulte mais**e selecione a sua aplicação lógica. Ou no menu à esquerda Olá, escolha **mais serviços**. Em **Integração Empresarial**, escolha **Aplicações Lógicas** e selecione a sua aplicação lógica.

4. Quando abre pela primeira vez a sua aplicação lógica para Olá, Olá Designer de aplicação lógica mostra modelos que pode utilizar tooget foi iniciado. Por agora, escolha **Aplicação Lógica Vazia**, para que possa criá-la do zero.

    Olá Designer de aplicação lógica abre-se e mostra os serviços disponíveis e *acionadores* que pode utilizar na sua aplicação lógica.

5. Na caixa de pesquisa de Olá, escreva `RSS`e selecione este acionador: **RSS - quando um item de feed é publicado** 

    ![Acionador RSS](media/logic-apps-create-a-logic-app/rss-trigger.png)

6. Introduza a ligação de Olá feed do Web site Olá RSS que pretende que o tootrack. 

     Também pode alterar a **Frequência** e o **Intervalo**. 
     Estas definições determinam a frequência com que a aplicação lógica verifica novos itens e devolve todos os itens encontrados durante esse intervalo de tempo.

     Neste exemplo, vamos verifique todos os dias para stories superiores publicados Web site CNN toohello.

     ![Configurar o acionador com o feed RSS, a frequência e o intervalo](media/logic-apps-create-a-logic-app/rss-trigger-setup.png)

7. Guarde o seu trabalho por agora. (Na barra de comando estruturador Olá, escolha **guardar**.)

   ![Guardar a aplicação lógica](media/logic-apps-create-a-logic-app/save-logic-app.png)

   Quando guardar, a sua aplicação lógica vai em direto, mas atualmente, a aplicação lógica só verifica a existência de novos itens na Olá especificado RSS feed. 
   Neste exemplo mais útil, que vamos adicionar uma ação que executa a sua aplicação lógica após o acionador toomake é acionado.

## <a name="add-an-action-that-responds-tooyour-trigger"></a>Adicionar uma ação que responde tooyour acionador

Uma [*ação*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa realizada pelo fluxo de trabalho da sua aplicação lógica. Depois de adicionar uma aplicação de lógica do acionador tooyour, pode adicionar operações de tooperform uma ação com dados gerados pelo que trigger. Para o nosso exemplo, iremos agora adicionar uma ação que envia correio eletrónico quando novos itens são apresentados no feed RSS do Web site Olá.

1. No estruturador de Olá, sob o acionador, escolha **novo passo** > **adicionar uma ação** conforme mostrado aqui:

   ![Adicionar uma ação](media/logic-apps-create-a-logic-app/add-new-action.png)

   Olá designer mostra [conectores disponíveis](../connectors/apis-list.md) , de modo a que possa selecionar uma ação tooperform quando o acionador é acionado.

2. Com base na sua conta de e-mail, siga os passos de Olá para o Outlook ou Gmail.

   * Introduza toosend e-mail da sua conta do Outlook, na caixa de pesquisa de Olá, `outlook`. Em **Serviços**, escolha **Outlook.com**, para contas Microsoft pessoais, ou **Office 365 Outlook**, para contas escolares ou profissionais do Azure. 
   Em **Ações**, selecione **Enviar e-mail**.

       ![Selecionar a ação "Enviar e-mail" do Outlook](media/logic-apps-create-a-logic-app/actions.png)

   * Introduza toosend e-mail da sua conta do Gmail, na caixa de pesquisa de Olá, `gmail`. 
   Em **Ações**, selecione **Enviar e-mail**.

       ![Escolher "Gmail - Enviar e-mail”](media/logic-apps-create-a-logic-app/actions-gmail.png)

3. Quando lhe for pedida credenciais, inicie sessão com Olá nome de utilizador e palavra-passe para a sua conta de e-mail. 

4. Forneça detalhes de Olá para esta ação, como o endereço de correio eletrónico de destino Olá e escolha os parâmetros de Olá para Olá tooinclude de dados no e-mail de Olá, por exemplo:

   ![Selecione os dados tooinclude por correio eletrónico](media/logic-apps-create-a-logic-app/rss-action-setup.png)

    Por isso, se optou pelo Outlook, a sua aplicação lógica poderá ser semelhante a este exemplo:

    ![Aplicação lógica concluída](media/logic-apps-create-a-logic-app/save-run-complete-logic-app.png)

5.  Guarde as alterações. (Na barra de comando estruturador Olá, escolha **guardar**.)

6. Pode agora executar manualmente a sua aplicação lógica para testes. Na barra de comando estruturador Olá, escolha **executar**. Caso contrário, pode permitir que a aplicação lógica, certifique-se Olá especificado feed RSS com base numa agenda Olá que configurou.

   Se a sua aplicação lógica localiza novos itens, a aplicação de lógica de Olá envia correio eletrónico que inclui os dados selecionados. 
   Se não for encontrados nenhuma novos itens, a sua aplicação lógica ignora ação Olá que envia correio eletrónico.

7. toomonitor e verifique a sua aplicação lógica do executar e acionar o histórico de, no menu aplicação lógica, escolha **descrição geral**.

   ![Monitorizar e ver o histórico de execuções e acionadores da aplicação lógica](media/logic-apps-create-a-logic-app/logic-app-run-trigger-history.png)

   > [!TIP]
   > Se não encontrar dados Olá que espera que, na barra de comando Olá, tente escolher **atualizar**.

   mais sobre o estado da sua aplicação lógica toolearn ou execute e acionar histórico ou toodiagnose a sua aplicação lógica, consulte [resolver problemas da aplicação lógica](logic-apps-diagnosing-failures.md).

      > [!NOTE]
      > A aplicação lógica continua a ser executada até que a desative. Escolha tooturn desativar a aplicação por agora, no menu aplicação lógica, **descrição geral**. Na barra de comando Olá, escolha **desativar**.

Parabéns! Acabou de configurar e executar a sua primeira aplicação lógica básica. Também ficou a saber como pode criar facilmente fluxos de trabalho que automatizam processos e integram aplicações na cloud e serviços cloud, tudo sem ter de escrever código.

## <a name="manage-your-logic-app"></a>Gerir a aplicação lógica

toomanage a aplicação, pode realizar tarefas como verificar o estado de Olá, editar, ver o histórico, desativar ou eliminar a sua aplicação lógica.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com "portal do Azure").

2. No menu à esquerda Olá, escolha **mais serviços**. Em **Integração Empresarial**, escolha **Aplicações Lógicas**. Selecione a sua aplicação lógica. 

   No menu de aplicação de lógica de Olá, pode encontrar estas tarefas de gestão de aplicação lógica:

   |Tarefa|Passos| 
   |:---|:---| 
   | Ver o estado da aplicação, o histórico de execuções e informações gerais| Escolha **Descrição geral**.| 
   | Editar a sua aplicação | Escolha **Estruturador da Aplicação Lógica**. | 
   | Ver a definição de JSON do fluxo de trabalho da aplicação lógica | Escolha **Vista de Código da Aplicação Lógica**. | 
   | Ver operações realizadas na aplicação lógica | Escolha **Registo de atividades**. | 
   | Ver as versões passadas da aplicação lógica | Escolha **Versões**. | 
   | Desativar temporariamente a aplicação | Escolha **descrição geral**, em seguida, na barra de comando Olá, escolha **desativar**. | 
   | Eliminar a aplicação | Escolha **descrição geral**, em seguida, na barra de comando Olá, escolha **eliminar**. Introduza o nome da sua aplicação lógica e selecione **Eliminar**. | 

## <a name="get-help"></a>Obter ajuda

perguntas tooask, responda às perguntas e saiba que outras Azure Logic Apps os utilizadores estão a fazer, visite Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador do Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passos seguintes

*  [Adicionar condições e executar fluxos de trabalho](../logic-apps/logic-apps-use-logic-app-features.md)
*    [Modelos de aplicações lógicas](../logic-apps/logic-apps-use-logic-app-templates.md)
*  [Create logic apps from Azure Resource Manager templates](../logic-apps/logic-apps-arm-provision.md) (Criar aplicações lógicas a partir de modelos do Azure Resource Manager)
