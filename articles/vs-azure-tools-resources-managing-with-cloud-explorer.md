---
title: aaaManaging Azure recursos com o Explorador de nuvem | Microsoft Docs
description: Saiba como toouse Cloud Explorer toobrowse e gerir recursos do Azure no Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Gerir recursos de Olá associados as contas do Azure no Visual Studio Cloud Explorer
Explorador de nuvem permite-lhe tooview os recursos do Azure e os grupos de recursos, verifique as respetivas propriedades e efetuar ações de diagnóstico de chave para programadores no Visual Studio. 

Como Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer baseia-se na pilha do Olá do Azure Resource Manager. Por conseguinte, o Cloud Explorer compreende recursos, tais como grupos de recursos do Azure e serviços do Azure, tais como aplicações lógicas e API apps e suporta [controlo de acesso baseado em funções](active-directory/role-based-access-control-configure.md) (RBAC). 

## <a name="prerequisites"></a>Pré-requisitos
- [Visual Studio 2017](https://www.visualstudio.com/downloads/) com Olá **carga de trabalho do Azure** selecionado, ou uma versão anterior do Visual Studio com Olá [Microsoft Azure SDK para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Conta do Microsoft Azure - se não tiver uma conta, pode [inscrever-se numa avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) ou [ativar os benefícios de subscritor do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> tooview Cloud Explorer, selecione **vista** > **Cloud Explorer** na barra de menus Olá.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Adicionar uma conta do Azure de tooCloud Explorer
recursos de Olá tooview associados uma conta do Azure, terá de adicionar primeiro Olá conta tooCloud Explorer. 

1. No **Cloud Explorer**, selecione **as definições da conta do Azure**.

    ![Ícone de definições de conta do cloud Explorer Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecione **Adicionar nova conta**. 

    ![Ligação de adicionar a conta do Explorador de nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Inicie sessão no toohello conta do Azure cujos recursos que pretende toobrowse. 

1. Depois de a sessão tooan conta do Azure, apresentam subscrições Olá associadas com essa conta. Selecione as caixas de verificação para as subscrições da conta de Olá que pretende toobrowse e, em seguida, selecione de Olá **aplicar**. 
 
    ![Explorador de nuvem: selecione toodisplay de subscrições do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Depois de selecionar subscrições Olá cujos recursos que pretende apresentam toobrowse, essas subscrições e recursos no Olá Cloud Explorer.

    ![Nuvem recursos Explorer listagem numa conta do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Remover uma conta do Azure a partir do Explorador de nuvem 

1. No **Cloud Explorer**, selecione **as definições da conta do Azure**.

    ![Ícone de definições de conta do cloud Explorer Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecione o seguinte toohello conta que pretende tooremove, **remover**.

    ![Ícone de definições de conta do cloud Explorer Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Ver os tipos de recurso ou grupos de recursos
tooview os recursos do Azure, pode escolher uma **tipos de recursos** ou **grupos de recursos** vista.

1. No **Cloud Explorer**, selecione Olá pendente de vista de recursos.

    ![Vista do Explorador de lista pendente lista tooselect Olá pretendido recursos de nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. No menu de contexto de Olá, selecione a vista de Olá pretendido: 

    - **Tipos de recursos** vista - vista comuns Olá numa Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), mostra os recursos do Azure categorizados pelo respetivo tipo, tais como web apps, contas de armazenamento e máquinas virtuais. 
    - **Grupos de recursos** ver - recursos do Azure categoriza pelo grupo de recursos do Azure de Olá com a qual está associados. Um grupo de recursos é um pacote de recursos do Azure, normalmente utilizadas por uma aplicação específica. toolearn mais informações sobre grupos de recursos do Azure, consulte [descrição geral do Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).

    Olá imagem seguinte mostra uma comparação de Olá duas vistas de recursos:

    ![Comparação de vistas de recursos do Explorador da nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Ver e navegue recursos no Cloud Explorer
toonavigate tooan recursos do Azure e ver a informação no Cloud Explorer, expanda o grupo de recursos associados ou de tipo do item de Olá e, em seguida, selecione o recurso de Olá. Quando seleciona um recurso, informações aparecem no separadores Olá dois - **ações** e **propriedades** - na Olá parte inferior da Cloud Explorer. 

- **Ações** separador - apresenta uma lista de ações de Olá pode efetuar no Cloud Explorer para o recurso de Olá selecionado. Também pode ver estas opções clicando Olá recursos tooview o menu de contexto.

- **Propriedades** - separador de propriedades de Olá mostra de recurso de Olá, tal como o grupo de recursos, região e tipo a que está associada.

Olá imagem seguinte mostra uma comparação de exemplo de o que vê em cada separador, para um serviço de aplicações:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Cada recurso tem a ação de Olá **aberto no portal**. Ao escolher esta ação, Cloud Explorer apresenta recursos Olá selecionado no Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Olá **aberto no portal** funcionalidade é útil para navegar recursos toodeeply aninhado.

Também podem aparecer com base nos recursos do Azure de Olá ações adicionais e valores de propriedade. Por exemplo, as web apps e logic apps também tem ações Olá **abertos no browser** e **anexar depurador** além demasiado**aberto no portal**. Editores de tooopen ações aparecem quando seleciona um blob de conta de armazenamento, uma fila ou uma tabela. As aplicações do Azure têm **URL** e **estado** propriedades, enquanto os recursos de armazenamento ter propriedades de cadeia de ligação e a chave.

## <a name="find-resources-in-cloud-explorer"></a>Localizar recursos no Cloud Explorer
recursos de toolocate com um nome específico nas suas subscrições de conta do Azure, introduza o nome de Olá no Olá **pesquisa** caixa no Cloud Explorer.

![Localizar recursos na Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Como a introduzir carateres no Olá **pesquisa** apresentada a caixa, apenas os recursos que correspondam a esses carateres na árvore de recursos de Olá.
