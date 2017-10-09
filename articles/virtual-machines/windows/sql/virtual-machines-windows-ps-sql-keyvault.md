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
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Configurar a integração do Cofre de chaves do Azure para o SQL Server em Virtual Machines do Azure (Gestor de recursos)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-ps-sql-keyvault.md)
> * [Clássico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Descrição geral
Existem várias funcionalidades de encriptação do SQL Server, tais como [encriptação de dados transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [encriptação de nível de coluna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), e [encriptação de cópias de segurança](https://msdn.microsoft.com/library/dn449489.aspx). Estes formulários de encriptação requerem toomanage e armazenam as chaves criptográficas Olá que utilizar para a encriptação. Olá serviço Cofre de chaves do Azure (AKV) é concebida tooimprove Olá segurança e a gestão destas chaves numa localização segura e altamente disponível. Olá [conector do SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permite que o SQL Server toouse estas chaves a partir do Cofre de chaves do Azure.

Se a execução do SQL Server no local máquinas, existe são [passos que pode seguir tooaccess Cofre de chaves do Azure a partir do seu computador do SQL Server no local](https://msdn.microsoft.com/library/dn198405.aspx). Mas para o SQL Server em VMs do Azure, pode poupar tempo ao utilizar Olá *integração do Cofre de chaves do Azure* funcionalidade.

Quando esta funcionalidade está ativada, é automaticamente instalada Olá conector do SQL Server, configura tooaccess de fornecedor EKM Olá Cofre de chaves do Azure e cria Olá credencial tooallow que tooaccess o cofre. Se de que consultou passos Olá Olá mencionado anteriormente documentação no local, pode ver que esta funcionalidade automatiza os passos 2 e 3. Olá única coisa que ainda terá toodo manualmente é o Cofre de chaves do toocreate Olá e as chaves. A partir daí, a configuração completa Olá da sua VM do SQL Server é um processo automatizada. Depois desta funcionalidade concluída esta configuração, pode executar T-SQL instruções toobegin encriptar as cópias de segurança ou bases de dados, como faria normalmente.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Ativar e configurar a integração AKV
Pode ativar a integração AKV durante o aprovisionamento ou configurá-la para VMs existentes.

### <a name="new-vms"></a>Novas VMs
Se estiver a aprovisionar uma nova máquina de virtual do SQL Server com o Resource Manager, Olá portal do Azure fornece um tooenable passo integração do Cofre de chaves do Azure. funcionalidade do Cofre de chaves do Azure de Olá só está disponível para Olá Enterprise, Developer e edições de avaliação do SQL Server.

![Integração do Cofre de Chaves do SQL Azure](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Para obter instruções detalhadas de aprovisionamento, consulte [aprovisionar uma máquina virtual do SQL Server no Portal do Azure de Olá](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>VMs existentes
Para máquinas virtuais do SQL Server existentes, selecione a máquina virtual do SQL Server. Em seguida, selecione Olá **configuração do SQL Server** secção Olá **definições** painel.

![Integração AKV SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

No Olá **configuração do SQL Server** painel, clique em Olá **editar** botão no Olá secção de integração do Cofre de chaves automatizada.

![Configurar a integração AKV SQL para VMs existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Quando terminar, clique em Olá **OK** botão Olá parte inferior da Olá **configuração do SQL Server** painel toosave as suas alterações.

> [!NOTE]
> Também pode configurar a integração AKV através de um modelo. Para obter mais informações, consulte [modelo de início rápido do Azure para a integração do Cofre de chaves do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

