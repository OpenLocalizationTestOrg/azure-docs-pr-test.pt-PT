---
title: "as políticas de acesso do aaaData informações de séries de tempo do Azure | Microsoft Docs"
description: "Neste tutorial, aprende toomanage políticas de acesso de dados no Insights de séries de tempo"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Conceder acesso tooa Insights de séries de tempo ambiente do dados através do portal do Azure

Os ambientes do Time Series Insights têm dois tipos de políticas de acesso independentes:

* Políticas de acesso de gestão
* Políticas de acesso a dados

Ambas as políticas concedem aos principais (utilizadores e aplicações) do Azure Active Directory várias permissões num determinado ambiente. Olá principais (utilizadores e aplicações) têm de pertencer toohello active directory (ou "Inquilino do Azure") associado à subscrição Olá que contém o ambiente de Olá.

Políticas de gestão de acesso conceder configuração toohello relacionados de permissões de ambiente de Olá, tais como
*   Criação e eliminação do ambiente de Olá, origens de eventos, referenciam conjuntos de dados, e
*   Gestão de políticas de acesso de dados de Olá.

Políticas de acesso de dados conceder permissões tooissue as consultas de dados, manipular dados de referência no ambiente de Olá e partilham consultas guardadas e perspetivas associadas Olá ambiente.

dois tipos de Olá das políticas permitem clara separação entre a gestão de toohello de acesso de ambiente de Olá e aceder a dados toohello Olá ambiente. Por exemplo, é possível toosetup um ambiente que Olá proprietário/criador de ambiente de Olá é removido do acesso a dados Olá. Bem como os utilizadores e serviços que são permitidos dados tooread do ambiente de Olá não pode ser concedido nenhuma configuração de toohello de acesso de ambiente de Olá.

## <a name="grant-data-access"></a>Conceder acesso a dados
Olá passos seguintes mostram como toogrant de acesso aos dados para um principal de utilizador:

1.  Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2.  Clique em "Todos os recursos" no menu de Olá no lado esquerdo do Olá da Olá portal do Azure.
3.  Selecione o seu ambiente do Time Series Insights.

  ![Gerir a origem de informações de séries de tempo de Olá - ambiente](media/data-access/getstarted-grant-data-access1.png)

4.  Selecione "Acesso do Plano de Dados", clique em "Adicionar"

  ![Gerir a origem de informações de séries de tempo de Olá – adicionar](media/data-access/getstarted-grant-data-access2.png)

5.  Clique em "Selecionar utilizador".
6.  Procure e selecione o utilizador por correio eletrónico de Olá.
7.  Clique em “Selecionar”, no painel “Selecionar Utilizador”.

  ![Gerir a origem de informações de séries de tempo de Olá - selecionar utilizador](media/data-access/getstarted-grant-data-access3.png)

8.  Clique em “Selecionar função”.
9.  Se pretender que os dados de referência do tooallow utilizador toochange e partilhar consultas guardadas e perspetivas com outros utilizadores do ambiente de Olá, selecione "Contribuinte". Caso contrário, selecione "Leitor" tooallow utilizador consultar os dados no ambiente de Olá e guarde consultas de (não partilhadas) pessoais no ambiente de Olá.
10. Clique em "Ok" no painel do Olá "Selecionar função".

  ![Gerir a origem de informações de séries de tempo de Olá - selecionar função](media/data-access/getstarted-grant-data-access4.png)

11. Clique em "Ok" no painel do Olá "Selecionar função de utilizador".
12. Deverá ver:

  ![Gerir a origem de informações de séries de tempo de Olá - resultados](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Passos seguintes

* [Criar uma origem de eventos](time-series-insights-add-event-source.md)
* [Enviar eventos](time-series-insights-send-events.md) toohello origem de evento
* Ver o seu ambiente no [Portal do Time Series Insights](https://insights.timeseries.azure.com)
