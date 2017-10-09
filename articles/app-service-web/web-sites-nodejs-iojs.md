---
title: aaaHow toouse io.js com as Web Apps do Azure App Service
description: "Saiba como toouse uma aplicação web no App Service do Azure com o io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>Como toouse io.js com as Web Apps do Azure App Service
bifurcação de nó popular Olá [io.js] funcionalidades projeto de Node.js vários tooJoyent de diferenças, incluindo um modelo de governação mais aberto, um ciclo de lançamento mais rápido e uma adoção mais rápida das funcionalidades de JavaScript novas e experimental.

Enquanto [App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicações Web tem várias versões de Node.js pré-instalado, também permite para um binário de Node.js fornecidos pelo utilizador. Este artigo aborda os dois métodos para ativar a utilização de Olá de io.js na Web Apps do App Service: Olá a utilização de um script de implementação expandida, que configura automaticamente a versão de io.js disponível mais recente do Azure toouse Olá, bem como carregamento manual de Olá de um binário io.js. 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>Utilizar um Script de implementação
Após a implementação de uma aplicação Node.js, Web Apps do App Service executa uma série de comandos pequenos tooensure Olá ambiente está corretamente configurado. Utilizar um script de implementação, este processo pode ser transferências de Olá tooinclude personalizados e a configuração de io.js.

Olá [io.js Script de implementação](https://github.com/felixrieseberg/iojs-azure) está disponível no GitHub. tooenable io.js na sua aplicação web, basta copiar **.deployment**, **deploy.cmd** e **IISNode.yml** toohello raiz da sua pasta de aplicação e implementar aplicações tooWeb.  

primeiro ficheiro Olá, **.deployment**, dá instruções ao Web Apps toorun **deploy.cmd** após a implementação. Este script é executado todos os passos habitual Olá para uma aplicação Node.js, mas também transfere a versão mais recente do Olá do io.js. Por fim, **IISNode.yml** configura as aplicações Web toouse Olá apenas transferido io.js binário em vez de um binário Node.js pré-instaladas.

> [!NOTE]
> Olá tooupdate utilizada io.js binário, basta Reimplementar a sua aplicação - script Olá irá transferir uma nova versão do io.js que todas as aplicações de Olá única vez é implementada.
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>Utilizar a instalação Manual
instalação manual do Olá de uma versão personalizada io.js inclui apenas dois passos. Em primeiro lugar, transferir Olá **win x64** binário diretamente a partir de Olá [io.js distribuição]. Necessários são dois ficheiros - **iojs.exe** e **iojs.lib**. Guardar ambos os ficheiros tooa pasta dentro da sua aplicação web, por exemplo em **bin/iojs**.

tooconfigure Web Apps toouse **iojs.exe** em vez de uma versão de nó pré-instaladas, crie um **IISNode.yml** ficheiro na raiz de Olá da sua aplicação e adicione a seguinte linha de Olá.

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>Passos Seguintes
Este artigo aprendeu como toouse io.js com o serviço Web Apps do App, utilizando ambos fornecido scripts de implementação, bem como a instalação manual. 

> [!NOTE]
> IO.js está em desenvolvimento pesado e atualizados mais frequentemente do que Node.js. Um número de módulos do Node.js poderão não funcionar com io.js -. consulte [io.js no GitHub] para resolução de problemas.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de Web sites tooApp serviço consulte: [App Service do Azure e o respetivo impacto nos serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Se quiser tooget iniciado com o App Service do Azure antes de inscrever-se numa conta do Azure, aceda demasiado[experimentar o App Service](https://azure.microsoft.com/try/app-service/), onde, pode criar imediatamente uma aplicação web de arranque de curta duração no App Service. Sem cartões de crédito; sem compromissos.
> 
> 

[io.js]: https://iojs.org
[io.js distribuição]: https://iojs.org/dist/
[io.js no GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
