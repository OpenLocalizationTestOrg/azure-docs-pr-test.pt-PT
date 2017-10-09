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
# <a name="back-up-a-vmware-server-tooazure"></a>Criar cópias de segurança uma tooAzure de servidor do VMware

Este artigo explica como toohelp de servidor de cópia de segurança do Azure tooconfigure proteger cargas de trabalho de servidor de VMware. Este artigo pressupõe que já tiver instalado de servidor do Backup do Azure. Se não tiver instalado de servidor do Backup do Azure, consulte [preparar tooback utilizando o servidor de cópia de segurança do Azure de cargas de trabalho](backup-azure-microsoft-azure-backup.md).

Servidor de cópia de segurança do Azure pode criar cópias de segurança ou ajudar a proteger, versão do servidor vCenter 6.5, 6.0 e 5.5 do VMware.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Criar um servidor vCenter toohello ligação segura

Por predefinição, o servidor de cópia de segurança do Azure comunica com cada servidor vCenter através de um canal HTTPS. tooturn em comunicação segura Olá, recomendamos que instale o certificado de autoridade de certificação de VMware (CA) de Olá no servidor de cópia de segurança do Azure. Se não necessitam de uma comunicação segura e prefere requisito de HTTPS do toodisable Olá, consulte [protocolo de comunicação segura desativar](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate uma ligação segura entre o servidor de cópia de segurança do Azure e Olá vCenter Server, importe o certificado fidedigno do Olá no servidor de cópia de segurança do Azure.

Normalmente, utilizar um browser no Olá servidor de cópia de segurança do Azure machine tooconnect toohello vCenter Server através de Olá vSphere cliente Web. Olá pela primeira vez que é utilizar Olá servidor de cópia de segurança do Azure browser tooconnect toohello vCenter Server, ligação Olá não é segura. Olá imagem a seguir mostra ligação Olá protegida.

![Exemplo de servidor de tooVMware de uma ligação não segura](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix este problema e criar uma ligação segura, transfira Olá fidedigno certificados de AC de raiz.

1. Num browser de Olá no servidor de cópia de segurança do Azure, introduza Olá URL toohello vSphere cliente Web. é apresentada a página de início de sessão do Olá vSphere cliente Web.

    ![vSphere Web cliente](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Na parte inferior de Olá de informações de Olá para os administradores e programadores, localize Olá **transferência os certificados de AC de raiz fidedigna** ligação.

    ![Ligação toodownload Olá fidedigno certificados de AC raiz](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Se não vir a página de início de sessão de cliente Web de vSphere Olá, verifique as definições de proxy do seu browser.

2. Clique em **transferência os certificados de AC de raiz fidedigna**.

    Olá vCenter Server transfere um computador local do ficheiro tooyour. Olá nome do ficheiro é denominado **transferir**. Dependendo do seu browser, receberá uma mensagem a perguntar se tooopen ou guardar o ficheiro de Olá.

    ![Transferir a mensagem quando os certificados são transferidos](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Localização Olá ficheiro tooa no servidor de cópia de segurança do Azure. Quando guardar ficheiro Olá, adicione a extensão de nome de ficheiro do Olá. zip.

    ficheiro de Olá é um ficheiro. zip que contém informações de Olá sobre certificados Olá. Com a extensão. zip de Olá, pode utilizar ferramentas de extração Olá.

4. Clique com botão direito **download.zip**e, em seguida, selecione **extrair todos os** conteúdo de Olá tooextract.

    ficheiro. zip de Olá extrai a respetiva pasta de tooa de conteúdo com o nome **certificados**. São apresentados dois tipos de ficheiros na pasta de certificados de Olá. ficheiro de certificado de raiz de Olá tem uma extensão que comece com uma sequência como.0 e.1 numerada.
    
    ficheiro CRL Olá tem uma extensão que comece com uma sequência como .r0 ou .r1. ficheiro CRL Olá está associado um certificado.

    ![Transferir os ficheiros extraídos localmente ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. No Olá **certificados** pasta, clique no ficheiro de certificado de raiz de Olá e, em seguida, clique em **mudar o nome**.

    ![Mudar o nome do certificado de raiz ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Altere o too.crt de extensão certificado de raiz a Olá. Quando estiver a pedido se tiver a certeza de que pretende toochange extensão de Olá, clique em **Sim** ou **OK**. Caso contrário, alterar função pretendida do ficheiro de Olá. ícone de Olá para ícone tooan de alterações de ficheiros de Olá que representa um certificado de raiz.

6. Clique no certificado de raiz de Olá e no menu de pop-up Olá, selecione **instalar certificado**.

    Olá **Assistente para importar certificados** é apresentada a caixa de diálogo.

7. No Olá **Assistente para importar certificados** caixa de diálogo, selecione **máquina Local** como destino de Olá para Olá certificado e, em seguida, clique em **seguinte** toocontinue.

    ![Opções de destino de armazenamento de certificados ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Se estiver a lhe for perguntado se pretende que o computador de toohello tooallow alterações, clique em **Sim** ou **OK**, alterações de Olá tooall.

8. No Olá **arquivo de certificados** página, selecione **colocar todos os certificados no Olá seguir arquivo**e, em seguida, clique em **procurar** arquivo de certificados de Olá toochoose.

    ![Colocar os certificados num lugar para cima de armazenamento específico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Olá **selecionar arquivo de certificados** é apresentada a caixa de diálogo.

    ![Hierarquia de pastas de armazenamento de certificados](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Selecione **autoridades de certificação de raiz fidedigna** como pasta de destino Olá de Olá certificados e, em seguida, clique em **OK**.

    ![Pasta de destino de certificado](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Olá **autoridades de certificação de raiz fidedigna** pasta foi confirmada como como arquivo de certificados de Olá. Clique em **Seguinte**.

    ![Pasta de arquivo de certificados](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. No Olá **Olá concluir o Assistente de importação de certificados** página, certifique-se de que esse certificado Olá é na pasta pretendido Olá e, em seguida, clique em **concluir**.

    ![Verificar o certificado é na pasta correta Olá](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    É apresentada uma caixa de diálogo, a importação do certificado com êxito de Olá é confirmada.

11. Inicie sessão no toohello vCenter tooconfirm de servidor que a ligação é segura.

  Se importar certificados de Olá não for concluída com êxito e não é possível estabelecer uma ligação segura, consulte a documentação de vSphere de VMware Olá no [obter certificados de servidor](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Se tiver limites segurados na sua organização e não pretende tooturn no Olá protocolo HTTPS, utilize Olá comunicações seguro do procedimento toodisable Olá a seguir.

### <a name="disable-secure-communication-protocol"></a>Desativar o protocolo de comunicação segura

Se a sua organização não requer o protocolo HTTPS de Olá, utilize Olá os seguintes passos toodisable HTTPS. toodisable Olá comportamento predefinido, crie uma chave de registo que ignora o comportamento predefinido de Olá.

1. Copie e cole Olá seguir texto num ficheiro. txt.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Guarde o computador de servidor de cópia de segurança do Azure Olá ficheiro tooyour. Para nome de ficheiro Olá, utilize DisableSecureAuthentication.reg.

3. Faça duplo clique entrada de registo do Olá ficheiro tooactivate Olá.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Criar uma conta de utilizador e função no Olá vCenter Server

No Olá vCenter Server, uma função é um conjunto predefinido de privilégios. Um administrador do servidor vCenter cria funções Olá. tooassign permissões, o administrador de Olá pares contas de utilizador com uma função. tooestablish Olá utilizador necessário credenciais tooback se o computador do servidor do vCenter Olá, criar uma função com privilégios específicos e, em seguida, associar a conta de utilizador Olá com função Olá.

Servidor de cópia de segurança do Azure utiliza um nome de utilizador e palavra-passe tooauthenticate com Olá vCenter Server. Servidor do Backup do Azure utiliza estas credenciais como autenticação para todas as operações de cópia de segurança.

tooadd um função de servidor do vCenter e os respetivos privilégios para um administrador de cópias de segurança:

1. Inicie sessão no toohello vCenter Server e, em seguida, no Olá vCenter Server **navegador** painel, clique em **administração**.

    ![Opção de administração no painel do vCenter Server navegador](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. No **administração** selecione **funções**e, em seguida, no Olá **funções** painel clique Olá adicionar ícone de função (símbolo + Olá).

    ![Adicionar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Olá **criar função** é apresentada a caixa de diálogo.

    ![Criar função](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. No Olá **criar função** Olá caixa de diálogo **nome da função** box, introduza *BackupAdminRole*. nome da função Olá pode ser que quiser, mas deve ser reconhecível para fim da função de Olá.

4. Selecione privilégios Olá para a versão adequada do Olá do vCenter e, em seguida, clique em **OK**. Olá, a tabela seguinte identifica privilégios Olá necessário para o vCenter 6.0 e vCenter 5.5.

  Quando seleciona privilégios Olá, clique em Olá ícone seguintes toohello principal etiqueta tooexpand Olá principal e vista Olá subordinado privilégios. privilégios de máquina virtual do tooselect Olá, terá de toogo vários níveis em Olá principal hierarquia subordinado. Não precisa de tooselect todos os privilégios subordinado dentro de um privilégio principal.

  ![Hierarquia de privilégio principal subordinado](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Depois de clicar em **OK**, nova função de Olá aparece na lista de Olá no painel de funções de Olá.

|Privilégios para o vCenter 6.0| Privilégios para o vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Criar uma conta de utilizador do servidor vCenter e permissões

Depois de configurar função Olá com privilégios, crie uma conta de utilizador. conta de utilizador de Olá tem um nome e uma palavra-passe, fornece credenciais Olá que são utilizadas para autenticação.

1. toocreate uma conta de utilizador, no Olá vCenter Server **navegador** painel, clique em **utilizadores e grupos**.

    ![Opção de utilizadores e grupos](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Olá **vCenter utilizadores e grupos** painel aparece.

    ![Painel de utilizadores e grupos do vCenter](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. No Olá **vCenter utilizadores e grupos** painel, selecione de Olá **utilizadores** separador e, em seguida, clique em Olá adicionar ícone de utilizadores (símbolo + Olá).

    Olá **novo utilizador** é apresentada a caixa de diálogo.

3. No Olá **novo utilizador** diálogo caixa, adicionar informações do utilizador Olá e, em seguida, clique em **OK**. Neste procedimento, o nome de utilizador Olá é BackupAdmin.

    ![Caixa de diálogo do novo utilizador](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    nova conta de utilizador Olá aparece na lista de Olá.

4. conta de utilizador de Olá tooassociate na função Olá, no Olá **navegador** painel, clique em **permissões Global**. No Olá **permissões Global** painel, selecione de Olá **gerir** separador e, em seguida, clique em Olá adicionar ícone (símbolo + Olá).

    ![Painel de permissões global](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Olá **raiz de permissões de Global - adicionar permissão** é apresentada a caixa de diálogo.

5. No Olá **raiz de permissão de Global - adicionar permissão** caixa de diálogo, clique em **adicionar** toochoose Olá utilizador ou grupo.

    ![Escolha o utilizador ou grupo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Olá **selecionar utilizadores/grupos** é apresentada a caixa de diálogo.

6. No Olá **selecionar utilizadores/grupos** diálogo caixa, escolha **BackupAdmin** e, em seguida, clique em **adicionar**.

    No **utilizadores**, Olá *domínio ome de utilizador* formato é utilizado para a conta de utilizador Olá. Se quiser toouse um domínio diferente, selecione de Olá **domínio** lista.

    ![Adicionar utilizador BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Clique em **OK** tooadd Olá selecionado utilizadores toohello **adicionar permissão** caixa de diálogo.

7. Agora que identificou utilizador Olá, atribua a função de toohello Olá utilizador. No **função atribuída**, na Olá na lista pendente, selecione **BackupAdminRole**e, em seguida, clique em **OK**.

    ![Atribuir toorole de utilizador](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  No Olá **gerir** separador Olá **permissões Global** painel, a nova conta de utilizador Olá e a função de Olá associado são apresentados na lista de Olá.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Estabelecer as credenciais do servidor vCenter no servidor de cópia de segurança do Azure

Antes de adicionar Olá VMware server tooAzure servidor de cópia de segurança, instale [atualização 1 para o servidor de cópia de segurança do Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen servidor de cópia de segurança do Azure, faça duplo clique no ícone Olá no ambiente de trabalho do Olá servidor de cópia de segurança do Azure.

    ![Ícone de servidor do Backup do Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Se não é possível localizar o ícone de Olá no ambiente de trabalho Olá, abra o servidor de cópia de segurança do Azure na lista de Olá das aplicações instaladas. nome de aplicação de servidor de cópia de segurança do Azure Olá denomina-se a cópia de segurança do Microsoft Azure.

2. Na consola do servidor de cópia de segurança do Azure Olá, clique em **gestão**, clique em **servidores de produção**e, em seguida, no Friso de ferramentas Olá, clique em **gerir VMware**.

    ![Consola do servidor do Backup do Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Olá **gerir credenciais** é apresentada a caixa de diálogo.

    ![Caixa de diálogo Gerir credenciais do servidor de cópia de segurança do Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. No Olá **gerir credenciais** caixa de diálogo, clique em **adicionar** tooopen Olá **adicionar credencial** caixa de diálogo.

4. No Olá **adicionar credencial** caixa de diálogo, introduza um nome e uma descrição para a nova credencial do Olá. Em seguida, especifique Olá nome de utilizador e palavra-passe. nome de Olá, *Contoso Vcenter credencial* é utilizado credencial de Olá tooidentify no procedimento seguinte Olá. Utilize Olá mesmo nome de utilizador e palavra-passe que é utilizado para Olá vCenter Server. Se Olá vCenter Server e o servidor de cópia de segurança do Azure não estiverem em Olá mesmo domínio, no **nome de utilizador**, especifique o domínio de Olá.

    ![Caixa de diálogo Adicionar credencial do servidor de cópia de segurança do Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Clique em **adicionar** tooadd Olá tooAzure de credencial novo servidor de cópia de segurança. nova credencial do Olá aparece na lista de Olá no Olá **gerir credenciais** caixa de diálogo.
    
    ![Caixa de diálogo Gerir credenciais do servidor de cópia de segurança do Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. Olá tooclose **gerir credenciais** caixa de diálogo, clique em Olá **X** no canto superior direito de Olá.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Adicionar Olá vCenter Server tooAzure cópia de segurança do servidor

Assistente de adição do servidor de produção é utilizado tooadd Olá vCenter Server tooAzure servidor de cópia de segurança.

tooopen Assistente de adição de servidor de produção, Olá concluída seguinte procedimento:

1. Na consola do servidor de cópia de segurança do Azure Olá, clique em **gestão**, clique em **servidores de produção**e, em seguida, clique em **adicionar**.

    ![Assistente de adição do servidor de produção aberta](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Olá **Assistente de adição do servidor de produção** é apresentada a caixa de diálogo.

    ![Assistente de adição do servidor de produção](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. No Olá **tipo selecionar servidor de produção** página, selecione **servidores VMware**e, em seguida, clique em **seguinte**.

3. No **servidor nome/endereço IP**, especifique o nome de domínio completamente qualificado (FQDN) do Olá ou endereço IP do servidor do VMware Olá. Se todos os servidores de ESXi Olá são geridos pelo Olá mesmo vCenter, pode utilizar Olá vCenter nome.

    ![Especifique o endereço IP ou FQDN do servidor de VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. No **porta SSL**, introduza a porta de Olá que é utilizado toocommunicate com o servidor do VMware Olá. Utilize a porta 443, que é a porta predefinida de Olá, a menos que saiba que é necessária uma porta diferente.

5. No **especificar credenciais**, selecione Olá credenciais que criou anteriormente.

    ![Especificar credenciais](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Clique em **adicionar** lista do tooadd Olá VMware server toohello de **adicionados servidores do VMware**e, em seguida, clique em **seguinte** toomove toohello página seguinte no Assistente de Olá.

    ![Adicionar servidor VMWare e credenciais](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. No Olá **resumo** página, clique em **adicionar** tooadd Olá especificado VMware tooAzure de servidor servidor de cópia de segurança.

    ![Adicionar VMware tooAzure de servidor servidor de cópia de segurança](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  cópia de segurança do Olá VMware server é uma cópia de segurança sem agente e é adicionado no novo servidor de Olá a imediatamente. Olá **concluir** página mostra Olá resultados.

  ![Página de conclusão](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd várias instâncias do vCenter Server tooAzure servidor de cópia de segurança, repita Olá anterior passos nesta secção.

Depois de adicionar Olá vCenter Server tooAzure servidor de cópia de segurança, o passo seguinte Olá é toocreate um grupo de proteção. grupo de proteção de Olá Especifica Olá vários detalhes para a retenção de curto ou longo prazo e é onde definir e aplicar a política de cópia de segurança de Olá. política de cópia de segurança de Olá é agenda Olá quando ocorrem as cópias de segurança e o que é uma cópia de segurança.


## <a name="configure-a-protection-group"></a>Configurar um grupo de proteção

Se não tiver utilizado o System Center Data Protection Manager ou o servidor de cópia de segurança do Azure antes, consulte o artigo [planear para cópias de segurança de disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare o ambiente do hardware. Depois, verifique se tem o armazenamento adequado, utilize Olá criar novo grupo de proteção assistente tooadd as máquinas virtuais VMware.

1. Na consola do servidor de cópia de segurança do Azure Olá, clique em **proteção**e no Friso de ferramentas Olá, clique em **novo** Assistente de criação de novo grupo de proteção de Olá tooopen.

    ![Assistente Criar novo grupo de proteção de Olá aberta](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Olá **criar novo grupo de proteção** é apresentada a caixa de diálogo do assistente.

    ![Caixa de diálogo Assistente Criar novo grupo de proteção](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Clique em **seguinte** tooadvance toohello **selecionar tipo de grupo de proteção** página.

2. No Olá **tipo de grupo de proteção selecione** página, selecione **servidores** e, em seguida, clique em **seguinte**. Olá **selecionar membros do grupo** é apresentada a página.

3. No Olá **selecionar membros do grupo** página, membros disponíveis Olá e membros de Olá selecionado são apresentados. Selecionar Membros do Olá que pretende tooprotect e, em seguida, clique em **seguinte**.

    ![Selecionar Membros do grupo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Quando seleciona um membro, se selecionar uma pasta que contém outros pastas ou VMs, essas pastas e VMs também são selecionadas. inclusão de Olá de pastas de Olá e VMs na pasta de principal de Olá denomina-se proteção ao nível da pasta. tooremove uma pasta ou VM, desmarque Olá caixa de verificação.

    Se uma VM ou uma pasta que contenha uma VM, já se encontra protegido tooAzure, não é possível selecionar essa VM novamente. Ou seja, depois de uma VM tooAzure protegida, não pode ser protegido novamente, que impede que o pontos de recuperação duplicados a ser criada para uma VM. Se quiser toosee que instância de servidor de cópia de segurança do Azure já protege um membro, ponto toohello toosee Olá o nome de membro de Olá proteger o servidor.

4. No Olá **selecionar método de proteção de dados** página, introduza um nome para o grupo de proteção de Olá. Proteção de curta duração (toodisk) e a proteção online são selecionados. Se quiser toouse proteção online (tooAzure), tem de utilizar toodisk curta duração de proteção. Clique em **seguinte** intervalo de proteção de curto prazo do tooproceed toohello.

    ![Selecione o método de proteção de dados](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. No Olá **especificar objetivos a curto prazo** página, para **período de retenção**, especifique Olá número de dias que pretende que os pontos de recuperação tooretain estão *armazenados toodisk*. Se pretender que o tempo de Olá toochange e dias quando são criados os pontos de recuperação, clique em **modificar**. pontos de recuperação de curto prazo Olá são cópias de segurança completas. Não são cópias de segurança incrementais. Quando estiver satisfeito com objetivos a curto prazo Olá, clique em **seguinte**.

    ![Especificar objetivos a curto prazo](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. No Olá **rever alocação do disco** página, reveja e se necessário, modifique o espaço em disco de Olá para Olá VMs. Olá recomendado alocações de disco baseiam-se no período de retenção de Olá especificado no Olá **especificar objetivos a curto prazo** página, tipo de Olá da carga de trabalho e o tamanho de Olá de Olá protegidos dados (identificados no passo 3).  

  - **Tamanho dos dados:** tamanho dos dados de Olá Olá grupo de proteção.
  - **Espaço em disco:** Olá recomendado a quantidade de espaço em disco para o grupo de proteção de Olá. Se quiser toomodify esta definição, deve alocar espaço total ligeiramente superior à quantidade de Olá que estimar o que crescimentos de cada origem de dados.
  - **Colocalizar dados:** se ativar a colocalização, várias origens de dados na proteção de Olá podem mapear tooa única réplica e o volume de pontos de recuperação. A colocalização não é suportada para todas as cargas de trabalho.
  - **Aumente automaticamente:** se ativar esta definição, se os dados no grupo de Olá protegido superarem alocação inicial Olá, System Center Data Protection Manager tenta tamanho do disco tooincrease Olá por 25 por cento.
  - **Detalhes do agrupamento de armazenamento:** mostra o estado de Olá Olá do agrupamento de armazenamento, incluindo total e o tamanho de disco restante.

    ![Rever alocação do disco](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Quando estiver satisfeito com alocação de espaço de Olá, clique em **seguinte**.

7. No Olá **escolher método de criação de réplica** página, especifique como pretende que a cópia inicial do toogenerate hello, ou a réplica, dos dados de Olá protegida no servidor de cópia de segurança do Azure.

    predefinição de Olá é **automaticamente através da rede Olá** e **agora**. Se utilizar a predefinição de Olá, recomendamos que especifique uma hora de ponta. Escolha **mais tarde** e especifique um dia e hora.

    Para grandes quantidades de dados ou menos-a-ideal nas condições da rede, considere replicar dados Olá offline utilizando suportes de dados amovível.

    Depois de efetuar as suas opções, clique em **seguinte**.

    ![Escolher método de criação de réplica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. No Olá **opções de verificação de consistência** página, selecione como e quando verifica a consistência de Olá tooautomate. Pode executar verificações de consistência quando os dados de réplica se tornar inconsistentes ou numa agenda definida.

    Se não quiser tooconfigure verificações de consistência automática, pode executar uma verificação manual. Na área de proteção de Olá da consola do servidor de cópia de segurança do Azure Olá, clique no grupo de proteção de Olá e, em seguida, selecione **efetuar verificação de consistência**.

    Clique em **seguinte** toomove toohello seguinte página.

9. No Olá **especificar dados da proteção Online** página, selecione um ou mais origens de dados que pretende que o tooprotect. Pode selecionar membros do Olá individualmente ou clique em **Selecionar tudo** toochoose todos os membros. Após escolher membros Olá, clique em **seguinte**.

    ![Especificar dados da proteção online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. No Olá **Especificar agenda de cópia de segurança Online** página, especificar agenda de Olá toogenerate pontos de recuperação de cópia de segurança de disco de Olá. Depois do ponto de recuperação Olá é gerado, é toohello transferidos Cofre de serviços de recuperação no Azure. Quando estiver satisfeito com a agenda de cópia de segurança online Olá, clique em **seguinte**.

    ![Especifique a agenda de cópia de segurança online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. No Olá **especificar política de retenção Online** página, indique o tempo durante o qual pretende que os dados de cópia de segurança Olá tooretain no Azure. Depois de política de Olá estiver definida, clique em **seguinte**.

    ![Especificar a política de retenção online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Não há nenhum limite de tempo para o período de tempo pode manter os dados no Azure. Quando armazena os dados de ponto de recuperação no Azure, hello apenas limite é que não pode ter mais do que 9999 pontos de recuperação por instância protegido. Neste exemplo, instância protegido Olá é o servidor do VMware Olá.

12. No Olá **resumo** página, reveja os detalhes de Olá para os membros do grupo de proteção e as definições e, em seguida, clique em **criar grupo**.

    ![Membro do grupo de proteção e o resumo da definição](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Passos seguintes
Se utilizar cargas de trabalho do servidor de cópia de segurança do Azure tooprotect VMware, poderá estar interessado em utilizar o servidor de cópia de segurança do Azure toohelp proteger um [do Microsoft Exchange server](./backup-azure-exchange-mabs.md), um [farm do SharePoint do Microsoft](./backup-azure-backup-sharepoint-mabs.md), ou um [Base de dados do SQL Server](./backup-azure-sql-mabs.md).

Para informações sobre problemas com a registar o agente de Olá, configurar o grupo de proteção de Olá, ou cópia de segurança das tarefas, consulte [resolver problemas do servidor de cópia de segurança do Azure](./backup-azure-mabs-troubleshoot.md).
