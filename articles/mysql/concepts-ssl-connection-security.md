---
title: aaaSSL conectividade da base de dados do Azure para MySQL | Microsoft Docs
description: "Informações para configurar a base de dados do Azure para o MySQL e aplicações associadas tooproperly utilizar ligações SSL"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>Conectividade SSL na base de dados do Azure para MySQL
Base de dados do Azure para MySQL suporta a ligação as aplicações tooclient do servidor de base de dados utilizando Secure Sockets Layer (SSL). Imposição de ligações de SSL entre o servidor de base de dados e as aplicações de cliente ajuda a proteger contra ataques "man no meio de Olá" ao encriptar o fluxo de dados de Olá entre o servidor de Olá e a sua aplicação.

## <a name="default-settings"></a>As predefinições
Por predefinição, o serviço de base de dados de Olá deve ser ligações de SSL configurado toorequire ao ligar tooMySQL.  Recomenda-se evitar desativar Olá SSL opção sempre que possível. 

Quando aprovisionar uma nova base de dados do Azure para o servidor de MySQL através de Olá portal do Azure e a CLI, a imposição de ligações de SSL está ativada por predefinição. 

Da mesma forma, as cadeias de ligação previamente definidas nas definições do "Cadeias de ligação" Olá sob o servidor no portal do Azure de Olá incluem parâmetros de Olá necessário para comuns idiomas tooconnect tooyour servidor base de dados através de SSL. Olá parâmetro SSL varia com base no conector Olá, por exemplo "ssl = true" ou "sslmode = requerem" ou "sslmode = necessária" e outras variações.

toolearn como ligação de SSL tooenable ou desative quando desenvolver aplicações, consulte demasiado[como tooconfigure SSL](howto-configure-ssl.md).

## <a name="next-steps"></a>Passos seguintes
[Bibliotecas de ligação para base de dados do Azure para MySQL](concepts-connection-libraries.md)
