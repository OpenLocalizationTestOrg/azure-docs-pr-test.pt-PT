---
title: "aaaEncrypt uma Máquina Virtual do Azure | Microsoft Docs"
description: "Este documento ajuda-o a tooencrypt uma Máquina Virtual do Azure depois de receber um alerta a partir do Centro de segurança do Azure."
services: security, security-center
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: 
ms.assetid: f6c28bc4-1f79-4352-89d0-03659b2fa2f5
ms.service: security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/15/2017
ms.author: tomsh
ms.openlocfilehash: 7c7c6eed39d16bde8a0dfaffe3a3331c58101634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-an-azure-virtual-machine"></a>Encriptar uma Máquina Virtual do Azure
O Centro de Segurança do Azure alerta-o se tiver máquinas virtuais que não estão encriptadas. Estes alertas serão apresentados como de elevada gravidade e Olá recomendação é tooencrypt estas máquinas virtuais.

![Recomendação de encriptação de disco](./media/security-center-disk-encryption/security-center-disk-encryption-fig1.png)

> [!NOTE]
> informações de Olá neste documento aplicam-se máquinas de virtuais tooencrypting sem utilizar uma chave de encriptação de chaves (que é necessário para efetuar cópia de segurança de máquinas virtuais utilizando cópia de segurança do Azure). Consulte o artigo de Olá [encriptação de disco do Azure para Windows e Linux Azure Virtual Machines](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) para obter informações sobre como toouse toosupport uma chave de encriptação de chave cópia de segurança do Azure para encriptados máquinas virtuais do Azure.
>
>

tooencrypt máquinas de virtuais do Azure que tenham sido identificadas pelo centro de segurança do Azure como tendo necessidade de encriptação, recomendamos que Olá os seguintes passos:

* Instalar e configurar o Azure PowerShell. Isto permitirá toorun Olá PowerShell comandos necessário tooset segurança Olá pré-requisitos necessários tooencrypt Virtual Machines do Azure.
* Obter e executar scripts de pré-requisitos do Azure PowerShell do Azure disco encriptação Olá
* Encriptar as suas máquinas virtuais

Olá objetivo deste documento é tooenable tooencrypt as máquinas virtuais, mesmo se tiver pouco ou nenhum em segundo plano no Azure PowerShell.
Este documento parte do princípio de que está a utilizar o Windows 10 como máquina do cliente Olá partir do qual irá configurar o Azure Disk Encryption.

Existem várias abordagens que podem ser utilizados toosetup Olá pré-requisitos e tooconfigure encriptação para máquinas virtuais do Azure. Se já estiver bem familiarizado com o Azure PowerShell ou a CLI do Azure, em seguida, poderá preferir abordagens alternativas toouse.

> [!NOTE]
> toolearn mais informações sobre a encriptação de tooconfiguring abordagens alternativas para máquinas virtuais do Azure, consulte [encriptação de disco do Azure para Windows e Linux Azure Virtual Machines](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).
>
>

## <a name="install-and-configure-azure-powershell"></a>Instalar e configurar o Azure PowerShell
Precisa da versão 1.2.1 ou superior do Azure PowerShell instalada no seu computador. artigo de Olá [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) contém todos os passos de Olá terá tooprovision toowork o computador com o Azure PowerShell. abordagem mais simples de Olá é a abordagem instalação toouse Olá instalador de plataforma Web mencionada nesse artigo. Mesmo que já tenha instalado Azure PowerShell, instalar novamente utilizando a abordagem de instalador de plataforma Web Olá, de modo a que tem a versão mais recente do Olá do Azure PowerShell.

## <a name="obtain-and-run-hello-azure-disk-encryption-prerequisites-configuration-script"></a>Obter e executar um script de configuração de pré-requisitos de encriptação do Olá disco do Azure
Olá Script de configuração de pré-requisitos do Azure Disk Encryption irá configurar todos os pré-requisitos de Olá necessários para encriptar as suas máquinas virtuais do Azure.

