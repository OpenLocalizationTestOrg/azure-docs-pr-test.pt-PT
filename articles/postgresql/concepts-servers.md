---
title: conceitos de aaaServer na base de dados do Azure para PostgreSQL | Microsoft Docs
description: "Este tópico fornece considerações e diretrizes para trabalhar com a base de dados do Azure para servidores de PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a>Base de dados do Azure para servidores de PostgreSQL
Este tópico fornece considerações e diretrizes para trabalhar com a base de dados do Azure para servidores de PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>O que é uma base de dados do Azure para o servidor de PostgreSQL?
Uma base de dados do Azure para o servidor de PostgreSQL é um ponto de administração central para várias bases de dados. É Olá mesma construção de servidor PostgreSQL poderá estar familiarizado no Olá, mundo no local. Especificamente, Olá PostgreSQL serviço é gerida, fornece garantias de desempenho, expõe e funcionalidades ao nível do servidor de acesso.

Uma base de dados do Azure para o servidor de PostgreSQL:

- É criada dentro de uma subscrição do Azure.
- É o recurso de principal de Olá para bases de dados.
- Fornece um espaço de nomes para bases de dados.
- É um contentor com semântica de duração strong - eliminar um servidor e elimina as bases de dados de Olá contido.
- Collocates recursos numa região.
- Fornece um ponto final da ligação de acesso de servidor e base de dados (. postgresql.database.azure.com).
- Fornece o âmbito de Olá para políticas de gestão que se aplicam tooits bases de dados: início de sessão, firewall, os utilizadores, funções, configurações, etc.
- Está disponível em múltiplas versões. Para obter mais informações, consulte [versões de base de dados PostgreSQL suportado](concepts-supported-versions.md).
- É extensível pelos utilizadores. Para obter mais informações, consulte [PostgreSQL extensões](concepts-extensions.md).

Dentro de uma base de dados do Azure para o servidor de PostgreSQL, pode criar uma ou várias bases de dados. Pode optar ativamente por participar toocreate uma base de dados individual por servidor tooutilize todos os recursos de Olá ou criar várias bases de dados tooshare recursos Olá. Olá preços por servidor structured, com base na configuração de Olá do escalão de preço, unidades, de armazenamento (GB) de computação. Para obter mais detalhes, consulte [escalões de preço](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a>Como ligar e autenticar tooan base de dados do Azure para o servidor de PostgreSQL?
Olá elementos seguintes ajudam a garantir a base de dados do acesso seguro tooyour.

|||
| :-- | :-- |
| **Autenticação e autorização** | Base de dados do Azure para o servidor de PostgreSQL suporta a autenticação de PostgreSQL nativa. Pode estabelecer ligação e autenticar tooserver com início de sessão do servidor de Olá administrador. |
| **Protocolo** | o serviço de Olá suporta um protocolo baseado em mensagem utilizado pelo PostgreSQL. |
| **TCP/IP** | protocolo de hello é suportado TCP/IP e através de sockets de domínio do Unix. |
| **Firewall** | toohelp proteger os seus dados, uma regra de firewall impede o servidor de base de dados de tooyour acesso todos os ou tooits bases de dados, até especificar quais os computadores que tem permissão. Consulte [base de dados do Azure para as regras de firewall do servidor de PostgreSQL](concepts-firewall-rules.md). |
|||

## <a name="how-do-i-manage-a-server"></a>Como gerir a um servidor?
Pode gerir a base de dados do Azure para servidores de PostgreSQL utilizando Olá portal do Azure ou Olá [CLI do Azure](/cli/azure/postgres).

## <a name="next-steps"></a>Passos seguintes
- Para obter uma descrição geral do serviço de Olá, consulte [base de dados do Azure para PostgreSQL descrição-geral](overview.md)
- Para obter informações sobre recursos específico quotas e limitações com base na sua **camada de serviço**, consulte [escalões de serviço](concepts-service-tiers.md)
- Para obter informações sobre a ligação de toohello de serviço, consulte [bibliotecas de ligação para base de dados do Azure para PostgreSQL](concepts-connection-libraries.md).
