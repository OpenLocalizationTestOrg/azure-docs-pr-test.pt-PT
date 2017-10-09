---
title: "Descrição geral de Cache Local do serviço de aplicações aaaAzure | Microsoft Docs"
description: "Este artigo descreve como tooenable, redimensionamento e consulta o estado da funcionalidade de Cache Local do serviço de aplicações do Azure Olá Olá"
services: app-service
documentationcenter: app-service
author: SyntaxC4
manager: yochayk
editor: 
tags: optional
keywords: 
ms.assetid: e34d405e-c5d4-46ad-9b26-2a1eda86ce80
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/04/2016
ms.author: cfowler
ms.openlocfilehash: 220331ac7e15352a434d63266701071024d868c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-local-cache-overview"></a>Descrição geral de Cache Local do serviço de aplicações do Azure
Conteúdo de aplicação web do Azure é armazenado no Storage do Azure e é anexado cópias de segurança de forma durável, como uma partilha de conteúdo. Esta estrutura é toowork pretendido com uma variedade de aplicações e tem Olá seguintes atributos:  

* conteúdo de Olá é partilhado entre várias instâncias de máquina virtual (VM) da aplicação web de Olá.
* conteúdo de Olá é durável e pode ser modificado por aplicações web em execução.
* Ficheiros de registo e ficheiros de dados de diagnóstico estão disponíveis em Olá mesmo partilhado a pasta de conteúdo.
* Publicar conteúdo novo diretamente atualizações Olá pasta de conteúdo. Pode imediatamente Olá vista mesmo conteúdo através do Web site SCM Olá e Olá aplicação web em execução (normalmente, algumas tecnologias, como o ASP.NET iniciar um reinício de aplicação web em algumas alterações tooget Olá mais recente o conteúdo do ficheiro).

Apesar de muitas aplicações web utilizam uma ou todas estas funcionalidades, algumas aplicações web apenas terá um arquivo de conteúdo de alto desempenho, só de leitura que possam ser executadas com elevada disponibilidade. Estas aplicações podem beneficiar de uma instância VM de uma cache local específica.

Olá a funcionalidade de Cache Local do serviço de aplicações do Azure fornece uma vista de função da web do seu conteúdo. Este conteúdo é uma cache de write-mas-rejeição do seu conteúdo de armazenamento que é criado de forma assíncrona no arranque do site. Quando a cache de Olá estiver pronto, o site de Olá é toorun desativado conteúdos Olá em cache. As aplicações Web que são executadas em Local Cache tem Olá seguintes vantagens:

* São toolatencies immune que ocorrem quando acedem a conteúdo no armazenamento do Azure.
* São atualizações toohello immune planeada ou tempos de inatividade não planeados e outras perturbações com armazenamento do Azure que ocorrem nos servidores que servem de partilha de conteúdo de Olá.
* Têm menos reinicializações dos aplicação devido a alterações de partilha toostorage.

## <a name="how-local-cache-changes-hello-behavior-of-app-service"></a>Como Local Cache altera o comportamento de Olá do App Service
* cache local Olá é uma cópia de pastas de /site e /siteextensions Olá da aplicação web de Olá. É criada a instância de local VM Olá no arranque de aplicação web. Olá tamanho da cache local do Olá por aplicação web é limitado too300 MB por predefinição, mas pode aumentar, cópia de segurança too2 GB.
* cache local Olá é leitura e escrita. No entanto, quaisquer modificações serão rejeitadas quando a aplicação web de Olá mova as máquinas virtuais ou obtém reiniciada. Não deve utilizar a Local Cache para aplicações que armazenam dados fundamentais no arquivo de conteúdo de Olá.
* As Web apps podem continuar toowrite ficheiros de registo e dados de diagnóstico como fazem atualmente. Ficheiros de registo e dados, no entanto, são armazenados localmente num Olá VM. Em seguida, estes são copiadas periodicamente toohello arquivo de conteúdo partilhado. Olá cópia toohello partilhada de arquivo de conteúdos é um esforço mais favorável – faz uma cópia de escrita pode ser perdida devido a falhas de repentino tooa de uma instância VM.
* Há uma alteração na estrutura de pasta Olá Olá LogFiles e pastas de dados para aplicações web que utilizam a Local Cache. Agora existem subpastas Olá armazenamento LogFiles e dados pastas que se seguem o padrão de nomenclatura de Olá de "Identificador exclusivo" + o carimbo de data / hora. Cada um dos subpastas Olá corresponde à instância de VM tooa onde a aplicação web de Olá está em execução ou foi executada.  
* Publicação de aplicação de web do toohello alterações através de qualquer um dos mecanismos de publicação Olá publicarão toohello arquivo de conteúdo partilhado. Isto é propositado uma vez que queremos Olá publicados toobe conteúdo durável. cache de hora local do Olá toorefresh da aplicação web de Olá, necessita de toobe reiniciado. Aparenta isto como um passo excessivo? toomake Olá ciclo de vida de totalmente integrado, consulte as informações de Olá neste artigo.
* D:\home irá apontar toohello cache local. D:\Local irá continuar a apontar toohello VM específico armazenamento temporário.
* Vista de conteúdo Olá predefinido do site SCM Olá continuará toobe que Olá arquivo de conteúdo partilhado.

