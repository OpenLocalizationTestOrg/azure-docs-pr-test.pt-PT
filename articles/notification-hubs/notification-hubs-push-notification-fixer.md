---
title: "aaaAzure Notification Hubs – diretrizes de diagnóstico"
description: "Orientações sobre como toodiagnose comuns emite com Notification Hubs do Azure."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Hubs de notificação do Azure – diretrizes de diagnóstico
## <a name="overview"></a>Descrição geral
Uma das perguntas mais comuns Olá recebemos dos clientes de Notification Hubs do Azure é como toofigure enviados por que motivo não veem uma notificação enviada a partir do seu back-end da aplicação são apresentados no dispositivo de cliente olá - onde e por que razão as notificações foram removidas e como toofix isto. Neste artigo, irá passar por Olá vários motivos por que motivo notificações podem obter removidas ou não ficar nos dispositivos Olá. Podemos também irá procurar através de formas em que pode analisar e descobrir a causa de raiz de Olá. 

Primeiro de tudo, é fundamental toounderstand como Notification Hubs do Azure envia dispositivos toohello de notificações.
![][0]

Um fluxo de notificação de envio típica, mensagem de saudação é enviada do Olá **back-end da aplicação** demasiado**Azure Notification Hub (dos NH)** que por sua vez, tem algumas processamento em todos os registos de Olá tendo em Olá conta configurada etiquetas & toodetermine de expressões de etiqueta "destinos" ou seja, todos os Olá registos que necessitam de notificação de push de Olá tooreceive. Estes registos podem abranger em qualquer um ou todos os nossas as plataformas suportadas - iOS, Google, Windows, Windows Phone, Kindle e Baidu para Android na China. Assim que são estabelecidos destinos Olá, dos NH, em seguida, pushes saída notificações, dividir por vários lote de registos, específica da plataforma de dispositivo toohello **serviço de notificação Push (PNS)** -por exemplo, o APNS para Apple, o GCM para Google etc. Dos NH autentica com Olá que PNS correspondentes com base nas credenciais de Olá definido nas Olá Portal clássico do Azure na página de configurar o Notification Hub Olá. Olá PNS reencaminha, então, Olá notificações toohello respetivo **dispositivos cliente**. Esta é a plataforma de Olá notificações de push de toodeliver de forma e tenha em atenção que fase final de Olá da entrega de notificações ocorre entre plataforma Olá PNS e o dispositivo de Olá recomendadas. Assim que poderemos ter quatro componentes principais - *cliente*, *back-end da aplicação*, *Azure Notification Hubs (dos NH)* e *serviços de notificação Push (PNS)* e qualquer uma destas pode provocar notificações obter removidas. Obter mais detalhes sobre esta arquitetura não está disponível na [descrição geral dos Notification Hubs].

Toodeliver falha podem ocorrer notificações durante Olá inicial/testes fase que pode indicar um problema de configuração ou pode acontecer na produção em que todos ou alguns dos Olá notificações pode ser obter removido que indica que algumas aplicações mais aprofundada ou, problema de padrão de mensagens. Na secção de Olá, abaixo veremos vários cenários de notificações de ignorados de toohello rarer tipo comum, que algumas das quais pode encontrar óbvios e outros não, tanto que. 

## <a name="azure-notifications-hub-mis-configuration"></a>Configuração incorrecta do Hub de notificações do Azure
Os Hubs de notificação do Azure tem tooauthenticate próprio no contexto de Olá de toohello notificações de envio toosuccessfully capaz de programadores Olá aplicação toobe PNS correspondentes. Isto é possibilitado pela programador Olá criar uma conta de programador com respetiva plataforma Olá (Google, Apple, Windows etc) e, em seguida, registar a respetiva aplicação onde obter credenciais que precisam toobe configurado no portal de Olá em notificação Secção de configuração de hubs. Se não existem notificações estabelecem, através do primeiro passo deve ser tooensure que as credenciais corretas Olá estão configuradas no Olá Notification Hub correspondência destes com a aplicação Olá criado sob a conta de programador específico da plataforma. Encontrará nosso [obter tutoriais iniciado] toogo úteis sobre este processo de uma forma de passo a passo. Seguem-se algumas configurações incorrecta comuns:

