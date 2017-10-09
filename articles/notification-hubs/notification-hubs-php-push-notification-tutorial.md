---
title: aaaHow toouse Notification Hubs com o PHP
description: Saiba como toouse Notification Hubs do Azure de um back-end do PHP.
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 0156f994-96d0-4878-b07b-49b7be4fd856
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: php
ms.devlang: php
ms.topic: article
ms.date: 06/07/2016
ms.author: yuaxu
ms.openlocfilehash: 6cd426286a684006a07867fcf44a8ff71be7efa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-php"></a>Como toouse Notification Hubs de PHP
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Pode aceder a todas as funcionalidades de Hubs de notificação de um back-end de Java/PHP/Ruby utilizando a interface de REST de Hub de notificação de Olá conforme descrito no tópico do MSDN Olá [APIs REST do Notification Hubs](http://msdn.microsoft.com/library/dn223264.aspx).

Neste tópico mostram como:

* Criar um cliente REST para funcionalidades de Notification Hubs do PHP;
* Siga Olá [tutorial de introdução](notification-hubs-ios-apple-push-notification-apns-get-started.md) para a sua plataforma móvel escolhidas, implementar a parte de back-end Olá no PHP.

## <a name="client-interface"></a>Interface do cliente
interface de principal do cliente Olá pode fornecer Olá mesmos métodos que estão disponíveis no Olá [SDK .NET Dosnotification Hubs](http://msdn.microsoft.com/library/jj933431.aspx), esta ação irá permitir toodirectly traduzir todos os tutoriais de Olá e amostras atualmente disponíveis neste site, e contribuídos por Comunidade Olá no Olá internet.

Pode encontrar todos os código Olá disponível no Olá [exemplo de wrapper do PHP REST].

Por exemplo, toocreate um cliente:

    $hub = new NotificationHub("connection string", "hubname");    

toosend uma notificação de nativa do iOS:

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a>Implementação
Se ainda não fez, siga a nossa [tutorial de introdução] até toohello última seção onde tenha tooimplement Olá back-end.
Além disso, se pretender que pode utilizar código de Olá Olá [exemplo de wrapper do PHP REST] e aceda diretamente toohello [tutorial Olá concluída](#complete-tutorial) secção.

Todos os Olá tooimplement detalhes um wrapper REST completo pode ser encontrado no [MSDN](http://msdn.microsoft.com/library/dn530746.aspx). Nesta secção dita implementação PHP Olá Olá passos principais necessário tooaccess pontos finais REST de Hubs de notificação:

1. Analisar cadeia de ligação de Olá
2. Gerar o token de autorização de Olá
3. Efetuar a chamada de Olá HTTP

### <a name="parse-hello-connection-string"></a>Analisar cadeia de ligação de Olá
Eis Olá classe principal implementar Olá cliente, cujo construtor que analisa a cadeia de ligação de Olá:

    class NotificationHub {
        const API_VERSION = "?api-version=2013-10";

        private $endpoint;
        private $hubPath;
        private $sasKeyName;
        private $sasKeyValue;

        function __construct($connectionString, $hubPath) {
            $this->hubPath = $hubPath;

            $this->parseConnectionString($connectionString);
        }

        private function parseConnectionString($connectionString) {
            $parts = explode(";", $connectionString);
            if (sizeof($parts) != 3) {
                throw new Exception("Error parsing connection string: " . $connectionString);
            }

            foreach ($parts as $part) {
                if (strpos($part, "Endpoint") === 0) {
                    $this->endpoint = "https" . substr($part, 11);
                } else if (strpos($part, "SharedAccessKeyName") === 0) {
                    $this->sasKeyName = substr($part, 20);
                } else if (strpos($part, "SharedAccessKey") === 0) {
                    $this->sasKeyValue = substr($part, 16);
                }
            }
        }
    }


### <a name="create-security-token"></a>Criar o token de segurança
estão disponíveis detalhes Olá de criação de token de segurança de Olá [aqui](http://msdn.microsoft.com/library/dn495627.aspx).
Olá seguinte método tem toobe adicionado toohello **NotificationHub** com base no token de Olá toocreate de classe no Olá URI do pedido atual Olá e as credenciais de Olá extraídas da cadeia de ligação de Olá.

    private function generateSasToken($uri) {
        $targetUri = strtolower(rawurlencode(strtolower($uri)));

        $expires = time();
        $expiresInMins = 60;
        $expires = $expires + $expiresInMins * 60;
        $toSign = $targetUri . "\n" . $expires;

        $signature = rawurlencode(base64_encode(hash_hmac('sha256', $toSign, $this->sasKeyValue, TRUE)));

        $token = "SharedAccessSignature sr=" . $targetUri . "&sig="
                    . $signature . "&se=" . $expires . "&skn=" . $this->sasKeyName;

        return $token;
    }

### <a name="send-a-notification"></a>Enviar uma notificação
Em primeiro lugar, defina informe-numa classe que representa uma notificação.

    class Notification {
        public $format;
        public $payload;

        # array with keynames for headers
        # Note: Some headers are mandatory: Windows: X-WNS-Type, WindowsPhone: X-NotificationType
        # Note: For Apple you can set Expiry with header: ServiceBusNotification-ApnsExpiry in W3C DTF, YYYY-MM-DDThh:mmTZD (for example, 1997-07-16T19:20+01:00).
        public $headers;

        function __construct($format, $payload) {
            if (!in_array($format, ["template", "apple", "windows", "gcm", "windowsphone"])) {
                throw new Exception('Invalid format: ' . $format);
            }

            $this->format = $format;
            $this->payload = $payload;
        }
    }

Esta classe é um contentor para um corpo de notificação nativo, ou um conjunto de propriedades no caso de uma notificação de modelo e um conjunto de cabeçalhos que contém o formato (plataforma nativa ou modelo) e propriedades específicos da plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).

Consulte toohello [documentação de APIs de REST do Notification Hubs](http://msdn.microsoft.com/library/dn495827.aspx) e Olá formatos as plataformas específicas de notificação para Olá todas as opções disponíveis.

Armed com esta classe, pode agora escrever Olá envio métodos de notificação dentro Olá **NotificationHub** classe.

    public function sendNotification($notification, $tagsOrTagExpression="") {
        if (is_array($tagsOrTagExpression)) {
            $tagExpression = implode(" || ", $tagsOrTagExpression);
        } else {
            $tagExpression = $tagsOrTagExpression;
        }

        # build uri
        $uri = $this->endpoint . $this->hubPath . "/messages" . NotificationHub::API_VERSION;
        $ch = curl_init($uri);

        if (in_array($notification->format, ["template", "apple", "gcm"])) {
            $contentType = "application/json";
        } else {
            $contentType = "application/xml";
        }

        $token = $this->generateSasToken($uri);

        $headers = [
            'Authorization: '.$token,
            'Content-Type: '.$contentType,
            'ServiceBusNotification-Format: '.$notification->format
        ];

        if ("" !== $tagExpression) {
            $headers[] = 'ServiceBusNotification-Tags: '.$tagExpression;
        }

        # add headers for other platforms
        if (is_array($notification->headers)) {
            $headers = array_merge($headers, $notification->headers);
        }

        curl_setopt_array($ch, array(
            CURLOPT_POST => TRUE,
            CURLOPT_RETURNTRANSFER => TRUE,
            CURLOPT_SSL_VERIFYPEER => FALSE,
            CURLOPT_HTTPHEADER => $headers,
            CURLOPT_POSTFIELDS => $notification->payload
        ));

        // Send hello request
        $response = curl_exec($ch);

        // Check for errors
        if($response === FALSE){
            throw new Exception(curl_error($ch));
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] <> 201) {
            throw new Exception('Error sending notificaiton: '. $info['http_code'] . ' msg: ' . $response);
        }
    } 

Olá acima métodos enviar um HTTP POST pedido toohello /messages ponto final do seu hub de notificação, com o corpo correto Olá e notificação de Olá toosend de cabeçalhos.

## <a name="complete-tutorial"></a>Tutorial de Olá concluída
Agora pode concluir o tutorial de introdução Olá enviando uma notificação de Olá de um back-end do PHP.

Inicializar o cliente de Notification Hubs (substitua o nome de hub e a cadeia de ligação de Olá com as instruções na Olá [tutorial de introdução]):

    $hub = new NotificationHub("connection string", "hubname");    

Em seguida, adicione o código de envio de Olá dependendo da sua plataforma móvel de destino.

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a>Loja Windows e Windows Phone 8.1 (não Silverlight)
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a>iOS
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a>Android
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a>Windows Phone 8.0 e 8.1 Silverlight
    $toast = '<?xml version="1.0" encoding="utf-8"?>' .
                '<wp:Notification xmlns:wp="WPNotification">' .
                   '<wp:Toast>' .
                        '<wp:Text1>Hello from PHP!</wp:Text1>' .
                   '</wp:Toast> ' .
                '</wp:Notification>';
    $notification = new Notification("windowsphone", $toast);
    $notification->headers[] = 'X-WindowsPhone-Target : toast';
    $notification->headers[] = 'X-NotificationClass : 2';
    $hub->sendNotification($notification, null);


### <a name="kindle-fire"></a>Kindle Fire
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

Executar o seu código PHP deveria produzir agora uma notificação de apresentação no seu dispositivo de destino.

## <a name="next-steps"></a>Passos Seguintes
Este tópico é mostrado como toocreate um Java simple REST cliente para os Notification Hubs. A partir daqui, pode:

* Transferir Olá completa [exemplo de wrapper do PHP REST], que contém todo Olá o código acima.
* Saber mais sobre os Notification Hubs a marcação de funcionalidade Olá [tutorial notícias de última hora]
* Saiba mais sobre a enviar os utilizadores de tooindividual notificações [tutorial notificam os utilizadores]

Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).

[exemplo de wrapper do PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[tutorial de introdução]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

