---
title: "aaaPublish um contentor de Docker utilizando Olá Toolkit do Azure para o Eclipse | Microsoft Docs"
description: "Saiba como toopublish um tooMicrosoft de aplicação web do Azure como um contentor de Docker utilizando Olá Toolkit do Azure para o Eclipse."
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
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="a8067-103">Publicar uma aplicação web como um contentor de Docker utilizando Olá Toolkit do Azure para o Eclipse</span><span class="sxs-lookup"><span data-stu-id="a8067-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="a8067-104">Os contentores de docker são um método amplamente utilizado para implementar aplicações web.</span><span class="sxs-lookup"><span data-stu-id="a8067-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="a8067-105">Ao utilizar os contentores de Docker, os programadores podem consolidar todos os respetivos ficheiros de projeto e dependências para um único pacote para o servidor de tooa de implementação.</span><span class="sxs-lookup"><span data-stu-id="a8067-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="a8067-106">Olá Toolkit do Azure para o Eclipse simplifica este processo para programadores de Java adicionando *publicar como contentor de Docker* funcionalidades para tooMicrosoft de implementação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8067-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="a8067-107">Este artigo explica Olá passos necessários toopublish sua tooAzure aplicações como contentores de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="a8067-108">Obter mais informações sobre o Docker estão disponíveis no Olá [Web site do Docker].</span><span class="sxs-lookup"><span data-stu-id="a8067-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="a8067-109">Publicar o seu tooAzure de aplicação web utilizando um contentor de Docker</span><span class="sxs-lookup"><span data-stu-id="a8067-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="a8067-110">Abra o projeto de aplicação web no Eclipse.</span><span class="sxs-lookup"><span data-stu-id="a8067-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="a8067-111">Olá toostart **publicar como contentor de Docker** assistente, efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="a8067-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="a8067-112">No Olá **navegador** ver, clique no seu projeto, clique em **Azure**e, em seguida, clique em **publicar como contentor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="a8067-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Vista de navegador publicar como comando de contentor do Docker][PUB01]

   * <span data-ttu-id="a8067-114">Na barra de ferramentas do Olá Eclipse, clique em Olá **publicar** botão e, em seguida, clique em **publicar como contentor de Docker**.</span><span class="sxs-lookup"><span data-stu-id="a8067-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Barra de ferramentas do Eclipse publicar como comando de contentor do Docker][PUB02]
      
    <span data-ttu-id="a8067-116">Olá **contentor de Docker implementar no Azure** é aberto o assistente.</span><span class="sxs-lookup"><span data-stu-id="a8067-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Olá implementar o contentor de Docker no Assistente do Azure][PUB03]

3. <span data-ttu-id="a8067-118">No Olá **escreva um nome de imagem, selecione o caminho do artefacto Olá e verificar um toobe de anfitriões de Docker utilizado** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8067-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="a8067-119">a.</span><span class="sxs-lookup"><span data-stu-id="a8067-119">a.</span></span> <span data-ttu-id="a8067-120">No Olá **nome de imagem de Docker** box, introduza um nome exclusivo para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="a8067-121">(o Assistente de Olá cria automaticamente um nome, mas pode modificá-la.)</span><span class="sxs-lookup"><span data-stu-id="a8067-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="a8067-122">b.</span><span class="sxs-lookup"><span data-stu-id="a8067-122">b.</span></span> <span data-ttu-id="a8067-123">Olá **anfitriões** área apresenta quaisquer anfitriões de Docker que já tenha criado.</span><span class="sxs-lookup"><span data-stu-id="a8067-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="a8067-124">Efetue um dos seguintes Olá:</span><span class="sxs-lookup"><span data-stu-id="a8067-124">Do either of hello following:</span></span>

    * <span data-ttu-id="a8067-125">Se tiver um anfitrião de Docker existente, pode implementar a sua tooit de aplicação web.</span><span class="sxs-lookup"><span data-stu-id="a8067-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="a8067-126">Clique em toocreate um novo anfitrião do Docker, **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a8067-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="a8067-127">Olá **criar anfitriões de Docker** é aberta a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a8067-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Implementar o contentor de Docker no Assistente do Azure][PUB04a]

