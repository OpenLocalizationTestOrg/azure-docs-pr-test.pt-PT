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
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="3f727-103">Permitir sincronização offline para a sua aplicação móvel Android</span><span class="sxs-lookup"><span data-stu-id="3f727-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="3f727-104">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="3f727-104">Overview</span></span>
<span data-ttu-id="3f727-105">Este tutorial abrange a funcionalidade de sincronização offline Olá de Mobile Apps do Azure para Android.</span><span class="sxs-lookup"><span data-stu-id="3f727-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="3f727-106">Sincronização offline permite que os utilizadores de fim toointeract com uma aplicação móvel&mdash;visualizar, adicionar ou modificar dados&mdash;, mesmo quando não existe nenhuma ligação de rede.</span><span class="sxs-lookup"><span data-stu-id="3f727-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="3f727-107">As alterações são armazenadas na base de dados local.</span><span class="sxs-lookup"><span data-stu-id="3f727-107">Changes are stored in a local database.</span></span> <span data-ttu-id="3f727-108">Quando o dispositivo de Olá estiver novamente online, estas alterações são sincronizadas com Olá remoto back-end.</span><span class="sxs-lookup"><span data-stu-id="3f727-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="3f727-109">Se esta for a primeira experiência com Mobile Apps do Azure, deve concluir primeiro tutorial de Olá [criar uma aplicação Android].</span><span class="sxs-lookup"><span data-stu-id="3f727-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="3f727-110">Se não utilizar Olá transferir o projeto de servidor de início rápido, tem de adicionar o projeto de tooyour de pacotes de extensão acesso dados Olá.</span><span class="sxs-lookup"><span data-stu-id="3f727-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="3f727-111">Para obter mais informações sobre pacotes de extensão de servidor, consulte [trabalhar com o servidor de back-end de .NET Olá SDK de Mobile Apps do Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="3f727-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="3f727-112">toolearn mais informações sobre a funcionalidade de sincronização offline Olá, consulte o tópico de Olá [sincronização de dados Offline no Mobile Apps do Azure].</span><span class="sxs-lookup"><span data-stu-id="3f727-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="3f727-113">Atualizar a sincronização offline do Olá aplicação toosupport</span><span class="sxs-lookup"><span data-stu-id="3f727-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="3f727-114">Com a sincronização offline, leia tooand escrita de um *tabela sincronização* (utilizando Olá *IMobileServiceSyncTable* interface), que faz parte de um **SQLite** base de dados no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3f727-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="3f727-115">alterações toopush e pull entre o dispositivo de Olá e Mobile Services do Azure, utilize um *contexto de sincronização* (*MobileServiceClient.SyncContext*), qual inicializar com base de dados local Olá dados toostore localmente.</span><span class="sxs-lookup"><span data-stu-id="3f727-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="3f727-116">No `TodoActivity.java`, comente a definição existente do Olá de `mToDoTable` e anule os comentários versão Olá da tabela de sincronização:</span><span class="sxs-lookup"><span data-stu-id="3f727-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="3f727-117">No Olá `onCreate` método, comente Olá existente inicializar `mToDoTable` e anule os comentários esta definição:</span><span class="sxs-lookup"><span data-stu-id="3f727-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="3f727-118">No `refreshItemsFromTable` comente a definição de Olá de `results` e anule os comentários esta definição:</span><span class="sxs-lookup"><span data-stu-id="3f727-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="3f727-119">Comente a definição de Olá de `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="3f727-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="3f727-120">Anule os comentários definição Olá de `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="3f727-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="3f727-121">Anule os comentários definição Olá de `sync`:</span><span class="sxs-lookup"><span data-stu-id="3f727-121">Uncomment hello definition of `sync`:</span></span>
   
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

