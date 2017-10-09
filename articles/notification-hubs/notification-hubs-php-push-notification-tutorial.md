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
# <a name="how-toouse-notification-hubs-from-php"></a><span data-ttu-id="d78dd-103">Como toouse Notification Hubs de PHP</span><span class="sxs-lookup"><span data-stu-id="d78dd-103">How toouse Notification Hubs from PHP</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="d78dd-104">Pode aceder a todas as funcionalidades de Hubs de notificação de um back-end de Java/PHP/Ruby utilizando a interface de REST de Hub de notificação de Olá conforme descrito no tópico do MSDN Olá [APIs REST do Notification Hubs](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="d78dd-104">You can access all Notification Hubs features from a Java/PHP/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span>

<span data-ttu-id="d78dd-105">Neste tópico mostram como:</span><span class="sxs-lookup"><span data-stu-id="d78dd-105">In this topic we show how to:</span></span>

* <span data-ttu-id="d78dd-106">Criar um cliente REST para funcionalidades de Notification Hubs do PHP;</span><span class="sxs-lookup"><span data-stu-id="d78dd-106">Build a REST client for Notification Hubs features in PHP;</span></span>
* <span data-ttu-id="d78dd-107">Siga Olá [tutorial de introdução](notification-hubs-ios-apple-push-notification-apns-get-started.md) para a sua plataforma móvel escolhidas, implementar a parte de back-end Olá no PHP.</span><span class="sxs-lookup"><span data-stu-id="d78dd-107">Follow hello [Get started tutorial](notification-hubs-ios-apple-push-notification-apns-get-started.md) for your mobile platform of choice, implementing hello back-end portion in PHP.</span></span>

