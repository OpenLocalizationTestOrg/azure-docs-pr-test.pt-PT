---
title: "aaaAzure geridos aplicação criar funções de definição de IU | Microsoft Docs"
description: "Descreve Olá funções toouse ao construir a definições de IU para aplicações geridas do Azure"
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
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Elementos de CreateUiDefinition
Este artigo descreve o esquema de Olá e propriedades para todos os elementos suportados um CreateUiDefinition. Utilize estes elementos quando [criar uma aplicação gerida do Azure](managed-application-publishing.md). esquema de Olá para a maioria dos elementos é o seguinte:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Propriedade | Necessário | Descrição |
| -------- | -------- | ----------- |
| nome | Sim | Um identificador interno tooreference uma instância específica de um elemento. Hello mais comuns a utilização do nome de elemento Olá é no `outputs`, em que os valores de saída de Olá de Olá especificado de elementos são toohello mapeada parâmetros de modelo de Olá. Também pode utilizá-la toobind Olá valor de saída de um elemento toohello `defaultValue` de outro elemento. |
| tipo | Sim | Olá toorender de controlo de IU para o elemento de Olá. Para obter uma lista dos tipos suportados, consulte [elementos](#elements). |
| Etiqueta | Sim | Olá apresentar o texto do elemento de Olá. Alguns tipos de elemento contém várias etiquetas, para que o valor de Olá pode ser um objeto que contém vários cadeias. |
| DefaultValue | Não | valor predefinido de Olá do elemento de Olá. Alguns tipos de elemento suportam valores predefinidos complexa, pelo que o valor de Olá pode ser um objeto. |
| Descrição | Não | Olá toodisplay de texto na descrição do elemento de Olá Olá. Semelhante demasiado`label`, alguns elementos suportam vários cadeias de sugestão de ferramenta. Ligações de inline podem ser incorporadas utilizando a sintaxe de Markdown.
| Restrições | Não | Uma ou mais propriedades que são utilizados toocustomize Olá comportamento de validação do elemento de Olá. Propriedades de Olá suportado para restrições variam consoante o tipo de elemento. Alguns tipos de elemento não suporta a personalização do comportamento de validação de Olá e assim não ter nenhuma propriedade de restrições. |
| Opções | Não | Propriedades adicionais, personalizar o comportamento de Olá do elemento de Olá. Semelhante demasiado`constraints`, propriedades Olá suportado variam consoante o tipo de elemento. |
| Visível | Não | Indica se o elemento de Olá é apresentado. Se `true`, elemento Olá e elementos subordinados aplicáveis são apresentados. valor predefinido de Olá é `true`. Utilize [funções lógicas](managed-application-createuidefinition-functions.md#logical-functions) toodynamically controlar o valor desta propriedade.

## <a name="elements"></a>Elementos

Olá, documentação de cada elemento contém um exemplo de IU, observações de esquema, no comportamento de Olá de elemento de Olá (normalmente concerning validação e personalização suportada) e saída de exemplo.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Passos seguintes
* Para aplicações de toomanaged uma introdução, consulte [descrição geral do Azure gerida aplicações](managed-application-overview.md).
* Para definições de IU toocreating uma introdução, consulte [introdução CreateUiDefinition](managed-application-createuidefinition-overview.md).
