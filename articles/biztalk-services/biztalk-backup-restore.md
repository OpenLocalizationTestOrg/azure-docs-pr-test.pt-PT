---
title: "aaaCreate e restaurar uma cópia de segurança nos BizTalk Services | Microsoft Docs"
description: "BizTalk Services inclui a cópia de segurança e restauro. Saiba como toocreate e restaurar uma cópia de segurança e determinar o que obtém uma cópia de segurança. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="0d71c-105">BizTalk Services: Cópia de segurança e Restauro</span><span class="sxs-lookup"><span data-stu-id="0d71c-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="0d71c-106">BizTalk Services do Azure inclui capacidades de cópia de segurança e restauro.</span><span class="sxs-lookup"><span data-stu-id="0d71c-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="0d71c-107">Este tópico descreve como toobackup e restauro dos BizTalk Services utilizando Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d71c-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="0d71c-108">Também pode criar uma cópia dos BizTalk Services utilizando Olá [API de REST do BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="0d71c-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="0d71c-109">As ligações híbridas não são guardados em cópia de segurança, independentemente da edição de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="0d71c-110">Tem de recriar as ligações híbridas.</span><span class="sxs-lookup"><span data-stu-id="0d71c-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="0d71c-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="0d71c-111">Before you Begin</span></span>
* <span data-ttu-id="0d71c-112">Cópia de segurança e restauro poderão não estar disponíveis em todas as edições.</span><span class="sxs-lookup"><span data-stu-id="0d71c-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="0d71c-113">Consulte [dos BizTalk Services: gráfico de edições](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="0d71c-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="0d71c-114">Utilizar Olá portal clássico do Azure, pode criar uma cópia de segurança a pedido ou criar uma cópia de segurança agendada.</span><span class="sxs-lookup"><span data-stu-id="0d71c-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="0d71c-115">Conteúdo de cópia de segurança pode ser restaurada toohello mesmo serviço BizTalk ou tooa novo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="0d71c-116">toorestore Olá BizTalk Service com o mesmo nome, Olá existente BizTalk Service têm de ser eliminado de Olá e nome de Olá tem de estar disponível.</span><span class="sxs-lookup"><span data-stu-id="0d71c-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="0d71c-117">Depois de eliminar um BizTalk Service, pode demorar mais tempo do que pretendia para Olá o mesmo nome toobe disponível.</span><span class="sxs-lookup"><span data-stu-id="0d71c-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="0d71c-118">Se não puder aguardar Olá mesmo nome toobe disponível, em seguida, restaure tooa novo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="0d71c-119">BizTalk Services pode ser restaurada toohello mesma edição ou uma edição superior.</span><span class="sxs-lookup"><span data-stu-id="0d71c-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="0d71c-120">Restaurar os BizTalk Services tooa edição inferior, de quando foi feita a cópia de segurança de Olá, não é suportada.</span><span class="sxs-lookup"><span data-stu-id="0d71c-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="0d71c-121">Por exemplo, uma cópia de segurança utilizando Olá que edição básica pode ser restaurada toohello edição Premium.</span><span class="sxs-lookup"><span data-stu-id="0d71c-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="0d71c-122">Uma cópia de segurança utilizando Olá que Premium Edition não pode ser restaurada toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="0d71c-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="0d71c-123">números de controlo de EDI Olá são cópias de segurança toomaintain continuidade de números de controlo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="0d71c-124">Se as mensagens são processadas após a última cópia de segurança Olá, este conteúdo de cópia de segurança a restaurar pode fazer com que os números de controlo duplicado.</span><span class="sxs-lookup"><span data-stu-id="0d71c-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="0d71c-125">Se um lote tem mensagens Active Directory, processo de batch de Olá **antes** executar uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0d71c-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="0d71c-126">Ao criar uma cópia de segurança (como necessários ou agendada), as mensagens em lotes nunca são armazenadas.</span><span class="sxs-lookup"><span data-stu-id="0d71c-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="0d71c-127">**Se uma cópia de segurança foi efetuada com o Active Directory mensagens num batch, estas mensagens não são cópia de segurança e, por conseguinte, foram perdidas.**</span><span class="sxs-lookup"><span data-stu-id="0d71c-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="0d71c-128">Opcional: No Portal de serviços de BizTalk Olá, pare a quaisquer operações de gestão.</span><span class="sxs-lookup"><span data-stu-id="0d71c-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="0d71c-129">Criar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-129">Create a backup</span></span>
<span data-ttu-id="0d71c-130">Uma cópia de segurança pode ser executada em qualquer altura e é totalmente controlada por si.</span><span class="sxs-lookup"><span data-stu-id="0d71c-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="0d71c-131">Esta secção lista Olá passos toocreate cópias de segurança utilizando Olá clássico do Azure portal, incluindo:</span><span class="sxs-lookup"><span data-stu-id="0d71c-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="0d71c-132">Numa cópia de segurança a pedido</span><span class="sxs-lookup"><span data-stu-id="0d71c-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="0d71c-133">Agendar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="0d71c-134"><a name="backupnow"></a>Numa cópia de segurança a pedido</span><span class="sxs-lookup"><span data-stu-id="0d71c-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="0d71c-135">No portal clássico do Azure Olá, selecione **BizTalk Services**, e, em seguida, selecione Olá pretende toobackup do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="0d71c-136">No Olá **Dashboard** separador, selecione **cópia de segurança** em Olá parte inferior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="0d71c-137">Introduza um nome de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0d71c-137">Enter a backup name.</span></span> <span data-ttu-id="0d71c-138">Por exemplo, introduza *myBizTalkService*BU*data*.</span><span class="sxs-lookup"><span data-stu-id="0d71c-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="0d71c-139">Escolha uma conta do blob storage e a cópia de segurança do Olá selecione marca de verificação toostart Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="0d71c-140">Uma vez concluída a cópia de segurança de Olá, é criado um contentor com o nome de cópia de segurança Olá que introduzir na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="0d71c-141">Este contentor contém a configuração de cópia de segurança do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="0d71c-142"><a name="backupschedule"></a>Agendar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="0d71c-143">No portal clássico do Azure Olá, selecione **BizTalk Services**, selecione Olá nome do BizTalk Service pretende cópia de segurança do tooschedule Olá e, em seguida, selecione Olá **configurar** separador.</span><span class="sxs-lookup"><span data-stu-id="0d71c-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="0d71c-144">Conjunto Olá **estado de cópia de segurança** demasiado**automática**.</span><span class="sxs-lookup"><span data-stu-id="0d71c-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="0d71c-145">Selecione Olá **conta de armazenamento** toostore Olá cópia de segurança, introduza Olá **frequência** toocreate Olá cópias de segurança, cópias de segurança e quanto tookeep Olá (**retenção dias**):</span><span class="sxs-lookup"><span data-stu-id="0d71c-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="0d71c-146">**Notas**</span><span class="sxs-lookup"><span data-stu-id="0d71c-146">**Notes**</span></span>     
   
   * <span data-ttu-id="0d71c-147">No **retenção dias**, o período de retenção de Olá tem de ser superior à frequência de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="0d71c-148">Selecione **mantenha sempre, pelo menos, uma cópia de segurança**, mesmo se for passado Olá período de retenção.</span><span class="sxs-lookup"><span data-stu-id="0d71c-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="0d71c-149">Selecione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0d71c-149">Select **Save**.</span></span>

