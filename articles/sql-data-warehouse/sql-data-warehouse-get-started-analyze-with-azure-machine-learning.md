---
title: Analisar dados com o Azure Machine Learning | Microsoft Docs
description: Utilize o Azure Machine Learning para criar um modelo preditivo de machine learning com base em dados armazenados no Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3197948e32fe5c95b111fe5495a0e5f85966a24b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/11/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Analisar dados com o Azure Machine Learning
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Este tutorial utiliza o Azure Machine Learning para criar um modelo preditivo de machine learning com base em dados armazenados no Azure SQL Data Warehouse. Mais especificamente, cria uma campanha de marketing direcionada para Adventure Works, a loja de bicicletas, ao prever se existe ou não probabilidade de um cliente comprar uma bicicleta.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Para seguir este tutorial, é necessário:

* Um SQL Data Warehouse pré-carregado com dados de exemplo da AdventureWorksDW. Para proceder ao aprovisionamento, consulte [Create a SQL Data Warehouse (Criar um SQL Data Warehouse)][Create a SQL Data Warehouse] e opte por carregar os dados de exemplo. Se já tiver um armazém de dados, mas não tiver dados de exemplo, pode [carregar dados de exemplo manualmente][load sample data manually].

## <a name="1-get-the-data"></a>1. Obter os dados
Os dados encontram-se na vista dbo.vTargetMail na base de dados AdventureWorksDW. Para ler estes dados:

1. Inicie sessão no [Azure Machine Learning studio][Azure Machine Learning studio] e clique em as minhas experimentações.
2. Clique em **+NOVO** e selecione **Experimentação em Branco**.
3. Introduza um nome para a experimentação: Marketing Direcionado.
4. Arraste o módulo **Leitor** do painel de módulos para a tela.
5. Especifique os detalhes da sua base de dados SQL Data Warehouse no painel Propriedades.
6. Especifique a **consulta** de base de dados para ler os dados de interesse.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Execute experimentação ao clicar em **Executar** na tela de experimentação.
![Executar a experimentação][1]

Depois de a execução da experimentação ser concluída com êxito, clique na porta de saída na parte inferior do módulo Leitor e selecione **Visualizar** para ver os dados importados.
![Ver os dados importados][3]

## <a name="2-clean-the-data"></a>2. Limpar os dados
Para limpar os dados, remova algumas colunas que não sejam relevantes para o modelo. Para efetuar este procedimento:

1. Arraste o módulo **Colunas do Projeto** para a tela.
2. Clique em **Iniciar seletor de colunas** no painel Propriedades, para especificar as colunas que pretende remover.
   ![Colunas do Projeto][4]
3. Exclua duas colunas: CustomerAlternateKey e GeographyKey.
   ![Remover colunas desnecessárias][5]

## <a name="3-build-the-model"></a>3. Criar o modelo
Iremos dividir os dados 80-20: 80% para preparar um modelo de machine learning e 20% para testar o modelo. Iremos utilizar os algoritmos das “Duas Classes” para este problema de classificação binária.

1. Arraste o módulo **Dividir** para a tela.
2. Introduza 0.8 para a Fração de linhas no primeiro conjunto de dados de saída no painel Propriedades.
   ![Dividir os dados em conjunto de preparação e teste][6]
3. Arraste o módulo **Árvore de Decisões Elevada de Duas Classes** para a tela.
4. Arraste o módulo **Preparar Modelo** para a tela e especifique as entradas. Em seguida, clique em **Iniciar seletor de colunas** no painel Propriedades.
   * Primeira entrada: algoritmo ML.
   * Segunda entrada: dados nos quais preparar o algoritmo.
     ![Ligar o módulo Preparar Modelo][7]
5. Selecione a coluna **BikeBuyer** como a coluna a prever.
   ![Selecionar Coluna a prever][8]

## <a name="4-score-the-model"></a>4. Pontuar o modelo
Agora, iremos testar o desempenho do modelo em dados de teste. Iremos comparar o algoritmo escolhido com um algoritmo diferente, para ver qual tem o melhor desempenho.

1. Arraste o módulo **Pontuar Modelo** para a tela.
    Primeira entrada: modelo de preparação Segunda entrada: testar dados ![Pontuar o modelo][9]
2. Arraste a **Máquina do Ponto Bayes de Duas Classes** para a tela de experimentação. Iremos comparar o desempenho deste algoritmo em comparação com a Árvore de Decisões Elevada de Duas Classes.
3. Copie e cole os módulos Preparar Modelo e Pontuar Modelo na tela.
4. Arraste o módulo **Avaliar Modelo** para a tela, para comparar os dois algoritmos.
5. **Execute** a experimentação.
   ![Executar a experimentação][10]
6. Clique na porta de saída na parte inferior do módulo Avaliar Modelo e clique em Visualizar.
   ![Visualizar os resultados da avaliação][11]

As métricas fornecidas são a curva ROC, a curva de diagrama de resgate de precisão e a curva de comparação de precisão. Ao observar estas métricas, é possível ver que o primeiro modelo tem melhor desempenho do que o segundo. Para ver o que o primeiro modelo previu, clique na porta de saída de Pontuar Modelo e clique em Visualizar.
![Visualize os resultados de pontuação][12]

Verá mais duas colunas adicionadas ao conjunto de dados de teste.

* Probabilidades Classificadas: a probabilidade de um cliente ser comprador de uma bicicleta.
* Etiquetas Classificadas: a classificação efetuada pelo modelo – comprador de bicicleta (1) ou não (0). Este limiar de probabilidade para etiquetas está definido como 50% e pode ser ajustado.

Ao comparar a coluna BikeBuyer (real) com as Etiquetas Classificadas (predição), pode ver quão bom foi o desempenho do modelo. Nos passos seguintes, pode utilizar este modelo para fazer predições para clientes novos e publicar este modelo como um serviço Web ou escrever os resultados de volta para o SQL Data Warehouse.

## <a name="next-steps"></a>Passos seguintes
Para saber mais sobre como criar modelos preditivos de machine learning, consulte [Introduction to Machine Learning on Azure (Introdução ao Machine Learning no Azure)][Introduction to Machine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
