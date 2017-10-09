---
title: "aaaHow toomake uma chamada telefónica do Twilio (PHP) | Microsoft Docs"
description: "Saiba como toomake uma chamada telefónica e enviar um SMS mensagem com o serviço de API do Twilio Olá no Azure. São exemplos para aplicação PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 44e35adc-be06-4700-beee-8c9e2c20c540
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: e6fecc345bf9ae787d14d533bd8d96b175c2453b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a><span data-ttu-id="0e8bd-104">Como tooMake Twilio de utilização de uma chamada telefónica numa aplicação PHP no Azure</span><span class="sxs-lookup"><span data-stu-id="0e8bd-104">How tooMake a Phone Call Using Twilio in a PHP Application on Azure</span></span>
<span data-ttu-id="0e8bd-105">Olá exemplo seguinte mostra como pode utilizar o Twilio toomake uma chamada de uma página web PHP alojado no Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-105">hello following example shows you how you can use Twilio toomake a call from a PHP web page hosted in Azure.</span></span> <span data-ttu-id="0e8bd-106">aplicação resultante Olá pedirá utilizador Olá para os valores de chamada telefónica, conforme mostrado na seguinte captura de ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-106">hello resulting application will prompt hello user for phone call values, as shown in hello following screen shot.</span></span>

![Formato de chamada do Azure utilizando Twilio e PHP][twilio_php]

<span data-ttu-id="0e8bd-108">Vai precisar toodo Olá seguinte código de Olá toouse neste tópico:</span><span class="sxs-lookup"><span data-stu-id="0e8bd-108">You'll need toodo hello following toouse hello code in this topic:</span></span>

