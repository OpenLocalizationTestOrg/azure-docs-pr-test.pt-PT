---
title: "conector de base de dados Oracle Olá aaaAdd nas suas Logic Apps do Azure | Microsoft Docs"
description: "Utilizar o conector de base de dados Oracle Olá numa aplicação lógica"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a>Começar a utilizar o conector de base de dados Oracle Olá

Utilizar o conector de base de dados Oracle Olá, criar organizacionais fluxos de trabalho que utilizam dados na base de dados existente. Este conector pode ligar tooan base de dados no local Oracle ou uma máquina virtual do Azure com a base de dados Oracle instalado. Com este conector, pode:

* Crie o fluxo de trabalho ao adicionar uma base de dados de clientes de tooa de cliente novo ou atualizar uma ordem numa base de dados ordens.
* Utilize ações tooget uma linha de dados, insira uma nova linha e mesmo eliminar. Por exemplo, quando é criado um registo no Dynamics CRM Online (um acionador), em seguida, inserir uma linha numa base de dados Oracle (uma ação). 

Este tópico mostra como toouse Olá conector de base de dados Oracle numa aplicação lógica.

## <a name="prerequisites"></a>Pré-requisitos

* Versões suportadas do Oracle: 
    * Oracle 9 e posterior
    * Software de cliente Oracle 8.1.7 e posterior

* Instale o gateway de dados do Olá no local. [Ligar dados tooon local a partir das logic apps](../logic-apps/logic-apps-gateway-connection.md) listas Olá passos. gateway de Olá é necessário tooconnect tooan base de dados no local Oracle ou VM do Azure com o Oracle DB instalado. 

    > [!NOTE]
    > gateway de dados no local Olá atua como uma ponte e fornece uma transferência de dados seguros entre os dados no local (dados que não se encontra numa nuvem Olá) e as logic apps. Olá mesmo gateway pode ser utilizado com vários serviços e várias origens de dados. Por isso, poderá apenas terá de gateway de Olá tooinstall uma vez.

