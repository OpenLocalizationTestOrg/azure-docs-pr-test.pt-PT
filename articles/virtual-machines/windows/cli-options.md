---
title: "Olá aaaUsing CLI do Azure no Windows | Microsoft Docs"
description: "Utilizar Olá CLI do Azure no Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Utilizar Olá CLI do Azure no Windows

Olá Interface de linha de comandos do Azure (CLI) fornece uma linha de comandos e o ambiente de script para criar e gerir recursos do Azure. Olá CLI do Azure está disponível para macOS, Linux e sistemas operativos Windows. Entre estes sistemas operativos, comandos da CLI Olá são idênticos, no entanto, a sintaxe de scripting específicos de sistema operativo pode ser diferente.

Estes documento detalhes Olá formas Olá CLI do Azure podem ser instaladas e executadas no Windows detalhes syntactical as considerações de e para cada. Para aprofundada CLI do Azure documentação, consulte [documentação da CLI do Azure]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Subsistema Windows para Linux

Olá subsistema Windows para Linux (WSL) fornece um ambiente de Ubuntu Linux aniversário do Windows 10 e edições posteriores. Quando ativada, WSL fornece uma experiência de Bash nativa, o que pode ser utilizada para criar e executar scripts da CLI do Azure. Porque WSL fornece uma experiência de Bash nativa, os scripts da CLI do Azure podem ser partilhados entre macOS, Linux e Windows sem modificação.

toouse Olá CLI do Azure no WSL, conclua os seguintes Olá.

|Tarefa | Instruções |
|---|---|
| Ativar WSL | [Instalar documentação WSL](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Instalar Olá CLI do Azure |[Instalar Olá CLI no WSL/Ubuntu 14.04](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Olá CLI do Azure pode ser executada nativamente no Windows. Nesta configuração, pacote da CLI do Azure de Olá está instalado no sistema de operativo do Windows hello e comandos podem ser executados a partir do PowerShell. Nesta configuração, scripts e comandos da CLI do Azure podem ser executados em qualquer versão suportada do Windows, no entanto, não é necessária sintaxe de scripting específicas de plataforma. Por este motivo, scripts não não necessariamente ser partilhados entre macOS, Linux e Windows sem modificação.

Olá toouse CLI do Azure no Windows, instale o pacote de Olá utilizar estas instruções, [instalação Olá CLI no Windows](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Imagem de docker

Ao utilizar o Docker para Windows, pode ser iniciada uma imagem de Docker que inclui Olá CLI do Azure. Esta imagem baseia-se remotas Linux e inclui uma experiência nativa do Bash.  Ao utilizar o Docker para Windows e a imagem da CLI do Azure de Olá, toobe scripts partilhado entre macOS, Linux e Windows. 

Olá toouse CLI do Azure no Docker para Windows, certifique-se de que Docker para Windows está em execução e execute Olá os seguintes comandos.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Depois de concluído, um Bash será de início de sessão que é pré-carregado com ferramentas da CLI do Azure de Olá.

## <a name="next-steps"></a>Passos Seguintes

[Exemplo CLI para máquinas virtuais do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Exemplos da CLI para Web Apps do Azure](../../app-service-web/app-service-cli-samples.md)

[Exemplos da CLI para SQL do Azure](../../sql-database/sql-database-cli-samples.md)
