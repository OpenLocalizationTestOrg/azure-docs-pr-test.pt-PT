---
title: aaaNever arquivo de dados confidenciais em imagens personalizadas para o Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as diretrizes de Olá para armazenar dados no imagens personalizadas no Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Nunca armazenar dados confidenciais em imagens personalizadas
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.
> 
> 

Ao alojar a sua própria aplicação no Azure RemoteApp, o primeiro passo de Olá é toocreate uma imagem personalizada. Utilizamos que instâncias VM de toocreate imagem personalizada servem as suas aplicações tooyour utilizadores. imagem personalizada Olá deve conter apenas aplicações e dados nunca confidenciais que podem ser perdidos, tais como bases de dados do SQL Server, ficheiros de técnicos ou ficheiros de dados especiais, como ficheiros do QuickBooks da empresa. Todos os dados confidenciais devem residir externo tooAzure RemoteApp num servidor de ficheiros, outra VM do Azure, ou no SQL Azure. imagem de Olá deve apenas Olá aplicação anfitriã que se liga a origem de dados de toohello e apresenta dados de Olá. Reveja [requisitos para o Azure RemoteApp imagens](remoteapp-imagereqs.md) para obter mais informações. 

toounderstand por que motivo não deve armazenar dados confidenciais, tem de toounderstand como funciona o Azure RemoteApp. Quando uma coleção é criada ou atualizada, em segundo plano de Olá vários clones ou cópias da imagem de Olá são criadas. Todas as instâncias de VM são réplicas exatas de imagem personalizada Olá; Quando os utilizadores iniciarem aplicações estão ligado tooone destas instâncias VM. Mas hello mesma instância não é garantida e deve importa porque são não persistentes. Olá, instâncias de VM alojamento Olá aplicações são não persistentes e podem ser destruída ou eliminada com base, por exemplo, durante a atualização da coleção. 

Depois de coleção de Olá está aprovisionada e os utilizadores iniciam a ligação toohello VMs, dados de utilizador são persistentes e protegidos porque é guardado em armazenamento separado dentro de uma imagem VHD que chamamos um [disco de perfil de utilizador (UDP)](remoteapp-upd.md), que é que o perfil de utilizador Olá no c:\users\<userprofile >. Quando uma aplicação é iniciado, Olá UPD está montado e tratada, tal como um perfil de utilizador local pelo sistema de operativo Olá. Leia mais sobre como [Azure RemoteApp guarda os dados de utilizador e definições](remoteapp-upd.md).

Dados de exemplo que não devem residir na imagem de Olá:

* Dados partilhada para os utilizadores tooaccess
* BD do SQL ou base de dados de QuickBooks
* Todos os dados em D:\

Dados de exemplo que podem residir em Olá predefinido perfil toobe copiado para UPD todos os utilizadores:

* Ficheiros de configuração por utilizador
* Scripts que os utilizadores teriam preservados na respetiva UPD

Pontos de chave:

* Nunca armazene dados confidenciais que podem ser perdidos no imagem Olá ao criar uma imagem personalizada.
* Os dados confidenciais deve sempre residem num servidor de ficheiros separado, separe VM do Azure, na nuvem de Olá e instâncias de VM toohello externo sempre que aloja as suas aplicações no Azure RemoteApp. 
* Dados de utilizador são guardados e persistir no disco de perfil de utilizador de Olá (UDP)

