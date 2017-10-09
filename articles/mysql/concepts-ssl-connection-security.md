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
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="1bd4e-103">Conectividade SSL na base de dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="1bd4e-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="1bd4e-104">Base de dados do Azure para MySQL suporta a ligação as aplicações tooclient do servidor de base de dados utilizando Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="1bd4e-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="1bd4e-105">Imposição de ligações de SSL entre o servidor de base de dados e as aplicações de cliente ajuda a proteger contra ataques "man no meio de Olá" ao encriptar o fluxo de dados de Olá entre o servidor de Olá e a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="1bd4e-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="1bd4e-106">As predefinições</span><span class="sxs-lookup"><span data-stu-id="1bd4e-106">Default settings</span></span>
<span data-ttu-id="1bd4e-107">Por predefinição, o serviço de base de dados de Olá deve ser ligações de SSL configurado toorequire ao ligar tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="1bd4e-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="1bd4e-108">Recomenda-se evitar desativar Olá SSL opção sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="1bd4e-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="1bd4e-109">Quando aprovisionar uma nova base de dados do Azure para o servidor de MySQL através de Olá portal do Azure e a CLI, a imposição de ligações de SSL está ativada por predefinição.</span><span class="sxs-lookup"><span data-stu-id="1bd4e-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="1bd4e-110">Da mesma forma, as cadeias de ligação previamente definidas nas definições do "Cadeias de ligação" Olá sob o servidor no portal do Azure de Olá incluem parâmetros de Olá necessário para comuns idiomas tooconnect tooyour servidor base de dados através de SSL.</span><span class="sxs-lookup"><span data-stu-id="1bd4e-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="1bd4e-111">Olá parâmetro SSL varia com base no conector Olá, por exemplo "ssl = true" ou "sslmode = requerem" ou "sslmode = necessária" e outras variações.</span><span class="sxs-lookup"><span data-stu-id="1bd4e-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="1bd4e-112">toolearn como ligação de SSL tooenable ou desative quando desenvolver aplicações, consulte demasiado[como tooconfigure SSL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="1bd4e-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bd4e-113">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1bd4e-113">Next steps</span></span>
[<span data-ttu-id="1bd4e-114">Bibliotecas de ligação para base de dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="1bd4e-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