## <a name="test-hello-app"></a><span data-ttu-id="3f727-122">Aplicação de Olá de teste</span><span class="sxs-lookup"><span data-stu-id="3f727-122">Test hello app</span></span>
<span data-ttu-id="3f727-123">Nesta secção, testar o comportamento de Olá com Wi-Fi e, em seguida, desative Wi-Fi toocreate um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="3f727-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="3f727-124">Ao adicionar itens de dados, são guardados no arquivo local do SQLite Olá, mas o serviço móvel toohello não sincronizado até prima Olá **atualizar** botão.</span><span class="sxs-lookup"><span data-stu-id="3f727-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="3f727-125">Outras aplicações podem ter diferentes requisitos relativos ao dados precisam de toobe sincronizado, mas para fins de demonstração neste tutorial tem utilizador Olá explicitamente solicitá-la.</span><span class="sxs-lookup"><span data-stu-id="3f727-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="3f727-126">Quando prima este botão, inicia uma nova tarefa em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="3f727-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="3f727-127">Primeiro, este empurra todas as alterações efetuadas toohello arquivo local utilizando o contexto de sincronização, em seguida, obtém todos os alterado dados da tabela local toohello do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f727-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="3f727-128">Testar offline</span><span class="sxs-lookup"><span data-stu-id="3f727-128">Offline testing</span></span>
1. <span data-ttu-id="3f727-129">Dispositivo de Olá local ou simulador no *modo de avião*.</span><span class="sxs-lookup"><span data-stu-id="3f727-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="3f727-130">Esta ação cria um cenário offline.</span><span class="sxs-lookup"><span data-stu-id="3f727-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="3f727-131">Adicione alguns *ToDo* itens ou marca alguns itens como concluídos.</span><span class="sxs-lookup"><span data-stu-id="3f727-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="3f727-132">Sair Olá dispositivo ou simulador (ou Olá forçado a fechar aplicação) e reinicie.</span><span class="sxs-lookup"><span data-stu-id="3f727-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="3f727-133">Certifique-se de que as alterações foram continuadas num dispositivo Olá porque estes são guardados no arquivo local do SQLite Olá.</span><span class="sxs-lookup"><span data-stu-id="3f727-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="3f727-134">Ver conteúdo Olá Olá Azure *TodoItem* tabela com uma ferramenta SQL, tais como *SQL Server Management Studio*, ou um cliente REST, tais como *Fiddler* ou  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="3f727-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="3f727-135">Certifique-se de que novos itens de Olá têm *não* foi sincronizado toohello servidor</span><span class="sxs-lookup"><span data-stu-id="3f727-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="3f727-136">Para um back-end Node.js, visite toohello [portal do Azure](https://portal.azure.com/), e na sua aplicação móvel de back-end clique **tabelas fácil** > **TodoItem** tooview conteúdo Olá Olá `TodoItem` tabela.</span><span class="sxs-lookup"><span data-stu-id="3f727-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="3f727-137">Para um back-end do .NET, tabela de Olá vista contents com uma ferramenta SQL, tais como *SQL Server Management Studio*, ou um cliente REST, tais como *Fiddler* ou *Postman*.</span><span class="sxs-lookup"><span data-stu-id="3f727-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="3f727-138">Ative Wi-Fi no dispositivo de Olá ou simulador.</span><span class="sxs-lookup"><span data-stu-id="3f727-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="3f727-139">Em seguida, prima Olá **atualizar** botão.</span><span class="sxs-lookup"><span data-stu-id="3f727-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="3f727-140">Ver dados de TodoItem Olá novamente Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f727-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="3f727-141">Olá que todoitems novas e alteradas deverá agora aparecer.</span><span class="sxs-lookup"><span data-stu-id="3f727-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f727-142">Recursos Adicionais</span><span class="sxs-lookup"><span data-stu-id="3f727-142">Additional Resources</span></span>
* <span data-ttu-id="3f727-143">[sincronização de dados Offline no Mobile Apps do Azure]</span><span class="sxs-lookup"><span data-stu-id="3f727-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="3f727-144">[Nuvem abrangem: Sincronização Offline nos Mobile Services do Azure] \(Nota: Olá vídeo está nos Mobile Services, mas a sincronização offline funciona de forma semelhante em Mobile Apps do Azure\)</span><span class="sxs-lookup"><span data-stu-id="3f727-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[sincronização de dados Offline no Mobile Apps do Azure]: app-service-mobile-offline-data-sync.md

[criar uma aplicação Android]: app-service-mobile-android-get-started.md

[Nuvem abrangem: Sincronização Offline nos Mobile Services do Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