1. <span data-ttu-id="0e8bd-109">Adquirir uma conta do Twilio e a autenticação de token da sua [Twilio consola][twilio_console].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-109">Acquire a Twilio account and authentication token from your [Twilio Console][twilio_console].</span></span> <span data-ttu-id="0e8bd-110">tooget ao Twilio, avaliar preços em [http://www.twilio.com/pricing][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-110">tooget started with Twilio, evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="0e8bd-111">Pode inscrever-se para uma conta de avaliação em [https://www.twilio.com/try-twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-111">You can sign up for a trial account at [https://www.twilio.com/try-twilio][try_twilio].</span></span>
2. <span data-ttu-id="0e8bd-112">Obter Olá [Twilio biblioteca para PHP](https://github.com/twilio/twilio-php) ou instalá-lo como um pacote PEAR.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-112">Obtain hello [Twilio library for PHP](https://github.com/twilio/twilio-php) or install it as a PEAR package.</span></span> <span data-ttu-id="0e8bd-113">Para obter mais informações, consulte Olá [ficheiro Leia-me](https://github.com/twilio/twilio-php/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="0e8bd-113">For more information, see hello [readme file](https://github.com/twilio/twilio-php/blob/master/README.md).</span></span>
3. <span data-ttu-id="0e8bd-114">Instale Olá Azure SDK para PHP.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-114">Install hello Azure SDK for PHP.</span></span> <span data-ttu-id="0e8bd-115">Para uma descrição geral Olá SDK e instruções sobre como instalá-lo, consulte [configurar Olá Azure SDK para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span><span class="sxs-lookup"><span data-stu-id="0e8bd-115">For an overview of hello SDK and instructions on installing it, see [Set up hello Azure SDK for PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)</span></span>

## <a name="create-a-web-form-for-making-a-call"></a><span data-ttu-id="0e8bd-116">Criar um formulário web para efetuar uma chamada</span><span class="sxs-lookup"><span data-stu-id="0e8bd-116">Create a web form for making a call</span></span>
<span data-ttu-id="0e8bd-117">código de Olá HTML a seguir mostra como toobuild uma página web (**callform.html**) que obtém dados de utilizador para efetuar uma chamada:</span><span class="sxs-lookup"><span data-stu-id="0e8bd-117">hello following HTML code shows how toobuild a web page (**callform.html**) that retrieves user data for making a call:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
  <title>Automated call form</title>
</head>
<body>
  <h1>Automated Call Form</h1>
  <p>Fill in all fields and click <b>Make this call</b>.</p>
  <form action="makecall.php" method="post">
    <table>
      <tr>
        <td>To:</td>
        <td><input name="callTo" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>From:</td>
        <td><input name="callFrom" size="50" type="text" value=""></td>
      </tr>
      <tr>
        <td>Call message:</td>
        <td><input name="callText" size="100" type="text" value="Hello. This is hello call text. Good bye."></td>
      </tr>
      <tr>
        <td colspan="2"><input type="submit" value="Make this call"></td>
      </tr>
    </table>
  </form><br>
</body>
</html>
```

## <a name="create-hello-code-toomake-hello-call"></a><span data-ttu-id="0e8bd-118">Criação de Olá código toomake Olá chamada</span><span class="sxs-lookup"><span data-stu-id="0e8bd-118">Create hello code toomake hello call</span></span>
<span data-ttu-id="0e8bd-119">Olá a seguir mostra código como toobuild **makecall.php**, o que é chamado quando o utilizador de Olá submete formulário Olá apresentado pela **callform.html**.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-119">hello following code shows how toobuild **makecall.php**, which is called when hello user submits hello form displayed by **callform.html**.</span></span> <span data-ttu-id="0e8bd-120">código de Olá mostrado abaixo cria a mensagem de chamada de saudação e gera chamada Olá.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-120">hello code shown below creates hello call message and generates hello call.</span></span> <span data-ttu-id="0e8bd-121">Além disso, ser toouse se a conta do Twilio e a autenticação de token de Olá [Twilio consola] [ twilio_console] em vez de valores de marcador de posição de Olá atribuídos demasiado**$sid** e **$token** no código Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-121">Also, be sure toouse your Twilio account and authentication token from hello [Twilio Console][twilio_console] instead of hello placeholder values assigned too**$sid** and **$token** in hello code below.</span></span>

```html
<html>
<head><title>Making call...</title></head>
<body>
<p>Your call is being made.</p>

<?php
require_once 'path/to/vendor/autoload.php';

$sid   = "your_account_sid";
$token = "your_authentication_token";

$from_number = $_POST['callFrom']; // Calls must be made from a registered Twilio number.
$to_number   = $_POST['callTo'];
$message     = $_POST['callText'];

$client = new Twilio\Rest\Client($sid, $token);

$call = $client->calls->create(
            $to_number,
            $from_number,
            array('url' => http://twimlets.com/message?Message=' . urlencode($message))
        );

echo "Call status: " . $call->status . "<br />";
echo "URI resource: " . $call->uri . "<br />";
?>
</body>
</html>
```

<span data-ttu-id="0e8bd-122">Além disso toomaking Olá chamada, **makecall.php** apresenta alguns metadados de chamada, conforme é mostrado na imagem de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-122">In addition toomaking hello call, **makecall.php** displays some call metadata, as is shown in hello image below.</span></span> <span data-ttu-id="0e8bd-123">Para mais informações sobre os metadados de chamada, consulte [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-123">For more information about call metadata, see [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].</span></span>

![Resposta de chamada do Azure utilizando Twilio e o PHP][twilio_php_response]

## <a name="run-hello-application"></a><span data-ttu-id="0e8bd-125">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="0e8bd-125">Run hello application</span></span>
<span data-ttu-id="0e8bd-126">passo seguinte Olá é toodeploy tooAzure a aplicação Web sites.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-126">hello next step is toodeploy your application tooAzure Websites.</span></span> <span data-ttu-id="0e8bd-127">Olá artigos que se seguem contêm informações de Olá para criar um Web site e implementar o seu código com o Git, FTP ou o WebMatrix (embora não todas as informações de cada artigo são relevantes):</span><span class="sxs-lookup"><span data-stu-id="0e8bd-127">hello following articles contain hello information for creating a website and deploying your code with Git, FTP, or WebMatrix (though not all information in each article is relevant):</span></span>

* [<span data-ttu-id="0e8bd-128">Criar um Web Site do MySQL do PHP do Azure e implementar utilizando o Git</span><span class="sxs-lookup"><span data-stu-id="0e8bd-128">Create a PHP-MySQL Azure Web Site and deploy using Git</span></span>](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [<span data-ttu-id="0e8bd-129">Criar um Site Web do Azure do PHP MySQL e implementar a utilizar FTP</span><span class="sxs-lookup"><span data-stu-id="0e8bd-129">Create a PHP-MySQL Azure Web Site and Deploy Using FTP</span></span>](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a><span data-ttu-id="0e8bd-130">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0e8bd-130">Next steps</span></span>
<span data-ttu-id="0e8bd-131">Este código foi fornecido tooshow a funcionalidades básicas utilizando Twilio no PHP no Azure.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-131">This code was provided tooshow you basic functionality using Twilio in PHP on Azure.</span></span> <span data-ttu-id="0e8bd-132">Antes de implementar tooAzure na produção, poderá ser útil tooadd mais processamento de erros ou outras funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-132">Before deploying tooAzure in production, you may want tooadd more error handling or other features.</span></span> <span data-ttu-id="0e8bd-133">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0e8bd-133">For example:</span></span>

* <span data-ttu-id="0e8bd-134">Em vez de utilizar um formulário web, pode utilizar blobs de armazenamento do Azure ou números de telefone de toostore de base de dados SQL e chamar texto.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-134">Instead of using a web form, you could use Azure storage blobs or SQL Database toostore phone numbers and call text.</span></span> <span data-ttu-id="0e8bd-135">Para obter informações sobre como utilizar o blobs storage do Azure no PHP, consulte [utilizando o armazenamento do Azure com as aplicações PHP][howto_blob_storage_php].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-135">For information about using Azure storage blobs in PHP, see [Using Azure Storage with PHP Applications][howto_blob_storage_php].</span></span> <span data-ttu-id="0e8bd-136">Para obter informações sobre como utilizar a base de dados SQL no PHP, consulte [utilizando a base de dados SQL com as aplicações PHP][howto_sql_azure_php].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-136">For information about using SQL Database in PHP, see [Using SQL Database with PHP Applications][howto_sql_azure_php].</span></span>
* <span data-ttu-id="0e8bd-137">Olá **makecall.php** código utiliza Twilio URL fornecido pelo ([http://twimlets.com/message][twimlet_message_url]) tooprovide uma resposta do Twilio Markup Language (TwiML) que informa como Twilio tooproceed com chamada de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-137">hello **makecall.php** code uses Twilio-provided URL ([http://twimlets.com/message][twimlet_message_url]) tooprovide a Twilio Markup Language (TwiML) response that informs Twilio how tooproceed with hello call.</span></span> <span data-ttu-id="0e8bd-138">Por exemplo, pode conter Olá TwiML que é devolvido um `<Say>` verbo que resulta em texto a ser ditas toohello destinatário da chamada.</span><span class="sxs-lookup"><span data-stu-id="0e8bd-138">For example, hello TwiML that is returned can contain a `<Say>` verb that results in text being spoken toohello call recipient.</span></span> <span data-ttu-id="0e8bd-139">Em vez de utilizar Olá Twilio URL fornecido pelo, foi possível criar o pedido do seu próprio serviço toorespond tooTwilio; Para obter mais informações, consulte [como tooUse Twilio de voz e capacidades de SMS do PHP][howto_twilio_voice_sms_php].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-139">Instead of using hello Twilio-provided URL, you could build your own service toorespond tooTwilio's request; for more information, see [How tooUse Twilio for Voice and SMS Capabilities in PHP][howto_twilio_voice_sms_php].</span></span> <span data-ttu-id="0e8bd-140">Obter mais informações sobre TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml]e mais informações sobre `<Say>` e outros verbos Twilio podem ser encontrados em [http:// www.twilio.com/Docs/API/twiml/Say][twilio_say].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-140">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml], and more information about `<Say>` and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>
* <span data-ttu-id="0e8bd-141">Leia as diretrizes de segurança do Twilio Olá em [https://www.twilio.com/docs/security][twilio_docs_security].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-141">Read hello Twilio security guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>

<span data-ttu-id="0e8bd-142">Para obter informações adicionais sobre Twilio, consulte [https://www.twilio.com/docs][twilio_docs].</span><span class="sxs-lookup"><span data-stu-id="0e8bd-142">For additional information about Twilio, see [https://www.twilio.com/docs][twilio_docs].</span></span>

## <a name="see-also"></a><span data-ttu-id="0e8bd-143">Veja Também</span><span class="sxs-lookup"><span data-stu-id="0e8bd-143">See Also</span></span>
* [<span data-ttu-id="0e8bd-144">Como tooUse Twilio de voz e capacidades de SMS do PHP</span><span class="sxs-lookup"><span data-stu-id="0e8bd-144">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>](partner-twilio-php-how-to-use-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/docs/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
[twimlet_message_url]: http://twimlets.com/message
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api_service]: http://api.twilio.com
[build_php_azure_app]: http://azurephp.interoperabilitybridges.com/articles/build-and-deploy-a-windows-azure-php-application
[howto_twilio_voice_sms_php]: partner-twilio-php-how-to-use-voice-sms.md
[howto_blob_storage_php]: http://azure.microsoft.com/documentation/articles/storage-php-how-to-use-blobs/
[howto_sql_azure_php]: http://azure.microsoft.com/documentation/articles/sql-database-php-how-to-use/
[twilio_call_properties]: https://www.twilio.com/docs/api/rest/call#instance-properties
[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_php]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPCallForm.jpg
[twilio_php_response]: ./media/partner-twilio-php-make-phone-call/WA_TwilioPHPMakeCall.jpg
[website-git]: ./web-sites/web-sites-php-mysql-deploy-use-git.md
[website-ftp]: ./web-sites/web-sites-php-mysql-deploy-use-ftp.md
[twilio_php_github]: https://github.com/twilio/twilio-php
