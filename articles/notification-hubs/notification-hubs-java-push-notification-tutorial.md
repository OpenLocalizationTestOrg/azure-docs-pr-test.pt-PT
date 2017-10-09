---
title: aaaHow toouse Notification Hubs com Java
description: Saiba como toouse Notification Hubs do Azure de um back-end de Java.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="c7ce9-103">Como toouse Notification Hubs de Java</span><span class="sxs-lookup"><span data-stu-id="c7ce9-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="c7ce9-104">Este tópico descreve as principais funcionalidades Olá de oficial Olá novo totalmente suportada SDK de Java do Hub de notificação do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="c7ce9-105">Este é um projeto de código aberto e pode ver o código SDK todo Olá no [Java SDK].</span><span class="sxs-lookup"><span data-stu-id="c7ce9-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="c7ce9-106">Em geral, pode aceder a todas as funcionalidades de Hubs de notificação de um back-end de Java/PHP/Python/Ruby utilizando a interface de REST de Hub de notificação de Olá conforme descrito no tópico do MSDN Olá [APIs REST do Notification Hubs](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c7ce9-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="c7ce9-107">Este SDK de Java fornece um wrapper dinâmico estas interfaces REST em Java.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="c7ce9-108">Olá SDK suporta atualmente:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="c7ce9-109">CRUD em Hubs de notificação</span><span class="sxs-lookup"><span data-stu-id="c7ce9-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="c7ce9-110">CRUD nos registos</span><span class="sxs-lookup"><span data-stu-id="c7ce9-110">CRUD on Registrations</span></span>
* <span data-ttu-id="c7ce9-111">Gestão de instalação</span><span class="sxs-lookup"><span data-stu-id="c7ce9-111">Installation Management</span></span>
* <span data-ttu-id="c7ce9-112">Importar/Exportar registos</span><span class="sxs-lookup"><span data-stu-id="c7ce9-112">Import/Export Registrations</span></span>
* <span data-ttu-id="c7ce9-113">Envia regular</span><span class="sxs-lookup"><span data-stu-id="c7ce9-113">Regular Sends</span></span>
* <span data-ttu-id="c7ce9-114">Envia agendada</span><span class="sxs-lookup"><span data-stu-id="c7ce9-114">Scheduled Sends</span></span>
* <span data-ttu-id="c7ce9-115">Operações assíncronas através de NIO de Java</span><span class="sxs-lookup"><span data-stu-id="c7ce9-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="c7ce9-116">Plataformas suportadas: APNS (iOS), GCM (Android), o WNS (aplicações da loja Windows), MPNS (Windows Phone), ADM (Amazon Kindle Fire), o Baidu (Android sem serviços do Google)</span><span class="sxs-lookup"><span data-stu-id="c7ce9-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="c7ce9-117">Utilização do SDK</span><span class="sxs-lookup"><span data-stu-id="c7ce9-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="c7ce9-118">Compilação e compilação</span><span class="sxs-lookup"><span data-stu-id="c7ce9-118">Compile and build</span></span>
<span data-ttu-id="c7ce9-119">Utilize [Maven]</span><span class="sxs-lookup"><span data-stu-id="c7ce9-119">Use [Maven]</span></span>

<span data-ttu-id="c7ce9-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="c7ce9-121">Código</span><span class="sxs-lookup"><span data-stu-id="c7ce9-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="c7ce9-122">CRUDs de Hub de notificação</span><span class="sxs-lookup"><span data-stu-id="c7ce9-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="c7ce9-123">**Crie um NamespaceManager:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="c7ce9-124">**Crie o Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="c7ce9-125">OU</span><span class="sxs-lookup"><span data-stu-id="c7ce9-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="c7ce9-126">**Obter o Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="c7ce9-127">**Hub de notificação de atualização:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="c7ce9-128">**Elimine o Hub de notificação:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="c7ce9-129">Registo CRUDs</span><span class="sxs-lookup"><span data-stu-id="c7ce9-129">Registration CRUDs</span></span>
<span data-ttu-id="c7ce9-130">**Crie um Hub de notificação de cliente:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="c7ce9-131">**Crie registo do Windows:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="c7ce9-132">**Crie registo de iOS:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="c7ce9-133">Da mesma forma, pode criar registos para Android (GCM), Windows Phone (MPNS) e Fire Kindle (ADM).</span><span class="sxs-lookup"><span data-stu-id="c7ce9-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="c7ce9-134">**Crie registos de modelo:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="c7ce9-135">**Criar registos utilizando criar registrationid + upsert padrão**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="c7ce9-136">Remove os duplicados devido tooany perdido respostas se armazenar os ids de registo no dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="c7ce9-137">**Atualize registos:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="c7ce9-138">**Elimine registos:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="c7ce9-139">**Registos de consulta:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-139">**Query registrations:**</span></span>

* <span data-ttu-id="c7ce9-140">**Obter registo único:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="c7ce9-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="c7ce9-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="c7ce9-142">**Obter todos os registos no hub:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="c7ce9-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="c7ce9-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="c7ce9-144">**Obter registos com etiqueta:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="c7ce9-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="c7ce9-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="c7ce9-146">**Obter registos por canal:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="c7ce9-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="c7ce9-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="c7ce9-148">Todas as consultas de coleção suportam tokens $top e continuação.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="c7ce9-149">Utilização de instalação API</span><span class="sxs-lookup"><span data-stu-id="c7ce9-149">Installation API usage</span></span>
<span data-ttu-id="c7ce9-150">API de instalação é um mecanismo alternativo para a gestão de registo.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="c7ce9-151">Em vez de manutenção de vários registos que não é trivial e pode ser feito facilmente erradamente ou inefficiently, é agora possível toouse um objeto de instalação única.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="c7ce9-152">Instalação contém tudo o que necessita: push canal (token do dispositivo), as etiquetas, modelos, mosaicos secundários (para WNS e APNS).</span><span class="sxs-lookup"><span data-stu-id="c7ce9-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="c7ce9-153">Não precisa de toocall Olá serviço tooget Id já - apenas gerar GUID ou qualquer outro tipo de identificador, mantenha-a no dispositivo e enviar back-end de tooyour juntamente com o canal de emissão (token do dispositivo).</span><span class="sxs-lookup"><span data-stu-id="c7ce9-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="c7ce9-154">No back-end de Olá só deve fazer uma única chamada: CreateOrUpdateInstallation, é totalmente idempotent, por isso, sentir tooretry livre se for necessário.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="c7ce9-155">Como exemplo da Amazon Kindle Fire este aspeto:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="c7ce9-156">Se quiser tooupdate-lo:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="c7ce9-157">Para cenários avançados temos de capacidade de atualização parcial que lhe permite toomodify apenas específicas propriedades do objeto de instalação de Olá.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="c7ce9-158">Basicamente atualização parcial é o subconjunto de operações de Patch de JSON, que pode executar o objeto de instalação.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="c7ce9-159">Elimine a instalação:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="c7ce9-160">CreateOrUpdate, Patch e Delete são eventualmente consistente com Get.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="c7ce9-161">A operação pedida apenas for toohello fila de sistema durante a chamada de Olá e será executada em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="c7ce9-162">Tenha em atenção de que Get não foi concebido para o cenário de tempo de execução principal, mas apenas para fins de resolução de problemas e de depuração, totalmente é limitado pelo serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="c7ce9-163">Fluxo de envio para instalações é hello igual para registos.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="c7ce9-164">Tiver introduzimos apenas toohello de notificação de tootarget uma opção determinada instalação - tag de utilização de apenas "InstallationId: {desired-id}".</span><span class="sxs-lookup"><span data-stu-id="c7ce9-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="c7ce9-165">Para caso acima, seria este aspeto:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="c7ce9-166">Para um dos vários modelos:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="c7ce9-167">Agendar notificações (disponíveis para o escalão STANDARD)</span><span class="sxs-lookup"><span data-stu-id="c7ce9-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="c7ce9-168">Olá mesmo como enviar regular mas com um parâmetro adicional - scheduledTime que indica quando deve ser entregue notificação.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="c7ce9-169">Serviço aceita qualquer ponto de tempo entre agora + 5 minutos e agora + 7 dias.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="c7ce9-170">**Agende uma notificação nativa do Windows:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="c7ce9-171">Importar/exportar (disponível para o escalão STANDARD)</span><span class="sxs-lookup"><span data-stu-id="c7ce9-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="c7ce9-172">Por vezes, é necessário tooperform em massa operação contra registos.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="c7ce9-173">Normalmente, trata-se para a integração com outro sistema ou apenas uma correção enormes toosay atualização Olá as etiquetas.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="c7ce9-174">É vivamente não recomendado toouse fluxo Get/atualização se de que estão a comunicar sobre milhares de registos.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="c7ce9-175">Capacidade de importação/exportação é cenário de Olá toocover concebida.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="c7ce9-176">Basicamente fornecer um contentor de blob toosome acesso na sua conta de armazenamento como uma origem de dados recebidos e a localização de saída.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="c7ce9-177">**Submeta a tarefa de exportação:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="c7ce9-178">**Submeta a tarefa de importação:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="c7ce9-179">**Aguarde até que a tarefa é concluída:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="c7ce9-180">**Obter todas as tarefas:**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="c7ce9-181">**URI com assinatura SAS:** trata Olá URL de alguns ficheiros de blob ou o contentor de blob e o conjunto de parâmetros, tais como permissões e a hora de expiração e assinatura de todos os estas ações efetuadas utilizando a chave SAS da conta.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="c7ce9-182">O SDK de Java de armazenamento do Azure tem capacidades avançadas, incluindo a criação desse tipo de URIs.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="c7ce9-183">Como alternativa simple que pode tomar uma vista de olhos ImportExportE2E classe de teste (a partir da localização do github Olá) que tem uma implementação muito básica e compacta do algoritmo de assinatura.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="c7ce9-184">Enviar notificações</span><span class="sxs-lookup"><span data-stu-id="c7ce9-184">Send Notifications</span></span>
<span data-ttu-id="c7ce9-185">o objeto de notificação de Olá é simplesmente um corpo com cabeçalhos, alguns métodos de utilitário ajudam na criação de objetos de notificações de Olá nativo e modelo.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="c7ce9-186">**Loja Windows e Windows Phone 8.1 (não Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="c7ce9-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="c7ce9-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="c7ce9-189">**Windows Phone 8.0 e 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="c7ce9-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="c7ce9-191">**Enviar tooTags**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="c7ce9-192">**Enviar tootag expressão**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="c7ce9-193">**Enviar notificação de modelo**</span><span class="sxs-lookup"><span data-stu-id="c7ce9-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="c7ce9-194">Executar o seu código de Java deve agora produzir uma notificação de apresentação no seu dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="c7ce9-195"><a name="next-steps"></a>Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="c7ce9-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="c7ce9-196">Este tópico é mostrado como toocreate um Java simple REST cliente para os Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="c7ce9-197">A partir daqui, pode:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-197">From here you can:</span></span>

* <span data-ttu-id="c7ce9-198">Transferir Olá completa [Java SDK], que contém o código SDK todo Olá.</span><span class="sxs-lookup"><span data-stu-id="c7ce9-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="c7ce9-199">Reproduzir com exemplos de Olá:</span><span class="sxs-lookup"><span data-stu-id="c7ce9-199">Play with hello samples:</span></span>
  * <span data-ttu-id="c7ce9-200">[Introdução aos Hubs de notificação]</span><span class="sxs-lookup"><span data-stu-id="c7ce9-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="c7ce9-201">[Enviar notícias de última hora]</span><span class="sxs-lookup"><span data-stu-id="c7ce9-201">[Send breaking news]</span></span>
  * <span data-ttu-id="c7ce9-202">[Notícias de última hora envio localizado]</span><span class="sxs-lookup"><span data-stu-id="c7ce9-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="c7ce9-203">[Enviar notificações tooauthenticated utilizadores]</span><span class="sxs-lookup"><span data-stu-id="c7ce9-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="c7ce9-204">[Enviar notificações de plataforma tooauthenticated utilizadores]</span><span class="sxs-lookup"><span data-stu-id="c7ce9-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introdução aos Hubs de notificação]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Enviar notícias de última hora]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Notícias de última hora envio localizado]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Enviar notificações tooauthenticated utilizadores]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Enviar notificações de plataforma tooauthenticated utilizadores]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

