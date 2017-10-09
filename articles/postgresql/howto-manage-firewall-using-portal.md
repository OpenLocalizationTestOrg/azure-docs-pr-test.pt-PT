---
title: "aaaCreate e gerir a base de dados do Azure PostgreSQL das regras de firewall utilizando Olá portal do Azure | Microsoft Docs"
description: "Criar e gerir a base de dados do Azure PostgreSQL das regras de firewall utilizando Olá portal do Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="fcb9c-103">Criar e gerir a base de dados do Azure PostgreSQL das regras de firewall utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fcb9c-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="fcb9c-104">Regras de firewall ao nível do servidor ativar administradores tooaccess uma base de dados do Azure para o servidor de PostgreSQL a partir de um endereço IP especificado ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fcb9c-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fcb9c-105">Prerequisites</span></span>
<span data-ttu-id="fcb9c-106">toostep através deste tooguide como, tem de:</span><span class="sxs-lookup"><span data-stu-id="fcb9c-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="fcb9c-107">Um servidor [criar uma base de dados do Azure para PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fcb9c-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="fcb9c-108">Criar uma regra de firewall ao nível do servidor no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fcb9c-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="fcb9c-109">No painel de servidor PostgreSQL Olá, em definições, clique em **ligação segurança** painel de segurança de ligação de Olá tooopen para Olá base de dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="fcb9c-111">Clique em **Adicionar IP do meu** na barra de ferramentas Olá.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="fcb9c-112">Isto irá criar automaticamente uma regra com o endereço IP Olá do seu computador, como percetível por Olá sistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Portal do Azure – clique em Adicionar meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="fcb9c-114">Verifique o seu endereço IP antes de guardar a configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="fcb9c-115">Em algumas situações, o endereço IP Olá observado pelo portal do Azure é diferente do endereço IP Olá utilizado quando aceder ao hello internet e os servidores do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="fcb9c-116">Por conseguinte, poderá ser necessário toochange Olá IP inicial e final IP toomake Olá regra função conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="fcb9c-117">Utilize um motor de busca ou outra ferramenta online toocheck os seus próprios endereços IP (por exemplo, pesquisa de Bing "qual é o meu IP").</span><span class="sxs-lookup"><span data-stu-id="fcb9c-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Pesquisa do Bing para saber o que é o meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="fcb9c-119">Adicione intervalos de endereços adicionais.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-119">Add additional address ranges.</span></span> <span data-ttu-id="fcb9c-120">Nas regras de Olá para Olá base de dados do Azure para PostgreSQL firewall, pode especificar um único endereço IP ou um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="fcb9c-121">Se quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final IP.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="fcb9c-122">Ao abrir a firewall Olá permite que os administradores e utilizadores toologin tooany da base de dados no Olá PostgreSQL servidor toowhich têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="fcb9c-123">Portal do Azure – regras de firewall</span><span class="sxs-lookup"><span data-stu-id="fcb9c-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="fcb9c-124">Clique em **guardar** no Olá toosave da barra de ferramentas, esta regra de firewall ao nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="fcb9c-125">Aguarde a confirmação de Olá Olá regras de firewall de toohello de atualização foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Portal do Azure – clique em Guardar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="fcb9c-127">Gerir regras de firewall ao nível do servidor existente através de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fcb9c-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="fcb9c-128">Repita Olá passos toomanage Olá as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="fcb9c-129">tooadd Olá do computador atual, clique no botão de Olá demasiado + **Adicionar IP do meu**.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="fcb9c-130">Clique em **guardar** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="fcb9c-131">endereços IP adicionais tooadd, escreva na Olá nome da regra, o endereço IP inicial e o endereço IP final.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="fcb9c-132">Clique em **guardar** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="fcb9c-133">toomodify uma regra existente, clique em qualquer um dos campos de Olá na regra Olá e modificar.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="fcb9c-134">Clique em **guardar** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="fcb9c-135">toodelete uma regra existente, clique em reticências Olá [...] e clicar eliminar remove Olá regra.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="fcb9c-136">Clique em **guardar** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="fcb9c-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcb9c-137">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fcb9c-137">Next steps</span></span>
- <span data-ttu-id="fcb9c-138">Da mesma forma, pode aplicar o script demasiado[criar e gerir a base de dados do Azure PostgreSQL das regras de firewall ao utilizar a CLI do Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="fcb9c-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="fcb9c-139">Para obter ajuda na ligação tooan base de dados do Azure para o servidor de PostgreSQL, consulte [bibliotecas de ligação para base de dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="fcb9c-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
