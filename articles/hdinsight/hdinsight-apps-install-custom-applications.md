---
title: "aaaInstall as suas próprias aplicações de Hadoop personalizadas no Azure HDInsight | Microsoft Docs"
description: "Saiba como tooinstall aplicações do HDInsight em aplicações do HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e556b29c-8176-4bc5-a90b-aa01abfd3aee
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ed3148f2c4d4d2b568d84e44fa6d76bb5a001902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-custom-hadoop-applications-on-azure-hdinsight"></a>Instalar aplicações do Hadoop personalizadas no Azure HDInsight

Neste artigo, ficará a saber como tooinstall uma aplicação de Hadoop no HDInsight do Azure, que não foi publicado toohello portal do Azure. aplicação Olá instalará este artigo é [Hue](http://gethue.com/).

Uma aplicação HDInsight é uma aplicação que os utilizadores podem instalar num cluster do HDInsight baseado em Linux.  Estas aplicações podem ser desenvolvidas pela Microsoft, por fornecedores independentes de software (ISV) ou por si.  

Outros artigos relacionados:

* [Instalar aplicações HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters tooinstall um tooyour de aplicação do HDInsight.
* [Publicar aplicações HDInsight](hdinsight-apps-publish-applications.md): Saiba como toopublish sua tooAzure de aplicações HDInsight personalizada Marketplace.
* [MSDN: Instalar uma aplicação do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Saiba como aplicações do HDInsight toodefine.

## <a name="prerequisites"></a>Pré-requisitos
Se quiser tooinstall aplicações do HDInsight num cluster do HDInsight existente, tem de ter um cluster do HDInsight. toocreate um, consulte [criar clusters](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). Também pode instalar aplicações do HDInsight ao criar um cluster do HDInsight.

## <a name="install-hdinsight-applications"></a>Instalar aplicações do HDInsight
Aplicações do HDInsight podem ser instaladas quando cria um cluster ou tooan cluster do HDInsight existente. Para definir modelos do Azure Resource Manager, consulte [MSDN: Instalar uma aplicação do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).

ficheiros de Olá necessários para implementar esta aplicação (Hue):

* [azuredeploy. JSON](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/azuredeploy.json): modelo do Resource Manager Olá para instalar a aplicação do HDInsight. Consulte [MSDN: instalar uma aplicação do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx) para desenvolver o seu próprio modelo do Azure Resource Manager.
* [hue install_v0.sh](https://github.com/hdinsight/Iaas-Applications/blob/master/Hue/scripts/Hue-install_v0.sh): Olá ação de Script a ser chamada pelo modelo do Resource Manager Olá para a configuração de nó de extremidade Olá.
* [hue binaries.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): Olá ficheiro binário da hue a ser chamado a partir de hui install_v0.sh.
* [hue-binários-14-04.tgz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/hue-binaries-14-04.tgz): Olá ficheiro binário da hue a ser chamado a partir de hui install_v0.sh.
* [webwasb tomcat.tar.gz](https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv01/webwasb-tomcat.tar.gz): Uma aplicação Web de exemplo (Tomcat) a ser chamada a partir de hui install_v0.sh.

**cluster do HDInsight tooinstall Hue tooan existente**

1. Clique em Olá seguir toosign de imagem no tooAzure e modelo do Resource Manager Olá aberta no Olá Portal do Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2FIaas-Applications%2Fmaster%2FHue%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Este botão abre um modelo do Resource Manager no Olá portal do Azure.  Olá modelo do Resource Manager está localizado em [https://github.com/hdinsight/Iaas-Applications/tree/master/Hue](https://github.com/hdinsight/Iaas-Applications/tree/master/Hue).  toolearn como toowrite este modelo do Resource Manager, consulte [MSDN: instalar uma aplicação do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. De Olá **parâmetros** painel, introduza Olá seguinte:

   * **ClusterName**: introduza o nome de Olá do cluster de Olá de onde pretende que a aplicação de Olá tooinstall. Este cluster tem de ser um cluster existente.
3. Clique em **OK** parâmetros de Olá toosave.
4. De Olá **implementação personalizada** painel, introduza **grupo de recursos**.  grupo de recursos de Olá é um contentor que agrupa o cluster de Olá, a conta do storage dependente Olá e a outros recursos. É necessário toouse Olá mesmo grupo de recursos do cluster de Olá.
5. Clique em **Termos legais** e em **Criar**.
6. Certifique-se Olá **Pin toodashboard** caixa de verificação está selecionada e, em seguida, clique em **criar**. Pode ver o estado de instalação de Olá de dashboard do portal Olá mosaico afixado toohello e notificação Olá do portal (clique Olá ícone de sino na parte superior de Olá do portal de Olá).  Demora a aplicação de Olá tooinstall de cerca de 10 minutos.

**tooinstall Hue ao criar um cluster**

1. Clique em Olá seguir toosign de imagem no tooAzure e modelo do Resource Manager Olá aberta no Olá Portal do Azure.

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhdinsightapps%2Fcreate-linux-based-hadoop-cluster-in-hdinsight.json" target="_blank"><img src="./media/hdinsight-apps-install-custom-applications/deploy-to-azure.png" alt="Deploy tooAzure"></a>

    Este botão abre um modelo do Resource Manager no Olá portal do Azure.  Olá modelo do Resource Manager está localizado em [https: //hditutorialdata.blob.Core.Windows.NET/hdinsightapps/Create-Linux-based-hadoop-cluster-in-hdinsight.JSON](https://hditutorialdata.blob.core.windows.net/hdinsightapps/create-linux-based-hadoop-cluster-in-hdinsight.json).  toolearn como toowrite este modelo do Resource Manager, consulte [MSDN: instalar uma aplicação do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx).
2. Siga o cluster de toocreate de instrução de Olá e instalar a Hue. Para obter mais informações sobre a criação de clusters do HDInsight, consulte [Criar clusters do Hadoop baseados em Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

Além disso toohello portal do Azure, também pode utilizar [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-powershell) e [CLI do Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md#deploy-with-cli) toocall modelos do Resource Manager.

## <a name="validate-hello-installation"></a>Validar a instalação de Olá
Pode verificar o estado da aplicação Olá em Olá instalação da aplicação Olá toovalidate portal do Azure. Além disso, também pode validar a todos os HTTP pontos finais surgiram conforme esperado e a página Olá Web, se existir:

**portal da Hue tooopen Olá**

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Clusters do HDInsight** no menu à esquerda Olá.  Se o mesmo não for apresentado, clique em **Procurar** e, em seguida, em **Clusters do HDInsight**.
3. Clique em cluster olá onde instalou a aplicação Olá.
4. De Olá **definições** painel, clique em **aplicações** em Olá **geral** categoria. Deverá ver **hue** listado no Olá **aplicações instaladas** painel.
5. Clique em **hue** a partir das propriedades do Olá lista toolist Olá.  
6. Clique em Web de site do Olá página Web ligação toovalidate Olá; Abra o ponto final de Olá HTTP um browser toovalidate Olá Hue IU da web, ponto final de SSH Olá aberta utilizando SSH. Para obter informações, veja [Use SSH with HDInsight (Utilizar SSH com o HDInsight)](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="troubleshoot-hello-installation"></a>Resolver problemas de instalação de Olá
Pode verificar o estado de instalação da aplicação Olá da notificação Olá do portal (clique Olá ícone de sino na parte superior de Olá do portal de Olá).

Se a falha de instalação de uma aplicação, pode ver as mensagens de erro Olá e as informações de 3 locais depuração:

* Aplicações do HDInsight: informações de erro gerais.

    Abrir cluster Olá a partir do portal de Olá e clique em aplicações no painel de definições de Olá:

    ![aplicações do hdinsight erro de instalação da aplicação](./media/hdinsight-apps-install-applications/hdinsight-apps-error.png)
* Ação de script do HDInsight: se a mensagem de erro Olá das aplicações do HDInsight indicar uma falha de ação de script, obter mais detalhes sobre a falha de script de Olá serão apresentados no painel de ações de script de Olá.

    Clique em ação de Script a partir do painel de definições de Olá. Histórico de ações de script apresenta mensagens de erro de Olá

    ![aplicações do hdinsight erro de ação de script](./media/hdinsight-apps-install-applications/hdinsight-apps-script-action-error.png)
* IU da Ambari Web: Se o script de instalação de Olá foi causa Olá falha Olá, utilize o IU da Web do Ambari toocheck os registos completos sobre scripts de instalação de Olá.

    Para obter mais informações, consulte [Resolução de problemas](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting).

## <a name="remove-hdinsight-applications"></a>Remover aplicações do HDInsight
Existem várias aplicações do HDInsight formas toodelete.

### <a name="use-portal"></a>Utilizar o portal
**tooremove uma aplicação através do portal Olá**

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Clusters do HDInsight** no menu à esquerda Olá.  Se o mesmo não for apresentado, clique em **Procurar** e, em seguida, em **Clusters do HDInsight**.
3. Clique em cluster olá onde instalou a aplicação Olá.
4. De Olá **definições** painel, clique em **aplicações** em Olá **geral** categoria. Deverá ver uma lista da aplicação instalada. Para este tutorial, **hue** listado no Olá **aplicações instaladas** painel.
5. Aplicação Olá pretende tooremove e, em seguida, clique com o botão direito **eliminar**.
6. Clique em **Sim** tooconfirm.

No portal de Olá, também pode eliminar cluster Olá ou eliminar o grupo de recursos de Olá que contém a aplicação Olá.

### <a name="use-azure-powershell"></a>Utilizar o Azure PowerShell
Com o Azure PowerShell, pode eliminar cluster Olá ou eliminar o grupo de recursos de Olá. Consulte [Eliminar clusters ao utilizar o Azure PowerShell](hdinsight-administer-use-powershell.md#delete-clusters).

### <a name="use-azure-cli"></a>Utilizar a CLI do Azure
Utilizar a CLI do Azure, pode eliminar cluster Olá ou eliminar o grupo de recursos de Olá. Consulte [Eliminar clusters ao utilizar a CLI do Azure](hdinsight-administer-use-command-line.md#delete-clusters).

## <a name="next-steps"></a>Passos seguintes
* [MSDN: Instalar uma aplicação do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): Saiba como toodevelop modelos do Resource Manager para implementar aplicações do HDInsight.
* [Instalar aplicações HDInsight](hdinsight-apps-install-applications.md): Saiba como clusters tooinstall um tooyour de aplicação do HDInsight.
* [Publicar aplicações HDInsight](hdinsight-apps-publish-applications.md): Saiba como toopublish sua tooAzure de aplicações HDInsight personalizada Marketplace.
* [Personalizar clusters do HDInsight baseado em Linux através da ação de Script](hdinsight-hadoop-customize-cluster-linux.md): Saiba como aplicações do toouse ação de Script tooinstall adicionais.
* [Criar clusters do Hadoop baseados em Linux no HDInsight com modelos do Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): Saiba como clusters toocall Resource Manager modelos toocreate HDInsight.
* [Utilize nós de limite vazio no HDInsight](hdinsight-apps-use-edge-node.md): Saiba como toouse vazio contorno nó para aceder ao cluster do HDInsight, testar aplicações HDInsight e alojamento de aplicações do HDInsight.
