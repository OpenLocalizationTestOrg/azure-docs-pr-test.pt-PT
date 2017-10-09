---
title: "os clientes de nível inferior do armazém de dados aaaSQL suportem para auditoria de dados | Microsoft Docs"
description: "Saiba mais sobre o suporte de clientes de nível inferior do armazém de dados do SQL Server para auditoria de dados"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>Suportem de clientes de nível inferior do armazém de dados do SQL Server - para máscara de dados de auditoria e dinâmicos
[Auditoria](sql-data-warehouse-auditing-overview.md) funciona com os clientes de SQL que suportam redirecionamento de TDS.

Qualquer cliente que implementa TDS 7.4 também deve suportar redirecionamento. Exceções toothis incluem JDBC 4.0 no qual o recurso redirecionamento Olá não é totalmente suportado e Tedious do Node.JS em que o redirecionamento não foi implementado.

"Em clientes de", ou seja, que suportam TDS versão 7.3 e abaixo - Olá FQDN do servidor na cadeia de ligação de Olá deverá ser modificado:

Original FQDN do servidor na cadeia de ligação de Olá: <*nome do servidor*>. database.windows.net

Modificação FQDN do servidor na cadeia de ligação de Olá: <*nome do servidor*> .database. **segura**. windows.net

Uma lista parcial de "Clientes de nível inferior" inclui:

* O .NET 4.0 e abaixo
* ODBC 10.0 e abaixo.
* JDBC (enquanto JDBC suporta TDS 7.4, Olá funcionalidade de redirecionamento do TDS não é totalmente suportada)
* Tedious (para Node.JS)

**Remark:** Olá acima modificação do FDQN de servidor pode ser úteis para além disso, para aplicar uma política de auditoria de nível de servidor de SQL, sem necessidade de uma configuração passo em cada base de dados (mitigação temporária).     

