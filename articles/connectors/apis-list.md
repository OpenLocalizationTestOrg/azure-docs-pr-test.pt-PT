---
title: aaaConnectors para Azure Logic Apps | Microsoft Docs
description: "Escolha entre todas as toobuild de conectores disponíveis gerida pela Microsoft Olá e criar as logic apps"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Lista de conectores
> [!TIP]
> Olá [lista completa de A-Z](#az) (deste tópico) apresenta uma lista de todos os Olá disponíveis conectores pode utilizar nas suas Logic Apps. [Detalhes do conector](/connectors/) apresenta uma lista de todos os acionadores e ações definidas no swagger Olá e também apresenta uma lista de quaisquer limites para cada conector.

Os conectores fazem parte integral da criação de aplicações lógicas. Utilizar estes conectores, pode realmente expanda no local e na nuvem coisas de diferentes toodo aplicações com dados por si e os dados que já tem. conectores Olá estão disponíveis nos Olá seguintes categorias: 

* **Conectores padrão**: disponíveis e incluídos automaticamente quando utiliza aplicações lógicas. Alguns exemplos incluem Service Bus, Power BI, Oracle Database, OneDrive e muitos outros.

* **Conectores de contas de integração**: disponíveis quando comprar uma conta de integração. Com estes conectores, pode transformar e validar XML, processar mensagens B2B com AS2 / X12 / EDIFACT e codificar e descodificar ficheiros simples. Se trabalha com BizTalk Server, em seguida, estes conectores são que uma boa ajustar tooexpand os fluxos de trabalho do BizTalk do Azure.  

    BizTalk Server também tem um [adaptador Logic Apps](https://msdn.microsoft.com/library/mt787163.aspx) que inclui a receção de uma aplicação lógica e o envio de aplicação de lógica de tooa.

* **Conectores empresariais**: inclui MQ e SAP. Disponível mediante custo adicional. 

[Preços de aplicações lógicas](https://azure.microsoft.com/pricing/details/logic-apps/) e [modelo de preços](../logic-apps/logic-apps-pricing.md) fornecem mais detalhes sobre os custos de Olá. 

## <a name="popular-connectors"></a>Conectores populares
Existem milhares de aplicações e milhões de execuções que utilizam estes conectores para processar dados e informações com êxito. Olá, a tabela seguinte lista Olá mais popular e algumas favoritos com os nossos utilizadores:

| |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][AzureBlobStorageicon]<br/>**Armazenamento de Blobs do<br/>Azure**][AzureBlobStoragedoc] | Se quiser tooautomate todas as tarefas com a sua conta de armazenamento, em seguida, deverá observar este conector. Suporta operações de CRUD (criar, ler, atualizar, eliminar). | [![API Icon][Azure-Functionsicon]<br/>**Funções do Azure**][azure-functionsdoc] | Crie funções que executam fragmentos personalizados de C# ou node.js e utilize-as nas suas aplicações lógicas.  |
| [![API Icon][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Um dos Olá maioria--lhe pedido para os conectores. Tem acionadores e ações toohelp automatizar fluxos de trabalho com clientes potenciais clientes potenciais e muito mais. | [![API Icon][Event-Hubs-icon]<br/>**Hubs de Eventos**][event-hubs-doc] | Consuma e publique eventos num hub do Hub de Eventos. Por exemplo, pode obter o resultado da sua aplicação lógica utilizar Event Hubs e, em seguida, envie o fornecedor de análise em tempo real do Olá saída tooa. |
| [![API Icon][FTPicon]<br/>**FTP**][FTPdoc] | Se o servidor de FTP é acessível a partir do Olá internet, em seguida, pode automatizar fluxos de trabalho toowork com ficheiros e pastas. <br/><br/>SFTP também está disponível com o conector do Olá SFTP. | [![API Icon][HTTPicon]<br/>**HTTP**][httpdoc] | Utilize as logic apps toocommunicate com qualquer ponto final através de HTTP. |
| [![API Icon][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Muitos acionadores e muito mais ações toouse do Office 365 e-mail e a eventos nos seus fluxos de trabalho. <br/><br/>Este conector inclui um *e-mail aprovação* ação tooapprove férias pedidos, despesa relatórios e assim sucessivamente. <br/><br/>Utilizadores do Office 365 também estão disponíveis com o conector de utilizadores do Office 365 Olá.| [![API Icon][HTTP-Requesticon]<br/>**Request / Response**][HTTP-Requestdoc] | Este conector fornece um URL HTTPS. Quando a aplicação de lógica de Olá recebe um URL do pedido toothis, inicia a aplicação de lógica de Olá. |
| [![API Icon][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Facilmente iniciar sessão com a sua tooobjects de acesso do Salesforce conta tooget, tais como clientes potenciais clientes potenciais e muito mais. |  [![API Icon][Service-Busicon]<br/>**Service Bus**][Service-Busdoc] | conector mais popular do Olá nas logic apps, inclui acionadores e ações toodo assíncrona de mensagens e publicar/subscrever com as filas, tópicos e subscrições. |
|  [![API Icon][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Se fizer alguma coisa com o SharePoint e puder beneficiar de automatização, recomendamos ver este conector. Pode ser utilizado com o SharePoint no local e o SharePoint Online. | [![API Icon][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Um dos Olá utilizado mais conectores, pode ligar-se tooan no local do SQL Server e uma base de dados do SQL do Azure. | 
| [![API Icon][Twittericon]<br/>**Twitter**][Twitterdoc] | Inicie sessão facilmente com uma conta do Twitter e inicie um fluxo de trabalho quando for publicado um tweet novo. Em seguida, guarde estas tweets tooa SQL da base de dados ou uma lista do SharePoint. | | | 

## <a name="integration-account-connectors"></a>Conectores de conta de integração 

Olá Enterprise Integration Pack (EIP) inclui conectores que estão bem conhecido toohello Comunidade de BizTalk Server. Se comprar um [conta integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), utilizador também obtém Olá conectores os seguintes: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![API Icon][as2icon]<br/>**AS2</br> descodificar**][as2decode] | [![API Icon][as2icon]<br/>**AS2</br> codificar**][as2encode] | [![API Icon][x12icon]<br/>**EDIFACT</br> descodificar**][EDIFACTdecode] | [![API Icon][x12icon]<br/>**EDIFACT</br> codificar**][EDIFACTencode] |
[![API Icon][flatfileicon]<br/>**Codificação de ficheiro</br>simples**][flatfiledoc] | [![API Icon][flatfiledecodeicon]<br/>**Codificação de ficheiro</br>simples**][flatfiledecodedoc] | [![API Icon][integrationaccounticon]<br/>**Conta de<br/>integração**][integrationaccountdoc] | [![API Icon][xmltransformicon]<br/>**Transform<br/>XML**][xmltransformdoc] |
| [![API Icon][x12icon]<br/>**X12</br> descodificar**][x12decode] | [![API Icon][x12icon]<br/>**X12</br> codificar**][x12encode] | [![API Icon][xmlvalidateicon]<br/>**Validação de<br/>XML**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Conectores empresariais

Ligar tooyour aplicações da empresa nas suas logic apps.

|  |  |
| --- | --- |
|[![API Icon][MQicon]<br/>**MQ**][mqdoc]|[![API Icon][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Lista completa de A a Z

[Detalhes do conector](/connectors/) lista todos os acionadores e ações definidas no swagger Olá e também apresenta uma lista de quaisquer limites para cada conector.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 Appointment Scheduling<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>API Management do Azure<br/>Serviços de Aplicações do Azure<br/>Aplicação do Azure<br/>Automatização do Azure<br/>[Armazenamento de Blobs do Azure][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Funções do Azure][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Filas do Azure<br/>Azure Resource Manager<br/>[Base de Dados SQL do Azure][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Benchmark Email<br/>Pesquisa do Bing<br/>Bitbucket<br/>Bitly<br/>BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>API de Imagem Digitalizada dos Serviços Cognitivos<br/>API Face dos Serviços Cognitivos<br/>LUIS dos Serviços Cognitivos<br/>Análise de Texto dos Serviços Cognitivos<br/>Common Data Service<br/>Content Conversion<br/>Control-Terminate<br/>[APIs Personalizadas/Aplicações Web][api/web-appdoc]<br/><br/><a name="d"></a>Operações de Dados<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Fazer Até<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Hubs de Eventos][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[File System][filesystemdoc]<br/>[Ficheiro Simples][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>Freshservice<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Calendário Google<br/>Contactos do Google<br/>Google Drive<br/>Folhas do Google<br/>Tarefas do Google<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP Webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Conta de Integração<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Médio<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Meteorologia<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Utilizadores do Office 365<br/>Vídeos do Office 365<br/>OneDrive<br/>OneDrive para Empresas<br/>OneNote (Business)<br/>[Oracle Database][oracle-db-doc]<br/>Outlook Customer Manager<br/>Tarefas do Outlook<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Request / Response][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP Application Server][sapconnector]<br/>[SAP Message Server][sapconnector]<br/>[Schedule][recurrencedoc]<br/>Âmbito<br/>SendGrid<br/>Enviar mensagens toobatch<br/>[Service Bus][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[Transform XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Variables<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[XML Validation][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget iniciado com Azure Logic Apps antes de inscrever-se numa conta do Azure, aceda demasiado[tente Logic Apps](https://tryappservice.azure.com/?appservice=logic). Pode criar de imediato uma aplicação lógica de arranque de curta duração. Sem cartões de crédito; sem compromissos.

## <a name="connectors-as-triggers-and-actions"></a>Conectores como acionadores e ações

Os **acionadores** iniciam ou para instâncias da sua aplicação lógica. Alguns conectores disponibilizam acionadores que notificam a sua aplicação quando ocorrem eventos específicos. Por exemplo, o conector de Olá FTP tem Olá `OnUpdatedFile` acionador inicia a sua aplicação lógica, quando um ficheiro é atualizado. 

As Logic apps incluem Olá tipos de acionadores seguintes:  

* *Consultar acionadores*: estes acionadores consultam o serviço toocheck uma frequência especificada para novos dados. 

    Quando estão disponíveis novos dados, é executada uma nova instância da sua aplicação lógica com dados Olá como entrada. 

* *Push acionadores*: estes acionadores estão à escuta de dados num ponto final ou um evento toohappen, em seguida, aciona uma nova instância da sua aplicação lógica.

* *Acionador de periodicidade*: este acionador cria uma instância da sua aplicação lógica com base numa agenda prescrita.

Os conectores também disponibilizam **ações** que pode utilizar no seu fluxo de trabalho. Por exemplo, a sua aplicação lógica pode procurar dados e, depois, pode utilizá-los posteriormente na mesma. Mais especificamente, pode procurar dados de cliente de uma base de dados do SQL Server e, em seguida, utilize este toobuild de dados de cliente do seu fluxo de trabalho. 

> [!TIP]
> A[descrição geral dos conectores](connectors-overview.md) disponibiliza mais detalhes sobre os acionadores e as ações. 


## <a name="message-manipulation-actions"></a>Ações de manipulação de mensagens

As aplicações lógicas incluem ações incorporadas que podem alterar ou manipular os dados do seu payload. Olá incorporada **operações dados** conector inclui Olá seguintes ações: 

| | |
|---|---|
| **Compor** | Criar ou gerar valores ou objetos toouse mais tarde ou, como criar o fluxo de trabalho. Por exemplo, pode criar um objeto JSON com valores de vários passos ou calcular um tooreference constante posteriormente numa aplicação lógica executar. |
| **Criar tabela CSV**<br/>**Criar tabela HTML** | Transforme um conjunto de resultados de matriz numa tabela CSV ou HTML. Por exemplo, adicionar Olá CRM "Registos de lista" ação e adicionar um filtro de registos adicionados hoje. Em seguida, envie os resultados de Olá como uma tabela HTML num e-mail. |
| **Filtrar matriz** (consulta) | Filtre um entradas de toohello do conjunto de resultados que lhe interessarem. Por exemplo, pesquisar todos as tweets com `#Azure`, e, em seguida, Olá "filtro" devolvido tweets tooonly devolve resultados são `Tweeted_by_followers > 50`. |
| **Associar** | Associe uma matriz com um delimitador. Por exemplo, Olá operação detetar expressões de chave devolve uma matriz de expressões de chaves. Pode "associá-las" com `,` ou algo parecido. Assim, em vez `["Some", "Phrase"]`, tem `"Some, Phrase"`. |
| **Analisar JSON** | Analisar a saída e valores de acesso de um objeto JSON no estruturador de Olá. Por exemplo, se a função do Azure devolver um payload JSON, em seguida, pode analisar-as propriedades de JSON tooaccess hello mais tarde no passo outro. ação de Olá também valida que Olá JSON correspondências Olá especificada esquema durante a execução. | 
| **Selecionar** | Selecione determinadas propriedades de uma matriz para processamento adicional. Se "Listar registos" a partir do SQL e forem devolvidas 15 colunas, selecione apenas algumas destas para processamento adicional. o resultado de Olá é uma matriz que contenha apenas propriedades Olá que selecionar. |

## <a name="custom-connectors-and-azure-certification"></a>Conectores personalizados e certificação do Azure 

toocall em APIs que executar código personalizado ou não estão disponíveis como conectores, pode expandir a plataforma de Logic Apps Olá por [criar baseado em REST API Apps como conectores personalizados](../logic-apps/logic-apps-create-api-app.md). 

Se quiser toomake sua personalizado API Apps público e disponível toouse no Azure, em seguida, submeter o seu toohello nominations [programa de certificados do Microsoft Azure](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder a perguntas e ver que outros utilizadores do Azure Logic Apps estão a fazer, aceda toohello [fórum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp melhorar Azure Logic Apps e conectores, votar em ou submeter ideias em Olá [site de comentários do utilizador Logic Apps](http://aka.ms/logicapps-wish).

Falta um tópico do conector ou detalhes que considera importantes? Se Sim, em seguida, ajude-nos através da adição de tópicos existentes tooour ou escrever os seus próprios. A nossa documentação é open source e está alojada no GitHub. Comece no nosso [repositório do GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Passos seguintes
* [Criar a sua primeira aplicação lógica](../logic-apps/logic-apps-create-a-logic-app.md)
* [Criar APIs personalizadas para aplicações lógicas](../logic-apps/logic-apps-create-api-app.md)
* [Monitorizar as aplicações lógicas](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Integrar aplicações lógicas com Aplicações API do Serviço de Aplicações"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Gerir ficheiros no seu contentor de blobs com o conector de armazenamento de blobs do Azure"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Integrar aplicações lógicas com Funções do Azure"
[db2doc]: ./connectors-create-api-db2.md "Ligar tooIBM DB2 na nuvem de Olá ou no local. Atualize uma linha, obtenha uma tabela e muito mais"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Ligar tooDynamics CRM Online, para que possa trabalhar com dados CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Ligar tooAzure Event Hubs. Receba e envie eventos entre aplicações lógicas e os Hubs de Eventos"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Ligar o sistema de ficheiros tooan no local"
[ftpdoc]: ./connectors-create-api-ftp.md "Ligar tooan FTP / FTPS servidor para tarefas FTP, como carregar, obter, eliminar ficheiros e muito mais"
[httpdoc]: ./connectors-native-http.md "Efetuar chamadas HTTP com o conector HTTP Olá"
[http-requestdoc]: ./connectors-native-reqres.md "Adicione as ações de HTTP pedidos e respostas tooyour as logic apps"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Faça chamadas HTTP com o conector HTTP + Swagger."
[informixdoc]: ./connectors-create-api-informix.md "Ligar tooInformix na nuvem de Olá ou no local. Ler uma linha, Listar tabelas de Olá e muito mais"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Integre aplicações lógicas com fluxos de trabalho aninhados"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Ligar a conta de tooyour do Office 365. Envie e receba e-mails, gira o seu calendário e contactos, e muito mais"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Ligar tooan Oracle da base de dados tooadd, inserir, eliminar linhas e muito mais"
[mqdoc]: ./connectors-create-api-mq.md "Ligar tooMQ no local ou do Azure e enviar e receber mensagens"
[recurrencedoc]:  ./connectors-native-recurrence.md "Acione ações periódicas para aplicações lógicas"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Ligue-se a conta do Salesforce tooyour. Gira contas, responsáveis, oportunidades e muito mais"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Ligar o sistema SAP tooan no local"
[service-busdoc]: ./connectors-create-api-servicebus.md "Envie mensagens das Filas e dos Tópicos do Service Bus e receba mensagens das Filas e das Subscrições do Service Bus"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Ligar tooSharePoint Online. Gira documentos, liste itens e muito mais"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Ligar tooSharePoint no servidor no local. Gira documentos, liste itens e muito mais"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Ligar tooAzure base de dados SQL ou SQL server. Crie, atualize, obtenha e elimine entradas numa tabela da Base de Dados SQL."
[twitterdoc]: ./connectors-create-api-twitter.md "Ligar tooTwitter. Obtenha linhas cronológicas, publique tweets e muito mais"
[webhookdoc]: ./connectors-native-webhook.md "Adicionar Webhook ações e acionadores tooyour as logic apps"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Saiba mais sobre a integração empresarial AS2."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Saiba mais sobre a integração empresarial X12."
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre a integração empresarial de ficheiros simples."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre a integração empresarial de ficheiros simples."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Saiba mais sobre a integração empresarial de validação XML."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Saiba mais sobre a integração empresarial de transformações."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Saiba mais sobre a integração empresarial de descodificação AS2."
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Saiba mais sobre a integração empresarial de codificação AS2."
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Saiba mais sobre a integração empresarial de descodificação X12."
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Saiba mais sobre a integração empresarial de codificação X12."
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Saiba mais sobre a integração empresarial de descodificação EDIFACT."
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Saiba mais sobre a integração empresarial de codificação EDIFACT."
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Procure esquemas, mapas, parceiros e mais na sua conta de integração"


[boxDoc]: ./connectors-create-api-box.md "Ligar tooBox. Carregue, obtenha, elimine, liste os seus ficheiros e muito mais"
[delaydoc]: ./connectors-native-delay.md "Efetue ações atrasadas"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Ligar tooDropbox. Carregue, obtenha, elimine, liste os seus ficheiros e muito mais"
[facebookdoc]: ./connectors-create-api-facebook.md "Ligar tooFacebook. Publicar a linha cronológica tooa, obter uma feed de página e muito mais"
[githubdoc]: ./connectors-create-api-github.md "Ligar tooGitHub e controlar problemas"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Ligar tooGoogleDrive para que possa trabalhar com os seus dados"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Liga tooGoogle folhas, pelo que pode pode modificar as suas folhas de"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Estabelece ligação tooGoogle tarefas, para que consiga gerir as suas tarefas"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Estabelece ligação tooGoogle calendário e pode gerir o calendário."
[http-responsedoc]: ./connectors-native-reqres.md "Adicione as ações de HTTP pedidos e respostas tooyour as logic apps"
[instagramdoc]: ./connectors-create-api-instagram.md "Ligar tooInstagram. Acione ou interaja em eventos"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Ligar a tooyour MailChimp conta. Gira e automatize e-mails"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Ligar tooMandrill para a comunicação"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Ligar tooMicrosoft tradutor. Traduza texto, detete idiomas e muito mais" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Obtenha informações de vídeo, listas de vídeos e canais, e URLs de reprodução para vídeos do Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Ligar tooyour Microsoft OneDrive pessoal. Carregue, elimine, liste os ficheiros e muito mais"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Ligar o negócio tooyour Microsoft OneDrive. Carregue, elimine, liste os seus ficheiros e muito mais"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Ligar a caixa de correio do Outlook tooyour. Gira o seu e-mail, calendários, contactos e muito mais"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Ligar tooMicrosoft Project Online. Gira os seus projetos, tarefas, recursos e muito mais"
[querydoc]: ./connectors-native-query.md "Selecionar e filtrar matrizes com a ação de consulta Olá"
[rssdoc]: ./connectors-create-api-rss.md "Publicar e obter itens do feed, acionem operações quando um novo item é publicado tooan RSS feed."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Ligar tooSendGrid. Envie e-mails e gira listas de recipientes"
[sftpdoc]: ./connectors-create-api-sftp.md "Ligar a tooyour SFTP conta. Carregue, obtenha, elimine ficheiros e muito mais"
[slackdoc]: ./connectors-create-api-slack.md "Ligar tooSlack e publique mensagens tooSlack canais"
[smtpdoc]: ./connectors-create-api-smtp.md "Ligar o servidor de SMTP tooa e enviar correio eletrónico com anexos"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Estabelece ligação tooSparkPost para a comunicação"
[trellodoc]: ./connectors-create-api-trello.md "Ligar tooTrello. Gira os seus projetos e organize tudo com qualquer pessoa"
[twiliodoc]: ./connectors-create-api-twilio.md "Ligar tooTwilio. Envie e receba mensagens, obtenha números disponíveis, gira números de telefone de chamadas recebidas, entre outras ações"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Ligar tooWunderlist. Gira tarefas e listas de itens pendentes, mantenha a sua vida em sincronização e muito mais"
[yammerdoc]: ./connectors-create-api-yammer.md "Ligar tooYammer. Publique mensagens, obtenha novas mensagens e muito mais"
[youtubedoc]: ./connectors-create-api-youtube.md "Ligar tooYouTube. Gira os seus vídeos e canais"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
