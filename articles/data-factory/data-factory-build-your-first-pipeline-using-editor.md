---
title: "aaaBuild a primeira fábrica de dados (portal do Azure) | Microsoft Docs"
description: "Neste tutorial, crie um exemplo de pipeline do Azure Data Factory com o Editor do Data Factory no Olá portal do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a>Tutorial: Criar a primeira fábrica de dados do Azure com o portal do Azure
> [!div class="op_single_selector"]
> * [Descrição geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)


Neste artigo, saiba como toouse [portal do Azure](https://portal.azure.com/) toocreate a primeira fábrica de dados do Azure. toodo Olá tutorial, utilizando outras ferramentas/SDKs, selecione uma das opções de Olá Olá na lista pendente. 

pipeline de Olá neste tutorial tem uma atividade: **atividade do ramo de registo do HDInsight**. Esta atividade executa um script de ramo de registo num cluster do Azure HDInsight transformações dados de saída de tooproduce de dados de entrada. pipeline de Olá é agendada toorun depois de um mês entre Olá especificado tempos de início e de fim. 

> [!NOTE]
> pipeline de dados de Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada. Para um tutorial sobre como os dados de toocopy utilizando o Azure Data Factory, consulte [Tutorial: copiar dados do Blob Storage tooSQL da base de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Um pipeline pode ter mais de uma atividade. Além disso, pode encadeiam duas atividades (executadas uma atividade após outro) definindo o conjunto de dados de saída de Olá de uma atividade como Olá de entrada de conjunto de dados de Olá outra atividade. Para obter mais informações, veja [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) (agendamento e execução no Data Factory).

## <a name="prerequisites"></a>Pré-requisitos
1. Leia [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e Olá concluída **pré-requisito** passos.
2. Este artigo fornece uma descrição geral conceptual dos Olá serviço Azure Data Factory. Recomendamos que leia [introdução tooAzure Data Factory](data-factory-introduction.md) artigo para obter uma descrição detalhada do serviço de Olá.  

## <a name="create-data-factory"></a>Criar fábrica de dados
Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline pode conter uma atividade ou mais. Por exemplo, dados de toocopy uma atividade de cópia de um arquivo de dados de destino de tooa de origem e um toorun de atividade do ramo de registo do HDInsight um tootransform de script de ramo de registo introduzir dados de saída de tooproduct de dados. Vamos começar a criar a fábrica de dados de Olá neste passo.

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **novo** no menu à esquerda Olá, clique em **dados + análise**e clique em **Data Factory**.

   ![Criar painel](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. No Olá **nova fábrica de dados** painel, introduza **GetStartedDF** para Olá nome.

   ![Painel Nova fábrica de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > nome de Olá do Olá do Azure data factory deve ser **globalmente exclusivo**. Se receber o erro de Olá: **nome "GetStartedDF" da fábrica de dados não está disponível**. Altere o nome de Olá do Olá data factory (por exemplo, Seunomegetstarteddf) e tente criar novamente. Veja o tópico [Data Factory – Naming Rules (Data Factory – Regras de Nomenclatura)](data-factory-naming-rules.md) para obter as regras de nomenclatura dos artefactos do Data Factory.
   >
   > nome de Olá da fábrica de dados de Olá pode ser registado como um **DNS** nome no Olá futuro e, por conseguinte, ficar publicamente visível.
   >
   >
4. Selecione Olá **subscrição do Azure** onde pretende toobe de fábrica de dados de Olá criado.
5. Selecione o **grupo de recursos** existente ou crie um grupo de recursos. Tutorial de Olá, crie um grupo de recursos denominado: **ADFGetStartedRG**.
6. Selecione Olá **localização** Olá fábrica de dados. São apresentadas apenas as regiões suportadas pelo serviço Data Factory de Olá Olá na lista pendente.
7. Selecione **Pin toodashboard**. 
8. Clique em **criar** no Olá **nova fábrica de dados** painel.

   > [!IMPORTANT]
   > toocreate instâncias do Data Factory, tem de ser um membro de Olá [contribuinte da fábrica de dados](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) função ao nível do grupo de recursos/subscrição de Olá.
   >
   >
7. No dashboard de Olá, verá a seguinte Olá mosaico com o estado: implementação fábrica de dados.    

   ![Estado de criação da fábrica de dados](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. Parabéns! Criou com êxito a sua primeira fábrica de dados. Depois de Olá a fábrica de dados foi criada com êxito, será apresentada a página de fábrica do Olá dados, que mostra-lhe Olá conteúdos da fábrica de dados de Olá.     

    ![Painel Data Factory](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

Antes de criar um pipeline na fábrica de dados de Olá, terá de toocreate algumas entidades do Data Factory primeiro. Primeiro criar serviços ligados toolink dados arquivos/computações tooyour armazenar, definir a entrada e saída de dados de entrada/saída toorepresent conjuntos de dados nos arquivos de dados ligados e, em seguida, criar o pipeline de Olá com uma atividade que utiliza estes conjuntos de dados.

## <a name="create-linked-services"></a>Criar serviços ligados
Neste passo, pode liga a sua conta do Storage do Azure e uma fábrica de dados a pedido do Azure HDInsight cluster tooyour. Olá contém Olá dados de entrada e de saída do pipeline de Olá neste exemplo de conta de armazenamento do Azure. Olá serviço ligado do HDInsight é toorun utilizado um script de ramo de registo especificado na atividade de Olá de pipeline de Olá neste exemplo. Identificar quais [arquivo de dados](data-factory-data-movement-activities.md)/[serviços de computação](data-factory-compute-linked-services.md) são utilizados no seu cenário e ligar esses fábrica de dados de toohello serviços criando serviços ligados.  

### <a name="create-azure-storage-linked-service"></a>Criar o serviço ligado do Storage do Azure
Neste passo, ligar a fábrica de dados de tooyour de conta do Storage do Azure. Neste tutorial, utilize Olá mesma conta de armazenamento do Azure ficheiro de script de dados de entrada/saída toostore e Olá HQL.

1. Clique em **autor e implementar** no Olá **DATA FACTORY** painel **GetStartedDF**. Deverá ver Olá Editor do Data Factory.

   ![Mosaico Criar e implementar](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. Clique em **Novo arquivo de dados** e escolha **Armazenamento do Azure**.

   ![Menu Novo armazenamento de dados – Armazenamento do Azure](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. Deverá ver Olá script JSON para criar um Storage do Azure ligado serviço num editor de Olá.

   ![Serviço ligado do Storage do Azure](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. Substitua **nome da conta** com o nome de Olá da sua conta de armazenamento do Azure e **chave da conta** com a chave de acesso de Olá de Olá conta do storage do Azure. toolearn como tooget o armazenamento de acesso da chave, consulte Olá obter informações sobre como tooview, copiar e voltar a gerar armazenamento aceder às chaves na [gerir a sua conta de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
5. Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.

    ![Botão Implementar](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   Depois de Olá serviço ligado é implementado com êxito, Olá **rascunho-1** janela deve desaparecer e verá **AzureStorageLinkedService** na vista de árvore Olá Olá esquerda.

    ![Serviço Ligado do Storage no menu](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a>Criar o serviço ligado do Azure HDInsight
Neste passo, pode liga a uma fábrica de dados a pedido HDInsight cluster tooyour. cluster do HDInsight Olá é automaticamente criada no tempo de execução e eliminado depois de ter é processado e ficado inativo para o período de tempo especificado Olá.

1. No Olá **Editor do Data Factory**, clique em **... Mais**, em **Nova computação** e selecione **Cluster de HDInsight a Pedido**.

    ![Nova computação](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. Copie e cole o seguinte fragmento toohello de Olá **rascunho-1** janela. fragmento JSON de Olá descreve Olá as propriedades utilizadas toocreate Olá HDInsight cluster a pedido.

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:

   | Propriedade | Descrição |
   |:--- |:--- |
   | ClusterSize |Especifica o tamanho de cluster do HDInsight Olá Olá. |
   | TimeToLive | Especifica esse tempo de inatividade Olá para o cluster do HDInsight Olá, antes de ser eliminado. |
   | linkedServiceName | Especifica a conta de armazenamento Olá, que é utilizado toostore os registos de Olá que são gerados pelo HDInsight. |

    Tenha em atenção Olá seguintes pontos:

   * Olá Data Factory cria um **baseado em Linux** cluster do HDInsight com Olá JSON. Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
   * Também pode utilizar o **seu próprio cluster do HDInsight** em vez de utilizar um cluster do HDInsight a pedido. Veja [HDInsight Linked Service (Serviço Ligado do HDInsight)](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
   * cluster do HDInsight Olá cria um **contentor predefinido** no armazenamento de BLOBs de Olá especificado na Olá JSON (**linkedServiceName**). HDInsight não é eliminado deste contentor quando cluster Olá é eliminado. Este comportamento é propositado. Com o serviço ligado do HDInsight a pedido, é criado um cluster do HDInsight sempre que é processado um setor, exceto se houver um cluster em direto (**timeToLive**). cluster de Olá é eliminado automaticamente quando o processamento de Olá terminar.

       À medida que são processados mais setores, verá muitos contentores no armazenamento de blobs do Azure. Se não precisar deles para resolução de problemas de tarefas Olá, poderá ser útil toodelete-los armazenamento de Olá tooreduce custo. os nomes de Olá destes contentores seguem um padrão: "adf**nomedafábricadedados**-**linkedservicename**- datetimestamp". Utilize ferramentas como [Explorador de armazenamento do Microsoft](http://storageexplorer.com/) toodelete contentores no seu Azure armazenamento de Blobs.

     Veja [On-demand HDInsight Linked Service (Serviço Ligado do HDInsight a Pedido)](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.
3. Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.

    ![Implementar o serviço ligado de HDInsight a pedido](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. Confirme se vê tanto **AzureStorageLinkedService** e **HDInsightOnDemandLinkedService** na vista de árvore Olá Olá esquerda.

    ![Vista de árvore com serviços ligados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a>Criar conjuntos de dados
Neste passo, poderá criar conjuntos de dados toorepresent Olá entrada e saída dados para o processamento do ramo de registo. Estes conjuntos de dados Consulte toohello **AzureStorageLinkedService** que criou anteriormente neste tutorial. Olá tooan de pontos de serviço ligado conta de armazenamento do Azure e os conjuntos de dados especificam um contentor, pasta, nome de ficheiro no armazenamento de Olá que contém a entrada e saída de dados.   

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. No Olá **Editor do Data Factory**, clique em **... Mais** na barra de comando Olá, clique em **novo conjunto de dados**e selecione **Blob storage do Azure**.

    ![Novo conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. Copie e cole Olá seguinte janela do fragmento toohello rascunho-1. No fragmento JSON de Olá, está a criar um conjunto de dados denominado **AzureBlobInput** que representa dados de entrada para uma atividade no pipeline de Olá. Além disso, especificar que os dados de entrada de Olá estão localizados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **inputdata**.

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    Olá tabela que se segue fornece descrições para as propriedades JSON de Olá utilizadas no fragmento de Olá:

   | Propriedade | Descrição |
   |:--- |:--- |
   | tipo |a propriedade de tipo Olá estiver definida demasiado**AzureBlob** porque os dados que residem no armazenamento de Blobs do Azure. |
   | linkedServiceName |Refere-se toohello **AzureStorageLinkedService** que criou anteriormente. |
   | folderPath | Especifica o blob Olá **contentor** e Olá **pasta** que contém a entrada de blobs. | 
   | fileName |Esta propriedade é opcional. Se omitir esta propriedade, serão escolhidos todos os ficheiros de Olá de Olá folderPath. Neste tutorial, apenas Olá **input.log** está a ser processado. |
   | tipo |ficheiros de registo de Olá estão no formato de texto, pelo que iremos utilizar **TextFormat**. |
   | columnDelimiter |colunas nos ficheiros de registo Olá são delimitadas por **vírgula (`,`)** |
   | frequência/intervalo |a frequência definida demasiado**mês** e o intervalo é **1**, que significa que Olá entrada setores estão disponíveis mensalmente. |
   | externo | Esta propriedade for definida demasiado**verdadeiro** se os dados de entrada de Olá não forem gerados por este pipeline. Neste tutorial, ficheiros de input.log Olá não é gerado por este pipeline, pelo que definimos Olá propriedade tootrue. |

    Para obter mais informações sobre estas propriedades JSON, veja [Azure Blob connector](data-factory-azure-blob-connector.md#dataset-properties) (Conector de Blobs do Azure).
3. Clique em **implementar** no comando Olá barra toodeploy Olá recém-criado dataset. Deverá ver o conjunto de dados de Olá na vista de árvore Olá Olá esquerda.

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Agora, crie Olá dataset toorepresent Olá saída dados de saída armazenados no Olá Blob storage do Azure.

1. No Olá **Editor do Data Factory**, clique em **... Mais** na barra de comando Olá, clique em **novo conjunto de dados**e selecione **Blob storage do Azure**.  
2. Copie e cole Olá seguinte janela do fragmento toohello rascunho-1. No fragmento JSON de Olá, está a criar um conjunto de dados denominado **AzureBlobOutput**e especificar Olá estrutura de dados de Olá que são produzidos pelo script de ramo de registo Olá. Além disso, especifica que os resultados de Olá são armazenados no contentor de blob Olá denominado **adfgetstarted** e pasta Olá **partitioneddata**. Olá **disponibilidade** secção especifica o conjunto de dados de saída que Olá é produzido mensalmente.

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Consulte **criar conjunto de dados de entrada Olá** secção para obter descrições destas propriedades. Não pode definir a propriedade externa Olá um conjunto de dados de saída como Olá conjunto de dados é produzido pelo serviço do Data Factory Olá.
3. Clique em **implementar** no comando Olá barra toodeploy Olá recém-criado dataset.
4. Certifique-se de que esse conjunto de dados de Olá é criado com êxito.

    ![Vista de árvore com serviços ligados](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a>Criar pipeline
Neste passo, irá criar o seu primeiro pipeline com uma atividade **HDInsightHive**. Setor de entrada está disponível mensalmente (frequência: mês, intervalo: 1), o setor de saída é produzido mensalmente e propriedade do agendador Olá atividade Olá seja também definida toomonthly. Olá as definições de conjunto de dados de saída de Olá e agendador de atividade Olá têm de corresponder. Atualmente, o conjunto de dados de saída é que unidades Olá agenda, pelo que deve criar um conjunto de dados de saída, mesmo se Olá atividade não produzir qualquer saída. Se a atividade de Olá não incluir entradas, pode ignorar o conjunto de dados de entrada Olá criar. Propriedades de Olá utilizadas em Olá JSON a seguir são explicadas em final Olá desta secção.

1. No Olá **Editor do Data Factory**, clique em **reticências (…) Comandos mais** e, em seguida, clique em **novo pipeline**.

    ![botão Novo pipeline](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. Copie e cole Olá seguinte janela do fragmento toohello rascunho-1.

   > [!IMPORTANT]
   > Substitua **storageaccountname** com o nome de Olá da sua conta de armazenamento no Olá JSON.
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    No fragmento JSON de Olá, está a criar um pipeline que consiste numa única atividade que utiliza o ramo de registo tooprocess dados num cluster do HDInsight.

    ficheiro de script de ramo de registo de Olá **partitionweblogs.hql**, é armazenada no Olá conta do storage do Azure (especificado pelo scriptLinkedService Olá, denominado **AzureStorageLinkedService**) e, em  **script** pasta no contentor de Olá **adfgetstarted**.

    Olá **define** secção é utilizado toospecify Olá runtime as definições que são transmitidas toohello script de ramo de registo como valores de configuração do ramo de registo (por exemplo ${hiveconf: inputtable}, ${hiveconf}).

    Olá **iniciar** e **final** propriedades de pipeline de Olá Especifica o período ativo de Olá de pipeline de Olá.

    No JSON de atividade de Olá, especifique esse Olá script de ramo de registo é executado na computação Olá especificada pelo Olá **linkedServiceName** – **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Consulte "JSON do Pipeline" em [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md) para obter detalhes sobre as propriedades JSON utilizadas no exemplo de Olá.
   >
   >
3. Confirme o seguinte Olá:

   1. **Input.log** ficheiro existe Olá **inputdata** pasta de Olá **adfgetstarted** contentor no Olá blob storage do Azure
   2. **partitionweblogs.hql** ficheiro existe Olá **script** pasta de Olá **adfgetstarted** contentor no Olá blob storage do Azure. Passos de pré-requisitos concluída Olá em Olá [descrição geral do Tutorial](data-factory-build-your-first-pipeline.md) se não vir estes ficheiros.
   3. Confirme se substituiu **storageaccountname** com o nome de Olá da sua conta de armazenamento no Olá pipeline de JSON.
4. Clique em **implementar** no comando Olá barra pipeline de Olá toodeploy. Desde Olá **iniciar** e **final** são definidas no passado Olá e **isPaused** é conjunto toofalse, pipeline Olá executa (atividade no pipeline de Olá) imediatamente depois da implementação.
5. Confirme que vê o pipeline de Olá na vista de árvore Olá.

    ![Vista de árvore com o pipeline](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. Parabéns, criou com êxito o seu primeiro pipeline!

## <a name="monitor-pipeline"></a>Monitorizar o pipeline
### <a name="monitor-pipeline-using-diagram-view"></a>Monitorizar o pipeline com a Vista de Diagrama
1. Clique em **X** painéis de Editor do Data Factory tooclose toonavigate fazer uma cópia do painel do Data Factory toohello e clique em **diagrama**.

    ![Mosaico do diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. Na vista de diagrama Olá, verá uma descrição geral dos pipelines Olá e conjuntos de dados utilizados neste tutorial.

    ![Vista de Diagrama](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. tooview todas as atividades no pipeline de Olá, contexto pipeline Olá diagrama e clique em abrir Pipeline.

    ![Menu Abrir pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. Confirme que vê atividade HDInsightHive de Olá no pipeline de Olá.

    ![Vista Abrir pipeline](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    fazer uma cópia de toonavigate toohello de vista anterior, clique em **fábrica de dados** no menu de trilho Olá na parte superior do Olá.
5. No Olá **vista de diagrama**, faça duplo clique em dataset Olá **AzureBlobInput**. Confirme que Olá setor estiver no **pronto** estado. Esta operação pode demorar alguns minutos para Olá tooshow de setor no estado pronto. Se tal não acontecer depois de aguardar algum tempo para, consulte o artigo se tiver Olá o ficheiro de entrada (input.log) colocado no contentor de direito de Olá (adfgetstarted) e a pasta (inputdata adequados).

   ![Setor de entrada no estado pronto](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. Clique em **X** tooclose **AzureBlobInput** painel.
7. No Olá **vista de diagrama**, faça duplo clique em dataset Olá **AzureBlobOutput**. Verá o setor que Olá que está atualmente a ser processado.

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. Quando o processamento terminar, verá o setor de Olá no **pronto** estado.

   ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > A criação de um cluster do HDInsight a pedido demora, por norma, algum tempo (cerca de 20 minutos). Por conseguinte, esperar pipeline Olá demorar demasiado **aproximadamente 30 minutos** tooprocess Olá setor.
   >
   >

9. Quando Olá setor estiver no **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** dados de saída do contentor de armazenamento de BLOBs para Olá.  

   ![dados de saída](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. Clique em Olá setor toosee detalhes acerca do mesmo num **setor de dados** painel.

   ![Detalhes do setor de dados](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. Clique numa atividade executada nos Olá **atividade é executada lista** toosee detalhes sobre uma atividade executam (atividade do ramo de registo no nosso cenário) **detalhes da execução da atividade** janela.   

   ![Detalhes da execução da atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   A partir de ficheiros de registo de Olá, pode ver a consulta do Hive Olá que foi executada e informações de estado. Estes registos são úteis para resolver eventuais problemas.
   Consulte o artigo [Monitor and manage pipelines using Azure portal blades (Monitorizar e gerir pipelines com os painéis do Portal do Azure)](data-factory-monitor-manage-pipelines.md) para obter mais detalhes.

> [!IMPORTANT]
> ficheiro de entrada Olá é eliminado quando o setor de Olá é processado com êxito. Por conseguinte, se pretender setor de Olá toorerun ou Olá novamente o tutorial, carregue Olá ficheiro de entrada (input.log) toohello na pasta inputdata do contentor adfgetstarted de Olá.
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitorizar o pipeline com a Aplicação de Monitorização e Gestão
Também pode utilizar o Monitor e gerir aplicações toomonitor seus pipelines. Para obter detalhes sobre a utilização desta aplicação, veja [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App (Monitorizar e gerir pipelines do Azure Data Factory com a Aplicação de Monitorização e Gestão)](data-factory-monitor-manage-app.md).

1. Clique em **Monitor & Gerir** mosaico na Olá home page da fábrica de dados.

    ![Mosaico Monitorizar e Gerir](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. Deverá ver a **Aplicação de Monitorização e Gestão**. Olá alteração **hora de início** e **hora de fim** toomatch início e fim do seu pipeline e clique em **aplicar**.

    ![Aplicação Monitorizar e Gerir](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. Selecione uma janela de atividade no Olá **atividade Windows** lista toosee detalhes acerca do mesmo.

    ![Detalhes da janela de atividade](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a>Resumo
Neste tutorial, criou um dados de tooprocess da fábrica de dados do Azure executando o script de ramo de registo num cluster de hadoop do HDInsight. Utilizou Olá Editor do Data Factory no Olá toodo portal do Azure de Olá os seguintes passos:  

1. Criou uma **fábrica de dados** do Azure.
2. Criar dois **serviços ligados**:
   1. **Armazenamento do Azure** ligado serviço toolink o armazenamento de Blobs do Azure que contém a fábrica de dados de toohello de ficheiros de entrada/saída.
   2. **O Azure HDInsight** a pedido ligado serviço toolink uma fábrica de dados a pedido do HDInsight Hadoop cluster toohello. O Azure Data Factory cria do HDInsight Hadoop, dados de entrada do cluster just-in-time tooprocess e produzir dados de saída.
3. Criar dois **conjuntos de dados**, que descrevem dados de entrada e de saída para a atividade do ramo de registo do HDInsight no pipeline de Olá.
4. Criar um **pipeline** com uma atividade do **Ramo de Registo do HDInsight**.

## <a name="next-steps"></a>Passos Seguintes
Neste artigo, criou um pipeline com uma atividade de transformação (Atividade do HDInsight) que executa um Script de ramo de registo num cluster do HDInsight a pedido. toosee como toouse um toocopy de dados de atividade de cópia de tooAzure um Blob do Azure SQL, consulte [Tutorial: copiar dados de um tooAzure de Blobs do Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Veja Também
| Tópico | Descrição |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda-o a compreender os pipelines e atividades no Azure Data Factory e como toouse-los tooconstruct ponto a ponto condicionados por dados fluxos de trabalho para o seu cenário ou empresa. |
| [Conjuntos de dados](data-factory-create-datasets.md) |Este artigo ajuda-o a compreender os conjuntos de dados no Azure Data Factory. |
| [Agendamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspetos de agendamento e execução de Olá do modelo de aplicação do Azure Data Factory. |
| [Monitorizar e gerir pipelines com a Aplicação de Monitorização](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerir e depurar pipelines utilizando Olá de monitorização e gestão de aplicações. |