4. <span data-ttu-id="a8067-129">No Olá **configurar a máquina virtual nova do Olá** janela, especifique Olá seguintes opções para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="a8067-130">(o Assistente de Olá gera automaticamente a maior parte das opções de Olá para si, mas pode modificar qualquer uma delas).</span><span class="sxs-lookup"><span data-stu-id="a8067-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="a8067-131">a.</span><span class="sxs-lookup"><span data-stu-id="a8067-131">a.</span></span> <span data-ttu-id="a8067-132">**Nome**: introduza um nome exclusivo para o anfitrião de Docker Olá.</span><span class="sxs-lookup"><span data-stu-id="a8067-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="a8067-133">(É não Olá igual ao hello do nome de imagem de Docker que especificou anteriormente.)</span><span class="sxs-lookup"><span data-stu-id="a8067-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="a8067-134">b.</span><span class="sxs-lookup"><span data-stu-id="a8067-134">b.</span></span> <span data-ttu-id="a8067-135">**Subscrição**: introduza Olá subscrição do Azure que utiliza para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="a8067-136">c.</span><span class="sxs-lookup"><span data-stu-id="a8067-136">c.</span></span> <span data-ttu-id="a8067-137">**Região**: introduza a região geográfica olá onde está localizado o seu anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="a8067-138">d.</span><span class="sxs-lookup"><span data-stu-id="a8067-138">d.</span></span> <span data-ttu-id="a8067-139">No Olá **sistema operativo anfitrião e o tamanho** separador:</span><span class="sxs-lookup"><span data-stu-id="a8067-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="a8067-140">**SO do anfitrião**: introduza o sistema de operativo Olá para a máquina virtual Olá que contém o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="a8067-141">**Tamanho**: introduza o tamanho de máquina virtual de Olá para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="a8067-142">e.</span><span class="sxs-lookup"><span data-stu-id="a8067-142">e.</span></span> <span data-ttu-id="a8067-143">No Olá **grupo de recursos** separador:</span><span class="sxs-lookup"><span data-stu-id="a8067-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="a8067-144">**Novo grupo de recursos**: criar um novo grupo de recursos para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="a8067-145">**Grupo de recursos existente**: introduza um grupo de recursos existentes da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8067-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="a8067-146">f.</span><span class="sxs-lookup"><span data-stu-id="a8067-146">f.</span></span> <span data-ttu-id="a8067-147">No Olá **rede** separador:</span><span class="sxs-lookup"><span data-stu-id="a8067-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="a8067-148">**Nova rede virtual**: criar uma nova rede virtual para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="a8067-149">**Rede virtual existente**: introduza uma rede virtual existente a partir da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8067-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="a8067-150">g.</span><span class="sxs-lookup"><span data-stu-id="a8067-150">g.</span></span> <span data-ttu-id="a8067-151">No Olá **armazenamento** separador:</span><span class="sxs-lookup"><span data-stu-id="a8067-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="a8067-152">**Nova conta do storage**: criar uma nova conta de armazenamento para o anfitrião.</span><span class="sxs-lookup"><span data-stu-id="a8067-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="a8067-153">**Conta de armazenamento existente**: introduza uma conta de armazenamento existentes da sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8067-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="a8067-154">Clique em **Seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a8067-154">Click **Next**.</span></span>

