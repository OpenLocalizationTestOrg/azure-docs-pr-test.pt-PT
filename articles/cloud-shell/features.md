---
title: "funcionalidades de Shell de nuvem (pré-visualização) aaaAzure | Microsoft Docs"
description: "Descrição geral das funcionalidades de Shell de nuvem do Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Funcionalidades e ferramentas para a Shell de nuvem do Azure
Shell de nuvem do Azure é um toomanage de experiência de shell baseada no browser e desenvolver recursos do Azure.

Shell de nuvem oferece um browser acessível, pré-configurados experiência de shell para gerir recursos do Azure sem a sobrecarga Olá de instalar, controlo de versões e manutenção de uma máquina por si.

Shell de nuvem Aprovisiona máquinas numa base por pedido e como resultado o estado da máquina não serão mantidas entre sessões. Uma vez que a Shell de nuvem é criada para sessões interativas, shells terminam automaticamente após 20 minutos de inatividade de shell.

## <a name="bash-in-cloud-shell"></a>Bash na Shell de nuvem
### <a name="tools"></a>Ferramentas
|Categoria   |Nome   |
|---|---|
|Interpretador de shell do Linux|Bash<br> partilhar               |
|Ferramentas do Azure            |[CLI do Azure 2.0](https://github.com/Azure/azure-cli) e [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AZCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Editores de texto           |VIM<br> Nano<br> emacs       |
|Controlo de código fonte         |Git                    |
|Ferramentas de compilação            |Certifique-<br> maven<br> npm<br> PIP         |
|Contentores             |[CLI do docker](https://github.com/docker/cli)/[Docker máquina](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Rascunho](https://github.com/Azure/draft)<br> [CLI DE DC/SO](https://github.com/dcos/dcos-cli)         |
|Bases de Dados              |Cliente de MySQL<br> Cliente PostgreSql<br> [SQLCMD utilitário](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [MSSQL scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Outros                  |iPython cliente<br> [Nuvem Foundry CLI](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Suporte de idiomas
|Idioma   |Versão   |
|---|---|
|.NET       |1.01       |
|Ir         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 e 3.5 (predefinição)|

## <a name="secure-automatic-authentication"></a>Autenticação automática segura
Shell de nuvem e em segurança os automaticamente autentica o acesso de conta para Olá Azure CLI 2.0.

## <a name="azure-files-persistence"></a>Persistência de ficheiros do Azure
Uma vez que a Shell de nuvem é atribuído numa base por pedido através de uma máquina temporária, ficheiros fora do Estado de $Home e a máquina não são mantidos entre sessões.
ficheiros de toopersist entre sessões, Shell da nuvem explica como anexar um ficheiro do Azure através de partilha na primeira execução.
Uma vez concluída nuvem Shell ligará automaticamente o armazenamento para todas as futuras sessões.

[Saiba mais sobre a ligação de partilhas de ficheiros do Azure tooCloud Shell.](persisting-shell-storage.md)

## <a name="next-steps"></a>Passos seguintes
[Início rápido de Shell de nuvem](quickstart.md) <br>
[Saiba mais sobre a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>