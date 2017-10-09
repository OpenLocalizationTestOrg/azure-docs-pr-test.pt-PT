---
title: aaaUse Azure Machine Learning com o SQL Data Warehouse | Microsoft Docs
description: "Tutorial para utilizar o Azure Machine Learning com o Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>Utilização do Azure Machine Learning com o SQL Data Warehouse
O Azure Machine Learning é um serviço de Análise Preditiva completamente gerido que pode utilizar modelos preditivos toocreate contra os dados no armazém de dados do SQL Server e, em seguida, publicar como serviços web prontos a consumir. Pode saber Olá Noções básicas de Análise Preditiva e machine learning ao ler [introdução tooMachine Learning no Azure][Introduction tooMachine Learning on Azure].  Em seguida, pode saber como toocreate, preparar, Pontuar e testar um modelo de machine learning utilizando Olá [criar experimentação tutorial][Create experiment tutorial].

Neste artigo, ficará a saber como Olá toodo seguir utilizando Olá [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* Ler dados a partir do seu toocreate de base de dados, formação e Pontuar um modelo preditivo
* Base de dados de tooyour de dados de escrita

## <a name="read-data-from-sql-data-warehouse"></a>Ler dados do SQL Data Warehouse
Iremos ler dados da tabela do produto na base de dados do Olá AdventureWorksDW.

### <a name="step-1"></a>Passo 1
Inicie uma nova experimentação, clicando em + nova em Olá parte inferior da janela Machine Learning Studio, de Olá selecione experimentação e, em seguida, selecione a experimentar em branco. Predefinição de Olá selecione experimentação nome na Olá parte superior da tela Olá e renomeie-toosomething significativo, por exemplo, predição do preço de bicicletas.

### <a name="step-2"></a>Passo 2
Procure o módulo de leitor de Olá na paleta Olá de conjuntos de dados e módulos esquerda Olá da tela de experimentação Olá. Arraste a tela de experimentação do Olá módulo toohello.
![][drag_reader]

### <a name="step-3"></a>Passo 3
Selecione o módulo de leitor de Olá e preencher o painel de propriedades de Olá.

1. Selecione a SQL Database do Azure como Olá origem de dados.
2. Nome do servidor de base de dados: nome do servidor de Olá de tipo. Pode utilizar Olá [portal do Azure] [ Azure portal] toofind isto.

![][server_name]

1. Nome da base de dados: nome do tipo hello do servidor de Olá que acabou de especificar uma base de dados.
2. Nome de conta de utilizador do servidor: nome de utilizador de Olá de tipo de uma conta que tenha permissões de acesso para a base de dados de Olá.
3. Palavra-passe de conta de utilizador do: forneça Olá palavra-passe para Olá especificar conta de utilizador.
4. Aceitar qualquer certificado de servidor: Utilize esta opção (menos segura), se quiser tooskip rever o certificado de site Olá antes de ler os dados.
5. Consulta de base de dados: introduza uma instrução de SQL que descreve os dados de Olá pretende tooread. Neste caso, iremos irá ler os dados da tabela de produto Olá seguinte consulta a utilizar.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>Passo 4
1. Execute Olá experimentação ao clicar em execução na tela de experimentação Olá.
2. Quando Olá da experimentação ser concluída, o módulo leitor de Olá terá uma marca de verificação verde tooindicate que foi concluída com êxito. Repare também Olá terminado com o estado no canto superior direito de Olá.

![][run]

1. toosee Olá dados importados, clique Olá porta de saída na parte inferior de Olá de conjunto de dados para automóveis Olá e selecione o visualizar.

## <a name="create-train-and-score-a-model"></a>Criar, dar formação e um modelo de pontuação
Agora pode utilizar este conjunto de dados:

* Criar um modelo: processar os dados e definir funcionalidades
* Preparar o modelo de Olá: escolher e aplicar um algoritmo de aprendizagem
* Classificação e teste Olá modelo: prever novos preços de bicicletas

![][model]

mais informações sobre como toocreate, preparar, Pontuar e testar um machine learning Olá de utilização do modelo de toolearn [criar experimentação tutorial][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Escrever tooAzure de dados do armazém de dados do SQL Server
Iremos escrever Olá resultado conjunto tooProductPriceForecast tabela na base de dados do Olá AdventureWorksDW.

### <a name="step-1"></a>Passo 1
Procure o módulo de escritor Olá na paleta Olá de conjuntos de dados e módulos esquerda Olá da tela de experimentação Olá. Arraste a tela de experimentação do Olá módulo toohello.

![][drag_writer]

### <a name="step-2"></a>Passo 2
Selecione o módulo de escritor Olá e preencher o painel de propriedades de Olá.

1. Selecione a SQL Database do Azure como Olá dados de destino.
2. Nome do servidor de base de dados: nome do servidor de Olá de tipo. Pode utilizar Olá [portal do Azure] [ Azure portal] toofind isto.
3. Nome da base de dados: nome do tipo hello do servidor de Olá que acabou de especificar uma base de dados.
4. Nome de conta de utilizador do servidor: nome de utilizador de Olá de tipo de uma conta que tenha permissões de escrita da base de dados de Olá.
5. Palavra-passe de conta de utilizador do: forneça Olá palavra-passe para Olá especificar conta de utilizador.
6. Aceitar qualquer certificado de servidor (inseguras): selecione esta opção se não quiser que o certificado de Olá tooview.
7. Lista separada por vírgulas de toobe colunas guardado: forneça uma lista de colunas de conjunto de dados ou o resultado de Olá que pretende que o toooutput.
8. Nome da tabela de dados: Especifique Olá nome da tabela de dados de Olá.
9. Lista separada por vírgulas de colunas de datatable: especificar toouse de nomes de coluna Olá numa tabela nova Olá. Olá nomes de coluna podem ser diferentes do Olá aqueles no conjunto de dados de origem de Olá, mas tem de listar Olá o mesmo número de colunas aqui por si para a tabela de saída Olá.
10. Número de linhas escrito por operação de SQL Azure: pode configurar Olá número de linhas que são escritos tooa SQL da base de dados numa única operação.

![][writer_properties]

### <a name="step-3"></a>Passo 3
1. Execute Olá experimentação ao clicar em execução na tela de experimentação Olá.
2. Quando Olá da experimentação ser concluída, todos os módulos terá um tooindicate de marca de verificação verde foi concluídas com êxito.

## <a name="next-steps"></a>Passos seguintes
Para obter mais sugestões de desenvolvimento, veja [SQL Data Warehouse development overview (Descrição geral do desenvolvimento no SQL Data Warehouse)][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