1. Página do GitHub toohello aceda que tenha Olá [Script de configuração do Azure Disk Encryption pré-requisitos](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
2. Na página do GibHub Olá, clique em Olá **Raw** botão.
3. Utilizar **CTRL-A** tooselect todos os Olá texto na página Olá e, em seguida, utilizar **CTRL-C** toocopy todas Olá texto na área de transferência do Olá página toohello.
4. Abra **bloco de notas** e cole o texto de Olá copiado no bloco de notas.
5. Crie uma nova pasta na sua unidade C: com o nome **AzureADEScript**.
6. Guarde o ficheiro de bloco de notas Olá – clique em **ficheiro**, em seguida, clique em **guardar como**. Na caixa de texto do nome do ficheiro de Olá, introduza **"ADEPrereqScript.ps1"** e clique em **guardar**. (Certifique-se de que coloca as aspas de Olá à volta de nome de Olá, caso contrário, irá guardar ficheiro Olá com uma extensão de ficheiro. txt).

Agora que o conteúdo do script Olá é guardado, abra o script Olá Olá ISE do PowerShell:

1. No Menu Iniciar Olá, clique em **Cortana**. Peça **Cortana** "PowerShell" escrevendo **PowerShell** na caixa de texto de pesquisa do Olá Cortana.
2. Clique com o botão direito do rato em **ISE do Windows PowerShell** e clique em **Executar como administrador**.
3. No Olá **administrador: ISE do Windows PowerShell** janela, clique em **vista** e, em seguida, clique em **Mostrar painel de Script**.
4. Se vir Olá **comandos** painel no lado direito de Olá da janela de Olá, clique em Olá **"x"** no Olá canto superior direito do Olá painel tooclose-lo. Se o texto de Olá é demasiado pequeno para toosee, utilize **CTRL + adicionar** ("Adicionar" é Olá "+" iniciar sessão). Se o texto de Olá é demasiado grande, utilize **CTRL + subtrair** (subtrair é Olá "-" início de sessão).
5. Clique em **Ficheiro** e, em seguida, clique em **Abrir**. Navegue toohello **C:\AzureADEScript** pasta e Olá faça duplo clique no Olá **ADEPrereqScript**.
6. Olá **ADEPrereqScript** conteúdo deverá agora aparecer na Olá ISE do PowerShell e é codificado por cores toohelp pode ver mais facilmente diversos componentes, tais como comandos, parâmetros e variáveis.

Deverá ver algo semelhante Olá figura abaixo.

![Janela ISE do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig2.png)

painel superior Olá é referenciado tooas Olá "painel de script" e painel inferior de Olá é referenciado tooas Olá "consola". Utilizaremos estes termos posteriormente neste artigo.

## <a name="run-hello-azure-disk-encryption-prerequisites-powershell-command"></a>Executar o comando de PowerShell de pré-requisitos de encriptação de disco do Azure de Olá
Olá script de pré-requisitos de encriptação de disco do Azure irá pedir-lhe Olá seguintes informações depois de iniciar o script de Olá:

* **Nome do grupo de recursos** - nome de Olá grupo de recursos que pretende que o tooput Olá Cofre de chaves.  Será criado um novo grupo de recursos com o nome de Olá que introduziu se não existe não estiver já um com esse nome criado. Se já tiver um grupo de recursos que pretende que o toouse nesta subscrição, em seguida, introduza o nome de Olá desse grupo de recursos.
* **Nome do Cofre de chave** -nome do Cofre de chaves de Olá no qual encriptação chaves são toobe colocado. Será criado um novo Cofre de Chaves com este nome se ainda não tiver um Cofre de Chaves com este nome. Se já tiver um cofre de chaves que pretende que o toouse, introduza o nome de Olá de Olá existente Cofre de chaves.
* **Localização** -localização do Olá Cofre de chaves. Certifique-se Olá o Cofre de chaves e VMs toobe encriptado Olá mesma localização. Se não souber a localização de Olá, existem passos neste artigo que irá mostrar-lhe como toofind enviados.
* **Nome de aplicação do Active Directory do Azure** -nome do Olá aplicação Azure Active Directory que será utilizado toowrite segredos toohello Cofre de chaves. Será criada uma nova aplicação com este nome, caso ainda não exista. Se já tiver uma aplicação do Azure Active Directory que pretende que o toouse, introduza o nome de Olá dessa aplicação do Azure Active Directory.

> [!NOTE]
> Se estiver com curiosidade como toowhy terá toocreate uma aplicação do Azure Active Directory, consulte *registar uma aplicação no Azure Active Directory* secção artigo Olá [introdução ao Cofre de chaves do Azure](../key-vault/key-vault-get-started.md).
>
>

Execute Olá os seguintes passos tooencrypt uma Máquina Virtual do Azure:

1. Se tiver fechado Olá ISE do PowerShell, abra uma instância elevada do Olá ISE do PowerShell. Siga as instruções Olá anteriormente neste artigo se Olá que ISE do PowerShell ainda não estiver aberto. Se tiver fechado o script de Olá, em seguida, abra Olá **ADEPrereqScript.ps1** clicar **ficheiro**, em seguida, **abrir** e selecionando script Olá Olá **c:\ AzureADEScript** pasta. Se seguiu este artigo desde o início de Olá, em seguida, apenas movê-lo no toohello próximo passo.
2. Na consola de Olá de Olá ISE do PowerShell (painel de inferior Olá de Olá ISE do PowerShell), alterar Olá foco toohello local do script Olá escrevendo **cd c:\AzureADEScript** e prima **ENTER**.
3. Definir a política de execução de Olá no seu computador para que possam executar script de Olá. Tipo **Set-ExecutionPolicy Unrestricted** no Olá consola e, em seguida, prima ENTER. Se vir uma caixa de diálogo informar sobre Olá os efeitos das políticas de tooexecution de alteração de Olá, clique em **Sim tooall** ou **Sim** (se vir **Sim tooall**, selecionar essa opção – se não vê **Sim tooall**, em seguida, clique em **Sim**).
4. Inicie sessão na sua conta do Azure. Na consola de Olá, escreva **Login-AzureRmAccount** e prima **ENTER**. Apresentada uma caixa de diálogo na qual introduz as suas credenciais (Certifique-se de que tem direitos toochange Olá máquinas virtuais – se não tiver direitos, não será capaz de tooencrypt-los. Se não tiver a certeza, pergunte ao proprietário ou administrador da subscrição). Deverá ver informações sobre o seu **Ambiente**, **Conta**, **TenantId**, **SubscriptionId** e **CurrentStorageAccount**. Olá cópia **SubscriptionId** tooNotepad. Irá precisar toouse no passo #6.
5. Localizar a máquina virtual a que subscrição pertence tooand respetiva localização. Aceda demasiado[https://portal.azure.com](ttps://portal.azure.com) e iniciar sessão.  Olá à esquerda do lado da página Olá, clique em **máquinas virtuais**. Irá ver uma lista das suas máquinas virtuais e subscrições Olá a que pertencem.

   ![Virtual Machines](./media/security-center-disk-encryption/security-center-disk-encryption-fig3.png)
6. Devolva toohello ISE do PowerShell. Definir o contexto de subscrição de Olá na qual Olá script será executado. Na consola de Olá, escreva **Select-AzureRmSubscription – SubscriptionId < your_subscription_Id >** (substituir **< your_subscription_Id >** com o seu ID de subscrição real) e prima  **INTRODUZA**. Deverá ver informações sobre Olá ambiente, **conta**, **TenantId**, **SubscriptionId** e **CurrentStorageAccount**.
7. Agora, está pronto toorun script de Olá. Clique em Olá **executar Script** botão ou prima **F5** no teclado Olá.

   ![Executar Script do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig4.png)
8. script de Olá pede-lhe **resourceGroupName:** -introduza o nome de Olá do *grupo de recursos* pretende toouse, em seguida, prima **ENTER**. Se não tiver uma, introduza um nome que pretende toouse para um novo. Se já tiver um *grupo de recursos* que pretende toouse (por exemplo, Olá um que a máquina virtual está no), introduza o nome de Olá de Olá grupo de recursos existente.
9. script de Olá pede-lhe **keyVaultName:** -introduza o nome de Olá de Olá *Cofre de chaves* pretende toouse, em seguida, prima ENTER. Se não tiver uma, introduza um nome que pretende toouse para um novo. Se já tiver um cofre de chaves que pretende que o toouse, introduza o nome de Olá do Olá existente *Cofre de chaves*.
10. script de Olá pede-lhe **localização:** - introduza Olá nome de localização de Olá em que Olá VM pretende tooencrypt se encontra, em seguida, prima **ENTER**. Se não se lembra da localização de Olá, volte toostep #5.
11. script de Olá pede-lhe **aadAppName:** -introduza o nome de Olá de Olá *do Azure Active Directory* aplicação que pretende toouse, em seguida, prima **ENTER**. Se não tiver uma, introduza um nome que pretende toouse para um novo. Se já tiver um *aplicação Azure Active Directory* que pretende toouse, introduza o nome de Olá de Olá existente *aplicação Azure Active Directory*.
12. Será apresentada um caixa de diálogo de início de sessão. Indique as suas credenciais (Sim, iniciou sessão uma vez, mas agora é preciso toodo-lo novamente).
13. Olá script é executado e concluído, irá pedir-lhe valores Olá toocopy Olá **aadClientID**, **aadClientSecret**, **diskEncryptionKeyVaultUrl**e **keyVaultResourceId**. Copie cada área de transferência de toohello estes valores e cole-os no bloco de notas.
14. Devolver toohello ISE do PowerShell e coloque o cursor Olá no fim de Olá da última linha de Olá e prima **ENTER**.

saída de Olá do script Olá deve ter um aspeto semelhante Olá ecrã abaixo:

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig5.png)

## <a name="encrypt-hello-azure-virtual-machine"></a>Encriptar Olá máquina virtual do Azure
Está agora pronto tooencrypt a máquina virtual. Se a máquina virtual está localizada na Olá mesmo grupo de recursos como o seu Cofre de chave, pode mover na secção de passos de encriptação toohello. No entanto, se a máquina virtual não está no hello mesmo grupo de recursos como o seu Cofre de chave, terá de seguinte de Olá tooenter na consola de Olá na Olá ISE do PowerShell:

**$resourceGroupName = <’Virtual_Machine_RG’>**

Substitua **< Virtual_Machine_RG >** com o nome de Olá Olá do grupo de recursos no qual as máquinas virtuais estão contidas, rodeado por uma aspa simples. Em seguida, prima **ENTER**.
tooconfirm que Olá correto foi introduzido o nome do grupo de recursos, escreva o seguinte Olá no Olá consola do ISE do PowerShell:

**$resourceGroupName**

Prima **ENTER**. Deverá ver o nome Olá do grupo de recursos que as máquinas virtuais estão localizadas em. Por exemplo:

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig6.png)

