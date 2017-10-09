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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="7722a-104">Como tooUse Twilio de voz e capacidades de SMS do PHP</span><span class="sxs-lookup"><span data-stu-id="7722a-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="7722a-105">Este guia demonstra como serviço de programação de tarefas comuns tooperform com Olá Twilio API no Azure.</span><span class="sxs-lookup"><span data-stu-id="7722a-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="7722a-106">cenários de Olá abrangidos incluem a efetuar uma chamada telefónica e enviar uma mensagem de serviço de mensagens curto (SMS).</span><span class="sxs-lookup"><span data-stu-id="7722a-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="7722a-107">Para obter mais informações sobre Twilio e a utilização de voz e SMS nas suas aplicações, consulte Olá [passos](#NextSteps) secção.</span><span class="sxs-lookup"><span data-stu-id="7722a-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="7722a-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="7722a-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="7722a-109">Twilio está a ligar a Olá futuro das comunicações de negócio, ativar voz tooembed de programadores, VoIP e de mensagens em aplicações.</span><span class="sxs-lookup"><span data-stu-id="7722a-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="7722a-110">Estes virtualizar todos os infraestrutura necessária num ambiente baseado na nuvem, global, expor-lo através da plataforma de Olá Twilio comunicações API.</span><span class="sxs-lookup"><span data-stu-id="7722a-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="7722a-111">As aplicações são simple toobuild e dimensionável.</span><span class="sxs-lookup"><span data-stu-id="7722a-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="7722a-112">Desfrute de mais flexibilidade consigo pay-como vá preços e beneficiar da fiabilidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="7722a-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="7722a-113">**Voz do Twilio** permite toomake a aplicações e receber chamadas telefónicas.</span><span class="sxs-lookup"><span data-stu-id="7722a-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="7722a-114">**Twilio SMS** permite toosend a aplicação e receba mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="7722a-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="7722a-115">**Cliente do Twilio** permite-lhe toomake VoIP chamadas de qualquer telefone, o tablet ou o browser e suporta WebRTC.</span><span class="sxs-lookup"><span data-stu-id="7722a-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="7722a-116"><a id="Pricing"></a>Preços do Twilio e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="7722a-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="7722a-117">Clientes do Azure recebem um [oferta especial](http://www.twilio.com/azure): complimentary $10 do Twilio crédito ao atualizar a sua conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="7722a-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="7722a-118">Este crédito do Twilio podem ser aplicados tooany Twilio utilização ($10 crédito equivalente toosending máximo de 1000 mensagens SMS ou receção segurança too1000 minutos de voz, dependendo da localização Olá o destino de número e a mensagem ou a chamada telefónica de entrada).</span><span class="sxs-lookup"><span data-stu-id="7722a-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="7722a-119">Resgatar este crédito do Twilio e começar a utilizar em: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="7722a-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="7722a-120">Twilio é um serviço pay as you go.</span><span class="sxs-lookup"><span data-stu-id="7722a-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="7722a-121">Existem não existem taxas de configuração e pode fechar a sua conta em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="7722a-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="7722a-122">Pode encontrar mais detalhes em [preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="7722a-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="7722a-123"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="7722a-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="7722a-124">Olá Twilio API é uma API RESTful que fornece uma funcionalidade SMS de voz e de aplicações.</span><span class="sxs-lookup"><span data-stu-id="7722a-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="7722a-125">Bibliotecas de cliente estão disponíveis em vários idiomas; Para obter uma lista, consulte [Twilio as bibliotecas API][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="7722a-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="7722a-126">Aspetos fundamentais da Olá Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="7722a-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="7722a-127"><a id="Verbs"></a>Twilio verbos</span><span class="sxs-lookup"><span data-stu-id="7722a-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="7722a-128">Olá API faz com que o utilize do Twilio verbos; Por exemplo, Olá  **&lt;indiquem&gt;**  verbo dá instruções ao Twilio tooaudibly entregar uma mensagem durante uma chamada.</span><span class="sxs-lookup"><span data-stu-id="7722a-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="7722a-129">Olá segue-se uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="7722a-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="7722a-130">Saiba mais sobre Olá outros verbos e funcionalidades através de [documentação do Twilio Markup Language](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="7722a-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="7722a-131">**&lt;Marcação&gt;**: estabelece ligação telefónica de tooanother Olá autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="7722a-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="7722a-132">**&lt;Recolher&gt;**: recolhe dígitos numéricos introduzidos no teclado do telefone de Olá.</span><span class="sxs-lookup"><span data-stu-id="7722a-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="7722a-133">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="7722a-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="7722a-134">**&lt;Reproduzir&gt;**: desempenha um ficheiro de áudio.</span><span class="sxs-lookup"><span data-stu-id="7722a-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="7722a-135">**&lt;Colocar em pausa&gt;**: silenciosamente aguarda que um número de segundos especificado.</span><span class="sxs-lookup"><span data-stu-id="7722a-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="7722a-136">**&lt;Registo&gt;**: regista voz invocadora Olá e devolve um URL de um ficheiro que contém a gravação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7722a-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="7722a-137">**&lt;Redirecionar&gt;**: transfere o controlo de uma chamada ou SMS toohello TwiML um URL diferente.</span><span class="sxs-lookup"><span data-stu-id="7722a-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="7722a-138">**&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem a faturação</span><span class="sxs-lookup"><span data-stu-id="7722a-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="7722a-139">**&lt;Diga&gt;**: converte texto toospeech que é efetuada numa chamada.</span><span class="sxs-lookup"><span data-stu-id="7722a-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="7722a-140">**&lt;SMS&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="7722a-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="7722a-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="7722a-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="7722a-142">TwiML é um conjunto de instruções baseado em XML com base no verbos de Twilio Olá que o informam Twilio como tooprocess uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="7722a-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="7722a-143">Por exemplo, Olá seguir TwiML teria de converter o texto de Olá **Olá mundo** toospeech.</span><span class="sxs-lookup"><span data-stu-id="7722a-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="7722a-144">Quando as chamadas de aplicação Olá Twilio API, um dos parâmetros de API de Olá é Olá URL que devolve Olá TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="7722a-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="7722a-145">Para fins de desenvolvimento, pode utilizar os URLs do Twilio fornecidos pelo tooprovide Olá TwiML as respostas utilizadas pelas suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="7722a-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="7722a-146">Também pode alojar as suas próprias as respostas hello URLs tooproduce TwiML e outra opção consiste toouse Olá **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="7722a-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="7722a-147">Para obter mais informações sobre Twilio verbos, os respetivos atributos e TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="7722a-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="7722a-148">Para obter informações adicionais sobre Olá API do Twilio, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="7722a-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="7722a-149"><a id="CreateAccount"></a>Criar uma conta do Twilio</span><span class="sxs-lookup"><span data-stu-id="7722a-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="7722a-150">Quando estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="7722a-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="7722a-151">Pode começar com uma conta gratuita e atualize a sua conta mais tarde.</span><span class="sxs-lookup"><span data-stu-id="7722a-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="7722a-152">Quando se inscreve para uma conta do Twilio, receberá um ID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7722a-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="7722a-153">Ambos irão ser chamadas de API do Twilio toomake necessários.</span><span class="sxs-lookup"><span data-stu-id="7722a-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="7722a-154">tooprevent não autorizado aceder à conta tooyour, mantenha o seu token de autenticação segura.</span><span class="sxs-lookup"><span data-stu-id="7722a-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="7722a-155">O seu ID de conta e a autenticação de token são visíveis em Olá [página de conta do Twilio][twilio_account], na Olá campos com a etiqueta **SID da conta** e **AUTH TOKEN**, respetivamente.</span><span class="sxs-lookup"><span data-stu-id="7722a-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="7722a-156"><a id="create_app"></a>Criar uma aplicação PHP</span><span class="sxs-lookup"><span data-stu-id="7722a-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="7722a-157">Uma aplicação PHP que utiliza o serviço de Twilio Olá e está em execução no Azure é não diferente de qualquer outra aplicação PHP que utiliza Olá Twilio serviço.</span><span class="sxs-lookup"><span data-stu-id="7722a-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="7722a-158">Enquanto os serviços de Twilio são baseado em REST e podem ser chamados a partir do PHP de várias formas, este artigo foca-se na forma como toouse Twilio serviços com [Twilio biblioteca para que o PHP a partir do GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="7722a-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="7722a-159">Para obter mais informações sobre como utilizar a biblioteca de Twilio Olá para PHP, consulte [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="7722a-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="7722a-160">Instruções detalhadas para criar e implementar uma tooAzure de aplicação do Twilio/PHP estão disponíveis em [como tooMake Twilio de utilização de uma chamada telefónica numa aplicação PHP no Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="7722a-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="7722a-161"><a id="configure_app"></a>Configurar a sua aplicação tooUse Twilio bibliotecas</span><span class="sxs-lookup"><span data-stu-id="7722a-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="7722a-162">Pode configurar a sua biblioteca de Twilio aplicação toouse Olá para PHP de duas formas:</span><span class="sxs-lookup"><span data-stu-id="7722a-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="7722a-163">Transferir a biblioteca de Twilio Olá para PHP a partir do GitHub ([https://github.com/twilio/twilio-php][twilio_php]) e adicione Olá **serviços** aplicação tooyour de diretório.</span><span class="sxs-lookup"><span data-stu-id="7722a-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="7722a-164">-OU-</span><span class="sxs-lookup"><span data-stu-id="7722a-164">-OR-</span></span>
2. <span data-ttu-id="7722a-165">Instale a biblioteca de Twilio Olá para PHP como um pacote PEAR.</span><span class="sxs-lookup"><span data-stu-id="7722a-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="7722a-166">Podem ser instalado com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7722a-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="7722a-167">Depois de ter instalada a biblioteca de Twilio Olá para PHP, em seguida, pode adicionar um **require_once** declaração, Olá parte superior do seu PHP ficheiros de biblioteca de Olá tooreference:</span><span class="sxs-lookup"><span data-stu-id="7722a-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="7722a-168">Para obter mais informações, consulte [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="7722a-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="7722a-169"><a id="howto_make_call"></a>Como: efetuar uma chamada de saída</span><span class="sxs-lookup"><span data-stu-id="7722a-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="7722a-170">Olá seguinte mostra como uma saída de toomake chamada utilizando Olá **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="7722a-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="7722a-171">Este código também utiliza um Olá de tooreturn Twilio fornecidos pelo site resposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="7722a-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="7722a-172">Substitua os valores para Olá **de** e **para** números de telefone e certifique-se de que verifique Olá **de** número para o seu código de Olá do Twilio conta toorunning anterior de telefone.</span><span class="sxs-lookup"><span data-stu-id="7722a-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="7722a-173">Conforme mencionado, este código utiliza um Olá de tooreturn Twilio fornecidos pelo site TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="7722a-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="7722a-174">Em vez disso, pode utilizar o seus próprios Olá tooprovide de site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas do seu próprio Web Site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="7722a-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="7722a-175">**Tenha em atenção**: tootroubleshoot erros de validação de certificado SSL, consulte [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="7722a-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="7722a-176"><a id="howto_send_sms"></a>Como: enviar uma mensagem SMS</span><span class="sxs-lookup"><span data-stu-id="7722a-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="7722a-177">Olá seguinte mostra como toosend uma mensagem SMS utilizando Olá **Services_Twilio** classe.</span><span class="sxs-lookup"><span data-stu-id="7722a-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="7722a-178">Olá **de** número é fornecido pela Twilio para avaliação contas toosend mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="7722a-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="7722a-179">Olá **para** número tem de ser verificado para o seu código de Olá do Twilio conta toorunning anterior.</span><span class="sxs-lookup"><span data-stu-id="7722a-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="7722a-180"><a id="howto_provide_twiml_responses"></a>Como: forneça TwiML respostas a partir do seu próprio site</span><span class="sxs-lookup"><span data-stu-id="7722a-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="7722a-181">Quando inicia a sua aplicação toohello uma chamada de API do Twilio, Twilio enviará o seu URL de tooa pedido que é esperado tooreturn uma resposta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="7722a-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="7722a-182">exemplo de Olá acima utiliza Olá Twilio URL fornecido pelo [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="7722a-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="7722a-183">(Embora TwiML está concebido para utilização por Twilio, pode ver Olá-lo no seu browser.</span><span class="sxs-lookup"><span data-stu-id="7722a-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="7722a-184">Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio `<Response>` elemento; como outro exemplo, clique em [http://twimlets.com/message? Mensagem % 5B0 %5 D = Olá % 20World] [ twimlet_message_url_hello_world] toosee um `<Response>` elemento que contenha um `<Say>` elemento.)</span><span class="sxs-lookup"><span data-stu-id="7722a-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="7722a-185">Em vez de depender Olá Twilio URL fornecido pelo, pode criar o seu próprio site, que devolve as respostas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="7722a-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="7722a-186">Pode criar site Olá em qualquer idioma que devolve respostas XML; Este tópico parte do princípio de que irá utilizar Olá toocreate do PHP TwiML.</span><span class="sxs-lookup"><span data-stu-id="7722a-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="7722a-187">Olá PHP página resultados numa resposta TwiML que indica que os seguintes **Olá mundo** na chamada de Olá.</span><span class="sxs-lookup"><span data-stu-id="7722a-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="7722a-188">Como pode ver do exemplo Olá acima, Olá TwiML resposta é simplesmente um documento XML.</span><span class="sxs-lookup"><span data-stu-id="7722a-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="7722a-189">Biblioteca do Twilio Olá para PHP contém classes que irão gerar TwiML por si.</span><span class="sxs-lookup"><span data-stu-id="7722a-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="7722a-190">exemplo de Olá abaixo produz resposta equivalente Olá, conforme mostrado acima, mas utiliza Olá **serviços\_Twilio\_Twiml** classe na biblioteca do Twilio Olá para PHP:</span><span class="sxs-lookup"><span data-stu-id="7722a-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="7722a-191">Para mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="7722a-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="7722a-192">Assim que tiver a sua página PHP configurar respostas de TwiML tooprovide, utilize Olá URL da página PHP Olá como Olá URL transmitido Olá `Services_Twilio->account->calls->create` método.</span><span class="sxs-lookup"><span data-stu-id="7722a-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="7722a-193">Por exemplo, se tiver uma aplicação Web com o nome **MyTwiML** tooan implementado Azure serviço alojado, não sendo nome Olá da página PHP Olá **mytwiml.php**, Olá URL pode ser transmitido demasiado **Services_ Twilio-conta > -> chamadas -> criar** conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="7722a-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="7722a-194">Para obter informações adicionais sobre a utilização do Twilio no Azure com o PHP, consulte [como tooMake Twilio de utilização de uma chamada telefónica numa aplicação PHP no Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="7722a-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="7722a-195"><a id="AdditionalServices"></a>Como: utilizar os serviços do Twilio adicionais</span><span class="sxs-lookup"><span data-stu-id="7722a-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="7722a-196">Além disso exemplos toohello mostrados aqui, que twilio oferece as APIs baseadas na web que pode utilizar funcionalidades de Twilio adicionais tooleverage da sua aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7722a-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="7722a-197">Para mais informações, consulte Olá [documentação da API do Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="7722a-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="7722a-198"><a id="NextSteps"></a>Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="7722a-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="7722a-199">Agora que aprendeu as noções básicas de Olá de Olá Twilio serviço, siga estas toolearn ligações mais:</span><span class="sxs-lookup"><span data-stu-id="7722a-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="7722a-200">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="7722a-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="7722a-201">[De Twilio HowTo e código de exemplo][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="7722a-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="7722a-202">[Tutoriais de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="7722a-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="7722a-203">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="7722a-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="7722a-204">[Fale com tooTwilio suporte][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="7722a-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
