---
title: "Bibliotecas de ligação para base de dados do Azure para PostgreSQL | Microsoft Docs"
description: "Este artigo descreve vários controladores de que os programadores podem utilizar quando a codificação tooconnect de aplicações e a consulta de base de dados do Azure para PostgreSQL e bibliotecas."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 06/15/2017
ms.openlocfilehash: 1f7234499d8abe37f8de9008e3158765b1fb0bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connection-libraries-for-azure-database-for-postgresql"></a>Bibliotecas de ligação para base de dados do Azure para PostgreSQL
Este tópico apresenta uma lista de bibliotecas e controladores para utilização pelos programadores para programação tooconnect de aplicações e a consulta de base de dados do Azure para PostgreSQL.

## <a name="client-interfaces"></a>Interfaces de cliente
A maioria das idioma cliente bibliotecas tooconnect tooPostgreSQL servidor são projetos externos e são distribuídas de forma independente. Estas são suportadas em plataformas Windows, Linux e Mac. Alguns dos controladores de cliente populares Olá estão listadas:

| **Idioma** | **Interface do cliente** | **Informações adicionais** | **Transferência** |
|--------------|----------------------------------------------------------------|-------------------------------------|--------------------------------------------------------------------|
| Python | [psycopg](http://initd.org/psycopg/) | API de BD em conformidade 2.0 | [Transferência](http://initd.org/psycopg/download/) |
| PHP | [PHP pgsql](https://php.net/manual/en/book.pgsql.php) | Extensão de base de dados | [Instalar](https://secure.php.net/manual/en/pgsql.installation.php) |
| Node.js | [Pacote de npm do grupo de proteção](https://www.npmjs.com/package/pg) | Puro JavaScript não bloquear cliente | [Instalar](https://www.npmjs.com/package/pg) |
| Java | [JDBC](http://jdbc.postgresql.org/) | Controlador JDBC de tipo 4 | [Transferência](https://jdbc.postgresql.org/download.html)  |
| Ruby | [Gem de grupo de proteção](https://deveiate.org/code/pg/) | Ruby Interface | [Transferência](https://rubygems.org/downloads/pg-0.20.0.gem) |
| Ir | [Pacote pq](https://godoc.org/github.com/lib/pq) | Controlador de postgres aceda puro | [Instalar](https://github.com/lib/pq/blob/master/README.md) |
| C\#/ .NET | [Npgsql](http://www.npgsql.org/) | Fornecedor de dados do ADO.NET | [Transferência](https://www.microsoft.com/net/) |
| ODBC | [psqlODBC](https://odbc.postgresql.org/) | Controlador ODBC | [Transferência](http://www.postgresql.org/ftp/odbc/versions/) |
| C | [libpq](https://www.postgresql.org/docs/9.6/static/libpq.html) | Interface de linguagem C primária | Incluído |
| C++ | [libpqxx](http://pqxx.org/) | Interface do novo estilo C++ | [Transferência](http://pqxx.org/download/software/) |

## <a name="next-steps"></a>Passos seguintes
Ler estes inícios rápidos sobre tooconnect e consulta Azure base de dados para PostgreSQL utilizando o idioma à escolha:

[Python](./connect-python.md) | [Node.JS](./connect-nodejs.md) | [.NET (c#)](./connect-csharp.md)
