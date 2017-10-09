---
title: "aaaWeb aplicação rápidas (Node.js) | Microsoft Docs"
description: "Um tutorial que baseia-se no tutorial de serviço de nuvem Olá e demonstra como toouse Olá módulo rápida."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>Criar uma aplicação de web do Node.js utilizando rápida num serviço em nuvem do Azure
NODE.js inclui um conjunto mínimo de funcionalidades no tempo de execução do Olá core.
Os programadores utilizam frequentemente 3rd terceiros módulos tooprovide funcionalidades adicionais quando desenvolver uma aplicação Node.js. Este tutorial irá criar uma nova aplicação com Olá [Express] [ Express] módulo, que fornece uma arquitetura MVC para criar aplicações web do Node.js.

Abaixo é uma captura de ecrã da aplicação Olá concluída:

![Um browser a apresentar tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>Criar um projeto de serviço em nuvem
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

Execute o seguinte Olá passos toocreate um novo projeto de serviço de nuvem com o nome 'expressapp':

1. De Olá **Menu Iniciar** ou **ecrã Iniciar**, procure **do Windows PowerShell**. Por fim, clique com botão direito **do Windows PowerShell** e selecione **executar como administrador**.
   
    ![Ícone do PowerShell do Azure](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. Altere os diretórios toohello **c:\\nó** diretório e, em seguida, introduza os seguintes comandos toocreate uma nova solução com o nome de Olá **expressapp** e uma função da web com o nome **WebRole1** :
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > Por predefinição, **Add-AzureNodeWebRole** utiliza uma versão antiga do Node.js. Olá **conjunto AzureServiceProjectRole** acima da declaração dá instruções ao Azure toouse v0.10.21 do nó.  Tenha em atenção de que os parâmetros de Olá diferenciam maiúsculas de minúsculas.  Pode verificar a versão correta do Olá do Node.js tiver sido selecionada, verificando Olá **motores** propriedade no **WebRole1\package.json**.
    > 
    > 

## <a name="install-express"></a>Instalação rápida
1. Instale o gerador do Express Olá emitindo Olá os seguintes comandos:
   
        PS C:\node\expressapp> npm install express-generator -g
   
    saída de Olá do comando de npm Olá deverá ter um aspeto semelhante resultado toohello abaixo. 
   
    ![Saída de apresentação Olá do Windows PowerShell de npm Olá instalar comando rápido.](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. Altere os diretórios toohello **WebRole1** diretório e utilize Olá comando rápida toogenerate uma nova aplicação:
   
        PS C:\node\expressapp\WebRole1> express
   
    Poderá é pedido toooverwrite a aplicação anterior. Introduza **y** ou **Sim** toocontinue. Express irá gerar ficheiro de app.js Olá e uma estrutura de pasta para criar a sua aplicação.
   
    ![saída de Olá do comando rápida Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. tooinstall dependências adicionais definidas no ficheiro de Package. JSON Olá, introduza Olá os seguintes comandos:
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![comando de instalação de npm Olá resultado Olá](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. Seguinte de Olá utilize comando toocopy Olá **bin/www** ficheiro demasiado**server.js**. Isto é para que o serviço em nuvem Olá possa encontrar o ponto de entrada Olá para esta aplicação.
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   Depois de concluída este comando, deve ter um **server.js** ficheiro no diretório de Olá WebRole1.
5. Modificar Olá **server.js** tooremove um Olá '.' carateres de Olá seguinte linha.
   
       var app = require('../app');
   
   Depois de efetuar esta alteração, linha Olá deverá aparecer da seguinte forma.
   
       var app = require('./app');
   
   Esta alteração é necessária uma vez que foi movida ficheiro Olá (anteriormente **bin/www**,) toohello mesmo diretório do ficheiro da aplicação Olá necessário. Depois de efetuar esta alteração, guarde Olá **server.js** ficheiro.
6. Utilize Olá seguintes aplicações de Olá toorun comando no Olá emulador do Azure:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![Uma página web que contém tooexpress boas-vindas.](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>Modificar Olá vista
Modificar agora a mensagem de saudação do Olá vista toodisplay "Boas-vindas tooExpress no Azure".

1. Introduza Olá seguintes comandos tooopen Olá Index. jade ficheiro:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![Olá conteúdo de Olá Index. jade ficheiro.](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade é o motor de vista Olá predefinido utilizado por aplicações rápida. Para obter mais informações sobre o motor de vista Jade Olá, consulte [http://jade-lang.com][http://jade-lang.com].
2. Modificar a última linha de Olá de texto, acrescentando **no Azure**.
   
   ![ficheiro de index. jade Olá, a última linha de Olá lê: p de boas-vindas demasiado\#{title} no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. Guarde o ficheiro de Olá e sair do bloco de notas.
4. Atualize o browser e verá as suas alterações.
   
   ![Uma janela do browser, a página Olá contém tooExpress boas-vindas no Azure](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

Após a aplicação de Olá teste, utilize Olá **Stop-AzureEmulator** emulador do cmdlet toostop Olá.

## <a name="publishing-hello-application-tooazure"></a>Publicação tooAzure de aplicação Olá
Na janela do PowerShell do Azure Olá, utilize Olá **Publish-AzureServiceProject** cmdlet toodeploy Olá aplicação tooa o serviço em nuvem

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Uma vez concluída a operação de implementação de Olá, o seu browser abrir e apresentar a página web de Olá.

![Um browser apresentar página Olá, Express. URL de Olá indica, agora está alojado no Azure.](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>Passos seguintes
Para obter mais informações, consulte Olá [Centro para programadores do Node.js](/develop/nodejs/).

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


