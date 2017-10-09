---
title: dados de aaaExplore no Azure blob storage com Pandas | Microsoft Docs
description: Como tooexplore dados armazenados no Azure contentor de blob Pandas a utilizar.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Explorar dados no Armazenamento de Blobs do Azure com o Pandas
Este documento abrange como tooexplore dados armazenados no Azure blob contentor utilizando [Pandas](http://pandas.pydata.org/) pacote do Python.

seguinte Olá **menu** liga tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento. Esta tarefa é um passo Olá [o processo de ciência de dados]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que tem:

* Criar uma conta de armazenamento do Azure. Se precisar de instruções, consulte [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Armazenados os dados numa conta de armazenamento de Blobs do Azure. Se precisar de instruções, consulte [mover dados tooand do armazenamento do Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Carregar dados de Olá para um DataFrame Pandas
tooexplore e manipular um conjunto de dados, primeiro deve ser transferido a partir Olá blob tooa local ficheiro de origem, que, em seguida, pode ser carregado num DataFrame Pandas. Seguem-se passos de Olá toofollow para este procedimento:

1. Transferir dados Olá a partir do Azure blob com Olá seguinte exemplo de código de Python com o serviço blob. Substitua a variável de Olá no Olá código com os seus valores específicos a seguir: 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. Ler Olá dados para um intervalo de dados Pandas de Olá transferidos ficheiros.
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Agora, os dados de Olá tooexplore pronto e gerar funcionalidades neste conjunto de dados.

## <a name="blob-dataexploration"></a>Exemplos de exploração de dados utilizando Pandas
Seguem-se alguns exemplos de formas dados tooexplore Pandas a utilizar:

1. Inspecione Olá **número de linhas e colunas** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Inspecione** Olá algumas primeira ou últimas **linhas** no Olá seguinte conjunto de dados:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Verifique Olá **tipo de dados** cada coluna foi importada como utilizar o seguinte código de exemplo de Olá
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Verifique Olá **estatísticas básicas** para colunas de Olá na Olá conjunto de dados da seguinte forma
   
        dataframe_blobdata.describe()
5. Observe o número de Olá de entradas para cada valor de coluna da seguinte forma
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Contagem de valores em falta** versus número real de Olá de entradas em cada coluna utilizando o seguinte código de exemplo de Olá
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Se tiver **valores em falta** para uma coluna específica nos dados de Olá, pode colocá-los da seguinte forma:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape
   
   Outra forma tooreplace os valores em falta é com a função de modo Olá:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna ({< nome_coluna >: .mode()[0]}) dataframe_blobdata ['< nome_coluna >']        
8. Criar um **histograma** desenhar utilizando variável número de intervalos binários tooplot Olá distribuição uma variável    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Observe **correlações** entre variáveis utilizando um scatterplot ou função de correlação incorporada Olá
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

