---
title: Configurar e os registos do servidor de acesso PostgreSQL no Portal do Azure | Microsoft Docs
description: Este artigo descreve como configurar e aceder os registos do servidor na base de dados do Azure para PostgreSQL do Portal do Azure.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 10/19/2017
ms.openlocfilehash: a2f67b21293a1a0456b27cad9043be01fdd5274a
ms.sourcegitcommit: df4ddc55b42b593f165d56531f591fdb1e689686
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 01/04/2018
---
# <a name="configure-and-access-server-logs-in-the-azure-portal"></a>Configurar e iniciar sessão no servidor de acesso no portal do Azure

Pode configurar, lista e transferir o [base de dados do Azure para os registos do servidor PostgreSQL](concepts-server-logs.md) do portal do Azure.

## <a name="prerequisites"></a>Pré-requisitos
Para seguir este guia de procedimentos, tem de:
- [Base de dados do Azure para o servidor de PostgreSQL](quickstart-create-server-database-portal.md)

## <a name="configure-logging"></a>Configurar o registo
Configure o acesso aos registos de consulta e registos de erros. 

1. Inicie sessão no [portal do Azure](http://portal.azure.com/).

2. Selecione a base de dados do Azure para o servidor de PostgreSQL.

3. Sob o **monitorização** secção na barra lateral, selecione **registos do servidor**. 

   ![Selecione os registos do servidor e selecione 'Clique aqui para ativar...'](./media/howto-configure-server-logs-in-portal/1-select-server-logs-configure.png)

4. Selecione o título **clique aqui para ativar os registos e configurar parâmetros de registo** para ver os parâmetros de servidor.

5. Selecione o **mostrar mais** expander para ver uma lista dos parâmetros disponíveis expandida. 

   Para obter mais informações sobre as definições de parâmetros, consulte a documentação de PostgreSQL no [relatório de erros e registo](https://www.postgresql.org/docs/current/static/runtime-config-logging.html).

   ![Pequena lista de parâmetros de registo. Clique em Mostrar mais para longa](./media/howto-configure-server-logs-in-portal/2-show-more.png)

6. Altere os parâmetros que terá de ajustar. Todas as alterações efetuadas nesta sessão são realçadas na roxa.

   Assim que tiver alterado os parâmetros, pode clicar em **guardar**. Ou pode **rejeitar** as suas alterações. 

   ![Longa lista de parâmetros com as alterações para guardar ou eliminar](./media/howto-configure-server-logs-in-portal/3-save-discard.png)

7. Regressar à lista de registos, clicando a **botão Fechar** (X ícone) no **parâmetros do** página.

## <a name="view-list-and-download-logs"></a>Ver lista e transferir os registos
Depois de inicia o registo, pode ver uma lista de registos disponíveis e transferir ficheiros de registo individuais no painel de registos do servidor. 

1. Abra o portal do Azure.

2. Selecione a base de dados do Azure para o servidor de PostgreSQL.

3. Sob o **monitorização** secção na barra lateral, selecione **registos do servidor**. A página mostra uma lista dos ficheiros de registo, conforme mostrado:

   ![Lista de registos do servidor](./media/howto-configure-server-logs-in-portal/4-server-logs-list.png)

   > [!TIP]
   > A Convenção de nomenclatura do registo é **postgresql-aaaa-mm-dd_hh0000.log**. A data e hora utilizado no nome do ficheiro é a hora quando o registo foi emitido. Roda os ficheiros de registo para a cada uma hora ou 100 MB de tamanho, o que ocorrer primeiro.

4. Se necessário, utilize o **caixa pesquisa** para restringir rapidamente um registo específicos com base na data/hora. A pesquisa está no nome do registo.

   ![Pesquisa de exemplo nos nomes de registo](./media/howto-configure-server-logs-in-portal/5-search.png)

5. Transferir ficheiros de registo individuais utilizando o **transferir** botão (inativo ícone de seta) junto a cada ficheiro de registo na linha da tabela, conforme mostrado:

   ![Clique em transferir ícone](./media/howto-configure-server-logs-in-portal/6-download.png)

## <a name="next-steps"></a>Passos Seguintes
- Consulte [registos do servidor de acesso na CLI](howto-configure-server-logs-using-cli.md) para saber como transferir os registos através de programação.
- Saiba mais sobre [registos do servidor](concepts-server-logs.md) do BD Azure para PostgreSQL. 
- Para obter mais informações sobre as definições de parâmetro e PostgreSQL registo, consulte a documentação de PostgreSQL no [relatório de erros e de registo](https://www.postgresql.org/docs/current/static/runtime-config-logging.html).