* Instale Olá cliente Oracle no computador de olá onde instalou o gateway de dados do Olá no local. Não se esqueça de tooinstall hello 64-bit Oracle Data Provider para .NET do Oracle:  

  [64-bit ODAC 12c versão 4 (12.1.0.2.4) para Windows x64](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > Se não estiver instalado o cliente de Oracle Olá, ocorre um erro ao tentar toocreate ou utilizar Olá ligação. Consulte os erros comuns de Olá neste tópico.


## <a name="add-hello-connector"></a>Adicione o conector de Olá

> [!IMPORTANT]
> Este conector não ter acionadores. Tem apenas ações. Por isso, ao criar a sua aplicação lógica, adicionar outro toostart de Acionador a aplicação lógica, tais como **agenda - periodicidade**, ou **pedido / resposta - resposta**. 

1. No Olá [portal do Azure](https://portal.azure.com), criar uma aplicação lógica em branco.

2. Início Olá da sua aplicação lógica, selecione Olá **pedido / resposta - pedido** acionador: 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. Selecione **Guardar**. Quando guardar, o URL do pedido é gerado automaticamente. 

4. Selecione **novo passo**e selecione **adicionar uma ação**. Escreva `oracle` toosee Olá ações disponíveis: 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > Este é também toosee de forma mais rápida Olá Olá acionadores e ações disponíveis para os conectores. Escreva a parte do nome de conector Olá, tal como `oracle`. designer de Olá apresenta uma lista de acionadores e ações. 

5. Selecione uma das ações de Olá, tais como **base de dados Oracle - Get linha**. Selecione **ligar através do gateway de dados no local**. Introduza o nome de servidor Oracle Olá, método de autenticação, nome de utilizador, palavra-passe e selecione Olá gateway:

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. Assim que estiver ligado, selecione uma tabela na lista de Olá e introduza a tabela de tooyour Olá linha ID. Terá de tabela de toohello tooknow Olá identificador. Se não souber, contacte o administrador de Oracle DB e obter um resultado de Olá `select * from yourTableName`. Este oferece Olá terá tooproceed de informações de identificação.

    No seguinte exemplo de Olá, os dados da tarefa estão a ser devolvidos de uma base de dados de recursos humanos: 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. Neste passo seguinte, pode utilizar qualquer um dos Olá toobuild outros conectores o fluxo de trabalho. Se pretender tootest dados ao obter do Oracle, em seguida, enviar uma mensagem de e-mail por si com Olá Oracle dados, utilizando um dos Olá envie correio eletrónico conectores, do Office 365 ou Gmail. Utilize Olá tokens dinâmico de Olá do Olá Oracle tabela toobuild `Subject` e `Body` do seu correio eletrónico:

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. **Guardar** sua aplicação lógica e, em seguida, selecione **executar**. Fechar o designer de Olá e observe o histórico de execuções de Olá para o estado de Olá. Se falhar, selecione a linha de mensagem de falha de Olá. designer de Olá abre e mostra que o passo houve e também mostra Olá informações de erro. Se tiver êxito, deverá receber um e-mail com as informações de Olá adicionou.


### <a name="workflow-ideas"></a>Ideias de fluxo de trabalho

* Pretende toomonitor Olá #oracle hashtag e colocar Olá tweets numa base de dados para que possa ser consultadas e utilizados dentro de outras aplicações. Numa aplicação lógica, adicionar Olá `Twitter - When a new tweet is posted` acionar e introduza Olá **#oracle** hashtag. Em seguida, adicionar Olá `Oracle Database - Insert row` ação e selecione a tabela:

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* São enviadas mensagens de fila do Service Bus tooa. Pretende tooget estas mensagens e colocá-los numa base de dados. Numa aplicação lógica, adicionar Olá `Service Bus - when a message is received in a queue` acionador e selecione Olá fila. Em seguida, adicionar Olá `Oracle Database - Insert row` ação e selecione a tabela:

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a>Erros comuns

#### <a name="error-cannot-reach-hello-gateway"></a>**Erro**: não é possível alcançar Olá Gateway

**Causa**: gateway de dados no local Olá não é possível tooconnect toohello nuvem. 

**Mitigação**: Certifique-se de que o gateway está em execução na máquina no local de olá onde a instalou e que as TI podem ser ligados toohello internet.  Recomendamos que não instale o gateway de Olá num computador que pode ser desativada ou em suspensão. Também pode reiniciar o serviço de gateway de dados do Olá no local (PBIEgwService).

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a>**Erro**: Olá o fornecedor utilizado foi preterido: ' System.Data.OracleClient requer Oracle versão do software de cliente 8.1.7 ou superior.'. Visite [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) fornecedor oficial do tooinstall Olá.

**Causa**: cliente Oracle de Olá SDK não está instalado na máquina de olá onde hello no local o gateway de dados está em execução.  

**Resolução**: transferir e instalar o SDK do cliente de Oracle Olá Olá mesmo computador como gateway de dados do Olá no local.

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a>**Erro**: tabela '[Tablename]' não define quaisquer colunas de chaves

**Causa**: Olá tabela não tem nenhuma chave primária.  

**Resolução**: conector de base de dados Oracle Olá necessita que uma tabela com uma coluna de chave primária utilizada.

#### <a name="currently-not-supported"></a>Atualmente não suportado

* As vistas e procedimentos armazenados 
* Nenhuma tabela com as chaves compostas
* Tipos de objeto aninhado nas tabelas
 
## <a name="connector-specific-details"></a>Detalhes específicos do conector

Ver todos os acionadores e ações definidas no swagger Olá e consulte também os limites de Olá [detalhes do conector](/connectors/oracle/). 

## <a name="get-some-help"></a>Obter ajuda

Olá [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) é ótimo colocar perguntas tooask, responda às perguntas e ver que outros utilizadores Logic Apps estão a fazer. 

Pode ajudar a melhorar as Logic Apps e conectores ao voto e submeter as suas ideias em [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish). 


## <a name="next-steps"></a>Passos seguintes
[Criar uma aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md)e explore os conectores disponíveis de Olá em Logic Apps no nosso [lista APIs](apis-list.md).
