---
title: "Python de exemplo para efetuar a derivação de novas colunas em preparação de dados do Azure Machine Learning | Microsoft Docs"
description: "Este documento fornece exemplos de código do Python para criar novas colunas em preparação de dados do Azure Machine Learning."
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
ms.openlocfilehash: e576d44a854159054d4f7886fe7859ae34875c8f
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="sample-of-custom-column-transforms-python"></a>Exemplo de transformações de coluna personalizado (Python) 
O nome desta transformação no menu é **Add Column (Script)**.

Antes de ler este anexo, leia [descrição geral de extensibilidade do Python](data-prep-python-extensibility-overview.md).

## <a name="test-equivalence-and-replace-values"></a>Testar equivalência e substitua os valores 
Se o valor Col1 é inferior a 4, a nova coluna deve ter um valor de 1. Se o valor Col1 é mais de 4, a nova coluna tem o valor 2. 

```python
    1 if row["Col1"] < 4 else 2
```
## <a name="current-date-and-time"></a>Data e hora atuais 

```python
    datetime.datetime.now()
```
## <a name="typecasting"></a>Typecasting 
```python
    float(row["Col1"]) / float(row["Col2"] - 1)
```
## <a name="evaluate-for-nullness"></a>Avaliar para nullness 
Se Col1 contém um valor nulo, em seguida, marcar a nova coluna como **incorreto**. Se não estiver, marque-a como **bom.** 

```python
    'Bad' if pd.isnull(row["Col1"]) else 'Good'
```
## <a name="new-computed-column"></a>Nova coluna calculada 
```python
    np.log(row["Col1"])
```
## <a name="epoch-computation"></a>Cálculo de época 
Número de segundos desde a época de Unix (partindo do princípio de Col1 já é uma data): 
```python
    row["Col1"] - datetime.datetime.utcfromtimestamp(0)).total_seconds()
```

## <a name="hash-a-column-value-into-a-new-column"></a>Um valor de coluna de hash para uma nova coluna
```python
    import hashlib
    hash(row["MyColumnToHashCol1"])

```




