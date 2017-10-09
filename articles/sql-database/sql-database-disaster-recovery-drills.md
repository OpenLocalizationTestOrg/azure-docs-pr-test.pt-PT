---
title: "aaaSQL simulações de recuperação de desastre de base de dados | Microsoft Docs"
description: "Saiba orientações e melhores práticas para utilizar a SQL Database do Azure tooperform desastre recuperação aprofunda toohelp a mantê o missão aplicações de negócio crítico toofailures resiliente e falhas."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Efetuar exercício de recuperação de desastre
Recomenda-se que a validação da preparação da aplicação para o fluxo de trabalho de recuperação é efetuada periodicamente. Comportamento da aplicação Olá verificar e implicações de interrupção de perda de e/ou Olá dados envolve a que a ativação pós-falha é uma boa prática de engenharia. Também é um requisito pela maioria das normas da indústria como parte da certificação de continuidade do negócio.

Efetuar um exercício de recuperação de desastre é composta por:

* Falha de camada de dados simulando
* Recuperar
* Validar a recuperação de post de integridade de aplicações

Dependendo de como pode [concebido a aplicação para a continuidade do negócio](sql-database-business-continuity.md), desagregação de Olá Olá fluxo de trabalho tooexecute pode variar. Abaixo, iremos descrevem as melhores práticas de Olá realizar um exercício de recuperação após desastre no contexto de Olá da SQL Database do Azure.

## <a name="geo-restore"></a>Georrestauro
tooprevent Olá potencial perda de dados quando realizar um exercício de recuperação após desastre, recomendamos desagregação Olá utilizando um ambiente de teste ao criar uma cópia do ambiente de produção Olá e utilizá-lo a executar o fluxo de trabalho da aplicação Olá tooverify ativação pós-falha.

#### <a name="outage-simulation"></a>Simulação de falha
toosimulate Olá falha, pode eliminar ou mudar o nome da base de dados de origem de Olá. Isto faz com que as falhas de conectividade de aplicação.

#### <a name="recovery"></a>Recuperação
* Efetuar georrestauro Olá da base de dados de Olá para um servidor diferente, tal como descrito [aqui](sql-database-disaster-recovery.md).
* Alteração Olá aplicação configuração tooconnect toohello recuperado da base de dados e siga Olá [configurar uma base de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de Olá toocomplete.

#### <a name="validation"></a>Validação
* Exercício Olá concluída, verificando recuperação post Olá aplicação integridade (incluindo cadeias de ligação, inícios de sessão, testar a funcionalidade básica ou outro parte validações dos procedimentos de signoffs padrão de aplicação).

## <a name="geo-replication"></a>Georreplicação
Para uma base de dados que está protegida com desagregação de Olá georreplicação exercício envolve a base de dados secundária do toohello de ativação pós-falha planeada. Olá ativação pós-falha planeada garante que Olá primário e as bases de dados secundária Olá permanecerem sincronizadas quando funções Olá são mudadas. Ao contrário Olá ativação pós-falha não planeada, esta operação resulta numa perda de dados, modo de desagregação Olá pode ser executada no ambiente de produção Olá.

#### <a name="outage-simulation"></a>Simulação de falha
Falha de Olá toosimulate, pode desativar aplicação web de Olá ou toohello base de dados de dados da máquina virtual ligada. Isto resulta em falhas de conectividade Olá para clientes de web de Olá.

#### <a name="recovery"></a>Recuperação
* Certifique-se de configuração da aplicação Olá no Olá DR região pontos toohello anterior secundário que fica Olá acessível completamente nova principal.
* Efetuar [a ativação pós-falha planeada](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake Olá secundário base de dados de um novo site primário
* Siga Olá [configurar uma base de dados após a recuperação](sql-database-disaster-recovery.md) guia de recuperação de Olá toocomplete.

#### <a name="validation"></a>Validação
* Exercício Olá concluída, verificando recuperação post Olá aplicação integridade (incluindo cadeias de ligação, inícios de sessão, testar a funcionalidade básica ou outro parte validações dos procedimentos de signoffs padrão de aplicação).

## <a name="next-steps"></a>Passos seguintes
* toolearn sobre cenários de continuidade do negócio, consulte [cenários de continuidade](sql-database-business-continuity.md)
* toolearn sobre cópias de segurança automatizada de SQL Database do Azure, consulte [cópias de segurança automatizadas de base de dados SQL](sql-database-automated-backups.md)
* toolearn sobre a utilização de cópias de segurança automatizadas para recuperação, consulte [restaurar uma base de dados de cópias de segurança do Olá iniciou o serviço](sql-database-recovery-using-backups.md)
* toolearn sobre as opções de recuperação mais rápidas, consulte [georreplicação ativa](sql-database-geo-replication-overview.md)  
