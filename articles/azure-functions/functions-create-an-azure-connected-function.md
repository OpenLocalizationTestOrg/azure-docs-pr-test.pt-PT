---
title: "aaaCreate uma função que estabelece ligação a serviços tooAzure | Microsoft Docs"
description: "Utilize as funções do Azure toocreate uma aplicação sem servidor que liga tooother Azure serviços."
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 9d1f7d3b236f8d2c1a404c76aee410f6d458fb7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-toocreate-a-function-that-connects-tooother-azure-services"></a>Utilize as funções do Azure toocreate uma função que estabelece ligação tooother Azure serviços

Este tópico mostra como toocreate uma função nas funções do Azure que escuta toomessages no Olá de fila e as cópias de um armazenamento do Azure mensagens toorows uma tabela de armazenamento do Azure. Uma função de temporizador acionada é utilizado tooload mensagens na fila de Olá. Uma segunda função lê a partir da fila de Olá e escreve tabela toohello de mensagens. Fila Olá e tabela de Olá são criados pelas funções do Azure com base nas definições de enlace Olá. 

ações de toomake mais interessantes, uma função é escrita em JavaScript e Olá outro é escrito em c# script. Isto demonstra como uma aplicação de função pode ter funções em várias linguagens. 

Pode ver este cenário demonstrado num [vídeo no Canal 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).

## <a name="create-a-function-that-writes-toohello-queue"></a>Criar uma função que escreve toohello fila

