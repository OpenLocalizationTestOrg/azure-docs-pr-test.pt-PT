---
title: aaaCreate e partilhar dashboards de portais do Azure | Microsoft Docs
description: "Este artigo explica como dashboards toocreate e editar no Olá portal do Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a><span data-ttu-id="392b1-103">Criar e partilhar dashboards no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="392b1-103">Create and share dashboards in hello Azure portal</span></span>
<span data-ttu-id="392b1-104">Pode criar dashboards vários e partilhá-los com outras pessoas que têm acesso tooyour Azure subscrições.</span><span class="sxs-lookup"><span data-stu-id="392b1-104">You can create multiple dashboards and share them with others who have access tooyour Azure subscriptions.</span></span>  <span data-ttu-id="392b1-105">Este artigo atravessa Olá Noções básicas sobre criar, editar, publicar e gerir o acesso toodashboards.</span><span class="sxs-lookup"><span data-stu-id="392b1-105">This article goes through hello basics of creating, editing, publishing, and managing access toodashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="392b1-106">Criar um dashboard</span><span class="sxs-lookup"><span data-stu-id="392b1-106">Create a dashboard</span></span>
<span data-ttu-id="392b1-107">toocreate um dashboard, selecione de Olá **novo dashboard** no botão seguinte toohello atual do nome do dashboard.</span><span class="sxs-lookup"><span data-stu-id="392b1-107">toocreate a dashboard, select hello **New dashboard** button next toohello current dashboard's name.</span></span>  

![criar o dashboard](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="392b1-109">Esta ação cria um dashboard novo, vazio, privado e coloca-o no modo de personalização onde pode nome o dashboard e adicionar ou reorganizar os mosaicos.</span><span class="sxs-lookup"><span data-stu-id="392b1-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="392b1-110">Neste modo, Olá expansível mosaico Galeria demora através do menu de navegação esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="392b1-110">When in this mode, hello collapsible tile gallery takes over hello left navigation menu.</span></span>  <span data-ttu-id="392b1-111">Olá mosaico galeria permite-lhe localizar mosaicos para os seus recursos do Azure de várias formas: pode procurar por [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), por tipo de recurso, por [tag](../azure-resource-manager/resource-group-using-tags.md), ou ao pesquisar para o seu recurso por nome.</span><span class="sxs-lookup"><span data-stu-id="392b1-111">hello tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![Personalizar o dashboard](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="392b1-113">Adicione peças de mosaicos e largue-os para a superfície de dashboard olá onde quiser.</span><span class="sxs-lookup"><span data-stu-id="392b1-113">Add tiles by dragging and dropping them onto hello dashboard surface wherever you want.</span></span>

<span data-ttu-id="392b1-114">Há uma nova categoria designada **geral** para mosaicos não estão associados um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="392b1-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="392b1-115">Neste exemplo, vamos afixar mosaico de Markdown Olá.</span><span class="sxs-lookup"><span data-stu-id="392b1-115">In this example, we pin hello Markdown tile.</span></span>  <span data-ttu-id="392b1-116">Utilize este dashboard do mosaico tooadd tooyour conteúdo personalizado.</span><span class="sxs-lookup"><span data-stu-id="392b1-116">You use this tile tooadd custom content tooyour dashboard.</span></span>  <span data-ttu-id="392b1-117">Olá mosaico suporta texto simples, [sintaxe de Markdown](https://daringfireball.net/projects/markdown/syntax)e um conjunto limitado de HTML.</span><span class="sxs-lookup"><span data-stu-id="392b1-117">hello tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="392b1-118">(Para segurança, que não pode fazer coisas como injetar `<script>` etiquetas ou utilizar determinado elemento estilo CSS pode interferir com o portal de Olá.)</span><span class="sxs-lookup"><span data-stu-id="392b1-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with hello portal.)</span></span> 

