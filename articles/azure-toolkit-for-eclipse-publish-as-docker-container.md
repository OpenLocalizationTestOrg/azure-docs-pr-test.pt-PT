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
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Publicar uma aplicação web como um contentor de Docker utilizando Olá Toolkit do Azure para o Eclipse

Os contentores de docker são um método amplamente utilizado para implementar aplicações web. Ao utilizar os contentores de Docker, os programadores podem consolidar todos os respetivos ficheiros de projeto e dependências para um único pacote para o servidor de tooa de implementação. Olá Toolkit do Azure para o Eclipse simplifica este processo para programadores de Java adicionando *publicar como contentor de Docker* funcionalidades para tooMicrosoft de implementação do Azure. Este artigo explica Olá passos necessários toopublish sua tooAzure aplicações como contentores de Docker.

> [!NOTE]
> Obter mais informações sobre o Docker estão disponíveis no Olá [Web site do Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar o seu tooAzure de aplicação web utilizando um contentor de Docker

1. Abra o projeto de aplicação web no Eclipse.

2. Olá toostart **publicar como contentor de Docker** assistente, efetue um dos seguintes Olá:

   * No Olá **navegador** ver, clique no seu projeto, clique em **Azure**e, em seguida, clique em **publicar como contentor de Docker**.

      ![Vista de navegador publicar como comando de contentor do Docker][PUB01]

   * Na barra de ferramentas do Olá Eclipse, clique em Olá **publicar** botão e, em seguida, clique em **publicar como contentor de Docker**.

      ![Barra de ferramentas do Eclipse publicar como comando de contentor do Docker][PUB02]
      
    Olá **contentor de Docker implementar no Azure** é aberto o assistente.

    ![Olá implementar o contentor de Docker no Assistente do Azure][PUB03]

3. No Olá **escreva um nome de imagem, selecione o caminho do artefacto Olá e verificar um toobe de anfitriões de Docker utilizado** janela, Olá a seguir:

    a. No Olá **nome de imagem de Docker** box, introduza um nome exclusivo para o anfitrião de Docker. (o Assistente de Olá cria automaticamente um nome, mas pode modificá-la.)

    b. Olá **anfitriões** área apresenta quaisquer anfitriões de Docker que já tenha criado. Efetue um dos seguintes Olá:

    * Se tiver um anfitrião de Docker existente, pode implementar a sua tooit de aplicação web.
    * Clique em toocreate um novo anfitrião do Docker, **adicionar**.  
      
    Olá **criar anfitriões de Docker** é aberta a caixa de diálogo.

    ![Implementar o contentor de Docker no Assistente do Azure][PUB04a]

4. No Olá **configurar a máquina virtual nova do Olá** janela, especifique Olá seguintes opções para o anfitrião de Docker. (o Assistente de Olá gera automaticamente a maior parte das opções de Olá para si, mas pode modificar qualquer uma delas).

   a. **Nome**: introduza um nome exclusivo para o anfitrião de Docker Olá. (É não Olá igual ao hello do nome de imagem de Docker que especificou anteriormente.)

   b. **Subscrição**: introduza Olá subscrição do Azure que utiliza para o anfitrião.

   c. **Região**: introduza a região geográfica olá onde está localizado o seu anfitrião.

   d. No Olá **sistema operativo anfitrião e o tamanho** separador:
     * **SO do anfitrião**: introduza o sistema de operativo Olá para a máquina virtual Olá que contém o anfitrião.
     * **Tamanho**: introduza o tamanho de máquina virtual de Olá para o anfitrião.

   e. No Olá **grupo de recursos** separador:
     * **Novo grupo de recursos**: criar um novo grupo de recursos para o anfitrião.
     * **Grupo de recursos existente**: introduza um grupo de recursos existentes da sua conta do Azure.

   f. No Olá **rede** separador:
     * **Nova rede virtual**: criar uma nova rede virtual para o anfitrião.
     * **Rede virtual existente**: introduza uma rede virtual existente a partir da sua conta do Azure.

   g. No Olá **armazenamento** separador:
     * **Nova conta do storage**: criar uma nova conta de armazenamento para o anfitrião.
     * **Conta de armazenamento existente**: introduza uma conta de armazenamento existentes da sua conta do Azure.

5. Clique em **Seguinte**.

6. No Olá **configurar registo de credenciais e definições de porta** janela, selecione uma das seguintes opções de Olá:

    * **Importar as credenciais do Cofre de chaves do Azure**: Especifica um conjunto de credenciais que são armazenados na sua subscrição do Azure guardado anteriormente.

      >[!NOTE]
      >Não é automaticamente acessível por outra conta ou principal de serviço que partilha subscrição Olá um cofre de chaves do Azure que é criado com uma conta específica ou um principal de serviço. tooallow outro toouse conta ou serviço principal Olá Cofre de chaves, tem de utilizar Olá conta de Olá tooadd portal do Azure ou principal de serviço.

    * **Novo registo credenciais**: cria um novo conjunto de credenciais de início de sessão. Se selecionar esta opção, Olá a seguir:
    
      * No Olá **VM credenciais** separador, escolha uma das seguintes Olá opções para credenciais de início de sessão de máquina virtual de Olá do anfitrião do Docker:

          * **Nome de utilizador**: introduza o nome de utilizador Olá para as credenciais de início de sessão de máquina virtual.
          * **Palavra-passe** e **confirmar**: introduza a palavra-passe de Olá para as credenciais de início de sessão de máquina virtual.
          * **SSH**: introduza Olá as definições de Secure Shell (SSH) para o anfitrião de Docker. Pode escolher entre Olá seguintes opções:
            * **Nenhum**: Especifica que a máquina virtual não irá permitir ligações SSH.
            * **Gerar automaticamente**: cria automaticamente Olá definições requisitos para ligar através de SSH.
            * **Importar do directory**: Especifica um diretório que contém um conjunto de definições de SSH guardados anteriormente. diretório de Olá tem de conter Olá seguintes dois ficheiros:
                * *id_rsa*: contém a identificação de RSA Olá para um utilizador.
                * *id_rsa.pub*: contém Olá RSA chave pública que é utilizado para autenticação.
        
        ![Criar anfitrião Docker][PUB05]

      * No Olá **Docker Daemon credenciais** separador, especifique Olá seguintes opções:

          * **Porta de Daemon de docker**: introduza a porta TCP exclusiva Olá para o anfitrião de Docker.
          * **Segurança de TLS**: introduza Olá Transport Layer Security definições para o anfitrião de Docker. Pode escolher entre Olá seguintes opções:
            * **Nenhum**: Especifica que a máquina virtual não irá permitir ligações TLS.
            * **Gerar automaticamente**: cria automaticamente Olá definições requisitos para ligar através de TLS.
            * **Importar do directory**: Especifica um diretório que contém um conjunto de definições de TLS guardados anteriormente. Mais especificamente, o diretório de Olá tem de conter Olá seis ficheiros a seguir:
                * *CA.pem* e *AC key.pem*: contém o certificado de Olá e chave pública para Olá TLS autoridade de certificação.
                * *CERT.pem* e *key.pem*: contém o certificado de cliente de Olá e chave pública que é utilizado para autenticação de TLS.
                * *Server.pem* e *servidor key.pem*: contém o certificado de servidor Olá e chave pública para o anfitrião de Olá.

        ![Criar anfitrião Docker][PUB06]

7. Após introduzir todas Olá precedente informações, clique em **concluir**.

8. No Olá **contentor de Docker implementar no Azure** assistente, clique em **seguinte**.

   ![Olá implementar o contentor de Docker no Assistente do Azure][PUB07]

9. No Olá **configurar toobe de contentor de Docker Olá criado** janela, Olá a seguir:

   a. No Olá **nome do contentor de Docker** box, introduza um nome exclusivo para o contentor de Docker.

   b. Escolha uma das seguintes imagens de Docker de Olá:
     * **Imagem predefinida do Docker**: Especifica uma imagem de Docker pré-existentes a partir do Azure.

       >[!NOTE]
       >lista de Olá das imagens de Docker nesta caixa é composta por várias imagens que Olá Toolkit do Azure tiver sido configurado toopatch para que o artefacto é automaticamente implementado.

     * **Dockerfile personalizado**: Especifica um Dockerfile guardado anteriormente a partir do seu computador local.

       >[!NOTE]
       >Esta é uma funcionalidade mais avançada para programadores que pretendem toodeploy os seus próprios Dockerfile. No entanto, está a funcionar toodevelopers que utilizam este tooensure opção que os respetivos Dockerfile baseia-se corretamente. Olá Toolkit do Azure não validar conteúdo Olá um Dockerfile personalizada, para a implementação de Olá poderá falhar se Olá Dockerfile tem problemas. Além disso, Olá Azure Toolkit espera Olá personalizado Dockerfile toocontain um artefacto de aplicação web e tentará tooopen uma ligação HTTP. Se os programadores publicar um tipo diferente de artefactos, poderá receber erros innocuous após a implementação.

   c. **Definições de porta**: introduza Olá TCP porta enlace exclusivo para o contentor de Docker.

     ![janela de toobe criado de contentor de Docker Olá configurar Olá][PUB08]

10. Depois de concluir todos os Olá precedente passos, clique em **concluir**.

Olá, Azure Toolkit começa a implementar a sua tooAzure de aplicação web num contentor de Docker. 

## <a name="next-steps"></a>Passos seguintes
Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá os seguintes recursos:

* [Toolkit do Azure do Eclipse]
  * [Novidades no Olá Toolkit de Azure do Eclipse]
  * [Instalar Olá Toolkit de Azure do Eclipse]
  * [Instruções de início de sessão para Olá Toolkit de Azure do Eclipse]
  * [Criar uma aplicação de web de Olá, mundo do Azure no Eclipse]
* [Azure Toolkit para IntelliJ]
  * [Novidades no Olá Toolkit do Azure para o IntelliJ]
  * [Instalar Olá Toolkit do Azure para o IntelliJ]
  * [Início de sessão instruções para Olá Toolkit do Azure para o IntelliJ]
  * [Criar uma aplicação de web de Olá, mundo do Azure no IntelliJ]

Para obter mais informações sobre como utilizar o Azure com Java, consulte [Centro de programadores Java do Azure] e [ferramentas de Java para Visual Studio Team Services].

Para obter recursos adicionais para Docker, consulte oficial Olá [Web site do Docker].

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