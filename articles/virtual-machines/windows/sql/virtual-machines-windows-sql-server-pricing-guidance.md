---
title: os custos de aaaManage eficazmente para SQL Server em virtual machines do Azure | Microsoft Docs
description: "Fornece as melhores práticas para escolher Olá direita SQL máquina virtual do modelo de preços."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 6c6a4394e95b5a915ea3e7d5965730000d331036
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a>Preço orientação para as VMs do SQL do Azure

Este tópico fornece orientações de preço para máquinas virtuais do SQL Server no Azure. Existem várias opções que afetam o custo e é importante toopick Olá direita imagem equilibrar os custos com os requisitos empresariais.

## <a name="free-licensed-sql-server-editions"></a>Liberte-edições licenciadas de SQL Server

Se quiser toodevelop, testar, ou criar uma prova de conceito, então, utilizar Olá licenciado livre **edição do SQL Server Developer**. Esta edição tem tudo na edição Enterprise do SQL Server, assim pode utilizá-la toobuild qualquer aplicação que desejar. Tal não é permitido toorun na produção. Uma VM do SQL Server para programadores apenas cobrará um encargo custo de Olá de Olá VM, não para licenciamento do SQL Server.

Se quiser toorun uma carga de trabalho simples em produção (< 4 núcleos, < 1 GB de memória, < 10 GB/base de dados), em seguida, utilize Olá licenciado livre **SQL Server Express edition**. Uma VM do SQL Server Express só será cobram custo de Olá de Olá VM, não licenciamento do SQL Server.

Para estas desenvolvimento/teste ou cargas de trabalho de produção simples, também pode poupar dinheiro ao escolher um tamanho mais pequeno da VM que corresponde a estas cargas de trabalho. Olá DS1v2 poderá ser uma boa opção para estas cargas de trabalho.

toocreate uma VM do SQL Server 2016 do Azure com uma destas imagens, consulte Olá seguintes ligações:

