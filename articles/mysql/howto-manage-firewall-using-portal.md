---
title: "aaaCreate e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando Olá portal do Azure | Microsoft Docs"
description: "Criar e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando Olá portal do Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="9b02a-103">Criar e gerir a base de dados do Azure para as regras de firewall de MySQL utilizando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b02a-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="9b02a-104">Regras de firewall ao nível do servidor ativar administradores tooaccess uma base de dados do Azure para o servidor de MySQL a partir de um endereço IP especificado ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="9b02a-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="9b02a-105">Criar uma regra de firewall ao nível do servidor no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b02a-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="9b02a-106">No painel server, MySQL Olá, em definições, clique em **ligação segurança** painel de segurança de ligação de Olá tooopen para Olá base de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="9b02a-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="9b02a-108">Clique em **Adicionar IP do meu** na barra de ferramentas de Olá toocreate uma regra com o endereço IP Olá do seu computador, como interpretadas pela Olá sistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b02a-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Portal do Azure – clique em Adicionar meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="9b02a-110">Verifique o seu endereço IP antes de guardar a configuração de Olá.</span><span class="sxs-lookup"><span data-stu-id="9b02a-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="9b02a-111">Em algumas situações, o endereço IP Olá observado pelo portal do Azure é diferente do endereço IP Olá utilizado quando aceder ao hello internet e os servidores do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b02a-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="9b02a-112">Por conseguinte, poderá ser necessário toochange Olá IP inicial e final IP toomake Olá regra função conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="9b02a-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="9b02a-113">Utilizar um motor de busca ou outra ferramenta online toocheck o seu próprio endereço IP (por exemplo, pesquisar "qual é o meu endereço IP").</span><span class="sxs-lookup"><span data-stu-id="9b02a-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing para saber o que é o meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="9b02a-115">Adicione intervalos de endereços adicionais.</span><span class="sxs-lookup"><span data-stu-id="9b02a-115">Add additional address ranges.</span></span> <span data-ttu-id="9b02a-116">Nas regras de Olá para Olá base de dados do Azure para firewall de MySQL, pode especificar um único endereço IP ou um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="9b02a-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="9b02a-117">Se quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final IP.</span><span class="sxs-lookup"><span data-stu-id="9b02a-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="9b02a-118">Ao abrir a firewall Olá permite que os administradores e utilizadores tooaccess qualquer base de dados no Olá MySQL servidor toowhich têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="9b02a-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="9b02a-119">Portal do Azure – regras de firewall</span><span class="sxs-lookup"><span data-stu-id="9b02a-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="9b02a-120">Clique em **guardar** no Olá toosave da barra de ferramentas, esta regra de firewall ao nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="9b02a-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="9b02a-121">Aguarde a confirmação de Olá Olá regras de firewall de toohello de atualização foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="9b02a-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Portal do Azure – clique em Guardar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="9b02a-123">Gerir regras de firewall ao nível do servidor existente através de Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9b02a-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="9b02a-124">Repita Olá passos toomanage Olá as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="9b02a-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="9b02a-125">tooadd Olá do computador atual, clique em **+ adicionar My IP**.</span><span class="sxs-lookup"><span data-stu-id="9b02a-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="9b02a-126">endereços IP adicionais tooadd, escreva Olá **nome da regra**, **IP inicial**, e **IP final**.</span><span class="sxs-lookup"><span data-stu-id="9b02a-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="9b02a-127">toomodify uma regra existente, clique em qualquer um dos campos de Olá na regra Olá e modificar.</span><span class="sxs-lookup"><span data-stu-id="9b02a-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="9b02a-128">regra de toodelete existente, clique o botão de reticências Olá […] e clique em **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="9b02a-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="9b02a-129">Clique em **guardar** alterações de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="9b02a-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b02a-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9b02a-130">Next steps</span></span>
- <span data-ttu-id="9b02a-131">Para obter ajuda na ligação tooan base de dados do Azure para o servidor de MySQL, consulte [bibliotecas de ligação para base de dados do Azure para MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9b02a-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