6. <span data-ttu-id="a8067-155">No Olá **configurar registo de credenciais e definições de porta** janela, selecione uma das seguintes opções de Olá:</span><span class="sxs-lookup"><span data-stu-id="a8067-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="a8067-156">**Importar as credenciais do Cofre de chaves do Azure**: Especifica um conjunto de credenciais que são armazenados na sua subscrição do Azure guardado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a8067-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="a8067-157">Não é automaticamente acessível por outra conta ou principal de serviço que partilha subscrição Olá um cofre de chaves do Azure que é criado com uma conta específica ou um principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="a8067-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="a8067-158">tooallow outro toouse conta ou serviço principal Olá Cofre de chaves, tem de utilizar Olá conta de Olá tooadd portal do Azure ou principal de serviço.</span><span class="sxs-lookup"><span data-stu-id="a8067-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="a8067-159">**Novo registo credenciais**: cria um novo conjunto de credenciais de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="a8067-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="a8067-160">Se selecionar esta opção, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8067-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="a8067-161">No Olá **VM credenciais** separador, escolha uma das seguintes Olá opções para credenciais de início de sessão de máquina virtual de Olá do anfitrião do Docker:</span><span class="sxs-lookup"><span data-stu-id="a8067-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="a8067-162">**Nome de utilizador**: introduza o nome de utilizador Olá para as credenciais de início de sessão de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a8067-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="a8067-163">**Palavra-passe** e **confirmar**: introduza a palavra-passe de Olá para as credenciais de início de sessão de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a8067-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="a8067-164">**SSH**: introduza Olá as definições de Secure Shell (SSH) para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="a8067-165">Pode escolher entre Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="a8067-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="a8067-166">**Nenhum**: Especifica que a máquina virtual não irá permitir ligações SSH.</span><span class="sxs-lookup"><span data-stu-id="a8067-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="a8067-167">**Gerar automaticamente**: cria automaticamente Olá definições requisitos para ligar através de SSH.</span><span class="sxs-lookup"><span data-stu-id="a8067-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="a8067-168">**Importar do directory**: Especifica um diretório que contém um conjunto de definições de SSH guardados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a8067-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="a8067-169">diretório de Olá tem de conter Olá seguintes dois ficheiros:</span><span class="sxs-lookup"><span data-stu-id="a8067-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="a8067-170">*id_rsa*: contém a identificação de RSA Olá para um utilizador.</span><span class="sxs-lookup"><span data-stu-id="a8067-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="a8067-171">*id_rsa.pub*: contém Olá RSA chave pública que é utilizado para autenticação.</span><span class="sxs-lookup"><span data-stu-id="a8067-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Criar anfitrião Docker][PUB05]

      * <span data-ttu-id="a8067-173">No Olá **Docker Daemon credenciais** separador, especifique Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="a8067-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="a8067-174">**Porta de Daemon de docker**: introduza a porta TCP exclusiva Olá para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="a8067-175">**Segurança de TLS**: introduza Olá Transport Layer Security definições para o anfitrião de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="a8067-176">Pode escolher entre Olá seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="a8067-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="a8067-177">**Nenhum**: Especifica que a máquina virtual não irá permitir ligações TLS.</span><span class="sxs-lookup"><span data-stu-id="a8067-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="a8067-178">**Gerar automaticamente**: cria automaticamente Olá definições requisitos para ligar através de TLS.</span><span class="sxs-lookup"><span data-stu-id="a8067-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="a8067-179">**Importar do directory**: Especifica um diretório que contém um conjunto de definições de TLS guardados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a8067-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="a8067-180">Mais especificamente, o diretório de Olá tem de conter Olá seis ficheiros a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8067-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="a8067-181">*CA.pem* e *AC key.pem*: contém o certificado de Olá e chave pública para Olá TLS autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="a8067-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="a8067-182">*CERT.pem* e *key.pem*: contém o certificado de cliente de Olá e chave pública que é utilizado para autenticação de TLS.</span><span class="sxs-lookup"><span data-stu-id="a8067-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="a8067-183">*Server.pem* e *servidor key.pem*: contém o certificado de servidor Olá e chave pública para o anfitrião de Olá.</span><span class="sxs-lookup"><span data-stu-id="a8067-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Criar anfitrião Docker][PUB06]

