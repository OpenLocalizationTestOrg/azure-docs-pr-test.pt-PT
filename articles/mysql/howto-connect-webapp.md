---
title: aaaConnect tooAzure da App Service do Azure existente da base de dados MySQL | Microsoft Docs
description: "Instruções sobre como tooproperly ligar um tooAzure App Service do Azure existente da base de dados para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="855cf-103">Ligar um tooAzure App Service do Azure existente da base de dados para o servidor de MySQL</span><span class="sxs-lookup"><span data-stu-id="855cf-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="855cf-104">Este documento explica como tooconnect um tooyour App Service do Azure existente Azure base de dados para o servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="855cf-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="855cf-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="855cf-105">Before you begin</span></span>
<span data-ttu-id="855cf-106">Inicie sessão no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="855cf-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="855cf-107">Crie uma base de dados do Azure para o servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="855cf-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="855cf-108">Para obter detalhes, consulte demasiado[como toocreate Azure base de dados para o servidor de MySQL do Portal](quickstart-create-mysql-server-database-using-azure-portal.md) ou [como toocreate Azure base de dados para o servidor de MySQL utilizando a CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="855cf-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="855cf-109">Atualmente, existem duas soluções tooenable acesso a partir de uma base de dados do Azure de tooan do App Service do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="855cf-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="855cf-110">Ambas as soluções envolvem configurar regras de firewall ao nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="855cf-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="855cf-111">Solução 1 - criar um tooallow de regra de firewall todos os IPs</span><span class="sxs-lookup"><span data-stu-id="855cf-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="855cf-112">Base de dados do Azure para MySQL fornece segurança de acesso através de uma firewall tooprotect os dados.</span><span class="sxs-lookup"><span data-stu-id="855cf-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="855cf-113">Quando ligar a partir de um tooAzure do App Service do Azure da base de dados para o servidor de MySQL, tenha em atenção que Olá saída IPs de serviço de aplicações são dinâmicas natureza.</span><span class="sxs-lookup"><span data-stu-id="855cf-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="855cf-114">disponibilidade de Olá tooensure do seu serviço de aplicações do Azure, recomendamos que utilize tooallow esta solução todos os IPs.</span><span class="sxs-lookup"><span data-stu-id="855cf-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="855cf-115">Microsoft está a trabalhar para um tooavoid solução longo prazo, permitindo todos os IPs para serviços do Azure tooconnect tooAzure da base de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="855cf-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="855cf-116">No painel server, MySQL Olá, em definições, clique em **ligação segurança** painel de segurança de ligação de Olá tooopen para Olá base de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="855cf-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="855cf-118">Introduza **nome da regra**, **IP inicial**, e **IP final**.</span><span class="sxs-lookup"><span data-stu-id="855cf-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="855cf-119">Em seguida, clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="855cf-119">Then click **Save**.</span></span>
   - <span data-ttu-id="855cf-120">Nome da regra: permitir-All-IPs</span><span class="sxs-lookup"><span data-stu-id="855cf-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="855cf-121">Iniciar IP: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="855cf-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="855cf-122">IP de fim: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="855cf-122">End IP: 255.255.255.255</span></span>

   ![Portal do Azure – adicionar todos os IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="855cf-124">Solução 2 - criar uma firewall tooexplicitly de regra permitir IPs de saída</span><span class="sxs-lookup"><span data-stu-id="855cf-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="855cf-125">Pode adicionar explicitamente que Olá todos os IPs de saída do seu serviço de aplicações do Azure.</span><span class="sxs-lookup"><span data-stu-id="855cf-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="855cf-126">No painel de propriedades do serviço de aplicação Olá, ver o **saída endereço de IP**.</span><span class="sxs-lookup"><span data-stu-id="855cf-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portal do Azure – IPs de saída de vista](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="855cf-128">No painel de segurança de ligação de MySQL Olá, adicione IPs saída um por um.</span><span class="sxs-lookup"><span data-stu-id="855cf-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portal do Azure – adicionar IPs explícita](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="855cf-130">Lembre-se demasiado**guardar** regras da firewall.</span><span class="sxs-lookup"><span data-stu-id="855cf-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="855cf-131">Embora Olá App service do Azure tenta constante de endereços IP tookeep ao longo do tempo, há casos em que os endereços IP de Olá podem ser alterados.</span><span class="sxs-lookup"><span data-stu-id="855cf-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="855cf-132">Por exemplo, quando Olá aplicação recicla ocorre uma operação de escala, ou quando são adicionadas novas máquinas nos dados regionais Azure centros de capacidade de Olá tooincrease.</span><span class="sxs-lookup"><span data-stu-id="855cf-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="855cf-133">Quando a alteração de endereços IP de Olá, aplicação Olá foi tempo de inatividade no evento Olá que já não consegue estabelecer ligação toohello MySQL servidor.</span><span class="sxs-lookup"><span data-stu-id="855cf-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="855cf-134">Considere este potencial problema ao escolher uma das Olá precedente soluções.</span><span class="sxs-lookup"><span data-stu-id="855cf-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="855cf-135">Configuração de SSL</span><span class="sxs-lookup"><span data-stu-id="855cf-135">SSL configuration</span></span>
<span data-ttu-id="855cf-136">Base de dados do Azure para MySQL tem SSL ativado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="855cf-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="855cf-137">Se a aplicação não está a utilizar base de dados do SSL tooconnect toohello, em seguida, é necessário toodisable SSL no servidor de MySQL.</span><span class="sxs-lookup"><span data-stu-id="855cf-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="855cf-138">Para obter detalhes sobre como tooconfigure SSL, consulte [utilizando o SSL com a base de dados do Azure para MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="855cf-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="855cf-139">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="855cf-139">Next steps</span></span>
<span data-ttu-id="855cf-140">Para mais informações sobre cadeias de ligação, consulte demasiado[cadeias de ligação](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="855cf-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
