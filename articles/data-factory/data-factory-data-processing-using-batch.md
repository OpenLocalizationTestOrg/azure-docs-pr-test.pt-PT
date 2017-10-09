---
title: aaaProcess conjuntos de dados em grande escala com o Data Factory e Batch | Microsoft Docs
description: Descreve como o pipeline de tooprocess quantidades enormes de dados de um Azure Data Factory, utilizando a capacidade de processamento paralelo de lote do Azure.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a>Processar grandes conjuntos de dados com o Data Factory e o Batch
Este artigo descreve uma arquitetura de uma solução de exemplo que se move e processa os conjuntos de dados em grande escala de forma automática e agendada. Também fornece uma solução de Olá instruções ponto a ponto tooimplement através do Azure Data Factory e do Azure Batch.

Este artigo é maior do que o nosso artigo típico porque contém uma explicação passo a passo de uma solução de exemplo completo. Se for novo tooBatch e fábrica de dados, pode saber sobre estes serviços e como funcionam em conjunto. Se souber algo sobre os serviços de Olá e são estruturar/arquitetar uma solução, pode concentrar-se apenas nos Olá [secção de arquitetura](#architecture-of-sample-solution) do artigo Olá e se estiver a desenvolver um protótipo ou uma solução, também poderá tootry instruções passo a passo Olá [instruções](#implementation-of-sample-solution). Convidamo-os seus comentários sobre este conteúdo e como utilizá-lo.

Em primeiro lugar, vamos ver como podem ajudar a fábrica de dados e Batch serviços com grandes conjuntos de dados na nuvem de Olá de processamento.     

## <a name="why-azure-batch"></a>Por que motivo o Azure Batch?
O Azure Batch permite-lhe toorun em grande escala paralelas e elevado desempenho aplicações de computação (HPC) e forma eficiente na nuvem de Olá. É um serviço de plataforma que agenda trabalho de computação intensiva toorun numa coleção gerida de máquinas virtuais e pode dimensionar automaticamente de computação necessidades de Olá toomeet recursos das suas tarefas.

Com o serviço Batch Olá, é possível definir tooexecute de recursos de computação do Azure as suas aplicações em paralelo e com dimensionamento. Pode executar a pedido ou agendadas tarefas e não precisa de toomanually criar, configurar e gerir um cluster HPC, máquinas virtuais individuais, redes virtuais ou uma tarefa complexa e infraestrutura de agendamento de tarefas.

Consulte Olá seguintes artigos se não estiver familiarizado com o Azure Batch como ajuda com compreender Olá arquitetura/implementação da solução de Olá descrita neste artigo.   

* [Noções básicas do Azure Batch](../batch/batch-technical-overview.md)
* [Descrição geral da funcionalidade do Batch](../batch/batch-api-basics.md)

(opcional) toolearn mais informações sobre o Azure Batch, consulte Olá [percurso de aprendizagem para o Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).

## <a name="why-azure-data-factory"></a>Por que motivo fábrica de dados do Azure?
Data Factory é um serviço de integração de dados baseado na nuvem que orquestra e automatiza o movimento de Olá e a transformação de dados. Utilizar o serviço do Data Factory Olá, pode criar pipelines de dados geridos que movem os dados no local e na nuvem arquivo de dados centralizada de tooa de arquivos de dados (por exemplo: Blob Storage do Azure) e o processo/transformação dados através de serviços como o Azure HDInsight e do Azure Machine Learning. Também pode agendar toorun de pipelines de dados no monitor e forma agendada (hora a hora, diária, semanal, etc.) e geri-los em problemas de tooidentify um rapidamente e tomar medidas.

Consulte Olá seguintes artigos se não estiver familiarizado com o Azure Data Factory como ajuda com compreender Olá arquitetura/implementação da solução de Olá descrita neste artigo.  

* [Introdução ao Azure Data Factory](data-factory-introduction.md)
* [Criar o seu primeiro pipeline de dados](data-factory-build-your-first-pipeline.md)   

(opcional) toolearn mais informações sobre o Azure Data Factory, consulte Olá [percurso de aprendizagem do Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).

## <a name="data-factory-and-batch-together"></a>Fábrica de dados e em conjunto do Batch
Fábrica de dados inclui atividades incorporadas, como o arquivo de dados de destino tooa e dados de tooprocess de atividade do ramo de registo utilizando clusters do Hadoop (HDInsight) no Azure do arquivo de dados de toocopy/mover de atividade de cópia de uma origem de dados. Consulte [atividades de transformação de dados](data-factory-data-transformation-activities.md) para uma lista de atividades de transformação suportados.

Também permite toocreate .NET atividades personalizadas toomove ou processo de dados com a sua própria lógica e executar estas atividades num cluster do HDInsight do Azure ou num conjunto de VMs do Azure Batch. Quando utilizar o Azure Batch, pode configurar o conjunto de Olá tooauto hiper escala (adicionar ou remover VMs com base na carga de trabalho Olá) com base numa fórmula que fornecer.     

## <a name="architecture-of-sample-solution"></a>Arquitetura de solução de exemplo
Apesar de arquitetura de Olá descrita neste artigo destina-se uma solução simples, é toocomplex relevantes cenários tais como a modelação de serviços financeiros, processamento de imagem e composição e análise genomic riscos.

Diagrama de Olá ilustra 1) como o Data Factory orquestra movimento de dados e processamento e 2) como o Azure Batch processa Olá dados de forma paralela. Transferir e diagrama de impressão Olá para fácil referência (11 x 17 pol. ou tamanho A3): [HPC e de dados orchestration através do Azure Batch e do Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).

