---
title: "aaaEnable sincronização offline da aplicação móvel de Azure (Android)"
description: "Saiba como toouse Mobile Apps do App Service toocache e sincronização de dados offline na sua aplicação Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a>Permitir sincronização offline para a sua aplicação móvel Android
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Descrição geral
Este tutorial abrange a funcionalidade de sincronização offline Olá de Mobile Apps do Azure para Android. Sincronização offline permite que os utilizadores de fim toointeract com uma aplicação móvel&mdash;visualizar, adicionar ou modificar dados&mdash;, mesmo quando não existe nenhuma ligação de rede. As alterações são armazenadas na base de dados local. Quando o dispositivo de Olá estiver novamente online, estas alterações são sincronizadas com Olá remoto back-end.

Se esta for a primeira experiência com Mobile Apps do Azure, deve concluir primeiro tutorial de Olá [criar uma aplicação Android]. Se não utilizar Olá transferir o projeto de servidor de início rápido, tem de adicionar o projeto de tooyour de pacotes de extensão acesso dados Olá. Para obter mais informações sobre pacotes de extensão de servidor, consulte [trabalhar com o servidor de back-end de .NET Olá SDK de Mobile Apps do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn mais informações sobre a funcionalidade de sincronização offline Olá, consulte o tópico de Olá [sincronização de dados Offline no Mobile Apps do Azure].

## <a name="update-hello-app-toosupport-offline-sync"></a>Atualizar a sincronização offline do Olá aplicação toosupport
Com a sincronização offline, leia tooand escrita de um *tabela sincronização* (utilizando Olá *IMobileServiceSyncTable* interface), que faz parte de um **SQLite** base de dados no seu dispositivo.

alterações toopush e pull entre o dispositivo de Olá e Mobile Services do Azure, utilize um *contexto de sincronização* (*MobileServiceClient.SyncContext*), qual inicializar com base de dados local Olá dados toostore localmente.

1. No `TodoActivity.java`, comente a definição existente do Olá de `mToDoTable` e anule os comentários versão Olá da tabela de sincronização:
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. No Olá `onCreate` método, comente Olá existente inicializar `mToDoTable` e anule os comentários esta definição:
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. No `refreshItemsFromTable` comente a definição de Olá de `results` e anule os comentários esta definição:
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. Comente a definição de Olá de `refreshItemsFromMobileServiceTable`.
5. Anule os comentários definição Olá de `refreshItemsFromMobileServiceTableSyncTable`:
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. Anule os comentários definição Olá de `sync`:
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a>Aplicação de Olá de teste
Nesta secção, testar o comportamento de Olá com Wi-Fi e, em seguida, desative Wi-Fi toocreate um cenário offline.

Ao adicionar itens de dados, são guardados no arquivo local do SQLite Olá, mas o serviço móvel toohello não sincronizado até prima Olá **atualizar** botão. Outras aplicações podem ter diferentes requisitos relativos ao dados precisam de toobe sincronizado, mas para fins de demonstração neste tutorial tem utilizador Olá explicitamente solicitá-la.

Quando prima este botão, inicia uma nova tarefa em segundo plano. Primeiro, este empurra todas as alterações efetuadas toohello arquivo local utilizando o contexto de sincronização, em seguida, obtém todos os alterado dados da tabela local toohello do Azure.

### <a name="offline-testing"></a>Testar offline
1. Dispositivo de Olá local ou simulador no *modo de avião*. Esta ação cria um cenário offline.
2. Adicione alguns *ToDo* itens ou marca alguns itens como concluídos. Sair Olá dispositivo ou simulador (ou Olá forçado a fechar aplicação) e reinicie. Certifique-se de que as alterações foram continuadas num dispositivo Olá porque estes são guardados no arquivo local do SQLite Olá.
3. Ver conteúdo Olá Olá Azure *TodoItem* tabela com uma ferramenta SQL, tais como *SQL Server Management Studio*, ou um cliente REST, tais como *Fiddler* ou  *Postman*. Certifique-se de que novos itens de Olá têm *não* foi sincronizado toohello servidor
   
       + Para um back-end Node.js, visite toohello [portal do Azure](https://portal.azure.com/), e na sua aplicação móvel de back-end clique **tabelas fácil** > **TodoItem** tooview conteúdo Olá Olá `TodoItem` tabela.
       + Para um back-end do .NET, tabela de Olá vista contents com uma ferramenta SQL, tais como *SQL Server Management Studio*, ou um cliente REST, tais como *Fiddler* ou *Postman*.
4. Ative Wi-Fi no dispositivo de Olá ou simulador. Em seguida, prima Olá **atualizar** botão.
5. Ver dados de TodoItem Olá novamente Olá portal do Azure. Olá que todoitems novas e alteradas deverá agora aparecer.

## <a name="additional-resources"></a>Recursos Adicionais
* [sincronização de dados Offline no Mobile Apps do Azure]
* [Nuvem abrangem: Sincronização Offline nos Mobile Services do Azure] \(Nota: Olá vídeo está nos Mobile Services, mas a sincronização offline funciona de forma semelhante em Mobile Apps do Azure\)

<!-- URLs. -->

[sincronização de dados Offline no Mobile Apps do Azure]: app-service-mobile-offline-data-sync.md

[criar uma aplicação Android]: app-service-mobile-android-get-started.md

[Nuvem abrangem: Sincronização Offline nos Mobile Services do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

