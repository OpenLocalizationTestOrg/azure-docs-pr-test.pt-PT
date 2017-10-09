---
title: "aaaBuild uma aplicação sem servidor no Visual Studio | Microsoft Docs"
description: "Introdução à sua primeira aplicação sem servidor com este guia sobre como criar, implementar e gerir aplicação Olá no Visual Studio."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 74530eea6060ffe2139f7c9d6daab8a46f808162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-serverless-app-in-visual-studio-with-logic-apps-and-functions"></a>Criar uma aplicação sem servidor no Visual Studio com Logic Apps e funções

Sem servidor ferramentas e capacidades do Azure permitem um rápido desenvolvimento e implementação das aplicações em nuvem.  Este documento centra-se sobre tooget iniciada no Visual Studio para criar uma aplicação sem servidor.  Uma descrição geral sem servidor no Azure [podem ser encontrados neste artigo](logic-apps-serverless-overview.md).

## <a name="getting-everything-ready"></a>A obter tudo pronto

Seguem-se Olá pré-requisitos necessários toobuild uma aplicação sem servidor a partir do Visual Studio:

* [Visual Studio 2017](https://www.visualstudio.com/vs/) ou Visual Studio 2015 - Comunidade, Professional ou Enterprise
* [Logic Apps Tools para Visual Studio](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551)
* [Azure SDK mais recente](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)
* [Azure PowerShell](https://github.com/Azure/azure-powershell#installation)
* [Ferramentas de núcleos de funções do Azure](https://www.npmjs.com/package/azure-functions-core-tools) toodebug funciona localmente
* Web toohello de acesso ao utilizar Olá incorporado designer de aplicação lógica

## <a name="getting-started-with-a-deployment-template"></a>Começar a utilizar um modelo de implementação

Gerir recursos no Azure terminar dentro de um grupo de recursos.  Um grupo de recursos é um agrupamento lógico de recursos.  Grupos de recursos permitem a implementação e gestão de uma coleção de recursos.  Para uma aplicação sem servidor no Azure, o nosso grupo de recursos contém Azure Logic Apps tanto as funções do Azure.  Ao utilizar o projeto do grupo de recursos de Olá no Visual Studio, estamos toodevelop capaz, gerir e implementar a aplicação completa de Olá como um único recurso.

### <a name="create-a-resource-group-project-in-visual-studio"></a>Criar um projeto do grupo de recursos no Visual Studio

1. No Visual Studio, clique em tooadd um **novo projeto**
1. No Olá **nuvem** categoria, selecione toocreate um Azure **grupo de recursos** projeto  
 * Se não vir a categoria de Olá ou projeto listado, não se esqueça de que ter Olá Azure SDK instalado para o Visual Studio
1. Dê projeto Olá um nome e localização e selecionar **Ok** toocreate Visual Studio solicita tooselect um modelo.  Pode selecionar toostart em branco, a começar com uma lógica de aplicação ou a outros recursos.  No entanto, neste caso, utilizamos uma tooget de modelo de início rápido do Azure-na começar a utilizar uma aplicação sem servidor.
1. Selecione os modelos de tooshow da **início rápido do Azure** ![modelos de início rápido do Azure de seleção][1]
1. Modelo de início rápido sem servidor Olá selecione: **101-logic-app-and-function-app** e clique em **Ok**

modelo de início rápido Olá cria um modelo de implementação no seu projeto de grupo de recursos.  modelo de Olá contém uma aplicação lógica simples que chama das funções do Azure e devolve o resultado de Olá.  Se abrir Olá `azuredeploy.json` Olá de ficheiro no Explorador de soluções, pode ver os recursos de Olá da aplicação sem servidor Olá.

## <a name="deploying-hello-serverless-application"></a>Implementar a aplicação sem servidor Olá

Antes de pode abrir o estruturador visual de aplicação lógica Olá no Visual Studio, tem de existir toobe um grupo de recursos do Azure previamente implementado.  Isto permite que a toocreate estruturador Olá e os serviços e utilize as ligações tooresources na aplicação de lógica de Olá.  tooget iniciado, precisamos simplesmente de solução de Olá toodeploy criada.

1. Projeto de Olá do rato no Visual Studio, selecione **implementar**e criar um **novo** implementação ![selecionando a nova implementação de recursos][2]
1. Selecione uma subscrição do Azure válida e o grupo de recursos
1. Selecione demasiado**implementar** Olá solução
1. Introduza o nome de Olá para Olá aplicação lógica e Olá aplicação de função do Azure.  nome de função do Azure Olá necessário toobe globalmente exclusivo

solução sem servidor Olá implementa no grupo de recursos especificado Olá.  Se observar Olá **saída** no Visual Studio que pode ver o estado de Olá da implementação de Olá.

## <a name="editing-hello-logic-app-in-visual-studio"></a>Editar aplicação de lógica de Olá no Visual Studio

Assim que tiver sido implementada a solução de Olá em qualquer grupo de recursos, designer visual Olá pode ser utilizado tooedit e tornar a aplicação de lógica de toohello de alterações.

1. Contexto Olá `azuredeploy.json` ficheiros Olá Explorador de soluções e selecione **aberto com Logic Apps Designer**
1. Selecione Olá **grupo de recursos** e **localização** solução Olá foi implementado tooand selecione **OK**

designer visual de aplicação lógica Olá deve agora estar visível com o Visual Studio.  Pode continuar tooadd passos, modifique o fluxo de trabalho Olá e guardar as alterações.  Também pode criar as logic apps a partir do Visual Studio.  Se, faça duplo clique Olá **recursos** no navegador de modelo de Olá, pode escolher tooadd um **aplicação lógica** toohello projeto.  Carregar aplicações lógicas vazio no designer visual de Olá sem uma pré-implementar num grupo de recursos.

### <a name="managing-and-viewing-run-history-for-a-deployed-logic-app"></a>Gerir e ver o histórico de execução de uma aplicação lógica implementado

Também pode gerir e ver o histórico de Olá executar para aplicações lógicas implementado no Azure.  Se abrir Olá **Cloud Explorer** ferramenta no Visual Studio, pode qualquer aplicação lógica com o botão direito e selecione tooedit, desativar, ver propriedades ou ver histórico de execução.  Ao clicar em Editar também permite-lhe toodownload uma aplicação lógica publicados para um projeto do grupo de recursos do Visual Studio.  Isto significa que, mesmo se tiver iniciado a criar uma aplicação lógica em Olá portal do Azure, pode ainda importá-los e geri-lo a partir do Visual Studio.

## <a name="developing-an-azure-function-in-visual-studio"></a>Desenvolver uma função do Azure no Visual Studio

Olá modelo de implementação implementa quaisquer funções do Azure que estão incluídas na solução de Olá para o repositório de git Olá especificado no Olá `azuredeploy.json` variáveis.  Se criar um projeto de função na solução de Olá, registá-lo para o controlo de origem (GitHub, Visual Studio Team Services, etc.) e atualizar Olá `repo` variável, o modelo de Olá implementará Olá função do Azure.

### <a name="creating-an-azure-function-project"></a>Criar um projeto de função do Azure

Se utilizar o JavaScript, Python, F #, Bash, Batch ou PowerShell, siga Olá [os passos em Olá funções CLI](../azure-functions/functions-run-local.md) toocreate um projeto.  Se desenvolver uma função em c#, pode utilizar um [biblioteca de classes do c#](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/16/publishing-a-net-class-library-as-a-function-app/) na solução atual de Olá para Olá função do Azure.

## <a name="next-steps"></a>Passos seguintes

* [Saiba como toobuild um dashboard de redes social sem servidor](logic-apps-scenario-social-serverless.md)
* [Gerir uma aplicação lógica a partir do Explorador de nuvem do Visual Studio](logic-apps-manage-from-vs.md)
* [Linguagem de definição de fluxo de trabalho de aplicação lógica](logic-apps-workflow-definition-language.md)

<!-- Image references -->
[1]: ./media/logic-apps-serverless-get-started-vs/select-template.png
[2]: ./media/logic-apps-serverless-get-started-vs/deploy.png