<span data-ttu-id="0d71c-150">Quando uma tarefa de cópia de segurança agendada é executada, cria um contentor (dados de cópia de segurança toostore) na conta do storage Olá que introduziu.</span><span class="sxs-lookup"><span data-stu-id="0d71c-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="0d71c-151">nome de Olá do contentor de Olá é denominado *nome-data / hora de BizTalk Service*.</span><span class="sxs-lookup"><span data-stu-id="0d71c-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="0d71c-152">Se Olá dashboard do BizTalk Service mostra um **falha** Estado:</span><span class="sxs-lookup"><span data-stu-id="0d71c-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Último Estado de cópia de segurança agendado][BackupStatus] 

<span data-ttu-id="0d71c-154">ligação de Olá abre Olá registos de operação de serviços de gestão toohelp resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="0d71c-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="0d71c-155">Consulte [BizTalk Services: resolver problemas com os registos de operações](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="0d71c-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="0d71c-156">Restauro</span><span class="sxs-lookup"><span data-stu-id="0d71c-156">Restore</span></span>
<span data-ttu-id="0d71c-157">Pode restaurar cópias de segurança de Olá portal clássico do Azure ou de Olá [API REST do serviço BizTalk restaurar](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="0d71c-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="0d71c-158">Esta secção lista Olá passos toorestore através do portal clássico Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="0d71c-159">Antes de restaurar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-159">Before restoring a backup</span></span>
* <span data-ttu-id="0d71c-160">Novo controlo, arquivar e arquivos de monitorização, podem ser introduzidos ao restaurar um BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="0d71c-161">Olá mesmo EDI Runtime serem restaurados.</span><span class="sxs-lookup"><span data-stu-id="0d71c-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="0d71c-162">cópia de segurança do Olá EDI Runtime armazena os números de controlo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="0d71c-163">os números de controlo de Olá restaurada estão na sequência do momento de Olá da cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="0d71c-164">Se as mensagens são processadas após a última cópia de segurança Olá, este conteúdo de cópia de segurança a restaurar pode fazer com que os números de controlo duplicado.</span><span class="sxs-lookup"><span data-stu-id="0d71c-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="0d71c-165">Restaurar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-165">Restore a backup</span></span>
1. <span data-ttu-id="0d71c-166">No portal clássico do Azure Olá, selecione **novo** > **serviços aplicacionais** > **BizTalk Service** > **restaurar** :</span><span class="sxs-lookup"><span data-stu-id="0d71c-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restaurar uma cópia de segurança][Restore]
2. <span data-ttu-id="0d71c-168">No **URL de cópia de segurança**, selecione o ícone da pasta Olá e expanda a conta de armazenamento do Azure Olá que arquivos Olá cópia de segurança de configuração de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="0d71c-169">Expanda o contentor de Olá e no painel direito Olá, selecione Olá correspondente a cópia de segurança ficheiro. txt.</span><span class="sxs-lookup"><span data-stu-id="0d71c-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="0d71c-170">Selecione **abra**.</span><span class="sxs-lookup"><span data-stu-id="0d71c-170">Select **Open**.</span></span>
3. <span data-ttu-id="0d71c-171">No Olá **restaurar o BizTalk Service** página, introduza um **nome do BizTalk Service** e certifique-se Olá **URL do domínio**, **edição**e **Região** para Olá restaurada BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="0d71c-172">**Criar uma nova instância de base de dados do SQL Server** para Olá da base de dados de controlo:</span><span class="sxs-lookup"><span data-stu-id="0d71c-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="0d71c-173">Selecione a seta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="0d71c-174">Verifique o nome de Olá da base de dados SQL de Olá, introduza o servidor físico olá onde será criada a base de dados SQL de Olá e uma nome de utilizador/palavra-passe para esse servidor.</span><span class="sxs-lookup"><span data-stu-id="0d71c-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="0d71c-175">Se pretender que a edição de base de dados SQL do tooconfigure Olá, tamanho e outras propriedades, selecione **configurar definições avançadas da base de dados**.</span><span class="sxs-lookup"><span data-stu-id="0d71c-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="0d71c-176">Selecione a seta seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="0d71c-177">Criar uma nova conta de armazenamento ou introduza uma conta de armazenamento existente para Olá BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="0d71c-178">Selecione o restauro de Olá toostart do Olá marca de verificação.</span><span class="sxs-lookup"><span data-stu-id="0d71c-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="0d71c-179">Depois do restauro de Olá concluir com êxito, um novo serviço BizTalk é listado num estado suspenso na página de BizTalk Services Olá na Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d71c-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="0d71c-180"><a name="postrestore"></a>Depois de restaurar uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="0d71c-181">Olá BizTalk Service está sempre restaurada num **suspenso** estado.</span><span class="sxs-lookup"><span data-stu-id="0d71c-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="0d71c-182">Neste estado, pode efetuar alterações de configuração antes do novo ambiente do Olá está funcional, incluindo:</span><span class="sxs-lookup"><span data-stu-id="0d71c-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="0d71c-183">Se tiver criado Olá SDK dos BizTalk Services do Azure a utilizar aplicações do BizTalk Service, terá as credenciais de controlo de acesso (ACS) de Olá tootooupdate no toowork aplicações com o ambiente de Olá restaurada.</span><span class="sxs-lookup"><span data-stu-id="0d71c-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="0d71c-184">Restaurar tooreplicate um BizTalk Service num ambiente existente do BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="0d71c-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="0d71c-185">Nesta situação, se existirem contratos configurados no portal de BizTalk Services original Olá que utilizam uma pasta de origem FTP, poderá ser necessário contratos de Olá tooupdate no Olá recentemente restaurado ambiente toouse uma pasta FTP de origem diferente.</span><span class="sxs-lookup"><span data-stu-id="0d71c-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="0d71c-186">Caso contrário, poderão existir dois contratos diferentes tentar toopull Olá a mesma mensagem.</span><span class="sxs-lookup"><span data-stu-id="0d71c-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="0d71c-187">Se os tiver restaurado toohave vários ambientes do BizTalk Service, certifique-se de que Olá correto ambiente Olá Visual Studio aplicações, os cmdlets do PowerShell, REST APIs ou APIs de OM de gestão de parceiros comerciais de destino.</span><span class="sxs-lookup"><span data-stu-id="0d71c-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="0d71c-188">É uma boa prática tooconfigure automatizada as cópias de segurança ambiente de serviço BizTalk Olá recentemente restaurado.</span><span class="sxs-lookup"><span data-stu-id="0d71c-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="0d71c-189">toostart Olá BizTalk Service na Olá portal clássico do Azure, selecione de Olá restaurada BizTalk Service e selecione **retomar** na barra de tarefas Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="0d71c-190">O que obtém uma cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-190">What gets backed up</span></span>
<span data-ttu-id="0d71c-191">Quando é criada uma cópia de segurança, hello seguintes itens são uma cópia de segurança:</span><span class="sxs-lookup"><span data-stu-id="0d71c-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="0d71c-192">Itens de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="0d71c-193">
 <strong>Portal de serviços do BizTalk do Azure</strong></span><span class="sxs-lookup"><span data-stu-id="0d71c-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="0d71c-194">Configuração e o tempo de execução</span><span class="sxs-lookup"><span data-stu-id="0d71c-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="0d71c-195">Detalhes de parceiros e perfil</span><span class="sxs-lookup"><span data-stu-id="0d71c-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="0d71c-196">Contratos de parceiros</span><span class="sxs-lookup"><span data-stu-id="0d71c-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="0d71c-197">Assemblagens personalizadas implementadas</span><span class="sxs-lookup"><span data-stu-id="0d71c-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="0d71c-198">Pontes implementado</span><span class="sxs-lookup"><span data-stu-id="0d71c-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="0d71c-199">Certificados</span><span class="sxs-lookup"><span data-stu-id="0d71c-199">Certificates</span></span></li>
<li><span data-ttu-id="0d71c-200">Transformações implementadas</span><span class="sxs-lookup"><span data-stu-id="0d71c-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="0d71c-201">Pipelines</span><span class="sxs-lookup"><span data-stu-id="0d71c-201">Pipelines</span></span></li>
<li><span data-ttu-id="0d71c-202">Modelos criados e guardados no Olá Portal de serviços BizTalk</span><span class="sxs-lookup"><span data-stu-id="0d71c-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="0d71c-203">X12 mapeamentos ST01 e GS01</span><span class="sxs-lookup"><span data-stu-id="0d71c-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="0d71c-204">Números de controlo (EDI)</span><span class="sxs-lookup"><span data-stu-id="0d71c-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="0d71c-205">Valores de AS2 mensagem Dinâmicas</span><span class="sxs-lookup"><span data-stu-id="0d71c-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="0d71c-206">
 <strong>Serviço BizTalk do Azure</strong></span><span class="sxs-lookup"><span data-stu-id="0d71c-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="0d71c-207">Certificado SSL</span><span class="sxs-lookup"><span data-stu-id="0d71c-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="0d71c-208">Dados de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="0d71c-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="0d71c-209">Palavra-passe de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="0d71c-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="0d71c-210">Definições do BizTalk Service</span><span class="sxs-lookup"><span data-stu-id="0d71c-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="0d71c-211">Contagem de unidades de escala</span><span class="sxs-lookup"><span data-stu-id="0d71c-211">Scale unit count</span></span></li>
<li><span data-ttu-id="0d71c-212">Edição</span><span class="sxs-lookup"><span data-stu-id="0d71c-212">Edition</span></span></li>
<li><span data-ttu-id="0d71c-213">Versão do produto</span><span class="sxs-lookup"><span data-stu-id="0d71c-213">Product Version</span></span></li>
<li><span data-ttu-id="0d71c-214">Região/Datacenter</span><span class="sxs-lookup"><span data-stu-id="0d71c-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="0d71c-215">Espaço de nomes de serviço de controlo (ACS) de acesso e a chave</span><span class="sxs-lookup"><span data-stu-id="0d71c-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="0d71c-216">Cadeia de ligação de base de dados de controlo</span><span class="sxs-lookup"><span data-stu-id="0d71c-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="0d71c-217">Cadeia de ligação de conta de armazenamento de arquivo</span><span class="sxs-lookup"><span data-stu-id="0d71c-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="0d71c-218">Cadeia de ligação de conta de armazenamento de monitorização</span><span class="sxs-lookup"><span data-stu-id="0d71c-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="0d71c-219">
 <strong>Itens adicionais</strong></span><span class="sxs-lookup"><span data-stu-id="0d71c-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="0d71c-220">Base de dados de controlo</span><span class="sxs-lookup"><span data-stu-id="0d71c-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="0d71c-221">Quando é criado Olá BizTalk Service, os detalhes da base de dados de controlo de Olá são introduzidos, incluindo Olá SQL Database do Azure e o nome de base de dados de controlo de Olá.</span><span class="sxs-lookup"><span data-stu-id="0d71c-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="0d71c-222">Olá controlo a base de dados não é automaticamente uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0d71c-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="0d71c-223">
<strong>Importante</strong></span><span class="sxs-lookup"><span data-stu-id="0d71c-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="0d71c-224">Se Olá base de dados de controlo é eliminado e Olá necessidades de base de dados recuperadas, tem de existir uma cópia de segurança anterior.</span><span class="sxs-lookup"><span data-stu-id="0d71c-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="0d71c-225">Se não existir uma cópia de segurança, Olá base de dados de controlo e os respetivos dados não são recuperáveis.</span><span class="sxs-lookup"><span data-stu-id="0d71c-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="0d71c-226">Nesta situação, criar uma nova base de dados de controlo Olá com o mesmo nome de base de dados.</span><span class="sxs-lookup"><span data-stu-id="0d71c-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="0d71c-227">Recomenda-se a Georreplicação.</span><span class="sxs-lookup"><span data-stu-id="0d71c-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="0d71c-228">Seguinte</span><span class="sxs-lookup"><span data-stu-id="0d71c-228">Next</span></span>
<span data-ttu-id="0d71c-229">BizTalk Services do Azure toocreate no hello do Azure clássica, aceda demasiado[BizTalk Services: portal clássico do Azure de utilizar o aprovisionamento](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="0d71c-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="0d71c-230">toostart criar aplicações, acedas demasiado[BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="0d71c-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="0d71c-231">Veja Também</span><span class="sxs-lookup"><span data-stu-id="0d71c-231">See Also</span></span>
* [<span data-ttu-id="0d71c-232">Serviço de cópia de segurança de BizTalk</span><span class="sxs-lookup"><span data-stu-id="0d71c-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="0d71c-233">Restaurar o BizTalk Service a partir de cópia de segurança</span><span class="sxs-lookup"><span data-stu-id="0d71c-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="0d71c-234">Os BizTalk Services: Programador, básicas, Standard e Premium gráfico de edições</span><span class="sxs-lookup"><span data-stu-id="0d71c-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="0d71c-235">BizTalk Services: Portal clássico do Azure através de aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="0d71c-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="0d71c-236">Serviços BizTalk: Gráfico de Estado de Aprovisionamento</span><span class="sxs-lookup"><span data-stu-id="0d71c-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="0d71c-237">Serviços BizTalk: Separadores Dashboard, Monitorizar e Dimensionar</span><span class="sxs-lookup"><span data-stu-id="0d71c-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="0d71c-238">Serviços BizTalk: limitação</span><span class="sxs-lookup"><span data-stu-id="0d71c-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="0d71c-239">Serviços BizTalk: Nome e Chave do Emissor</span><span class="sxs-lookup"><span data-stu-id="0d71c-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="0d71c-240">Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure</span><span class="sxs-lookup"><span data-stu-id="0d71c-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

