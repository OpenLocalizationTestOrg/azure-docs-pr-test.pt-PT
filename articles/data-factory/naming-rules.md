---
title: "Regras para atribuição de nomes de entidades do Azure Data Factory | Microsoft Docs"
description: Descreve as regras de nomenclatura para entidades do Data Factory.
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: shlo
ms.openlocfilehash: 17661f139c162f1ed22f9e186ae12bcf963e57f9
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/23/2018
---
# <a name="azure-data-factory---naming-rules"></a>O Azure Data Factory - as regras de nomenclatura
A tabela seguinte fornece regras de nomenclatura artefactos do Data Factory de dados.

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em pré-visualização. Se estiver a utilizar a versão 1 do serviço do Data Factory, o que é geralmente disponível (DG), consulte [nomenclatura regras no Data Factory version1](v1/data-factory-naming-rules.md).

| Nome | Exclusividade de nome | Verificações de validação |
|:--- |:--- |:--- |
| Data Factory |Exclusivo em todo o Microsoft Azure. Os nomes são sensível, ou seja, `MyDF` e `mydf` Consulte para a mesma fábrica de dados. |<ul><li>Cada fábrica de dados está associada ao exatamente uma subscrição do Azure.</li><li>Nomes de objeto tem de começar com uma letra ou um número e só podem conter letras, números e o caráter de travessão (-).</li><li>Cada caráter de travessão (-) tem de ser imediatamente precedido e seguido por uma letra ou um número. Traços consecutivos não são permitidos em nomes de contentor.</li><li>Nome pode ter entre 3 e 63 carateres.</li></ul> |
| Os serviços ligados/tabelas/Pipelines |Exclusivo com uma fábrica de dados. Os nomes são sensível. |<ul><li>Número máximo de carateres num nome de tabela: a 260.</li><li>Nomes de objeto tem de começar com uma letra, o número ou um caráter de sublinhado (_).</li><li>Os seguintes carateres não são permitidos: ".", "+","?", "/", "<", ">","*", "%", "&", ":","\\"</li></ul> |
| Grupo de Recursos |Exclusivo em todo o Microsoft Azure. Os nomes são sensível. |<ul><li>Número máximo de carateres: 1000.</li><li>O nome pode conter letras, dígitos e os seguintes carateres: "-", "_",","e"."</li></ul> |

## <a name="next-steps"></a>Passos Seguintes
Saiba como criar fábricas de dados ao seguir as instruções passo a passo em [início rápido: criar uma fábrica de dados](quickstart-create-data-factory-powershell.md) artigo. 