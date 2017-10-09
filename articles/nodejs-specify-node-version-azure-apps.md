---
title: "aaaSpecifying uma versão do Node.js"
description: "Saiba como toospecify Olá versão do Node.js utilizados pelo Azure Web Sites e serviços em nuvem"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>Especificar uma versão do Node.js numa aplicação do Azure
Quando a alojar uma aplicação Node.js, poderá pretender tooensure que a sua aplicação utiliza uma versão específica do Node.js. Existem várias formas tooaccomplish isto para aplicações alojadas no Azure.

## <a name="default-versions"></a>Versões de predefinido
versões de Node.js Olá fornecidas pelo Azure são atualizadas constantemente. Salvo especificação em contrário, Olá versão predefinida que é especificado no Olá `WEBSITE_NODE_DEFAULT_VERSION` variável de ambiente será utilizada. toooverride este valor predefinido, siga os passos de Olá nas seguintes secções deste artigo

> [!NOTE]
> Se estiver a alojar a aplicação num serviço em nuvem do Azure (função web ou de trabalho) e é Olá pela primeira vez que implementou a aplicação Olá, Azure tentará toouse Olá a mesma versão do Node.js que instalou no seu ambiente de desenvolvimento se-la corresponde a uma das versões de predefinição Olá disponíveis no Azure.
>
>

## <a name="versioning-with-packagejson"></a>Controlo de versões com Package. JSON
Pode especificar a versão de Olá do toobe Node.js utilizado ao adicionar Olá seguir tooyour **Package. JSON** ficheiro:

    "engines":{"node":version}

Onde *versão* é toouse de número de versão específica de Olá. Pode especificar as condições mais complexas para versão, tais como:

    "engines":{"node": "0.6.22 || 0.8.x"}

Uma vez que 0.6.22 não é uma das versões de Olá disponíveis no ambiente de alojamento de Olá, hello versão mais recente do Olá 0.8 série que está disponível será utilizado em vez disso, - 0.8.4.

## <a name="versioning-websites-with-app-settings"></a>Controlo de versões sites com as definições de aplicação
Se estiver a alojar aplicações Olá num Web site, pode definir a variável de ambiente de Olá **WEBSITE_NODE_DEFAULT_VERSION** versão pretendida do toohello.

## <a name="versioning-cloud-services-with-powershell"></a>Serviços de Cloud de controlo de versões com o PowerShell
Se estiver a alojar aplicações Olá num serviço em nuvem e estiver a implementar aplicações de Olá com o Azure PowerShell, pode substituir versão do Node.js predefinida Olá utilizando Olá **conjunto AzureServiceProjectRole** cmdlet do PowerShell. Por exemplo:

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

Nota Olá parâmetros Olá acima instrução diferenciam maiúsculas de minúsculas.  Pode verificar a versão correta do Olá do Node.js tiver sido selecionada, verificando Olá **motores** propriedade da função de **Package. JSON**.

Também pode utilizar Olá **Get-AzureServiceProjectRoleRuntime** tooretrieve uma lista das versões de Node.js disponíveis para aplicações alojadas como um serviço em nuvem.  Verifique sempre a versão de Olá do Node.js depende do seu projeto estiver nesta lista.

## <a name="using-a-custom-version-with-azure-websites"></a>Utilizar uma versão personalizada com Web sites do Azure
Enquanto o Azure oferece várias versões de predefinição de Node.js, poderá pretender toouse uma versão que não é fornecida por predefinição. Se a aplicação será alojada como um Web site do Azure, pode conseguir isto utilizando Olá **iisnode.yml** ficheiro. Olá seguintes passos guiá-lo através do processo de Olá de utilizar uma versão personalizada do Node.Js com um Web site do Azure:

1. Criar um novo diretório e, em seguida, crie um **server.js** ficheiros dentro do diretório de Olá. Olá **server.js** ficheiro deve conter a seguinte Olá:

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    Esta ação apresenta a versão do Node.js Olá a ser utilizado quando o utilizador procura site Olá.
2. Crie um novo Web site e um nome de Olá nota do site de Olá. Por exemplo, o seguinte Olá utiliza Olá [ferramentas da linha de comandos do Azure] toocreate um novo Web site do Azure com o nome **mywebsite**e, em seguida, ative um repositório de Git para o Web site Olá.

        azure site create mywebsite --git
3. Criar um novo diretório designado **bin** como subordinado de diretório Olá Olá **server.js** ficheiro.
4. Transferir a versão específica do Olá do **node.exe** (versão do Windows hello) que pretende toouse com a sua aplicação. Por exemplo, Olá seguintes utiliza **curl** versão toodownload 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    Guardar Olá **node.exe** ficheiro para Olá **bin** pasta criada anteriormente.
5. Criar um **iisnode.yml** ficheiros Olá mesmo diretório como Olá **server.js** de ficheiros e, em seguida, adicionar Olá seguir toohello conteúdo **iisnode.yml** ficheiro:

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    Este caminho é onde hello **node.exe** ficheiros dentro do seu projeto estarão localizados assim que tiver publicado a toohello de aplicação Web site do Azure.
6. Publica a aplicação. Por exemplo, uma vez que criar um novo Web site com o parâmetro de – git Olá anteriormente, hello seguintes comandos irão adicionar Olá aplicação ficheiros toomy repositório de Git local e emiti-las toohello repositório de Web site:

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Depois de tem publicado aplicações Olá, abra o Web site de Olá num browser. Deverá ver uma mensagem a indicar "Olá da versão de nó do Azure em execução: v0.8.1".

## <a name="next-steps"></a>Passos Seguintes
Agora que compreende como versão de Olá toospecify do Node.js utilizadas pela sua aplicação, saiba como demasiado[funcionam com módulos], [criar e implementar um Site Web do Node.js](app-service-web/app-service-web-get-started-nodejs.md), e [como toouse hello do Azure Ferramentas de linha de comandos para Mac e Linux].

Para obter mais informações, consulte Olá [Centro para programadores do Node.js](https://azure.microsoft.com/develop/nodejs/).

[como toouse hello do Azure Ferramentas de linha de comandos para Mac e Linux]:cli-install-nodejs.md
[ferramentas da linha de comandos do Azure]:cli-install-nodejs.md
[funcionam com módulos]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
