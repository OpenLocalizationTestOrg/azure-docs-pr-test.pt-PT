---
title: "aaaBack dos servidores do VMware com o servidor de cópia de segurança do Azure | Microsoft Docs"
description: "Utilize o servidor de cópia de segurança do Azure tooback um VMware vCenter/ESXi servidores tooAzure ou disco. Este artigo fornece passo = instruções passo a passo para a cópia de segurança (ou da proteção) as cargas de trabalho do VMware."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a><span data-ttu-id="0a586-104">Criar cópias de segurança uma tooAzure de servidor do VMware</span><span class="sxs-lookup"><span data-stu-id="0a586-104">Back up a VMware server tooAzure</span></span>

<span data-ttu-id="0a586-105">Este artigo explica como toohelp de servidor de cópia de segurança do Azure tooconfigure proteger cargas de trabalho de servidor de VMware.</span><span class="sxs-lookup"><span data-stu-id="0a586-105">This article explains how tooconfigure Azure Backup Server toohelp protect VMware server workloads.</span></span> <span data-ttu-id="0a586-106">Este artigo pressupõe que já tiver instalado de servidor do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-106">This article assumes you already have Azure Backup Server installed.</span></span> <span data-ttu-id="0a586-107">Se não tiver instalado de servidor do Backup do Azure, consulte [preparar tooback utilizando o servidor de cópia de segurança do Azure de cargas de trabalho](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="0a586-107">If you don't have Azure Backup Server installed, see [Prepare tooback up workloads using Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

<span data-ttu-id="0a586-108">Servidor de cópia de segurança do Azure pode criar cópias de segurança ou ajudar a proteger, versão do servidor vCenter 6.5, 6.0 e 5.5 do VMware.</span><span class="sxs-lookup"><span data-stu-id="0a586-108">Azure Backup Server can back up, or help protect, VMware vCenter Server version 6.5, 6.0 and 5.5.</span></span>


## <a name="create-a-secure-connection-toohello-vcenter-server"></a><span data-ttu-id="0a586-109">Criar um servidor vCenter toohello ligação segura</span><span class="sxs-lookup"><span data-stu-id="0a586-109">Create a secure connection toohello vCenter Server</span></span>

