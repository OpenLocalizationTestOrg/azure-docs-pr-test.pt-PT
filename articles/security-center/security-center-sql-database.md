---
title: "aaaAzure serviço Centro de segurança e a SQL Database do Azure | Microsoft Docs"
description: "Este artigo mostra como o Centro de segurança pode ajudar a proteger as bases de dados na base de dados do Azure SQL."
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Serviço de centro de segurança do Azure e SQL Database do Azure
[Centro de segurança do Azure](https://azure.microsoft.com/documentation/services/security-center/) ajuda-o a evitar, detetar e responder toothreats. Fornece gestão de políticas e monitorização de segurança integrada nas suas subscrições do Azure, ajuda a detetar ameaças que caso contrário podem passar despercebidas e funciona com um ecossistema abrangente de soluções de segurança.

Este artigo mostra como o Centro de segurança pode ajudar a proteger as bases de dados na base de dados do Azure SQL.

## <a name="why-use-security-center"></a>Porquê utilizar o Centro de Segurança?
Centro de segurança ajuda a salvaguardar os dados na base de dados do SQL Server, fornecendo visibilidade segurança Olá de todos os servidores e bases de dados. Centro de segurança, pode:

* Defina políticas para auditoria e de encriptação de base de dados SQL.
* Monitorizar a segurança de Olá dos recursos de base de dados SQL em todas as subscrições.
* Rapidamente identificar e resolver problemas de segurança.
* Integrar alertas a partir do [deteção de ameaças da SQL Database do Azure](../sql-database/sql-database-threat-detection.md).

Além disso, toohelping proteger os seus recursos de base de dados SQL, o Centro de segurança também fornece monitorização de segurança e gestão de máquinas virtuais do Azure, serviços em nuvem, serviços de aplicações, redes virtuais e muito mais. Saiba mais acerca do Centro de segurança [aqui](security-center-intro.md).

## <a name="prerequisites"></a>Pré-requisitos
tooget começar a utilizar o Centro de segurança, tem de ter um tooMicrosoft de subscrição do Azure. escalão gratuito do Olá do Centro de segurança está ativado com a sua subscrição. Para obter mais informações sobre o Centro de segurança escalões gratuito e Standard, consulte [preços do Centro de segurança](https://azure.microsoft.com/pricing/details/security-center/).

Centro de segurança suporta o acesso baseado em funções. toolearn mais informações sobre o controlo de acesso baseado em funções (RBAC) no Azure, consulte [controlo de acesso baseado em função do Active Directory do Azure](../active-directory/role-based-access-control-configure.md). Olá FAQ do Centro de segurança fornece informações sobre [como permissões são processadas no Centro de segurança](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Aceder ao Centro de Segurança
Aceder ao centro de segurança de Olá [portal do Azure](https://azure.microsoft.com/features/azure-portal/). [Inicie sessão no portal de toohello](https://portal.azure.com/) e selecione Olá **opção Centro de segurança**.

![Opção de centro de segurança][1]

Olá **Centro de segurança** abre o painel.
![Painel Centro de segurança][2]

## <a name="set-security-policy"></a>Definir política de segurança
Uma política de segurança define o conjunto de Olá de controlos que são recomendados para recursos dentro Olá especificado subscrição ou grupo de recursos. No Centro de segurança, é possível definir políticas para as suas subscrições ou grupos de recursos de acordo com as necessidades de segurança tooyour da empresa e do tipo de Olá de aplicações ou sensibilidade dos dados de Olá em cada subscrição.

Pode definir uma política tooshow recomendações para auditoria de SQL e a encriptação transparente de dados do SQL Server (TDE).

* Quando ativar **auditoria de SQL e deteção de ameaças**, o Centro de segurança recomenda que possível ativar a auditoria de acesso tooAzure da base de dados de conformidade, deteção e efeitos de investigação avançadas.
* Quando ativar **encriptação transparente de dados SQL**, o Centro de segurança recomenda que a encriptação Inativos estar ativado para a SQL Database do Azure, cópias de segurança associadas e ficheiros de registo de transações.

tooset uma política de segurança, selecione de Olá **política** mosaico no painel de centro de segurança de Olá. No Olá **política de segurança** painel, subscrição Olá selecione em que pretende que a política de segurança de Olá tooenable. Selecione **política de prevenção** e ative **no** Olá recomendações de segurança que pretende que o toouse nesta subscrição.
![Política de segurança][3]

toolearn mais, consulte [definir políticas de segurança](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Gerir a recomendação de segurança
Centro de segurança analisa periodicamente o estado de segurança de Olá dos seus recursos Azure. Quando o Centro de Segurança identifica potenciais vulnerabilidades de segurança, cria recomendações. recomendações de Olá ajudá-lo através do processo de Olá de configurar os controlos de Olá necessário.

Depois de definir uma política de segurança, o Centro de segurança analisa Olá o estado de segurança dos seus recursos tooidentify potenciais vulnerabilidades. recomendações de Olá são apresentadas num formato de tabela em que cada linha representa uma recomendação específica. Utilize Olá a tabela seguinte como um toohelp de referência que compreende as recomendações de disponíveis Olá para a SQL Database do Azure, e que cada recomendação não se aplicá-lo. Selecionar uma recomendação leva-o artigo tooan que explica como tooimplement Olá recomendação no Centro de segurança.

| Recomendação | Descrição |
| --- | --- |
| [Ativar a auditoria e deteção de ameaças em servidores SQL](security-center-enable-auditing-on-sql-servers.md) |Recomenda-se que ative a auditoria e deteção de ameaças para servidores de base de dados SQL. (Apenas para serviço de base de dados SQL. Não inclui o Microsoft SQL Server em execução em máquinas virtuais.) |
| [Ativar a auditoria e deteção de ameaças nas bases de dados do SQL Server](security-center-enable-auditing-on-sql-databases.md) |Recomenda-se que ative a auditoria e deteção de ameaças para bases de dados de base de dados SQL. (Apenas para serviço de base de dados SQL. Não inclui o Microsoft SQL Server em execução em máquinas virtuais.) |
| [Ativar a Encriptação de Dados Transparente](security-center-enable-transparent-data-encryption.md) |Recomenda-se de que permitem a encriptação de bases de dados do SQL Server. (Apenas serviço base de dados SQL.) |

recomendações de toosee para os seus recursos do Azure, selecione de Olá **recomendações** mosaico no painel de centro de segurança de Olá. No Olá **recomendações** painel, selecione os detalhes de toosee uma recomendação. Neste exemplo, vamos selecione **deteção de ameaças e ativar a auditoria em servidores SQL**.

![Recomendações][4]

Como mostrado abaixo, mostra o Centro de segurança Olá servidores SQL Server onde a auditoria e deteção de ameaças não estão ativadas. Depois de ativar a auditoria, pode configurar as definições de deteção de ameaças e tooreceive de definições de e-mail alertas de segurança. A deteção de ameaças alerta quando Deteta atividades de base de dados anómalas que indicam potenciais segurança ameaças toohello base de dados do. alertas de Olá são apresentados no dashboard do Centro de segurança de Olá.
![Auditoria e deteção de ameaças][5]

Siga os passos Olá [deteção de ameaças de base de dados SQL no portal do Azure de Olá](../sql-database/sql-database-threat-detection-portal.md) tooturn no e configurar a deteção de ameaças e a lista de Olá tooconfigure de e-mails que vão receber alertas de segurança mediante a deteção de atividades anómalas.

toolearn mais informações sobre as recomendações, consulte [gerir recomendações de segurança](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Monitorizar o estado de funcionamento da segurança
Depois de ativar [políticas de segurança](security-center-policies.md) para recursos de uma subscrição, o Centro de segurança irá analisar a segurança de Olá dos seus recursos tooidentify potenciais vulnerabilidades.  Pode ver o estado de segurança de Olá dos seus recursos no Olá **estado de funcionamento de segurança de recursos** mosaico. Ao clicar em **dados** no Olá **estado de funcionamento de segurança de recursos** mosaico, hello **recursos de dados** painel abre-se com recomendações de SQL para problemas tais como a auditoria e transparente encriptação de dados não ativada. Também tem recomendações para o estado de funcionamento geral Olá da base de dados de Olá.
![Estado de funcionamento de segurança de recursos][6]

toolearn mais, consulte [monitorização de estado de funcionamento de segurança](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Gerir e responder a alertas de toosecurity
Centro de segurança automaticamente recolhe, analisa e integra-se os dados de registo de [deteção de ameaças de SQL do Azure](../sql-database/sql-database-threat-detection.md), como, bem como outros recursos do Azure, toodetect de ameaças reais e reduzir os falsos positivos. Uma lista de alertas de segurança prioritários é apresentada no Centro de segurança juntamente com Olá informações necessárias tooquickly investigar o problema de Olá e recomendações sobre como tooremediate um ataque.

toosee alertas, selecione de Olá **alertas de segurança** mosaico no painel de centro de segurança de Olá. No Olá **alertas de segurança** painel, selecione um alerta toolearn mais informações sobre eventos de Olá que acionou o alerta Olá e o que, se aplicável, os passos precisa de tootake tooremediate um ataque. Neste exemplo, vamos selecione **injeção de SQL potenciais**.
![Alertas de segurança][7]

Como é mostrado abaixo, o Centro de segurança fornece detalhes adicionais facultam informações aprofundadas que alerta accionadas Olá, hello recurso, de destino, quando aplicável Olá origem endereço IP e as recomendações sobre como tooremediate.
![Potencial injeção de SQL][8]

toolearn mais, consulte [está a responder e gerir alertas toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Passos seguintes
* [FAQ do Centro de segurança](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá.
* [Guia de operações e planeamento do Centro de segurança](security-center-planning-and-operations-guide.md) - um conjunto de passos e tarefas toooptimize a utilização do Centro de segurança com base nos requisitos de segurança da sua organização e o modelo de gestão de nuvem.
* [Segurança de dados do Centro de segurança](security-center-data-security.md) – Saiba como o Centro de segurança recolhe e processa dados sobre os seus recursos do Azure, incluindo informações de configuração, metadados, registos de eventos, ficheiros de informação de falha e muito mais.
* [Processamento de incidentes de segurança](security-center-incident.md) -Saiba como de segurança de Olá toouse alertas capacidade no Centro de segurança tooassist no processamento de incidentes de segurança.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png
