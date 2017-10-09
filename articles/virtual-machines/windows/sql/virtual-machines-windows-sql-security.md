---
title: "aaaSecurity considerações para o SQL Server no Azure | Microsoft Docs"
description: "Este tópico fornece orientações gerais para proteger o SQL Server em execução de uma Máquina Virtual no Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Considerações de Segurança para SQL Server em Máquinas Virtuais do Azure

Este tópico inclui geral diretrizes de segurança que ajudam a estabelecer instâncias de servidor do acesso seguro tooSQL numa máquina virtual do Azure (VM).

Azure está em conformidade com várias normas que podem permitir-toobuild uma solução em conformidade com o SQL Server em execução numa máquina virtual e regulamentos da indústria. Para obter informações sobre a conformidade regulamentar com o Azure, consulte [Centro de fidedignidade do Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Controlar o acesso toohello VM do SQL Server

Ao criar a máquina virtual do SQL Server, considere como toocarefully controlar quem tem máquina toohello de acesso e tooSQL servidor. Em geral, deve fazer seguinte Olá:

- Restringir o acesso tooSQL tooonly Olá as aplicações de servidor e clientes que precisem dele.
- Siga as melhores práticas para gerir contas de utilizador e palavras-passe.

Olá secções a seguir fornece sugestões sobre pensar através destes pontos.

## <a name="secure-connections"></a>Ligações seguras

Quando cria uma máquina virtual do SQL Server com uma imagem de galeria, Olá **conectividade do SQL Server** opção fornecem Olá escolha de **Local (no interior da VM)**, **privada (na Virtual Network)** , ou **público (Internet)**.

![Conectividade do SQL Server](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Para segurança de melhor Olá, escolha a opção mais restritiva do Olá para o seu cenário. Por exemplo, se estiver a executar uma aplicação que acede ao SQL Server no Olá mesma VM, em seguida, **Local** é Olá de opção mais segura. Se estiver a executar uma aplicação do Azure que requer acesso toohello SQL Server, em seguida, **privada** protege comunicação tooSQL Server apenas dentro do Olá especificado [Azure Virtual Network](../../../virtual-network/virtual-networks-overview.md). Se necessitar de **pública** (internest) de acesso de toohello VM do SQL Server, em seguida, marca se toofollow outros de melhores práticas no tooreduce tópico sua área de superfície de ataque.

Olá as opções selecionadas no portal de Olá utilizam regras de segurança de entrada no Olá VMs [grupo de segurança de rede](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) ou negar o tráfego de rede tooyour máquina de virtual. Pode modificar ou criar novas regras NSG entradas porta do SQL Server do tooallow tráfego toohello (a predefinição é 1433). Também pode especificar endereços IP específicos que são permitidos toocommunicate através desta porta.

![Regras do grupo de segurança de rede](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Além disso tooNSG regras de tráfego de rede toorestrict, também pode utilizar Olá Firewall do Windows na máquina virtual de Olá.

Se estiver a utilizar os pontos finais com o modelo de implementação clássica Olá, remova quaisquer pontos finais na máquina virtual de Olá se não utilizá-los. Para obter instruções sobre a utilização de ACLs com pontos finais, consulte [gerir Olá ACL num ponto final](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Não é necessário para as VMs que utilizam Olá Resource Manager.

Por fim, considere ativar ligações encriptadas para a instância de Olá de Olá motor de base de dados do SQL Server na sua máquina virtual do Azure. Configure a instância do SQL Server com um certificado assinado. Para obter mais informações, consulte [ativar ligações encriptadas toohello motor de base de dados](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) e [sintaxe da cadeia de ligação](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Utilizar uma porta não predefinido

Por predefinição, o SQL Server escuta numa porta bem conhecida, 1433. Para maior segurança, configure o SQL Server toolisten numa porta não predefinidos, tais como 1401. Se aprovisionar uma imagem de galeria do SQL Server no Olá portal do Azure, pode especificar esta porta no Olá **definições do SQL Server** painel.

tooconfigure este após o aprovisionamento, tem duas opções:

- Para VMs do Gestor de recursos, pode selecionar **configuração do SQL Server** do painel de descrição geral do Olá VM. Isto oferece uma opção de porta de Olá toochange.

  ![Alterar a porta TCP no portal](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Para VMs clássicas ou para VMs de SQL Server que não tenham sido aprovisionados com o portal de Olá, pode configurar manualmente a porta de Olá ligando-se remotamente toohello VM. Para obter passos de configuração de Olá, consulte [configurar um servidor tooListen numa porta TCP específica](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Se utilizar esta técnica manual, terá também tooadd um Firewall do Windows regra tooallow tráfego de entrada nessa porta de TCP.

> [!IMPORTANT]
> Especificar uma porta não predefinida é uma boa ideia se a porta do SQL Server é aberta toopublic ligações de internet.

Quando o SQL Server está à escuta numa porta não predefinido, tem de especificar a porta de Olá quando se liga. Por exemplo, considere um cenário em que o endereço IP do servidor Olá é 13.55.255.255 e SQL Server está a escutar na porta 1401. tooconnect tooSQL servidor, tem de especificar `13.55.255.255,1401` na cadeia de ligação de Olá.

## <a name="manage-accounts"></a>Gerir contas

Não pretende que os nomes de atacantes tooeasily estimado contas ou palavras-passe. Utilize Olá toohelp sugestões a seguir:

- Criar uma conta de administrador local exclusivo que não tem um nome **administrador**.

- Utilize palavras-passe fortes complexas para todas as suas contas. Para obter mais informações sobre como toocreate uma palavra-passe segura, consulte [criar uma palavra-passe segura](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) artigo.

- Por predefinição, o Azure seleciona a autenticação do Windows durante a configuração de Máquina Virtual do SQL Server. Por conseguinte, Olá **SA** início de sessão está desativado e uma palavra-passe é atribuída pelo programa de configuração. Recomendamos que Olá **SA** início de sessão não deve ser utilizado ou ativado. Se tem de ter um início de sessão do SQL Server, utilize uma das seguintes estratégias de Olá:

  - Criar uma conta SQL com um nome exclusivo que tenha **sysadmin** associação. Para fazer isto no portal de Olá Ativando **autenticação SQL** durante o aprovisionamento.

    > [!TIP] 
    > Se não ativar a autenticação de SQL durante o aprovisionamento, tem de alterar manualmente o modo de autenticação de Olá demasiado**do SQL Server e o modo de autenticação do Windows**. Para obter mais informações, consulte [Alterar modo de autenticação de servidor](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Se tiver de utilizar Olá **SA** início de sessão, ativar início de sessão de Olá após o aprovisionamento e atribuir uma nova palavra-passe segura.

## <a name="follow-on-premises-best-practices"></a>Siga as melhores práticas de no local

Além disso toohello práticas descritas neste tópico, recomendamos que analise e se implementar práticas de segurança Olá tradicional no local onde for aplicável. Para obter mais informações, consulte [considerações de segurança para uma instalação do SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>Passos Seguintes

Se também estiver interessado em melhores práticas em torno de desempenho, consulte o artigo [práticas recomendadas do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Para outros tópicos relacionados com toorunning do SQL Server em VMs do Azure, consulte [SQL Server em Virtual Machines do Azure descrição-geral](virtual-machines-windows-sql-server-iaas-overview.md).

