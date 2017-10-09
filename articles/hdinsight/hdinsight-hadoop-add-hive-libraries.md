---
title: "as bibliotecas Hive de aaaAdd durante HDInsight cluster criação - Azure | Microsoft Docs"
description: "Saiba como bibliotecas de ramo de registo tooadd (ficheiros jar), tooan HDInsight cluster durante a criação do cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Adicione as bibliotecas Hive personalizadas ao criar o cluster do HDInsight

Se tiver de bibliotecas que utiliza com frequência, com o Hive no HDInsight, este documento contém informações sobre como utilizar as bibliotecas de Olá uma ação de Script toopre carga durante a criação do cluster. Bibliotecas adicionadas utilizando os passos de Olá neste documento são globalmente disponíveis no ramo de registo - há toouse sem necessidade de [adicionar JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload-los.

## <a name="how-it-works"></a>Como funciona

Quando criar um cluster, pode especificar opcionalmente uma ação de Script que executa um script em nós de cluster Olá, enquanto que estão a ser criadas. script de Olá neste documento aceita um único parâmetro que é uma localização de WASB contém Olá bibliotecas (armazenadas como ficheiros jar) toobe previamente carregada.

Durante a criação do cluster, o script de Olá enumera ficheiros Olá, copia-as toohello `/usr/lib/customhivelibs/` diretório em nós head e de trabalho, em seguida, adiciona-toohello `hive.aux.jars.path` propriedade no Olá `core-site.xml` ficheiro. Em clusters baseados em Linux, também atualiza Olá `hive-env.sh` ficheiro com a localização Olá ficheiros Olá.

> [!NOTE]
> Utilizando ações de script de Olá neste artigo disponibiliza bibliotecas Olá no Olá os seguintes cenários:
>
> * **HDInsight baseado em Linux** - quando utilizar Olá um cliente do Hive, **WebHCat**, e **HiveServer2**.
> * **HDInsight baseado em Windows** - ao utilizar o cliente do ramo de registo de Olá e **WebHCat**.

## <a name="hello-script"></a>script de Olá

**Localização do script**

Para **clusters baseados em Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

Para **clusters baseados em Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux for Olá único sistema operativo utilizado no HDInsight versão 3.4 ou superior. Para obter mais informações, veja [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight no Windows).

**Requisitos**

* scripts de Olá tem de ser aplicados tooboth Olá **nós principais** e **nós de trabalho**.

* Olá v7 desejar tooinstall deve ser armazenado no armazenamento de Blobs do Azure num **único contentor**.

* conta de armazenamento de Olá que contém a biblioteca de Olá dos ficheiros jar **tem** ser o cluster do HDInsight toohello ligados durante a criação. -Tem de estar conta do storage predefinida Olá ou uma conta adicionados através do __configuração opcional__.

* contentor de toohello Olá WASB caminho tem de ser especificado como um parâmetro toohello ação de Script. Por exemplo, se hello v7 é armazenados num contentor com o nome **libs** numa conta de armazenamento com o nome **mystorage**, parâmetro Olá seria  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Este documento assume que já tem criar uma conta de armazenamento, o contentor de blob e Olá carregado ficheiros tooit.
  >
  > Se não tiver criado uma conta de armazenamento, pode fazê-através de Olá [portal do Azure](https://portal.azure.com). Em seguida, pode utilizar um utilitário como [Explorador de armazenamento do Azure](http://storageexplorer.com/) toocreate um contentor na conta de Olá e carregar ficheiros tooit.

## <a name="create-a-cluster-using-hello-script"></a>Criar um cluster utilizando o script de Olá

> [!NOTE]
> os seguintes passos de Olá criar um cluster do HDInsight baseado em Linux. Selecione toocreate um cluster baseado no Windows, **Windows** como Olá cluster SO ao criar o cluster de Olá e utilizar o script do Windows (PowerShell) de Olá em vez de scripts de bash Olá.
>
> Também pode utilizar o Azure PowerShell ou Olá SDK .NET do HDInsight toocreate um cluster com este script. Para obter mais informações sobre como utilizar estes métodos, consulte [HDInsight personalizar clusters com ações de Script](hdinsight-hadoop-customize-cluster-linux.md).

1. Começar a aprovisionar um cluster, utilizando os passos de Olá no [aprovisionar clusters do HDInsight no Linux](hdinsight-hadoop-provision-linux-clusters.md), mas não concluir o aprovisionamento.

2. No Olá **configuração opcional** painel, selecione **ações de Script**e forneça Olá seguintes informações:

   * **NOME**: introduza um nome amigável para a ação de script de Olá.

   * **URI de SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **HEAD**: selecione esta opção.

   * **TRABALHO**: selecione esta opção.

   * **ZOOKEEPER**: deixar isto em branco.

   * **Os parâmetros**: introduza Olá WASB toohello contentor de armazenamento e de conta do endereço que contém Olá v7. Por exemplo,  **wasb://libs@mystorage.blob.core.windows.net/** .

3. Na parte inferior de Olá de Olá **ações de Script**, utilize Olá **selecione** configuração de Olá toosave do botão.

4. No Olá **configuração opcional** painel, selecione **contas de armazenamento ligadas** e selecione Olá **adicionar uma chave de armazenamento** ligação. Selecionar conta de armazenamento de Olá contém v7 Olá e, em seguida, utilizar Olá **selecione** definições de toosave botões e retorno Olá **configuração opcional** painel.

5. Olá utilize **selecione** botão na parte inferior de Olá de Olá **configuração opcional** painel toosave Olá opcional as informações de configuração.

6. Continuar aprovisionamento cluster Olá, conforme descrito em [aprovisionar clusters do HDInsight no Linux](hdinsight-hadoop-provision-linux-clusters.md).

Depois de concluída a criação do cluster, é capaz de toouse v7 de Olá adicionados através deste script de ramo de registo, sem ter toouse Olá `ADD JAR` instrução.

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre como trabalhar com o Hive, consulte [utilizar o Hive com o HDInsight](hdinsight-use-hive.md)
