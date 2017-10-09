---
title: aaaDeploy um contentor de Docker de cluster no Azure | Microsoft Docs
description: "Implemente uma solução Kubernetes, DC/OS ou Docker Swarm no serviço de contentor Azure utilizando Olá portal do Azure ou um modelo do Resource Manager."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>Implementar um contentor de Docker alojamento solução utilizando Olá portal do Azure



O Serviço de Contentor do Azure fornece uma implementação rápida de soluções de orquestração e de clustering populares e de open source do contentor. Este documento explica como implementar um cluster do serviço de contentor Azure utilizando Olá portal do Azure ou um modelo de início rápido do Azure Resource Manager. 

Também pode implementar um cluster do serviço de contentor Azure utilizando Olá [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) ou Olá APIs de serviço de contentor do Azure.

Para obter informações de contexto, veja [Introdução ao Azure Container Service](../container-service-intro.md).


## <a name="prerequisites"></a>Pré-requisitos

* **Subscrição do Azure**: se não tiver uma, inscreva-se numa [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). Para um cluster maior, considere uma subscrição pay-as-you-go ou outras opções de compra.

    > [!NOTE]
    > A utilização da subscrição do Azure e [quotas de recursos](../../azure-subscription-service-limits.md), tais como quotas de núcleos, pode limitar tamanho de Olá do cluster de Olá implementar. toorequest um aumento de quota, abra uma [pedido de suporte ao cliente online](../../azure-supportability/how-to-create-azure-support-request.md) , sem encargos.
    >

* **Chave pública SSH RSA**: ao implementar através do portal de Olá ou um dos modelos de início rápido do Azure Olá, necessita de chave pública do tooprovide Olá para autenticação nas máquinas virtuais do serviço de contentor do Azure. as chaves RSA de Secure Shell (SSH) de toocreate, consulte Olá [OS X e Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md) orientações. 

