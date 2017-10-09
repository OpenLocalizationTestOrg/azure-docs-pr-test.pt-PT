---
title: "aaaPublish um contentor de Docker utilizando Olá Toolkit do Azure para o IntelliJ | Microsoft Docs"
description: "Saiba como toopublish um tooMicrosoft de aplicação web do Azure como um contentor de Docker utilizando Olá Toolkit do Azure para o IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="ec784-103">Publicar uma aplicação web como um contentor de Docker utilizando Olá Toolkit do Azure para o IntelliJ</span><span class="sxs-lookup"><span data-stu-id="ec784-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="ec784-104">Os contentores de docker são um método amplamente utilizado para implementar aplicações web.</span><span class="sxs-lookup"><span data-stu-id="ec784-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="ec784-105">Ao utilizar os contentores de Docker, os programadores podem consolidar todos os respetivos ficheiros de projeto e dependências para um único pacote para o servidor de tooa de implementação.</span><span class="sxs-lookup"><span data-stu-id="ec784-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="ec784-106">Olá Toolkit do Azure para o IntelliJ simplifica este processo para programadores de Java adicionando *publicar como contentor de Docker* funcionalidades para tooMicrosoft de implementação do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec784-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="ec784-107">Este artigo explica Olá passos necessários toopublish sua tooAzure aplicações como contentores de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="ec784-108">Obter mais informações sobre o Docker estão disponíveis no Olá [Web site do Docker].</span><span class="sxs-lookup"><span data-stu-id="ec784-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="ec784-109">Publicar o seu tooAzure de aplicação web utilizando um contentor de Docker</span><span class="sxs-lookup"><span data-stu-id="ec784-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="ec784-110">toopublish aplicação web, tem de criar um artefacto pronta para a implementação.</span><span class="sxs-lookup"><span data-stu-id="ec784-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="ec784-111">toolearn mais, consulte Olá [informações adicionais sobre a criação de artefactos](#artifacts) secção.</span><span class="sxs-lookup"><span data-stu-id="ec784-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="ec784-112">Depois de concluir o Assistente de implementação de Olá, pelo menos, uma vez, a maioria das definições de é utilizada como predefinições quando executar o Assistente de Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="ec784-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="ec784-113">Abra o projeto de aplicação web in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ec784-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="ec784-114">Olá toostart **publicar como contentor de Docker** assistente, efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="ec784-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="ec784-115">No Olá **projeto** ferramenta janela, clique no seu projeto, clique em **Azure**e, em seguida, clique em **publicar como contentor de Docker**:</span><span class="sxs-lookup"><span data-stu-id="ec784-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Olá publicar como comando de contentor do Docker][PUB01]

   * <span data-ttu-id="ec784-117">Na barra de ferramentas de IntelliJ Olá, clique em Olá **publicar grupo** botão e, em seguida, clique em **publicar como contentor de Docker**:</span><span class="sxs-lookup"><span data-stu-id="ec784-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="ec784-118">![Olá publicar como comando de contentor do Docker][PUB02]</span><span class="sxs-lookup"><span data-stu-id="ec784-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="ec784-119">Olá **contentor de Docker implementar no Azure** é aberto o assistente.</span><span class="sxs-lookup"><span data-stu-id="ec784-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Olá implementar o contentor de Docker no Assistente do Azure][PUB03]

3. <span data-ttu-id="ec784-121">No Olá **escreva um nome de imagem, selecione o caminho do artefacto Olá e verificar um toobe de anfitriões de Docker utilizado** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec784-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="ec784-122">a.</span><span class="sxs-lookup"><span data-stu-id="ec784-122">a.</span></span> <span data-ttu-id="ec784-123">No Olá **nome de imagem de Docker** box, introduza um nome exclusivo para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="ec784-124">(o Assistente de Olá cria automaticamente um nome, mas pode modificá-la.)</span><span class="sxs-lookup"><span data-stu-id="ec784-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="ec784-125">b.</span><span class="sxs-lookup"><span data-stu-id="ec784-125">b.</span></span> <span data-ttu-id="ec784-126">Olá **anfitriões** área apresenta quaisquer anfitriões de Docker que já tenha criado.</span><span class="sxs-lookup"><span data-stu-id="ec784-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="ec784-127">Efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="ec784-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="ec784-128">Se tiver um anfitrião de Docker existente, pode implementar a sua tooit de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="ec784-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="ec784-129">toocreate um anfitrião de Docker, clique em verde Olá sinal de adição (**+**).</span><span class="sxs-lookup"><span data-stu-id="ec784-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="ec784-130">Olá **criar anfitriões de Docker** é aberta a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ec784-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Implementar o contentor de Docker no Assistente do Azure][PUB04a]

