---
title: aaaCreate e gerir a base de dados do Azure para o servidor de MySQL utilizando o portal do Azure | Microsoft Docs
description: "Este artigo descreve como pode rapidamente criar uma nova base de dados do Azure para o servidor de MySQL e gerir o servidor de Olá utilizando Olá Portal do Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="50a51-103">Criar e gerir a base de dados do Azure para o servidor de MySQL utilizando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="50a51-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="50a51-104">Este artigo descreve como pode rapidamente criar uma nova base de dados do Azure para o servidor de MySQL e gerir o servidor de Olá utilizando Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="50a51-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="50a51-105">Gestão de servidor inclui visualizar detalhes do servidor e as bases de dados, repor palavra-passe e a eliminação Olá servidor.</span><span class="sxs-lookup"><span data-stu-id="50a51-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="50a51-106">Início de sessão toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="50a51-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="50a51-107">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="50a51-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="50a51-108">Criar uma Base de Dados do Azure para o servidor MySQL</span><span class="sxs-lookup"><span data-stu-id="50a51-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="50a51-109">Siga estes passos toocreate uma base de dados do Azure para o servidor de MySQL com o nome "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="50a51-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="50a51-110">Clique 1 **novo** botão encontrado no canto esquerda superior Olá de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="50a51-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="50a51-111">Selecione 2 **bases de dados** da página Olá e selecione **base de dados do Azure para MySQL** da página de bases de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="50a51-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="50a51-112">É criada uma base de dados do Azure para o servidor de MySQL com um conjunto definido de [computação e armazenamento](./concepts-compute-unit-and-storage.md) recursos.</span><span class="sxs-lookup"><span data-stu-id="50a51-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="50a51-113">base de dados de Olá é criado dentro de um grupo de recursos do Azure e numa base de dados do Azure para o servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="50a51-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![Criar novo-servidor](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="50a51-115">3 - preencha Olá base de dados do Azure para o formulário de MySQL com Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="50a51-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="50a51-116">**Campo do Formulário**</span><span class="sxs-lookup"><span data-stu-id="50a51-116">**Form Field**</span></span> | <span data-ttu-id="50a51-117">**Descrição do Campo**</span><span class="sxs-lookup"><span data-stu-id="50a51-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="50a51-118">*Nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="50a51-118">*Server name*</span></span> | <span data-ttu-id="50a51-119">Azure mysql (nome do servidor é exclusivo global)</span><span class="sxs-lookup"><span data-stu-id="50a51-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="50a51-120">*Subscrição*</span><span class="sxs-lookup"><span data-stu-id="50a51-120">*Subscription*</span></span> | <span data-ttu-id="50a51-121">MySQLaaS (selecione na lista pendente)</span><span class="sxs-lookup"><span data-stu-id="50a51-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="50a51-122">*Grupo de recursos*</span><span class="sxs-lookup"><span data-stu-id="50a51-122">*Resource group*</span></span> | <span data-ttu-id="50a51-123">MyResource (criar um novo grupo de recursos ou utilize uma já existente)</span><span class="sxs-lookup"><span data-stu-id="50a51-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="50a51-124">*Início de sessão de administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="50a51-124">*Server admin login*</span></span> | <span data-ttu-id="50a51-125">myadmin (configure o nome da conta de administração)</span><span class="sxs-lookup"><span data-stu-id="50a51-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="50a51-126">*Palavra-passe*</span><span class="sxs-lookup"><span data-stu-id="50a51-126">*Password*</span></span> | <span data-ttu-id="50a51-127">palavra-passe de conta de administrador a configuração</span><span class="sxs-lookup"><span data-stu-id="50a51-127">setup admin account password</span></span> |
| <span data-ttu-id="50a51-128">*Confirmar palavra-passe*</span><span class="sxs-lookup"><span data-stu-id="50a51-128">*Confirm password*</span></span> | <span data-ttu-id="50a51-129">confirme a palavra-passe da conta de administrador</span><span class="sxs-lookup"><span data-stu-id="50a51-129">confirm admin account password</span></span> |
| <span data-ttu-id="50a51-130">*Localização*</span><span class="sxs-lookup"><span data-stu-id="50a51-130">*Location*</span></span> | <span data-ttu-id="50a51-131">Europa do Norte (selecione entre Europa do Norte e EUA oeste)</span><span class="sxs-lookup"><span data-stu-id="50a51-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="50a51-132">*Versão*</span><span class="sxs-lookup"><span data-stu-id="50a51-132">*Version*</span></span> | <span data-ttu-id="50a51-133">5.6 (escolher a base de dados do Azure para a versão do servidor MySQL)</span><span class="sxs-lookup"><span data-stu-id="50a51-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="50a51-134">Clique 4 **escalão de preço** toospecify Olá camada e o desempenho do nível de serviço para o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="50a51-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="50a51-135">Unidade pode ser configurada entre 50 e 100 na camada básica, 100 e 200 no escalão Standard, e o armazenamento pode ser adicionado, com base na quantidade incluída de computação.</span><span class="sxs-lookup"><span data-stu-id="50a51-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="50a51-136">Para este guia HowTo, vamos escolha a unidade de computação de 50 e 50GB.</span><span class="sxs-lookup"><span data-stu-id="50a51-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="50a51-137">Clique em **OK** toosave a seleção.</span><span class="sxs-lookup"><span data-stu-id="50a51-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="50a51-138">![Criar-server--escalão de preço](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="50a51-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="50a51-139">Clique 5 **criar** servidor de Olá tooprovision.</span><span class="sxs-lookup"><span data-stu-id="50a51-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="50a51-140">O aprovisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="50a51-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="50a51-141">Verifique Olá **Pin toodashboard** controlo de fácil tooallow opção das implementações.</span><span class="sxs-lookup"><span data-stu-id="50a51-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="50a51-142">Apesar de segurança too1000GB na camada básica e 10000GB padrão camada será suportada para armazenamento, para a pré-visualização pública, o armazenamento máximo Olá está temporariamente too1000GB ainda limitado.</span><span class="sxs-lookup"><span data-stu-id="50a51-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="50a51-143">Atualizar uma base de dados do Azure para o servidor de MySQL</span><span class="sxs-lookup"><span data-stu-id="50a51-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="50a51-144">Depois do novo servidor é aprovisionado, o utilizador tem 2 opções tooedit um servidor existente: Repor palavra-passe de administrador ou escala cima/para baixo servidor Olá alterando computação-unidades de Olá.</span><span class="sxs-lookup"><span data-stu-id="50a51-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="50a51-145">Palavra-passe de utilizador do administrador de Olá de alteração</span><span class="sxs-lookup"><span data-stu-id="50a51-145">Change hello administrator user password</span></span>
<span data-ttu-id="50a51-146">1 - no servidor de Olá **descrição geral** painel, clique em **Repor palavra-passe** toopopulate uma janela de entrada e a confirmação da palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="50a51-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="50a51-147">2 - Introduza a nova palavra-passe e Confirmar palavra-passe de Olá na janela de Olá como abaixo: ![reposição de palavra-passe](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="50a51-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="50a51-148">Clique 3 **OK** toosave Olá nova palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="50a51-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="50a51-149">Escala para cima/para baixo alterando as unidades de computação</span><span class="sxs-lookup"><span data-stu-id="50a51-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="50a51-150">1 - no painel do servidor de Olá, sob **definições**, clique em **escalão de preço** tooopen Olá preços camada painel Olá base de dados do Azure para o servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="50a51-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="50a51-151">Passo 2-siga 4 no **criar uma base de dados do Azure para o servidor de MySQL** toochange unidades de computação por Olá mesmo escalão de preço.</span><span class="sxs-lookup"><span data-stu-id="50a51-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="50a51-152">Eliminar uma base de dados do Azure para o servidor de MySQL</span><span class="sxs-lookup"><span data-stu-id="50a51-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="50a51-153">1 - no servidor de Olá **descrição geral** painel, clique em **eliminar** painel de confirmação de eliminação tooopen Olá comando botão.</span><span class="sxs-lookup"><span data-stu-id="50a51-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="50a51-154">Nome de servidor correto de tipo de 2 Olá na caixa de entrada do painel de Olá confirmação duplo.</span><span class="sxs-lookup"><span data-stu-id="50a51-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="50a51-155">Clique 3 **eliminar** botão novamente tooconfirm eliminar ação e aguarde pop-up "Eliminar êxito" na barra de notificação de Olá.</span><span class="sxs-lookup"><span data-stu-id="50a51-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="50a51-156">Lista Olá base de dados do Azure para bases de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="50a51-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="50a51-157">No servidor de Olá **descrição geral** painel, desloque para baixo até ver a base de dados de Olá mosaico na parte inferior de Olá.</span><span class="sxs-lookup"><span data-stu-id="50a51-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="50a51-158">Todas as bases de dados de Olá serão apresentados na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="50a51-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="50a51-159">Clique em **eliminar** painel de confirmação de eliminação tooopen Olá comando botão.</span><span class="sxs-lookup"><span data-stu-id="50a51-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![Mostrar-bases de dados](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="50a51-161">Mostrar detalhes de uma base de dados do Azure para o servidor de MySQL</span><span class="sxs-lookup"><span data-stu-id="50a51-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="50a51-162">Clique em **propriedades** em **definições** no servidor de Olá painel será aberto Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="50a51-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="50a51-163">Em seguida, pode ver todas as informações detalhadas sobre o servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="50a51-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50a51-164">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="50a51-164">Next steps</span></span>

[<span data-ttu-id="50a51-165">Início rápido: Criar a base de dados do Azure para o servidor de MySQL utilizando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="50a51-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
