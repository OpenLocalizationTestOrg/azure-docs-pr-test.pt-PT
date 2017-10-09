---
title: aaaHow tooUse Twilio de voz e o SMS (PHP) | Microsoft Docs
description: "Saiba como toomake uma chamada telefónica e enviar um SMS mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de código escrito em PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Como tooUse Twilio de voz e capacidades de SMS do PHP
Este guia demonstra como serviço de programação de tarefas comuns tooperform com Olá Twilio API no Azure. cenários de Olá abrangidos incluem a efetuar uma chamada telefónica e enviar uma mensagem de serviço de mensagens curto (SMS). Para obter mais informações sobre Twilio e a utilização de voz e SMS nas suas aplicações, consulte Olá [passos](#NextSteps) secção.

## <a id="WhatIs"></a>O que é Twilio?
Twilio está a ligar a Olá futuro das comunicações de negócio, ativar voz tooembed de programadores, VoIP e de mensagens em aplicações. Estes virtualizar todos os infraestrutura necessária num ambiente baseado na nuvem, global, expor-lo através da plataforma de Olá Twilio comunicações API. As aplicações são simple toobuild e dimensionável. Desfrute de mais flexibilidade consigo pay-como vá preços e beneficiar da fiabilidade da nuvem.

**Voz do Twilio** permite toomake a aplicações e receber chamadas telefónicas. **Twilio SMS** permite toosend a aplicação e receba mensagens de texto. **Cliente do Twilio** permite-lhe toomake VoIP chamadas de qualquer telefone, o tablet ou o browser e suporta WebRTC.

## <a id="Pricing"></a>Preços do Twilio e ofertas especiais
Clientes do Azure recebem um [oferta especial](http://www.twilio.com/azure): complimentary $10 do Twilio crédito ao atualizar a sua conta do Twilio. Este crédito do Twilio podem ser aplicados tooany Twilio utilização ($10 crédito equivalente toosending máximo de 1000 mensagens SMS ou receção segurança too1000 minutos de voz, dependendo da localização Olá o destino de número e a mensagem ou a chamada telefónica de entrada). Resgatar este crédito do Twilio e começar a utilizar em: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Twilio é um serviço pay as you go. Existem não existem taxas de configuração e pode fechar a sua conta em qualquer altura. Pode encontrar mais detalhes em [preços do Twilio][twilio_pricing].

## <a id="Concepts"></a>Conceitos
Olá Twilio API é uma API RESTful que fornece uma funcionalidade SMS de voz e de aplicações. Bibliotecas de cliente estão disponíveis em vários idiomas; Para obter uma lista, consulte [Twilio as bibliotecas API][twilio_libraries].

Aspetos fundamentais da Olá Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Twilio verbos
Olá API faz com que o utilize do Twilio verbos; Por exemplo, Olá  **&lt;indiquem&gt;**  verbo dá instruções ao Twilio tooaudibly entregar uma mensagem durante uma chamada.

Olá segue-se uma lista de verbos do Twilio. Saiba mais sobre Olá outros verbos e funcionalidades através de [documentação do Twilio Markup Language](http://www.twilio.com/docs/api/twiml).

* **&lt;Marcação&gt;**: estabelece ligação telefónica de tooanother Olá autor da chamada.
* **&lt;Recolher&gt;**: recolhe dígitos numéricos introduzidos no teclado do telefone de Olá.
* **&lt;Hangup&gt;**: termina uma chamada.
* **&lt;Reproduzir&gt;**: desempenha um ficheiro de áudio.
* **&lt;Colocar em pausa&gt;**: silenciosamente aguarda que um número de segundos especificado.
* **&lt;Registo&gt;**: regista voz invocadora Olá e devolve um URL de um ficheiro que contém a gravação de Olá.
* **&lt;Redirecionar&gt;**: transfere o controlo de uma chamada ou SMS toohello TwiML um URL diferente.
* **&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem a faturação
* **&lt;Diga&gt;**: converte texto toospeech que é efetuada numa chamada.
* **&lt;SMS&gt;**: envia uma mensagem SMS.

### <a id="TwiML"></a>TwiML
TwiML é um conjunto de instruções baseado em XML com base no verbos de Twilio Olá que o informam Twilio como tooprocess uma chamada ou SMS.

Por exemplo, Olá seguir TwiML teria de converter o texto de Olá **Olá mundo** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Quando as chamadas de aplicação Olá Twilio API, um dos parâmetros de API de Olá é Olá URL que devolve Olá TwiML resposta. Para fins de desenvolvimento, pode utilizar os URLs do Twilio fornecidos pelo tooprovide Olá TwiML as respostas utilizadas pelas suas aplicações. Também pode alojar as suas próprias as respostas hello URLs tooproduce TwiML e outra opção consiste toouse Olá **TwiMLResponse** objeto.

Para obter mais informações sobre Twilio verbos, os respetivos atributos e TwiML, consulte [TwiML][twiml]. Para obter informações adicionais sobre Olá API do Twilio, consulte [Twilio API][twilio_api].

## <a id="CreateAccount"></a>Criar uma conta do Twilio
Quando estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio]. Pode começar com uma conta gratuita e atualize a sua conta mais tarde.

Quando se inscreve para uma conta do Twilio, receberá um ID de conta e um token de autenticação. Ambos irão ser chamadas de API do Twilio toomake necessários. tooprevent não autorizado aceder à conta tooyour, mantenha o seu token de autenticação segura. O seu ID de conta e a autenticação de token são visíveis em Olá [página de conta do Twilio][twilio_account], na Olá campos com a etiqueta **SID da conta** e **AUTH TOKEN**, respetivamente.

## <a id="create_app"></a>Criar uma aplicação PHP
Uma aplicação PHP que utiliza o serviço de Twilio Olá e está em execução no Azure é não diferente de qualquer outra aplicação PHP que utiliza Olá Twilio serviço. Enquanto os serviços de Twilio são baseado em REST e podem ser chamados a partir do PHP de várias formas, este artigo foca-se na forma como toouse Twilio serviços com [Twilio biblioteca para que o PHP a partir do GitHub][twilio_php]. Para obter mais informações sobre como utilizar a biblioteca de Twilio Olá para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Instruções detalhadas para criar e implementar uma tooAzure de aplicação do Twilio/PHP estão disponíveis em [como tooMake Twilio de utilização de uma chamada telefónica numa aplicação PHP no Azure][howto_phonecall_php].

## <a id="configure_app"></a>Configurar a sua aplicação tooUse Twilio bibliotecas
Pode configurar a sua biblioteca de Twilio aplicação toouse Olá para PHP de duas formas:

1. Transferir a biblioteca de Twilio Olá para PHP a partir do GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e adicione Olá **serviços** aplicação tooyour de diretório.
   
    -OU-
2. Instale a biblioteca de Twilio Olá para PHP como um pacote PEAR. Podem ser instalado com Olá os seguintes comandos:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Depois de ter instalada a biblioteca de Twilio Olá para PHP, em seguida, pode adicionar um **require_once** declaração, Olá parte superior do seu PHP ficheiros de biblioteca de Olá tooreference:

        require_once 'Services/Twilio.php';

Para obter mais informações, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Como: efetuar uma chamada de saída
Olá seguinte mostra como uma saída de toomake chamada utilizando Olá **Services_Twilio** classe. Este código também utiliza um Olá de tooreturn Twilio fornecidos pelo site resposta Twilio Markup Language (TwiML). Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que verifique Olá **de** número para o seu código de Olá do Twilio conta toorunning anterior de telefone.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Conforme mencionado, este código utiliza um Olá de tooreturn Twilio fornecidos pelo site TwiML resposta. Em vez disso, pode utilizar o seus próprios Olá tooprovide de site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas do seu próprio Web Site](#howto_provide_twiml_responses).

* **Tenha em atenção**: tootroubleshoot erros de validação de certificado SSL, consulte [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Como: enviar uma mensagem SMS
Olá seguinte mostra como toosend uma mensagem SMS utilizando Olá **Services_Twilio** classe. Olá **de** número é fornecido pela Twilio para avaliação contas toosend mensagens SMS. Olá **para** número tem de ser verificado para o seu código de Olá do Twilio conta toorunning anterior.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Como: forneça TwiML respostas a partir do seu próprio site
Quando inicia a sua aplicação toohello uma chamada de API do Twilio, Twilio enviará o seu URL de tooa pedido que é esperado tooreturn uma resposta de TwiML. exemplo de Olá acima utiliza Olá Twilio URL fornecido pelo [http://twimlets.com/message][twimlet_message_url]. (Embora TwiML está concebido para utilização por Twilio, pode ver Olá-lo no seu browser. Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio `<Response>` elemento; como outro exemplo, clique em [http://twimlets.com/message? Mensagem % 5B0 %5 D = Olá % 20World] [ twimlet_message_url_hello_world] toosee um `<Response>` elemento que contenha um `<Say>` elemento.)

Em vez de depender Olá Twilio URL fornecido pelo, pode criar o seu próprio site, que devolve as respostas de HTTP. Pode criar site Olá em qualquer idioma que devolve respostas XML; Este tópico parte do princípio de que irá utilizar Olá toocreate do PHP TwiML.

Olá PHP página resultados numa resposta TwiML que indica que os seguintes **Olá mundo** na chamada de Olá.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Como pode ver do exemplo Olá acima, Olá TwiML resposta é simplesmente um documento XML. Biblioteca do Twilio Olá para PHP contém classes que irão gerar TwiML por si. exemplo de Olá abaixo produz resposta equivalente Olá, conforme mostrado acima, mas utiliza Olá **serviços\_Twilio\_Twiml** classe na biblioteca do Twilio Olá para PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Para mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Assim que tiver a sua página PHP configurar respostas de TwiML tooprovide, utilize Olá URL da página PHP Olá como Olá URL transmitido Olá `Services_Twilio->account->calls->create` método. Por exemplo, se tiver uma aplicação Web com o nome **MyTwiML** tooan implementado Azure serviço alojado, não sendo nome Olá da página PHP Olá **mytwiml.php**, Olá URL pode ser transmitido demasiado **Services_ Twilio-conta > -> chamadas -> criar** conforme mostrado no seguinte exemplo de Olá:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Para obter informações adicionais sobre a utilização do Twilio no Azure com o PHP, consulte [como tooMake Twilio de utilização de uma chamada telefónica numa aplicação PHP no Azure][howto_phonecall_php].

## <a id="AdditionalServices"></a>Como: utilizar os serviços do Twilio adicionais
Além disso exemplos toohello mostrados aqui, que twilio oferece as APIs baseadas na web que pode utilizar funcionalidades de Twilio adicionais tooleverage da sua aplicação do Azure. Para mais informações, consulte Olá [documentação da API do Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Passos Seguintes
Agora que aprendeu as noções básicas de Olá de Olá Twilio serviço, siga estas toolearn ligações mais:

* [Diretrizes de segurança do Twilio][twilio_security_guidelines]
* [De Twilio HowTo e código de exemplo][twilio_howtos]
* [Tutoriais de início rápido do Twilio][twilio_quickstarts] 
* [Twilio no GitHub][twilio_on_github]
* [Fale com tooTwilio suporte][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
