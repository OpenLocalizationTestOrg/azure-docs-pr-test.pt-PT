---
title: "aaaNode.js guia de introdução | Microsoft Docs"
description: "Saiba como toocreate Node.js uma simples aplicação web e implementá-la tooan serviço em nuvem Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Criar e implementar uma tooan de aplicação Node.js o serviço em nuvem do Azure

Este tutorial mostra como toocreate Node.js uma simples aplicação em execução num serviço em nuvem do Azure. Serviços cloud são os blocos modulares de Olá das aplicações em nuvem dimensionáveis no Azure. Permitem a separação de Olá e gestão independente e escalável de componentes front-end e back-end da aplicação.  Os Cloud Services fornecem uma máquina virtual dedicada robusta para alojar cada função de forma fiável.

Para obter mais informações sobre serviços em nuvem e como comparar tooAzure Web sites e as máquinas virtuais, consulte [comparação de Web sites do Azure, os serviços de nuvem e máquinas virtuais].

> [!TIP]
> Está à procura toobuild um site simples? Se o seu cenário envolver apenas um front-end de site simples, considere a [utilização de uma aplicação Web simples]. Pode facilmente atualizar tooa serviço em nuvem à medida que aumenta a sua aplicação web e os seus requisitos se alteram.

Este tutorial descreve como compilar uma aplicação Web simples alojada numa função da Web. Irá utilizar tootest de emulador de computação Olá a aplicação localmente, e em seguida, implementá-la utilizando as ferramentas de linha de comandos do PowerShell.

aplicação Olá é uma aplicação "Olá, mundo" simples:

