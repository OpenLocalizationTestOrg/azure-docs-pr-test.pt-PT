---
title: "Criar ambientes de várias VMS e PaaS recursos com modelos Azure Resource Manager | Microsoft Docs"
description: "Saiba como criar ambientes de várias VMS e PaaS recursos no Azure DevTest Labs a partir de um modelo Azure Resource Manager"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: v-craic
ms.openlocfilehash: 55a6c5cd5a0544b297bb68841c5ff0314f48dcc9
ms.sourcegitcommit: 562a537ed9b96c9116c504738414e5d8c0fd53b1
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/12/2018
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Criar ambientes de várias VMS e PaaS recursos com modelos Azure Resource Manager

O [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) permite-lhe facilmente [criar e adicionar uma VM para um laboratório](https://docs.microsoft.com/azure/devtest-lab/devtest-lab-add-vm). Isto funciona bem para criar uma VM a uma hora. No entanto, se o ambiente contém várias VMs, cada VM tem de ser individualmente criado. Para cenários como uma aplicação Web de várias camada ou um farm do SharePoint, é necessário um mecanismo para permitir a criação de várias VMs num único passo. Ao utilizar modelos Azure Resource Manager, pode agora definir a infraestrutura e a configuração da sua solução do Azure e implementar repetidamente várias VMs num estado consistente. Esta funcionalidade fornece as seguintes vantagens:

- Modelos Azure Resource Manager são carregados diretamente a partir do seu repositório de controlo de origem (GitHub ou equipa de serviços de Git).
- Depois de ter configurado, os utilizadores podem criar um ambiente por escolher um modelo Azure Resource Manager no portal do Azure, como fazem com outros tipos de [bases de VM](./devtest-lab-comparing-vm-base-image-types.md).
- Recursos de PaaS do Azure podem ser aprovisionados num ambiente de um modelo Azure Resource Manager para além de VMs de IaaS.
- O custo dos ambientes pode ser controlado no laboratório, além de VMs individuais criadas por outros tipos de bases de.
- Recursos de PaaS são criados e aparecerão no custo controlo; No entanto, o encerramento automático VM não é aplicável a recursos de PaaS.
- Os utilizadores têm o mesmo controlo de política VM para ambientes, pois têm o para as VMs de laboratório único.

Saiba mais sobre os muitos [vantagens da utilização de modelos do Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) para implementar, atualizar ou eliminar todos os seus recursos de laboratório numa única operação.

> [!NOTE]
> Quando utiliza um modelo do Resource Manager como base para criar mais de laboratório de VMs, existem algumas diferenças que tenha em atenção se estiver a criar várias VMs ou VMs único. [Utilizar o modelo Azure Resource Manager de uma máquina virtual](devtest-lab-use-resource-manager-template.md) explica estas diferenças em maior detalhe.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Configurar repositórios de modelo do Azure Resource Manager

Como uma das melhores práticas com infraestrutura como o código e a configuração como código, modelos de ambiente devem ser geridos no controlo de origem. Azure DevTest Labs seguir esta prática e carrega todos os modelos Azure Resource Manager diretamente a partir do seu repositórios do GitHub ou VSTS Git. Como resultado, os modelos do Resource Manager podem ser utilizados entre o ciclo de lançamento completa, do ambiente de teste para o ambiente de produção.

Existem duas regras a seguir para organizar os modelos Azure Resource Manager num repositório:

- O ficheiro de modelo global tem de ser o nome `azuredeploy.json`. 

    ![Ficheiros de modelo de chave do Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Se pretender utilizar os valores de parâmetros definidos no ficheiro de parâmetros, o ficheiro de parâmetros deve ter o nome `azuredeploy.parameters.json`.
- Pode utilizar os parâmetros `_artifactsLocation` e `_artifactsLocationSasToken` para construir o valor URI parametersLink, permitindo DevTest Labs gerir automaticamente modelos aninhados. Consulte [como o Azure DevTest Labs facilita o Gestor de recursos aninhados implementações do modelo para ambientes de teste](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) para obter mais informações.
- Metadados podem ser definido para especificar o nome a apresentar do modelo e a descrição. Estes metadados tem de ser um ficheiro denominado `metadata.json`. O ficheiro de metadados de exemplo seguinte ilustra como especificar o nome a apresentar e uma descrição: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of the template>"
 
}
```

Os seguintes passos guiá-lo através da adição de um repositório para o laboratório no portal do Azure. 

1. Inicie sessão no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista.
1. Na lista de laboratórios, selecione o laboratório pretendido.   
1. No laboratório de **descrição geral** painel, selecione **políticas de configuração e**.

    ![Configuração e políticas](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. Do **políticas de configuração e** lista de definições, selecione **repositórios**. O **repositórios** painel lista repositórios que foram adicionados para o laboratório. Um repositório denominado `Public Repo` é gerado automaticamente para todos os laboratórios e estabelece ligação com o [repositório do GitHub do DevTest Labs](https://github.com/Azure/azure-devtestlab) que contém vários artefactos VM para utilização.

    ![Repositório público](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Selecione **adicionar +** para adicionar o seu repositório de modelo Azure Resource Manager.
1. Quando a segunda **repositórios** é aberto o painel, introduza as informações necessárias, da seguinte forma:
    - **Nome** -introduza o nome do repositório que é utilizado no laboratório.
    - **URL de clone de Git** -introduza o URL de clone de HTTPS de GIT do GitHub ou Visual Studio Team Services.  
    - **Ramo** -introduza o nome de ramo para aceder as definições de modelo Azure Resource Manager. 
    - **Token de acesso pessoal** -o token de acesso pessoal é utilizado para aceder de forma segura o repositório. Para obter o token do Visual Studio Team Services, selecione  **&lt;YourName >> meu perfil > Segurança > token de acesso de público**. Para obter o token a partir do GitHub, selecione o seu avatar seguido selecionando **definições > token de acesso de público**. 
    - **Caminhos de pastas** -utilizando um dos dois campos de entrada, introduza o caminho da pasta que começa com uma barra - / - e é relativo ao seu URI de clone do Git para qualquer as definições de artefactos (campo de entrada primeiro) ou as definições de modelo Azure Resource Manager .   
    
        ![Repositório público](./media/devtest-lab-create-environment-from-arm/repo-values.png)


1. Depois de todos os campos necessários são introduzidos e transmite a validação, selecionar **guardar**.

A secção seguinte irá guiá-lo a criar ambientes de um modelo Azure Resource Manager.

## <a name="create-an-environment-from-a-resource-manager-template-using-the-azure-portal"></a>Criar um ambiente a partir de um modelo do Resource Manager no portal do Azure

Assim que tiver sido configurado um repositório de modelo Azure Resource Manager no laboratório, os utilizadores de laboratório podem criar um ambiente com o portal do Azure com os seguintes passos:

1. Inicie sessão no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista.
1. Na lista de laboratórios, selecione o laboratório pretendido.   
1. No painel do laboratório, selecione **adicionar +**.
1. O **escolher uma base** painel apresenta as imagens de base que pode utilizar com os modelos Azure Resource Manager listados pela primeira vez. Selecione o modelo Azure Resource Manager pretendido.

    ![Escolher uma base](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. No **adicionar** painel, introduza o **o nome do ambiente** valor. O nome do ambiente é o que é apresentado aos utilizadores no laboratório. Os campos de entrada restantes são definidos no modelo Azure Resource Manager. Se os valores predefinidos são definidos no modelo ou o `azuredeploy.parameter.json` ficheiro está presente, os valores predefinidos são apresentados nesses campos de entrada. Para os parâmetros do tipo *secure cadeia*, pode utilizar os segredos armazenados no laboratório de [arquivo pessoal do segredo](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Adicionar o painel](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Existem vários valores de parâmetros que - mesmo especificado - são apresentados como valores vazios. Por conseguinte, se os utilizadores atribuir esses valores para parâmetros de um modelo Azure Resource Manager, DevTest Labs não apresentar os valores. Em vez disso, os campos de entrada em branco são apresentados em que os utilizadores de laboratório tem de introduzir um valor ao criar o ambiente.
    > 
    > - GEN EXCLUSIVO
    > - GEN - EXCLUSIVO-[N]
    > - GEN--PUB-CHAVE SSH
    > - GEN-PALAVRA-PASSE 
 
1. Selecione **adicionar** para criar o ambiente. O ambiente inicia imediatamente de aprovisionamento com a apresentação de estado no **meu máquinas de virtuais** lista. Um novo grupo de recursos é criado automaticamente pelo laboratório para aprovisionar todos os recursos definidos no modelo Azure Resource Manager.
1. Assim que for criado o ambiente, selecione o ambiente no **meu máquinas de virtuais** lista para abrir o painel do grupo de recursos e procurar todos os recursos aprovisionados no ambiente.
    
    ![A minha lista de máquinas virtuais](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   Também pode expandir o ambiente para ver apenas a lista de VMs que são aprovisionadas no ambiente.
    
    ![A minha lista de máquinas virtuais](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Clique em qualquer um dos ambientes para ver as ações disponíveis - como a aplicação de artefactos, ligando os discos de dados, alterar o tempo de encerramento automático e muito mais.

    ![Ações de ambiente](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="deploy-a-resource-manager-template-to-create-a-vm"></a>Implementar um modelo do Resource Manager para criar uma VM
Depois de guardar um modelo do Resource Manager e personalizada-lo para as suas necessidades, pode utilizá-lo a automatizar a criação de VM. 
- [Implementar recursos com modelos do Resource Manager e o Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) descreve como utilizar o Azure PowerShell com modelos do Resource Manager para implementar os recursos no Azure. 
- [Implementar recursos com modelos do Resource Manager e a CLI do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) descreve como utilizar a CLI do Azure com modelos do Resource Manager para implementar os recursos no Azure.

> [!NOTE]
> Apenas um utilizador com permissões de proprietário do laboratório pode criar VMs a partir de um modelo do Resource Manager, utilizando o Azure PowerShell. Se pretender automatizar a criação de VM com um modelo do Resource Manager e apenas tiver permissões de utilizador, pode utilizar o [ **az laboratório vm criar** no CLI](https://docs.microsoft.com/cli/azure/lab/vm#az_lab_vm_create).

### <a name="general-limitations"></a>Limitações gerais 

Considere estas limitações ao utilizar um modelo do Resource Manager no DevTest Labs:

- Qualquer modelo do Resource Manager que criar não pode referenciar recursos existentes; só pode fazer referência a novos recursos. Além disso, se tiver um modelo do Resource Manager existente que normalmente implementa fora DevTest Labs e contém referências a recursos existentes, não pode ser utilizado no laboratório.

   A única exceção é que lhe **pode** fazer referência a uma rede virtual existente. 

- Não não possível criar as fórmulas de laboratório VMs que foram criadas a partir de um modelo do Resource Manager. 

- Não não possível criar imagens personalizadas do laboratório VMs que foram criadas a partir de um modelo do Resource Manager. 

- A maioria das políticas não são avaliadas quando implementar modelos do Resource Manager.

   Por exemplo, poderá ter uma política de laboratório, especificar que um utilizador pode criar apenas cinco VMs. No entanto, se o utilizador implementa um modelo do Resource Manager que cria dezenas de VMs, que é permitida. As políticas que não são avaliadas incluem:

   - Número de VMs por utilizador
   - Número de VMs do premium por utilizador do laboratório
   - Número de discos premium por utilizador do laboratório


### <a name="configure-environment-resource-group-access-rights-for-lab-users"></a>Configurar direitos de acesso do ambiente recursos grupo de utilizadores de laboratório

Utilizadores de laboratório, podem implementar um modelo do Resource Manager. Mas, por predefinição, que têm direitos de acesso de leitor, o que significa que não é possível alterar os recursos de um grupo de recursos do ambiente. Por exemplo, não é possível parar ou iniciar os seus recursos.

Siga estes passos para conceder aos seus utilizadores de laboratório direitos de acesso de contribuinte. Em seguida, quando implementam um modelo do Resource Manager, poderão editar os recursos nesse ambiente. 


1. No seu laboratório **descrição geral** painel, selecione **políticas de configuração e**.
1. Selecione **definições de laboratório**.
1. No painel de definições de laboratório, selecione **contribuinte** para conceder permissões de escrita aos utilizadores de laboratório.

    ![Configurar direitos de acesso de utilizador do laboratório](./media/devtest-lab-create-environment-from-arm/configure-access-rights.png)

1. Selecione **Guardar**.

## <a name="next-steps"></a>Passos Seguintes
* Depois de criar uma VM, pode ligar à VM selecionando **Connect** no painel de gestão da VM.
* Ver e gerir recursos num ambiente selecionando o ambiente no **meu máquinas de virtuais** lista no laboratório. 
* Explorar o [modelos Azure Resource Manager na Galeria de modelo de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).