## <a name="enable-local-cache-in-app-service"></a>Ativar a Cache Local no App Service
Configurar a Local Cache utilizando uma combinação de definições de aplicação reservado. Pode configurar estas definições de aplicação utilizando Olá seguintes métodos:

* [Portal do Azure](#Configure-Local-Cache-Portal)
* [Azure Resource Manager](#Configure-Local-Cache-ARM)

### <a name="configure-local-cache-by-using-hello-azure-portal"></a>Configurar a Local Cache utilizando Olá portal do Azure
<a name="Configure-Local-Cache-Portal"></a>

Ativar a Local Cache numa base por web-aplicação ao utilizar esta definição de aplicação:`WEBSITE_LOCAL_CACHE_OPTION` = `Always`  

![Definições de aplicação do portal do Azure: Local Cache](media/app-service-local-cache/app-service-local-cache-configure-portal.png)

### <a name="configure-local-cache-by-using-azure-resource-manager"></a>Configurar a Local Cache utilizando o Azure Resource Manager
<a name="Configure-Local-Cache-ARM"></a>

```

...

{
    "apiVersion": "2015-08-01",
    "type": "config",
    "name": "appsettings",
    "dependsOn": [
        "[resourceId('Microsoft.Web/sites/', variables('siteName'))]"
    ],

"properties": {
        "WEBSITE_LOCAL_CACHE_OPTION": "Always",
        "WEBSITE_LOCAL_CACHE_SIZEINMB": "300"
    }
}

...
```

## <a name="change-hello-size-setting-in-local-cache"></a>Alterar a definição de tamanho de Olá na Local Cache
Por predefinição, é o tamanho da local cache Olá **300 MB**. Isto inclui Olá /site e /siteextensions pastas que foram copiadas de Olá conteúdo de arquivo, bem como qualquer localmente criadas pastas de dados e registos. tooincrease este limite, utilize a definição de aplicação Olá `WEBSITE_LOCAL_CACHE_SIZEINMB`. Pode aumentar o tamanho de Olá até demasiado**2 GB** (2000 MB) por aplicação web.

## <a name="best-practices-for-using-app-service-local-cache"></a>Melhores práticas para utilizar a Cache Local do serviço de aplicações
Recomendamos que utilize a Local Cache em conjunto com Olá [ambientes de teste](../app-service-web/web-sites-staged-publishing.md) funcionalidade.

* Adicionar Olá *temporária* definição de aplicação `WEBSITE_LOCAL_CACHE_OPTION` com o valor de Olá `Always` tooyour **produção** ranhura. Se estiver a utilizar `WEBSITE_LOCAL_CACHE_SIZEINMB`, também adicioná-la como uma ranhura de produção de tooyour definição temporária.
* Criar um **transição** espaço e publicar tooyour ranhura de teste. Normalmente, não definido Olá ranhura toouse Local Cache tooenable um ciclo de vida de teste compilação implementar totalmente integrado para se obter vantagens de Olá da Local Cache para a ranhura de produção Olá de transição de teste.
* O site contra o bloco de transição de teste.  
* Quando estiver pronto, emitir uma [operação de troca](../app-service-web/web-sites-staged-publishing.md#Swap) entre a transição e produção ranhuras.  
* As definições de temporária incluem o nome e a ranhura de tooa temporária. Por isso, quando o bloco de transição de Olá obtém alternado em produção, irá herdar definições da aplicação Olá Local Cache. Olá recentemente alternados ranhura será executada em relação a cache local Olá após alguns minutos e preparada cópias de segurança como parte de aquecimento de ranhura após a troca de produção. Por isso, quando a troca de ranhura Olá estiver concluída, a ranhura de produção estarão em execução em relação a cache local Olá.

## <a name="frequently-asked-questions-faq"></a>Perguntas mais frequentes (FAQ)
### <a name="how-can-i-tell-if-local-cache-applies-toomy-web-app"></a>Como posso saber se a Local Cache aplica toomy web aplicação?
Se a sua aplicação web precisa de um arquivo de conteúdo de elevado desempenho e fiável, não utiliza dados críticos de toowrite do arquivo de conteúdo de Olá no tempo de execução e é inferior a 2 GB de tamanho total, em seguida, Olá resposta é "Sim"! tooget Olá total tamanho das suas pastas de /site e /siteextensions, pode utilizar a extensão de site Olá "Utilização do disco de aplicações de Web do Azure".  

### <a name="how-can-i-tell-if-my-site-has-switched-toousing-local-cache"></a>Como posso saber se o meu site mudou toousing Local Cache?
Se estiver a utilizar a funcionalidade de Local Cache Olá com ambientes de teste, operação de troca de Olá não será concluída até que a Local Cache está preparada. toocheck se o seu site for executado relativamente a Local Cache, pode verificar a variável de ambiente de processo de trabalho de Olá `WEBSITE_LOCALCACHE_READY`. Utilize as instruções de Olá no Olá [variável de ambiente de processo de trabalho](https://github.com/projectkudu/kudu/wiki/Process-Threads-list-and-minidump-gcdump-diagsession#process-environment-variable) tooaccess página Olá variável de ambiente de processo de trabalho em várias instâncias.  

### <a name="i-just-published-new-changes-but-my-web-app-does-not-seem-toohave-them-why"></a>Posso apenas publicou novas alterações, mas a minha aplicação web não está toohave-los. Porquê?
Se a aplicação web utiliza a Local Cache, em seguida, é necessário toorestart as alterações mais recentes do site tooget Olá. Não pretende o site de produção do toopublish alterações tooa? Consulte as opções de ranhura Olá na secção de práticas de melhor anterior de Olá.

### <a name="where-are-my-logs"></a>Onde estão os meus registos?
Com a Cache Local, as pastas de dados e registos de ter um aspeto ligeiramente diferentes. No entanto, hello estrutura do seu permanece subpastas Olá mesmo, exceto que subpastas Olá são nestled sob uma subpasta com Olá formatar "Identificador exclusivo de VM" + o carimbo de data / hora.

### <a name="i-have-local-cache-enabled-but-my-web-app-still-gets-restarted-why-is-that-i-thought-local-cache-helped-with-frequent-app-restarts"></a>Tenho de Cache Local ativada, mas a minha aplicação web ainda obtém reiniciada. Por que motivo é que? Posso considerar o que ajudou a Local Cache com o reinício da aplicação frequentes.
Local Cache ajudar a impedir o reinício da aplicação web relacionadas com o armazenamento. No entanto, a aplicação web foi ainda são submetidos a reinícios durante as atualizações de infraestrutura planeada de Olá VM. Olá geral reinícios de aplicação experiência com a Cache Local ativado devem ser menos.

### <a name="does-local-cache-exclude-any-directories-from-being-copied-toohello-faster-local-drive"></a>Local Cache excluir os diretórios de ser copiados unidade local mais rápida de toohello?
Como parte do passo de Olá que copia os conteúdos de armazenamento Olá qualquer pasta denominada repositório será excluída. Isto ajuda-o com cenários em que o conteúdo do site pode conter um repositório de controlo de origem que pode não ser necessária na operação de tooday dia da aplicação web de Olá. 