1. **Geral**
   
    um) certifique-se de que o nome de hub de notificação (sem erros de digitação) é Olá mesmo:
   
   * Onde está a registar a partir do cliente de Olá, 
   * Onde está a enviar notificações de back-end de Olá,  
   * Onde configurou as credenciais PNS Olá e 
   * Olá, cujas credenciais SAS que configurou no cliente e Olá back-end. 
     
     b) certifique-se de que está a utilizar cadeias de configuração de SAS Olá corretas no cliente Olá e back-end da aplicação Olá. Como uma regra geral, tem de utilizar Olá **DefaultListenSharedAccessSignature** no cliente Olá e **DefaultFullSharedAccessSignature** no Olá aplicação back-end da (o que lhe dá toobe de permissão toosend capaz de notificação toohello dos NH)
2. **Configuração de Push serviço Apple Notification (APNS)**
   
    Tem de manter dois hubs – um para produção e outra para testes objetivo. Isto significa que o carregamento de certificado Olá que vai toouse no sandbox ambiente tooa separado hub- and certificado Olá que vai toouse no hub separado de tooa de produção. Não tente tipos diferentes de tooupload de certificados toohello mesmo hub, pois pode causar falhas de notificação para baixo de linha de Olá. Se der por si numa posição onde inadvertidamente carregou diferentes tipos de certificado toohello mesmo hub, recomenda-se toodelete Olá hub- and início raiz. Se, por algum motivo, não toodelete capaz de hub de Olá, em seguida, no Olá muito menos, terá de eliminar todos os registos existentes de Olá do hub de Olá. 
3. **Configuração do Google Cloud Messaging (GCM)** 
   
    um) certifique-se de que pretende ativar "Google Cloud Messaging para Android" sob o projeto de nuvem. 
   
    ![][2]
   
    b) certifique-se de que cria um "chave de servidor" durante a obtenção de credenciais de Olá qual dos NH utilizará tooauthenticate com o GCM. 
   
    ![][3]
   
    c) certifique-se de que configurou "ID do projeto" no cliente Olá que é uma entidade inteiramente numérica que pode obter a partir do dashboard de Olá:
   
    ![][1]

## <a name="application-issues"></a>Problemas de aplicações
1) **Etiquetas / expressões de etiqueta**

Se estiver a utilizar etiquetas ou etiqueta expressões toosegment seu público-alvo, é sempre possível que quando está a enviar notificação de Olá, não há nenhum destino que está a ser encontrado com base em expressões de etiquetas/etiqueta de Olá que estiver a especificar a chamada de envio. É melhor tooreview tooensure os registos que existem etiquetas que correspondem ao enviar a notificação e, em seguida, certifique-se de receção de notificações de Olá apenas a partir de clientes de Olá com esses registos. Por exemplo, Se todos os seus registos dos NH foram efetuados com diga a etiqueta "Política" e está a enviar uma notificação com etiqueta de "Desporto", este não será enviada tooany dispositivo. Caso complexo pode incluir expressões de etiqueta onde apenas registou com "A etiqueta" ou "Tag B", mas durante o envio de notificações, está a filtrar "Tag A e e etiqueta B". Olá automática diagnosticar secção sugestões abaixo, existem formas em que pode rever os registos, juntamente com etiquetas de Olá têm. 

2) **Problemas de modelo**

Se estiver a utilizar modelos e certifique-se de que está a seguir diretrizes de Olá descritas no [orientações de modelo]. 

3) **Registos inválidos**

Partindo do princípio de Olá que hub de notificação foi configurado corretamente e de quaisquer expressões de etiquetas/tag foram utilizadas corretamente resultavam localizar Olá de destinos válidos tem de notificações de Olá toowhich toobe enviado, dos NH desencadeado desativar várias de processamento de lotes em paralelo - cada lote enviar mensagens tooa conjunto de registos. 

