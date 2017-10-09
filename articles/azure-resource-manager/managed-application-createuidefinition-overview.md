---
title: "aaaUnderstand Criar definição de IU para aplicações geridas do Azure | Microsoft Docs"
description: "Descreve como toocreate definições de IU para aplicações geridas do Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>Introdução ao CreateUiDefinition
Este documento apresenta alguns conceitos de núcleos de Olá de um CreateUiDefinition, que é utilizada pela interface de utilizador de Olá do Olá toogenerate portal do Azure para criar uma aplicação gerida.

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

Um CreateUiDefinition sempre contém três propriedades: 

* processador
* Versão
* parâmetros

Para aplicações geridas, o processador deve ser sempre `Microsoft.Compute.MultiVm`, e a versão de Olá mais recente suportado é `0.1.2-preview`.

esquema de Olá da propriedade de parâmetros de Olá depende da combinação de Olá de processador especificado Olá e versão. Para aplicações geridas, propriedades Olá suportado são `basics`, `steps`, e `outputs`. Olá propriedades as noções básicas e passos contenham Olá _elementos_ , como as caixas de texto e as dropdowns - toobe apresentado no Olá portal do Azure. saídas Olá propriedade é utilizada toomap Olá saída valores de Olá especificado de elementos toohello parâmetros do modelo de implementação Azure Resource Manager Olá.

Incluindo `$schema` é recomendada, mas opcionais. Se for especificado, Olá valor para `version` tem de corresponder à versão de Olá dentro Olá `$schema` URI.

## <a name="basics"></a>Noções básicas
passo Noções básicas de Olá é sempre Olá primeiro passo assistente Olá gerado ao hello do portal do Azure analisa um CreateUiDefinition. Além disso elementos de Olá toodisplaying especificado no `basics`, portal Olá injects elementos para a subscrição do utilizadores toochoose Olá, grupo de recursos e localização para a implementação de Olá. Geralmente, os elementos de consulta para os parâmetros de toda a implementação, como o nome de Olá de credenciais de administrador ou de cluster, devem passar neste passo.

Se o comportamento de um elemento depende da subscrição, o grupo de recursos ou localização do utilizador Olá, em seguida, que o elemento não é possível utilizar Noções básicas. Por exemplo, **Microsoft.Compute.SizeSelector** depende subscrição e localização toodetermine Olá lista do utilizador Olá de tamanhos disponíveis. Por conseguinte, **Microsoft.Compute.SizeSelector** só pode ser utilizada nos passos. Geralmente, apenas os elementos da Olá **Microsoft.Common** espaço de nomes pode ser utilizado no Noções básicas. Embora alguns elementos em outros espaços de nomes (como **Microsoft.Compute.Credentials**) que não dependem do contexto do utilizador Olá, ainda são permitidas.

## <a name="steps"></a>Passos
propriedade de passos de Olá pode conter zero ou mais toodisplay de passos adicionais após Noções básicas, cada um dos quais contém um ou mais elementos. Considere adicionar passos por função ou a camada da aplicação Olá a ser implementada. Por exemplo, adicione um passo para entradas de nós principais Olá e um passo para nós de trabalho de Olá num cluster.

## <a name="outputs"></a>saídas
Olá portal do Azure utiliza Olá `outputs` elementos da propriedade toomap de `basics` e `steps` toohello parâmetros do modelo de implementação Azure Resource Manager Olá. chaves de Olá deste dicionário estão nomes Olá Olá dos parâmetros do modelo e valores de Olá são propriedades dos objetos de resultado Olá de elementos de Olá referenciado.

## <a name="functions"></a>Funções
Semelhante demasiado[funções de modelo](resource-group-template-functions.md) no Azure Resource Manager (tanto no como sintaxe funcionalidade), CreateUiDefinition fornece funções para trabalhar com dos elementos entradas e saídas, bem como as funcionalidades, tais como conditionals.

## <a name="next-steps"></a>Passos seguintes
CreateUiDefinition próprio tem um esquema simple. profundidade real de Olá-provém de todos os elementos de Olá suportada e as funções, que Olá seguintes documentos descrevem wondrous detalhadamente:

- [Elementos](managed-application-createuidefinition-elements.md)
- [Funções](managed-application-createuidefinition-functions.md)

Está aqui disponível atual do esquema JSON para CreateUiDefinition: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json. 

Versões posteriores estará disponíveis em Olá mesma localização. Substitua Olá `0.1.2-preview` parte do URL de Olá e Olá `version` valor com o identificador da versão Olá tenciona toouse. identificadores de versão Olá atualmente suportado são `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, e `0.1.2-preview`.
