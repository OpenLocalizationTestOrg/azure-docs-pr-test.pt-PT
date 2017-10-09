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
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Suporte SSH para a aplicação de Web do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Descrição geral

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) é um protocolo de rede criptográficos por utilizar os serviços de rede em segurança. É frequentemente utilizada toolog num sistema remotamente em segurança de uma linha de comandos e executar remotamente comandos administrativos.

Web App no Linux fornece suporte SSH num contentor de aplicação Olá com cada uma das imagens Olá incorporadas Docker utilizadas para Olá pilha de tempo de execução de aplicações web novas. 

![Pilhas de tempo de execução](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Também pode utilizar o SSH com as imagens de Docker personalizadas, incluindo o servidor SSH Olá como parte da imagem de Olá e configurá-lo, tal como descrito neste tópico.



## <a name="making-a-client-connection"></a>Efetuar uma ligação de cliente

toomake uma ligação de cliente SSH, o site principal Olá tem de ser iniciado. 

Cole o ponto final de gestão de controlo de origem (SCM) Olá para a sua aplicação web no seu browser utilizando Olá seguinte formato:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Se não está já autenticado, são necessário tooauthenticate com tooconnect sua subscrição do Azure.

![Ligação de SSH](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Suporte SSH com imagens personalizadas do Docker

Por ordem para uma personalizado Docker imagem toosupport SSH comunicação entre o cliente Olá Olá portal do Azure e contentor de Olá, efetue Olá os seguintes passos para a imagem de Docker. 

Estes passos são apresentados na Olá repositório do App Service do Azure como um exemplo [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Incluir Olá `openssh-server` instalação no [ `RUN` instrução](https://docs.docker.com/engine/reference/builder/#run) no hello Dockerfile para a imagem e defina Olá palavra-passe da conta de raiz de Olá demasiado`"Docker!"`. 

    > [!NOTE] 
    > Esta configuração não permite o contentor de toohello ligações externas. SSH só pode ser acedido através de Olá Kudu / SCM Site, o que é autenticado utilizando Olá credenciais publicação.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Adicionar um [ `COPY` instrução](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy um [sshd_config](http://man.openbsd.org/sshd_config) ficheiro toohello */etc/ssh/* diretório. O ficheiro de configuração deve ser baseado no nosso ficheiro sshd_config no repositório do GitHub do serviço de aplicações do Azure de Olá [aqui](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Olá *sshd_config* ficheiros têm de incluir seguinte Olá ou Olá ligação falhar: 
    > * `Ciphers`tem de incluir, pelo menos, um dos seguintes Olá: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`tem de incluir, pelo menos, um dos seguintes Olá: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Incluir porta 2222 Olá [ `EXPOSE` instrução](https://docs.docker.com/engine/reference/builder/#expose) para Olá Dockerfile. Embora a palavra-passe de raiz de Olá é conhecido, porta 2222 não pode ser acedida a partir Olá internet. É uma porta única interna acessível apenas por contentores dentro da rede de bridge de Olá de uma rede privada virtual.

    ```docker
    EXPOSE 2222 80
    ```

4. Certifique-se toostart Olá ssh do serviço. exemplo de Olá [aqui](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) utiliza um script de shell na */bin* diretório.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Olá Dockerfile utiliza Olá [ `CMD` instrução](https://docs.docker.com/engine/reference/builder/#cmd) script de Olá toorun.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Passos seguintes
Consulte Olá seguintes ligações para mais informações sobre a aplicação Web no Linux. Pode publicar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Como toouse um Docker personalizado imagem para a aplicação de Web do Azure no Linux](app-service-linux-using-custom-docker-image.md)
* [Utilizar a configuração de PM2 para Node.js na aplicação Web do Azure no Linux](app-service-linux-using-nodejs-pm2.md)
* [Utilizando o .NET Core na aplicação Web do Azure no Linux](app-service-linux-using-dotnetcore.md)
* [Utilizar Ruby na aplicação Web do Azure no Linux](app-service-linux-ruby-get-started.md)
* [Aplicação de Web do App Service do Azure no Linux FAQ](app-service-linux-faq.md)