[![Diagrama de processamento de dados em grande escala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)

Olá lista seguinte fornece os passos básicos Olá do processo de Olá. Olá inclui código de solução e de explicações toobuild Olá ponto-a-ponto.

1. **Configurar o Azure Batch com um conjunto de nós de computação (VMs)**. Pode especificar o número de Olá de nós e o tamanho de cada nó.
2. **Criar uma instância do Azure Data Factory** que está configurado com entidades que representam o blob storage do Azure, serviço de computação do Azure Batch, dados de entrada/saída e um fluxo de trabalho pipeline com atividades que mover e transforme dados.
3. **Criar uma atividade personalizada do .NET no pipeline do Data Factory Olá**. atividade de Olá é o código de utilizador que é executado no Olá conjunto do Azure Batch.
4. **Armazenar grandes quantidades de dados de entrada que os blobs no armazenamento do Azure**. Dados estão divididos em setores lógicas (normalmente por hora).
5. **Fábrica de dados copia os dados que estão a ser processados em paralelo** toohello de localização secundária.
6. **Fábrica de dados executa atividades personalizadas Olá utilizar agrupamento Olá atribuído pelo Batch**. Fábrica de dados pode ser executados atividades em simultâneo. Cada atividade processa um setor de dados. resultados de Olá são armazenados no armazenamento do Azure.
7. **Fábrica de dados move a localização de terceira Olá resultados final tooa**, para distribuição através de uma aplicação ou para processamento adicional por outras ferramentas.

## <a name="implementation-of-sample-solution"></a>Implementação da solução de exemplo
solução de exemplo de Olá é intencionalmente simple e é tooshow como toouse fábrica de dados e Batch tooprocess em conjunto os conjuntos de dados. solução Olá conta simplesmente o número de Olá de ocorrências de um termo de pesquisa ("Microsoft") nos ficheiros de entrada organizados de uma série de tempo. -Produz os ficheiros de toooutput Olá contagem.

**Tempo**: Se estiver familiarizado com as noções básicas do Azure, a fábrica de dados e o Batch e tem os pré-requisitos de Olá concluída listados abaixo, iremos fazer a estimativa esta solução assume toocomplete 1-2 horas.

### <a name="prerequisites"></a>Pré-requisitos
#### <a name="azure-subscription"></a>Subscrição do Azure
Se não tiver uma subscrição do Azure, pode criar uma conta de avaliação gratuita em apenas alguns minutos. Consulte [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="azure-storage-account"></a>Conta de armazenamento do Azure
Utilize uma conta de armazenamento do Azure para armazenar dados de Olá neste tutorial. Se não tiver uma conta de armazenamento do Azure, consulte o artigo [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account). solução de exemplo de Olá utiliza o armazenamento de Blobs.

#### <a name="azure-batch-account"></a>Conta de Batch do Azure
Criar uma conta do Azure Batch com Olá [portal do Azure](http://manage.windowsazure.com/). Consulte [criar e gerir uma conta do Azure Batch](../batch/batch-account-create-portal.md). Tenha em atenção Olá do Azure Batch e conta de nome de chave da conta. Também pode utilizar [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate uma conta do Azure Batch. Consulte [introdução aos cmdlets do Azure Batch PowerShell](../batch/batch-powershell-cmdlets-get-started.md) para obter instruções detalhadas sobre como utilizar este cmdlet.

solução de exemplo de Olá utiliza dados do Azure Batch (indiretamente através de um pipeline do Azure Data Factory) tooprocess de forma parallel num conjunto de nós de computação (coleção gerida de máquinas virtuais).

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a>Conjunto do Batch do Azure de máquinas virtuais (VMs)
Criar um **conjunto do Azure Batch** com, pelo menos, 2 nós de computação.

1. No Olá [portal do Azure](https://portal.azure.com), clique em **procurar** no Olá menu à esquerda e clique em **contas do Batch**.
2. Selecione o seu Olá de tooopen de conta do Azure Batch **conta do Batch** painel.
3. Clique em **agrupamentos** mosaico.
4. No Olá **agrupamentos** painel, clique em Adicionar botão na barra de ferramentas de Olá tooadd um conjunto.
   1. Introduza um ID para o conjunto de Olá (**ID do conjunto**). Olá nota **ID do conjunto de Olá**; apenas quando criar a solução de fábrica de dados de Olá.
   2. Especifique **Windows Server 2012 R2** para definição do Olá família do sistema operativo.
   3. Selecione um **escalão de preço de nó**.
   4. Introduza **2** como valor de Olá **destino dedicado** definição.
   5. Introduza **2** como valor de Olá **máx. tarefas por nó** definição.
   6. Clique em **OK** conjunto de Olá toocreate.

#### <a name="azure-storage-explorer"></a>Explorador do Storage do Azure
[6 do Explorador de armazenamento do Azure (ferramenta)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (a partir do ClumsyLeaf Software). Utilizar estas ferramentas para inspecionar e alteração de dados de Olá nos seus projetos de armazenamento do Azure, incluindo Olá os registos das suas aplicações alojadas na nuvem.

1. Criar um contentor com o nome **mycontainer** com acesso privado (sem acesso anónimo)
2. Se estiver a utilizar **CloudXplorer**, criar pastas e subpastas com Olá a seguir a estrutura:

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   `Inputfolder`e `outputfolder` são pastas de nível superior no `mycontainer`. Olá `inputfolder` tem subpastas com carimbos de data / hora (AAAA-MM-DD-HH).

   Se estiver a utilizar **Explorador de armazenamento do Azure**, no próximo passo Olá, terá de tooupload os ficheiros com nomes: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e assim sucessivamente. Este passo cria automaticamente a pastas Olá.
3. Criar um ficheiro de texto **file.txt** no seu computador com o conteúdo que tenha a palavra-chave de Olá **Microsoft**. Por exemplo: "atividades personalizadas do atividade personalizada Microsoft teste Microsoft de teste".
4. Carregar Olá ficheiro toohello seguir entradas pastas no armazenamento de Blobs do Azure.

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   Se estiver a utilizar **Explorador de armazenamento do Azure**, carregue o ficheiro de Olá **file.txt** demasiado**mycontainer**. Clique em **cópia** na barra de ferramentas de Olá toocreate uma cópia do blob Olá. No Olá **copiar Blob** caixa de diálogo, a alteração Olá **nome do blob de destino** demasiado`inputfolder/2015-11-16-00/file.txt`. Repita este passo toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e assim sucessivamente. Esta ação cria automaticamente a pastas Olá.
5. Criar outro contentor com o nome: `customactivitycontainer`. Carregue o contentor de toothis Olá atividade personalizada zip ficheiros.

#### <a name="visual-studio"></a>Visual Studio
Instale o Microsoft Visual Studio 2012 ou posterior toocreate Olá personalizado Batch atividade toobe utilizado no Olá solução Data Factory.

### <a name="high-level-steps-toocreate-hello-solution"></a>Solução de Olá toocreate de passos de alto nível
1. Crie uma atividade personalizada que contém a lógica de processamento de dados de Olá.
2. Crie um Azure data factory que utiliza a atividade personalizada Olá:

### <a name="create-hello-custom-activity"></a>Criar atividades personalizadas Olá
Olá atividade personalizada da fábrica de dados é heart Olá desta solução de exemplo. solução de exemplo de Olá utiliza a atividade personalizada do Azure Batch toorun Olá. Consulte [utilizar atividades personalizadas num pipeline do Azure Data Factory](data-factory-use-custom-activities.md) para Olá informações básicas toodevelop atividades e utilize-las no Azure Data Factory pipelines.

toocreate uma atividade personalizada do .NET que pode utilizar um pipeline do Azure Data Factory, tem de toocreate um **biblioteca de classe de .NET** projeto com uma classe que implementa que **IDotNetActivity** interface. Esta interface tem apenas um método: **executar**. Segue-se a assinatura do método Olá Olá:

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

o método de Olá tem alguns componentes principais que terá de toounderstand.

* método de Olá aceita quatro parâmetros:

  1. **linkedServices**. Uma lista enumeráveis de serviços ligados para ligar a origens de dados de entrada/saída (por exemplo: Blob Storage do Azure) toohello fábrica de dados. Neste exemplo, não há apenas um serviço ligado do tipo de armazenamento do Azure utilizados para a entrada e saída.
  2. **conjuntos de dados**. Esta é uma lista enumeráveis de conjuntos de dados. Pode utilizar este localizações do parâmetro tooget Olá e esquemas definidas conjuntos de dados de entrada e de saída.
  3. **atividade**. Este parâmetro representa Olá atual computação entidade - neste caso, um serviço Azure Batch.
  4. **registo**. permite de registo de Olá que escrever comentários de depuração esse superfície como Olá "Utilizador" iniciar sessão para Olá pipeline.
* método de Olá devolve um dicionário que pode ser utilizados toochain de atividades personalizadas em conjunto no futuro Olá. Esta funcionalidade ainda não está implementada, por isso, devolver um dicionário vazio do método Olá.

#### <a name="procedure-create-hello-custom-activity"></a>Procedimento: Criar atividades personalizadas Olá
1. Crie um projeto da biblioteca de classe de .NET no Visual Studio.

   1. Iniciar **Visual Studio 2012**/**2013/2015**.
   2. Clique em **ficheiro**, ponto demasiado**novo**e clique em **projeto**.
   3. Expanda **modelos**e selecione **Visual C\#**. Nestas instruções, utilizar o C\#, mas pode utilizar qualquer .NET idioma toodevelop Olá atividade personalizada.
   4. Selecione **biblioteca de classes** da lista de Olá dos tipos de projeto no Olá à direita.
   5. Introduza **MyDotNetActivity** para Olá **nome**.
   6. Selecione **c:\\ADF** para Olá **localização**. Criar a pasta de Olá **ADF** se não existir.
   7. Clique em **OK** projeto de Olá toocreate.
2. Clique em **ferramentas**, ponto demasiado**Gestor de pacotes NuGet**e clique em **consola do Gestor de pacotes**.
3. No Olá **consola do Gestor de pacotes**, executar Olá os seguintes comandos tooimport **Microsoft.Azure.Management.DataFactories**.

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. Olá importação **Storage do Azure** pacote NuGet no projeto toohello. Este pacote tem porque utiliza a API de armazenamento de BLOBs de Olá neste exemplo.

    ```powershell
    Install-Package Azure.Storage
    ```
5. Adicione Olá seguinte **utilizando** ficheiro de origem toohello diretivas no projeto Olá.

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. Nome de Olá de alteração de Olá **espaço de nomes** demasiado**MyDotNetActivityNS**.

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. Alterar o nome de Olá da classe de Olá demasiado**MyDotNetActivity** e derivar-Olá **IDotNetActivity** interface conforme mostrado abaixo.

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. Olá implementar (adicionar) **executar** método de Olá **IDotNetActivity** interface toohello **MyDotNetActivity** Olá classe e copie o método de toohello do código de exemplo a seguir. Consulte Olá [executar o método](#execute-method) secção para obter explicações para a lógica de Olá utilizada este método.

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. Adicione a seguinte classe de toohello de métodos de programa auxiliar de Olá. Estes métodos são invocados pelo Olá **executar** método. Mais importante ainda, Olá **Calculate** método isola código Olá itera através de cada blob.

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    Olá **GetFolderPath** método devolve pasta do Olá caminho toohello esse Olá de tooand de pontos de conjunto de dados de Olá **GetFileName** método devolve o nome de Olá de Olá/ficheiro blob que Olá pontos de conjunto de dados.

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    Olá **Calculate** método calcula o número de Olá de instâncias de palavra-chave **Microsoft** no Olá os ficheiros de entrada (blobs na pasta Olá). o termo de pesquisa de Olá ("Microsoft") é "hard-coded" no código Olá.

1. Compile o projeto de Olá. Clique em **criar** no menu de Olá e clique em **compilar solução**.
2. Iniciar **Explorador do Windows**e navegue demasiado**bin\\depurar** ou **bin\\versão** pasta, dependendo do tipo de Olá de compilação.
3. Criar um ficheiro zip **MyDotNetActivity.zip** que contém todos os binários de Olá no Olá  **\\bin\\depurar** pasta. Poderá pretender tooinclude Olá MyDotNetActivity. **pdb** para que obtenha detalhes adicionais, tais como o número de linha no código fonte Olá que causou o problema de Olá quando ocorre uma falha de ficheiros.

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. Carregar **MyDotNetActivity.zip** como um contentor de blob do blob toohello: `customactivitycontainer` no Olá Azure armazenamento de BLOBs que Olá **StorageLinkedService** serviço no Olá ligado  **ADFTutorialDataFactory** utiliza. Criar contentor de blob Olá `customactivitycontainer` se já existir.

#### <a name="execute-method"></a>Executar o método
Esta secção fornece mais detalhes e notas sobre o código de Olá no Olá método de execução.

1. os membros de Olá para repetir a coleção de entrada Olá encontram Olá [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) espaço de nomes. Repetir a coleção de blob Olá requer a utilização Olá **BlobContinuationToken** classe. Essencialmente, tem de utilizar um efetue-ao ciclo com token Olá como mecanismo de Olá para sair do ciclo de Olá. Para obter mais informações, consulte [como toouse Blob storage do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Um ciclo básico é mostrado aqui:

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   Consulte a documentação de Olá para Olá [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) método para obter mais detalhes.
2. Olá código para funcionar através de conjunto de Olá de blobs logicamente fica dentro Olá fazer-ao ciclo. No Olá **executar** método, efetue de Olá-enquanto ciclo transmite lista Olá de blobs com o nome de método de tooa **Calculate**. método de Olá devolve uma variável de cadeia denominada **saída** que Olá resultado ter iterated através de todos os blobs Olá no segmento Olá.

   -Devolve o número de Olá de ocorrências do termo de pesquisa de Olá (**Microsoft**) num blob Olá transmitido toohello **Calculate** método.

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. Uma vez Olá **Calculate** método tem de terminar o trabalho de Olá, têm de ser escrito tooa blob de novo. Por isso, para cada conjunto de blobs processados, um novo blob pode ser escrito com resultados de Olá. toowrite tooa novos BLOBs, primeiro localizar o Olá saída dataset.

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. Olá também chama um método de programa auxiliar: **GetFolderPath** caminho da pasta tooretrieve Olá (nome do contentor de armazenamento de Olá).

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   Olá **GetFolderPath** casts Olá tooan de objeto do conjunto de dados AzureBlobDataSet, que tem uma propriedade chamada FolderPath.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. Olá código chamadas Olá **GetFileName** nome do ficheiro do método tooretrieve Olá (nome do blob). código de Olá é semelhante toohello acima caminho da pasta do código tooget Olá.

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. Olá o nome do ficheiro de Olá é escrito através da criação de um objeto URI. o construtor URI Olá utiliza Olá **BlobEndpoint** nome da propriedade tooreturn Olá contentor. nome de ficheiro e caminho da pasta Olá são adicionados URI de blob tooconstruct Olá saída.  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. nome de Olá do ficheiro de Olá foi escrito e agora pode escrever Olá cadeia da saída de Olá **Calculate** blob novo do método tooa:

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a>Criar fábrica de dados de Olá
No Olá [criar atividades personalizadas Olá](#create-the-custom-activity) secção, criou uma atividade personalizada e o ficheiro zip Olá carregado com os binários e Olá PDB ficheiros tooan contentor de Blobs do Azure. Nesta secção, vai criar um Azure **fábrica de dados** com um **pipeline** que utiliza Olá **atividade personalizada**.

Olá o conjunto de dados de entrada para a atividade personalizada Olá representa blobs Olá (ficheiros) na pasta de entrada Olá (`mycontainer\\inputfolder`) no armazenamento de Blobs. Olá conjunto de dados de saída para a atividade de Olá representa Olá saída blobs na pasta de saída Olá (`mycontainer\\outputfolder`) no armazenamento de Blobs.

Remova um ou mais ficheiros em pastas de entrada Olá:

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

Por exemplo, remova um ficheiro (file.txt) com Olá seguir o conteúdo para cada uma das pastas de Olá.

```
test custom activity Microsoft test custom activity Microsoft
```

Cada pasta de entrada corresponde setor tooa no Azure Data Factory, mesmo se tiver de pasta Olá 2 ou mais ficheiros. Quando cada setor é processado pelo pipeline Olá, atividade personalizada Olá itera através de todos os blobs Olá na pasta de entrada Olá para esse setor.

Consulte a saída cinco ficheiros com Olá mesmo conteúdo. Por exemplo, o ficheiro de saída de Olá de processar o ficheiro de Olá na pasta de Olá 2015-11-16-00 tem Olá seguinte conteúdo:

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

Se remover vários ficheiros (file.txt file2.txt, file3.txt) com Olá de pasta de entrada toohello mesmo conteúdo, consulte Olá seguir o conteúdo no ficheiro de saída Olá. Cada pasta (2015-11-16-00, etc.) corresponde tooa setor neste exemplo, apesar de pasta de Olá tem vários ficheiros de entrada.

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

ficheiro de saída de Olá tem três linhas agora, um para cada ficheiro de entrada (blob) na pasta Olá associado setor Olá (2015-11-16-00).

Uma tarefa é criada para cada execução da atividade. Neste exemplo, não há apenas uma atividade no pipeline de Olá. Quando um setor é processado pelo pipeline Olá, atividade personalizada Olá é executado no setor da Olá tooprocess do Azure Batch. Uma vez que existem cinco setores (cada setor pode ter vários blobs ou ficheiro), existem cinco tarefas criadas no Azure Batch. Quando é executada uma tarefa do batch, está efetivamente Olá atividade personalizada que está em execução.

Olá instruções a seguir fornece detalhes adicionais.

#### <a name="step-1-create-hello-data-factory"></a>Passo 1: Criar a fábrica de dados de Olá
1. Após iniciar sessão toohello [portal do Azure](https://portal.azure.com/), Olá os seguintes passos:

   1. Clique em **novo** no menu à esquerda Olá.
   2. Clique em **dados + análise** no Olá **novo** painel.
   3. Clique em **Data Factory** no Olá **análise de dados** painel.
2. No Olá **nova fábrica de dados** painel, introduza **CustomActivityFactory** para Olá nome. nome de Olá do Olá do Azure data factory deve ser globalmente exclusivo. Se receber o erro de Olá: **nome da fábrica de dados "CustomActivityFactory" não está disponível**, altere Olá nome da fábrica de dados de Olá (por exemplo, **yournameCustomActivityFactory**) e tente criar novamente.
3. Clique em **nome do grupo de recursos**e selecione um grupo de recursos existente ou crie um grupo de recursos.
4. Certifique-se de que está a utilizar a subscrição correta Olá e região onde pretende toobe de fábrica de dados de Olá criado.
5. Clique em **criar** no Olá **nova fábrica de dados** painel.
6. Consulte a fábrica de dados de Olá a ser criada no Olá **Dashboard** de Olá portal do Azure.
7. Depois de Olá a fábrica de dados foi criada com êxito, será apresentada a página de fábrica do Olá dados, que mostra-lhe Olá conteúdos da fábrica de dados de Olá.

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a>Passo 2: Criar serviços ligados
Os serviços ligados ligam os arquivos de dados ou fábrica de dados do Azure tooan de serviços de computação. Neste passo, ligue o **Storage do Azure** conta e **do Azure Batch** fábrica de dados de tooyour de conta.

#### <a name="create-azure-storage-linked-service"></a>Criar o serviço ligado do Storage do Azure
1. Clique em Olá **autor e implementar** mosaico Olá **DATA FACTORY** painel **CustomActivityFactory**. Consulte Olá Editor do Data Factory.
2. Clique em **novo arquivo de dados** na barra de comando de Olá e escolha **storage do Azure.** Deverá ver Olá script JSON para criar um Storage do Azure ligado serviço num editor de Olá.

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. Substitua **nome da conta** com o nome de Olá da sua conta de armazenamento do Azure e **chave da conta** com a chave de acesso de Olá de Olá conta do storage do Azure. toolearn como tooget seu armazenamento aceder à chave, consulte [chaves de acesso de ver, copiar e voltar a gerar armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

4. Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a>Criar o serviço ligado do Azure Batch
Neste passo, vai criar um serviço ligado para sua **do Azure Batch** conta que seja utilizado toorun fábrica de dados de Olá atividade personalizada.

1. Clique em **nova computação** na barra de comando de Olá e escolha **do Azure Batch.** Deverá ver Olá script JSON para criar um Azure Batch ligado serviço num editor de Olá.
2. No Olá script JSON:

   1. Substitua **nome da conta** com o nome de Olá da sua conta do Azure Batch.
   2. Substitua **chave de acesso** com a chave de acesso de Olá de Olá conta do Azure Batch.
   3. Introduza o ID de Olá do conjunto de Olá para Olá **poolName** propriedade**.** Para esta propriedade, pode especificar o nome do conjunto ou agrupamento ID.
   4. Introduza o lote de Olá URI para Olá **batchUri** propriedade JSON.

      > [!IMPORTANT]
      > Olá **URL** de Olá **painel de conta do Azure Batch** está a ser Olá seguinte formato: \<accountname\>.\< região\>. batch.azure.com. Para Olá **batchUri** propriedade no Olá JSON, terá de demasiado**remover "accountname."** do URL de Olá. Exemplo: `"batchUri": "https://eastus.batch.azure.com"`.
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      Para Olá **poolName** propriedade, também pode especificar Olá ID do conjunto de Olá em vez do nome de Olá do conjunto de Olá.

      > [!NOTE]
      > Olá serviço fábrica de dados não suporta uma opção a pedido para o Azure Batch como para o HDInsight. Só pode utilizar o seu próprio conjunto do Azure Batch num Azure data factory.
      >
      >
   5. Especifique **StorageLinkedService** para Olá **linkedServiceName** propriedade. Este serviço ligado que criou no passo anterior Olá. Este tipo de armazenamento é utilizado como uma área de transição para ficheiros e registos.
3. Clique em **implementar** no comando Olá barra toodeploy Olá ligado serviço.

#### <a name="step-3-create-datasets"></a>Passo 3: Criar conjuntos de dados
Neste passo, criar toorepresent de conjuntos de dados de entrada e saída de dados.

#### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
1. No Olá **Editor** para Olá Data Factory, clique em **novo conjunto de dados** botão na toolbar Olá e clique em **Blob storage do Azure** no menu de Olá pendente.
2. Substitua Olá JSON no painel direito Olá Olá seguinte fragmento JSON:

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    Pode cria um pipeline mais tarde esta explicação passo a passo com a hora de início: 2015-11-tempo 16T00:00:00Z e de fim: 2015-11-16T05:00:00Z. É agendada tooproduce dados **hora a hora**, pelo que existem 5 setores de entrada/saída (entre **00**: 00:00 -\> **05**: 00:00).

    Olá **frequência** e **intervalo** para o conjunto de dados de entrada Olá estiver definido demasiado**hora** e **1**, que significa que Olá entrada setor está disponível hora a hora.

    Seguem-se Olá horas de início cada setor, que são representadas por **SliceStart** variável de sistema no Olá acima fragmento JSON.

    | **Setor** | **Hora de início**          |
    |-----------|-------------------------|
    | 1         | 2015-11-16T**00**: 00:00 |
    | 2         | 2015-11-16T**01**: 00:00 |
    | 3         | 2015-11-16T**02**: 00:00 |
    | 4         | 2015-11-16T**03**: 00:00 |
    | 5         | 2015-11-16T**04**: 00:00 |

    Olá **folderPath** é calculado utilizando a parte ano, mês, dia e hora Olá Olá setor da hora de início (**SliceStart**). Por conseguinte, aqui é a forma como uma pasta de entrada setor tooa mapeada.

    | **Setor** | **Hora de início**          | **Pasta de entrada**  |
    |-----------|-------------------------|-------------------|
    | 1         | 2015-11-16T**00**: 00:00 | 2015-11-16-**00** |
    | 2         | 2015-11-16T**01**: 00:00 | 2015-11-16-**01** |
    | 3         | 2015-11-16T**02**: 00:00 | 2015-11-16-**02** |
    | 4         | 2015-11-16T**03**: 00:00 | 2015-11-16-**03** |
    | 5         | 2015-11-16T**04**: 00:00 | 2015-11-16-**04** |

1. Clique em **implementar** no Olá toocreate da barra de ferramentas e implementar Olá **InputDataset** tabela.

#### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Neste passo, crie outro conjunto de dados do tipo AzureBlob toorepresent Olá dados de saída.

1. No Olá **Editor** para Olá Data Factory, clique em **novo conjunto de dados** botão na toolbar Olá e clique em **Blob storage do Azure** no menu de Olá pendente.
2. Substitua Olá JSON no painel direito Olá Olá seguinte fragmento JSON:

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    Um ficheiro/blob de saída é gerado para cada setor de entrada. Eis como um ficheiro de saída é designado para cada setor. Todos os ficheiros de saída de Olá são gerados por uma pasta de saída: `mycontainer\\outputfolder`.

    | **Setor** | **Hora de início**          | **Ficheiro de saída**       |
    |-----------|-------------------------|-----------------------|
    | 1         | 2015-11-16T**00**: 00:00 | 2015-11-16 -**00. txt** |
    | 2         | 2015-11-16T**01**: 00:00 | 2015-11-16 -**01. txt** |
    | 3         | 2015-11-16T**02**: 00:00 | 2015-11-16 -**02. txt** |
    | 4         | 2015-11-16T**03**: 00:00 | 2015-11-16 -**03. txt** |
    | 5         | 2015-11-16T**04**: 00:00 | 2015-11-16 -**04. txt** |

    Lembre-se de que todos os ficheiros numa pasta entrada de Olá (por exemplo: 2015-11-16-00) fazem parte de um setor com a hora de início Olá: 2015-11-16-00. Quando este setor é processado, atividade personalizada Olá analisa através de cada ficheiro e produz uma linha no ficheiro de saída de Olá com o número de Olá de ocorrências do termo de pesquisa ("Microsoft"). Se existirem três ficheiros na pasta Olá 2015-11-16-00, existem três linhas no ficheiro de saída Olá: 2015-11-16-00.txt.

1. Clique em **implementar** no Olá toocreate da barra de ferramentas e implementar Olá **OutputDataset**.

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a>Passo 4: Criar e executar o pipeline de Olá com atividade personalizada
Neste passo, vai criar um pipeline com uma atividade, atividade personalizada Olá que criou anteriormente.

> [!IMPORTANT]
> Se ainda não adicionou Olá **file.txt** tooinput pastas no contentor de blob Olá, fazê-lo antes de criar o pipeline de Olá. Olá **isPaused** propriedade é definida toofalse na Olá JSON do pipeline, para o pipeline de Olá seja executada imediatamente como Olá **iniciar** data está no passado Olá.
>
>

1. No Editor do Data Factory Olá, clique em **novo pipeline** na barra de comandos Olá. Se não vir comando Olá, clique em **... (Reticências)**  toosee-lo.
2. Substitua Olá JSON no painel direito Olá Olá seguinte script JSON:

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   Tenha em atenção Olá seguintes pontos:

   * Não existe apenas uma atividade no pipeline de Olá e que é do tipo: **DotNetActivity**.
   * **AssemblyName** é definir nome toohello Olá DLL: **MyDotNetActivity.dll**.
   * **EntryPoint** estiver definido demasiado**MyDotNetActivityNS.MyDotNetActivity**. É basicamente \<espaço de nomes\>.\< ClassName\> no seu código.
   * **PackageLinkedService** estiver definido demasiado**StorageLinkedService** que aponta de armazenamento de BLOBs de toohello que contém o ficheiro zip do Olá atividade personalizada. Se estiver a utilizar diferentes contas de armazenamento do Azure para ficheiros de entrada/saída e o ficheiro zip do Olá atividade personalizada, terá de toocreate outro armazenamento do Azure serviço ligado. Este artigo assume que está a utilizar Olá a mesma conta de armazenamento do Azure.
   * **PackageFile** estiver definido demasiado**customactivitycontainer/MyDotNetActivity.zip**. Está no formato de Olá: \<containerforthezip\>/\<nameofthezip.zip\>.
   * atividade personalizada Olá demora **InputDataset** como entrada e **OutputDataset** como saída.
   * Olá **linkedServiceName** propriedade de atividade personalizado Olá aponta toohello **AzureBatchLinkedService**, que informa a Azure Data Factory dessa atividade personalizada Olá tem toorun do Azure batch.
   * Olá **simultaneidade** definição é importante. Se utilizar o valor predefinido de Olá, que é 1, mesmo se tiver de 2 ou mais nós de computação num conjunto do Azure Batch de Olá, são processados de setores de Olá umas a seguir. Por conseguinte, não são tirar partido da capacidade de processamento paralelo de Olá do Azure Batch. Se definir **simultaneidade** tooa valor mais alto, diga 2, significa que dois setores (corresponde tootwo tarefas no Azure Batch) podem ser processados em Olá mesmo tempo, caso em que ambas as VMs de Olá no Olá do Azure Batch são utilizados de agrupamento. Por conseguinte, defina a propriedade de simultaneidade de Olá adequadamente.
   * Por predefinição, apenas uma tarefa (setor) é executada numa VM em qualquer momento. Olá razão é que, por predefinição, hello **máximo de tarefas por VM** está definido too1 para um conjunto do Azure Batch. Como parte da pré-requisitos, criou um conjunto com este too2 de conjunto de propriedade para duas setores de fábrica de dados podem estar em execução numa VM em Olá mesmo tempo.

    -   **isPaused** propriedade está definida toofalse por predefinição. pipeline de Olá executa imediatamente neste exemplo, porque setores Olá iniciar no Olá passado. Pode definir o pipeline do Olá tootrue toopause esta propriedade e defini-lo toorestart toofalse anterior.

    -   Olá **iniciar** tempo e **final** vezes são, à excepção de cinco horas e setores são produzidos de hora a hora, pelo que os cinco setores são produzidos pelo pipeline Olá.

1. Clique em **implementar** no comando Olá barra pipeline de Olá toodeploy.

#### <a name="step-5-test-hello-pipeline"></a>Passo 5: Testar o pipeline de Olá
Neste passo, teste pipeline Olá, arrastando ficheiros em pastas Olá de entrada. Vamos começar com o pipeline de Olá teste com um ficheiro por uma pasta de entrada.

1. No painel de fábrica de dados de Olá no Olá portal do Azure, clique em **diagrama**.

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. Na vista de diagrama Olá, faça duplo clique em conjunto de dados de entrada: **InputDataset**.

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. Deverá ver Olá **InputDataset** painel com todos os cinco setores pronto. Olá aviso **hora de início do SETOR** e **hora de fim de SETOR** para cada setor.

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. No Olá **vista de diagrama**, agora, clique em **OutputDataset**.
5. Deverá ver que os setores de saída cinco Olá estão no estado pronto Olá se que já foram produzidos.

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. Olá tooview portal do Azure de utilização **tarefas** associado Olá **setores** e ver que VM cada setor é executado no. Consulte [integração com o Data Factory e Batch](#data-factory-and-batch-integration) secção para obter detalhes.
7. Deverá ver ficheiros de saída de Olá no Olá `outputfolder` de `mycontainer` no seu Azure armazenamento de Blobs.

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   Deverá ver cinco ficheiros de saída, uma para cada setor de entrada. Cada um dos Olá de saída do ficheiro deve ter conteúdo toohello semelhante seguinte saída:

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   Olá diagrama seguinte ilustra como setores de fábrica de dados de Olá mapeiam tootasks no Azure Batch. Neste exemplo, um setor tem apenas uma execução.

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. Agora, vamos tentar com vários ficheiros numa pasta. Criar ficheiros: **file2.txt**, **file3.txt**, **file4.txt**, e **file5.txt** com Olá mesmo conteúdo, tal como em file.txt na pasta Olá: **2015-11-06-01**.
9. Na pasta de saída Olá, **eliminar** Olá o ficheiro de saída: **2015-11-16-01.txt**.
10. Agora, no Olá **OutputDataset** painel, o setor de Olá contexto com **hora de início do SETOR** definido demasiado**11/16/2015 01:00:00 AM**e clique em **executar**setor Olá toorerun/re-process. Agora, o setor de Olá tem cinco ficheiros em vez de um ficheiro.

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. Depois de setor de Olá é executado e o respetivo estado é **pronto**, verifique o conteúdo de Olá no ficheiro de saída de Olá neste setor (**2015-11-16-01.txt**) no Olá `outputfolder` de `mycontainer` no seu armazenamento de Blobs. Deve ser uma linha para cada ficheiro de setor de Olá.

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> Se não eliminou o 2015 de ficheiro da saída Olá-11-16-01.txt antes de tentar com cinco ficheiros de entrada, verá uma linha de setor anterior Olá executar e cinco linhas de setor atual Olá executar. Por predefinição, o conteúdo de Olá é anexado toooutput ficheiro se já existir.
>
>

#### <a name="data-factory-and-batch-integration"></a>Integração de fábrica de dados e de Batch
Olá serviço Data Factory cria uma tarefa no Azure Batch com o nome de Olá: `adf-poolname:job-xxx`.

![O Azure Data Factory - tarefas do Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

É criada uma tarefa na tarefa de Olá para cada execução de atividade de um setor. Se existirem toobe pronto 10 do setores, processados, são criadas 10 tarefas na tarefa de Olá. Pode ter mais do que um setor ser executado em paralelo se tiver vários nós de computação no conjunto de Olá. Se Olá máximo por computação nó estiver definido demasiado > 1, podem existir mais do que um setor a ser executado no Olá computação mesma.

Neste exemplo, existem cinco setores, por isso, cinco tarefas no Azure Batch. Com Olá **simultaneidade** definido demasiado**5** no Olá pipeline JSON no Azure Data Factory e **máximo de tarefas por VM** definido demasiado**2** no Azure Batch conjunto com **2** VMs, Olá tarefas é executado rápida (Verifique os tempos de início e de fim para tarefas).

Utilize a tarefa de lote do Olá portal tooview Olá e as respetivas tarefas associadas Olá **setores** e ver que VM cada setor é executado no.

![O Azure Data Factory - tarefas de lote](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a>Depurar o pipeline de Olá
A depuração inclui algumas técnicas básicas:

1. Se o setor de entrada Olá não estiver definido demasiado**pronto**, confirmar que a estrutura de entrada de pasta Olá está correta e file.txt existe nas pastas de entrada Olá.

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. No Olá **executar** método da atividade personalizada, utilize Olá **IActivityLogger** informações do objeto toolog que o ajuda a resolver problemas. mensagens Hello registado apareçam no utilizador Olá\_0. ficheiro de registo.

   No Olá **OutputDataset** painel, clique em Olá do Olá setor toosee **SETOR de dados** painel para essa setor. Verá **execuções de atividade** para esse setor. Deverá ver uma atividade executar o setor de Olá. Se clicar em **executar** na barra de comando Olá, pode começar a outra atividade executada para Olá setor mesmo.

   Ao clicar em execução da atividade Olá, consulte Olá **detalhes da execução da ATIVIDADE** painel com uma lista de ficheiros de registo. Consulte as mensagens anteriormente registadas no Olá **utilizador\_0. registo** ficheiro. Quando ocorre um erro, consulte três execuções de atividade porque Olá contagem de repetições está definida too3 Olá pipeline/atividade JSON. Ao clicar em execução da atividade Olá, consulte os ficheiros de registo Olá que pode rever o erro de Olá tootroubleshoot.

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   Na lista de Olá dos ficheiros de registo, clique em Olá **utilizador 0.log**. No painel à direita Olá são Olá os resultados da utilizando Olá **IActivityLogger.Write** método.

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   Verifique o sistema-0.log para quaisquer mensagens de erro de sistema e exceções.

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. Incluir Olá **PDB** ficheiro no ficheiro zip de Olá, para que os detalhes do erro Olá tem informações como **pilha de chamadas** quando ocorre um erro.
4. Todos os Olá ficheiros no ficheiro zip de Olá para a atividade personalizada Olá tem de estar no Olá **principais nível** com sem subpastas.

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. Certifique-se de que Olá **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), e **packageLinkedService** (deve Azure toohello de ponto de armazenamento de BLOBs que contém o ficheiro zip Olá) estão definidos valores toocorrect.
6. Se corrigido um erro e pretender setor de Olá tooreprocess, faça duplo clique setor de Olá no Olá **OutputDataset** painel e clique em **executar**.

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > Verá um **contentor** no seu armazenamento de Blobs do Azure com o nome: `adfjobs`. Este contentor não é eliminado automaticamente, mas pode eliminar em segurança depois de terminar a solução de Olá teste. Da mesma forma, Olá solução Data Factory cria um Azure Batch **tarefa** com o nome: `adf-\<pool ID/name\>:job-0000000001`. É possível eliminar esta tarefa depois de testar solução Olá se assim o desejar.
   >
   >
7. atividade personalizada Olá não utiliza Olá **App. config** ficheiro a partir do seu pacote. Por conseguinte, se o seu código lê quaisquer cadeias de ligação do ficheiro de configuração de Olá, não funciona no tempo de execução. Olá melhor prática quando utilizar o Azure Batch é toohold qualquer segredos num **Azure KeyVault**, utilize um keyvault de Olá de principal tooprotect de serviço baseada em certificado e distribuir conjunto do Batch Olá certificado tooAzure. Olá atividade personalizada do .NET, em seguida, pode aceder a segredos do Olá KeyVault no tempo de execução. Esta solução é um genérico e pode dimensionar o tipo de tooany do segredo, não apenas a cadeia de ligação.

    Há uma solução mais fácil (mas não uma boa prática): pode criar um **serviço ligado de SQL do Azure** com as definições de cadeia de ligação, criar um conjunto de dados que utiliza Olá serviço ligado e o conjunto de dados de cadeia Olá como um conjunto de dados de entrada fictício atividade de .NET personalizada toohello. Pode, em seguida, Olá de acesso associados a cadeia de ligação do serviço no código de atividade personalizado Olá e deverão funcionar ajustar no tempo de execução.  

#### <a name="extend-hello-sample"></a>Expandir o exemplo de Olá
Pode expandir este exemplo toolearn mais informações sobre as funcionalidades do Azure Data Factory e do Azure Batch. Por exemplo, Olá tooprocess setores um intervalo de hora diferente, os seguintes passos:

1. Adicionar Olá seguir subpastas na Olá `inputfolder`: 2015-11-16-05, 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 e coloque ficheiros de entrada nessas pastas. Alterar a hora de fim do pipeline de Olá do Olá `2015-11-16T05:00:00Z` demasiado`2015-11-16T10:00:00Z`. No Olá **vista de diagrama**, faça duplo clique em Olá **InputDataset**e confirme que os setores de entrada Olá estão prontos. Faça duplo clique em **OuptutDataset** toosee Estado Olá setores de saída. Se forem no estado pronto, verifique a pasta de saída de Olá para ficheiros de saída Olá.
2. Aumentar ou diminuir Olá **simultaneidade** definição toounderstand a forma como os afeta o desempenho de Olá da sua solução, especialmente Olá processamento que ocorre no Azure Batch. (Consulte o passo 4: criar e executar o pipeline de Olá para obter mais informações sobre Olá **simultaneidade** definição.)
3. Criar um conjunto com maior/menor **máximo de tarefas por VM**. toouse Olá novo conjunto que criou, Olá de atualização de serviço ligado do Azure Batch na solução de fábrica de dados de Olá. (Consulte o passo 4: criar e executar o pipeline de Olá para obter mais informações sobre Olá **máximo de tarefas por VM** definição.)
4. Criar um conjunto do Azure Batch com **dimensionamento automático** funcionalidade. Dimensionar automaticamente nós de computação num conjunto do Azure Batch é ajustamento dinâmico do Olá do processamento de energia utilizada pela sua aplicação. 

    fórmula de exemplo de Olá aqui distribui Olá seguinte comportamento: quando o conjunto de Olá for criado inicialmente, começa com 1 VM. Métrica de $PendingTasks define o número de Olá das tarefas em execução + Active Directory (em fila) Estado.  a fórmula Olá localiza Olá o número médio de tarefas pendentes na Olá último segundos 180 e define TargetDedicated em conformidade. Garante que nunca chegam TargetDedicated para além de 25 VMs. Por isso, são submetidas novas tarefas, agrupamento automaticamente o crescimentos e as tarefas são concluídas, as VMs fiquem livre um a um e o dimensionamento automático de Olá diminui dessas VMs. startingNumberOfVMs e maxNumberofVMs podem ser ajustada tooyour necessidades.
 
    Fórmula de dimensionamento automático:

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   Consulte [automaticamente Dimensionar nós de computação num conjunto do Azure Batch](../batch/batch-automatic-scaling.md) para obter mais detalhes.

   Se o conjunto de Olá estiver a utilizar predefinição de Olá [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Olá serviço Batch pode demorar 15-30 minutos tooprepare Olá VM antes de executar a atividade personalizada Olá.  Se o conjunto de Olá estiver a utilizar um autoScaleEvaluationInterval diferentes, Olá serviço Batch pode demorar autoScaleEvaluationInterval + 10 minutos.
5. Na solução de exemplo de Olá, Olá **executar** invoca o método Olá **Calculate** método que processe um tooproduce de setor de dados de entrada um setor de dados de saída. Pode escrever o seu próprio método tooprocess dados de entrada e substitua chamada de método Calculate Olá no método de execução de Olá com um método de tooyour de chamada.

### <a name="next-steps-consume-hello-data"></a>Próximos passos: consumir dados Olá
Depois de processar dados, pode consumi-lo com ferramentas online como **Microsoft Power BI**. Seguem-se toohelp ligações compreender o Power BI e como toouse-lo no Azure:

* [Explore um conjunto de dados no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [Introdução ao hello do Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [Atualizar dados no Power BI](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [Azure e o Power BI - descrição geral básica](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a>Referências
* [Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)

  * [Introdução tooAzure serviço Data Factory](data-factory-introduction.md)
  * [Introdução ao Azure Data Factory](data-factory-build-your-first-pipeline.md)
  * [Utilizar atividades personalizadas num pipeline do Azure Data Factory (Use custom activities in an Azure Data Factory pipeline)](data-factory-use-custom-activities.md)
* [O Azure Batch](https://azure.microsoft.com/documentation/services/batch/)

  * [Noções básicas do Azure Batch](../batch/batch-technical-overview.md)
  * [Descrição geral das funcionalidades do Azure Batch](../batch/batch-api-basics.md)
  * [Criar e gerir a conta do Azure Batch no portal do Azure de Olá](../batch/batch-account-create-portal.md)
  * [Introdução à biblioteca .NET do Azure Batch](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
