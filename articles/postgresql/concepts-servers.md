---
title: Conceitos de servidor na base de dados do Azure para PostgreSQL | Microsoft Docs
description: "Este tópico fornece considerações e diretrizes para configurar e gerir a base de dados do Azure para servidores de PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 12/02/2017
ms.openlocfilehash: d7eec2735e48f57500eb2ea822f0949d2ec2e585
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/03/2018
---
# <a name="azure-database-for-postgresql-servers"></a>Base de dados do Azure para servidores de PostgreSQL
Este artigo fornece considerações e diretrizes para trabalhar com a base de dados do Azure para servidores de PostgreSQL.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>O que é uma base de dados do Azure para o servidor de PostgreSQL?
Uma base de dados do Azure para o servidor de PostgreSQL é um ponto de administração central para várias bases de dados. É a construção de servidor PostgreSQL mesma que poderá estar familiarizado no mundo no local. Especificamente, o serviço de PostgreSQL é gerido, fornece garantias de desempenho, expõe funcionalidades ao nível do servidor e de acesso.

Uma base de dados do Azure para o servidor de PostgreSQL:

- É criada dentro de uma subscrição do Azure.
- É o recurso principal para bases de dados.
- Fornece um espaço de nomes para bases de dados.
- É um contentor com semântica de duração strong - eliminar um servidor e elimina as bases de dados contidas.
- Collocates recursos numa região.
- Fornece um ponto final da ligação de acesso de servidor e base de dados (. postgresql.database.azure.com).
- Fornece o âmbito de políticas de gestão que se aplicam às respetivas bases de dados: início de sessão, firewall, os utilizadores, funções, configurações, etc.
- Está disponível em múltiplas versões. Para obter mais informações, consulte [versões da base de dados PostgreSQL](concepts-supported-versions.md).
- É extensível pelos utilizadores. Para obter mais informações, consulte [PostgreSQL extensões](concepts-extensions.md).

Dentro de uma base de dados do Azure para o servidor de PostgreSQL, pode criar uma ou várias bases de dados. Pode optar por criar uma base de dados por servidor para utilizar todos os recursos ou criar várias bases de dados para partilhar os recursos. Os preços é estruturado por cada servidor, com base na configuração de armazenamento (GB), unidades de computação e escalão de preço. Para obter mais informações, consulte [escalões de preço](./concepts-service-tiers.md).

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-postgresql-server"></a>Como ligar e autenticar para uma base de dados do Azure para o servidor de PostgreSQL?
Os seguintes elementos ajudam a garantir o acesso seguro à sua base de dados:

|||
|:--|:--|
| **Autenticação e autorização** | Base de dados do Azure para o servidor de PostgreSQL suporta a autenticação de PostgreSQL nativa. Pode estabelecer ligação e autenticar para o servidor com início de sessão de administrador do servidor. |
| **Protocolo** | O serviço suporta um protocolo baseado em mensagem utilizado pelo PostgreSQL. |
| **TCP/IP** | O protocolo é suportado o TCP/IP e através de sockets de domínio do Unix. |
| **Firewall** | Para ajudar a proteger os seus dados, uma regra de firewall impede a todos os acessos ao seu servidor e respetivas bases de dados, até que especifique os computadores que têm permissão. Consulte [base de dados do Azure para as regras de firewall do servidor de PostgreSQL](concepts-firewall-rules.md). |

## <a name="how-do-i-manage-a-server"></a>Como gerir a um servidor?
Pode gerir a base de dados do Azure para PostgreSQL servidores utilizando o [portal do Azure](https://portal.azure.com) ou [CLI do Azure](/cli/azure/postgres).

## <a name="server-parameters"></a>Parâmetros do servidor
Os parâmetros de servidor PostgreSQL determinam a configuração do servidor. Na base de dados do Azure para PostgreSQL, a lista de parâmetros pode ser visualizada e editá-lo utilizando o portal do Azure ou a CLI do Azure. 

Como um serviço gerido para Postgres, os parâmetros configuráveis na base de dados do Azure para PostgreSQL são um subconjunto dos parâmetros numa instância Postgres local (para obter mais informações sobre parâmetros Postgres, consulte o [PostgreSQL documentação](https://www.postgresql.org/docs/9.6/static/runtime-config.html)). A base de dados do Azure para o servidor de PostgreSQL está ativado com valores predefinidos para cada parâmetro na criação. Reinicie os parâmetros que necessitem de um servidor ou não é possível configurar o acesso de Superutilizador para que as alterações serem aplicadas pelo utilizador.


## <a name="next-steps"></a>Passos Seguintes
- Para obter uma descrição geral do serviço, consulte [base de dados do Azure para descrição geral de PostgreSQL](overview.md).
- Para obter informações sobre recursos específico quotas e limitações com base na sua **camada de serviço**, consulte [escalões de serviço](concepts-service-tiers.md).
- Para obter informações sobre a ligação ao serviço, consulte [bibliotecas de ligação para base de dados do Azure para PostgreSQL](concepts-connection-libraries.md).
- Ver e editar os parâmetros de servidor através de [portal do Azure](howto-configure-server-parameters-using-portal.md) ou [CLI do Azure](howto-configure-server-parameters-using-cli.md).
