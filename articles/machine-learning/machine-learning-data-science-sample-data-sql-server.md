---
title: aaaSample dados no SQL Server no Azure | Microsoft Docs
description: Dados de exemplo no SQL Server no Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Dados de exemplo no SQL Server no Azure
Este documento mostra como toosample dados armazenados no SQL Server no Azure com o SQL Server ou Olá linguagem de programação do Python. Também mostra como toomove amostragem dados no Azure Machine Learning ao guardá-lo ficheiro tooa, carregá-lo tooan BLOBs do Azure e, em seguida, ao ler para o Azure Machine Learning Studio.

a amostragem de Python Olá utiliza Olá [pyodbc](https://code.google.com/p/pyodbc/) ODBC biblioteca tooconnect tooSQL Server no Azure e Olá [Pandas](http://pandas.pydata.org/) amostragem de Olá toodo de biblioteca.

> [!NOTE]
> código de SQL de exemplo de Olá este documento assume que Olá dados estão a ser um servidor de SQL no Azure. Se não estiver, consulte demasiado[mover dados tooSQL Server no Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tópico para obter instruções sobre como toomove sua tooSQL dados Server no Azure.
> 
> 

seguinte Olá **menu** liga tootopics que descrevem como toosample dados de vários ambientes de armazenamento. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Os dados de exemplo por que motivo?**
Se o conjunto de dados de Olá planear tooanalyze for grande, é normalmente tooreduce de dados de exemplo toodown Olá uma boa ideia-tooa mais pequeno, mas representativo e mais fácil gerir o tamanho. Isto facilita a compreensão de dados, exploração e engenharia da funcionalidade. A função no Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) é tooenable rápido fazer o protótipo de funções de processamento de dados de Olá e modelos de machine learning.

Esta tarefa de amostragem é um passo Olá [processo de ciência de dados de equipa (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Utilizar o SQL Server
Esta secção descreve vários métodos com o SQL Server tooperform simple aleatória amostragem contra dados Olá na base de dados de Olá. Escolha um método com base no seu tamanho de dados e a distribuição da mesma.

Olá dois itens abaixo mostram como toouse newid no SQL Server tooperform Olá amostragem. Olá método que escolher depende aleatórias como pretende toobe de exemplo de Olá (pk_id no código de exemplo de Olá abaixo pressupõe-se toobe uma chave primária gerado automaticamente).

1. Amostra aleatória menos strict
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Amostra aleatória mais 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Tablesample pode ser utilizado para a amostragem, bem como demonstrado abaixo. Isto poderá ser uma abordagem de melhor se o tamanho de dados for grande (assumindo que não estão correlacionados dados em diferentes páginas) e para Olá consulta toocomplete num tempo razoável.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Pode explorar e gerar funcionalidades a partir destes amostras de dados armazenando-os numa nova tabela
> 
> 

### <a name="sql-aml"></a>Ligar tooAzure Machine Learning
Pode utilizar consultas de exemplo de Olá acima diretamente no Azure Machine Learning de Olá [importar dados] [ import-data] dados toodown-exemplo hello módulo Olá viaje até e colocá-la para uma experimentação do Azure Machine Learning. Uma captura de ecrã da utilização de dados do Olá leitor módulo tooread Olá amostragem é mostrada abaixo:

![leitor sql][1]

## <a name="python"></a>Utilizando a linguagem de programação Olá Python
Esta secção demonstra utilizando Olá [pyodbc biblioteca](https://code.google.com/p/pyodbc/) tooestablish um ODBC ligar tooa SQL server da base de dados no Python. cadeia de ligação de base de dados de Olá é o seguinte: (substitua servername, dbname, nome de utilizador e palavra-passe com a sua configuração):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Olá [Pandas](http://pandas.pydata.org/) biblioteca no Python fornece um conjunto avançado de estruturas de dados e ferramentas de análise de dados para manipulação de dados para a programação do Python. código de Olá abaixo lê uma amostra de 0.1% de dados de Olá de uma tabela na base de dados SQL do Azure para dados de Pandas:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Agora, pode trabalhar com dados Olá amostragem num intervalo de dados de Pandas Olá. 

### <a name="python-aml"></a>Ligar tooAzure Machine Learning
Pode utilizar Olá seguintes exemplo código toosave Olá dados de objeto de amostragem de baixo tooa ficheiro e carregá-la tooan BLOBs do Azure. Olá num blob Olá podem ser diretamente ler dados para uma experimentação do Azure Machine Learning utilizando Olá [importar dados] [ import-data] módulo. passos de Olá são os seguintes: 

1. Escrever Olá pandas moldura tooa local ficheiro de dados
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Carregar ficheiro local tooAzure blob
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. Ler dados de Blobs do Azure utilizando o Azure Machine Learning [importar dados] [ import-data] módulo, conforme mostrado no Olá ecrã captar abaixo:

![blob de leitor][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Olá o processo de ciência de dados de equipa no exemplo de ação
Para obter um exemplo de instruções ponto a ponto do Olá o processo de ciência de dados de equipa um utilizando um conjunto de dados público, consulte o artigo [processo de ciência de dados de equipa em ação: utilizar o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
