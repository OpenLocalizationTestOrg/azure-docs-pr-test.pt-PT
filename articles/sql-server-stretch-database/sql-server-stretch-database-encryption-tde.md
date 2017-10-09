---
title: "aaaEnable encriptação transparente de dados para a Stretch Database - Azure | Microsoft Docs"
description: "Ativar a encriptação de dados transparente (TDE) para o SQL Server Stretch Database no Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Ativar a encriptação de dados transparente (TDE) para a Stretch Database no Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Encriptação de dados transparente (TDE) ajuda a proteger contra ameaças de Olá de atividade maliciosa através de encriptação em tempo real e a desencriptação da base de dados de Olá, cópias de segurança associadas e os ficheiros de registo de transações Inativos sem necessidade de alterações toohello aplicação.

TDE encripta armazenamento Olá de uma base de dados completo com uma chave de encriptação da base de dados de Olá chamado de chave simétrica. chave de encriptação de base de dados de Olá está protegido por um certificado de servidor incorporada. certificado de servidor incorporada Olá é exclusivo para cada servidor do Azure. Microsoft roda automaticamente estes certificados, pelo menos, todos os 90 dias. Para obter uma descrição geral de TDE, consulte [encriptação de dados transparente (TDE)].

## <a name="enabling-encryption"></a>Ativar a encriptação
tooenable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:

1. Base de dados de Olá aberta no Olá [portal do Azure](https://portal.azure.com)
2. No painel da base de dados de Olá, clique em Olá **definições** botão
3. Selecione Olá **encriptação transparente de dados** opção![][1]
4. Selecione Olá **no** definição e, em seguida, selecione **guardar**
   ![][2]

## <a name="disabling-encryption"></a>A desativação da encriptação
toodisable TDE para uma base de dados do Azure que está a armazenar Olá dados migrados da base de dados do SQL Server com a Stretch ativada Olá os seguintes aspetos:

1. Base de dados de Olá aberta no Olá [portal do Azure](https://portal.azure.com)
2. No painel da base de dados de Olá, clique em Olá **definições** botão
3. Selecione Olá **encriptação transparente de dados** opção
4. Selecione Olá **desativar** definição e, em seguida, selecione **guardar**

<!--Anchors-->
[encriptação de dados transparente (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