<span data-ttu-id="0a586-110">Por predefinição, o servidor de cópia de segurança do Azure comunica com cada servidor vCenter através de um canal HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0a586-110">By default, Azure Backup Server communicates with each vCenter Server via an HTTPS channel.</span></span> <span data-ttu-id="0a586-111">tooturn em comunicação segura Olá, recomendamos que instale o certificado de autoridade de certificação de VMware (CA) de Olá no servidor de cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-111">tooturn on hello secure communication, we recommend that you install hello VMware Certificate Authority (CA) certificate on Azure Backup Server.</span></span> <span data-ttu-id="0a586-112">Se não necessitam de uma comunicação segura e prefere requisito de HTTPS do toodisable Olá, consulte [protocolo de comunicação segura desativar](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span><span class="sxs-lookup"><span data-stu-id="0a586-112">If you don't require secure communication, and would prefer toodisable hello HTTPS requirement, see [Disable secure communication protocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol).</span></span> <span data-ttu-id="0a586-113">toocreate uma ligação segura entre o servidor de cópia de segurança do Azure e Olá vCenter Server, importe o certificado fidedigno do Olá no servidor de cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-113">toocreate a secure connection between Azure Backup Server and hello vCenter Server, import hello trusted certificate on Azure Backup Server.</span></span>

<span data-ttu-id="0a586-114">Normalmente, utilizar um browser no Olá servidor de cópia de segurança do Azure machine tooconnect toohello vCenter Server através de Olá vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="0a586-114">Typically, you use a browser on hello Azure Backup Server machine tooconnect toohello vCenter Server via hello vSphere Web Client.</span></span> <span data-ttu-id="0a586-115">Olá pela primeira vez que é utilizar Olá servidor de cópia de segurança do Azure browser tooconnect toohello vCenter Server, ligação Olá não é segura.</span><span class="sxs-lookup"><span data-stu-id="0a586-115">hello first time you use hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connection isn't secure.</span></span> <span data-ttu-id="0a586-116">Olá imagem a seguir mostra ligação Olá protegida.</span><span class="sxs-lookup"><span data-stu-id="0a586-116">hello following image shows hello unsecured connection.</span></span>

![Exemplo de servidor de tooVMware de uma ligação não segura](./media/backup-azure-backup-server-vmware/unsecure-url.png)

<span data-ttu-id="0a586-118">toofix este problema e criar uma ligação segura, transfira Olá fidedigno certificados de AC de raiz.</span><span class="sxs-lookup"><span data-stu-id="0a586-118">toofix this issue, and create a secure connection, download hello trusted root CA certificates.</span></span>

1. <span data-ttu-id="0a586-119">Num browser de Olá no servidor de cópia de segurança do Azure, introduza Olá URL toohello vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="0a586-119">In hello browser on Azure Backup Server, enter hello URL toohello vSphere Web Client.</span></span> <span data-ttu-id="0a586-120">é apresentada a página de início de sessão do Olá vSphere cliente Web.</span><span class="sxs-lookup"><span data-stu-id="0a586-120">hello vSphere Web Client login page appears.</span></span>

    ![vSphere Web cliente](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    <span data-ttu-id="0a586-122">Na parte inferior de Olá de informações de Olá para os administradores e programadores, localize Olá **transferência os certificados de AC de raiz fidedigna** ligação.</span><span class="sxs-lookup"><span data-stu-id="0a586-122">At hello bottom of hello information for administrators and developers, locate hello **Download trusted root CA certificates** link.</span></span>

    ![Ligação toodownload Olá fidedigno certificados de AC raiz](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  <span data-ttu-id="0a586-124">Se não vir a página de início de sessão de cliente Web de vSphere Olá, verifique as definições de proxy do seu browser.</span><span class="sxs-lookup"><span data-stu-id="0a586-124">If you don't see hello vSphere Web Client login page, check your browser's proxy settings.</span></span>

2. <span data-ttu-id="0a586-125">Clique em **transferência os certificados de AC de raiz fidedigna**.</span><span class="sxs-lookup"><span data-stu-id="0a586-125">Click **Download trusted root CA certificates**.</span></span>

    <span data-ttu-id="0a586-126">Olá vCenter Server transfere um computador local do ficheiro tooyour.</span><span class="sxs-lookup"><span data-stu-id="0a586-126">hello vCenter Server downloads a file tooyour local computer.</span></span> <span data-ttu-id="0a586-127">Olá nome do ficheiro é denominado **transferir**.</span><span class="sxs-lookup"><span data-stu-id="0a586-127">hello file's name is named **download**.</span></span> <span data-ttu-id="0a586-128">Dependendo do seu browser, receberá uma mensagem a perguntar se tooopen ou guardar o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-128">Depending on your browser, you receive a message that asks whether tooopen or save hello file.</span></span>

    ![Transferir a mensagem quando os certificados são transferidos](./media/backup-azure-backup-server-vmware/download-certs.png)

3. <span data-ttu-id="0a586-130">Localização Olá ficheiro tooa no servidor de cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-130">Save hello file tooa location on Azure Backup Server.</span></span> <span data-ttu-id="0a586-131">Quando guardar ficheiro Olá, adicione a extensão de nome de ficheiro do Olá. zip.</span><span class="sxs-lookup"><span data-stu-id="0a586-131">When you save hello file, add hello .zip file name extension.</span></span>

    <span data-ttu-id="0a586-132">ficheiro de Olá é um ficheiro. zip que contém informações de Olá sobre certificados Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-132">hello file is a .zip file that contains hello information about hello certificates.</span></span> <span data-ttu-id="0a586-133">Com a extensão. zip de Olá, pode utilizar ferramentas de extração Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-133">With hello .zip extension, you can use hello extraction tools.</span></span>

4. <span data-ttu-id="0a586-134">Clique com botão direito **download.zip**e, em seguida, selecione **extrair todos os** conteúdo de Olá tooextract.</span><span class="sxs-lookup"><span data-stu-id="0a586-134">Right-click **download.zip**, and then select **Extract All** tooextract hello contents.</span></span>

    <span data-ttu-id="0a586-135">ficheiro. zip de Olá extrai a respetiva pasta de tooa de conteúdo com o nome **certificados**.</span><span class="sxs-lookup"><span data-stu-id="0a586-135">hello .zip file extracts its contents tooa folder named **certs**.</span></span> <span data-ttu-id="0a586-136">São apresentados dois tipos de ficheiros na pasta de certificados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-136">Two types of files appear in hello certs folder.</span></span> <span data-ttu-id="0a586-137">ficheiro de certificado de raiz de Olá tem uma extensão que comece com uma sequência como.0 e.1 numerada.</span><span class="sxs-lookup"><span data-stu-id="0a586-137">hello root certificate file has an extension that begins with a numbered sequence like .0 and .1.</span></span>
    
    <span data-ttu-id="0a586-138">ficheiro CRL Olá tem uma extensão que comece com uma sequência como .r0 ou .r1.</span><span class="sxs-lookup"><span data-stu-id="0a586-138">hello CRL file has an extension that begins with a sequence like .r0 or .r1.</span></span> <span data-ttu-id="0a586-139">ficheiro CRL Olá está associado um certificado.</span><span class="sxs-lookup"><span data-stu-id="0a586-139">hello CRL file is associated with a certificate.</span></span>

    ![<span data-ttu-id="0a586-140">Transferir os ficheiros extraídos localmente</span><span class="sxs-lookup"><span data-stu-id="0a586-140">Download file extracted locally</span></span> ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. <span data-ttu-id="0a586-141">No Olá **certificados** pasta, clique no ficheiro de certificado de raiz de Olá e, em seguida, clique em **mudar o nome**.</span><span class="sxs-lookup"><span data-stu-id="0a586-141">In hello **certs** folder, right-click hello root certificate file, and then click **Rename**.</span></span>

    ![<span data-ttu-id="0a586-142">Mudar o nome do certificado de raiz</span><span class="sxs-lookup"><span data-stu-id="0a586-142">Rename root certificate</span></span> ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    <span data-ttu-id="0a586-143">Altere o too.crt de extensão certificado de raiz a Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-143">Change hello root certificate's extension too.crt.</span></span> <span data-ttu-id="0a586-144">Quando estiver a pedido se tiver a certeza de que pretende toochange extensão de Olá, clique em **Sim** ou **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a586-144">When you're asked if you're sure you want toochange hello extension, click **Yes** or **OK**.</span></span> <span data-ttu-id="0a586-145">Caso contrário, alterar função pretendida do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-145">Otherwise, you change hello file's intended function.</span></span> <span data-ttu-id="0a586-146">ícone de Olá para ícone tooan de alterações de ficheiros de Olá que representa um certificado de raiz.</span><span class="sxs-lookup"><span data-stu-id="0a586-146">hello icon for hello file changes tooan icon that represents a root certificate.</span></span>

6. <span data-ttu-id="0a586-147">Clique no certificado de raiz de Olá e no menu de pop-up Olá, selecione **instalar certificado**.</span><span class="sxs-lookup"><span data-stu-id="0a586-147">Right-click hello root certificate and from hello pop-up menu, select **Install Certificate**.</span></span>

    <span data-ttu-id="0a586-148">Olá **Assistente para importar certificados** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-148">hello **Certificate Import Wizard** dialog box appears.</span></span>

7. <span data-ttu-id="0a586-149">No Olá **Assistente para importar certificados** caixa de diálogo, selecione **máquina Local** como destino de Olá para Olá certificado e, em seguida, clique em **seguinte** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0a586-149">In hello **Certificate Import Wizard** dialog box, select **Local Machine** as hello destination for hello certificate, and then click **Next** toocontinue.</span></span>

    ![<span data-ttu-id="0a586-150">Opções de destino de armazenamento de certificados</span><span class="sxs-lookup"><span data-stu-id="0a586-150">Certificate storage destination options</span></span> ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    <span data-ttu-id="0a586-151">Se estiver a lhe for perguntado se pretende que o computador de toohello tooallow alterações, clique em **Sim** ou **OK**, alterações de Olá tooall.</span><span class="sxs-lookup"><span data-stu-id="0a586-151">If you're asked if you want tooallow changes toohello computer, click **Yes** or **OK**, tooall hello changes.</span></span>

8. <span data-ttu-id="0a586-152">No Olá **arquivo de certificados** página, selecione **colocar todos os certificados no Olá seguir arquivo**e, em seguida, clique em **procurar** arquivo de certificados de Olá toochoose.</span><span class="sxs-lookup"><span data-stu-id="0a586-152">On hello **Certificate Store** page, select **Place all certificates in hello following store**, and then click **Browse** toochoose hello certificate store.</span></span>

    ![Colocar os certificados num lugar para cima de armazenamento específico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    <span data-ttu-id="0a586-154">Olá **selecionar arquivo de certificados** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-154">hello **Select Certificate Store** dialog box appears.</span></span>

    ![Hierarquia de pastas de armazenamento de certificados](./media/backup-azure-backup-server-vmware/cert-store.png)

9. <span data-ttu-id="0a586-156">Selecione **autoridades de certificação de raiz fidedigna** como pasta de destino Olá de Olá certificados e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a586-156">Select **Trusted Root Certification Authorities** as hello destination folder for hello certificates, and then click **OK**.</span></span>

    ![Pasta de destino de certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    <span data-ttu-id="0a586-158">Olá **autoridades de certificação de raiz fidedigna** pasta foi confirmada como como arquivo de certificados de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-158">hello **Trusted Root Certification Authorities** folder is confirmed as hello certificate store.</span></span> <span data-ttu-id="0a586-159">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-159">Click **Next**.</span></span>

    ![Pasta de arquivo de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. <span data-ttu-id="0a586-161">No Olá **Olá concluir o Assistente de importação de certificados** página, certifique-se de que esse certificado Olá é na pasta pretendido Olá e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="0a586-161">On hello **Completing hello Certificate Import Wizard** page, verify that hello certificate is in hello desired folder, and then click **Finish**.</span></span>

    ![Verificar o certificado é na pasta correta Olá](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    <span data-ttu-id="0a586-163">É apresentada uma caixa de diálogo, a importação do certificado com êxito de Olá é confirmada.</span><span class="sxs-lookup"><span data-stu-id="0a586-163">A dialog box appears, hello successful certificate import is confirmed.</span></span>

11. <span data-ttu-id="0a586-164">Inicie sessão no toohello vCenter tooconfirm de servidor que a ligação é segura.</span><span class="sxs-lookup"><span data-stu-id="0a586-164">Sign in toohello vCenter Server tooconfirm that your connection is secure.</span></span>

  <span data-ttu-id="0a586-165">Se importar certificados de Olá não for concluída com êxito e não é possível estabelecer uma ligação segura, consulte a documentação de vSphere de VMware Olá no [obter certificados de servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span><span class="sxs-lookup"><span data-stu-id="0a586-165">If hello certificate import is not successful, and you cannot establish a secure connection, consult hello VMware vSphere documentation on [obtaining server certificates](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).</span></span>

  <span data-ttu-id="0a586-166">Se tiver limites segurados na sua organização e não pretende tooturn no Olá protocolo HTTPS, utilize Olá comunicações seguro do procedimento toodisable Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="0a586-166">If you have secure boundaries within your organization, and don't want tooturn on hello HTTPS protocol, use hello following procedure toodisable hello secure communications.</span></span>

### <a name="disable-secure-communication-protocol"></a><span data-ttu-id="0a586-167">Desativar o protocolo de comunicação segura</span><span class="sxs-lookup"><span data-stu-id="0a586-167">Disable secure communication protocol</span></span>

<span data-ttu-id="0a586-168">Se a sua organização não requer o protocolo HTTPS de Olá, utilize Olá os seguintes passos toodisable HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0a586-168">If your organization doesn't require hello HTTPS protocol, use hello following steps toodisable HTTPS.</span></span> <span data-ttu-id="0a586-169">toodisable Olá comportamento predefinido, crie uma chave de registo que ignora o comportamento predefinido de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-169">toodisable hello default behavior, create a registry key that ignores hello default behavior.</span></span>

1. <span data-ttu-id="0a586-170">Copie e cole Olá seguir texto num ficheiro. txt.</span><span class="sxs-lookup"><span data-stu-id="0a586-170">Copy and paste hello following text into a .txt file.</span></span>

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. <span data-ttu-id="0a586-171">Guarde o computador de servidor de cópia de segurança do Azure Olá ficheiro tooyour.</span><span class="sxs-lookup"><span data-stu-id="0a586-171">Save hello file tooyour Azure Backup Server computer.</span></span> <span data-ttu-id="0a586-172">Para nome de ficheiro Olá, utilize DisableSecureAuthentication.reg.</span><span class="sxs-lookup"><span data-stu-id="0a586-172">For hello file name, use DisableSecureAuthentication.reg.</span></span>

3. <span data-ttu-id="0a586-173">Faça duplo clique entrada de registo do Olá ficheiro tooactivate Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-173">Double-click hello file tooactivate hello registry entry.</span></span>


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a><span data-ttu-id="0a586-174">Criar uma conta de utilizador e função no Olá vCenter Server</span><span class="sxs-lookup"><span data-stu-id="0a586-174">Create a role and user account on hello vCenter Server</span></span>

<span data-ttu-id="0a586-175">No Olá vCenter Server, uma função é um conjunto predefinido de privilégios.</span><span class="sxs-lookup"><span data-stu-id="0a586-175">On hello vCenter Server, a role is a predefined set of privileges.</span></span> <span data-ttu-id="0a586-176">Um administrador do servidor vCenter cria funções Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-176">A vCenter Server administrator creates hello roles.</span></span> <span data-ttu-id="0a586-177">tooassign permissões, o administrador de Olá pares contas de utilizador com uma função.</span><span class="sxs-lookup"><span data-stu-id="0a586-177">tooassign permissions, hello administrator pairs user accounts with a role.</span></span> <span data-ttu-id="0a586-178">tooestablish Olá utilizador necessário credenciais tooback se o computador do servidor do vCenter Olá, criar uma função com privilégios específicos e, em seguida, associar a conta de utilizador Olá com função Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-178">tooestablish hello necessary user credentials tooback up hello vCenter Server computer, create a role with specific privileges, and then associate hello user account with hello role.</span></span>

<span data-ttu-id="0a586-179">Servidor de cópia de segurança do Azure utiliza um nome de utilizador e palavra-passe tooauthenticate com Olá vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="0a586-179">Azure Backup Server uses a username and password tooauthenticate with hello vCenter Server.</span></span> <span data-ttu-id="0a586-180">Servidor do Backup do Azure utiliza estas credenciais como autenticação para todas as operações de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0a586-180">Azure Backup Server uses these credentials as authentication for all backup operations.</span></span>

<span data-ttu-id="0a586-181">tooadd um função de servidor do vCenter e os respetivos privilégios para um administrador de cópias de segurança:</span><span class="sxs-lookup"><span data-stu-id="0a586-181">tooadd a vCenter Server role and its privileges for a backup administrator:</span></span>

1. <span data-ttu-id="0a586-182">Inicie sessão no toohello vCenter Server e, em seguida, no Olá vCenter Server **navegador** painel, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="0a586-182">Sign in toohello vCenter Server, and then in hello vCenter Server **Navigator** panel, click **Administration**.</span></span>

    ![Opção de administração no painel do vCenter Server navegador](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. <span data-ttu-id="0a586-184">No **administração** selecione **funções**e, em seguida, no Olá **funções** painel clique Olá adicionar ícone de função (símbolo + Olá).</span><span class="sxs-lookup"><span data-stu-id="0a586-184">In **Administration** select **Roles**, and then in hello **Roles** panel click hello add role icon (hello + symbol).</span></span>

    ![Adicionar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    <span data-ttu-id="0a586-186">Olá **criar função** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-186">hello **Create Role** dialog box appears.</span></span>

    ![Criar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. <span data-ttu-id="0a586-188">No Olá **criar função** Olá caixa de diálogo **nome da função** box, introduza *BackupAdminRole*.</span><span class="sxs-lookup"><span data-stu-id="0a586-188">In hello **Create Role** dialog box, in hello **Role name** box, enter *BackupAdminRole*.</span></span> <span data-ttu-id="0a586-189">nome da função Olá pode ser que quiser, mas deve ser reconhecível para fim da função de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-189">hello role name can be whatever you like, but it should be recognizable for hello role's purpose.</span></span>

4. <span data-ttu-id="0a586-190">Selecione privilégios Olá para a versão adequada do Olá do vCenter e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a586-190">Select hello privileges for hello appropriate version of vCenter, and then click **OK**.</span></span> <span data-ttu-id="0a586-191">Olá, a tabela seguinte identifica privilégios Olá necessário para o vCenter 6.0 e vCenter 5.5.</span><span class="sxs-lookup"><span data-stu-id="0a586-191">hello following table identifies hello required privileges for vCenter 6.0 and vCenter 5.5.</span></span>

  <span data-ttu-id="0a586-192">Quando seleciona privilégios Olá, clique em Olá ícone seguintes toohello principal etiqueta tooexpand Olá principal e vista Olá subordinado privilégios.</span><span class="sxs-lookup"><span data-stu-id="0a586-192">When you select hello privileges, click hello icon next toohello parent label tooexpand hello parent and view hello child privileges.</span></span> <span data-ttu-id="0a586-193">privilégios de máquina virtual do tooselect Olá, terá de toogo vários níveis em Olá principal hierarquia subordinado.</span><span class="sxs-lookup"><span data-stu-id="0a586-193">tooselect hello VirtualMachine privileges, you need toogo several levels into hello parent child hierarchy.</span></span> <span data-ttu-id="0a586-194">Não precisa de tooselect todos os privilégios subordinado dentro de um privilégio principal.</span><span class="sxs-lookup"><span data-stu-id="0a586-194">You don't need tooselect all child privileges within a parent privilege.</span></span>

  ![Hierarquia de privilégio principal subordinado](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  <span data-ttu-id="0a586-196">Depois de clicar em **OK**, nova função de Olá aparece na lista de Olá no painel de funções de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-196">After you click **OK**, hello new role appears in hello list on hello Roles panel.</span></span>

|<span data-ttu-id="0a586-197">Privilégios para o vCenter 6.0</span><span class="sxs-lookup"><span data-stu-id="0a586-197">Privileges for vCenter 6.0</span></span>| <span data-ttu-id="0a586-198">Privilégios para o vCenter 5.5</span><span class="sxs-lookup"><span data-stu-id="0a586-198">Privileges for vCenter 5.5</span></span>|
|--------------------------|---------------------------|
|<span data-ttu-id="0a586-199">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="0a586-199">Datastore.AllocateSpace</span></span>   | <span data-ttu-id="0a586-200">Datastore.AllocateSpace</span><span class="sxs-lookup"><span data-stu-id="0a586-200">Datastore.AllocateSpace</span></span>|
|<span data-ttu-id="0a586-201">Global.ManageCustomFields</span><span class="sxs-lookup"><span data-stu-id="0a586-201">Global.ManageCustomFields</span></span> | <span data-ttu-id="0a586-202">Global.ManageCustomerFields</span><span class="sxs-lookup"><span data-stu-id="0a586-202">Global.ManageCustomerFields</span></span>|
|<span data-ttu-id="0a586-203">Global.SetCustomFields</span><span class="sxs-lookup"><span data-stu-id="0a586-203">Global.SetCustomFields</span></span>    |   |
|<span data-ttu-id="0a586-204">Host.Local.CreateVM</span><span class="sxs-lookup"><span data-stu-id="0a586-204">Host.Local.CreateVM</span></span>       | <span data-ttu-id="0a586-205">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="0a586-205">Network.Assign</span></span> |
|<span data-ttu-id="0a586-206">Network.Assign</span><span class="sxs-lookup"><span data-stu-id="0a586-206">Network.Assign</span></span>            |  |
|<span data-ttu-id="0a586-207">Resource.AssignVMToPool</span><span class="sxs-lookup"><span data-stu-id="0a586-207">Resource.AssignVMToPool</span></span>   |  |
|<span data-ttu-id="0a586-208">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="0a586-208">VirtualMachine.Config.AddNewDisk</span></span>  | <span data-ttu-id="0a586-209">VirtualMachine.Config.AddNewDisk</span><span class="sxs-lookup"><span data-stu-id="0a586-209">VirtualMachine.Config.AddNewDisk</span></span>   |
|<span data-ttu-id="0a586-210">VirtualMachine.Config.AdvanceConfig</span><span class="sxs-lookup"><span data-stu-id="0a586-210">VirtualMachine.Config.AdvanceConfig</span></span>| <span data-ttu-id="0a586-211">VirtualMachine.Config.AdvancedConfig</span><span class="sxs-lookup"><span data-stu-id="0a586-211">VirtualMachine.Config.AdvancedConfig</span></span>|
|<span data-ttu-id="0a586-212">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="0a586-212">VirtualMachine.Config.ChangeTracking</span></span>| <span data-ttu-id="0a586-213">VirtualMachine.Config.ChangeTracking</span><span class="sxs-lookup"><span data-stu-id="0a586-213">VirtualMachine.Config.ChangeTracking</span></span> |
|<span data-ttu-id="0a586-214">VirtualMachine.Config.HostUSBDevice</span><span class="sxs-lookup"><span data-stu-id="0a586-214">VirtualMachine.Config.HostUSBDevice</span></span>||
|<span data-ttu-id="0a586-215">VirtualMachine.Config.QueryUnownedFiles</span><span class="sxs-lookup"><span data-stu-id="0a586-215">VirtualMachine.Config.QueryUnownedFiles</span></span>|    |
|<span data-ttu-id="0a586-216">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="0a586-216">VirtualMachine.Config.SwapPlacement</span></span>| <span data-ttu-id="0a586-217">VirtualMachine.Config.SwapPlacement</span><span class="sxs-lookup"><span data-stu-id="0a586-217">VirtualMachine.Config.SwapPlacement</span></span> |
|<span data-ttu-id="0a586-218">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="0a586-218">VirtualMachine.Interact.PowerOff</span></span>| <span data-ttu-id="0a586-219">VirtualMachine.Interact.PowerOff</span><span class="sxs-lookup"><span data-stu-id="0a586-219">VirtualMachine.Interact.PowerOff</span></span> |
|<span data-ttu-id="0a586-220">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="0a586-220">VirtualMachine.Inventory.Create</span></span>| <span data-ttu-id="0a586-221">VirtualMachine.Inventory.Create</span><span class="sxs-lookup"><span data-stu-id="0a586-221">VirtualMachine.Inventory.Create</span></span> |
|<span data-ttu-id="0a586-222">VirtualMachine.Provisioning.DiskRandomAccess</span><span class="sxs-lookup"><span data-stu-id="0a586-222">VirtualMachine.Provisioning.DiskRandomAccess</span></span>| |
|<span data-ttu-id="0a586-223">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="0a586-223">VirtualMachine.Provisioning.DiskRandomRead</span></span>|<span data-ttu-id="0a586-224">VirtualMachine.Provisioning.DiskRandomRead</span><span class="sxs-lookup"><span data-stu-id="0a586-224">VirtualMachine.Provisioning.DiskRandomRead</span></span> |
|<span data-ttu-id="0a586-225">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="0a586-225">VirtualMachine.State.CreateSnapshot</span></span>| <span data-ttu-id="0a586-226">VirtualMachine.State.CreateSnapshot</span><span class="sxs-lookup"><span data-stu-id="0a586-226">VirtualMachine.State.CreateSnapshot</span></span>|
|<span data-ttu-id="0a586-227">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="0a586-227">VirtualMachine.State.RemoveSnapshot</span></span>|<span data-ttu-id="0a586-228">VirtualMachine.State.RemoveSnapshot</span><span class="sxs-lookup"><span data-stu-id="0a586-228">VirtualMachine.State.RemoveSnapshot</span></span> |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a><span data-ttu-id="0a586-229">Criar uma conta de utilizador do servidor vCenter e permissões</span><span class="sxs-lookup"><span data-stu-id="0a586-229">Create a vCenter Server user account and permissions</span></span>

<span data-ttu-id="0a586-230">Depois de configurar função Olá com privilégios, crie uma conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="0a586-230">After hello role with privileges is set up, create a user account.</span></span> <span data-ttu-id="0a586-231">conta de utilizador de Olá tem um nome e uma palavra-passe, fornece credenciais Olá que são utilizadas para autenticação.</span><span class="sxs-lookup"><span data-stu-id="0a586-231">hello user account has a name and password, which provides hello credentials that are used for authentication.</span></span>

1. <span data-ttu-id="0a586-232">toocreate uma conta de utilizador, no Olá vCenter Server **navegador** painel, clique em **utilizadores e grupos**.</span><span class="sxs-lookup"><span data-stu-id="0a586-232">toocreate a user account, in hello vCenter Server **Navigator** panel, click **Users and Groups**.</span></span>

    ![Opção de utilizadores e grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    <span data-ttu-id="0a586-234">Olá **vCenter utilizadores e grupos** painel aparece.</span><span class="sxs-lookup"><span data-stu-id="0a586-234">hello **vCenter Users and Groups** panel appears.</span></span>

    ![Painel de utilizadores e grupos do vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. <span data-ttu-id="0a586-236">No Olá **vCenter utilizadores e grupos** painel, selecione de Olá **utilizadores** separador e, em seguida, clique em Olá adicionar ícone de utilizadores (símbolo + Olá).</span><span class="sxs-lookup"><span data-stu-id="0a586-236">In hello **vCenter Users and Groups** panel, select hello **Users** tab, and then click hello add users icon (hello + symbol).</span></span>

    <span data-ttu-id="0a586-237">Olá **novo utilizador** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-237">hello **New User** dialog box appears.</span></span>

3. <span data-ttu-id="0a586-238">No Olá **novo utilizador** diálogo caixa, adicionar informações do utilizador Olá e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a586-238">In hello **New User** dialog box, add hello user's information and then click **OK**.</span></span> <span data-ttu-id="0a586-239">Neste procedimento, o nome de utilizador Olá é BackupAdmin.</span><span class="sxs-lookup"><span data-stu-id="0a586-239">In this procedure, hello username is BackupAdmin.</span></span>

    ![Caixa de diálogo do novo utilizador](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    <span data-ttu-id="0a586-241">nova conta de utilizador Olá aparece na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-241">hello new user account appears in hello list.</span></span>

4. <span data-ttu-id="0a586-242">conta de utilizador de Olá tooassociate na função Olá, no Olá **navegador** painel, clique em **permissões Global**.</span><span class="sxs-lookup"><span data-stu-id="0a586-242">tooassociate hello user account with hello role, in hello **Navigator** panel, click **Global Permissions**.</span></span> <span data-ttu-id="0a586-243">No Olá **permissões Global** painel, selecione de Olá **gerir** separador e, em seguida, clique em Olá adicionar ícone (símbolo + Olá).</span><span class="sxs-lookup"><span data-stu-id="0a586-243">In hello **Global Permissions** panel, select hello **Manage** tab, and then click hello add icon (hello + symbol).</span></span>

    ![Painel de permissões global](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    <span data-ttu-id="0a586-245">Olá **raiz de permissões de Global - adicionar permissão** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-245">hello **Global Permissions Root - Add Permission** dialog box appears.</span></span>

5. <span data-ttu-id="0a586-246">No Olá **raiz de permissão de Global - adicionar permissão** caixa de diálogo, clique em **adicionar** toochoose Olá utilizador ou grupo.</span><span class="sxs-lookup"><span data-stu-id="0a586-246">In hello **Global Permission Root - Add Permission** dialog box, click **Add** toochoose hello user or group.</span></span>

    ![Escolha o utilizador ou grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    <span data-ttu-id="0a586-248">Olá **selecionar utilizadores/grupos** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-248">hello **Select Users/Groups** dialog box appears.</span></span>

6. <span data-ttu-id="0a586-249">No Olá **selecionar utilizadores/grupos** diálogo caixa, escolha **BackupAdmin** e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0a586-249">In hello **Select Users/Groups** dialog box, choose **BackupAdmin** and then click **Add**.</span></span>

    <span data-ttu-id="0a586-250">No **utilizadores**, Olá *domínio ome de utilizador* formato é utilizado para a conta de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-250">In **Users**, hello *domain\username* format is used for hello user account.</span></span> <span data-ttu-id="0a586-251">Se quiser toouse um domínio diferente, selecione de Olá **domínio** lista.</span><span class="sxs-lookup"><span data-stu-id="0a586-251">If you want toouse a different domain, choose it from hello **Domain** list.</span></span>

    ![Adicionar utilizador BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    <span data-ttu-id="0a586-253">Clique em **OK** tooadd Olá selecionado utilizadores toohello **adicionar permissão** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-253">Click **OK** tooadd hello selected users toohello **Add Permission** dialog box.</span></span>

7. <span data-ttu-id="0a586-254">Agora que identificou utilizador Olá, atribua a função de toohello Olá utilizador.</span><span class="sxs-lookup"><span data-stu-id="0a586-254">Now that you've identified hello user, assign hello user toohello role.</span></span> <span data-ttu-id="0a586-255">No **função atribuída**, na Olá na lista pendente, selecione **BackupAdminRole**e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a586-255">In **Assigned Role**, from hello drop-down list, select **BackupAdminRole**, and then click **OK**.</span></span>

    ![Atribuir toorole de utilizador](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  <span data-ttu-id="0a586-257">No Olá **gerir** separador Olá **permissões Global** painel, a nova conta de utilizador Olá e a função de Olá associado são apresentados na lista de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-257">On hello **Manage** tab in hello **Global Permissions** panel, hello new user account and hello associated role appear in hello list.</span></span>


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a><span data-ttu-id="0a586-258">Estabelecer as credenciais do servidor vCenter no servidor de cópia de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="0a586-258">Establish vCenter Server credentials on Azure Backup Server</span></span>

<span data-ttu-id="0a586-259">Antes de adicionar Olá VMware server tooAzure servidor de cópia de segurança, instale [atualização 1 para o servidor de cópia de segurança do Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span><span class="sxs-lookup"><span data-stu-id="0a586-259">Before you add hello VMware server tooAzure Backup Server, install [Update 1 for Azure Backup Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).</span></span>

1. <span data-ttu-id="0a586-260">tooopen servidor de cópia de segurança do Azure, faça duplo clique no ícone Olá no ambiente de trabalho do Olá servidor de cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-260">tooopen Azure Backup Server, double-click hello icon on hello Azure Backup Server desktop.</span></span>

    ![Ícone de servidor do Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    <span data-ttu-id="0a586-262">Se não é possível localizar o ícone de Olá no ambiente de trabalho Olá, abra o servidor de cópia de segurança do Azure na lista de Olá das aplicações instaladas.</span><span class="sxs-lookup"><span data-stu-id="0a586-262">If you can't find hello icon on hello desktop, open Azure Backup Server from hello list of installed apps.</span></span> <span data-ttu-id="0a586-263">nome de aplicação de servidor de cópia de segurança do Azure Olá denomina-se a cópia de segurança do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-263">hello Azure Backup Server app name is called Microsoft Azure Backup.</span></span>

2. <span data-ttu-id="0a586-264">Na consola do servidor de cópia de segurança do Azure Olá, clique em **gestão**, clique em **servidores de produção**e, em seguida, no Friso de ferramentas Olá, clique em **gerir VMware**.</span><span class="sxs-lookup"><span data-stu-id="0a586-264">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then on hello tool ribbon, click **Manage VMware**.</span></span>

    ![Consola do servidor do Backup do Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    <span data-ttu-id="0a586-266">Olá **gerir credenciais** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-266">hello **Manage Credentials** dialog box appears.</span></span>

    ![Caixa de diálogo Gerir credenciais do servidor de cópia de segurança do Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. <span data-ttu-id="0a586-268">No Olá **gerir credenciais** caixa de diálogo, clique em **adicionar** tooopen Olá **adicionar credencial** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-268">In hello **Manage Credentials** dialog box, click **Add** tooopen hello **Add Credential** dialog box.</span></span>

4. <span data-ttu-id="0a586-269">No Olá **adicionar credencial** caixa de diálogo, introduza um nome e uma descrição para a nova credencial do Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-269">In hello **Add Credential** dialog box, enter a name and a description for hello new credential.</span></span> <span data-ttu-id="0a586-270">Em seguida, especifique Olá nome de utilizador e palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="0a586-270">Then specify hello username and password.</span></span> <span data-ttu-id="0a586-271">nome de Olá, *Contoso Vcenter credencial* é utilizado credencial de Olá tooidentify no procedimento seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-271">hello name, *Contoso Vcenter credential* is used tooidentify hello credential in hello next procedure.</span></span> <span data-ttu-id="0a586-272">Utilize Olá mesmo nome de utilizador e palavra-passe que é utilizado para Olá vCenter Server.</span><span class="sxs-lookup"><span data-stu-id="0a586-272">Use hello same username and password that is used for hello vCenter Server.</span></span> <span data-ttu-id="0a586-273">Se Olá vCenter Server e o servidor de cópia de segurança do Azure não estiverem em Olá mesmo domínio, no **nome de utilizador**, especifique o domínio de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-273">If hello vCenter Server and Azure Backup Server are not in hello same domain, in **User name**, specify hello domain.</span></span>

    ![Caixa de diálogo Adicionar credencial do servidor de cópia de segurança do Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    <span data-ttu-id="0a586-275">Clique em **adicionar** tooadd Olá tooAzure de credencial novo servidor de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0a586-275">Click **Add** tooadd hello new credential tooAzure Backup Server.</span></span> <span data-ttu-id="0a586-276">nova credencial do Olá aparece na lista de Olá no Olá **gerir credenciais** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-276">hello new credential appears in hello list in hello **Manage Credentials** dialog box.</span></span>
    
    ![Caixa de diálogo Gerir credenciais do servidor de cópia de segurança do Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. <span data-ttu-id="0a586-278">Olá tooclose **gerir credenciais** caixa de diálogo, clique em Olá **X** no canto superior direito de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-278">tooclose hello **Manage Credentials** dialog box, click hello **X** in hello upper-right corner.</span></span>


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a><span data-ttu-id="0a586-279">Adicionar Olá vCenter Server tooAzure cópia de segurança do servidor</span><span class="sxs-lookup"><span data-stu-id="0a586-279">Add hello vCenter Server tooAzure Backup Server</span></span>

<span data-ttu-id="0a586-280">Assistente de adição do servidor de produção é utilizado tooadd Olá vCenter Server tooAzure servidor de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0a586-280">Production Server Addition Wizard is used tooadd hello vCenter Server tooAzure Backup Server.</span></span>

<span data-ttu-id="0a586-281">tooopen Assistente de adição de servidor de produção, Olá concluída seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="0a586-281">tooopen Production Server Addition Wizard, complete hello following procedure:</span></span>

1. <span data-ttu-id="0a586-282">Na consola do servidor de cópia de segurança do Azure Olá, clique em **gestão**, clique em **servidores de produção**e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0a586-282">In hello Azure Backup Server console, click **Management**, click **Production Servers**, and then click **Add**.</span></span>

    ![Assistente de adição do servidor de produção aberta](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    <span data-ttu-id="0a586-284">Olá **Assistente de adição do servidor de produção** é apresentada a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0a586-284">hello **Production Server Addition Wizard** dialog box appears.</span></span>

    ![Assistente de adição do servidor de produção](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. <span data-ttu-id="0a586-286">No Olá **tipo selecionar servidor de produção** página, selecione **servidores VMware**e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-286">On hello **Select Production Server type** page, select **VMware Servers**, and then click **Next**.</span></span>

3. <span data-ttu-id="0a586-287">No **servidor nome/endereço IP**, especifique o nome de domínio completamente qualificado (FQDN) do Olá ou endereço IP do servidor do VMware Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-287">In **Server Name/IP Address**, specify hello fully qualified domain name (FQDN) or IP address of hello VMware server.</span></span> <span data-ttu-id="0a586-288">Se todos os servidores de ESXi Olá são geridos pelo Olá mesmo vCenter, pode utilizar Olá vCenter nome.</span><span class="sxs-lookup"><span data-stu-id="0a586-288">If all hello ESXi servers are managed by hello same vCenter, you can use hello vCenter name.</span></span>

    ![Especifique o endereço IP ou FQDN do servidor de VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. <span data-ttu-id="0a586-290">No **porta SSL**, introduza a porta de Olá que é utilizado toocommunicate com o servidor do VMware Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-290">In **SSL Port**, enter hello port that is used toocommunicate with hello VMware server.</span></span> <span data-ttu-id="0a586-291">Utilize a porta 443, que é a porta predefinida de Olá, a menos que saiba que é necessária uma porta diferente.</span><span class="sxs-lookup"><span data-stu-id="0a586-291">Use port 443, which is hello default port, unless you know that a different port is required.</span></span>

5. <span data-ttu-id="0a586-292">No **especificar credenciais**, selecione Olá credenciais que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0a586-292">In **Specify Credential**, select hello credential that you created earlier.</span></span>

    ![Especificar credenciais](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. <span data-ttu-id="0a586-294">Clique em **adicionar** lista do tooadd Olá VMware server toohello de **adicionados servidores do VMware**e, em seguida, clique em **seguinte** toomove toohello página seguinte no Assistente de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-294">Click **Add** tooadd hello VMware server toohello list of **Added VMware Servers**, and then click **Next** toomove toohello next page in hello wizard.</span></span>

    ![Adicionar servidor VMWare e credenciais](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. <span data-ttu-id="0a586-296">No Olá **resumo** página, clique em **adicionar** tooadd Olá especificado VMware tooAzure de servidor servidor de cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0a586-296">In hello **Summary** page, click **Add** tooadd hello specified VMware server tooAzure Backup Server.</span></span>

    ![Adicionar VMware tooAzure de servidor servidor de cópia de segurança](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  <span data-ttu-id="0a586-298">cópia de segurança do Olá VMware server é uma cópia de segurança sem agente e é adicionado no novo servidor de Olá a imediatamente.</span><span class="sxs-lookup"><span data-stu-id="0a586-298">hello VMware server backup is an agentless backup, and hello new server is added immediately.</span></span> <span data-ttu-id="0a586-299">Olá **concluir** página mostra Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="0a586-299">hello **Finish** page shows you hello results.</span></span>

  ![Página de conclusão](./media/backup-azure-backup-server-vmware/summary-screen.png)

  <span data-ttu-id="0a586-301">tooadd várias instâncias do vCenter Server tooAzure servidor de cópia de segurança, repita Olá anterior passos nesta secção.</span><span class="sxs-lookup"><span data-stu-id="0a586-301">tooadd multiple instances of vCenter Server tooAzure Backup Server, repeat hello previous steps in this section.</span></span>

<span data-ttu-id="0a586-302">Depois de adicionar Olá vCenter Server tooAzure servidor de cópia de segurança, o passo seguinte Olá é toocreate um grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="0a586-302">After you add hello vCenter Server tooAzure Backup Server, hello next step is toocreate a protection group.</span></span> <span data-ttu-id="0a586-303">grupo de proteção de Olá Especifica Olá vários detalhes para a retenção de curto ou longo prazo e é onde definir e aplicar a política de cópia de segurança de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-303">hello protection group specifies hello various details for short or long-term retention, and it is where you define and apply hello backup policy.</span></span> <span data-ttu-id="0a586-304">política de cópia de segurança de Olá é agenda Olá quando ocorrem as cópias de segurança e o que é uma cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="0a586-304">hello backup policy is hello schedule for when backups occur, and what is backed up.</span></span>


## <a name="configure-a-protection-group"></a><span data-ttu-id="0a586-305">Configurar um grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="0a586-305">Configure a protection group</span></span>

<span data-ttu-id="0a586-306">Se não tiver utilizado o System Center Data Protection Manager ou o servidor de cópia de segurança do Azure antes, consulte o artigo [planear para cópias de segurança de disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare o ambiente do hardware.</span><span class="sxs-lookup"><span data-stu-id="0a586-306">If you have not used System Center Data Protection Manager or Azure Backup Server before, see [Plan for disk backups](https://technet.microsoft.com/library/hh758026.aspx) tooprepare your hardware environment.</span></span> <span data-ttu-id="0a586-307">Depois, verifique se tem o armazenamento adequado, utilize Olá criar novo grupo de proteção assistente tooadd as máquinas virtuais VMware.</span><span class="sxs-lookup"><span data-stu-id="0a586-307">After you check that you have proper storage, use hello Create New Protection Group wizard tooadd VMware virtual machines.</span></span>

1. <span data-ttu-id="0a586-308">Na consola do servidor de cópia de segurança do Azure Olá, clique em **proteção**e no Friso de ferramentas Olá, clique em **novo** Assistente de criação de novo grupo de proteção de Olá tooopen.</span><span class="sxs-lookup"><span data-stu-id="0a586-308">In hello Azure Backup Server console, click **Protection**, and in hello tool ribbon, click **New** tooopen hello Create New Protection Group wizard.</span></span>

    ![Assistente Criar novo grupo de proteção de Olá aberta](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    <span data-ttu-id="0a586-310">Olá **criar novo grupo de proteção** é apresentada a caixa de diálogo do assistente.</span><span class="sxs-lookup"><span data-stu-id="0a586-310">hello **Create New Protection Group** wizard dialog box appears.</span></span>

    ![Caixa de diálogo Assistente Criar novo grupo de proteção](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    <span data-ttu-id="0a586-312">Clique em **seguinte** tooadvance toohello **selecionar tipo de grupo de proteção** página.</span><span class="sxs-lookup"><span data-stu-id="0a586-312">Click **Next** tooadvance toohello **Select protection group type** page.</span></span>

2. <span data-ttu-id="0a586-313">No Olá **tipo de grupo de proteção selecione** página, selecione **servidores** e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-313">On hello **Select Protection group type** page, select **Servers** and then click **Next**.</span></span> <span data-ttu-id="0a586-314">Olá **selecionar membros do grupo** é apresentada a página.</span><span class="sxs-lookup"><span data-stu-id="0a586-314">hello **Select group members** page appears.</span></span>

3. <span data-ttu-id="0a586-315">No Olá **selecionar membros do grupo** página, membros disponíveis Olá e membros de Olá selecionado são apresentados.</span><span class="sxs-lookup"><span data-stu-id="0a586-315">On hello **Select group members** page, hello available members and hello selected members appear.</span></span> <span data-ttu-id="0a586-316">Selecionar Membros do Olá que pretende tooprotect e, em seguida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-316">Select hello members that you want tooprotect, and then click **Next**.</span></span>

    ![Selecionar Membros do grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    <span data-ttu-id="0a586-318">Quando seleciona um membro, se selecionar uma pasta que contém outros pastas ou VMs, essas pastas e VMs também são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="0a586-318">When you select a member, if you select a folder that contains other folders or VMs, those folders and VMs are also selected.</span></span> <span data-ttu-id="0a586-319">inclusão de Olá de pastas de Olá e VMs na pasta de principal de Olá denomina-se proteção ao nível da pasta.</span><span class="sxs-lookup"><span data-stu-id="0a586-319">hello inclusion of hello folders and VMs in hello parent folder is called folder-level protection.</span></span> <span data-ttu-id="0a586-320">tooremove uma pasta ou VM, desmarque Olá caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="0a586-320">tooremove a folder or VM, clear hello check box.</span></span>

    <span data-ttu-id="0a586-321">Se uma VM ou uma pasta que contenha uma VM, já se encontra protegido tooAzure, não é possível selecionar essa VM novamente.</span><span class="sxs-lookup"><span data-stu-id="0a586-321">If a VM, or a folder containing a VM, is already protected tooAzure, you cannot select that VM again.</span></span> <span data-ttu-id="0a586-322">Ou seja, depois de uma VM tooAzure protegida, não pode ser protegido novamente, que impede que o pontos de recuperação duplicados a ser criada para uma VM.</span><span class="sxs-lookup"><span data-stu-id="0a586-322">That is, after a VM is protected tooAzure, it cannot be protected again, which prevents duplicate recovery points from being created for one VM.</span></span> <span data-ttu-id="0a586-323">Se quiser toosee que instância de servidor de cópia de segurança do Azure já protege um membro, ponto toohello toosee Olá o nome de membro de Olá proteger o servidor.</span><span class="sxs-lookup"><span data-stu-id="0a586-323">If you want toosee which Azure Backup Server instance already protects a member, point toohello member toosee hello name of hello protecting server.</span></span>

4. <span data-ttu-id="0a586-324">No Olá **selecionar método de proteção de dados** página, introduza um nome para o grupo de proteção de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-324">On hello **Select Data Protection Method** page, enter a name for hello protection group.</span></span> <span data-ttu-id="0a586-325">Proteção de curta duração (toodisk) e a proteção online são selecionados.</span><span class="sxs-lookup"><span data-stu-id="0a586-325">Short-term protection (toodisk) and online protection are selected.</span></span> <span data-ttu-id="0a586-326">Se quiser toouse proteção online (tooAzure), tem de utilizar toodisk curta duração de proteção.</span><span class="sxs-lookup"><span data-stu-id="0a586-326">If you want toouse online protection (tooAzure), you must use short-term protection toodisk.</span></span> <span data-ttu-id="0a586-327">Clique em **seguinte** intervalo de proteção de curto prazo do tooproceed toohello.</span><span class="sxs-lookup"><span data-stu-id="0a586-327">Click **Next** tooproceed toohello short-term protection range.</span></span>

    ![Selecione o método de proteção de dados](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. <span data-ttu-id="0a586-329">No Olá **especificar objetivos a curto prazo** página, para **período de retenção**, especifique Olá número de dias que pretende que os pontos de recuperação tooretain estão *armazenados toodisk*.</span><span class="sxs-lookup"><span data-stu-id="0a586-329">On hello **Specify Short-Term Goals** page, for **Retention Range**, specify hello number of days that you want tooretain recovery points that are *stored toodisk*.</span></span> <span data-ttu-id="0a586-330">Se pretender que o tempo de Olá toochange e dias quando são criados os pontos de recuperação, clique em **modificar**.</span><span class="sxs-lookup"><span data-stu-id="0a586-330">If you want toochange hello time and days when recovery points are taken, click **Modify**.</span></span> <span data-ttu-id="0a586-331">pontos de recuperação de curto prazo Olá são cópias de segurança completas.</span><span class="sxs-lookup"><span data-stu-id="0a586-331">hello short-term recovery points are full backups.</span></span> <span data-ttu-id="0a586-332">Não são cópias de segurança incrementais.</span><span class="sxs-lookup"><span data-stu-id="0a586-332">They are not incremental backups.</span></span> <span data-ttu-id="0a586-333">Quando estiver satisfeito com objetivos a curto prazo Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-333">When you are satisfied with hello short-term goals, click **Next**.</span></span>

    ![Especificar objetivos a curto prazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. <span data-ttu-id="0a586-335">No Olá **rever alocação do disco** página, reveja e se necessário, modifique o espaço em disco de Olá para Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="0a586-335">On hello **Review Disk Allocation** page, review and if necessary, modify hello disk space for hello VMs.</span></span> <span data-ttu-id="0a586-336">Olá recomendado alocações de disco baseiam-se no período de retenção de Olá especificado no Olá **especificar objetivos a curto prazo** página, tipo de Olá da carga de trabalho e o tamanho de Olá de Olá protegidos dados (identificados no passo 3).</span><span class="sxs-lookup"><span data-stu-id="0a586-336">hello recommended disk allocations are based on hello retention range that is specified in hello **Specify Short-Term Goals** page, hello type of workload, and hello size of hello protected data (identified in step 3).</span></span>  

  - <span data-ttu-id="0a586-337">**Tamanho dos dados:** tamanho dos dados de Olá Olá grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="0a586-337">**Data size:** Size of hello data in hello protection group.</span></span>
  - <span data-ttu-id="0a586-338">**Espaço em disco:** Olá recomendado a quantidade de espaço em disco para o grupo de proteção de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-338">**Disk space:** hello recommended amount of disk space for hello protection group.</span></span> <span data-ttu-id="0a586-339">Se quiser toomodify esta definição, deve alocar espaço total ligeiramente superior à quantidade de Olá que estimar o que crescimentos de cada origem de dados.</span><span class="sxs-lookup"><span data-stu-id="0a586-339">If you want toomodify this setting, you should allocate total space that is slightly larger than hello amount that you estimate each data source grows.</span></span>
  - <span data-ttu-id="0a586-340">**Colocalizar dados:** se ativar a colocalização, várias origens de dados na proteção de Olá podem mapear tooa única réplica e o volume de pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="0a586-340">**Colocate data:** If you turn on colocation, multiple data sources in hello protection can map tooa single replica and recovery point volume.</span></span> <span data-ttu-id="0a586-341">A colocalização não é suportada para todas as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0a586-341">Colocation isn't supported for all workloads.</span></span>
  - <span data-ttu-id="0a586-342">**Aumente automaticamente:** se ativar esta definição, se os dados no grupo de Olá protegido superarem alocação inicial Olá, System Center Data Protection Manager tenta tamanho do disco tooincrease Olá por 25 por cento.</span><span class="sxs-lookup"><span data-stu-id="0a586-342">**Automatically grow:** If you turn on this setting, if data in hello protected group outgrows hello initial allocation, System Center Data Protection Manager tries tooincrease hello disk size by 25 percent.</span></span>
  - <span data-ttu-id="0a586-343">**Detalhes do agrupamento de armazenamento:** mostra o estado de Olá Olá do agrupamento de armazenamento, incluindo total e o tamanho de disco restante.</span><span class="sxs-lookup"><span data-stu-id="0a586-343">**Storage pool details:** Shows hello status of hello storage pool, including total and remaining disk size.</span></span>

    ![Rever alocação do disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    <span data-ttu-id="0a586-345">Quando estiver satisfeito com alocação de espaço de Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-345">When you are satisfied with hello space allocation, click **Next**.</span></span>

7. <span data-ttu-id="0a586-346">No Olá **escolher método de criação de réplica** página, especifique como pretende que a cópia inicial do toogenerate hello, ou a réplica, dos dados de Olá protegida no servidor de cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-346">On hello **Choose Replica Creation Method** page, specify how you want toogenerate hello initial copy, or replica, of hello protected data on Azure Backup Server.</span></span>

    <span data-ttu-id="0a586-347">predefinição de Olá é **automaticamente através da rede Olá** e **agora**.</span><span class="sxs-lookup"><span data-stu-id="0a586-347">hello default is **Automatically over hello network** and **Now**.</span></span> <span data-ttu-id="0a586-348">Se utilizar a predefinição de Olá, recomendamos que especifique uma hora de ponta.</span><span class="sxs-lookup"><span data-stu-id="0a586-348">If you use hello default, we recommend that you specify an off-peak time.</span></span> <span data-ttu-id="0a586-349">Escolha **mais tarde** e especifique um dia e hora.</span><span class="sxs-lookup"><span data-stu-id="0a586-349">Choose **Later** and specify a day and time.</span></span>

    <span data-ttu-id="0a586-350">Para grandes quantidades de dados ou menos-a-ideal nas condições da rede, considere replicar dados Olá offline utilizando suportes de dados amovível.</span><span class="sxs-lookup"><span data-stu-id="0a586-350">For large amounts of data or less-than-optimal network conditions, consider replicating hello data offline by using removable media.</span></span>

    <span data-ttu-id="0a586-351">Depois de efetuar as suas opções, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-351">After you have made your choices, click **Next**.</span></span>

    ![Escolher método de criação de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. <span data-ttu-id="0a586-353">No Olá **opções de verificação de consistência** página, selecione como e quando verifica a consistência de Olá tooautomate.</span><span class="sxs-lookup"><span data-stu-id="0a586-353">On hello **Consistency Check Options** page, select how and when tooautomate hello consistency checks.</span></span> <span data-ttu-id="0a586-354">Pode executar verificações de consistência quando os dados de réplica se tornar inconsistentes ou numa agenda definida.</span><span class="sxs-lookup"><span data-stu-id="0a586-354">You can run consistency checks when replica data becomes inconsistent, or on a set schedule.</span></span>

    <span data-ttu-id="0a586-355">Se não quiser tooconfigure verificações de consistência automática, pode executar uma verificação manual.</span><span class="sxs-lookup"><span data-stu-id="0a586-355">If you don't want tooconfigure automatic consistency checks, you can run a manual check.</span></span> <span data-ttu-id="0a586-356">Na área de proteção de Olá da consola do servidor de cópia de segurança do Azure Olá, clique no grupo de proteção de Olá e, em seguida, selecione **efetuar verificação de consistência**.</span><span class="sxs-lookup"><span data-stu-id="0a586-356">In hello protection area of hello Azure Backup Server console, right-click hello protection group and then select **Perform Consistency Check**.</span></span>

    <span data-ttu-id="0a586-357">Clique em **seguinte** toomove toohello seguinte página.</span><span class="sxs-lookup"><span data-stu-id="0a586-357">Click **Next** toomove toohello next page.</span></span>

9. <span data-ttu-id="0a586-358">No Olá **especificar dados da proteção Online** página, selecione um ou mais origens de dados que pretende que o tooprotect.</span><span class="sxs-lookup"><span data-stu-id="0a586-358">On hello **Specify Online Protection Data** page, select one or more data sources that you want tooprotect.</span></span> <span data-ttu-id="0a586-359">Pode selecionar membros do Olá individualmente ou clique em **Selecionar tudo** toochoose todos os membros.</span><span class="sxs-lookup"><span data-stu-id="0a586-359">You can select hello members individually, or click **Select All** toochoose all members.</span></span> <span data-ttu-id="0a586-360">Após escolher membros Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-360">After you choose hello members, click **Next**.</span></span>

    ![Especificar dados da proteção online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. <span data-ttu-id="0a586-362">No Olá **Especificar agenda de cópia de segurança Online** página, especificar agenda de Olá toogenerate pontos de recuperação de cópia de segurança de disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-362">On hello **Specify Online Backup Schedule** page, specify hello schedule toogenerate recovery points from hello disk backup.</span></span> <span data-ttu-id="0a586-363">Depois do ponto de recuperação Olá é gerado, é toohello transferidos Cofre de serviços de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-363">After hello recovery point is generated, it is transferred toohello Recovery Services vault in Azure.</span></span> <span data-ttu-id="0a586-364">Quando estiver satisfeito com a agenda de cópia de segurança online Olá, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-364">When you are satisfied with hello online backup schedule, click **Next**.</span></span>

    ![Especifique a agenda de cópia de segurança online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. <span data-ttu-id="0a586-366">No Olá **especificar política de retenção Online** página, indique o tempo durante o qual pretende que os dados de cópia de segurança Olá tooretain no Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-366">On hello **Specify Online Retention Policy** page, indicate how long you want tooretain hello backup data in Azure.</span></span> <span data-ttu-id="0a586-367">Depois de política de Olá estiver definida, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="0a586-367">After hello policy is defined, click **Next**.</span></span>

    ![Especificar a política de retenção online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    <span data-ttu-id="0a586-369">Não há nenhum limite de tempo para o período de tempo pode manter os dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="0a586-369">There is no time limit for how long you can keep data in Azure.</span></span> <span data-ttu-id="0a586-370">Quando armazena os dados de ponto de recuperação no Azure, hello apenas limite é que não pode ter mais do que 9999 pontos de recuperação por instância protegido.</span><span class="sxs-lookup"><span data-stu-id="0a586-370">When you store recovery point data in Azure, hello only limit is that you cannot have more than 9999 recovery points per protected instance.</span></span> <span data-ttu-id="0a586-371">Neste exemplo, instância protegido Olá é o servidor do VMware Olá.</span><span class="sxs-lookup"><span data-stu-id="0a586-371">In this example, hello protected instance is hello VMware server.</span></span>

12. <span data-ttu-id="0a586-372">No Olá **resumo** página, reveja os detalhes de Olá para os membros do grupo de proteção e as definições e, em seguida, clique em **criar grupo**.</span><span class="sxs-lookup"><span data-stu-id="0a586-372">On hello **Summary** page, review hello details for your protection group members and settings, and then click **Create Group**.</span></span>

    ![Membro do grupo de proteção e o resumo da definição](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a><span data-ttu-id="0a586-374">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0a586-374">Next steps</span></span>
<span data-ttu-id="0a586-375">Se utilizar cargas de trabalho do servidor de cópia de segurança do Azure tooprotect VMware, poderá estar interessado em utilizar o servidor de cópia de segurança do Azure toohelp proteger um [do Microsoft Exchange server](./backup-azure-exchange-mabs.md), um [farm do SharePoint do Microsoft](./backup-azure-backup-sharepoint-mabs.md), ou um [Base de dados do SQL Server](./backup-azure-sql-mabs.md).</span><span class="sxs-lookup"><span data-stu-id="0a586-375">If you use Azure Backup Server tooprotect VMware workloads, you may be interested in using Azure Backup Server toohelp protect a [Microsoft Exchange server](./backup-azure-exchange-mabs.md), a [Microsoft SharePoint farm](./backup-azure-backup-sharepoint-mabs.md), or a [SQL Server database](./backup-azure-sql-mabs.md).</span></span>

<span data-ttu-id="0a586-376">Para informações sobre problemas com a registar o agente de Olá, configurar o grupo de proteção de Olá, ou cópia de segurança das tarefas, consulte [resolver problemas do servidor de cópia de segurança do Azure](./backup-azure-mabs-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="0a586-376">For information on problems with registering hello agent, configuring hello protection group, or backing up jobs, see [Troubleshoot Azure Backup Server](./backup-azure-mabs-troubleshoot.md).</span></span>
