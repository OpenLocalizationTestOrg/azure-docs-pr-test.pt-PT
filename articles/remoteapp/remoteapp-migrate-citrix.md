---
title: aaaMigrate do Azure RemoteApp tooCitrix XenApp Essentials | Microsoft Docs
description: Como toomigrate do Azure RemoteApp tooCitrix XenApp Essentials
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 695a8165-3454-4855-8e21-f2eb2c61201b
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aa3ce28bc5a86d5b1dd3408196d51935395f55c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toocitrix-xenapp-essentials"></a>Migrar a partir do Azure RemoteApp tooCitrix XenApp Essentials

Se utilizar o Azure RemoteApp e quiser toomigrate tooCitrix XenApp Essentials, existem alguns pré-requisitos tookeep em mente. Em primeiro lugar, a leitura do Citrix [guia de implementação técnica do passo a passo para Citrix XenApp Essentials](https://docs.citrix.com/content/dam/docs/en-us/citrix-cloud/downloads/xenapp-essentials-deployment-guide.pdf) e a respetiva [online biblioteca técnica](http://docs.citrix.com/en-us/citrix-cloud/xenapp-and-xendesktop-service/xenapp-essentials.html). 

## <a name="prerequisite-steps-for-migration"></a>Passos de pré-requisitos para a migração

1. Criar uma nova rede virtual, ou a determinar qual no Gestor de recursos do Azure na qual implementará Citrix XenApp Essentials de rede virtual do Azure. O Azure RemoteApp utiliza Olá portal clássico do Azure; Citrix XenApp Essentials só suporta o Azure Resource Manager.  
2. Certifique-se de que Olá a rede virtual que selecionou tem redes de controlador de domínio do acesso tooyour, porque Citrix só suporta implementações híbridas. Se estiver a utilizar uma implementação de nuvem do Azure RemoteApp, certifique-se de que a rede virtual tem o controlador de domínio do Active Directory do acesso tooan de rede. Também pode utilizar o Azure Active Directory Domain Services (Azure AD DS). 
3. Certifique-se de que Olá que DNS está configurado corretamente para a rede virtual Olá, pelo que esse associação a um domínio é efetuada com êxito durante a primeira tentativa. Pode criar uma máquina virtual (VM) na rede virtual Olá que selecionou e efetuar uma tooverify de associação de domínio manual que Olá DNS e a associação a um domínio funciona conforme esperado. Isto garante que é efetuada com êxito Olá pela primeira vez que implementar Citrix XenApp Essentials. 
4. Se necessário, crie uma rede virtual peering entre uma rede do Azure clássica portal virtual que estiver a utilizar com o Azure RemoteApp e a rede virtual do Azure Resource Manager. Este processo peering funciona se a redes de Olá dois residem Olá mesma região. Caso contrário, utilize redes virtuais do site para site VPN tooconnect Olá para funcionamento em rede. 
5. Se necessário, leia [como dados toomigrate dentro e fora do Azure RemoteApp](remoteapp-migrate.md). 
6. Atualizar o seu Olá de tooinclude de imagem de Azure RemoteApp existente componente Citrix VDA (para obter instruções, consulte a documentação do Citrix Olá). 
7. Aceda toohello Azure Marketplace e iniciar a implementação do Citrix XenApp Essentials.

## <a name="other-considerations"></a>Outras considerações

Tenha em atenção Olá quando migra os seguintes considerações adicionais:
- Citrix XenApp Essentials só suporta implementações híbridas. Por outras palavras, requer controlador de domínio de rede acesso tooa na associação a um domínio tooperform ordem. Se estiver a utilizar uma implementação de nuvem do Azure RemoteApp, utilizar o Azure AD DS ou certifique-se de que a rede virtual tem acesso tooActive diretório para associação a um domínio. 
- toolearn como toomove utilizador dados tooCitrix XenApp Essentials, consulte [como dados toomigrate dentro e fora do Azure RemoteApp](remoteapp-migrate.md). 
- Citrix XenApp Essentials suporta apenas contas do Active Directory. Não suporta contas Microsoft (tais como outlook.com, msn.com ou hotmail.com). 

## <a name="citrix-xenapp-essentials-billing"></a>Faturação Citrix XenApp Essentials

Para obter detalhes completos sobre os preços, consulte Olá [FAQ](https://www.citrix.com/global-partners/microsoft/resources/xenapp-essentials-faq.html#tab-30699) e [artigo de descrição geral do Citrix](https://www.citrix.com/global-partners/microsoft/remote-app.html). Existem três componentes faturação tooCitrix XenApp Essentials:

- encargos de serviço do Olá Citrix, que é $12 por utilizador por mês. Como todas as compras de Azure Marketplace, esta é faturada toohello método de pagamento associado à sua subscrição do Azure. Para clientes do Enterprise Agreement (EA), não não possível utilizar créditos monetários do Azure. 
- Serviços de dados (RDS) cliente licenças de acesso remoto (CALs). Atualmente, pode comprar Olá taxa de acesso remoto que está incluído com Olá pagamento Citrix XenApp Essentials para $6.25. Se for um cliente EA, pode utilizar o Azure créditos monetários toopay para este. Se quiser toouse as CALs de RDS existentes, contacte-nos [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com), para que possa aplicar este tooyour fatura. 
- Armazenamento e computação do Azure. Este é o custo de armazenamento do Azure Olá e consumo de computação para VMs Olá consumido. Tenha em atenção ao selecionar a densidade de utilizador e de tamanho VM de preço. Se for um cliente EA, pode utilizar o Azure créditos monetários toopay para este.

Se ainda tiver questões, pode:
- Enviar-nos por e-mail [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
- [Contacte o suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Comece por [abrir um incidente de suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) toohelp com pré-requisito os passos 1 a 5. Para os passos 6 a 7, contacte o Citrix, abrindo um pedido de suporte no portal de gestão do Citrix Olá. 
