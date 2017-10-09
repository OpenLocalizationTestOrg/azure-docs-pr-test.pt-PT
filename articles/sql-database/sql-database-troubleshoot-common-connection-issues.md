---
title: "problemas de ligação comuns aaaTroubleshoot tooAzure base de dados SQL"
description: "Passos tooidentify e resolva comuns erros de ligação para a SQL Database do Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a>Resolver problemas de ligação tooAzure base de dados SQL
Quando a ligação de Olá tooAzure base de dados SQL falha, receberá [mensagens de erro](sql-database-develop-error-messages.md). Este artigo é um tópico centralizado que o ajuda a resolver problemas de conectividade da SQL Database do Azure. Introduz [Olá causas comuns](#cause) dos problemas de ligação, recomenda [uma ferramenta de resolução de problemas](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) que ajuda-o problema de Olá de identidade e fornece a resolução de problemas de passos toosolve [ erros transitórios](#troubleshoot-transient-errors) e [persistentes ou não transitório erros](#troubleshoot-persistent-errors). 

Se ocorrerem problemas de ligação de Olá, tente Olá passos descritos neste artigo de resolução de problemas.
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a>Causa
Problemas de ligação podem ser causados por Olá seguinte:

* Falha tooapply melhores práticas e diretrizes de conceção durante o processo de conceção da aplicação Olá.  Consulte [descrição geral do desenvolvimento de base de dados SQL](sql-database-develop-overview.md) tooget foi iniciado.
* Reconfiguração de base de dados SQL do Azure
* Definições de firewall
* Tempo limite de ligação
* Informações de início de sessão incorreto
* Atingido o limite máximo na alguns recursos da SQL Database do Azure

Geralmente, tooAzure de problemas de ligação da base de dados do SQL Server pode ser classificado da seguinte forma:

* [Erros transitórios (curta duração ou intermitentes)](#troubleshoot-transient-errors)
* [Erros persistentes ou não transitório (erros regularmente repetir)](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a>Tente troubleshooter Olá para problemas de conectividade da SQL Database do Azure
Se ocorrer um erro de ligação específico, tente [esta ferramenta](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), que irá ajudá-lo rapidamente identidade e resolver o problema.

## <a name="troubleshoot-transient-errors"></a>Resolver problemas de erros transitórios

Quando uma aplicação liga tooan SQL database do Azure, receber Olá seguir a mensagem de erro:

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> Esta mensagem de erro é normalmente transitória (curta duração).
> 
> 

Este erro ocorre quando hello base de dados do Azure está a ser movido (ou reconfigurado) e a respetiva base de dados do SQL Server de toohello ligação perde a sua aplicação. Eventos de reconfiguração de base de dados do SQL Server ocorrerem devido a um evento planeado (por exemplo, uma atualização de software) ou um evento não planeado (por exemplo, uma falha de processo ou o balanceamento de carga). A maioria dos eventos de reconfiguração são geralmente curta duração e devem ser realizados em menos de 60 segundos, no máximo. No entanto, estes eventos, ocasionalmente, poderá demorar mais toofinish, por exemplo, quando uma transação grande faz com que uma recuperação de longa execução.

### <a name="steps-tooresolve-transient-connectivity-issues"></a>Problemas de conectividade transitório passos tooresolve

1. Verifique Olá [Dashboard de serviço do Microsoft Azure](https://azure.microsoft.com/status) para quaisquer falhas conhecidas que ocorreu durante a hora de Olá durante o qual Olá foram reportados erros pela aplicação Olá.
2. As aplicações que ligam tooa o serviço em nuvem, tais como SQL Database do Azure deve esperar eventos de reconfiguração periódica e implementar repetir lógica toohandle estes erros em vez de analisar como toousers de erros de aplicação. Olá revisão [erros transitórios](sql-database-connectivity-issues.md) secção Olá melhores práticas e diretrizes em de design [descrição geral do desenvolvimento de base de dados SQL](sql-database-develop-overview.md) para obter mais informações e geral Repita estratégias. Em seguida, ver exemplos de código em [bibliotecas de ligação para base de dados SQL e SQL Server](sql-database-libraries.md) para informações específicas.
3. Como uma base de dados se aproxima dos respetivos limites de recursos, pode parecer toobe um problema de conectividade transitório. Consulte [resolução de problemas de desempenho](sql-database-troubleshoot-performance.md).
4. Se continuar a problemas de conetividade ou se hello duração para o qual a aplicação encontrar o erro de Olá excede 60 segundos, ou se visualizar várias ocorrências do erro Olá num determinado dia, ficheiro um pedido de suporte do Azure ao selecionar **obter suporta** no Olá [suporte do Azure](https://azure.microsoft.com/support/options) site.

## <a name="troubleshoot-persistent-errors"></a>Resolver erros persistentes
Se a aplicação Olá forma permanente falhar tooconnect tooAzure base de dados SQL, normalmente indica um problema com uma das seguintes Olá:

* Configuração da firewall. Olá firewall de base de dados ou do lado do cliente de SQL do Azure está a bloquear ligações tooAzure base de dados SQL.
* Rede de reconfiguração do lado do cliente de Olá: por exemplo, um novo endereço IP ou um servidor proxy.
* Erro de utilizador: por exemplo, escrito incorretamente, tais como o nome do servidor Olá na cadeia de ligação de Olá os parâmetros de ligação.

### <a name="steps-tooresolve-persistent-connectivity-issues"></a>Problemas de conectividade persistente de tooresolve passos
1. Configurar [regras de firewall](sql-database-configure-firewall-settings.md) o endereço IP de cliente tooallow Olá. Para fins de teste temporários, configure uma regra de firewall utilizando 0.0.0.0 como Olá a iniciar intervalo de endereços IP e utilizar 255.255.255.255 como Olá termina o intervalo de endereços IP. Esta ação irá abrir endereços IP do Olá servidor tooall. Se este procedimento resolve o problema de conectividade, remover esta regra e criar uma regra de firewall para um endereço IP adequadamente limitado ou intervalo de endereços. 
2. Em todas as firewalls entre o cliente de Olá e Olá Internet, certifique-se de que a porta 1433 está aberta para ligações de saída. Reveja [configurar tooAllow de Firewall do Windows hello acesso ao servidor de SQL](https://msdn.microsoft.com/library/cc646023.aspx) e [híbrida identidade necessários portas e protocolos](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) para apontadores adicionais relacionados com tooadditional portas que precisa de tooopen para Autenticação do Active Directory do Azure.
3. Certifique-se de que a cadeia de ligação e outras definições de ligação. Consulte Olá secção cadeia de ligação Olá [tópico de problemas de conectividade](sql-database-connectivity-issues.md#connections-to-azure-sql-database).
4. Verifique o estado de funcionamento do serviço no dashboard de Olá. Se considerar que não há uma falha regional, consulte [recuperar a partir de uma falha](sql-database-disaster-recovery.md) região de novos passos toorecover tooa.

## <a name="next-steps"></a>Passos seguintes
* [Resolver problemas de desempenho de SQL Database do Azure](sql-database-troubleshoot-performance.md)
* [Pesquisa Olá documentação no Microsoft Azure](http://azure.microsoft.com/search/documentation/)
* [Olá vista mais recentes atualizações de serviço de base de dados do Azure SQL toohello](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a>Recursos adicionais
* [Descrição geral do desenvolvimento de base de dados SQL](sql-database-develop-overview.md)
* [Orientações de processamento de falhas transitórias gerais](../best-practices-retry-general.md)
* [Bibliotecas de ligação para base de dados SQL e SQL Server](sql-database-libraries.md)

