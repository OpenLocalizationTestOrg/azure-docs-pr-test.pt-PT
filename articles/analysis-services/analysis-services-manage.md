---
title: aaaManage Azure Analysis Services | Microsoft Docs
description: Saiba como toomanage um Analysis Services server no Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="44e36-103">Gerir do Analysis Services</span><span class="sxs-lookup"><span data-stu-id="44e36-103">Manage Analysis Services</span></span>
<span data-ttu-id="44e36-104">Depois de criar um servidor de Analysis Services no Azure, poderão existir algumas tarefas de administração e gestão terá tooperform de imediato ou algum tempo baixo Olá viagem.</span><span class="sxs-lookup"><span data-stu-id="44e36-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="44e36-105">Por exemplo, execute o processamento de dados de atualização de toohello, controlar quem pode aceder à modelos Olá no seu servidor, ou monitorizar estado de funcionamento do seu servidor.</span><span class="sxs-lookup"><span data-stu-id="44e36-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="44e36-106">Algumas tarefas de gestão só podem ser efetuadas no portal do Azure, outros no SQL Server Management Studio (SSMS), e algumas tarefas podem ser efetuadas no.</span><span class="sxs-lookup"><span data-stu-id="44e36-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="44e36-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="44e36-107">Azure portal</span></span>
<span data-ttu-id="44e36-108">[Portal do Azure](http://portal.azure.com/) é onde pode criar e eliminar servidores, monitorizar os recursos do servidor, altere o tamanho e gerir quem tem acesso tooyour servidores.</span><span class="sxs-lookup"><span data-stu-id="44e36-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="44e36-109">Se estiver a ter alguns problemas, também pode submeter um pedido de suporte.</span><span class="sxs-lookup"><span data-stu-id="44e36-109">If you're having some problems, you can also submit a support request.</span></span>

![Obter o nome do servidor no Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="44e36-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="44e36-111">SQL Server Management Studio</span></span>
<span data-ttu-id="44e36-112">Ligar o servidor tooyour no Azure é semelhante à ligação tooa instância de servidor na sua própria organização.</span><span class="sxs-lookup"><span data-stu-id="44e36-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="44e36-113">Do SSMS, pode efetuar muitas das Olá mesmo tarefas como processamento de dados ou criar um script de processamento, gerir funções e utilizar o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44e36-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="44e36-115">Transfira e instale o SSMS</span><span class="sxs-lookup"><span data-stu-id="44e36-115">Download and install SSMS</span></span>
<span data-ttu-id="44e36-116">tooget Olá todas as funcionalidades mais recentes e experiência smoothest Olá ao ligar o servidor de Analysis Services do Azure tooyour, certifique-se de que está a utilizar a versão mais recente do Olá do SSMS.</span><span class="sxs-lookup"><span data-stu-id="44e36-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="44e36-117">[Transferir o SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="44e36-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="44e36-118">tooconnect com SSMS</span><span class="sxs-lookup"><span data-stu-id="44e36-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="44e36-119">Quando com o SSMS, antes de hello do servidor tooyour ao ligar pela primeira vez, certifique-se de que o seu nome de utilizador está incluído no grupo de administradores de serviços de análise Olá.</span><span class="sxs-lookup"><span data-stu-id="44e36-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="44e36-120">toolearn mais, consulte [os administradores de servidores](#server-administrators) posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="44e36-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="44e36-121">Antes de ligar, precisa de nome do servidor tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="44e36-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="44e36-122">No **portal do Azure** > servidor > **descrição geral** > **nome do servidor**, nome do servidor de Olá de cópia.</span><span class="sxs-lookup"><span data-stu-id="44e36-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Obter o nome do servidor no Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="44e36-124">No SSMS > **Object Explorer**, clique em **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="44e36-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="44e36-125">No Olá **ligar tooServer** caixa de diálogo, colar no nome do servidor de Olá, em seguida, em **autenticação**, escolha um dos seguintes tipos de autenticação de Olá:</span><span class="sxs-lookup"><span data-stu-id="44e36-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="44e36-126">**Autenticação do Windows** toouse as credenciais de domínio ome de utilizador e palavra-passe do Windows.</span><span class="sxs-lookup"><span data-stu-id="44e36-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="44e36-127">**Autenticação de palavra-passe do Active Directory** toouse uma conta organizacional.</span><span class="sxs-lookup"><span data-stu-id="44e36-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="44e36-128">Por exemplo, quando ligar a partir de um domínio associado a um computador.</span><span class="sxs-lookup"><span data-stu-id="44e36-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="44e36-129">**Autenticação de Universal do Active Directory** toouse [autenticação não interativa ou multifator](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44e36-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Se ligar no SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="44e36-131">Os administradores de servidores e os utilizadores de base de dados</span><span class="sxs-lookup"><span data-stu-id="44e36-131">Server administrators and database users</span></span>
<span data-ttu-id="44e36-132">No Azure Analysis Services, existem dois tipos de utilizadores, os administradores de servidores e os utilizadores de base de dados.</span><span class="sxs-lookup"><span data-stu-id="44e36-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="44e36-133">Ambos os tipos de utilizadores tem de estar no seu Azure Active Directory e tem de ser especificados por endereço de e-mail empresarial ou UPN.</span><span class="sxs-lookup"><span data-stu-id="44e36-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="44e36-134">toolearn mais, consulte [permissões de autenticação e utilizador](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="44e36-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="44e36-135">Resolução de problemas de ligação</span><span class="sxs-lookup"><span data-stu-id="44e36-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="44e36-136">Ao estabelecer ligação com o SSMS, caso se depare com problemas, poderá ter de cache de início de sessão de Olá tooclear.</span><span class="sxs-lookup"><span data-stu-id="44e36-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="44e36-137">Nada é toodisc em cache.</span><span class="sxs-lookup"><span data-stu-id="44e36-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="44e36-138">tooclear Olá cache, feche e reinicie Olá ligar o processo.</span><span class="sxs-lookup"><span data-stu-id="44e36-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="44e36-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="44e36-139">Next steps</span></span>
<span data-ttu-id="44e36-140">Se já não tiver implementado um modelo em tabela tooyour novo servidor, agora é uma boa altura.</span><span class="sxs-lookup"><span data-stu-id="44e36-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="44e36-141">toolearn mais, consulte [implementar tooAzure Analysis Services](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="44e36-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="44e36-142">Se tiver implementado um servidor de tooyour modelo, está tooit tooconnect pronto a utilizar um cliente ou browser.</span><span class="sxs-lookup"><span data-stu-id="44e36-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="44e36-143">toolearn mais, consulte [obter dados a partir do servidor de Analysis Services do Azure](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="44e36-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

