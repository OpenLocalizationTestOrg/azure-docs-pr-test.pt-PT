---
title: "Análise de fluxo: Rodar credenciais de início de sessão de entradas e saídas | Microsoft Docs"
description: "Saiba como tooupdate Olá credenciais para o Stream Analytics entradas e saídas."
keywords: "credenciais de início de sessão"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>Roda credenciais de início de sessão de entradas e saídas nas tarefas do Stream Analytics
## <a name="abstract"></a>Abstrato
O Azure Stream Analytics atualmente não permite substituir Olá as credenciais numa entrada/saída ao hello tarefa está em execução.

Enquanto o Azure Stream Analytics suporta retomar uma tarefa a partir do último saída, queremos processo completo de Olá tooshare para minimizar o desfasamento de Olá entre Olá parar e iniciar a tarefa de Olá e rodar as credenciais de início de sessão Olá.

## <a name="part-1---prepare-hello-new-set-of-credentials"></a>Parte 1 – preparar o novo conjunto de Olá de credenciais:
Esta peça é aplicável toohello entradas/saídas os seguintes:

* Blob Storage
* Event Hubs
* SQL Database
* Armazenamento de Tabelas

Para outras entradas/saídas, prossiga com a parte 2.

### <a name="blob-storagetable-storage"></a>Armazenamento de/tabela de armazenamento de BLOBs
1. Aceda a extensão de armazenamento toohello no portal de gestão do Azure Olá:  
   ![graphic1][graphic1]
2. Localize o armazenamento de Olá utilizado pelo seu trabalho e vá para a mesma:  
   ![graphic2][graphic2]
3. Clique no comando de gerir chaves de acesso de Olá:  
   ![graphic3][graphic3]
4. Entre Olá chave de acesso primária e chave de acesso secundária, de Olá **escolha Olá não utilizada pela sua tarefa**.
5. Voltar a gerar acessos:  
   ![graphic4][graphic4]
6. Copie a chave de Olá gerado recentemente:  
   ![graphic5][graphic5]
7. Continue tooPart 2.

### <a name="event-hubs"></a>Event hubs
1. Aceda a extensão de Service Bus toohello no portal de gestão do Azure Olá:  
   ![graphic6][graphic6]
2. Localize Olá espaço de nomes do barramento de serviço utilizada pelo seu trabalho e vá para a mesma:  
   ![graphic7][graphic7]
3. Se a sua tarefa utilizar uma política de acesso partilhado no Olá espaço de nomes do Service Bus, avance toostep 6  
4. Visite o separador de Event Hubs toohello:  
   ![graphic8][graphic8]
5. Localize Olá utilizado pela sua tarefa de Hub de eventos e vá para a mesma:  
   ![graphic9][graphic9]
6. Aceda toohello separador Configurar:  
   ![graphic10][graphic10]
7. No Olá pendente do nome da política, localize a política de acesso de Olá partilhado utilizada pela sua tarefa:  
   ![graphic11][graphic11]
8. Entre Olá chave primária e chave secundária, de Olá **escolha Olá não utilizada pela sua tarefa**.  
9. Voltar a gerar acessos:  
   ![graphic12][graphic12]
10. Copie a chave de Olá gerado recentemente:  
   ![graphic13][graphic13]
11. Continue tooPart 2.  

### <a name="sql-database"></a>SQL Database
> [!NOTE]
> Nota: precisa tooconnect toohello serviço de base de dados do SQL Server. Vamos tooshow como toodo esta utilizando Olá experiência de gestão no portal de gestão do Azure Olá, mas pode escolher toouse algumas ferramenta do lado do cliente, tais como o SQL Server Management Studio bem.
>
> 

1. Aceda a extensão de bases de dados SQL toohello no portal de gestão do Azure Olá:  
   ![graphic14][graphic14]
2. Localizar Olá base de dados do SQL Server utilizada pela sua tarefa e **clique no servidor de Olá** ligar sobre Olá mesmo linha:  
   ![graphic15][graphic15]
3. Clique no comando de gerir Olá:  
   ![graphic16][graphic16]
4. Tipo de base de dados mestra:  
   ![graphic17][graphic17]
5. Digite o nome de utilizador, palavra-passe e clique em registo em:  
   ![graphic18][graphic18]
6. Clique em nova consulta:  
   ![graphic19][graphic19]
7. Tipo de Olá seguinte consulta substituindo < login_name > com o nome de utilizador e de substituir <enterStrongPasswordHere> com a sua nova palavra-passe:  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. Clique em executar:  
   ![graphic20][graphic20]
9. Voltar atrás toostep 2 e desta vez clique base de dados de Olá:  
   ![graphic21][graphic21]
10. Clique no comando de gerir Olá:  
   ![graphic22][graphic22]
11. Digite o nome de utilizador, palavra-passe e clique em início de sessão:  
   ![graphic23][graphic23]
12. Clique em nova consulta:  
   ![graphic24][graphic24]