- [SQL Server 2016 para programadores do Azure VM](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [VM Express Azure do SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a>Pagas edições do SQL Server

Se tiver uma carga de trabalho de produção não lightweight, utilize uma das seguintes edições do SQL Server de Olá:

| Edição do SQL Server | Carga de trabalho |
|-----|-----|
| Web | Pequeno web sites |
| Standard | Toomedium pequenas cargas de trabalho |
| Enterprise | Grandes ou fundamentais cargas de trabalho|

Tem duas opções toopay para licenciamento do SQL Server para estas edições: *pague por utilização* ou *traga a sua própria licença*.

### <a name="pay-per-usage"></a>Pagar por utilização

**Licença do SQL Server Olá pagar por utilização** significa que um custo por minuto Olá da execução Olá VM do Azure inclui o custo de Olá de licença do SQL Server Olá. Pode ver Olá preços para Olá diferentes do SQL Server edições (Web, Standard, Enterprise) na Olá [VM do Azure, página de preços](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard). Olá custo é hello igual para todas as versões do SQL Server (too2016 2008 R2). Como com o SQL Server em geral, licenciamento Olá custo de licenciamento por minuto depende do número Olá de núcleos VM.

Pagar Olá do SQL Server de licenciamento por utilização é recomendada para:

- Cargas de trabalho temporárias ou periódicas. Por exemplo, uma aplicação que necessita de um evento de toosupport para alguns meses cada ano, ou análise de negócio em segundas.
- Cargas de trabalho com duração desconhecida ou escala. Por exemplo, uma aplicação que não pode ser necessário em alguns meses ou que pode exigir mais ou menos capacidade de computação, consoante a pedido.

toocreate uma VM do SQL Server 2016 do Azure com uma destas imagens de pagamento por utilização, consulte Olá seguintes ligações:

- [SQL Server 2016 Web do Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [VM do Azure Standard do SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> Quando cria uma máquina virtual do SQL Server no portal do Azure de Olá, Olá estimado custo mensal apresentado no Olá **escolher um tamanho** painel não inclui os custos de licenciamento do SQL Server. Este é o custo de Olá de Olá VM individualmente.
>
> ![Escolha o painel de tamanho VM](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
>Para Olá livre edições licenciadas de rápida e Developer do SQL Server, este é o custo estimado total de Olá. Mas para a Web, Standard e Enterprise, localizar Olá adicionais custos de licenciamento do SQL Server no Olá [página de preços de máquinas virtuais do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/). Na página de preços de Olá, selecione a edição de destino do SQL Server.

### <a name="bring-your-own-license-byol"></a>BYOL (traga a sua própria licença)

**Colocar a sua própria licença do SQL Server através da licença mobilidade**, também referido tooas **BYOL**, significa através de uma licença de Volume de servidor de SQL existente com Software Assurance numa VM do Azure. Uma VM do SQL Server utilizando BYOL apenas cobrará um encargo de custo de Olá de execução Olá VM, não para licenciamento do SQL Server, uma vez que já tenham adquirido licenças e Software Assurance através de um programa de licenciamento em Volume.

Licenciamento através de mobilidade de licenças é recomendado colocar o seus próprios SQL para:

- Cargas de trabalho contínuas. Por exemplo, uma aplicação que necessita de operações de negócio toosupport 24x7.
- Cargas de trabalho com duração conhecida e a escala. Por exemplo, uma aplicação que será necessária para o ano todo Olá e que a pedido tiver sido prevista.

toouse BYOL com uma VM do SQL Server, tem de ter uma licença para o SQL Server Standard ou Enterprise e [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), que é uma opção obrigatório através de alguns [licenciamento em Volume](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programas e opcional comprar com outras pessoas.  Olá níveis fornecidos através de programas de licenciamento em Volume de preço varia com base no tipo de Olá de contrato e Olá quantidade e ou compromisso tooSQL servidor. Mas como uma regra geral, colocar a sua própria licença para cargas de trabalho de produção contínua tem Olá seguintes vantagens:

| Benefício BYOL | Descrição |
|-----|-----|
| **Reduções de custos** | Colocar a sua própria licença do SQL Server é mais económico que pagar por utilização, se uma carga de trabalho será executado continuamente SQL Server Standard ou Enterprise para *mais de 10 meses*. |
| **Poupança de longa duração** | Em média, é *30% mais barata por ano* toobuy ou renovar uma licença do SQL Server para Olá primeiro 3 anos. Além disso, após a 3 anos, não precisa de toorenew Olá licença, pay apenas para o Software Assurance. Nessa altura, é *200% mais barata*. |
| **Réplica secundária de passiva livre** | Outra vantagem de colocar a sua própria licença é Olá [livre de licenciamento para uma réplica secundária passiva](https://azure.microsoft.com/pricing/licensing-faq/) por SQL Server para fins de elevada disponibilidade. Isto cuts no meio Olá licenciamento custo de uma implementação do SQL Server altamente disponível (por exemplo, utilizando grupos de disponibilidade Always). secundário passivo do Olá direitos toorun Olá são fornecidos através de Olá benefício de ativação pós-falha servidores Software Assurance. |

toocreate uma VM do SQL Server 2016 do Azure com uma destas imagens bring-your-proprietário-licenças, consulte o artigo VMs de Olá o prefixo "{BYOL}":

- [SQL Server 2016 Enterprise Azure VM](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [VM do Azure Standard do SQL Server 2016](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> Indique dentro de 10 dias quantas licenças de SQL Server irá utilizar no Azure. Olá imagens anterior do ligações toohello tem instruções sobre como toodo isto.

## <a name="avoid-unecessary-costs"></a>Evitar custos de unecessary

Se estiver a utilizar quaisquer cargas de trabalho que não executem continuamente, considere encerrar a máquina virtual de Olá durante períodos inativa Olá. Só paga o que utilizar.

Por exemplo, se apenas estiver a tentar terminar o SQL Server numa VM do Azure, não seria aconselhável tooincur encargos ao acidentalmente deixá-lo em execução para semanas. Uma solução é toouse Olá [funcionalidade de encerramento automático](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Autoshutdown de VM do SQL Server](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

Encerramento automático faz parte de um conjunto maior de semelhantes funcionalidades fornecidas pelo [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).

Para outros fluxos de trabalho, considere automaticamente encerrar e reiniciar as VMs do Azure com uma solução de script, tais como [da automatização do Azure](https://azure.microsoft.com/services/automation/).

> [!IMPORTANT]
> Encerrar e Desalocação da VM são encargos de tooavoid de forma Olá apenas. Basta parar ou utilizar as opções de energia tooshut baixo Olá VM ainda incorreu custos de utilização.

## <a name="next-steps"></a>Passos seguintes

Para o Azure geral preços orientações, consulte o artigo [evitar custos inesperados com faturação do Azure e custos de gestão](../../../billing/billing-getting-started.md).

Para Olá mais recente máquinas de virtuais preços, incluindo o SQL Server, consulte Olá [VM do Azure, página de preços](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).

Reveja os outros tópicos de Máquina Virtual do SQL Server em [do SQL Server na descrição geral de máquinas virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).