* **ID de principal de cliente e o segredo do serviço** (apenas Kubernetes): para obter mais informações e orientações toocreate um principal de serviço do Azure Active Directory, consulte [sobre principal de serviço Olá para um cluster de Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>Criar um cluster utilizando Olá portal do Azure
1. Início de sessão toohello portal do Azure, selecione **novo**e pesquisa Olá Azure Marketplace para **serviço de contentor Azure**.

    ![Azure Container Service no Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. Clique em **Azure Container Service** e clique em **Criar**.

3. No Olá **Noções básicas** painel, introduza Olá seguintes informações:

    * **Orchestrator**: selecione uma das Olá contentor orchestrators toodeploy no cluster de Olá.
        * **DC/OS**: implementa um cluster DC/OS.
        * **Swarm**: implementa um cluster Docker Swarm.
        * **Kubernetes**: implementa um cluster de Kubernetes.
    * **Subscrição**: selecione uma subscrição do Azure.
    * **Grupo de recursos**: introduza o nome Olá de um novo grupo de recursos para a implementação de Olá.
    * **Localização**: selecione uma região do Azure para a implementação do serviço de contentor Azure Olá. Para obter informações de disponibilidade, veja [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/).
    
    ![Definições básicas](./media/container-service-deployment/acs-portal3.png)  <br />
    
    Clique em **OK** quando estiver pronto tooproceed.

4. No Olá **mestra configuração** painel, introduza Olá seguintes definições para o nó principal do Linux Olá ou nós num cluster de Olá (algumas definições são específicas tooeach orchestrator):

    * **Nome DNS do mestre**: Olá prefix utilizado toocreate um único totalmente qualificado (FQDN) do nome de domínio para mestre Olá. Olá FQDN principal tem o formato de Olá *prefixo*mgmt.*localização*. cloudapp.azure.com.
    * **Nome de utilizador**: nome de utilizador de Olá para uma conta em cada uma das máquinas virtuais do Linux Olá num cluster de Olá.
    * **Chave pública SSH RSA**: Adicionar Olá toobe chave pública utilizada para autenticação nas máquinas virtuais Linux Olá. É importante que esta chave contém não quebras de linha e inclui Olá `ssh-rsa` prefixo. Olá `username@domain` sufixo é opcional. Olá chave deve ter um aspeto semelhante Olá: **ssh-rsa AAAAB3Nz... <>...... UcyupgH azureuser@linuxvm** . 
    * **Principal de serviço**: Se tiver selecionado o orchestrator de Kubernetes Olá, introduza um Azure Active Directory **ID de cliente principal de serviço** (também denominada Olá appId) e **segredo de cliente principal do serviço** (palavra-passe). Para obter mais informações, consulte [sobre principal de serviço Olá para um cluster de Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).
    * **Contagem de principal**: Olá número de estrutura mestres no cluster de Olá.
    * **Diagnósticos da VM**: para algumas orchestrators, pode ativar o diagnóstico VM em modelos de estrutura mestres Olá.

    ![Configuração do modelo de estrutura mestre](./media/container-service-deployment/acs-portal4.png)  <br />

    Clique em **OK** quando estiver pronto tooproceed.

5. No Olá **configuração do agente** painel, introduza Olá seguintes informações:

    * **Contagem de agentes**: para o Docker Swarm e Kubernetes, este valor é o número inicial de Olá de agentes no conjunto de dimensionamento do agente de Olá. Para DC/OS, é Olá número inicial de agentes no conjunto de dimensionamento privado. Além disso, é criado um conjunto de dimensionamento público para o DC/OS, que contém um número pré-determinado de agentes. Olá número de agentes neste conjunto de dimensionamento público é determinado pelo número de Olá de estrutura mestres no cluster de Olá: um agente público para um nó principal e dois agentes públicos para três ou cinco modelos de estrutura mestres.
    * **Tamanho da máquina virtual de agente**: Olá tamanho das máquinas de virtuais Olá agente.
    * **Sistema operativo**: esta definição está atualmente disponível apenas se tiver selecionado o orchestrator de Kubernetes Olá. Escolha uma distribuição de Linux ou um toorun de sistema operativo Windows Server em agentes Olá. Esta definição determina se o cluster pode executar aplicações de contentor Linux ou Windows. 

        > [!NOTE]
        > O suporte do contentor Windows está em pré-visualização para clusters do Kubernetes. Em clusters DC/OS e Swarm, atualmente apenas são suportados agentes Linux no Azure Container Service.

    * **Credenciais do agente**: Se tiver selecionado o sistema de operativo do Windows hello, introduza um administrador **nome de utilizador** e **palavra-passe** para o agente de Olá VMs. 

    ![Configuração do agente](./media/container-service-deployment/acs-portal5.png)  <br />

    Clique em **OK** quando estiver pronto tooproceed.

6. Quando a validação do serviço terminar, clique em **OK**.

    ![Validação](./media/container-service-deployment/acs-portal6.png)  <br />

7. Reveja os termos de Olá. processo de implementação do toostart Olá, clique em **criar**.

    Se tiver tiver optado por toopin Olá implementação toohello portal do Azure, pode ver o estado da implementação Olá.

    ![Estado da implementação](./media/container-service-deployment/acs-portal8.png)  <br />

implementação de Olá demora vários minutos toocomplete. Em seguida, o cluster do serviço de contentor do Azure de Olá está pronto a utilizar.


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>Utilizar um modelo de início rápido para criar um cluster
Os modelos de início rápido do Azure são toodeploy disponível um cluster no serviço de contentor do Azure. Olá fornecido modelos de início rápido podem ser modificadas tooinclude adicionais ou avançada configuração do Azure. toocreate um cluster do serviço de contentor Azure utilizando um modelo de início rápido do Azure, terá de uma subscrição do Azure. Se não tiver uma, inscreva-se numa [avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). 

Siga estes passos toodeploy um cluster utilizando um modelo e Olá 2.0 do Azure CLI (consulte [instruções de instalação e configuração](/cli/azure/install-az-cli2)).

> [!NOTE] 
> Se estiver num sistema Windows, pode utilizar toodeploy de passos semelhantes um modelo com o Azure PowerShell. Veja os passos mais adiante nesta secção. Também pode implementar um modelo através do Olá [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) ou outros métodos.

1. toodeploy um cluster DC/OS, Docker Swarm ou Kubernetes, selecione um dos modelos de início rápido disponíveis Olá a partir do GitHub. Segue uma lista parcial. Olá DC/OS e modelos de Swarm são Olá mesmo, exceto para a seleção do Olá predefinida do orchestrator.

    * [Modelo do DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Modelo do Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Modelo do Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Inicie sessão no tooyour conta do Azure (`az login`) e certifique-se de que Olá CLI do Azure ligado tooyour subscrição do Azure. Pode ver a subscrição predefinida de Olá utilizando Olá os seguintes comandos:

    ```azurecli
    az account show
    ```
    
    Se tiver mais do que um tooset de subscrição e a necessidade de uma subscrição de predefinido diferente, execute `az account set --subscription` e especifique o ID de subscrição de Olá ou nome.

3. Como melhor prática, utilize um novo grupo de recursos para a implementação de Olá. toocreate um grupo de recursos, utilize Olá `az group create` comando especificar um nome de grupo de recursos e localização: 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. Crie um ficheiro que contém Olá necessário modelo JSON parâmetros. Ficheiro de parâmetros de Olá de transferência com o nome `azuredeploy.parameters.json` que acompanha o modelo de serviço de contentor Azure Olá `azuredeploy.json` no GitHub. Introduza os valores dos parâmetros necessários para o cluster. 

    Por exemplo, toouse Olá [modelo do DC/SO](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), forneça os valores de parâmetros para `dnsNamePrefix` e `sshRSAPublicKey`. Consulte as descrições de Olá no `azuredeploy.json` e as opções para outros parâmetros.  
 

5. Criar um cluster do serviço de contentor transferindo o ficheiro de parâmetros de implementação de Olá com Olá seguinte comando, em que:

    * **RESOURCE_GROUP** é o nome de Olá Olá do grupo de recursos que criou no passo anterior Olá.
    * **DEPLOYMENT_NAME** (opcional) é um nome de dar toohello implementação.
    * **TEMPLATE_URI** Olá localização do ficheiro de implementação de Olá `azuredeploy.json`. Este URI deve ter o ficheiro Raw de Olá, não um ponteiro toohello IU do GitHub. toofind este URI, selecione de Olá `azuredeploy.json` de ficheiros no GitHub e clique em Olá **Raw** botão.  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    Também pode fornecer os parâmetros como uma cadeia formatada em JSON na linha de comandos Olá. Utilize um comando semelhante toohello seguinte procedimento:

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > implementação de Olá demora vários minutos toocomplete.
    > 

### <a name="equivalent-powershell-commands"></a>Comandos do PowerShell equivalentes
Também pode implementar um modelo de cluster do Azure Container Service com o PowerShell. Este documento baseia-se numa versão de Olá 1.0 [módulo Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).

1. toodeploy um cluster DC/OS, Docker Swarm ou Kubernetes, selecione um dos modelos de início rápido disponíveis Olá a partir do GitHub. Segue uma lista parcial. Tenha em atenção que as Olá DC/OS e modelos do Swarm são Olá mesmo, com exceção de Olá de seleção de orchestrator Olá predefinida.

    * [Modelo do DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Modelo do Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Modelo do Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Antes de criar um cluster na sua subscrição do Azure, certifique-se de que a sessão do PowerShell iniciou sessão no tooAzure. Pode fazê-lo com Olá `Get-AzureRMSubscription` comando:

    ```powershell
    Get-AzureRmSubscription
    ```

3. Se precisar de toosign no tooAzure, utilize Olá `Login-AzureRMAccount` comando:

    ```powershell
    Login-AzureRmAccount
    ```

4. Como melhor prática, utilize um novo grupo de recursos para a implementação de Olá. toocreate um grupo de recursos, utilize Olá `New-AzureRmResourceGroup` comando e especifique um nome e destino região grupo de recursos:

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. Depois de criar um grupo de recursos, pode criar o cluster com Olá os seguintes comandos. Olá URI de Olá pretendido modelo for especificado com Olá `-TemplateUri` parâmetro. Quando executa este comando, o PowerShell pede-lhe os valores dos parâmetros da implementação.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>Fornecer os parâmetros do modelo
Se estiver familiarizado com o PowerShell, sabe que pode percorrer parâmetros disponíveis de Olá de um cmdlet escrevendo um sinal de subtração (-) e, em seguida, premir a tecla de tabulação Olá. Esta mesma funcionalidade também funciona com os parâmetros que define no modelo. Assim que escrever o nome do modelo Olá, Olá cmdlet obtém o modelo de Olá, analisa os parâmetros de Olá e adiciona os comandos de toohello de parâmetros de modelo Olá dinamicamente. Isto torna valores de parâmetros de modelo de Olá toospecify fácil. Além disso, se se esquecer de um valor de parâmetro necessário, PowerShell pede-lhe o valor de Olá.

Eis o comando completo Olá, com parâmetros incluídos. Forneça os seus próprios valores para os nomes de Olá dos recursos de Olá.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>Passos seguintes
Agora que tem um cluster a funcionar, veja estes documentos para obter os detalhes de ligação e de gestão:

* [Ligue o cluster do serviço de contentor do Azure de tooan](../container-service-connect.md)
* [Trabalhar com o Azure Container Service e o DC/OS](container-service-mesos-marathon-rest.md)
* [Trabalhar com o Azure Container Service e o Docker Swarm](container-service-docker-swarm.md)
* [Trabalhar com o Azure Container Service e o Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)
