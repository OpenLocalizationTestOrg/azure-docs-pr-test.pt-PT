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
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a><span data-ttu-id="645e3-103">Conteúdo de sincronização a partir de um tooAzure da pasta de nuvem do serviço de aplicações</span><span class="sxs-lookup"><span data-stu-id="645e3-103">Sync content from a cloud folder tooAzure App Service</span></span>
<span data-ttu-id="645e3-104">Este tutorial mostra como toodeploy demasiado[App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) por a sincronizar o seu conteúdo a partir de serviços de armazenamento de nuvem populares, como o Dropbox e OneDrive.</span><span class="sxs-lookup"><span data-stu-id="645e3-104">This tutorial shows you how toodeploy too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by syncing your content from popular cloud storage services like Dropbox and OneDrive.</span></span> 

## <span data-ttu-id="645e3-105"><a name="overview"></a>Descrição geral da implementação de conteúdo de sincronização</span><span class="sxs-lookup"><span data-stu-id="645e3-105"><a name="overview"></a>Overview of content sync deployment</span></span>
<span data-ttu-id="645e3-106">implementação de sincronização de conteúdo a pedido Olá utiliza a tecnologia de Olá [motor de implementação do Kudu](https://github.com/projectkudu/kudu/wiki) integrado com o serviço de aplicações.</span><span class="sxs-lookup"><span data-stu-id="645e3-106">hello on-demand content sync deployment is powered by hello [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki) integrated with App Service.</span></span> <span data-ttu-id="645e3-107">No Olá [Portal do Azure](https://portal.azure.com), pode designar uma pasta no seu armazenamento na nuvem, trabalhar com o código da aplicação e conteúdo nessa pasta e clique em Sincronizar tooApp serviço com Olá de um botão.</span><span class="sxs-lookup"><span data-stu-id="645e3-107">In hello [Azure Portal](https://portal.azure.com), you can designate a folder in your cloud storage, work with your app code and content in that folder, and sync tooApp Service with hello click of a button.</span></span> <span data-ttu-id="645e3-108">Sincronização conteúda utiliza o processo do Kudu Olá para a compilação e implementação.</span><span class="sxs-lookup"><span data-stu-id="645e3-108">Content sync utilizes hello Kudu process for build and deployment.</span></span> 

## <span data-ttu-id="645e3-109"><a name="contentsync"></a>Como o conteúdo de tooenable sincronizar a implementação</span><span class="sxs-lookup"><span data-stu-id="645e3-109"><a name="contentsync"></a>How tooenable content sync deployment</span></span>
<span data-ttu-id="645e3-110">sincronização de conteúdo tooenable de Olá [Portal do Azure](https://portal.azure.com), siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="645e3-110">tooenable content sync from hello [Azure Portal](https://portal.azure.com), follow these steps:</span></span>

1. <span data-ttu-id="645e3-111">No painel da sua aplicação no Portal do Azure de Olá, clique em **definições** > **origem de implementação**.</span><span class="sxs-lookup"><span data-stu-id="645e3-111">In your app's blade in hello Azure Portal, click **Settings** > **Deployment Source**.</span></span> <span data-ttu-id="645e3-112">Clique em **Escolher origem**, em seguida, selecione **OneDrive** ou **Dropbox** como origem de Olá para implementação.</span><span class="sxs-lookup"><span data-stu-id="645e3-112">Click **Choose Source**, then select **OneDrive** or **Dropbox** as hello source for deployment.</span></span> 
   
    ![Sincronização de conteúdo](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > <span data-ttu-id="645e3-114">Devido às diferenças subjacentes no Olá APIs, **OneDrive para empresas** não é suportado neste momento.</span><span class="sxs-lookup"><span data-stu-id="645e3-114">Because of underlying differences in hello APIs, **OneDrive for Business** is not supported at this time.</span></span> 
   > 
   > 
2. <span data-ttu-id="645e3-115">Tooenable de fluxo de trabalho de autorização de Olá concluída tooaccess do serviço de aplicações específico definido previamente caminho designado para o OneDrive ou Dropbox onde todo o conteúdo do serviço de aplicações será armazenado.</span><span class="sxs-lookup"><span data-stu-id="645e3-115">Complete hello authorization workflow tooenable App Service tooaccess a specific pre-defined designated path for OneDrive or Dropbox where all of your App Service content will be stored.</span></span>  
    <span data-ttu-id="645e3-116">Depois de Olá autorização plataforma do App Service irá dar-lhe Olá opção toocreate uma pasta de conteúdo em Olá designado caminho de conteúdo ou toochoose uma pasta de conteúdo existente sob este caminho de conteúdo designado.</span><span class="sxs-lookup"><span data-stu-id="645e3-116">After authorization hello App Service platform will give you hello option toocreate a content folder under hello designated content path, or toochoose an existing content folder under this designated content path.</span></span> <span data-ttu-id="645e3-117">caminhos de conteúdo de Olá designado sob as contas de armazenamento em nuvem utilizados para sincronização do serviço de aplicações são seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="645e3-117">hello designated content paths under your cloud storage accounts used for App Service sync are hello following:</span></span>  
   
   * <span data-ttu-id="645e3-118">**OneDrive**:`Apps\Azure Web Apps`</span><span class="sxs-lookup"><span data-stu-id="645e3-118">**OneDrive**: `Apps\Azure Web Apps`</span></span> 
   * <span data-ttu-id="645e3-119">**Dropbox**:`Dropbox\Apps\Azure`</span><span class="sxs-lookup"><span data-stu-id="645e3-119">**Dropbox**: `Dropbox\Apps\Azure`</span></span>
3. <span data-ttu-id="645e3-120">Depois de Olá sincronização de conteúdo de Olá de sincronização inicial de conteúdo pode ser iniciada no pedido a partir do Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="645e3-120">After hello initial content sync hello content sync can be initiated on demand from hello Azure portal.</span></span> <span data-ttu-id="645e3-121">Histórico de implementação está disponível com Olá **implementações** painel.</span><span class="sxs-lookup"><span data-stu-id="645e3-121">Deployment history is available with hello **Deployments** blade.</span></span>
   
    ![Histórico de implementação](./media/app-service-deploy-content-sync/onedrive_sync.png)

<span data-ttu-id="645e3-123">Estão disponíveis em mais informações para a implementação da Dropbox [implementar da Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span><span class="sxs-lookup"><span data-stu-id="645e3-123">More information for Dropbox deployment is available under [Deploy from Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx).</span></span> 