> [!NOTE]
> Uma vez que vamos hello processamento em paralelo, não garantimos ordem Olá no qual Olá as notificações serão entregues. 
> 
> 

Agora o Hub de notificações do Azure está otimizado para um modelo de entrega de mensagem de "no máximo uma vez". Isto significa que tentarmos uma duplicação de Desativação, para que não existem notificações são fornecidas mais do que uma vez tooa dispositivo. tooensure isto, examine os registos de Olá e certifique-se de que apenas uma mensagem é enviado pelo identificador do dispositivo antes de enviar, na verdade, toohello de mensagem de Olá PNS. Como cada lote é enviado toohello PNS, que por sua vez está a aceitar e validar os registos de Olá, é possível que Olá PNS Deteta um erro com um ou mais dos registos de Olá num batch, devolve um erro tooAzure dos NH e interrompe o processamento deste modo, a remover que lote completamente. Isto é especialmente verdade com APNS que utiliza um protocolo de fluxo TCP. Embora iremos são otimizados no máximo uma vez entrega, neste caso, iremos remover Olá originar falha de registo da nossa base de dados e, em seguida, entrega de notificações de repetição para rest Olá dos dispositivos Olá esse batch.

Pode obter informações de erro para a tentativa de entrega falhada Olá contra um registo com Olá APIs REST do Azure Notification Hubs: [por mensagem de telemetria: obter telemetria de mensagem de notificação](https://msdn.microsoft.com/library/azure/mt608135.aspx) e [PNS comentários](https://msdn.microsoft.com/library/azure/mt705560.aspx). Consulte Olá [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) por exemplo de código.

## <a name="pns-issues"></a>Problemas PNS
Assim que foi recebida uma mensagem de notificação de saudação por Olá PNS respetivos, em seguida, que é o responsabilidade toodeliver Olá notificação toohello dispositivo. Os Hubs de notificação do Azure está fora do imagem de Olá aqui e não tem nenhum controlo no quando ou se notificação Olá vai toobe entregar toohello dispositivo. Uma vez que os serviços de notificação de plataforma Olá são pretty robustos, notificações tendem dispositivos de Olá tooreach dentro de alguns segundos de Olá PNS. Se hello PNS contudo é a limitação, em seguida, Notification Hubs do Azure aplicam-se um back exponencial desativar estratégia e se Olá PNS permanece inacessível para 30 minutos, em seguida, temos uma política no colocar tooexpire e remover permanentemente as mensagens. 

Se um PNS tenta toodeliver uma notificação mas Olá dispositivo estiver offline, notificação Olá é armazenada pelo Olá PNS por um período limitado de tempo e entregue toohello dispositivo quando ficar disponível. Apenas uma notificação recente para uma determinada aplicação está armazenada. Se várias notificações são enviadas enquanto Olá dispositivo estiver offline, cada nova notificação faz com que a notificação anterior Olá toobe rejeitados. Este comportamento manter apenas Olá mais recente notificação é referenciado tooas União de notificações no APNS e collapsing no GCM (que utiliza uma chave collapsing). Se o dispositivo de Olá permanecer offline durante muito tempo, são eliminadas quaisquer notificações que foram que está a ser armazenadas para o mesmo. Origem - [orientações APNS] & [orientações do GCM]

Com os Notification Hubs do Azure - pode transmitir uma chave de agregação através de um cabeçalho HTTP utilizando o Olá genérico `SendNotification` API (por exemplo, para o .NET SDK – `SendNotificationAsync`) que assume também os cabeçalhos de HTTP que são transmitidos como é toohello PNS correspondentes. 

## <a name="self-diagnose-tips"></a>Sugestões de diagnosticar automática
Aqui iremos irá examinar Olá vários meios toodiagnose e raiz causam problemas de Hub de notificação:

### <a name="verify-credentials"></a>Verificar credenciais
1. **Portal do programador PNS**
   
    Certifique-se ao hello respetivos PNS programador portal (WNS, APNS, GCM, etc.) utilizando a nossa [obter tutoriais iniciado].
2. **Portal clássico do Azure**
   
    Aceda toohello configurar separador tooreview e corresponde as credenciais de Olá com os obtidos a partir do portal de programador PNS Olá. 
   
    ![][4]

### <a name="verify-registrations"></a>Verifique os registos
1. **Visual Studio**
   
    Se utilizar o Visual Studio para o desenvolvimento pode ligar tooMicrosoft do Azure e ver e gerir um bunch dos serviços do Azure, incluindo o Hub de notificações "No Explorador de servidores". Isto é principalmente útil para o seu ambiente de desenvolvimento/teste. 
   
    ![][9]
   
    Pode ver e gerir todos os registos de Olá do seu hub são categorizados corretamente para o registo de plataforma, nativo ou modelo, qualquer etiquetas, identificador PNS, data de expiração de id e Olá do registo. Também pode editar um registo no momento de Olá - o que é útil diga se quiser tooedit quaisquer etiquetas. 
   
    ![][8]
   
   > [!NOTE]
   > Registos de tooedit de funcionalidades do Visual Studio só devem ser utilizados durante dev/teste com um número limitado de registos. Se for existe toofix uma necessidade dos registos em volume, considere utilizar uma funcionalidade de registo de exportação/importação de Olá descrita aqui - [exportação/importação de registos](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Explorador do Service Bus**
   
    Muitos clientes utilizam ServiceBus explorer descrito aqui - [Explorador de ServiceBus] para ver e gerir o seu hub de notificação. É um projeto de código aberto disponível a partir do code.microsoft.com - [código do Explorador de barramento de serviço]

### <a name="verify-message-notifications"></a>Certifique-se de notificações de mensagens
1. **Portal Clássico do Azure**
   
    Pode aceder toohello "Depuração" separador toosend teste notificações tooyour os clientes sem necessitar de qualquer back-end do serviço cópia de segurança e em execução. 
   
    ![][7]
2. **Visual Studio**
   
    Também pode enviar notificações de teste de comforts Olá do Visual Studio:
   
    ![][10]
   
    Pode ler mais em Olá Azure de Hub de notificação do Visual Studio explorer funcionalidade aqui- 
   
   * [Descrição geral do Explorador de servidor VS]
   * [Mensagem de blogue de Explorador de servidor VS - 1]
   * [Mensagem de blogue de Explorador de servidor VS - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Depurar falhas notificações / reveja o resultado da notificação
**Propriedade de EnableTestSend**

Enviar uma notificação através de Notification Hubs, inicialmente, apenas obtém colocados em fila cópias de segurança para toodo dos NH toofigure enviados todos os respetivos destinos de processamento e, em seguida, eventualmente dos NH envia-toohello PNS. Isto significa que quando estiver a utilizar a REST API ou de qualquer cliente Olá SDK, hello retorno com êxito do suas envio chamada apenas significa que Olá mensagem tem foi com êxito colocado em fila cópias de segurança com o Notification Hub. -Não atribua uma aprofundadas sobre o que aconteceu quando dos NH eventualmente obteve toosend Olá mensagem tooPNS. Se a sua notificação não é a chegar ao dispositivo de cliente Olá, há a possibilidade de que quando dos NH tentou toodeliver Olá mensagem tooPNS, Ocorreu um erro por exemplo, o tamanho de payload Olá excedeu o máximo de Olá permitido por Olá PNS ou credenciais Olá configuradas dos NH são tooget etc inválido. um aprofundadas sobre erros PNS Olá, ter introduzimos uma propriedade denominada [EnableTestSend funcionalidade]. Esta propriedade é ativada automaticamente quando enviar mensagens a partir do portal Olá ou o cliente do Visual Studio e, pelo que lhe permite toosee detalhada teste informações de depuração. Pode utilizá-lo através de APIs de colocar o exemplo de Olá de Olá SDK .NET onde se encontram disponíveis agora e será adicionada tooall SDKs do cliente eventualmente. toouse isto com chamada REST de Olá, basta acrescentar um parâmetro de cadeia de consulta chamado "teste" no fim de Olá do seu envio chamada por exemplo 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Exemplo (.NET SDK)*

Suponha que está a utilizar o .NET SDK toosend uma notificação de alerta nativo:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`irá simplesmente estado `Enqueued` no fim de Olá da execução de Olá sem qualquer aprofundadas sobre o que aconteceu tooyour push. Agora, pode utilizar Olá `EnableTestSend` booleana propriedade ao inicializar Olá `NotificationHubClient` e pode obter o estado detalhado sobre Olá PNS foram encontrados erros ao enviar a notificação de Olá. chamada de envio de Olá aqui irá demorar mais tempo tooreturn porque está a devolver apenas depois dos NH tem entregar o resultado da Olá notificação tooPNS toodetermine Olá. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Saída de exemplo*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Esta mensagem indica a credenciais inválidas estão configuradas no hub de notificação de Olá ou um problema com os registos de Olá no hub Olá e Olá recomendado decorrer teria de ser toodelete este registo e permitir que o cliente de Olá recriá-lo antes de enviar Olá mensagem. 

> [!NOTE]
> Tenha em atenção que utilizar Olá desta propriedade é limitado descontos elevados e, por isso, tem de utilizar isto apenas ambiente de desenvolvimento/teste com um conjunto limitado de registos. Iremos enviar apenas notificações de depuração too10 dispositivos. Além disso, temos um limite de processamento de depuração envia toobe 10 por minuto. 
> 
> 

### <a name="review-telemetry"></a>Reveja a telemetria
1. **Utilizar o Portal clássico do Azure**
   
    portal de Olá permite-lhe tooget uma rápida descrição geral de toda a atividade Olá no seu Hub de notificação. 
   
    a) a partir do separador de "dashboard" Olá, pode ver uma vista de agregados de registos de Olá, notificações, bem como de erros por plataforma. 
   
    ![][5]
   
    b) também pode adicionar vários outras plataforma métricas específicas de Olá ". o Monitor" separador tootake mais profundo ver particularmente quaisquer erros específicos de PNS devolvido quando dos NH tenta toosend Olá notificação toohello PNS. 
   
    ![][6]
   
    c) deve começar com rever Olá **mensagens a receber**, **operações de registo**, **notificações com êxito** e, em seguida, aceda Olá de tooreview tooper plataforma separador Erros específicos de PNS. 
   
    d) se tiver notificação Olá hub configurada incorretamente com definições de autenticação de Olá, em seguida, será apresentado o erro de autenticação de PNS. Este é o credenciais do PNS toocheck Olá um bom indicador. 

2) **Acesso programático**

Obter mais detalhes aqui- 

* [Acesso programático telemetria]
* [Acesso de telemetria através de exemplo APIs] 

> [!NOTE]
> Vários telemetria relacionada com funcionalidades como **registos de exportação/importação**, **telemetria acesso através de APIs** etc apenas estão disponíveis no escalão Standard. Se tentar toouse estas funcionalidades, se estiver na gratuito ou o escalão básico, em seguida, obterá o efeito de toothis de mensagem de exceção ao utilizar Olá SDK e um HTTP 403 (proibido) quando utilizá-los diretamente a partir de Olá REST APIs. Certifique-se de que tem de ter movidas para cima tooStandard camada através do Portal clássico do Azure.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[descrição geral dos Notification Hubs]: notification-hubs-push-notification-overview.md
[obter tutoriais iniciado]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[orientações de modelo]: https://msdn.microsoft.com/library/dn530748.aspx 
[orientações APNS]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[orientações do GCM]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[Explorador de ServiceBus]: http://msdn.microsoft.com/library/dn530751.aspx
[código do Explorador de barramento de serviço]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Descrição geral do Explorador de servidor VS]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[Mensagem de blogue de Explorador de servidor VS - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[Mensagem de blogue de Explorador de servidor VS - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend funcionalidade]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Acesso programático telemetria]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Acesso de telemetria através de exemplo APIs]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

