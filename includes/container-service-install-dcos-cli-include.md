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
> <span data-ttu-id="d68df-104">Esta ação é para trabalhar com clusters de ACS baseados em DC/SO.</span><span class="sxs-lookup"><span data-stu-id="d68df-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="d68df-105">Não há toodo sem necessidade de isto para clusters de ACS com base em Swarm.</span><span class="sxs-lookup"><span data-stu-id="d68df-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="d68df-106">Primeiro, [ligar tooyour ACS baseado no DC/SO cluster](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d68df-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="d68df-107">Depois de ter efetuado esta ação, pode instalar Olá DC/SO CLI no computador cliente com comandos Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="d68df-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="d68df-108">Se estiver a utilizar uma versão antiga do Python, poderá reparar alguns "InsecurePlatformWarnings".</span><span class="sxs-lookup"><span data-stu-id="d68df-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="d68df-109">Pode ignorar com segurança estes avisos.</span><span class="sxs-lookup"><span data-stu-id="d68df-109">You can safely ignore these.</span></span>

<span data-ttu-id="d68df-110">Na ordem tooget foi iniciado sem reiniciar o shell, execute:</span><span class="sxs-lookup"><span data-stu-id="d68df-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="d68df-111">Este passo não será necessário quando iniciar novamente o shell.</span><span class="sxs-lookup"><span data-stu-id="d68df-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="d68df-112">Agora, pode confirmar que Olá que CLI está instalado:</span><span class="sxs-lookup"><span data-stu-id="d68df-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```