Antes de poder ligar tooa fila de armazenamento, terá de toocreate uma função que carrega a fila de mensagens hello. Esta função de JavaScript utiliza um acionador de temporizador escreve uma fila de toohello mensagens cada 10 segundos. Se ainda não tiver uma conta do Azure, veja Olá [das funções do Azure de tente](https://functions.azure.com/try) experiência, ou [criar a sua conta do Azure gratuita](https://azure.microsoft.com/free/).

1. Aceda toohello portal do Azure e localize a aplicação de função.

2. Clique em **Nova Função** > **TimerTrigger JavaScript**. 

3. Nome de função Olá **FunctionsBindingsDemo1**, introduza um valor de expressão de cron de `0/10 * * * * *` para **agenda**e, em seguida, clique em **criar**.
   
    ![Adicionar uma função acionada por temporizador](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    Criou uma função acionada por temporizador que é executada a cada 10 segundos.

5. No Olá **desenvolver** separador, clique em **registos** e ver a atividade de Olá no registo de Olá. Verá uma entrada de registo escrita a cada 10 segundos.
   
    ![Ver Olá registo tooverify Olá função funciona](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a>Adicionar um enlace de saída da fila de mensagens

1. No Olá **integrar** separador, escolha **nova saída** > **armazenamento de filas do Azure** > **selecione**.

    ![Adicionar uma função de temporizador de acionador](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. Introduza `myQueueItem` para **nome do parâmetro mensagem** e `functions-bindings` para **nome da fila**, selecione um existente **ligação de conta de armazenamento** ou clique em **novo** toocreate um armazenamento de ligação de conta e, em seguida, clique em **guardar**.  

    ![Criar a fila de armazenamento de toohello de enlace de saída de Olá](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. Novamente no Olá **desenvolver** separador, acrescentar Olá função toohello de código a seguir:
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. Localizar Olá *se* instrução cerca de linha 9 da função de Olá e seguinte de Olá de inserção código após essa instrução.
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    Este código cria um **myQueueItem** e define o **tempo** propriedade toohello atual timeStamp. Em seguida, adiciona Olá nova fila item toohello contexto **myQueueItem** enlace.

3. Clique em **Guardar e executar**.

## <a name="view-storage-updates-by-using-storage-explorer"></a>Ver atualizações de armazenamento através do Explorador de Armazenamento
Pode verificar se a função está a funcionar visualizando as mensagens na fila de Olá que criou.  Pode ligar a fila de armazenamento tooyour utilizando Cloud Explorer no Visual Studio. No entanto, o portal de Olá torna conta de armazenamento de tooyour tooconnect fácil utilizando o Explorador de armazenamento do Microsoft Azure.

1. No Olá **integrar** separador, clique numa fila de saída do enlace > **documentação**, em seguida, Mostrar Olá cadeia de ligação para a sua conta de armazenamento e copie o valor de Olá. Utilize esta conta de armazenamento do valor tooconnect tooyour.

    ![Transferir o Explorador de Armazenamento do Azure](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. Se ainda não o fez, transfira e instale o [Explorador de Armazenamento do Microsoft Azure](http://storageexplorer.com). 
 
3. No Explorador de armazenamento, clique em Olá ligar tooAzure ícone de armazenamento, cole a cadeia de ligação de Olá no campo Olá e conclua o Assistente de Olá.

    ![Explorador de Armazenamento adicionar uma ligação](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. Em **Local e anexado**, expanda **contas do Storage** > a conta do storage > **filas** > **enlaces de funções**e certifique-se de que as mensagens são escritas toohello fila.

    ![Vista de mensagens em fila Olá](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    Se a fila de Olá não existe ou está vazia, não há provavelmente um problema com o enlace de função ou o código.

## <a name="create-a-function-that-reads-from-hello-queue"></a>Criar uma função que lê a partir da fila de Olá

Agora que configurou a serem adicionadas toohello fila de mensagens, pode criar outra função que lê a partir da fila de Olá e escritas de paginações hello permanentemente mensagens tooan tabela de armazenamento do Azure.

1. Clique em **Nova Função** > **QueueTrigger CSharp**. 
 
2. Nome de função Olá `FunctionsBindingsDemo2`, introduza **enlaces de funções** no Olá **nome da fila** campo, selecione uma conta de armazenamento existente ou criar um e, em seguida, clique em **criar**.

    ![Adicionar uma função de temporizador de fila de saída](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. (Opcional) Pode verificar que a nova função de Olá funciona através da visualização nova fila de Olá no Explorador de armazenamento como antes. Também pode utilizar o Cloud Explorer no Visual Studio.  

4. (Opcional) Atualizar Olá **enlaces de funções** fila e repare que itens foram removidos da fila de Olá. Olá remoção ocorre porque a função Olá está vinculada toohello **enlaces de funções** como uma entrada da função da acionador e Olá lê fila Olá da fila. 
 
## <a name="add-a-table-output-binding"></a>Adicionar um enlace de saída de tabela

1. Em FunctionsBindingsDemo2, clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabelas do Azure** > **Selecionar**.

    ![Adicionar uma tabela de armazenamento do Azure do enlace tooan](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. Introduza `functionbindings` para **Nome da tabela** e `myTable` para **Nome do parâmetro de tabela**, escolha um **Ligação da conta de armazenamento** ou crie uma nova e, em seguida, clique em **Guardar**.

    ![Configurar o vínculo de tabela de armazenamento Olá](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. No Olá **desenvolver** separador, substitua o código de função existente Olá seguinte Olá:
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add hello item toohello table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    Olá **TableItem** classe representa uma linha na tabela de armazenamento Olá e adicionar Olá item toohello `myTable` coleção de **TableItem** objetos. Tem de definir Olá **PartitionKey** e **RowKey** propriedades toobe tooinsert possível na tabela de Olá.

4. Clique em **Guardar**.  Por fim, pode verificar Olá função funciona através da visualização de tabela Olá no Explorador de armazenamento ou Visual Studio Cloud Explorer.

5. (Opcional) Na sua conta do storage no Explorador de armazenamento, expanda **tabelas** > **functionsbindings** e certifique-se de que as linhas são adicionadas toohello tabela. Pode fazê-lo Olá mesmo no Cloud Explorer no Visual Studio.

    ![Vista de linhas na tabela de Olá](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    Se a tabela de Olá não existe ou está vazia, não há provavelmente um problema com o enlace de função ou o código. 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações sobre as funções do Azure, consulte Olá os seguintes tópicos:

* [Referência para programadores das Funções do Azure](functions-reference.md)  
  Referência para programadores para codificar funções e definir acionadores e enlaces.
* [Testar as Funções do Azure](functions-test-a-function.md)  
  Descreve várias ferramentas e técnicas para testar as suas funções.
* [Como tooscale das funções do Azure](functions-scale.md)  
  Aborda os planos de serviço disponíveis com as funções do Azure, incluindo o plano de alojamento de consumo de Olá e como toochoose Olá plano adequado. 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

