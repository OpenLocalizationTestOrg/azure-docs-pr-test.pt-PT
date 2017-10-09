---
title: "aaaCreate uma área de trabalho do Machine Learning | Microsoft Docs"
description: "Como toocreate uma área de trabalho para o Azure Machine Learning Studio"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Criar e partilhar uma área de trabalho do Azure Machine Learning
Este menu contém ligações tootopics que descrevem como tooset segurança Olá vários ambientes de ciência de dados utilizadas por Olá processo de análise da Cortana (CAPS).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse Azure Machine Learning Studio, terá de toohave uma área de trabalho do Machine Learning. Esta área de trabalho contém as ferramentas de Olá terá toocreate, gerir e publicar experimentações.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate uma área de trabalho
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign no e criar uma área de trabalho, terá de toobe um administrador de subscrição do Azure. 
    >
    > 

2. Clique em **+ nova**

3. Selecione **Intelligence + análise**, clique em **área de trabalho do Machine Learning**, em seguida, clique em **criar**

4. Introduza as informações da sua área de trabalho

    - Olá *nome da área de trabalho* poderá estar cópia de segurança too260 carateres, não que termine num espaço. o nome de Olá não pode incluir os seguintes carateres:`< > * % & : \ ? + /`
    - Olá *plano de serviço web* escolher (ou crie), juntamente com Olá associado *escalão de preço* selecione, é utilizada se implementar serviços web desta área de trabalho.

    ![Criar uma nova área de trabalho](media/machine-learning-create-workspace/create-new-workspace.png)

5. Clique em **Criar**.

Assim que a área de trabalho Olá for implementada, pode abri-lo no Machine Learning Studio.

1. Procurar tooMachine Learning Studio no [https://studio.azureml.net/](https://studio.azureml.net/).

2. Selecione a área de trabalho Olá canto superior direito canto.

    ![Selecione a área de trabalho](media/machine-learning-create-workspace/open-workspace.png)

3. Clique em **as minhas experimentações**.

    ![Abra experimentações](media/machine-learning-create-workspace/my-experiments.png)

Para obter informações sobre como gerir a sua área de trabalho, consulte [gerir uma área de trabalho do Azure Machine Learning](machine-learning-manage-workspace.md).
Se ocorrer um problema ao criar a sua área de trabalho, consulte [guia de resolução de problemas: criar e ligar-se a área de trabalho de Machine Learning tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Partilha de uma área de trabalho do Azure Machine Learning
Quando é criada uma área de trabalho do Machine Learning, pode convidar os utilizadores tooyour área de trabalho tooshare acesso tooyour área de trabalho e todos os respetivos experimentações, conjuntos de dados, blocos de notas, etc. Pode adicionar utilizadores de uma das seguintes duas funções:

* **Utilizador** -um utilizador de área de trabalho pode criar, abrir, modificar e eliminar experimentações, conjuntos de dados, etc. na área de trabalho Olá.
* **Proprietário** - pode convidar um proprietário e remover utilizadores na área de trabalho de Olá, em adição toowhat um utilizador podem fazer.

> [!NOTE]
> conta de administrador de Olá que cria a área de trabalho Olá é automaticamente adicionada toohello área como proprietário da área de trabalho. No entanto, outros administradores ou utilizadores nessa subscrição não são automaticamente concedidos aceder à área de trabalho toohello - terá tooinvite-los explicitamente.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare uma área de trabalho

1. A iniciar sessão tooMachine Learning Studio no [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. No painel esquerdo Olá, clique em **definições**

3. Clique em Olá **utilizadores** separador

4. Clique em **CONVIDAR utilizadores mais** em Olá parte inferior da página Olá

    ![Definições do Studio](media/machine-learning-create-workspace/settings.png)

5. Introduza um ou mais endereços de e-mail. os utilizadores de Olá necessitam de uma conta Microsoft válida ou uma conta institucional (a partir do Azure Active Directory).

6. Selecione se pretende que os utilizadores de Olá tooadd como proprietário ou utilizador.

7. Clique em Olá **OK** botão de marca de verificação.

Cada utilizador que adiciona irão receber um e-mail com instruções sobre como toosign no toohello partilhados área de trabalho.

> [!NOTE]
> Para os utilizadores toobe capaz de toodeploy ou gerir os serviços web nesta área de trabalho, têm de ser um Contribuidor ou administrador no Olá subscrição do Azure. 



