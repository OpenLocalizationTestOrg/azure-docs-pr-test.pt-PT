---
title: aaaSend eventos tooAzure Event Hubs utilizando C | Microsoft Docs
description: Enviar eventos tooAzure Event Hubs utilizando C
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="5edf0-103">Enviar eventos tooAzure Event Hubs utilizando C</span><span class="sxs-lookup"><span data-stu-id="5edf0-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="5edf0-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="5edf0-104">Introduction</span></span>
<span data-ttu-id="5edf0-105">Os Event Hubs são um sistema de ingestão altamente dimensionável, que pode ingerir milhões de eventos por segundo, permitindo tooprocess uma aplicação e analisar Olá quantidades enormes de dados produzidos pelos seus dispositivos e aplicações ligados.</span><span class="sxs-lookup"><span data-stu-id="5edf0-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="5edf0-106">Depois de recolhidos para um hub de eventos, pode transformar e armazenar dados através de qualquer fornecedor de análise em tempo real ou cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5edf0-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="5edf0-107">Para obter mais informações, consulte Olá [descrição geral dos Event Hubs] [descrição geral dos Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="5edf0-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="5edf0-108">Neste tutorial, ficará a saber como toosend eventos tooan hub de eventos utilizando uma aplicação de consola no c. tooreceive eventos, clique em recetor de idioma apropriado Olá na tabela da esquerda do Olá do conteúdo.</span><span class="sxs-lookup"><span data-stu-id="5edf0-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="5edf0-109">toocomplete neste tutorial, terá de Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="5edf0-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="5edf0-110">Num ambiente de desenvolvimento de C.</span><span class="sxs-lookup"><span data-stu-id="5edf0-110">A C development environment.</span></span> <span data-ttu-id="5edf0-111">Para este tutorial, iremos assumir pilha do gcc Olá numa VM com Ubuntu 14.04 Linux do Azure.</span><span class="sxs-lookup"><span data-stu-id="5edf0-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="5edf0-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="5edf0-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="5edf0-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5edf0-113">An active Azure account.</span></span> <span data-ttu-id="5edf0-114">Se não tiver uma conta, pode criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5edf0-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5edf0-115">Para obter mais detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5edf0-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="5edf0-116">Enviar mensagens tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="5edf0-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="5edf0-117">Nesta secção, iremos escrever um hub de eventos do C aplicação toosend eventos tooyour.</span><span class="sxs-lookup"><span data-stu-id="5edf0-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="5edf0-118">código de Olá utiliza a biblioteca de Proton AMQP Olá de Olá [Apache Qpid projeto](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5edf0-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="5edf0-119">Isto é semelhante toousing filas do Service Bus e tópicos com o AMQP do C conforme mostrado [aqui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="5edf0-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="5edf0-120">Para obter mais informações, consulte [documentação Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="5edf0-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="5edf0-121">De Olá [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga Olá instruções tooinstall Qpid Proton, dependendo do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="5edf0-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="5edf0-122">toocompile Olá biblioteca Proton, instale Olá os seguintes pacotes:</span><span class="sxs-lookup"><span data-stu-id="5edf0-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="5edf0-123">Transferir Olá [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html)e extrair, por ex.:</span><span class="sxs-lookup"><span data-stu-id="5edf0-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="5edf0-124">Crie um diretório de compilação, a compilação e a instalar:</span><span class="sxs-lookup"><span data-stu-id="5edf0-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="5edf0-125">No seu diretório de trabalho, crie um novo ficheiro chamado **sender.c** com Olá seguinte código.</span><span class="sxs-lookup"><span data-stu-id="5edf0-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="5edf0-126">Lembre-se o valor de Olá toosubstitute para o seu nome de hub de eventos e o nome do espaço de nomes.</span><span class="sxs-lookup"><span data-stu-id="5edf0-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="5edf0-127">Também deve substituir uma versão com codificação URL da chave de Olá para Olá **SendRule** criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5edf0-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="5edf0-128">É possível codificar o URL [aqui](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="5edf0-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C toostop hello sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="5edf0-129">Compilar o ficheiro de Olá, partindo do princípio de **gcc**:</span><span class="sxs-lookup"><span data-stu-id="5edf0-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="5edf0-130">Este código, utilizamos uma janela de envio de mensagens de Olá tooforce 1 saída logo que possível.</span><span class="sxs-lookup"><span data-stu-id="5edf0-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="5edf0-131">Em geral, a aplicação deve experimentar o débito de tooincrease toobatch mensagens.</span><span class="sxs-lookup"><span data-stu-id="5edf0-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="5edf0-132">Consulte Olá [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obter informações sobre como toouse Olá biblioteca Qpid Proton neste e noutros ambientes e de plataformas para os quais são fornecidos enlaces (atualmente Perl, PHP, Python, Ruby e o).</span><span class="sxs-lookup"><span data-stu-id="5edf0-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="5edf0-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5edf0-133">Next steps</span></span>
<span data-ttu-id="5edf0-134">Pode saber mais sobre os Event Hubs, visitando Olá seguintes ligações:</span><span class="sxs-lookup"><span data-stu-id="5edf0-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="5edf0-135">Descrição geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5edf0-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="5edf0-136">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="5edf0-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="5edf0-137">FAQ dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5edf0-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
