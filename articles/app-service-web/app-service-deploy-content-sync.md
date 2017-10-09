---
title: "aaaSync conteúdo de um tooAzure da pasta de nuvem do serviço de aplicações"
description: "Saiba como toodeploy sua tooAzure de aplicação do serviço de aplicações através do conteúdo sincronizar a partir de uma pasta de nuvem."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Conteúdo de sincronização a partir de um tooAzure da pasta de nuvem do serviço de aplicações
Este tutorial mostra como toodeploy demasiado[App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) por a sincronizar o seu conteúdo a partir de serviços de armazenamento de nuvem populares, como o Dropbox e OneDrive. 

## <a name="overview"></a>Descrição geral da implementação de conteúdo de sincronização
implementação de sincronização de conteúdo a pedido Olá utiliza a tecnologia de Olá [motor de implementação do Kudu](https://github.com/projectkudu/kudu/wiki) integrado com o serviço de aplicações. No Olá [Portal do Azure](https://portal.azure.com), pode designar uma pasta no seu armazenamento na nuvem, trabalhar com o código da aplicação e conteúdo nessa pasta e clique em Sincronizar tooApp serviço com Olá de um botão. Sincronização conteúda utiliza o processo do Kudu Olá para a compilação e implementação. 

## <a name="contentsync"></a>Como o conteúdo de tooenable sincronizar a implementação
sincronização de conteúdo tooenable de Olá [Portal do Azure](https://portal.azure.com), siga estes passos:

1. No painel da sua aplicação no Portal do Azure de Olá, clique em **definições** > **origem de implementação**. Clique em **Escolher origem**, em seguida, selecione **OneDrive** ou **Dropbox** como origem de Olá para implementação. 
   
    ![Sincronização de conteúdo](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Devido às diferenças subjacentes no Olá APIs, **OneDrive para empresas** não é suportado neste momento. 
   > 
   > 
2. Tooenable de fluxo de trabalho de autorização de Olá concluída tooaccess do serviço de aplicações específico definido previamente caminho designado para o OneDrive ou Dropbox onde todo o conteúdo do serviço de aplicações será armazenado.  
    Depois de Olá autorização plataforma do App Service irá dar-lhe Olá opção toocreate uma pasta de conteúdo em Olá designado caminho de conteúdo ou toochoose uma pasta de conteúdo existente sob este caminho de conteúdo designado. caminhos de conteúdo de Olá designado sob as contas de armazenamento em nuvem utilizados para sincronização do serviço de aplicações são seguinte Olá:  
   
   * **OneDrive**:`Apps\Azure Web Apps` 
   * **Dropbox**:`Dropbox\Apps\Azure`
3. Depois de Olá sincronização de conteúdo de Olá de sincronização inicial de conteúdo pode ser iniciada no pedido a partir do Olá portal do Azure. Histórico de implementação está disponível com Olá **implementações** painel.
   
    ![Histórico de implementação](./media/app-service-deploy-content-sync/onedrive_sync.png)

Estão disponíveis em mais informações para a implementação da Dropbox [implementar da Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

