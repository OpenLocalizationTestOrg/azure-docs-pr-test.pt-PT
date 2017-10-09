---
title: aaaIntegrate Cofre de chaves com o SQL Server em VMs do Windows no Azure (Resource Manager) | Microsoft Docs
description: "Saiba como tooautomate Olá configuração de encriptação do SQL Server para utilização com o Cofre de chaves do Azure. Este tópico explica como toouse integração do Cofre de chaves do Azure com o SQL Server máquinas de virtuais criados com o Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="32da2-104">Configurar a integração do Cofre de chaves do Azure para o SQL Server em Virtual Machines do Azure (Gestor de recursos)</span><span class="sxs-lookup"><span data-stu-id="32da2-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32da2-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32da2-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="32da2-106">Clássico</span><span class="sxs-lookup"><span data-stu-id="32da2-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="32da2-107">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="32da2-107">Overview</span></span>
<span data-ttu-id="32da2-108">Existem várias funcionalidades de encriptação do SQL Server, tais como [encriptação de dados transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [encriptação de nível de coluna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), e [encriptação de cópias de segurança](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="32da2-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="32da2-109">Estes formulários de encriptação requerem toomanage e armazenam as chaves criptográficas Olá que utilizar para a encriptação.</span><span class="sxs-lookup"><span data-stu-id="32da2-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="32da2-110">Olá serviço Cofre de chaves do Azure (AKV) é concebida tooimprove Olá segurança e a gestão destas chaves numa localização segura e altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="32da2-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="32da2-111">Olá [conector do SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permite que o SQL Server toouse estas chaves a partir do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="32da2-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="32da2-112">Se a execução do SQL Server no local máquinas, existe são [passos que pode seguir tooaccess Cofre de chaves do Azure a partir do seu computador do SQL Server no local](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="32da2-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="32da2-113">Mas para o SQL Server em VMs do Azure, pode poupar tempo ao utilizar Olá *integração do Cofre de chaves do Azure* funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="32da2-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="32da2-114">Quando esta funcionalidade está ativada, é automaticamente instalada Olá conector do SQL Server, configura tooaccess de fornecedor EKM Olá Cofre de chaves do Azure e cria Olá credencial tooallow que tooaccess o cofre.</span><span class="sxs-lookup"><span data-stu-id="32da2-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="32da2-115">Se de que consultou passos Olá Olá mencionado anteriormente documentação no local, pode ver que esta funcionalidade automatiza os passos 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="32da2-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="32da2-116">Olá única coisa que ainda terá toodo manualmente é o Cofre de chaves do toocreate Olá e as chaves.</span><span class="sxs-lookup"><span data-stu-id="32da2-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="32da2-117">A partir daí, a configuração completa Olá da sua VM do SQL Server é um processo automatizada.</span><span class="sxs-lookup"><span data-stu-id="32da2-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="32da2-118">Depois desta funcionalidade concluída esta configuração, pode executar T-SQL instruções toobegin encriptar as cópias de segurança ou bases de dados, como faria normalmente.</span><span class="sxs-lookup"><span data-stu-id="32da2-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="32da2-119">Ativar e configurar a integração AKV</span><span class="sxs-lookup"><span data-stu-id="32da2-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="32da2-120">Pode ativar a integração AKV durante o aprovisionamento ou configurá-la para VMs existentes.</span><span class="sxs-lookup"><span data-stu-id="32da2-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="32da2-121">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="32da2-121">New VMs</span></span>
<span data-ttu-id="32da2-122">Se estiver a aprovisionar uma nova máquina de virtual do SQL Server com o Resource Manager, Olá portal do Azure fornece um tooenable passo integração do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="32da2-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="32da2-123">funcionalidade do Cofre de chaves do Azure de Olá só está disponível para Olá Enterprise, Developer e edições de avaliação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="32da2-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integração do Cofre de Chaves do SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="32da2-125">Para obter instruções detalhadas de aprovisionamento, consulte [aprovisionar uma máquina virtual do SQL Server no Portal do Azure de Olá](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="32da2-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="32da2-126">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="32da2-126">Existing VMs</span></span>
<span data-ttu-id="32da2-127">Para máquinas virtuais do SQL Server existentes, selecione a máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="32da2-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="32da2-128">Em seguida, selecione Olá **configuração do SQL Server** secção Olá **definições** painel.</span><span class="sxs-lookup"><span data-stu-id="32da2-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Integração AKV SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="32da2-130">No Olá **configuração do SQL Server** painel, clique em Olá **editar** botão no Olá secção de integração do Cofre de chaves automatizada.</span><span class="sxs-lookup"><span data-stu-id="32da2-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Configurar a integração AKV SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="32da2-132">Quando terminar, clique em Olá **OK** botão Olá parte inferior da Olá **configuração do SQL Server** painel toosave as suas alterações.</span><span class="sxs-lookup"><span data-stu-id="32da2-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="32da2-133">Também pode configurar a integração AKV através de um modelo.</span><span class="sxs-lookup"><span data-stu-id="32da2-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="32da2-134">Para obter mais informações, consulte [modelo de início rápido do Azure para a integração do Cofre de chaves do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="32da2-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