![adicionar o markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="392b1-120">Editar um dashboard</span><span class="sxs-lookup"><span data-stu-id="392b1-120">Edit a dashboard</span></span>
<span data-ttu-id="392b1-121">Depois de criar o dashboard, pode afixar mosaicos a partir da galeria do mosaico de Olá ou representação de mosaico Olá de painéis.</span><span class="sxs-lookup"><span data-stu-id="392b1-121">After creating your dashboard, you can pin tiles from hello tile gallery or hello tile representation of blades.</span></span> <span data-ttu-id="392b1-122">Vamos afixar representação Olá do nosso grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="392b1-122">Let's pin hello representation of our resource group.</span></span> <span data-ttu-id="392b1-123">Pode optar por afixar ao procurar Olá item, ou a partir do painel do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="392b1-123">You can either pin when browsing hello item, or from hello resource group blade.</span></span> <span data-ttu-id="392b1-124">Ambas as abordagens resultam em representação de mosaico Olá Olá do grupo de recursos de afixação.</span><span class="sxs-lookup"><span data-stu-id="392b1-124">Both approaches result in pinning hello tile representation of hello resource group.</span></span>

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="392b1-126">Após da afixação item Olá, aparece no dashboard.</span><span class="sxs-lookup"><span data-stu-id="392b1-126">After pinning hello item, it appears on your dashboard.</span></span>

![Veja o dashboard](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="392b1-128">Agora que temos um mosaico de Markdown e um dashboard de toohello afixado do grupo de recursos, mas pode redimensionar e reorganizar os mosaicos de Olá para um esquema adequado.</span><span class="sxs-lookup"><span data-stu-id="392b1-128">Now that we have a Markdown tile and a resource group pinned toohello dashboard, we can resize and rearrange hello tiles into a suitable layout.</span></span>

<span data-ttu-id="392b1-129">Por posicionado e selecionando "..." ou clicar num mosaico, pode ver todos os comandos de nível contextual das Olá para este mosaico.</span><span class="sxs-lookup"><span data-stu-id="392b1-129">By hovering and selecting "…" or right-clicking on a tile you can see all hello contextual commands for that tile.</span></span> <span data-ttu-id="392b1-130">Por predefinição, existem dois itens:</span><span class="sxs-lookup"><span data-stu-id="392b1-130">By default, there are two items:</span></span>

1. <span data-ttu-id="392b1-131">**Remover a partir do dashboard** – remove Olá mosaico do dashboard de Olá</span><span class="sxs-lookup"><span data-stu-id="392b1-131">**Unpin from dashboard** – removes hello tile from hello dashboard</span></span>
2. <span data-ttu-id="392b1-132">**Personalizar** – entra modo de personalização</span><span class="sxs-lookup"><span data-stu-id="392b1-132">**Customize** – enters customize mode</span></span>

![Personalizar o mosaico](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="392b1-134">Selecionando personalizar, pode redimensionar e reordenar os mosaicos.</span><span class="sxs-lookup"><span data-stu-id="392b1-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="392b1-135">um mosaico, selecione de tooresize Olá novo tamanho do menu de nível contextual das Olá, conforme mostrado no Olá seguinte imagem.</span><span class="sxs-lookup"><span data-stu-id="392b1-135">tooresize a tile, select hello new size from hello contextual menu, as shown in hello following image.</span></span>

![redimensionar o mosaico](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="392b1-137">Em alternativa, se o mosaico de Olá suporta qualquer tamanho, pode arrastar o tamanho do Olá inferior canto direito toohello assim o desejar.</span><span class="sxs-lookup"><span data-stu-id="392b1-137">Or, if hello tile supports any size, you can drag hello bottom right-hand corner toohello desired size.</span></span>

![redimensionar o mosaico](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="392b1-139">Depois de o redimensionamento de mosaicos, ver o dashboard de Olá.</span><span class="sxs-lookup"><span data-stu-id="392b1-139">After resizing tiles, view hello dashboard.</span></span>

![mosaico de vista](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="392b1-141">Quando tiver terminado de personalizar um dashboard, basta selecionar Olá **feito personalizar** tooexit personalizar modo ou com o botão direito e selecione **feito personalizar** no menu de contexto de Olá.</span><span class="sxs-lookup"><span data-stu-id="392b1-141">Once you are finished customizing a dashboard, simply select hello **Done customizing** tooexit customize mode or right-click and select **Done customizing** from hello context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="392b1-142">Publicar um dashboard e gerir o controlo de acesso</span><span class="sxs-lookup"><span data-stu-id="392b1-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="392b1-143">Quando cria um dashboard, é privado por predefinição, o que significa que é Olá só quem pode vê-lo.</span><span class="sxs-lookup"><span data-stu-id="392b1-143">When you create a dashboard, it is private by default, which means you are hello only person who can see it.</span></span>  <span data-ttu-id="392b1-144">toomake-lo visível tooothers, utilize Olá **partilha** Olá de botão que é apresentada juntamente com outros comandos do dashboard.</span><span class="sxs-lookup"><span data-stu-id="392b1-144">toomake it visible tooothers, use hello **Share** button that appears alongside hello other dashboard commands.</span></span>

![Partilhe o dashboard](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="392b1-146">É-lhe perguntado toochoose que um grupo de recursos e subscrição para o seu dashboard toobe publicado.</span><span class="sxs-lookup"><span data-stu-id="392b1-146">You are asked toochoose a subscription and resource group for your dashboard toobe published to.</span></span> <span data-ttu-id="392b1-147">tooseamlessly integrar dashboards do ecossistema de Olá, iremos tiver implementado dashboards partilhados como recursos do Azure (para que não é possível partilhar, escrevendo um endereço de e-mail).</span><span class="sxs-lookup"><span data-stu-id="392b1-147">tooseamlessly integrate dashboards into hello ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="392b1-148">Informação de toohello de acesso apresentada pela maioria dos mosaicos Olá no portal de Olá são regidos pelas [controlo de acesso baseado em do Azure funções](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="392b1-148">Access toohello information displayed by most of hello tiles in hello portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="392b1-149">De uma perspetiva de controlo de acesso partilhados dashboards são não diferentes de uma máquina virtual ou uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="392b1-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="392b1-150">Vamos supor que tiver uma subscrição do Azure e os membros da sua equipa tenham sido atribuídos a funções de Olá de **proprietário**, **contribuinte**, ou **leitor** da subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="392b1-150">Let's say you have an Azure subscription and members of your team have been assigned hello roles of **owner**, **contributor**, or **reader** of hello subscription.</span></span>  <span data-ttu-id="392b1-151">Os utilizadores que são proprietários ou contribuintes são toolist capaz, ver, criar, modificar ou eliminar dashboards dentro dessa subscrição.</span><span class="sxs-lookup"><span data-stu-id="392b1-151">Users who are owners or contributors are able toolist, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="392b1-152">Os utilizadores que são leitores são capazes de dashboards toolist e vista, mas não é possível modificar ou eliminar.</span><span class="sxs-lookup"><span data-stu-id="392b1-152">Users who are readers are able toolist and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="392b1-153">Os utilizadores com acesso de leitor são dashboard partilhado do toomake capaz de edições locais tooa, mas são toopublish não é possível servidor de back toohello essas alterações.</span><span class="sxs-lookup"><span data-stu-id="392b1-153">Users with reader access are able toomake local edits tooa shared dashboard, but are not able toopublish those changes back toohello server.</span></span>  <span data-ttu-id="392b1-154">No entanto, fazer uma cópia do dashboard de Olá para as seus próprios utilização privada.</span><span class="sxs-lookup"><span data-stu-id="392b1-154">However, they can make a private copy of hello dashboard for their own use.</span></span>  <span data-ttu-id="392b1-155">Como sempre, individuais mosaicos no dashboard de Olá impor as suas próprias regras de controlo de acesso com base nos recursos de Olá que correspondem a.</span><span class="sxs-lookup"><span data-stu-id="392b1-155">As always, individual tiles on hello dashboard enforce their own access control rules based on hello resources they correspond to.</span></span>  

<span data-ttu-id="392b1-156">Para sua comodidade, portal Olá da publicação de guias de experiência, para um padrão onde colocar dashboards num grupo de recursos chamado **dashboards**.</span><span class="sxs-lookup"><span data-stu-id="392b1-156">For convenience, hello portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![Publicar o dashboard](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="392b1-158">Também pode escolher toopublish um grupo de recurso específico de tooa do dashboard.</span><span class="sxs-lookup"><span data-stu-id="392b1-158">You can also choose toopublish a dashboard tooa particular resource group.</span></span>  <span data-ttu-id="392b1-159">controlo de acesso de Olá para esse dashboard corresponde ao controlo de acesso de Olá Olá grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="392b1-159">hello access control for that dashboard matches hello access control for hello resource group.</span></span>  <span data-ttu-id="392b1-160">Os utilizadores que podem gerir os recursos de Olá nesse grupo de recursos têm também acesso toohello dashboards.</span><span class="sxs-lookup"><span data-stu-id="392b1-160">Users that can manage hello resources in that resource group also have access toohello dashboards.</span></span>

![publicar o grupo de tooresource do dashboard](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="392b1-162">Depois do dashboard é publicado, Olá **partilha + acesso** painel de controlo irá atualizar e mostrar-lhe informações sobre o dashboard publicados Olá, incluindo um dashboard de toohello de acesso de utilizador de toomanage de ligação.</span><span class="sxs-lookup"><span data-stu-id="392b1-162">After your dashboard is published, hello **Sharing + access** control pane will refresh and show you information about hello published dashboard, including a link toomanage user access toohello dashboard.</span></span>  <span data-ttu-id="392b1-163">Esta ligação inicia Olá padrão controlo de acesso baseado em funções painel utilizado toomanage acesso para qualquer recurso do Azure.</span><span class="sxs-lookup"><span data-stu-id="392b1-163">This link launches hello standard Role Based Access Control blade used toomanage access for any Azure resource.</span></span>  <span data-ttu-id="392b1-164">Pode sempre regressar toothis vista selecionando **partilha**.</span><span class="sxs-lookup"><span data-stu-id="392b1-164">You can always get back toothis view by selecting **Share**.</span></span>

![Gerir o controlo de acesso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="392b1-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="392b1-166">Next steps</span></span>
* <span data-ttu-id="392b1-167">toomanage recursos, consulte [recursos do Azure de gerir através do portal](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="392b1-167">toomanage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="392b1-168">toodeploy recursos, consulte [implementar recursos com modelos do Resource Manager e o portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="392b1-168">toodeploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