### <a name="encryption-steps"></a>Passos de encriptação
Em primeiro lugar, precisa de nome de Olá tootell PowerShell da máquina virtual de Olá pretende tooencrypt. Na consola de Olá, escreva:

**$vmName = <’your_vm_name’>**

Substitua **<'your_vm_name ' >** com o nome de Olá da sua VM (Certifique-se de que o nome de Olá está rodeado por uma aspa simples) e, em seguida, prima **ENTER**.

tooconfirm que Olá correto foi introduzido o nome da VM, escreva:

**$vmName**

Prima **ENTER**. Deverá ver Olá nome da máquina virtual de Olá pretende tooencrypt. Por exemplo:

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig7.png)

Existem dois métodos toorun Olá encriptação comando tooencrypt todas as unidades na máquina virtual de Olá. o método primeiro Olá é Olá tootype seguinte comando na Olá consola do ISE do PowerShell:

~~~
Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
~~~

Depois de escrever este comando, prima **ENTER**.

Olá o segundo método é tooclick no painel de script de Olá (painel superior para o Olá de Olá ISE do PowerShell) e desloque-se para baixo toohello inferior do script Olá. Realce o comando de Olá listado acima e, em seguida, com o botão direito e, em seguida, clique em **executar seleção** ou prima **F8** no teclado Olá.