7. <span data-ttu-id="a8067-185">Após introduzir todas Olá precedente informações, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="a8067-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="a8067-186">No Olá **contentor de Docker implementar no Azure** assistente, clique em **seguinte**.</span><span class="sxs-lookup"><span data-stu-id="a8067-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Olá implementar o contentor de Docker no Assistente do Azure][PUB07]

9. <span data-ttu-id="a8067-188">No Olá **configurar toobe de contentor de Docker Olá criado** janela, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8067-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="a8067-189">a.</span><span class="sxs-lookup"><span data-stu-id="a8067-189">a.</span></span> <span data-ttu-id="a8067-190">No Olá **nome do contentor de Docker** box, introduza um nome exclusivo para o contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="a8067-191">b.</span><span class="sxs-lookup"><span data-stu-id="a8067-191">b.</span></span> <span data-ttu-id="a8067-192">Escolha uma das seguintes imagens de Docker de Olá:</span><span class="sxs-lookup"><span data-stu-id="a8067-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="a8067-193">**Imagem predefinida do Docker**: Especifica uma imagem de Docker pré-existentes a partir do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8067-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="a8067-194">lista de Olá das imagens de Docker nesta caixa é composta por várias imagens que Olá Toolkit do Azure tiver sido configurado toopatch para que o artefacto é automaticamente implementado.</span><span class="sxs-lookup"><span data-stu-id="a8067-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="a8067-195">**Dockerfile personalizado**: Especifica um Dockerfile guardado anteriormente a partir do seu computador local.</span><span class="sxs-lookup"><span data-stu-id="a8067-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="a8067-196">Esta é uma funcionalidade mais avançada para programadores que pretendem toodeploy os seus próprios Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="a8067-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="a8067-197">No entanto, está a funcionar toodevelopers que utilizam este tooensure opção que os respetivos Dockerfile baseia-se corretamente.</span><span class="sxs-lookup"><span data-stu-id="a8067-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="a8067-198">Olá Toolkit do Azure não validar conteúdo Olá um Dockerfile personalizada, para a implementação de Olá poderá falhar se Olá Dockerfile tem problemas.</span><span class="sxs-lookup"><span data-stu-id="a8067-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="a8067-199">Além disso, Olá Azure Toolkit espera Olá personalizado Dockerfile toocontain um artefacto de aplicação web e tentará tooopen uma ligação HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8067-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="a8067-200">Se os programadores publicar um tipo diferente de artefactos, poderá receber erros innocuous após a implementação.</span><span class="sxs-lookup"><span data-stu-id="a8067-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="a8067-201">c.</span><span class="sxs-lookup"><span data-stu-id="a8067-201">c.</span></span> <span data-ttu-id="a8067-202">**Definições de porta**: introduza Olá TCP porta enlace exclusivo para o contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![janela de toobe criado de contentor de Docker Olá configurar Olá][PUB08]

10. <span data-ttu-id="a8067-204">Depois de concluir todos os Olá precedente passos, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="a8067-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="a8067-205">Olá, Azure Toolkit começa a implementar a sua tooAzure de aplicação web num contentor de Docker.</span><span class="sxs-lookup"><span data-stu-id="a8067-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a8067-206">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a8067-206">Next steps</span></span>
<span data-ttu-id="a8067-207">Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="a8067-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="a8067-208">[Toolkit do Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8067-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8067-209">[Novidades no Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8067-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8067-210">[Instalar Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8067-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8067-211">[Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8067-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="a8067-212">[Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]</span><span class="sxs-lookup"><span data-stu-id="a8067-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="a8067-213">[Azure Toolkit para IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8067-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8067-214">[Novidades no Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8067-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8067-215">[Instalar Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8067-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8067-216">[Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8067-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="a8067-217">[Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="a8067-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="a8067-218">Para obter mais informações sobre como utilizar o Azure com Java, consulte [Centro de programadores Java do Azure] e [ferramentas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a8067-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a8067-219">Para obter recursos adicionais para Docker, consulte oficial Olá [Web site do Docker].</span><span class="sxs-lookup"><span data-stu-id="a8067-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png