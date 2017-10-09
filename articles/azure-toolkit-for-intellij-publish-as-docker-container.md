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
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Publicar uma aplicação web como um contentor de Docker utilizando Olá Toolkit do Azure para o IntelliJ

Os contentores de docker são um método amplamente utilizado para implementar aplicações web. Ao utilizar os contentores de Docker, os programadores podem consolidar todos os respetivos ficheiros de projeto e dependências para um único pacote para o servidor de tooa de implementação. Olá Toolkit do Azure para o IntelliJ simplifica este processo para programadores de Java adicionando *publicar como contentor de Docker* funcionalidades para tooMicrosoft de implementação do Azure. Este artigo explica Olá passos necessários toopublish sua tooAzure aplicações como contentores de Docker.

> [!NOTE]
>
> Obter mais informações sobre o Docker estão disponíveis no Olá [Web site do Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Publicar o seu tooAzure de aplicação web utilizando um contentor de Docker

> [!NOTE]
> * toopublish aplicação web, tem de criar um artefacto pronta para a implementação. toolearn mais, consulte Olá [informações adicionais sobre a criação de artefactos](#artifacts) secção.
>
> * Depois de concluir o Assistente de implementação de Olá, pelo menos, uma vez, a maioria das definições de é utilizada como predefinições quando executar o Assistente de Olá novamente.
>

1. Abra o projeto de aplicação web in IntelliJ.

2. Olá toostart **publicar como contentor de Docker** assistente, efetue um dos seguintes Olá:

   * No Olá **projeto** ferramenta janela, clique no seu projeto, clique em **Azure**e, em seguida, clique em **publicar como contentor de Docker**:

      ![Olá publicar como comando de contentor do Docker][PUB01]

   * Na barra de ferramentas de IntelliJ Olá, clique em Olá **publicar grupo** botão e, em seguida, clique em **publicar como contentor de Docker**:

      ![Olá publicar como comando de contentor do Docker][PUB02]  
    Olá **contentor de Docker implementar no Azure** é aberto o assistente.

   ![Olá implementar o contentor de Docker no Assistente do Azure][PUB03]

3. No Olá **escreva um nome de imagem, selecione o caminho do artefacto Olá e verificar um toobe de anfitriões de Docker utilizado** janela, Olá a seguir: 

   a. No Olá **nome de imagem de Docker** box, introduza um nome exclusivo para o anfitrião de Docker. (o Assistente de Olá cria automaticamente um nome, mas pode modificá-la.) 

   b. Olá **anfitriões** área apresenta quaisquer anfitriões de Docker que já tenha criado. Efetue um dos seguintes Olá: 
      * Se tiver um anfitrião de Docker existente, pode implementar a sua tooit de aplicação web.
      * toocreate um anfitrião de Docker, clique em verde Olá sinal de adição (**+**).  
       Olá **criar anfitriões de Docker** é aberta a caixa de diálogo. 

      ![Implementar o contentor de Docker no Assistente do Azure][PUB04a]

4. No Olá **configurar a máquina virtual nova do Olá** janela, fornecer Olá seguintes informações sobre o anfitrião de Docker. (o Assistente de Olá gera automaticamente a maioria das informações Olá, mas pode modificar qualquer uma delas). 

   a. No Olá **nome** box, introduza um nome exclusivo para o anfitrião de Docker Olá. (É não Olá igual ao hello do nome de imagem de Docker que especificou anteriormente.) 
    
   b. No Olá **subscrição** box, introduza Olá subscrição do Azure que utiliza para o anfitrião. 
      
   c. No Olá **região** box, introduza a região geográfica olá onde está localizado o seu anfitrião.
      
   d. No Olá **SO e tamanho** separador, Olá a seguir:      
      * **SO do anfitrião**: introduza o sistema de operativo Olá para a máquina virtual Olá que contém o anfitrião. 
      * **Tamanho**: introduza o tamanho de máquina virtual de Olá para o anfitrião.   
       
   e. No Olá **grupo de recursos** separador, selecione Olá seguinte:      
      * **Novo grupo de recursos**: criar um grupo de recursos para o anfitrião.
      * **Grupo de recursos existente**: Especifique um grupo de recursos existentes da sua conta do Azure. 
       
   f. No Olá **rede** separador, selecione Olá seguinte:      
      * **Nova rede virtual**: criar uma rede virtual para o anfitrião.
      * **Rede virtual existente**: Especifique uma rede virtual existente da sua conta do Azure. 
       
   g. No Olá **armazenamento** separador, selecione Olá seguinte:      
      * **Nova conta do storage**: criar uma conta de armazenamento para o anfitrião.
      * **Conta de armazenamento existente**: Especifique uma conta de armazenamento existentes da sua conta do Azure.
       
5. Clique em **Seguinte**.  
     Olá **configurar registo de credenciais e definições de porta** é aberta a janela.

      ![Olá configurar início de sessão credenciais e a janela de definições de porta][PUB05]

6. Selecione uma das seguintes opções de Olá:

      * **Importar as credenciais do Cofre de chaves do Azure**: Especifique um conjunto de credenciais que são armazenados na sua subscrição do Azure guardado anteriormente.

          > [!NOTE]
          > Não é automaticamente acessível por outra conta ou principal de serviço que partilha subscrição Olá um cofre de chaves do Azure que é criado com uma conta específica ou um principal de serviço. tooallow outra conta ou serviço principal toouse Olá chave de cofre, tem de utilizar Olá conta de Olá tooadd portal do Azure ou principal de serviço.

      * **Novo registo credenciais**: criar um novo conjunto de credenciais de início de sessão. Se selecionar esta opção, Olá a seguir:

        a. No Olá **VM credenciais** separador, forneça Olá seguindo as informações de credenciais de início de sessão de máquina virtual de Olá de anfitrião do Docker: * **Username**: introduza o nome de utilizador Olá para o início de sessão de máquina virtual credenciais.
             * **Palavra-passe** e **confirmar**: introduza a palavra-passe de Olá as suas credenciais de início de sessão de máquina virtual.
             * **SSH**: introduza Olá as definições de Secure Shell (SSH) para o anfitrião de Docker. Pode selecionar uma das seguintes opções de Olá: * **nenhum**: Especifica que a máquina virtual não permite ligações SSH.
                * **Gerar automaticamente**: cria automaticamente Olá definições requisitos para ligar através de SSH.
                * **Importar do directory**: permite-lhe toospecify um diretório que contém um conjunto de definições de SSH guardados anteriormente. diretório de Olá tem de conter Olá seguintes dois ficheiros:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. No Olá **Docker Daemon acesso** separador, forneça Olá seguintes informações:

          ![Criar anfitrião Docker][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. Depois de introduzir informações de Olá necessário, clique em **concluir**.  
    Olá **contentor de Docker implementar no Azure** reappears do assistente.

   ![Implementar o contentor de Docker no Assistente do Azure][PUB07]

8. Clique em **Seguinte**.  
    Olá **configurar toobe de contentor de Docker Olá criado** é aberta a janela.

   ![janela de toobe criado de contentor de Docker Olá configurar Olá][PUB08]

9. No Olá **configurar toobe de contentor de Docker Olá criado** janela, fornecer Olá seguintes informações: 

   a. No Olá **nome do contentor de Docker** box, introduza um nome exclusivo para o contentor de Docker.

   b. Escolha uma das seguintes imagens de Docker de Olá: 

      * **Imagem predefinida do Docker**: Especifique uma imagem de Docker pré-existentes a partir do Azure. 

        > [!NOTE]
        > lista de Olá das imagens de Docker nesta caixa é composta por várias imagens que Olá Toolkit do Azure tiver sido configurado toopatch para que o artefacto é automaticamente implementado. 

      * **Dockerfile personalizado**: especificar um Dockerfile guardado anteriormente a partir do seu computador local.

        > [!NOTE]
        > Esta é uma funcionalidade mais avançada para programadores que pretendem toodeploy os seus próprios Dockerfile. No entanto, está a funcionar toodevelopers que utilizam este tooensure opção que os respetivos Dockerfile baseia-se corretamente. Porque Olá Toolkit do Azure não validar conteúdo Olá um Dockerfile personalizado, implementação de Olá poderá falhar se Olá Dockerfile tem problemas. Além disso, porque Olá Azure Toolkit espera Olá personalizado Dockerfile toocontain um artefacto de aplicação web, este tenta tooopen uma ligação HTTP. Se os programadores publicar um tipo diferente de artefactos, estes poderão receber erros innocuous após a implementação.

   c. No Olá **definições de porta** box, introduza Olá TCP porta enlace exclusivo para o contentor de Docker. 

10. Depois de concluir Olá precedente passos, clique em **concluir**. 

Olá, Azure Toolkit começa a implementar a sua tooAzure de aplicação web num contentor de Docker. A menos que configurou toobe IntelliJ implementado em segundo plano de Olá, um **implementar tooAzure** barra de progresso é apresentado. 

![barra de progresso da implementação Olá][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Informações adicionais sobre a criação de artefactos

toocreate um artefacto pronta para a implementação, Olá seguintes:

1. Abra o projeto de aplicação web in IntelliJ.

2. Clique em **ficheiro**e, em seguida, clique em **estrutura do projeto**.

   ![Olá comandos de estrutura do projeto][ART01]

3. tooadd um artefacto, clique em verde Olá sinal de adição (**+**) e, em seguida, clique em **aplicação Web: arquivo**.

   ![Olá comando "Arquivo de: de aplicação Web"][ART02]

4. No Olá **nome** box, introduza um nome para o artefacto (não incluem Olá *.war* extensão) e, em seguida, clique em **OK**.

   ![caixa de nome de artefacto Olá][ART03]

Para obter mais informações sobre a criação de artefactos no IntelliJ, consulte [configurar artefactos] no Web site de JetBrains Olá.

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

Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure] e Olá [ferramentas de Java para Visual Studio Team Services].

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
