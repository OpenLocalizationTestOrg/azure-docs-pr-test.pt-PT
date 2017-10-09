---
title: "suporte de aaaSSH da aplicação Web de serviço de aplicações do Azure no Linux | Microsoft Docs"
description: "Saiba mais sobre a utilização do SSH com a aplicação de Web do Azure no Linux."
keywords: "serviço de aplicações do Azure, aplicação web, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a><span data-ttu-id="1e7b7-104">Suporte SSH para a aplicação de Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="1e7b7-104">SSH support for Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a><span data-ttu-id="1e7b7-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="1e7b7-105">Overview</span></span>

<span data-ttu-id="1e7b7-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) é um protocolo de rede criptográficos por utilizar os serviços de rede em segurança.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) is a cryptographic network protocol for using network services securely.</span></span> <span data-ttu-id="1e7b7-107">É frequentemente utilizada toolog num sistema remotamente em segurança de uma linha de comandos e executar remotamente comandos administrativos.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-107">It is most commonly used toolog into a system remotely securely from a command-line and execute administrative commands remotely.</span></span>

<span data-ttu-id="1e7b7-108">Web App no Linux fornece suporte SSH num contentor de aplicação Olá com cada uma das imagens Olá incorporadas Docker utilizadas para Olá pilha de tempo de execução de aplicações web novas.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-108">Web App on Linux provides SSH support into hello app container with each of hello built-in Docker images used for hello Runtime Stack of new web apps.</span></span> 

