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
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Ativar o acesso remoto para implementações do Azure no Eclipse
as implementações de resolução de problemas do toohelp, pode ativar e utilizar a máquina virtual acesso remoto tooconnect toohello a implementação de alojamento. Olá funcionalidade do acesso remoto depende Olá protocolo RDP (Remote Desktop Protocol). Pode configurar o acesso remoto para a sua implementação depois de ter publicado-tooAzure ou, se estiver a utilizar Eclipse com um sistema operativo Windows, pode configurar o acesso remoto antes de publicar tooAzure. Tenha em atenção de que precisa de um cliente de ambiente de trabalho remoto que é compatível com o sistema operativo na máquina de virtual da implementação de ordem, tooconnect tooyour no Azure.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Como tooenable acesso remoto antes de implementar tooAzure
> [!NOTE]
> Acesso remoto antes de implementar a aplicação tooAzure tooenable, terá de toobe Eclipse a ser executado no Windows.
> 
> 

Olá imagem seguinte mostra Olá **acesso remoto** caixa de diálogo Propriedades utilizado tooenable de acesso remoto.

![][ic719494]

Existem dois Olá de toodisplay formas **acesso remoto** caixa de diálogo de propriedades:

* Clique em Olá **avançadas** ligação no Olá **acesso remoto** secção Olá **publicar tooAzure** caixa de diálogo.

* Abra Olá **propriedades** caixa de diálogo do seu projeto do Azure.

Quando cria um novo projeto de implementação do Azure, o projeto de Olá não terá acesso remoto ativado por predefinição. No entanto, facilmente pode ativar o acesso remoto, especificando o nome de utilizador Olá e a palavra-passe na Olá **publicar tooAzure** caixa de diálogo. palavra-passe de acesso remoto de Olá é encriptada utilizando certificados x. 509. Se não utilizar os seus próprios certificados de fornecer encriptação Olá depende de um certificado autoassinado vem incluído no Olá Plug-in do Azure para o Eclipse. Este certificado autoassinado consta Olá **cert** pasta do projeto do Azure, armazenados ambos como um ficheiro de certificado pública (SampleRemoteAccessPublic.cer) e como um PFX Personal Information Exchange () (ficheiro de certificado SampleRemoteAccessPrivate.pfx). Olá última contém a chave privada do Olá certificado Olá e tem uma palavra-passe para a predefinição **Password1**. No entanto, uma vez que esta palavra-passe conhecimento público, certificado de predefinido Olá deve ser utilizado apenas para efeitos de aprendizagem, não para uma implementação de produção. Por isso, diferente para efeitos de aprendizagem, quando quiser tooenabled sessões remotas para as implementações, deverá clicar Olá **avançadas** ligação no Olá **publicar tooAzure** toospecify de caixa de diálogo os seus próprios certificado. Tenha em atenção que precisará tooupload Olá PFX versão do serviço de tooyour alojado certificado Olá dentro Olá Portal de gestão do Azure, pelo que esse Azure pode desencriptar a palavra-passe de utilizador de Olá.

resto Olá tutorial Olá mostra-lhe como tooenable acesso remoto-para um projeto de implementação do Azure que foi criado inicialmente com acesso remoto desativado. Para efeitos deste tutorial, vamos criar um novo certificado autoassinado e o ficheiro. pfx terão uma palavra-passe à sua escolha. Tem também a opção de Olá de utilizar um certificado emitido por uma autoridade de certificação.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Como tooenable acesso remoto depois de ter implementado tooAzure
tooenable acesso remoto depois de ter implementado tooAzure, Olá utilize os seguintes passos:

1. Inicie sessão no portal de gestão do Azure Olá utilizando a sua conta do Azure

2. Na lista de **serviços em nuvem**, selecione o seu serviço de nuvem implementado

3. Na página de web do serviço de nuvem do Olá, clique em Olá **configurar** ligação

4. Olá parte inferior da página de configuração de Olá, clique em Olá **remoto** ligação

5. Quando é apresentada a caixa de diálogo de pop-up Olá:
   
   * Especifique Olá função que para os quais pretende que o acesso remoto tooenable

   * Clique em tooselect Olá **ativar o ambiente de trabalho remoto** caixa de verificação
   
   * Especifique um nome de utilizador e palavra-passe que pretende toouse para acesso remoto
   
   * Selecione Olá toouse de certificado

6. Clique em **OK** 

Verá uma mensagem a indicar que a sua alteração de configuração está em curso, o que pode demorar alguns minutos toocomplete. Após a alteração da configuração Olá foi concluída, siga os passos de Olá Olá **toolog no remotamente** secção neste artigo.

## <a name="how-tooenable-remote-access-in-your-package"></a>Como tooenable acesso remoto no seu pacote
1. No painel do Explorador de projeto do Eclipse, clique no projeto do Azure e clique em **propriedades**.