![ISE do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig8.png)

Independentemente do método Olá utilizar, uma caixa de diálogo será apresentado a informar que irá demorar 10 a 15 minutos para Olá operação toocomplete. Clique em **Sim**.

Enquanto o processo de encriptação de Olá está a decorrer, pode devolver toohello Portal do Azure e ver o estado de Olá da máquina virtual de Olá. Olá à esquerda do lado da página Olá, clique em **máquinas virtuais**, em seguida, no Olá **máquinas virtuais** painel, clique no nome de Olá da máquina virtual de Olá que está a encriptar. No painel de Olá que aparece, verá que Olá **estado** indica que está **atualização**. Isto demonstra que a encriptação está em curso.

![Obter mais detalhes sobre Olá VM](./media/security-center-disk-encryption/security-center-disk-encryption-fig9.png)

Devolva toohello ISE do PowerShell. Quando o script de Olá estiver concluído, verá que é apresentado na figura Olá abaixo.

![Saída do PowerShell](./media/security-center-disk-encryption/security-center-disk-encryption-fig10.png)

toodemonstrate Olá máquina virtual já está encriptada, regresse toohello Portal do Azure e clique em **máquinas virtuais** no Olá à esquerda do lado da página Olá. Clique no nome da máquina virtual de Olá encriptou Olá. No Olá **definições** painel, clique em **discos**.

![Opções de definições](./media/security-center-disk-encryption/security-center-disk-encryption-fig11.png)

No Olá **discos** painel, verá que **encriptação** é **ativado**.

![Propriedades do disco](./media/security-center-disk-encryption/security-center-disk-encryption-fig12.png)

## <a name="next-steps"></a>Passos seguintes
Neste documento, aprendeu como tooencrypt uma Máquina Virtual do Azure. toolearn mais acerca do Centro de segurança do Azure, consulte o artigo seguinte Olá:

* [Monitorização de estado de funcionamento de segurança no Centro de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá estado de funcionamento dos seus recursos do Azure
* [Gestão e de que responde toosecurity alertas no Centro de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e respondeu
* [FAQ do Centro de segurança do Azure](security-center-faq.md) – encontre as perguntas mais frequentes sobre a utilização do serviço de Olá
* [Blogue de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – Encontre mensagens do blogue acerca da segurança e conformidade do Azure