4. <span data-ttu-id="ec784-132">No Olá **configurar a máquina virtual nova do Olá** janela, fornecer Olá seguintes informações sobre o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="ec784-133">(o Assistente de Olá gera automaticamente a maioria das informações Olá, mas pode modificar qualquer uma delas).</span><span class="sxs-lookup"><span data-stu-id="ec784-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="ec784-134">a.</span><span class="sxs-lookup"><span data-stu-id="ec784-134">a.</span></span> <span data-ttu-id="ec784-135">No Olá **nome** box, introduza um nome exclusivo para o anfitrião de Docker Olá.</span><span class="sxs-lookup"><span data-stu-id="ec784-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="ec784-136">(É não Olá igual ao hello do nome de imagem de Docker que especificou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="ec784-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="ec784-137">b.</span><span class="sxs-lookup"><span data-stu-id="ec784-137">b.</span></span> <span data-ttu-id="ec784-138">No Olá **subscrição** box, introduza Olá subscrição do Azure que utiliza para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="ec784-139">c.</span><span class="sxs-lookup"><span data-stu-id="ec784-139">c.</span></span> <span data-ttu-id="ec784-140">No Olá **região** box, introduza a região geográfica olá onde está localizado o seu anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="ec784-141">d.</span><span class="sxs-lookup"><span data-stu-id="ec784-141">d.</span></span> <span data-ttu-id="ec784-142">No Olá **SO e tamanho** separador, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec784-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="ec784-143">**SO do anfitrião**: introduza o sistema de operativo Olá para a máquina virtual Olá que contém o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="ec784-144">**Tamanho**: introduza o tamanho de máquina virtual de Olá para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="ec784-145">e.</span><span class="sxs-lookup"><span data-stu-id="ec784-145">e.</span></span> <span data-ttu-id="ec784-146">No Olá **grupo de recursos** separador, selecione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ec784-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="ec784-147">**Novo grupo de recursos**: criar um grupo de recursos para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="ec784-148">**Grupo de recursos existente**: Especifique um grupo de recursos existentes da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec784-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="ec784-149">f.</span><span class="sxs-lookup"><span data-stu-id="ec784-149">f.</span></span> <span data-ttu-id="ec784-150">No Olá **rede** separador, selecione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ec784-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="ec784-151">**Nova rede virtual**: criar uma rede virtual para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="ec784-152">**Rede virtual existente**: Especifique uma rede virtual existente da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec784-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="ec784-153">g.</span><span class="sxs-lookup"><span data-stu-id="ec784-153">g.</span></span> <span data-ttu-id="ec784-154">No Olá **armazenamento** separador, selecione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ec784-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="ec784-155">**Nova conta do storage**: criar uma conta de armazenamento para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="ec784-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="ec784-156">**Conta de armazenamento existente**: Especifique uma conta de armazenamento existentes da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec784-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="ec784-157">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="ec784-157">Click **Next**.</span></span>  
     <span data-ttu-id="ec784-158">Olá **configurar registo de credenciais e definições de porta** é aberta a janela.</span><span class="sxs-lookup"><span data-stu-id="ec784-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![Olá configurar início de sessão credenciais e a janela de definições de porta][PUB05]

6. <span data-ttu-id="ec784-160">Selecione uma das seguintes opções de Olá:</span><span class="sxs-lookup"><span data-stu-id="ec784-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="ec784-161">**Importar as credenciais do Cofre de chaves do Azure**: Especifique um conjunto de credenciais que são armazenados na sua subscrição do Azure guardado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ec784-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="ec784-162">Não é automaticamente acessível por outra conta ou principal de serviço que partilha subscrição Olá um cofre de chaves do Azure que é criado com uma conta específica ou um principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="ec784-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="ec784-163">tooallow outra conta ou serviço principal toouse Olá chave de cofre, tem de utilizar Olá conta de Olá tooadd portal do Azure ou principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="ec784-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="ec784-164">**Novo registo credenciais**: criar um novo conjunto de credenciais de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="ec784-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="ec784-165">Se selecionar esta opção, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec784-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="ec784-166">a.</span><span class="sxs-lookup"><span data-stu-id="ec784-166">a.</span></span> <span data-ttu-id="ec784-167">No Olá **VM credenciais** separador, forneça Olá seguindo as informações de credenciais de início de sessão de máquina virtual de Olá de anfitrião do Docker: * **Username**: introduza o nome de utilizador Olá para o início de sessão de máquina virtual credenciais.</span><span class="sxs-lookup"><span data-stu-id="ec784-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="ec784-168">* **Palavra-passe** e **confirmar**: introduza a palavra-passe de Olá as suas credenciais de início de sessão de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ec784-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="ec784-169">* **SSH**: introduza Olá as definições de Secure Shell (SSH) para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="ec784-170">Pode selecionar uma das seguintes opções de Olá: * **nenhum**: Especifica que a máquina virtual não permite ligações SSH.</span><span class="sxs-lookup"><span data-stu-id="ec784-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="ec784-171">* **Gerar automaticamente**: cria automaticamente Olá definições requisitos para ligar através de SSH.</span><span class="sxs-lookup"><span data-stu-id="ec784-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="ec784-172">* **Importar do directory**: permite-lhe toospecify um diretório que contém um conjunto de definições de SSH guardados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ec784-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="ec784-173">diretório de Olá tem de conter Olá seguintes dois ficheiros:</span><span class="sxs-lookup"><span data-stu-id="ec784-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="ec784-174">b.</span><span class="sxs-lookup"><span data-stu-id="ec784-174">b.</span></span> <span data-ttu-id="ec784-175">No Olá **Docker Daemon acesso** separador, forneça Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="ec784-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Criar anfitrião Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="ec784-177">Depois de introduzir informações de Olá necessário, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ec784-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="ec784-178">Olá **contentor de Docker implementar no Azure** reappears do assistente.</span><span class="sxs-lookup"><span data-stu-id="ec784-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Implementar o contentor de Docker no Assistente do Azure][PUB07]