2. No Olá **propriedades** caixa de diálogo, expanda **Azure** no painel da esquerda Olá e clique em **acesso remoto**.

3. No Olá **acesso remoto** caixa de diálogo, certifique-se **ativar todas as funções tooaccept ligações de ambiente de trabalho remoto com estas credenciais de início de sessão** está marcada.

4. Especifique um nome de utilizador para Olá ligação de ambiente de trabalho remoto.

5. Especifique e confirme Olá palavra-passe do utilizador Olá. Olá utilizador nome e palavra-passe valores definidos nesta caixa de diálogo serão utilizados quando efetuar uma ligação de ambiente de trabalho remoto. (Tenha em atenção de que se trata de uma palavra-passe separada da sua palavra-passe PFX.)

6. Especifique a data de expiração de Olá Olá conta de utilizador.

7. Clique em **novo** toocreate um novo certificado autoassinado. (Em alternativa, pode selecionar um certificado do sistema de ficheiro ou a área de trabalho através de Olá **área de trabalho** ou **FileSystem** botões, respetivamente, mas para efeitos deste tutorial, vamos criar um novo certificado.)

   * No Olá **novo certificado** caixa de diálogo, especifique e confirme a palavra-passe de Olá irá utilizar para o ficheiro PFX.

   * Aceite o valor de Olá fornecido para **nome (CN)**, ou utilizar um nome personalizado.

   * Especifique o nome de ficheiro e caminho do olá onde Olá novo certificado, no formato. cer, será guardado. Para este passo e o passo seguinte Olá, pode utilizar Olá **cert** pasta do projeto do Azure, mas estiver livre toochoose noutra localização. Para efeitos deste tutorial, iremos utilizar **c:\mycert\mycert.cer**. (Criar Olá **c:\mycert** tooproceeding anterior da pasta ou utilize uma pasta existente, se assim o desejar.)

   * Especifique o nome de ficheiro e caminho do olá onde Step-by-Olá novo certificado e a respetiva chave privada, no formato. pfx, serão guardados. Para efeitos deste tutorial, iremos utilizar **c:\mycert\mycert.pfx**. O **novo certificado** diálogo deverá ter um aspeto semelhante toohello seguinte (atualizar os caminhos de pastas de Olá se não utilizou **c:\mycert**):
     
      ![][ic712275]

   * Clique em **OK** tooclose Olá **novo certificado** caixa de diálogo.

8. O **acesso remoto** diálogo deverá ter um aspeto semelhante toohello seguinte:</p>
   
   ![][ic719495]

9. Clique em **OK** tooclose Olá **acesso remoto** caixa de diálogo.

Reconstruir a aplicação, com Olá criar conjunto toocloud de implementação.

## <a name="toolog-in-remotely"></a>toolog no remotamente
Assim que a instância de função estiver pronta, pode remotamente iniciar sessão na máquina virtual toohello que está a alojar a aplicação.

* Se estiver a utilizar Eclipse no Windows e Olá selecionado **implementar de ambiente de trabalho remoto do início no** opção durante a implementação tooAzure, será apresentada com um ecrã de início de sessão de ligação de ambiente de trabalho remoto quando a implementação é iniciado. Quando lhe for pedido Olá nome de utilizador e palavra-passe, introduza valores Olá que especificou para o utilizador remoto Olá e será capaz de toolog no.

* Outra forma toolog no remotamente é efetuada através de Olá <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:
  
  * Dentro do Olá **serviços em nuvem** vista de Olá portal de gestão do Azure, clique o seu serviço em nuvem, clique em **instâncias**, clique uma instância específica e, em seguida, clique em Olá **Connect**botão. Olá **Connect** botão aparece como seguinte Olá na barra de comando Olá:
    
      ![][ic659273]

  * Depois de clicar em Olá **Connect** botão, será pedido tooopen um ficheiro RDP. Abra o ficheiro Olá e siga as instruções de Olá. (Foi também guardar este computador local do ficheiro tooyour e, em seguida, execute Olá ficheiro ao fazer duplo clique tooremote registo no tooyour máquina virtual sem necessitar de toofirst aceda portal de gestão de Olá.)

  * Quando lhe for pedido Olá nome de utilizador e palavra-passe, introduza valores Olá que especificou para o utilizador remoto Olá e será capaz de toolog no.

> [!NOTE]
> Se estiver num sistema operativo Windows não, é necessário toouse um cliente de ambiente de trabalho remoto que é compatível com o sistema operativo e siga Olá passos tooconfigure que o cliente com definições de Olá no ficheiro RDP Olá que transferiu.
> 
> 

## <a name="see-also"></a>Veja Também
[Toolkit do Azure do Eclipse][Azure Toolkit for Eclipse]

[Criar uma aplicação do Olá mundo do Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Instalar Olá Toolkit de Azure do Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obter mais informações sobre como utilizar o Azure com Java, consulte Olá [Centro de programadores Java do Azure][Azure Java Developer Center].

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
