---
title: aaaAuthenticate com um registo de contentor do Azure | Microsoft Docs
description: Como toolog no registo de contentor do Azure tooan utilizando um Azure Active Directory service principal ou uma conta de administrador
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a0b0462e8432b2567689debca322e2426baa7fa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-a-private-docker-container-registry"></a>Autenticar com um registo de contentor do Docker privado
toowork com imagens do contentor num registo de contentor do Azure, inicie sessão com a Olá `docker login` comando. Pode iniciar sessão utilizando um  **[principal de serviço do Azure Active Directory](../active-directory/active-directory-application-objects.md)**  específicas do registo ou **conta de administrador**. Este artigo fornece mais detalhes sobre estas identidades.



## <a name="service-principal"></a>Principal de serviço

Pode [atribuir um principal de serviço](container-registry-get-started-azure-cli.md#assign-a-service-principal) tooyour registo e utilizá-lo para a autenticação básica do Docker. É recomendado utilizar um principal de serviço para a maioria dos cenários. Forneça o ID da aplicação Olá e palavra-passe de toohello principal do serviço Olá `docker login` comando, conforme mostrado no seguinte exemplo de Olá:

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Assim que a sessão iniciada, Docker coloca em cache as credenciais de Olá, por isso não terá de ID de aplicação do tooremember Olá.

> [!TIP]
> Se quiser, pode voltar a gerar Olá palavra-passe de um principal de serviço, executando Olá `az ad sp reset-credentials` comando.
>


Permitem principais de serviço [acesso baseado em funções](../active-directory/role-based-access-control-configure.md) tooa registo. Funções disponíveis são:
  * Leitor (acesso só de solicitação).
  * Contribuidor (push e pull).
  * Proprietário (extração, push e atribuir funções tooother utilizadores).

Acesso anónimo não está disponível sobre os registos do contentor do Azure. Pode utilizar imagens públicas [Docker Hub](https://docs.docker.com/docker-hub/).

Pode atribuir vários principais de serviço tooa registo, que permite-lhe acesso toodefine para diferentes utilizadores ou aplicações. Principais de serviço também ativar registo de tooa conectividade "sem interface" no programador ou cenários de DevOps como Olá exemplos a seguir:

  * Implementações de contentores de sistemas de tooorchestration um registo, incluindo DC/OS, Docker Swarm e Kubernetes. Pode também solicitar toorelated de registos do contentor serviços do Azure, tal como [serviço de contentor](../container-service/index.yml), [do serviço de aplicações](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/)entre outros.

  * Contínuas integração e a implementação soluções (por exemplo, o Visual Studio Team Services ou Jenkins) que criar imagens de contentor e emiti-las tooa registo.





## <a name="admin-account"></a>Conta de administrador
Com cada registo que criar, é criada automaticamente uma conta de administrador. Por predefinição está desativada conta Olá, mas pode ativá-la e gerir credenciais Olá, por exemplo através de Olá [portal](container-registry-get-started-portal.md#manage-registry-settings) ou utilizando Olá [comandos de Azure CLI 2.0](container-registry-get-started-azure-cli.md#manage-admin-credentials). Cada conta de administrador é fornecida com duas palavras-passe, que podem ser novamente geradas. duas palavras-passe Olá permitem-lhe registo do toomaintain ligações toohello utilizando uma palavra-passe enquanto volta a gerar Olá outra palavra-passe. Se a conta de Olá estiver ativada, pode passar de nome de utilizador de Olá e a palavra-passe toohello `docker login` comando para registo de toohello de autenticação básica. Por exemplo:

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> conta de administrador Olá foi concebida para um único utilizador tooaccess Olá de registo, principalmente para fins de teste. Não é recomendado tooshare credenciais de conta de administrador Olá entre os outros utilizadores. Todos os utilizadores são apresentados como um registo de toohello de utilizador único. Alterar ou desativar esta conta desativa o acesso de registo para todos os utilizadores que utilizam credenciais Olá.
>


### <a name="next-steps"></a>Passos seguintes
* [Push imagem primeiro utilizar Olá CLI do Docker](container-registry-get-started-docker-cli.md).
* Para obter mais informações sobre a autenticação na pré-visualização de registo do contentor de Olá, consulte Olá [blogue](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).
