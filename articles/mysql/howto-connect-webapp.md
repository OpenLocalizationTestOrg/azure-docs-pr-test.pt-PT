---
title: aaaConnect tooAzure da App Service do Azure existente da base de dados MySQL | Microsoft Docs
description: "Instruções sobre como tooproperly ligar um tooAzure App Service do Azure existente da base de dados para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>Ligar um tooAzure App Service do Azure existente da base de dados para o servidor de MySQL
Este documento explica como tooconnect um tooyour App Service do Azure existente Azure base de dados para o servidor de MySQL.

## <a name="before-you-begin"></a>Antes de começar
Inicie sessão no toohello [portal do Azure](https://portal.azure.com). Crie uma base de dados do Azure para o servidor de MySQL. Para obter detalhes, consulte demasiado[como toocreate Azure base de dados para o servidor de MySQL do Portal](quickstart-create-mysql-server-database-using-azure-portal.md) ou [como toocreate Azure base de dados para o servidor de MySQL utilizando a CLI](quickstart-create-mysql-server-database-using-azure-cli.md).

Atualmente, existem duas soluções tooenable acesso a partir de uma base de dados do Azure de tooan do App Service do Azure para MySQL. Ambas as soluções envolvem configurar regras de firewall ao nível do servidor.

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>Solução 1 - criar um tooallow de regra de firewall todos os IPs
Base de dados do Azure para MySQL fornece segurança de acesso através de uma firewall tooprotect os dados. Quando ligar a partir de um tooAzure do App Service do Azure da base de dados para o servidor de MySQL, tenha em atenção que Olá saída IPs de serviço de aplicações são dinâmicas natureza. 

disponibilidade de Olá tooensure do seu serviço de aplicações do Azure, recomendamos que utilize tooallow esta solução todos os IPs.

> [!NOTE]
> Microsoft está a trabalhar para um tooavoid solução longo prazo, permitindo todos os IPs para serviços do Azure tooconnect tooAzure da base de dados MySQL.

1. No painel server, MySQL Olá, em definições, clique em **ligação segurança** painel de segurança de ligação de Olá tooopen para Olá base de dados do Azure para MySQL.

   ![Portal do Azure – clique em segurança de ligação](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. Introduza **nome da regra**, **IP inicial**, e **IP final**. Em seguida, clique em **Guardar**.
   - Nome da regra: permitir-All-IPs
   - Iniciar IP: 0.0.0.0
   - IP de fim: 255.255.255.255

   ![Portal do Azure – adicionar todos os IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>Solução 2 - criar uma firewall tooexplicitly de regra permitir IPs de saída
Pode adicionar explicitamente que Olá todos os IPs de saída do seu serviço de aplicações do Azure.

1. No painel de propriedades do serviço de aplicação Olá, ver o **saída endereço de IP**.

   ![Portal do Azure – IPs de saída de vista](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. No painel de segurança de ligação de MySQL Olá, adicione IPs saída um por um.

   ![Portal do Azure – adicionar IPs explícita](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. Lembre-se demasiado**guardar** regras da firewall.

Embora Olá App service do Azure tenta constante de endereços IP tookeep ao longo do tempo, há casos em que os endereços IP de Olá podem ser alterados. Por exemplo, quando Olá aplicação recicla ocorre uma operação de escala, ou quando são adicionadas novas máquinas nos dados regionais Azure centros de capacidade de Olá tooincrease. Quando a alteração de endereços IP de Olá, aplicação Olá foi tempo de inatividade no evento Olá que já não consegue estabelecer ligação toohello MySQL servidor. Considere este potencial problema ao escolher uma das Olá precedente soluções.

## <a name="ssl-configuration"></a>Configuração de SSL
Base de dados do Azure para MySQL tem SSL ativado por predefinição. Se a aplicação não está a utilizar base de dados do SSL tooconnect toohello, em seguida, é necessário toodisable SSL no servidor de MySQL. Para obter detalhes sobre como tooconfigure SSL, consulte [utilizando o SSL com a base de dados do Azure para MySQL](howto-configure-ssl.md).

## <a name="next-steps"></a>Passos seguintes
Para mais informações sobre cadeias de ligação, consulte demasiado[cadeias de ligação](howto-connection-string.md).