![Um browser a apresentar a página de web de Olá mundo Olá][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Pré-requisitos
> [!NOTE]
> Este tutorial utiliza o Azure PowerShell, que requer o Windows.

* Instale e configure o [Azure PowerShell].
* Transfira e instale Olá [Azure SDK para .NET 2.7]. No Olá instalar o programa de configuração, selecione:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Criar um projeto do Serviço em Nuvem do Azure
Execute Olá tarefas toocreate um novo projeto do serviço de nuvem do Azure, juntamente com andaime Node.js básico a seguir:

1. Executar **do Windows PowerShell** como administrador; a partir de Olá **Menu Iniciar** ou **ecrã Iniciar**, procure **do Windows PowerShell**.
2. [Ligue o PowerShell] tooyour subscrição.
3. Introduza Olá projeto do PowerShell cmdlet toocreate toocreate Olá os seguintes:

        New-AzureServiceProject helloworld

    ![resultado de Olá do comando do Olá New-AzureService helloworld][hello result of hello New-AzureService helloworld command]

    Olá **New-AzureServiceProject** cmdlet gera uma estrutura básica para publicar um tooa de aplicação Node.js serviço em nuvem. Contém os ficheiros de configuração necessários para publicação tooAzure. Olá cmdlet também altera o diretório de toohello do diretório de trabalho para o serviço de Olá.

    Olá cmdlet cria Olá os seguintes ficheiros:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef**: ficheiros específicos do Azure necessários para publicar a aplicação. Para obter mais informações, consulte [Descrição Geral da Criação de um Serviço Alojado do Azure].
   * **Deploymentsettings**: armazena as definições locais que são utilizadas pelo Olá cmdlets de implementação do Azure PowerShell.
4. Introduza Olá os seguintes comandos tooadd uma nova função da web:

       Add-AzureNodeWebRole

   ![resultado Olá Olá comando Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   Olá **Add-AzureNodeWebRole** cmdlet cria uma aplicação Node.js básica. Também modifica Olá **. csfg** e **. csdef** ficheiros tooadd entradas de configuração para a nova função de Olá.

   > [!NOTE]
   > Se não especificar um nome de função, será utilizado um nome predefinido. Pode fornecer um nome como primeiro parâmetro de cmdlet Olá:`Add-AzureNodeWebRole MyRole`

aplicação de Node.js Olá está definida no ficheiro de Olá **server.js**, localizado no diretório de Olá de função da web Olá (**WebRole1** por predefinição). Eis o código de Olá:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Este código é, essencialmente, igual ao hello "Olá mundo" no Olá de exemplo de Olá [nodejs.org] Web site, exceto que utiliza o número de porta de Olá atribuído pelo ambiente de nuvem Olá.

## <a name="deploy-hello-application-tooazure"></a>Implementar Olá tooAzure de aplicação

> [!NOTE]
> toocomplete neste tutorial, precisa de uma conta do Azure. Pode [ativar os benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [inscrever-se numa conta gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Transferir Olá Azure as definições de publicação
toodeploy tooAzure sua aplicação, primeiro tem de transferir Olá publicação definições para a sua subscrição do Azure.

1. Execute Olá seguinte cmdlet do PowerShell do Azure:

       Get-AzurePublishSettingsFile

   Este procedimento irá utilizar o seu browser toonavigate toohello publicar a página de transferências de definições. Poderá ser pedido toolog com uma Account Microsoft. Se assim for, utilize conta Olá associada à subscrição do Azure.

   Guarde Olá transferido perfil tooa localização do ficheiro facilmente acessível.
2. Execute o seguinte cmdlet tooimport Olá que transferiu do perfil de publicação:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Depois de importar Olá definições de publicação, considere eliminar Olá transferido o ficheiro. publishsettings, porque contém informações que podem permitir a alguém tooaccess sua conta.

### <a name="publish-hello-application"></a>Publicar a aplicação Olá
toopublish executar Olá os seguintes comandos:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** Especifica Olá nome para a implementação de Olá. Tem de ser um nome exclusivo, caso contrário Olá publicar processo irá falhar. Olá **Get-Data** comando adiciona uma cadeia de data/hora que deve certificar-nome Olá exclusivo.
* **-Location** Especifica Olá datacenter que Olá aplicação será alojada no. toosee uma lista de datacenters disponíveis, utilize Olá **Get-AzureLocation** cmdlet.
* **-Launch** abre uma janela do browser e navega serviço toohello alojado após conclusão da implementação.

Publicação for bem sucedida, verá um resposta semelhante toohello seguinte procedimento:

![resultado Olá Olá comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Isto pode demorar alguns minutos até Olá aplicação toodeploy e fique disponível quando publicada pela primeira vez.

Depois de concluída a implementação de Olá, uma janela do browser irá abrir e navegue toohello o serviço em nuvem.

![Uma janela do browser a apresentar Olá página Olá, mundo; URL de Olá indica a página Olá está alojada no Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

A aplicação está agora em execução no Azure.

Olá **Publish-AzureServiceProject** cmdlet efetua Olá os seguintes passos:

1. Cria um toodeploy de pacote. pacote de Olá contém todos os ficheiros de Olá na pasta de aplicação.
2. Cria uma nova **Conta do Storage**, se ainda não existir. Olá conta do storage do Azure é o pacote de aplicação Olá toostore utilizado durante a implementação. Pode eliminar em segurança a conta de armazenamento Olá após a conclusão da implementação.
3. Cria um novo **serviço em nuvem**, se ainda não existir um. A **serviço em nuvem** é contentor Olá na qual a aplicação será alojada quando for tooAzure implementado. Para obter mais informações, consulte [Descrição Geral da Criação de um Serviço Alojado do Azure].
4. Publica tooAzure de pacote de implementação de Olá.

## <a name="stopping-and-deleting-your-application"></a>Parar e eliminar a aplicação
Depois de implementar a aplicação, poderá ser útil toodisable-lo, para evitar custos adicionais. O Azure cobra as instâncias de função da Web por hora de tempo do servidor consumido. Hora do servidor é consumida logo que a aplicação é implementada, mesmo se instâncias Olá não estão em execução e estão em estado de Olá parado.

1. Na janela do Windows PowerShell Olá, pare a implementação do serviço de Olá criada na secção anterior Olá com Olá seguinte cmdlet:

       Stop-AzureService

   A parar serviço Olá poderá demorar vários minutos. Quando Olá serviço for parado, receberá uma mensagem a indicar que foi parado.

   ![Estado de Olá do comando de Olá Stop-AzureService][hello status of hello Stop-AzureService command]
2. serviço de Olá toodelete, Olá chamada seguinte cmdlet:

       Remove-AzureService

   Quando lhe for pedido, introduza **Y** serviço de Olá toodelete.

   A eliminar o serviço de Olá poderá demorar vários minutos. Depois de Olá tiver sido eliminado, receberá uma mensagem a indicar que o serviço de Olá foi eliminado.

   ![Estado de Olá do comando de Olá Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > A eliminar o serviço de Olá não elimina a conta de armazenamento de Olá que foi criada quando o serviço de Olá foi inicialmente publicado e irá continuar toobe faturado por armazenamento utilizado. Se mais nada estiver a utilizar armazenamento Olá, poderá ser útil toodelete-lo.

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá [Centro para programadores do Node.js].

<!-- URL List -->

[comparação de Web sites do Azure, os serviços de nuvem e máquinas virtuais]: ../app-service-web/choose-web-site-cloud-service-vm.md
[utilização de uma aplicação Web simples]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Ligue o PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Descrição Geral da Criação de um Serviço Alojado do Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centro para programadores do Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
