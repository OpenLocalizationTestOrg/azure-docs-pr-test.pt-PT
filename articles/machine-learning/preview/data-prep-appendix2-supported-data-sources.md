---
title: "Origens de dados disponíveis com a preparação de dados do Azure Machine Learning suportadas | Microsoft Docs"
description: "Este documento fornece uma lista completa das origens de dados suportadas disponíveis para a preparação de dados do Azure Machine Learning."
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/12/2017
ms.openlocfilehash: 32707a8089abef6caebedea168f5891161b1b480
ms.sourcegitcommit: 68aec76e471d677fd9a6333dc60ed098d1072cfc
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 12/18/2017
---
# <a name="supported-data-sources-for-azure-machine-learning-data-preparation"></a>Origens de dados suportados de preparação de dados do Azure Machine Learning 
Este artigo descreve as origens de dados atualmente suportados para a preparação de dados do Azure Machine Learning.

As origens de dados suportada para esta versão são os seguintes.

## <a name="types"></a>Tipos 

### <a name="sql-server"></a>SQL Server
Ler a partir do servidor SQL no local ou a base de dados SQL do Azure.

#### <a name="options"></a>Opções
- Endereço do Servidor
- Confiança servidor (par quando o certificado no servidor não é válido. Utilize com cuidado)
- Tipo de autenticação (Windows, o servidor)
- Nome de Utilizador
- Palavra-passe
- Para ligar à base de dados
- Consulta SQL

#### <a name="notes"></a>Notas
- Colunas de variante do SQL não são suportadas
- Coluna de hora é convertida em datetime, acrescentando tempo da base de dados até à data 1970/1/1
- Quando executado no cluster do Spark, todos os dados relacionados com as colunas (data, datetime, datetime2, datetimeoffset) irão avaliar valores incorretos para datas anteriores 1583
- Os valores nas colunas decimais poderão perder precisão devido a conversão para decimal

### <a name="directory-vs-file"></a>Diretório vs. o ficheiro
Escolha um único ficheiro e lê-lo na preparação de dados. O tipo de ficheiro é analisado para determinar os parâmetros predefinidos para a ligação de ficheiro apresentadas no ecrã seguinte.

Escolha um diretório ou um conjunto de ficheiros dentro de um diretório (o Seletor de ficheiros é MultiSelect é). Com uma abordagem, os ficheiros são lida como um fluxo de dados único e são acrescentados entre si, com cabeçalhos repartidos saída, se necessário.

Os tipos de ficheiro suportados são:
- Delimitados (. csv, .tsv,. txt, etc.)
- Largura fixa
- Texto simples
- Ficheiro JSON

### <a name="csv-file"></a>Ficheiro CSV
Ler um ficheiro de valores separados por vírgulas de armazenamento.

#### <a name="options"></a>Opções
- separador
- Comentar
- Cabeçalhos
- Símbolo decimal
- Codificação de ficheiro
- Linhas a ignorar

### <a name="tsv-file"></a>Ficheiro TSV
Ler um ficheiro separador separados-valor de armazenamento.

#### <a name="options"></a>Opções
- Comentar
- Cabeçalhos
- Codificação de ficheiro
- Linhas a ignorar

### <a name="excel-xlsxlsx"></a>Excel (.xls/.xlsx)
Ler uma folha de um ficheiro Excel a uma hora, especificando o nome da folha ou número.

#### <a name="options"></a>Opções
- Nome da folha ou um número
- Cabeçalhos
- Linhas a ignorar

### <a name="json-file"></a>Ficheiro JSON
Ler um ficheiro JSON a partir do armazenamento. O ficheiro é "simplificado" na leitura.

#### <a name="options"></a>Opções
- Nenhum

### <a name="parquet"></a>Parquet
Ler um conjunto de dados Parquet, ou um único ficheiro ou pasta.

Parquet como um formato pode demorar várias formas no armazenamento. Para conjuntos de dados menores, um ficheiro único .parquet, por vezes, é utilizado. Vários Python bibliotecas suporte ler ou escrever ficheiros .parquet único. Neste momento, a preparação de dados do Azure Machine Learning baseia-se na biblioteca PyArrow Python para ler Parquet durante a utilização de interativa local. Suporta ficheiros .parquet único (, desde foram escritos como tal e não como parte de um conjunto de dados maior), bem como Parquet conjuntos de dados.

Um conjunto de dados Parquet é uma coleção de mais de um ficheiro de .parquet, cada um dos quais representa uma partição mais pequena de um conjunto de dados maior. Conjuntos de dados são normalmente contidos numa pasta e são o formato de saída de parquet predefinido para plataformas, tais como o Spark e o Hive.

>[!NOTE]
>Quando estiver a ler dados Parquet que está a ser uma pasta com vários ficheiros .parquet, é esta a selecionar o diretório para ler e o **conjunto de dados de Parquet** opção. Isto torna PyArrow ler a pasta toda em vez dos ficheiros individuais. Isto garante que suporte para ler mais complicadas formas de armazenar Parquet no disco, tais como a criação de partições de pasta.

Execução de escalamento horizontal depende Parquet do Spark capacidades de leitura e suporta ficheiros único, bem como pastas, semelhantes à utilização interativa local.

#### <a name="options"></a>Opções
- Parquet conjunto de dados. Esta opção determina se a preparação de dados do Azure Machine Learning expande um determinado diretório e tenta ler individualmente cada ficheiro (modo não seleccionado), ou se se trata o diretório como o conjunto de dados inteiro (o modo selecionado). Com o modo selecionado, PyArrow escolher a melhor forma de interpretar os ficheiros.


## <a name="locations"></a>Localizações
### <a name="local"></a>Local
Um disco rígido local ou uma localização de armazenamento de rede mapeadas.

### <a name="sql-server"></a>SQL Server
Servidor de SQL no local, ou a base de dados SQL do Azure.

### <a name="azure-blob-storage"></a>Armazenamento de Blobs do Azure
Blob storage do Azure, que requer uma subscrição do Azure.

