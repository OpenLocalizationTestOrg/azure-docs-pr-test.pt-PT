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
# <a name="how-toomake-a-phone-call-using-twilio-in-a-php-application-on-azure"></a>Como tooMake Twilio de utilização de uma chamada telefónica numa aplicação PHP no Azure
Olá exemplo seguinte mostra como pode utilizar o Twilio toomake uma chamada de uma página web PHP alojado no Azure. aplicação resultante Olá pedirá utilizador Olá para os valores de chamada telefónica, conforme mostrado na seguinte captura de ecrã de Olá.

![Formato de chamada do Azure utilizando Twilio e PHP][twilio_php]

Vai precisar toodo Olá seguinte código de Olá toouse neste tópico:

1. Adquirir uma conta do Twilio e a autenticação de token da sua [Twilio consola][twilio_console]. tooget ao Twilio, avaliar preços em [http://www.twilio.com/pricing][twilio_pricing]. Pode inscrever-se para uma conta de avaliação em [https://www.twilio.com/try-twilio][try_twilio].
2. Obter Olá [Twilio biblioteca para PHP](https://github.com/twilio/twilio-php) ou instalá-lo como um pacote PEAR. Para obter mais informações, consulte Olá [ficheiro Leia-me](https://github.com/twilio/twilio-php/blob/master/README.md).
3. Instale Olá Azure SDK para PHP. Para uma descrição geral Olá SDK e instruções sobre como instalá-lo, consulte [configurar Olá Azure SDK para PHP](app-service-web/web-sites-php-mysql-deploy-use-git.md)

## <a name="create-a-web-form-for-making-a-call"></a>Criar um formulário web para efetuar uma chamada
código de Olá HTML a seguir mostra como toobuild uma página web (**callform.html**) que obtém dados de utilizador para efetuar uma chamada:

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

## <a name="create-hello-code-toomake-hello-call"></a>Criação de Olá código toomake Olá chamada
Olá a seguir mostra código como toobuild **makecall.php**, o que é chamado quando o utilizador de Olá submete formulário Olá apresentado pela **callform.html**. código de Olá mostrado abaixo cria a mensagem de chamada de saudação e gera chamada Olá. Além disso, ser toouse se a conta do Twilio e a autenticação de token de Olá [Twilio consola] [ twilio_console] em vez de valores de marcador de posição de Olá atribuídos demasiado**$sid** e **$token** no código Olá abaixo.

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

Além disso toomaking Olá chamada, **makecall.php** apresenta alguns metadados de chamada, conforme é mostrado na imagem de Olá abaixo. Para mais informações sobre os metadados de chamada, consulte [https://www.twilio.com/docs/api/rest/call#instance-properties][twilio_call_properties].

![Resposta de chamada do Azure utilizando Twilio e o PHP][twilio_php_response]

## <a name="run-hello-application"></a>Executar a aplicação Olá
passo seguinte Olá é toodeploy tooAzure a aplicação Web sites. Olá artigos que se seguem contêm informações de Olá para criar um Web site e implementar o seu código com o Git, FTP ou o WebMatrix (embora não todas as informações de cada artigo são relevantes):

* [Criar um Web Site do MySQL do PHP do Azure e implementar utilizando o Git](app-service-web/web-sites-php-mysql-deploy-use-git.md)
* [Criar um Site Web do Azure do PHP MySQL e implementar a utilizar FTP](app-service-web/web-sites-php-mysql-deploy-use-ftp.md)

## <a name="next-steps"></a>Passos seguintes
Este código foi fornecido tooshow a funcionalidades básicas utilizando Twilio no PHP no Azure. Antes de implementar tooAzure na produção, poderá ser útil tooadd mais processamento de erros ou outras funcionalidades. Por exemplo:

* Em vez de utilizar um formulário web, pode utilizar blobs de armazenamento do Azure ou números de telefone de toostore de base de dados SQL e chamar texto. Para obter informações sobre como utilizar o blobs storage do Azure no PHP, consulte [utilizando o armazenamento do Azure com as aplicações PHP][howto_blob_storage_php]. Para obter informações sobre como utilizar a base de dados SQL no PHP, consulte [utilizando a base de dados SQL com as aplicações PHP][howto_sql_azure_php].
* Olá **makecall.php** código utiliza Twilio URL fornecido pelo ([http://twimlets.com/message][twimlet_message_url]) tooprovide uma resposta do Twilio Markup Language (TwiML) que informa como Twilio tooproceed com chamada de Olá. Por exemplo, pode conter Olá TwiML que é devolvido um `<Say>` verbo que resulta em texto a ser ditas toohello destinatário da chamada. Em vez de utilizar Olá Twilio URL fornecido pelo, foi possível criar o pedido do seu próprio serviço toorespond tooTwilio; Para obter mais informações, consulte [como tooUse Twilio de voz e capacidades de SMS do PHP][howto_twilio_voice_sms_php]. Obter mais informações sobre TwiML podem ser encontradas em [http://www.twilio.com/docs/api/twiml][twiml]e mais informações sobre `<Say>` e outros verbos Twilio podem ser encontrados em [http:// www.twilio.com/Docs/API/twiml/Say][twilio_say].
* Leia as diretrizes de segurança do Twilio Olá em [https://www.twilio.com/docs/security][twilio_docs_security].

Para obter informações adicionais sobre Twilio, consulte [https://www.twilio.com/docs][twilio_docs].

## <a name="see-also"></a>Veja Também
* [Como tooUse Twilio de voz e capacidades de SMS do PHP](partner-twilio-php-how-to-use-voice-sms.md)

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