![Pilhas de tempo de execução](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

<span data-ttu-id="1e7b7-110">Também pode utilizar o SSH com as imagens de Docker personalizadas, incluindo o servidor SSH Olá como parte da imagem de Olá e configurá-lo, tal como descrito neste tópico.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-110">You can also use SSH with your custom Docker images by including hello SSH server as part of hello image and configuring it as described in this topic.</span></span>



## <a name="making-a-client-connection"></a><span data-ttu-id="1e7b7-111">Efetuar uma ligação de cliente</span><span class="sxs-lookup"><span data-stu-id="1e7b7-111">Making a client connection</span></span>

<span data-ttu-id="1e7b7-112">toomake uma ligação de cliente SSH, o site principal Olá tem de ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-112">toomake an SSH client connection, hello main site must be started.</span></span> 

<span data-ttu-id="1e7b7-113">Cole o ponto final de gestão de controlo de origem (SCM) Olá para a sua aplicação web no seu browser utilizando Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="1e7b7-113">Paste hello Source Control Management (SCM) endpoint for your web app into your browser using hello following form:</span></span>

        https://<your sitename>.scm.azurewebsites.net/webssh/host

<span data-ttu-id="1e7b7-114">Se não está já autenticado, são necessário tooauthenticate com tooconnect sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-114">If you are not already authenticated, you are required tooauthenticate with your Azure subscription tooconnect.</span></span>

![Ligação de SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a><span data-ttu-id="1e7b7-116">Suporte SSH com imagens personalizadas do Docker</span><span class="sxs-lookup"><span data-stu-id="1e7b7-116">SSH support with custom Docker images</span></span>

<span data-ttu-id="1e7b7-117">Por ordem para uma personalizado Docker imagem toosupport SSH comunicação entre o cliente Olá Olá portal do Azure e contentor de Olá, efetue Olá os seguintes passos para a imagem de Docker.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-117">In order for a custom Docker image toosupport SSH communication between hello container and hello client in hello Azure portal, perform hello following steps for your Docker image.</span></span> 

<span data-ttu-id="1e7b7-118">Estes passos são apresentados na Olá repositório do App Service do Azure como um exemplo [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-118">These steps are are shown in hello Azure App Service repository as an example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).</span></span>

1. <span data-ttu-id="1e7b7-119">Incluir Olá `openssh-server` instalação no [ `RUN` instrução](https://docs.docker.com/engine/reference/builder/#run) no hello Dockerfile para a imagem e defina Olá palavra-passe da conta de raiz de Olá demasiado`"Docker!"`.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-119">Include hello `openssh-server` installation in [`RUN` instruction](https://docs.docker.com/engine/reference/builder/#run) in hello Dockerfile for your image and set hello password for hello root account too`"Docker!"`.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="1e7b7-120">Esta configuração não permite o contentor de toohello ligações externas.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-120">This configuration does not allow external connections toohello container.</span></span> <span data-ttu-id="1e7b7-121">SSH só pode ser acedido através de Olá Kudu / SCM Site, o que é autenticado utilizando Olá credenciais publicação.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-121">SSH can only be accessed via hello Kudu / SCM Site, which is authenticated using hello publishing credentials.</span></span>

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. <span data-ttu-id="1e7b7-122">Adicionar um [ `COPY` instrução](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy um [sshd_config](http://man.openbsd.org/sshd_config) ficheiro toohello */etc/ssh/* diretório.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-122">Add a [`COPY` instruction](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy a [sshd_config](http://man.openbsd.org/sshd_config) file toohello */etc/ssh/* directory.</span></span> <span data-ttu-id="1e7b7-123">O ficheiro de configuração deve ser baseado no nosso ficheiro sshd_config no repositório do GitHub do serviço de aplicações do Azure de Olá [aqui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-123">Your configuration file should be based on our sshd_config file in hello Azure-App-Service GitHub repository [here](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e7b7-124">Olá *sshd_config* ficheiros têm de incluir seguinte Olá ou Olá ligação falhar:</span><span class="sxs-lookup"><span data-stu-id="1e7b7-124">hello *sshd_config* file must include hello following or hello connection fails:</span></span> 
    > * <span data-ttu-id="1e7b7-125">`Ciphers`tem de incluir, pelo menos, um dos seguintes Olá: `aes128-cbc,3des-cbc,aes256-cbc`.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-125">`Ciphers` must include at least one of hello following: `aes128-cbc,3des-cbc,aes256-cbc`.</span></span>
    > * <span data-ttu-id="1e7b7-126">`MACs`tem de incluir, pelo menos, um dos seguintes Olá: `hmac-sha1,hmac-sha1-96`.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-126">`MACs` must include at least one of hello following: `hmac-sha1,hmac-sha1-96`.</span></span>

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. <span data-ttu-id="1e7b7-127">Incluir porta 2222 Olá [ `EXPOSE` instrução](https://docs.docker.com/engine/reference/builder/#expose) para Olá Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-127">Include port 2222 in hello [`EXPOSE` instruction](https://docs.docker.com/engine/reference/builder/#expose) for hello Dockerfile.</span></span> <span data-ttu-id="1e7b7-128">Embora a palavra-passe de raiz de Olá é conhecido, porta 2222 não pode ser acedida a partir Olá internet.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-128">Although hello root password is known, port 2222 cannot be accessed from hello internet.</span></span> <span data-ttu-id="1e7b7-129">É uma porta única interna acessível apenas por contentores dentro da rede de bridge de Olá de uma rede privada virtual.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-129">It is an internal only port accessible only by containers within hello bridge network of a private virtual network.</span></span>

    ```docker
    EXPOSE 2222 80
    ```

4. <span data-ttu-id="1e7b7-130">Certifique-se toostart Olá ssh do serviço.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-130">Make sure toostart hello ssh service.</span></span> <span data-ttu-id="1e7b7-131">exemplo de Olá [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utiliza um script de shell na */bin* diretório.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-131">hello example [here](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) uses a shell script in */bin* directory.</span></span>

    ```bash
    #!/bin/bash
    service ssh start
    ```

    <span data-ttu-id="1e7b7-132">Olá Dockerfile utiliza Olá [ `CMD` instrução](https://docs.docker.com/engine/reference/builder/#cmd) script de Olá toorun.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-132">hello Dockerfile uses hello [`CMD` instruction](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello script.</span></span>

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a><span data-ttu-id="1e7b7-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1e7b7-133">Next steps</span></span>
<span data-ttu-id="1e7b7-134">Consulte Olá seguintes ligações para mais informações sobre a aplicação Web no Linux.</span><span class="sxs-lookup"><span data-stu-id="1e7b7-134">See hello following links for more information regarding Web App on Linux.</span></span> <span data-ttu-id="1e7b7-135">Pode publicar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span><span class="sxs-lookup"><span data-stu-id="1e7b7-135">You can post questions and concerns on [our forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).</span></span>

* [<span data-ttu-id="1e7b7-136">Como toouse um Docker personalizado imagem para a aplicação de Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="1e7b7-136">How toouse a custom Docker image for Azure Web App on Linux</span></span>](app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="1e7b7-137">Utilizar a configuração de PM2 para Node.js na aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="1e7b7-137">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="1e7b7-138">Utilizando o .NET Core na aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="1e7b7-138">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="1e7b7-139">Utilizar Ruby na aplicação Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="1e7b7-139">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="1e7b7-140">Aplicação de Web do App Service do Azure no Linux FAQ</span><span class="sxs-lookup"><span data-stu-id="1e7b7-140">Azure App Service Web App on Linux FAQ</span></span>](app-service-linux-faq.md)