8. <span data-ttu-id="ec784-180">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="ec784-180">Click **Next**.</span></span>  
    <span data-ttu-id="ec784-181">Olá **configurar toobe de contentor de Docker Olá criado** é aberta a janela.</span><span class="sxs-lookup"><span data-stu-id="ec784-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![janela de toobe criado de contentor de Docker Olá configurar Olá][PUB08]

9. <span data-ttu-id="ec784-183">No Olá **configurar toobe de contentor de Docker Olá criado** janela, fornecer Olá seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="ec784-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="ec784-184">a.</span><span class="sxs-lookup"><span data-stu-id="ec784-184">a.</span></span> <span data-ttu-id="ec784-185">No Olá **nome do contentor de Docker** box, introduza um nome exclusivo para o contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="ec784-186">b.</span><span class="sxs-lookup"><span data-stu-id="ec784-186">b.</span></span> <span data-ttu-id="ec784-187">Escolha uma das seguintes imagens de Docker de Olá:</span><span class="sxs-lookup"><span data-stu-id="ec784-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="ec784-188">**Imagem predefinida do Docker**: Especifique uma imagem de Docker pré-existentes a partir do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec784-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="ec784-189">lista de Olá das imagens de Docker nesta caixa é composta por várias imagens que Olá Toolkit do Azure tiver sido configurado toopatch para que o artefacto é automaticamente implementado.</span><span class="sxs-lookup"><span data-stu-id="ec784-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="ec784-190">**Dockerfile personalizado**: especificar um Dockerfile guardado anteriormente a partir do seu computador local.</span><span class="sxs-lookup"><span data-stu-id="ec784-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="ec784-191">Esta é uma funcionalidade mais avançada para programadores que pretendem toodeploy os seus próprios Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="ec784-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="ec784-192">No entanto, está a funcionar toodevelopers que utilizam este tooensure opção que os respetivos Dockerfile baseia-se corretamente.</span><span class="sxs-lookup"><span data-stu-id="ec784-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="ec784-193">Porque Olá Toolkit do Azure não validar conteúdo Olá um Dockerfile personalizado, implementação de Olá poderá falhar se Olá Dockerfile tem problemas.</span><span class="sxs-lookup"><span data-stu-id="ec784-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="ec784-194">Além disso, porque Olá Azure Toolkit espera Olá personalizado Dockerfile toocontain um artefacto de aplicação web, este tenta tooopen uma ligação HTTP.</span><span class="sxs-lookup"><span data-stu-id="ec784-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="ec784-195">Se os programadores publicar um tipo diferente de artefactos, estes poderão receber erros innocuous após a implementação.</span><span class="sxs-lookup"><span data-stu-id="ec784-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="ec784-196">c.</span><span class="sxs-lookup"><span data-stu-id="ec784-196">c.</span></span> <span data-ttu-id="ec784-197">No Olá **definições de porta** box, introduza Olá TCP porta enlace exclusivo para o contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="ec784-198">Depois de concluir Olá precedente passos, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="ec784-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="ec784-199">Olá, Azure Toolkit começa a implementar a sua tooAzure de aplicação web num contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="ec784-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="ec784-200">A menos que configurou toobe IntelliJ implementado em segundo plano de Olá, um **implementar tooAzure** barra de progresso é apresentado.</span><span class="sxs-lookup"><span data-stu-id="ec784-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![barra de progresso da implementação Olá][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="ec784-202">Informações adicionais sobre a criação de artefactos</span><span class="sxs-lookup"><span data-stu-id="ec784-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="ec784-203">toocreate um artefacto pronta para a implementação, Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="ec784-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="ec784-204">Abra o projeto de aplicação web in IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ec784-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="ec784-205">Clique em **ficheiro**e, em seguida, clique em **estrutura do projeto**.</span><span class="sxs-lookup"><span data-stu-id="ec784-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Olá comandos de estrutura do projeto][ART01]

3. <span data-ttu-id="ec784-207">tooadd um artefacto, clique em verde Olá sinal de adição (**+**) e, em seguida, clique em **aplicação Web: arquivo**.</span><span class="sxs-lookup"><span data-stu-id="ec784-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Olá comando "Arquivo de: de aplicação Web"][ART02]

4. <span data-ttu-id="ec784-209">No Olá **nome** box, introduza um nome para o artefacto (não incluem Olá *.war* extensão) e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec784-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![caixa de nome de artefacto Olá][ART03]

<span data-ttu-id="ec784-211">Para obter mais informações sobre a criação de artefactos no IntelliJ, consulte [configurar artefactos] no Web site de JetBrains Olá.</span><span class="sxs-lookup"><span data-stu-id="ec784-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec784-212">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ec784-212">Next steps</span></span>
<span data-ttu-id="ec784-213">Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="ec784-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="ec784-214">[Toolkit do Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec784-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ec784-215">[Novidades no Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec784-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ec784-216">[Instalar Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec784-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ec784-217">[Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec784-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ec784-218">[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ec784-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="ec784-219">[Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ec784-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ec784-220">[Novidades no Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ec784-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ec784-221">[Instalar Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ec784-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ec784-222">[Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ec784-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ec784-223">[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ec784-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="ec784-224">Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure] e Olá [ferramentas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ec784-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="ec784-225">Para obter recursos adicionais para Docker, consulte oficial Olá [Web site do Docker].</span><span class="sxs-lookup"><span data-stu-id="ec784-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Toolkit do Azure do Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Instalar Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalar Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Olá Toolkit de Azure do Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/
[ferramentas de Java para Visual Studio Team Services]: https://java.visualstudio.com/

[Web site do Docker]: https://www.docker.com/
[configurar artefactos]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