13. Escreva Olá seguinte consulta substituindo < user_name > com um nome pelo qual pretende tooidentify este início de sessão no contexto de Olá desta base de dados (pode fornecer Olá mesmo valor que forneceu para < login_name >, por exemplo) e de substituir < login_name > com o o novo nome de utilizador:  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. Clique em executar:  
   ![graphic25][graphic25]
15. Agora deve fornecer o seu novo utilizador com Olá mesmas funções e privilégios tinha o utilizador original.
16. Continue tooPart 2.

## <a name="part-2-stopping-hello-stream-analytics-job"></a>Parte 2: A parar Olá tarefa do Stream Analytics
1. Aceda a extensão de Stream Analytics toohello no portal de gestão do Azure Olá:  
   ![graphic26][graphic26]
2. Localize a tarefa e vá para a mesma:  
   ![graphic27][graphic27]
3. Visite o separador de entradas de toohello ou separador saídas de Olá com base em se estão rodar credenciais Olá numa entrada ou um resultado.  
   ![graphic28][graphic28]
4. Clique em comando de paragem Olá e confirme a tarefa de Olá parou:  
   ![graphic29][graphic29] aguardar Olá tarefa toostop.
5. Localizar Olá entrada/saída pretender toorotate credenciais no e vá para a mesma:  
   ![graphic30][graphic30]
6. Continuar tooPart 3.

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a>Parte 3: Editar Olá as credenciais no Olá tarefa do Stream Analytics
### <a name="blob-storagetable-storage"></a>Armazenamento de/tabela de armazenamento de BLOBs
1. Localizar o campo de chave de conta de armazenamento de Olá e cole a chave recentemente criada para a mesma:  
   ![graphic31][graphic31]
2. Clique em comandos de guardar Olá e confirmar as alterações a guardar:  
   ![graphic32][graphic32]
3. Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de que é passou com êxito.
4. Continuar tooPart 4.

### <a name="event-hubs"></a>Event hubs
1. Localizar o campo de chave de política de Hub de eventos de Olá e cole a chave recentemente criada para a mesma:  
   ![graphic33][graphic33]
2. Clique em comandos de guardar Olá e confirmar as alterações a guardar:  
   ![graphic34][graphic34]
3. Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de que tem passou com êxito.
4. Continuar tooPart 4.

### <a name="power-bi"></a>Power BI
1. Clique em autorização de renovação de Olá:  

   ![graphic35][graphic35]
2. Irá obter Olá confirmação os seguintes:  

   ![graphic36][graphic36]
3. Clique em comandos de guardar Olá e confirmar as alterações a guardar:  
   ![graphic37][graphic37]
4. Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de passou com êxito.
5. Continuar tooPart 4.

### <a name="sql-database"></a>SQL Database
1. Localizar Olá campos de nome de utilizador e palavra-passe e cole-os do conjunto de credenciais criado recentemente:  
   ![graphic38][graphic38]
2. Clique em comandos de guardar Olá e confirmar as alterações a guardar:  
   ![graphic39][graphic39]
3. Um teste de ligação irá iniciar automaticamente quando guardar as alterações, certifique-se de que tem passou com êxito.  
4. Continuar tooPart 4.

## <a name="part-4-starting-your-job-from-last-stopped-time"></a>Parte 4: A iniciar a tarefa de hora da última paragem
1. Saia Olá entrada/saída:  
   ![graphic40][graphic40]
2. Clique no comando de início de Olá:  
   ![graphic41][graphic41]
3. Escolha Olá hora da última paragem e clique em OK:  
   ![graphic42][graphic42]
4. Continuar tooPart 5.  

## <a name="part-5-removing-hello-old-set-of-credentials"></a>Parte 5: Remover Olá antigo conjunto de credenciais
Esta peça é aplicável toohello entradas/saídas os seguintes:

* Blob Storage
* Event Hubs
* SQL Database
* Armazenamento de Tabelas

### <a name="blob-storagetable-storage"></a>Armazenamento de/tabela de armazenamento de BLOBs
Repita parte 1 para Olá chave de acesso que foi utilizado anteriormente pelo seu trabalho toorenew Olá agora não utilizados chave de acesso.

### <a name="event-hubs"></a>Event hubs
Repita parte 1 para Olá chave que foi utilizado anteriormente pelo seu trabalho toorenew Olá chave agora não utilizado.

### <a name="sql-database"></a>SQL Database
1. Volte atrás toohello janela de consulta do tipo no Olá consulta a seguir, substituindo < previous_login_name > com Olá nome de utilizador que foi utilizado anteriormente pelo seu trabalho e parte 1 passo 7:  
   `DROP LOGIN <previous_login_name>`  
2. Clique em executar:  
   ![graphic43][graphic43]  

Pode ser obtido Olá confirmação os seguintes: 

    Command(s) completed successfully.

## <a name="get-help"></a>Obter ajuda
Para mais assistência, tente ler o nosso [fórum do Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Passos seguintes
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Começar a utilizar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Tarefas de escala do Azure Stream Analytics](stream-analytics-scale-jobs.md)
* [Referência do idioma de consulta do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência de API do REST de gestão do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