## <a name="client-interface"></a><span data-ttu-id="d78dd-108">Interface do cliente</span><span class="sxs-lookup"><span data-stu-id="d78dd-108">Client interface</span></span>
<span data-ttu-id="d78dd-109">interface de principal do cliente Olá pode fornecer Olá mesmos métodos que estão disponíveis no Olá [SDK .NET Dosnotification Hubs](http://msdn.microsoft.com/library/jj933431.aspx), esta ação irá permitir toodirectly traduzir todos os tutoriais de Olá e amostras atualmente disponíveis neste site, e contribuídos por Comunidade Olá no Olá internet.</span><span class="sxs-lookup"><span data-stu-id="d78dd-109">hello main client interface can provide hello same methods that are available in hello [.NET Notification Hubs SDK](http://msdn.microsoft.com/library/jj933431.aspx), this will allow you toodirectly translate all hello tutorials and samples currently available on this site, and contributed by hello community on hello internet.</span></span>

<span data-ttu-id="d78dd-110">Pode encontrar todos os código Olá disponível no Olá [exemplo de wrapper do PHP REST].</span><span class="sxs-lookup"><span data-stu-id="d78dd-110">You can find all hello code available in hello [PHP REST wrapper sample].</span></span>

<span data-ttu-id="d78dd-111">Por exemplo, toocreate um cliente:</span><span class="sxs-lookup"><span data-stu-id="d78dd-111">For example, toocreate a client:</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="d78dd-112">toosend uma notificação de nativa do iOS:</span><span class="sxs-lookup"><span data-stu-id="d78dd-112">toosend an iOS native notification:</span></span>

    $notification = new Notification("apple", '{"aps":{"alert": "Hello!"}}');
    $hub->sendNotification($notification, null);

## <a name="implementation"></a><span data-ttu-id="d78dd-113">Implementação</span><span class="sxs-lookup"><span data-stu-id="d78dd-113">Implementation</span></span>
<span data-ttu-id="d78dd-114">Se ainda não fez, siga a nossa [tutorial de introdução] até toohello última seção onde tenha tooimplement Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="d78dd-114">If you did not already, please follow our [Get started tutorial] up toohello last section where you have tooimplement hello back-end.</span></span>
<span data-ttu-id="d78dd-115">Além disso, se pretender que pode utilizar código de Olá Olá [exemplo de wrapper do PHP REST] e aceda diretamente toohello [tutorial Olá concluída](#complete-tutorial) secção.</span><span class="sxs-lookup"><span data-stu-id="d78dd-115">Also, if you want you can use hello code from hello [PHP REST wrapper sample] and go directly toohello [Complete hello tutorial](#complete-tutorial) section.</span></span>

<span data-ttu-id="d78dd-116">Todos os Olá tooimplement detalhes um wrapper REST completo pode ser encontrado no [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span><span class="sxs-lookup"><span data-stu-id="d78dd-116">All hello details tooimplement a full REST wrapper can be found on [MSDN](http://msdn.microsoft.com/library/dn530746.aspx).</span></span> <span data-ttu-id="d78dd-117">Nesta secção dita implementação PHP Olá Olá passos principais necessário tooaccess pontos finais REST de Hubs de notificação:</span><span class="sxs-lookup"><span data-stu-id="d78dd-117">In this section we will describe hello PHP implementation of hello main steps required tooaccess Notification Hubs REST endpoints:</span></span>

1. <span data-ttu-id="d78dd-118">Analisar cadeia de ligação de Olá</span><span class="sxs-lookup"><span data-stu-id="d78dd-118">Parse hello connection string</span></span>
2. <span data-ttu-id="d78dd-119">Gerar o token de autorização de Olá</span><span class="sxs-lookup"><span data-stu-id="d78dd-119">Generate hello authorization token</span></span>
3. <span data-ttu-id="d78dd-120">Efetuar a chamada de Olá HTTP</span><span class="sxs-lookup"><span data-stu-id="d78dd-120">Perform hello HTTP call</span></span>

### <a name="parse-hello-connection-string"></a><span data-ttu-id="d78dd-121">Analisar cadeia de ligação de Olá</span><span class="sxs-lookup"><span data-stu-id="d78dd-121">Parse hello connection string</span></span>
<span data-ttu-id="d78dd-122">Eis Olá classe principal implementar Olá cliente, cujo construtor que analisa a cadeia de ligação de Olá:</span><span class="sxs-lookup"><span data-stu-id="d78dd-122">Here is hello main class implementing hello client, whose constructor that parses hello connection string:</span></span>

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


### <a name="create-security-token"></a><span data-ttu-id="d78dd-123">Criar o token de segurança</span><span class="sxs-lookup"><span data-stu-id="d78dd-123">Create security token</span></span>
<span data-ttu-id="d78dd-124">estão disponíveis detalhes Olá de criação de token de segurança de Olá [aqui](http://msdn.microsoft.com/library/dn495627.aspx).</span><span class="sxs-lookup"><span data-stu-id="d78dd-124">hello details of hello security token creation are available [here](http://msdn.microsoft.com/library/dn495627.aspx).</span></span>
<span data-ttu-id="d78dd-125">Olá seguinte método tem toobe adicionado toohello **NotificationHub** com base no token de Olá toocreate de classe no Olá URI do pedido atual Olá e as credenciais de Olá extraídas da cadeia de ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="d78dd-125">hello following method has toobe added toohello **NotificationHub** class toocreate hello token based on hello URI of hello current request and hello credentials extracted from hello connection string.</span></span>

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

### <a name="send-a-notification"></a><span data-ttu-id="d78dd-126">Enviar uma notificação</span><span class="sxs-lookup"><span data-stu-id="d78dd-126">Send a notification</span></span>
<span data-ttu-id="d78dd-127">Em primeiro lugar, defina informe-numa classe que representa uma notificação.</span><span class="sxs-lookup"><span data-stu-id="d78dd-127">First, let us define a class representing a notification.</span></span>

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

<span data-ttu-id="d78dd-128">Esta classe é um contentor para um corpo de notificação nativo, ou um conjunto de propriedades no caso de uma notificação de modelo e um conjunto de cabeçalhos que contém o formato (plataforma nativa ou modelo) e propriedades específicos da plataforma (como a propriedade de expiração da Apple e cabeçalhos WNS).</span><span class="sxs-lookup"><span data-stu-id="d78dd-128">This class is a container for a native notification body, or a set of properties on case of a template notification, and a set of headers which contains format (native platform or template) and platform-specific properties (like Apple expiration property and WNS headers).</span></span>

<span data-ttu-id="d78dd-129">Consulte toohello [documentação de APIs de REST do Notification Hubs](http://msdn.microsoft.com/library/dn495827.aspx) e Olá formatos as plataformas específicas de notificação para Olá todas as opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="d78dd-129">Please refer toohello [Notification Hubs REST APIs documentation](http://msdn.microsoft.com/library/dn495827.aspx) and hello specific notification platforms' formats for all hello options available.</span></span>

<span data-ttu-id="d78dd-130">Armed com esta classe, pode agora escrever Olá envio métodos de notificação dentro Olá **NotificationHub** classe.</span><span class="sxs-lookup"><span data-stu-id="d78dd-130">Armed with this class, we can now write hello send notification methods inside of hello **NotificationHub** class.</span></span>

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

<span data-ttu-id="d78dd-131">Olá acima métodos enviar um HTTP POST pedido toohello /messages ponto final do seu hub de notificação, com o corpo correto Olá e notificação de Olá toosend de cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="d78dd-131">hello above methods send an HTTP POST request toohello /messages endpoint of your notification hub, with hello correct body and headers toosend hello notification.</span></span>

## <span data-ttu-id="d78dd-132"><a name="complete-tutorial"></a>Tutorial de Olá concluída</span><span class="sxs-lookup"><span data-stu-id="d78dd-132"><a name="complete-tutorial"></a>Complete hello tutorial</span></span>
<span data-ttu-id="d78dd-133">Agora pode concluir o tutorial de introdução Olá enviando uma notificação de Olá de um back-end do PHP.</span><span class="sxs-lookup"><span data-stu-id="d78dd-133">Now you can complete hello Get Started tutorial by sending hello notification from a PHP back-end.</span></span>

<span data-ttu-id="d78dd-134">Inicializar o cliente de Notification Hubs (substitua o nome de hub e a cadeia de ligação de Olá com as instruções na Olá [tutorial de introdução]):</span><span class="sxs-lookup"><span data-stu-id="d78dd-134">Initialize your Notification Hubs client (substitute hello connection string and hub name as instructed in hello [Get started tutorial]):</span></span>

    $hub = new NotificationHub("connection string", "hubname");    

<span data-ttu-id="d78dd-135">Em seguida, adicione o código de envio de Olá dependendo da sua plataforma móvel de destino.</span><span class="sxs-lookup"><span data-stu-id="d78dd-135">Then add hello send code depending on your target mobile platform.</span></span>

### <a name="windows-store-and-windows-phone-81-non-silverlight"></a><span data-ttu-id="d78dd-136">Loja Windows e Windows Phone 8.1 (não Silverlight)</span><span class="sxs-lookup"><span data-stu-id="d78dd-136">Windows Store and Windows Phone 8.1 (non-Silverlight)</span></span>
    $toast = '<toast><visual><binding template="ToastText01"><text id="1">Hello from PHP!</text></binding></visual></toast>';
    $notification = new Notification("windows", $toast);
    $notification->headers[] = 'X-WNS-Type: wns/toast';
    $hub->sendNotification($notification, null);

### <a name="ios"></a><span data-ttu-id="d78dd-137">iOS</span><span class="sxs-lookup"><span data-stu-id="d78dd-137">iOS</span></span>
    $alert = '{"aps":{"alert":"Hello from PHP!"}}';
    $notification = new Notification("apple", $alert);
    $hub->sendNotification($notification, null);

### <a name="android"></a><span data-ttu-id="d78dd-138">Android</span><span class="sxs-lookup"><span data-stu-id="d78dd-138">Android</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("gcm", $message);
    $hub->sendNotification($notification, null);

### <a name="windows-phone-80-and-81-silverlight"></a><span data-ttu-id="d78dd-139">Windows Phone 8.0 e 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="d78dd-139">Windows Phone 8.0 and 8.1 Silverlight</span></span>
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


### <a name="kindle-fire"></a><span data-ttu-id="d78dd-140">Kindle Fire</span><span class="sxs-lookup"><span data-stu-id="d78dd-140">Kindle Fire</span></span>
    $message = '{"data":{"msg":"Hello from PHP!"}}';
    $notification = new Notification("adm", $message);
    $hub->sendNotification($notification, null);

<span data-ttu-id="d78dd-141">Executar o seu código PHP deveria produzir agora uma notificação de apresentação no seu dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="d78dd-141">Running your PHP code should produce now a notification appearing on your target device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d78dd-142">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="d78dd-142">Next Steps</span></span>
<span data-ttu-id="d78dd-143">Este tópico é mostrado como toocreate um Java simple REST cliente para os Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="d78dd-143">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="d78dd-144">A partir daqui, pode:</span><span class="sxs-lookup"><span data-stu-id="d78dd-144">From here you can:</span></span>

* <span data-ttu-id="d78dd-145">Transferir Olá completa [exemplo de wrapper do PHP REST], que contém todo Olá o código acima.</span><span class="sxs-lookup"><span data-stu-id="d78dd-145">Download hello full [PHP REST wrapper sample], which contains all hello code above.</span></span>
* <span data-ttu-id="d78dd-146">Saber mais sobre os Notification Hubs a marcação de funcionalidade Olá [tutorial notícias de última hora]</span><span class="sxs-lookup"><span data-stu-id="d78dd-146">Continue learning about Notification Hubs tagging feature in hello [Breaking News tutorial]</span></span>
* <span data-ttu-id="d78dd-147">Saiba mais sobre a enviar os utilizadores de tooindividual notificações [tutorial notificam os utilizadores]</span><span class="sxs-lookup"><span data-stu-id="d78dd-147">Learn about pushing notifications tooindividual users in [Notify Users tutorial]</span></span>

<span data-ttu-id="d78dd-148">Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d78dd-148">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[exemplo de wrapper do PHP REST]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/notificationhubs-rest-php
[tutorial de introdução]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/

