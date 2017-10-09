---
title: "aaaEnabling acesso remoto para implementações do Azure no Eclipse"
description: "Saiba como tooenable acesso remoto-para implementações do Azure utilizando Olá Toolkit do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="dd267-103">Ativar o acesso remoto para implementações do Azure no Eclipse</span><span class="sxs-lookup"><span data-stu-id="dd267-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="dd267-104">as implementações de resolução de problemas do toohelp, pode ativar e utilizar a máquina virtual acesso remoto tooconnect toohello a implementação de alojamento.</span><span class="sxs-lookup"><span data-stu-id="dd267-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="dd267-105">Olá funcionalidade do acesso remoto depende Olá protocolo RDP (Remote Desktop Protocol).</span><span class="sxs-lookup"><span data-stu-id="dd267-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="dd267-106">Pode configurar o acesso remoto para a sua implementação depois de ter publicado-tooAzure ou, se estiver a utilizar Eclipse com um sistema operativo Windows, pode configurar o acesso remoto antes de publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dd267-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="dd267-107">Tenha em atenção de que precisa de um cliente de ambiente de trabalho remoto que é compatível com o sistema operativo na máquina de virtual da implementação de ordem, tooconnect tooyour no Azure.</span><span class="sxs-lookup"><span data-stu-id="dd267-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="dd267-108">Como tooenable acesso remoto antes de implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="dd267-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="dd267-109">Acesso remoto antes de implementar a aplicação tooAzure tooenable, terá de toobe Eclipse a ser executado no Windows.</span><span class="sxs-lookup"><span data-stu-id="dd267-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="dd267-110">Olá imagem seguinte mostra Olá **acesso remoto** caixa de diálogo Propriedades utilizado tooenable de acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="dd267-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="dd267-111">Existem dois Olá de toodisplay formas **acesso remoto** caixa de diálogo de propriedades:</span><span class="sxs-lookup"><span data-stu-id="dd267-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="dd267-112">Clique em Olá **avançadas** ligação no Olá **acesso remoto** secção Olá **publicar tooAzure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dd267-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="dd267-113">Abra Olá **propriedades** caixa de diálogo do seu projeto do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd267-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="dd267-114">Quando cria um novo projeto de implementação do Azure, o projeto de Olá não terá acesso remoto ativado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="dd267-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="dd267-115">No entanto, facilmente pode ativar o acesso remoto, especificando o nome de utilizador Olá e a palavra-passe na Olá **publicar tooAzure** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dd267-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="dd267-116">palavra-passe de acesso remoto de Olá é encriptada utilizando certificados x. 509.</span><span class="sxs-lookup"><span data-stu-id="dd267-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="dd267-117">Se não utilizar os seus próprios certificados de fornecer encriptação Olá depende de um certificado autoassinado vem incluído no Olá Plug-in do Azure para o Eclipse.</span><span class="sxs-lookup"><span data-stu-id="dd267-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="dd267-118">Este certificado autoassinado consta Olá **cert** pasta do projeto do Azure, armazenados ambos como um ficheiro de certificado pública (SampleRemoteAccessPublic.cer) e como um PFX Personal Information Exchange () (ficheiro de certificado SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="dd267-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="dd267-119">Olá última contém a chave privada do Olá certificado Olá e tem uma palavra-passe para a predefinição **Password1**.</span><span class="sxs-lookup"><span data-stu-id="dd267-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="dd267-120">No entanto, uma vez que esta palavra-passe conhecimento público, certificado de predefinido Olá deve ser utilizado apenas para efeitos de aprendizagem, não para uma implementação de produção.</span><span class="sxs-lookup"><span data-stu-id="dd267-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="dd267-121">Por isso, diferente para efeitos de aprendizagem, quando quiser tooenabled sessões remotas para as implementações, deverá clicar Olá **avançadas** ligação no Olá **publicar tooAzure** toospecify de caixa de diálogo os seus próprios certificado.</span><span class="sxs-lookup"><span data-stu-id="dd267-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="dd267-122">Tenha em atenção que precisará tooupload Olá PFX versão do serviço de tooyour alojado certificado Olá dentro Olá Portal de gestão do Azure, pelo que esse Azure pode desencriptar a palavra-passe de utilizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd267-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="dd267-123">resto Olá tutorial Olá mostra-lhe como tooenable acesso remoto-para um projeto de implementação do Azure que foi criado inicialmente com acesso remoto desativado.</span><span class="sxs-lookup"><span data-stu-id="dd267-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="dd267-124">Para efeitos deste tutorial, vamos criar um novo certificado autoassinado e o ficheiro. pfx terão uma palavra-passe à sua escolha.</span><span class="sxs-lookup"><span data-stu-id="dd267-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="dd267-125">Tem também a opção de Olá de utilizar um certificado emitido por uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="dd267-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="dd267-126">Como tooenable acesso remoto depois de ter implementado tooAzure</span><span class="sxs-lookup"><span data-stu-id="dd267-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="dd267-127">tooenable acesso remoto depois de ter implementado tooAzure, Olá utilize os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="dd267-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="dd267-128">Inicie sessão no portal de gestão do Azure Olá utilizando a sua conta do Azure</span><span class="sxs-lookup"><span data-stu-id="dd267-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="dd267-129">Na lista de **serviços em nuvem**, selecione o seu serviço de nuvem implementado</span><span class="sxs-lookup"><span data-stu-id="dd267-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="dd267-130">Na página de web do serviço de nuvem do Olá, clique em Olá **configurar** ligação</span><span class="sxs-lookup"><span data-stu-id="dd267-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="dd267-131">Olá parte inferior da página de configuração de Olá, clique em Olá **remoto** ligação</span><span class="sxs-lookup"><span data-stu-id="dd267-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="dd267-132">Quando é apresentada a caixa de diálogo de pop-up Olá:</span><span class="sxs-lookup"><span data-stu-id="dd267-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="dd267-133">Especifique Olá função que para os quais pretende que o acesso remoto tooenable</span><span class="sxs-lookup"><span data-stu-id="dd267-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="dd267-134">Clique em tooselect Olá **ativar o ambiente de trabalho remoto** caixa de verificação</span><span class="sxs-lookup"><span data-stu-id="dd267-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="dd267-135">Especifique um nome de utilizador e palavra-passe que pretende toouse para acesso remoto</span><span class="sxs-lookup"><span data-stu-id="dd267-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="dd267-136">Selecione Olá toouse de certificado</span><span class="sxs-lookup"><span data-stu-id="dd267-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="dd267-137">Clique em **OK**</span><span class="sxs-lookup"><span data-stu-id="dd267-137">Click **OK**</span></span> 

<span data-ttu-id="dd267-138">Verá uma mensagem a indicar que a sua alteração de configuração está em curso, o que pode demorar alguns minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dd267-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="dd267-139">Após a alteração da configuração Olá foi concluída, siga os passos de Olá Olá **toolog no remotamente** secção neste artigo.</span><span class="sxs-lookup"><span data-stu-id="dd267-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="dd267-140">Como tooenable acesso remoto no seu pacote</span><span class="sxs-lookup"><span data-stu-id="dd267-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="dd267-141">No painel do Explorador de projeto do Eclipse, clique no projeto do Azure e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="dd267-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="dd267-142">No Olá **propriedades** caixa de diálogo, expanda **Azure** no painel da esquerda Olá e clique em **acesso remoto**.</span><span class="sxs-lookup"><span data-stu-id="dd267-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="dd267-143">No Olá **acesso remoto** caixa de diálogo, certifique-se **ativar todas as funções tooaccept ligações de ambiente de trabalho remoto com estas credenciais de início de sessão** está marcada.</span><span class="sxs-lookup"><span data-stu-id="dd267-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="dd267-144">Especifique um nome de utilizador para Olá ligação de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="dd267-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="dd267-145">Especifique e confirme Olá palavra-passe do utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="dd267-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="dd267-146">Olá utilizador nome e palavra-passe valores definidos nesta caixa de diálogo serão utilizados quando efetuar uma ligação de ambiente de trabalho remoto.</span><span class="sxs-lookup"><span data-stu-id="dd267-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="dd267-147">(Tenha em atenção de que se trata de uma palavra-passe separada da sua palavra-passe PFX.)</span><span class="sxs-lookup"><span data-stu-id="dd267-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="dd267-148">Especifique a data de expiração de Olá Olá conta de utilizador.</span><span class="sxs-lookup"><span data-stu-id="dd267-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="dd267-149">Clique em **novo** toocreate um novo certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="dd267-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="dd267-150">(Em alternativa, pode selecionar um certificado do sistema de ficheiro ou a área de trabalho através de Olá **área de trabalho** ou **FileSystem** botões, respetivamente, mas para efeitos deste tutorial, vamos criar um novo certificado.)</span><span class="sxs-lookup"><span data-stu-id="dd267-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="dd267-151">No Olá **novo certificado** caixa de diálogo, especifique e confirme a palavra-passe de Olá irá utilizar para o ficheiro PFX.</span><span class="sxs-lookup"><span data-stu-id="dd267-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="dd267-152">Aceite o valor de Olá fornecido para **nome (CN)**, ou utilizar um nome personalizado.</span><span class="sxs-lookup"><span data-stu-id="dd267-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="dd267-153">Especifique o nome de ficheiro e caminho do olá onde Olá novo certificado, no formato. cer, será guardado.</span><span class="sxs-lookup"><span data-stu-id="dd267-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="dd267-154">Para este passo e o passo seguinte Olá, pode utilizar Olá **cert** pasta do projeto do Azure, mas estiver livre toochoose noutra localização.</span><span class="sxs-lookup"><span data-stu-id="dd267-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="dd267-155">Para efeitos deste tutorial, iremos utilizar **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="dd267-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="dd267-156">(Criar Olá **c:\mycert** tooproceeding anterior da pasta ou utilize uma pasta existente, se assim o desejar.)</span><span class="sxs-lookup"><span data-stu-id="dd267-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="dd267-157">Especifique o nome de ficheiro e caminho do olá onde Step-by-Olá novo certificado e a respetiva chave privada, no formato. pfx, serão guardados.</span><span class="sxs-lookup"><span data-stu-id="dd267-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="dd267-158">Para efeitos deste tutorial, iremos utilizar **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="dd267-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="dd267-159">O **novo certificado** diálogo deverá ter um aspeto semelhante toohello seguinte (atualizar os caminhos de pastas de Olá se não utilizou **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="dd267-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="dd267-160">Clique em **OK** tooclose Olá **novo certificado** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dd267-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="dd267-161">O **acesso remoto** diálogo deverá ter um aspeto semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="dd267-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="dd267-162">Clique em **OK** tooclose Olá **acesso remoto** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="dd267-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="dd267-163">Reconstruir a aplicação, com Olá criar conjunto toocloud de implementação.</span><span class="sxs-lookup"><span data-stu-id="dd267-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="dd267-164">toolog no remotamente</span><span class="sxs-lookup"><span data-stu-id="dd267-164">toolog in remotely</span></span>
<span data-ttu-id="dd267-165">Assim que a instância de função estiver pronta, pode remotamente iniciar sessão na máquina virtual toohello que está a alojar a aplicação.</span><span class="sxs-lookup"><span data-stu-id="dd267-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="dd267-166">Se estiver a utilizar Eclipse no Windows e Olá selecionado **implementar de ambiente de trabalho remoto do início no** opção durante a implementação tooAzure, será apresentada com um ecrã de início de sessão de ligação de ambiente de trabalho remoto quando a implementação é iniciado.</span><span class="sxs-lookup"><span data-stu-id="dd267-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="dd267-167">Quando lhe for pedido Olá nome de utilizador e palavra-passe, introduza valores Olá que especificou para o utilizador remoto Olá e será capaz de toolog no.</span><span class="sxs-lookup"><span data-stu-id="dd267-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="dd267-168">Outra forma toolog no remotamente é efetuada através de Olá <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span><span class="sxs-lookup"><span data-stu-id="dd267-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="dd267-169">Dentro do Olá **serviços em nuvem** vista de Olá portal de gestão do Azure, clique o seu serviço em nuvem, clique em **instâncias**, clique uma instância específica e, em seguida, clique em Olá **Connect**botão.</span><span class="sxs-lookup"><span data-stu-id="dd267-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="dd267-170">Olá **Connect** botão aparece como seguinte Olá na barra de comando Olá:</span><span class="sxs-lookup"><span data-stu-id="dd267-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="dd267-171">Depois de clicar em Olá **Connect** botão, será pedido tooopen um ficheiro RDP.</span><span class="sxs-lookup"><span data-stu-id="dd267-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="dd267-172">Abra o ficheiro Olá e siga as instruções de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd267-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="dd267-173">(Foi também guardar este computador local do ficheiro tooyour e, em seguida, execute Olá ficheiro ao fazer duplo clique tooremote registo no tooyour máquina virtual sem necessitar de toofirst aceda portal de gestão de Olá.)</span><span class="sxs-lookup"><span data-stu-id="dd267-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="dd267-174">Quando lhe for pedido Olá nome de utilizador e palavra-passe, introduza valores Olá que especificou para o utilizador remoto Olá e será capaz de toolog no.</span><span class="sxs-lookup"><span data-stu-id="dd267-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="dd267-175">Se estiver num sistema operativo Windows não, é necessário toouse um cliente de ambiente de trabalho remoto que é compatível com o sistema operativo e siga Olá passos tooconfigure que o cliente com definições de Olá no ficheiro RDP Olá que transferiu.</span><span class="sxs-lookup"><span data-stu-id="dd267-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="dd267-176">Veja Também</span><span class="sxs-lookup"><span data-stu-id="dd267-176">See Also</span></span>
<span data-ttu-id="dd267-177">[Toolkit do Azure do Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dd267-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="dd267-178">[Criar uma aplicação do Olá mundo do Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dd267-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="dd267-179">[Instalar Olá Toolkit de Azure do Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dd267-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="dd267-180">Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="dd267-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
