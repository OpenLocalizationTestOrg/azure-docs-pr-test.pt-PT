---
title: "aaaHow toouse Olá serviço de e-mail do SendGrid (PHP) | Microsoft Docs"
description: "Saiba como enviar correio eletrónico com Olá serviço de e-mail do SendGrid no Azure. Exemplos de código escrito em PHP."
documentationcenter: php
services: 
manager: sendgrid
editor: mollybos
author: thinkingserious
ms.assetid: 51a9928a-4c9e-4b0a-aca8-9a408aeb6f47
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork; matt.bernier@sendgrid.com
ms.openlocfilehash: 0076e56dc185cb8f52e629395e7d2c143cb5cfa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-sendgrid-email-service-from-php"></a><span data-ttu-id="7d8da-104">Como tooUse Olá SendGrid o serviço de E-Mail do PHP</span><span class="sxs-lookup"><span data-stu-id="7d8da-104">How tooUse hello SendGrid Email Service from PHP</span></span>
<span data-ttu-id="7d8da-105">Este guia demonstra como de programação de tarefas comuns tooperform com Olá SendGrid e-mail serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8da-105">This guide demonstrates how tooperform common programming tasks with hello SendGrid email service on Azure.</span></span> <span data-ttu-id="7d8da-106">Exemplos de Olá são escritos no PHP.</span><span class="sxs-lookup"><span data-stu-id="7d8da-106">hello samples are written in PHP.</span></span>
<span data-ttu-id="7d8da-107">Olá os cenários abrangidos incluem **construir e-mail**, **enviar correio eletrónico**, e **adicionar anexos**.</span><span class="sxs-lookup"><span data-stu-id="7d8da-107">hello scenarios covered include **constructing email**, **sending email**, and **adding attachments**.</span></span> <span data-ttu-id="7d8da-108">Para obter mais informações sobre SendGrid e enviar correio eletrónico, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="7d8da-108">For more information on SendGrid and sending email, see hello [Next Steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="7d8da-109">O que é Olá SendGrid serviço de E-Mail?</span><span class="sxs-lookup"><span data-stu-id="7d8da-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="7d8da-110">SendGrid é um [serviço baseado na nuvem e-mail] que fornece fiável [entrega de correio eletrónico transacional], escalabilidade e a análise em tempo real, juntamente com APIs flexíveis que o facilitar a integração personalizados.</span><span class="sxs-lookup"><span data-stu-id="7d8da-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="7d8da-111">Cenários comuns de utilização do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="7d8da-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="7d8da-112">Enviar automaticamente os recibos toocustomers</span><span class="sxs-lookup"><span data-stu-id="7d8da-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="7d8da-113">Administrar distribuição lista para enviar aos clientes i-fliers mensais e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="7d8da-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="7d8da-114">Recolher métricas em tempo real para coisas como bloqueado por correio eletrónico e a capacidade de resposta do cliente</span><span class="sxs-lookup"><span data-stu-id="7d8da-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="7d8da-115">Gerar relatórios toohelp identificar tendências</span><span class="sxs-lookup"><span data-stu-id="7d8da-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="7d8da-116">Pedidos de cliente de reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="7d8da-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="7d8da-117">Notificações de correio eletrónico da sua aplicação</span><span class="sxs-lookup"><span data-stu-id="7d8da-117">Email notifications from your application</span></span>

<span data-ttu-id="7d8da-118">Para obter mais informações, consulte [https://sendgrid.com][https://sendgrid.com].</span><span class="sxs-lookup"><span data-stu-id="7d8da-118">For more information, see [https://sendgrid.com][https://sendgrid.com].</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="7d8da-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="7d8da-119">Create a SendGrid Account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="using-sendgrid-from-your-php-application"></a><span data-ttu-id="7d8da-120">Utilizar SendGrid da sua aplicação PHP</span><span class="sxs-lookup"><span data-stu-id="7d8da-120">Using SendGrid from your PHP Application</span></span>
<span data-ttu-id="7d8da-121">A utilização de SendGrid numa aplicação PHP do Azure não requer nenhum especial codificação ou de configuração.</span><span class="sxs-lookup"><span data-stu-id="7d8da-121">Using SendGrid in an Azure PHP application requires no special configuration or coding.</span></span> <span data-ttu-id="7d8da-122">Uma vez SendGrid é um serviço, pode ser acedido em exatamente Olá mesma de forma a partir de uma aplicação na nuvem, pois pode partir de uma aplicação no local.</span><span class="sxs-lookup"><span data-stu-id="7d8da-122">Because SendGrid is a service, it can be accessed in exactly hello same way from a cloud application as it can from an on-premises application.</span></span>

## <a name="how-to-send-an-email"></a><span data-ttu-id="7d8da-123">Como: enviar uma mensagem de E-Mail</span><span class="sxs-lookup"><span data-stu-id="7d8da-123">How to: Send an Email</span></span>
<span data-ttu-id="7d8da-124">Pode enviar correio eletrónico através de SMTP ou Olá API Web fornecidos pelo SendGrid.</span><span class="sxs-lookup"><span data-stu-id="7d8da-124">You can send email using either SMTP or hello Web API provided by SendGrid.</span></span>

### <a name="smtp-api"></a><span data-ttu-id="7d8da-125">API DE SMTP</span><span class="sxs-lookup"><span data-stu-id="7d8da-125">SMTP API</span></span>
<span data-ttu-id="7d8da-126">e-mail de toosend através de Olá API de SMTP do SendGrid, utilize *Swift Mailer*, uma biblioteca baseado em componentes para enviar e-mails de aplicações PHP.</span><span class="sxs-lookup"><span data-stu-id="7d8da-126">toosend email using hello SendGrid SMTP API, use *Swift Mailer*, a component-based library for sending emails from PHP applications.</span></span> <span data-ttu-id="7d8da-127">Pode transferir Olá *Swift Mailer* biblioteca a partir de [http://swiftmailer.org/download] [ http://swiftmailer.org/download] v5.3.0 (utilizar [compositor] tooinstall SWIFT Mailer).</span><span class="sxs-lookup"><span data-stu-id="7d8da-127">You can download hello *Swift Mailer* library from [http://swiftmailer.org/download][http://swiftmailer.org/download] v5.3.0 (use [Composer] tooinstall Swift Mailer).</span></span> <span data-ttu-id="7d8da-128">Enviar correio eletrónico com biblioteca Olá implica a criação de instâncias do <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, e <span class="auto-style2">Swift\_mensagem </span> classes, definir as propriedades adequadas e, ao chamar o <span class="auto-style2">Swift\_Mailer::send</span> método.</span><span class="sxs-lookup"><span data-stu-id="7d8da-128">Sending email with hello library involves creating instances of the <span class="auto-style2">Swift\_SmtpTransport</span>, <span class="auto-style2">Swift\_Mailer</span>, and <span class="auto-style2">Swift\_Message</span> classes, setting the appropriate properties, and calling the <span class="auto-style2">Swift\_Mailer::send</span> method.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello receiver is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
     $html = "<html>
           <head></head>
           <body>
               <p>Hi!<br>
                   How are you?<br>
               </p>
           </body>
           </html>";
     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');
     // Email recipients
     $too= array(
           'john@contoso.com'=>'Destination 1 Name',
           'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
         // This will let us know how many users received this message
         echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
         echo "Something went wrong - ";
         print_r($failures);
     }

### <a name="web-api"></a><span data-ttu-id="7d8da-129">API Web</span><span class="sxs-lookup"><span data-stu-id="7d8da-129">Web API</span></span>
<span data-ttu-id="7d8da-130">Utilizar do PHP [curl função] [ curl function] através de correio eletrónico toosend Olá SendGrid Web API.</span><span class="sxs-lookup"><span data-stu-id="7d8da-130">Use PHP's [curl function][curl function] toosend email using hello SendGrid Web API.</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $params = array(
          'api_user' => $user,
          'api_key' => $pass,
          'to' => 'john@contoso.com',
          'subject' => 'testing from curl',
          'html' => 'testing body',
          'text' => 'testing body',
          'from' => 'anna@contoso.com',
       );

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

<span data-ttu-id="7d8da-131">API de Web do SendGrid é muito semelhante tooa REST API, que não esteja verdadeiramente uma API RESTful, uma vez que, na maioria das chamadas, ambos obter e verbos POST podem ser utilizados-no alternadamente.</span><span class="sxs-lookup"><span data-stu-id="7d8da-131">SendGrid's Web API is very similar tooa REST API, though it is not truly a RESTful API since, in most calls, both GET and POST verbs can be used interchangeably.</span></span>

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="7d8da-132">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="7d8da-132">How to: Add an Attachment</span></span>
### <a name="smtp-api"></a><span data-ttu-id="7d8da-133">API DE SMTP</span><span class="sxs-lookup"><span data-stu-id="7d8da-133">SMTP API</span></span>
<span data-ttu-id="7d8da-134">Enviar um anexo utilizando Olá SMTP API envolve uma linha adicional do script de exemplo de toohello de código para enviar um e-mail com Swift Mailer.</span><span class="sxs-lookup"><span data-stu-id="7d8da-134">Sending an attachment using hello SMTP API involves one additional line of code toohello example script for sending an email with Swift Mailer.</span></span>

    <?php
     include_once "vendor/autoload.php";
     /*
      * Create hello body of hello message (a plain-text and an HTML version).
      * $text is your plain-text email
      * $html is your html version of hello email
      * If hello reciever is able tooview html emails then only hello html
      * email will be displayed
      */
     $text = "Hi!\nHow are you?\n";
      $html = "<html>
          <head></head>
          <body>
             <p>Hi!<br>
                How are you?<br>
             </p>
          </body>
          </html>";

     // This is your From email address
     $from = array('someone@example.com' => 'Name tooAppear');

     // Email recipients
     $too= array(
          'john@contoso.com'=>'Destination 1 Name',
          'anna@contoso.com'=>'Destination 2 Name'
     );
     // Email subject
     $subject = 'Example PHP Email';

     // Login credentials
     $username = 'yoursendgridusername';
     $password = 'yourpassword';

     // Setup Swift mailer parameters
     $transport = Swift_SmtpTransport::newInstance('smtp.sendgrid.net', 587);
     $transport->setUsername($username);
     $transport->setPassword($password);
     $swift = Swift_Mailer::newInstance($transport);

     // Create a message (subject)
     $message = new Swift_Message($subject);

     // attach hello body of hello email
     $message->setFrom($from);
     $message->setBody($html, 'text/html');
     $message->setTo($to);
     $message->addPart($text, 'text/plain');
     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName("file_name"));

     // send message
     if ($recipients = $swift->send($message, $failures))
     {
          // This will let us know how many users received this message
          echo 'Message sent out too'.$recipients.' users';
     }
     // something went wrong =(
     else
     {
          echo "Something went wrong - ";
          print_r($failures);
     }

<span data-ttu-id="7d8da-135">linha de Olá adicionais de código é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7d8da-135">hello additional line of code is as follows:</span></span>

     $message->attach(Swift_Attachment::fromPath("path\to\file")->setFileName('file_name'));

<span data-ttu-id="7d8da-136">Esta linha de código chamadas Olá anexar método no <span class="auto-style2">Swift\_mensagem</span> de objeto e utiliza um método estático <span class="auto-style2">fromPath</span> no <span class="auto-style2">Swift\_anexo</span>tooget de classe e anexar uma mensagem de tooa do ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7d8da-136">This line of code calls hello attach method on the <span class="auto-style2">Swift\_Message</span> object and uses static method <span class="auto-style2">fromPath</span> on the <span class="auto-style2">Swift\_Attachment</span> class tooget and attach a file tooa message.</span></span>

### <a name="web-api"></a><span data-ttu-id="7d8da-137">API Web</span><span class="sxs-lookup"><span data-stu-id="7d8da-137">Web API</span></span>
<span data-ttu-id="7d8da-138">Enviar um anexo utilizando Olá Web API é muito semelhante toosending utilizando um e-mail Olá Web API.</span><span class="sxs-lookup"><span data-stu-id="7d8da-138">Sending an attachment using hello Web API is very similar toosending an email using hello Web API.</span></span> <span data-ttu-id="7d8da-139">No entanto, tenha em atenção que no exemplo de Olá que se segue, Olá parâmetro matriz tem de conter este elemento:</span><span class="sxs-lookup"><span data-stu-id="7d8da-139">However, note that in hello example that follows, hello parameter array must contain this element:</span></span>

    'files['.$fileName.']' => '@'.$filePath.'/'.$fileName

<span data-ttu-id="7d8da-140">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7d8da-140">Example:</span></span>

    <?php

     $url = 'https://api.sendgrid.com/';
     $user = 'USERNAME';
     $pass = 'PASSWORD';

     $fileName = 'myfile';
     $filePath = dirname(__FILE__);

     $params = array(
         'api_user' => $user,
         'api_key' => $pass,
         'to' =>'john@contoso.com',
         'subject' => 'test of file sends',
         'html' => '<p> hello HTML </p>',
         'text' => 'hello plain text',
         'from' => 'anna@contoso.com',
         'files['.$fileName.']' => '@'.$filePath.'/'.$fileName
     );

     print_r($params);

     $request = $url.'api/mail.send.json';

     // Generate curl request
     $session = curl_init($request);

     // Tell curl toouse HTTP POST
     curl_setopt ($session, CURLOPT_POST, true);

     // Tell curl that this is hello body of hello POST
     curl_setopt ($session, CURLOPT_POSTFIELDS, $params);

     // Tell curl not tooreturn headers, but do return hello response
     curl_setopt($session, CURLOPT_HEADER, false);
     curl_setopt($session, CURLOPT_RETURNTRANSFER, true);

     // obtain response
     $response = curl_exec($session);
     curl_close($session);

     // print everything out
     print_r($response);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="7d8da-141">Como: utilizar filtros tooEnable rodapés de página, controlo e análise</span><span class="sxs-lookup"><span data-stu-id="7d8da-141">How to: Use Filters tooEnable Footers, Tracking, and Analytics</span></span>
<span data-ttu-id="7d8da-142">SendGrid fornece funcionalidades de e-mail adicionais através da utilização de Olá 'filtros'.</span><span class="sxs-lookup"><span data-stu-id="7d8da-142">SendGrid provides additional email functionality through hello use of 'filters'.</span></span> <span data-ttu-id="7d8da-143">Estas são as definições que podem ser adicionadas tooan mensagem de e-mail para ativar a funcionalidade específica, como ativar o controlo de clique, do Google analytics, subscrição de controlo, e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="7d8da-143">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span>

<span data-ttu-id="7d8da-144">Os filtros podem ser aplicados tooa mensagem utilizando a propriedade de filtros de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d8da-144">Filters can be applied tooa message by using hello filters property.</span></span> <span data-ttu-id="7d8da-145">Cada filtro especificado por um hash que contém definições específicas do filtro.</span><span class="sxs-lookup"><span data-stu-id="7d8da-145">Each filter is specified by a hash containing filter-specific settings.</span></span> <span data-ttu-id="7d8da-146">O exemplo seguinte ativa o filtro de rodapé Olá e especifica uma mensagem de texto que será anexado toohello inferior de mensagem de correio eletrónico de saudação.</span><span class="sxs-lookup"><span data-stu-id="7d8da-146">The following example enables hello footer filter and specifies a text message that will be appended toohello bottom of hello email message.</span></span>
<span data-ttu-id="7d8da-147">Neste exemplo utilizaremos [sendgrid php biblioteca].</span><span class="sxs-lookup"><span data-stu-id="7d8da-147">For this example we will use [sendgrid-php library].</span></span>
<span data-ttu-id="7d8da-148">Utilize [compositor] tooinstall biblioteca:</span><span class="sxs-lookup"><span data-stu-id="7d8da-148">Use [Composer] tooinstall library:</span></span>

    php composer.phar require sendgrid/sendgrid 2.1.1

<span data-ttu-id="7d8da-149">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="7d8da-149">Example:</span></span>    

    <?php
     /*
      * This example is used for sendgrid-php V2.1.1 (https://github.com/sendgrid/sendgrid-php/tree/v2.1.1)
      */
     include "vendor/autoload.php";

     $email = new SendGrid\Email();
     // hello list of addresses this message will be sent to
     // [This list is used for sending multiple emails using just ONE request tooSendGrid]
     $toList = array('john@contoso.com', 'anna@contoso.com');

     // Specify hello names of hello recipients
     $nameList = array('Name 1', 'Name 2');

     // Used as an example of variable substitution
     $timeList = array('4 PM', '5 PM');

     // Set all of hello above variables
     $email->setTos($toList);
     $email->addSubstitution('-name-', $nameList);
     $email->addSubstitution('-time-', $timeList);

     // Specify that this is an initial contact message
     $email->addCategory("initial");

     // You can optionally setup individual filters here, in this example, we have
     // enabled hello footer filter
     $email->addFilter('footer', 'enable', 1);
     $email->addFilter('footer', "text/plain", "Thank you for your business");
     $email->addFilter('footer', "text/html", "Thank you for your business");

     // hello subject of your email
     $subject = 'Example SendGrid Email';

     // Where is this message coming from. For example, this message can be from
     // support@yourcompany.com, info@yourcompany.com
     $from = 'someone@example.com';

     // If you do not specify a sender list above, you can specifiy hello user here. If
     // a sender list IS specified above, this email address becomes irrelevant.
     $too= 'john@contoso.com';

     # Create hello body of hello message (a plain-text and an HTML version).
     # text is your plain-text email
     # html is your html version of hello email
     # if hello receiver is able tooview html emails then only hello html
     # email will be displayed

     /*
      * Note hello variable substitution here =)
      */
     $text = "
     Hello -name-,
     Thank you for your interest in our products. We have set up an appointment toocall you at -time- EST toodiscuss your needs in more detail.
     Regards,
     Fred";

     $html = "
     <html>
     <head></head>
     <body>
     <p>Hello -name-,<br>
     Thank you for your interest in our products. We have set up an appointment
     toocall you at -time- EST toodiscuss your needs in more detail.

     Regards,

     Fred<br>
     </p>
     </body>
     </html>";

     // set subject
     $email->setSubject($subject);

     // attach hello body of hello email
     $email->setFrom($from);
     $email->setHtml($html);
     $email->addTo($to);
     $email->setText($text);

     // Your SendGrid account credentials
     $username = 'sendgridusername@yourdomain.com';
     $password = 'example';

     // Create SendGrid object
     $sendgrid = new SendGrid($username, $password);

     // send message
     $response = $sendgrid->send($email);

     print_r($response);

## <a name="next-steps"></a><span data-ttu-id="7d8da-150">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="7d8da-150">Next Steps</span></span>
<span data-ttu-id="7d8da-151">Agora que aprendeu as noções básicas de Olá de Olá serviço de E-Mail do SendGrid, siga estes toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="7d8da-151">Now that you've learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="7d8da-152">Documentação do SendGrid: <https://sendgrid.com/docs></span><span class="sxs-lookup"><span data-stu-id="7d8da-152">SendGrid documentation: <https://sendgrid.com/docs></span></span>
* <span data-ttu-id="7d8da-153">Biblioteca do SendGrid PHP: <https://github.com/sendgrid/sendgrid-php></span><span class="sxs-lookup"><span data-stu-id="7d8da-153">SendGrid PHP library: <https://github.com/sendgrid/sendgrid-php></span></span>
* <span data-ttu-id="7d8da-154">Oferta especial de SendGrid para clientes do Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="7d8da-154">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

<span data-ttu-id="7d8da-155">Para obter mais informações, consulte também Olá [Centro para programadores do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="7d8da-155">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[https://sendgrid.com]: https://sendgrid.com
[https://sendgrid.com/transactional-email/pricing]: https://sendgrid.com/transactional-email/pricing
[special offer]: https://www.sendgrid.com/windowsazure.html
[Packaging and Deploying PHP Applications for Azure]: http://msdn.microsoft.com/library/windowsazure/hh674499(v=VS.103).aspx
[http://swiftmailer.org/download]: http://swiftmailer.org/download
[curl function]: http://php.net/curl
[serviço baseado na nuvem e-mail]: https://sendgrid.com/email-solutions
[entrega de correio eletrónico transacional]: https://sendgrid.com/transactional-email
[sendgrid php biblioteca]: https://github.com/sendgrid/sendgrid-php/tree/v2.1.1
[compositor]: https://getcomposer.org/download/
