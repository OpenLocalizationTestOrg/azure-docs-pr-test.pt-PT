---
title: "aaaUsing Ruby na aplicação Web de serviço de aplicações do Azure no Linux | Microsoft Docs"
description: "Utilizar Ruby na aplicação de Web do App Service do Azure no Linux."
keywords: "serviço de aplicações do Azure, aplicação web, faq, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Utilizar Ruby na aplicação Web no Linux #

Com Olá mais recente atualização tooour back-end, iremos introduziu o suporte para Ruby v.2.3. Por definição de configuração de Olá da sua aplicação web do Linux, pode alterar a pilha de aplicação Olá.

## <a name="using-hello-azure-portal"></a>Utilizar Olá portal do Azure ##

No menu Olá novo no Olá [portal do Azure](https://portal.azure.com), pode escolher toocreate uma aplicação Web no Linux Olá Web + móvel opção conforme mostrado no Olá seguinte imagem:

![Iniciar criação de uma aplicação web no Olá portal do Azure][1]

Em seguida, Olá **painel criar** abre-se conforme mostrado na Olá seguinte imagem:

![Painel de criação de Olá][2]

1. Dê um nome de aplicação web.
2. Escolha um grupo de recursos existente ou crie um novo. (Consulte regiões disponíveis na Olá [secção limitações](app-service-linux-intro.md).)
3. Escolha um plano do App Service do Azure existente ou crie um novo. (Consulte as notas de plano de serviço de aplicações no Olá [secção limitações](app-service-linux-intro.md).)
4. Escolha Olá Ruby pilhas de tempo de execução incorporada Olá.

Depois da aplicação Ruby web é criada, pode implementar tooit utilizando Git ou FTP.

toolearn mais informações sobre como criar uma aplicação Ruby, verifique Olá [get guia de introdução](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Passos seguintes
* [O que é a aplicação Web no Linux?](app-service-linux-intro.md)
* [TooAzure de implementação de Git local do serviço de aplicações](app-service-deploy-local-git.md)
* [Aplicação de Web do App Service do Azure no Linux FAQ](app-service-linux-faq.md)
* [Criar uma aplicação Ruby com a aplicação Web do Azure no Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png