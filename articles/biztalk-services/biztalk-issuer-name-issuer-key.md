---
title: aaaIssuer nome e a chave do emissor nos BizTalk Services | Microsoft Docs
description: Saiba como o nome do emissor tooretrieve e a chave do emissor para o Service Bus ou controlo de acesso (ACS) nos BizTalk Services. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk Services: Nome e Chave do Emissor

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

BizTalk Services do Azure utiliza Olá nome do emissor de barramento de serviço e chave do emissor e Olá nome do emissor de controlo de acesso e a chave do emissor. Especificamente:

| Tarefa | O nome do emissor e chave do emissor |
| --- | --- |
| Implementar a aplicação a partir do Visual Studio |Nome do emissor de controlo de acesso e a chave do emissor |
| Configurar Olá Portal de serviços do BizTalk do Azure |Nome do emissor de controlo de acesso e a chave do emissor |
| Criar o LOB reencaminhamentos com Olá adaptador dos BizTalk Services no Visual Studio |Nome do emissor de barramento de serviço e a chave do emissor |

Este tópico lista Olá passos tooretrieve Olá nome do emissor e chave do emissor. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nome do emissor de controlo de acesso e a chave do emissor
Olá nome do emissor de controlo de acesso e a chave do emissor são utilizados pelo seguinte Olá:

* A aplicação do BizTalk Service do Azure criada no Visual Studio: toosuccessfully implementar a aplicação do serviço de BizTalk no Visual Studio tooAzure, introduza Olá nome do emissor de controlo de acesso e a chave do emissor. 
* Olá Portal do Azure BizTalk Services: Quando cria um BizTalk Service e abrir Olá BizTalk Services Portal, o nome de emissor de controlo de acesso e a chave do emissor são registados automaticamente para as implementações com Olá os mesmos valores de controlo de acesso.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Obter Olá nome do emissor de controlo de acesso e a chave do emissor

toouse ACS para autenticação e get Olá valores de nome de emissor e chave do emissor, hello gerais passos incluem:

1. Instalar Olá [cmdlets Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Adicione a sua conta do Azure:`Add-AzureAccount`
3. Devolva o nome da sua subscrição:`get-azuresubscription`
4. Selecione a sua subscrição:`select-azuresubscription <name of your subscription>` 
5. Crie um novo espaço de nomes:`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Exemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Quando o espaço de nomes Olá novo ACS for criado (que pode demorar vários minutos), valores de nome de emissor e chave do emissor Olá estão listados na cadeia de ligação de Olá: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
Nome do emissor = SharedSecretIssuer  
Chave do emissor = SharedSecretKey

Mais informações sobre as Olá [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nome do emissor de barramento de serviço e a chave do emissor
Nome do emissor de barramento de serviço e a chave do emissor são utilizados pelo BizTalk Services do adaptador. No projeto dos BizTalk Services no Visual Studio, utilize o sistema de linha de negócio (LOB) do Olá BizTalk Services do adaptador tooconnect tooan no local. tooconnect, criar Olá LOB de reencaminhamento e introduza os detalhes de sistema LOB. Ao fazê-lo, é também introduzir Olá nome do emissor de barramento de serviço e a chave do emissor.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>Olá tooretrieve nome do emissor de barramento de serviço e a chave do emissor
1. Inicie sessão no toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação esquerdo Olá, selecione **Service Bus**.
3. Selecione o seu espaço de nomes. Na barra de tarefas Olá, selecione **informações de ligação**. Esta ação apresenta Olá **predefinido emissor** (nome do emissor) e **predefinido chave** (Issuer Key). Podem ser copiados os respetivos valores.  

toosummarize:  
Nome do emissor = emissor predefinido  
Chave do emissor = chave predefinida

## <a name="next"></a>Seguinte
Tópicos de BizTalk Services do Azure adicionais:

* [Instalar Olá SDK dos BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Tutoriais: BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Como posso começar a utilizar Olá SDK dos BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [BizTalk Services do Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Veja Também
* [Como: tooConfigure do serviço de gestão de ACS utilizar identidades do serviço](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Os BizTalk Services: Programador, básicas, Standard e Premium gráfico de edições](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk Services: Portal clássico do Azure através de aprovisionamento](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Serviços BizTalk: Gráfico de Estado de Aprovisionamento](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Serviços BizTalk: Separadores Dashboard, Monitorizar e Dimensionar](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Serviços BizTalk: Cópia de segurança e Restauro](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Serviços BizTalk: limitação](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

