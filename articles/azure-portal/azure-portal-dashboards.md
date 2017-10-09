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
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Criar e partilhar dashboards no Olá portal do Azure
Pode criar dashboards vários e partilhá-los com outras pessoas que têm acesso tooyour Azure subscrições.  Este artigo atravessa Olá Noções básicas sobre criar, editar, publicar e gerir o acesso toodashboards.

## <a name="create-a-dashboard"></a>Criar um dashboard
toocreate um dashboard, selecione de Olá **novo dashboard** no botão seguinte toohello atual do nome do dashboard.  

![criar o dashboard](./media/azure-portal-dashboards/new-dashboard.png)

Esta ação cria um dashboard novo, vazio, privado e coloca-o no modo de personalização onde pode nome o dashboard e adicionar ou reorganizar os mosaicos.  Neste modo, Olá expansível mosaico Galeria demora através do menu de navegação esquerdo Olá.  Olá mosaico galeria permite-lhe localizar mosaicos para os seus recursos do Azure de várias formas: pode procurar por [grupo de recursos](../azure-resource-manager/resource-group-overview.md#resource-groups), por tipo de recurso, por [tag](../azure-resource-manager/resource-group-using-tags.md), ou ao pesquisar para o seu recurso por nome.  

![Personalizar o dashboard](./media/azure-portal-dashboards/customize-dashboard.png)

Adicione peças de mosaicos e largue-os para a superfície de dashboard olá onde quiser.

Há uma nova categoria designada **geral** para mosaicos não estão associados um recurso específico.  Neste exemplo, vamos afixar mosaico de Markdown Olá.  Utilize este dashboard do mosaico tooadd tooyour conteúdo personalizado.  Olá mosaico suporta texto simples, [sintaxe de Markdown](https://daringfireball.net/projects/markdown/syntax)e um conjunto limitado de HTML.  (Para segurança, que não pode fazer coisas como injetar `<script>` etiquetas ou utilizar determinado elemento estilo CSS pode interferir com o portal de Olá.) 

![adicionar o markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Editar um dashboard
Depois de criar o dashboard, pode afixar mosaicos a partir da galeria do mosaico de Olá ou representação de mosaico Olá de painéis. Vamos afixar representação Olá do nosso grupo de recursos. Pode optar por afixar ao procurar Olá item, ou a partir do painel do grupo de recursos de Olá. Ambas as abordagens resultam em representação de mosaico Olá Olá do grupo de recursos de afixação.

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Após da afixação item Olá, aparece no dashboard.

![Veja o dashboard](./media/azure-portal-dashboards/view-dashboard.png)

Agora que temos um mosaico de Markdown e um dashboard de toohello afixado do grupo de recursos, mas pode redimensionar e reorganizar os mosaicos de Olá para um esquema adequado.

Por posicionado e selecionando "..." ou clicar num mosaico, pode ver todos os comandos de nível contextual das Olá para este mosaico. Por predefinição, existem dois itens:

1. **Remover a partir do dashboard** – remove Olá mosaico do dashboard de Olá
2. **Personalizar** – entra modo de personalização

![Personalizar o mosaico](./media/azure-portal-dashboards/customize-tile.png)

Selecionando personalizar, pode redimensionar e reordenar os mosaicos. um mosaico, selecione de tooresize Olá novo tamanho do menu de nível contextual das Olá, conforme mostrado no Olá seguinte imagem.

![redimensionar o mosaico](./media/azure-portal-dashboards/resize-tile.png)

Em alternativa, se o mosaico de Olá suporta qualquer tamanho, pode arrastar o tamanho do Olá inferior canto direito toohello assim o desejar.

![redimensionar o mosaico](./media/azure-portal-dashboards/resize-corner.png)

Depois de o redimensionamento de mosaicos, ver o dashboard de Olá.

![mosaico de vista](./media/azure-portal-dashboards/view-tile.png)

Quando tiver terminado de personalizar um dashboard, basta selecionar Olá **feito personalizar** tooexit personalizar modo ou com o botão direito e selecione **feito personalizar** no menu de contexto de Olá.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Publicar um dashboard e gerir o controlo de acesso
Quando cria um dashboard, é privado por predefinição, o que significa que é Olá só quem pode vê-lo.  toomake-lo visível tooothers, utilize Olá **partilha** Olá de botão que é apresentada juntamente com outros comandos do dashboard.

![Partilhe o dashboard](./media/azure-portal-dashboards/share-dashboard.png)

É-lhe perguntado toochoose que um grupo de recursos e subscrição para o seu dashboard toobe publicado. tooseamlessly integrar dashboards do ecossistema de Olá, iremos tiver implementado dashboards partilhados como recursos do Azure (para que não é possível partilhar, escrevendo um endereço de e-mail).  Informação de toohello de acesso apresentada pela maioria dos mosaicos Olá no portal de Olá são regidos pelas [controlo de acesso baseado em do Azure funções](../active-directory/role-based-access-control-configure.md). De uma perspetiva de controlo de acesso partilhados dashboards são não diferentes de uma máquina virtual ou uma conta de armazenamento.  

Vamos supor que tiver uma subscrição do Azure e os membros da sua equipa tenham sido atribuídos a funções de Olá de **proprietário**, **contribuinte**, ou **leitor** da subscrição Olá.  Os utilizadores que são proprietários ou contribuintes são toolist capaz, ver, criar, modificar ou eliminar dashboards dentro dessa subscrição.  Os utilizadores que são leitores são capazes de dashboards toolist e vista, mas não é possível modificar ou eliminar.  Os utilizadores com acesso de leitor são dashboard partilhado do toomake capaz de edições locais tooa, mas são toopublish não é possível servidor de back toohello essas alterações.  No entanto, fazer uma cópia do dashboard de Olá para as seus próprios utilização privada.  Como sempre, individuais mosaicos no dashboard de Olá impor as suas próprias regras de controlo de acesso com base nos recursos de Olá que correspondem a.  

Para sua comodidade, portal Olá da publicação de guias de experiência, para um padrão onde colocar dashboards num grupo de recursos chamado **dashboards**.  

![Publicar o dashboard](./media/azure-portal-dashboards/publish-dashboard.png)

Também pode escolher toopublish um grupo de recurso específico de tooa do dashboard.  controlo de acesso de Olá para esse dashboard corresponde ao controlo de acesso de Olá Olá grupo de recursos.  Os utilizadores que podem gerir os recursos de Olá nesse grupo de recursos têm também acesso toohello dashboards.

![publicar o grupo de tooresource do dashboard](./media/azure-portal-dashboards/publish-to-resource-group.png)

Depois do dashboard é publicado, Olá **partilha + acesso** painel de controlo irá atualizar e mostrar-lhe informações sobre o dashboard publicados Olá, incluindo um dashboard de toohello de acesso de utilizador de toomanage de ligação.  Esta ligação inicia Olá padrão controlo de acesso baseado em funções painel utilizado toomanage acesso para qualquer recurso do Azure.  Pode sempre regressar toothis vista selecionando **partilha**.

![Gerir o controlo de acesso](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Passos seguintes
* toomanage recursos, consulte [recursos do Azure de gerir através do portal](../azure-resource-manager/resource-group-portal.md).
* toodeploy recursos, consulte [implementar recursos com modelos do Resource Manager e o portal do Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).

