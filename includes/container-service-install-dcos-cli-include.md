---
title: "Olá aaaInstall DC/SO CLI | Microsoft Docs"
description: "Instale Olá CLI de DC/OS."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contentores, Microserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> Esta ação é para trabalhar com clusters de ACS baseados em DC/SO. Não há toodo sem necessidade de isto para clusters de ACS com base em Swarm.
> 
> 

Primeiro, [ligar tooyour ACS baseado no DC/SO cluster](../articles/container-service/container-service-connect.md). Depois de ter efetuado esta ação, pode instalar Olá DC/SO CLI no computador cliente com comandos Olá abaixo:

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Se estiver a utilizar uma versão antiga do Python, poderá reparar alguns "InsecurePlatformWarnings". Pode ignorar com segurança estes avisos.

Na ordem tooget foi iniciado sem reiniciar o shell, execute:

```bash
source ~/.bashrc
```

Este passo não será necessário quando iniciar novamente o shell.

Agora, pode confirmar que Olá que CLI está instalado:

```bash
dcos --help
```