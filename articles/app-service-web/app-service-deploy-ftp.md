---
title: "aaaDeploy tooAzure a aplicação do serviço de aplicações através de FTP/S | Microsoft Docs"
description: "Saiba como toodeploy sua tooAzure de aplicação do serviço de aplicações através de FTP ou FTPS."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Implementar a sua tooAzure de aplicação do serviço de aplicações através de FTP/S

Este artigo mostra como toouse FTP ou FTPS toodeploy a aplicação web, o back-end da aplicação móvel ou a aplicação API demasiado[App Service do Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

ponto final FTP/S de Olá para a sua aplicação já está ativo. Nenhuma configuração é a implementação de FTP/S tooenable necessário.

> [!IMPORTANT]
> Iremos estão continuamente a demorar passos tooimprove segurança da plataforma Microsoft Azure. Como parte deste esforço em curso uma atualização de aplicações Web é planeada de regiões de Datacenters Central e nordeste da Alemanha. Durante este aplicações Web serão estar a desativar a utilização de Olá do protocolo FTP em texto simples para implementações. Os nossos clientes do recomendação tooour é tooswitch tooFTPS para implementações. Esperamos que não seja serviço interrupção tooyour durante esta atualização que está a ser planeada 9/5. Valorizamo-lo suportar deste esforço.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Passo 1: Definir credenciais de implementação

servidor FTP de Olá tooaccess para a sua aplicação, primeiro precisa de credenciais de implementação. 

tooset ou repor as credenciais de implementação, consulte [credenciais de implementação de serviço de aplicações do Azure](app-service-deployment-credentials.md). Este tutorial demonstra a utilização de Olá de credenciais de nível de utilizador.

## <a name="step-2-get-ftp-connection-information"></a>Passo 2: Obter informações de ligação de FTP

1. No Olá [portal do Azure](https://portal.azure.com), abra a aplicação [painel de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Selecione **descrição geral** no menu à esquerda Olá, em seguida, tenha em atenção os valores de Olá para **utilizador FTP/implementação**, **nome de anfitrião do FTP**, e **nome de anfitrião FTPS**. 

    ![Informações de ligação de FTP](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Olá **utilizador FTP/implementação** valor de utilizador, tal como apresentado pelo Olá Portal do Azure, incluindo o nome da aplicação Olá no contexto de adequada tooprovide ordem para o servidor de Olá FTP.
    > Pode encontrar Olá mesmas informações quando seleciona **propriedades** no menu à esquerda Olá. 
    >
    > Além disso, a palavra-passe de implementação de Olá nunca é apresentado. Se se esquecer da sua palavra-passe de implementação, volte atrás demasiado[passo 1](#step1) e repor a palavra-passe de implementação.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Passo 3: Implementar tooAzure de ficheiros

1. A partir do seu cliente FTP ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), etc), utilize informações de ligação de Olá que recolheu tooconnect tooyour aplicação.
3. Copie os ficheiros e os respetivos toohello de estrutura de diretório respetivos [ **/site/wwwroot** diretório](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) no Azure (ou Olá **/site/wwwroot/App_Data/tarefas/** diretório para WebJobs).
4. Aplicação de Olá da aplicação tooyour procurar URL tooverify está a funcionar corretamente. 

> [!NOTE] 
> Ao contrário [implementações baseadas em Git](app-service-deploy-local-git.md), implementação de FTP não suporta Olá seguir automatizações de implementação: 
>
> - restauro de dependência (por exemplo, automatizações NuGet, NPM, PIP e compositor)
> - compilação de binários de .NET
> - a geração da Web. config (aqui está uma [exemplo de Node.js](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> Deve restaurar, criar e gerar estes ficheiros necessários manualmente no seu computador local e implementá-las em conjunto com a sua aplicação.
>
>

## <a name="next-steps"></a>Passos seguintes

Para cenários de implementação mais avançados, tente [implementar tooAzure com o Git](app-service-deploy-local-git.md). Implementação baseada no Git tooAzure permite controlo de versão, o restauro de pacote, MSBuild e muito mais.

## <a name="more-resources"></a>Mais Recursos

* [Criar uma aplicação web do PHP MySQL e implementar a utilizar FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Credenciais de implementação do App Service do Azure](app-service-deploy-ftp.md)
