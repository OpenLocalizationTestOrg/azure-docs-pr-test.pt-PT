---
title: "Olá aaaInstalling Toolkit do Azure para o Eclipse | Microsoft Docs"
description: "Saiba como tooinstall Olá Toolkit do Azure para o Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6c195fab2b47fb5c42541a8cf52be4ec88d27b5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="installing-hello-azure-toolkit-for-eclipse"></a>Instalar Olá Toolkit de Azure do Eclipse
Olá Toolkit do Azure para o Eclipse fornece modelos e funcionalidades que lhe permitem tooeasily criam, desenvolver, testar e implementar aplicações do Azure utilizando o ambiente de desenvolvimento Eclipse Olá. Olá Toolkit do Azure para o Eclipse for um projeto de Open Source. código de origem Olá está disponível em Olá licença MIT de <https://github.com/microsoft/azure-tools-for-java>.

Olá, os passos seguintes mostra como tooinstall Olá Toolkit do Azure para o Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="tooinstall-hello-azure-toolkit-for-eclipse"></a>Olá tooinstall Toolkit de Azure do Eclipse
1. Abra o Eclipse.
2. Clique em Olá **ajudar** e, em seguida, clique em **instalar novo Software**, conforme apresentado na seguinte ilustração de Olá.
   
    ![Instalar Olá Toolkit de Azure do Eclipse][01]
3. No Olá **Software disponível** caixa de diálogo, dentro de Olá **trabalhar com** caixa de texto, escreva `http://dl.microsoft.com/eclipse` seguido Olá **Enter** chave.
4. No Olá **nome** painel, verificação **Toolkit do Azure para o Eclipse**e desmarque **contacte atualizar todos os sites durante a instalar o software de toofind necessário**. O ecrã deverá aparecer semelhante toohello seguinte:
   
    ![Instalar Olá Toolkit de Azure do Eclipse][02]
5. Se expandir Olá **Toolkit do Azure para o Eclipse**, verá Olá seguintes itens:
   
   * **Plug-in do Application Insights para Java**: este componente permite-lhe toouse serviços do Azure telemetria registo e análise para as suas aplicações e instâncias do servidor.
   * **Filtro de serviços de controlo de acesso do Azure**: este componente fornece suporte para autenticação de utilizadores de aplicação com o Azure ACS, ativar cenários de início de sessão único e externalizing lógica de identidade da aplicação Olá.
   * **O plug-ins comuns do Azure**: este componente fornece uma funcionalidade comum de Olá necessária por outros componentes do toolkit.
   * **Explorador do Azure para o Eclipse**: este componente fornece uma funcionalidade comum de Olá necessária por outros componentes do toolkit.
   * **Plug-in do Azure para o Eclipse com o Java**: este componente fornece suporte para o desenvolvimento projetos que ajudam a criar, testar e implementar aplicações de Java para a nuvem do Microsoft Azure de Olá no Eclipse e através de linha de comandos.
   * **Plugin de aplicações Web do Azure com Java**: este componente fornece suporte para implementar os contentores de aplicação Web do Azure de tooMicrosoft de aplicações de web de Java.
   * **4.2 de controlador JDBC Microsoft para o SQL Server**: este componente fornece JDBC API para SQL Server e base de dados de SQL do Microsoft Azure para Java plataforma Enterprise Edition 8.
   * **Pacote para as bibliotecas de cliente do Apache Qpid para JMS**: este componente fornece Olá JMS o componente de cliente de Olá Apache Qpid projeto tooenable a aplicação toouse AMQP mensagens no Microsoft Azure.
   * **Pacote de bibliotecas do Microsoft Azure para Java**: este componente fornece APIs para aceder aos serviços do Microsoft Azure, tais como o armazenamento, o barramento de serviço, tempo de execução do serviço, etc.
6. Clique em **Seguinte**. (Se ocorrer atrasos invulgares ao instalar o toolkit de Olá, certifique-se de que **contacte atualizar todos os sites durante a instalar o software de toofind necessário** está desmarcada.)
7. No Olá **instalar detalhes** caixa de diálogo, clique em **seguinte**.
   
    ![Reveja os detalhes da instalação][03]
8. No Olá **rever licenças** caixa de diálogo, reveja os termos de Olá Olá de contratos de licença. Se aceitar os termos de Olá Olá de contratos de licença, clique em **Olá termos Olá de contratos de licença** e, em seguida, clique em **concluir**. (Olá restantes passos partem do princípio de aceitar termos de Olá Olá de contratos de licença. Se não aceitar os termos de Olá Olá de contratos de licença, saia do processo de instalação de Olá.)
   
    ![Licenças de revisão][04]
   
    Eclipse irá transferir e instalar pacotes da Olá.
   
    ![Progresso da instalação][05]
9. Se lhe for pedido de instalação de toocomplete toorestart Eclipse, clique em **Sim**.
   
    ![Reinicie a linha de comandos][06]

## <a name="see-also"></a>Veja Também
Para mais informações sobre Olá Toolkits do Azure para Java IDEs, consulte Olá seguintes ligações:

* [Toolkit do Azure do Eclipse]
  * [Novidades no Olá Toolkit do Azure para o Eclipse]
  * *Instalar Olá Toolkit do Azure para o Eclipse (neste artigo)*
  * [Início de sessão em instruções para Olá Toolkit do Azure para o Eclipse]
  * [Criar uma aplicação de Web Olá mundo do Azure no Eclipse]
* [Azure Toolkit para IntelliJ]
  * [Novidades no Olá Toolkit do Azure para o IntelliJ]
  * [Instalar Olá Toolkit do Azure para o IntelliJ]
  * [Início de sessão em instruções para Olá Toolkit do Azure para o IntelliJ]
  * [Criar uma aplicação de Web Olá mundo do Azure no IntelliJ]

Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure].

<!-- URL List -->

[Toolkit do Azure do Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit para IntelliJ]: ./azure-toolkit-for-intellij.md
[Criar uma aplicação de Web Olá mundo do Azure no Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Criar uma aplicação de Web Olá mundo do Azure no IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Instalar Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Início de sessão em instruções para Olá Toolkit do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Início de sessão em instruções para Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novidades no Olá Toolkit do Azure para o Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novidades no Olá Toolkit do Azure para o IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro de programadores Java do Azure]: https://azure.microsoft.com/develop/java/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: ./media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->
