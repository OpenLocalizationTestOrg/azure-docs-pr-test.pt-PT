---
title: "aaaHow toouse AMQP 1.0 com Olá Java API do Service Bus | Microsoft Docs"
description: "Como toouse Olá serviço de mensagem de Java (JMS) com o Service Bus do Azure e avançadas mensagem colocação Protodol (AMQP) 1.0."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="7399a-103">Como toouse Olá Java mensagem de serviço (JMS) API com o Service Bus e AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="7399a-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="7399a-104">Olá avançadas mensagem colocação protocolo (AMQP) 1.0 é um protocolo de mensagens económicos, fiável e nível de rede que pode utilizar aplicações mensagens toobuild robusta, entre plataformas.</span><span class="sxs-lookup"><span data-stu-id="7399a-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="7399a-105">Suporte para AMQP 1.0 no Service Bus significa que pode utilizar Olá colocação e publica/subscreve funcionalidades de mensagens mediadas de uma variedade de plataformas utilizando um protocolo de binário eficiente.</span><span class="sxs-lookup"><span data-stu-id="7399a-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="7399a-106">Além disso, pode criar aplicações compostas por componentes construido utilizando uma combinação de idiomas, estruturas e sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="7399a-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="7399a-107">Este artigo explica como toouse Service Bus mensagens funcionalidades (filas e publicar/subscrever tópicos) de aplicações Java utilizando Olá populares Java mensagem de serviço (JMS) API padrão.</span><span class="sxs-lookup"><span data-stu-id="7399a-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="7399a-108">Não existe um [artigo complementar](service-bus-amqp-dotnet.md) que explica como toodo Olá mesmo utilizando Olá API .NET do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7399a-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="7399a-109">Pode utilizar estes toolearn em conjunto de dois guias sobre plataforma mensagens através de AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="7399a-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="7399a-110">Introdução ao Service Bus</span><span class="sxs-lookup"><span data-stu-id="7399a-110">Get started with Service Bus</span></span>
<span data-ttu-id="7399a-111">Este guia pressupõe que já tem um espaço de nomes de barramento de serviço que contém uma fila com o nome **queue1**.</span><span class="sxs-lookup"><span data-stu-id="7399a-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="7399a-112">Se não o fizer, em seguida, pode [criar espaço de nomes de Olá e fila](service-bus-create-namespace-portal.md) utilizando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7399a-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7399a-113">Para obter mais informações sobre como espaços de nomes de barramento de serviço de toocreate e as filas, consulte [introdução às filas do Service Bus](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="7399a-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7399a-114">Particionada filas e tópicos também suportam AMQP.</span><span class="sxs-lookup"><span data-stu-id="7399a-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="7399a-115">Para obter mais informações, consulte [entidades de mensagens Particionadas](service-bus-partitioning.md) e [AMQP 1.0 suporte para o Service Bus particionada filas e tópicos](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7399a-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="7399a-116">Transferir a biblioteca de cliente AMQP 1.0 JMS Olá</span><span class="sxs-lookup"><span data-stu-id="7399a-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="7399a-117">Para obter informações sobre onde toodownload Olá a versão mais recente da biblioteca de clientes Olá Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="7399a-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="7399a-118">Tem de adicionar Olá seguintes quatro ficheiros JAR de Olá Apache Qpid JMS AMQP 1.0 distribuição arquivo toohello Java CLASSPATH quando criar e executar aplicações de JMS com o Service Bus:</span><span class="sxs-lookup"><span data-stu-id="7399a-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="7399a-119">geronimo jms\_1.1\_spec 1.0.jar</span><span class="sxs-lookup"><span data-stu-id="7399a-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="7399a-120">qpid-amqp-1-0-Client-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="7399a-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="7399a-121">qpid-amqp-1-0-Client-jms-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="7399a-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="7399a-122">qpid-amqp-1-0-Common-[Version].JAR</span><span class="sxs-lookup"><span data-stu-id="7399a-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="7399a-123">Programação de aplicações Java</span><span class="sxs-lookup"><span data-stu-id="7399a-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="7399a-124">Atribuição de nomes de Java e Interface de diretório (JNDI)</span><span class="sxs-lookup"><span data-stu-id="7399a-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="7399a-125">JMS utiliza Olá atribuição de nomes de Java e diretório de Interface (JNDI) toocreate uma separação entre nomes de lógicos e físico.</span><span class="sxs-lookup"><span data-stu-id="7399a-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="7399a-126">Dois tipos de objetos JMS são resolvidos utilizando JNDI: ConnectionFactory e de destino.</span><span class="sxs-lookup"><span data-stu-id="7399a-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="7399a-127">JNDI utiliza um modelo de fornecedor na qual pode fixação deveres de resolução do nome do diretório diferente serviços toohandle.</span><span class="sxs-lookup"><span data-stu-id="7399a-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="7399a-128">Olá Apache Qpid JMS AMQP 1.0 biblioteca é fornecido com um simples propriedades fornecedor JNDI baseados em ficheiros, que é configurado através de um ficheiro as propriedades seguintes Olá formato:</span><span class="sxs-lookup"><span data-stu-id="7399a-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="7399a-129">Configurar Olá ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="7399a-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="7399a-130">Olá toodefine de entrada utilizada um **ConnectionFactory** no Olá Qpid do fornecedor JNDI do ficheiro de propriedades é dos Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="7399a-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="7399a-131">Onde **[jndi_name]** e **[ConnectionURL]** ter Olá significados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7399a-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="7399a-132">**[jndi_name]** : nome lógico do Olá de Olá ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="7399a-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="7399a-133">Este é o nome de Olá que será resolvido numa aplicação de Java Olá utilizando Olá JNDI IntialContext.lookup() método.</span><span class="sxs-lookup"><span data-stu-id="7399a-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="7399a-134">**[ConnectionURL]** : Um URL que fornece a biblioteca JMS Olá com informações de Olá necessário toohello mediador AMQP.</span><span class="sxs-lookup"><span data-stu-id="7399a-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="7399a-135">formato de Olá de Olá **ConnectionURL** é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="7399a-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="7399a-136">Onde **[espaço de nomes]**, **[SASPolicyName]** e **[SASPolicyKey]** ter Olá significados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7399a-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="7399a-137">**[espaço de nomes]** : Olá espaço de nomes do Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7399a-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="7399a-138">**[SASPolicyName]** : nome da política de assinatura de acesso partilhado fila Olá.</span><span class="sxs-lookup"><span data-stu-id="7399a-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="7399a-139">**[SASPolicyKey]** : chave de política de assinatura de acesso partilhado da fila de Olá.</span><span class="sxs-lookup"><span data-stu-id="7399a-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="7399a-140">Terá de codificar o URL a palavra-passe de Olá manualmente.</span><span class="sxs-lookup"><span data-stu-id="7399a-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="7399a-141">Um utilitário de codificação do URL útil está disponível em [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="7399a-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="7399a-142">Configurar destinos</span><span class="sxs-lookup"><span data-stu-id="7399a-142">Configure destinations</span></span>
<span data-ttu-id="7399a-143">entrada de Olá utilizados toodefine que tem um destino no fornecedor de JNDI Olá Qpid propriedades ficheiros Olá seguir o formato:</span><span class="sxs-lookup"><span data-stu-id="7399a-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="7399a-144">ou</span><span class="sxs-lookup"><span data-stu-id="7399a-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="7399a-145">Onde **[jndi\_nome]** e **[físico\_nome]** ter Olá significados os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7399a-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="7399a-146">**[jndi_name]** : nome lógico do Olá do destino de Olá.</span><span class="sxs-lookup"><span data-stu-id="7399a-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="7399a-147">Este é o nome de Olá que será resolvido numa aplicação de Java Olá utilizando Olá JNDI IntialContext.lookup() método.</span><span class="sxs-lookup"><span data-stu-id="7399a-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="7399a-148">**[physical_name]** : nome Olá Olá aplicação Olá do Service Bus entidade toowhich envia ou receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="7399a-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="7399a-149">Se receber de uma subscrição de tópico de barramento de serviço, nome físico Olá especificado no JNDI deve ser o nome de Olá tópico Olá.</span><span class="sxs-lookup"><span data-stu-id="7399a-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="7399a-150">nome da subscrição Olá é fornecida quando subscrição durável Olá for criada num Olá código da aplicação JMS.</span><span class="sxs-lookup"><span data-stu-id="7399a-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="7399a-151">Olá [guia para programadores 1.0 AMQP Bus Service](service-bus-amqp-dotnet.md) fornece mais detalhes sobre como trabalhar com tópicos do Service Bus do JMS.</span><span class="sxs-lookup"><span data-stu-id="7399a-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="7399a-152">Escrever Olá JMS aplicação</span><span class="sxs-lookup"><span data-stu-id="7399a-152">Write hello JMS application</span></span>
<span data-ttu-id="7399a-153">Não são especial APIs ou opções obrigatório quando usar JMS com o Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7399a-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="7399a-154">No entanto, existem algumas restrições que vai ser abordadas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="7399a-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="7399a-155">Como com qualquer aplicação JMS, Olá primeiro thing necessária é a configuração do ambiente de JNDI Olá, tooresolve capaz de toobe um **ConnectionFactory** e destinos.</span><span class="sxs-lookup"><span data-stu-id="7399a-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="7399a-156">Configurar Olá JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="7399a-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="7399a-157">ambiente de JNDI Olá é configurada através da transmissão de uma tabela hash de informações de configuração para o construtor de Olá da classe de javax.naming.InitialContext Olá.</span><span class="sxs-lookup"><span data-stu-id="7399a-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="7399a-158">dois elementos necessários Olá na tabela hash de Olá são nome de classe de Olá da Olá inicial fábrica de contexto e Olá URL do fornecedor.</span><span class="sxs-lookup"><span data-stu-id="7399a-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="7399a-159">Olá código seguinte mostra como tooconfigure Olá JNDI ambiente toouse Olá Qpid propriedades baseada em ficheiros JNDI fornecedor com um ficheiro de propriedades com o nome **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="7399a-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="7399a-160">Uma aplicação de JMS simples utilizando uma fila do Service Bus</span><span class="sxs-lookup"><span data-stu-id="7399a-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="7399a-161">Hello do programa seguinte exemplo envia JMS TextMessages tooa fila do Service Bus com o nome lógico de JNDI Olá da fila e recebe mensagens hello do novamente.</span><span class="sxs-lookup"><span data-stu-id="7399a-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a><span data-ttu-id="7399a-162">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="7399a-162">Run hello application</span></span>
<span data-ttu-id="7399a-163">Executar a aplicação Olá produz saída de formulário Olá:</span><span class="sxs-lookup"><span data-stu-id="7399a-163">Running hello application produces output of hello form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="7399a-164">Plataforma de mensagens entre JMS e .NET</span><span class="sxs-lookup"><span data-stu-id="7399a-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="7399a-165">Este guia mostrado como toosend e receber mensagens tooand do Service Bus utilizando JMS.</span><span class="sxs-lookup"><span data-stu-id="7399a-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="7399a-166">No entanto, uma das principais vantagens Olá AMQP 1.0 é o que permite a toobe de aplicações criado a partir do componentes escritos em idiomas diferentes, com mensagens trocadas em fidelidade completa e fiável.</span><span class="sxs-lookup"><span data-stu-id="7399a-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="7399a-167">Utilizando a aplicação de JMS de exemplo de Olá descrito acima e uma aplicação .NET semelhante obtidas a partir de um artigo complementar, [utilizando o Service Bus a partir do .NET com AMQP 1.0](service-bus-amqp-dotnet.md), podem trocar mensagens entre .NET e Java.</span><span class="sxs-lookup"><span data-stu-id="7399a-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="7399a-168">Leia este artigo para obter mais informações sobre os detalhes de Olá de plataforma mensagens utilizando o Service Bus e AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="7399a-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="7399a-169">JMS too.NET</span><span class="sxs-lookup"><span data-stu-id="7399a-169">JMS too.NET</span></span>
<span data-ttu-id="7399a-170">toodemonstrate JMS too.NET mensagens:</span><span class="sxs-lookup"><span data-stu-id="7399a-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="7399a-171">Inicie a aplicação de exemplo Olá .NET sem quaisquer argumentos da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7399a-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="7399a-172">Inicie a aplicação de exemplo Olá Java com o argumento da linha de comandos do Olá "sendonly".</span><span class="sxs-lookup"><span data-stu-id="7399a-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="7399a-173">Neste modo, hello aplicações não irão receber mensagens da fila de Olá, só irá enviar.</span><span class="sxs-lookup"><span data-stu-id="7399a-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="7399a-174">Prima **Enter** algumas vezes na consola de aplicação de Java Olá, que fará com que toobe de mensagens enviada.</span><span class="sxs-lookup"><span data-stu-id="7399a-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="7399a-175">Estas mensagens são recebidas pelo Olá aplicação .NET.</span><span class="sxs-lookup"><span data-stu-id="7399a-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="7399a-176">Resultado da aplicação JMS</span><span class="sxs-lookup"><span data-stu-id="7399a-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="7399a-177">Resultado da aplicação .NET</span><span class="sxs-lookup"><span data-stu-id="7399a-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="7399a-178">TooJMS de .NET</span><span class="sxs-lookup"><span data-stu-id="7399a-178">.NET tooJMS</span></span>
<span data-ttu-id="7399a-179">toodemonstrate tooJMS de .NET de mensagens:</span><span class="sxs-lookup"><span data-stu-id="7399a-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="7399a-180">Inicie a aplicação de exemplo Olá .NET com o argumento da linha de comandos do Olá "sendonly".</span><span class="sxs-lookup"><span data-stu-id="7399a-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="7399a-181">Neste modo, hello aplicações não irão receber mensagens da fila de Olá, só irá enviar.</span><span class="sxs-lookup"><span data-stu-id="7399a-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="7399a-182">Inicie a aplicação de exemplo Olá Java sem quaisquer argumentos da linha de comandos.</span><span class="sxs-lookup"><span data-stu-id="7399a-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="7399a-183">Prima **Enter** algumas vezes na consola de aplicação .NET de Olá, que fará com que toobe de mensagens enviada.</span><span class="sxs-lookup"><span data-stu-id="7399a-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="7399a-184">Estas mensagens são recebidas pelo Olá aplicação Java.</span><span class="sxs-lookup"><span data-stu-id="7399a-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="7399a-185">Resultado da aplicação .NET</span><span class="sxs-lookup"><span data-stu-id="7399a-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="7399a-186">Resultado da aplicação JMS</span><span class="sxs-lookup"><span data-stu-id="7399a-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="7399a-187">Restrições e funcionalidades não suportadas</span><span class="sxs-lookup"><span data-stu-id="7399a-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="7399a-188">Olá seguintes restrições existe quando utilizar JMS através de AMQP 1.0 com o Service Bus, nomeadamente:</span><span class="sxs-lookup"><span data-stu-id="7399a-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="7399a-189">Apenas um **MessageProducer** ou **MessageConsumer** é permitida por **sessão**.</span><span class="sxs-lookup"><span data-stu-id="7399a-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="7399a-190">Se precisar de toocreate vários **MessageProducers** ou **MessageConsumers** numa aplicação, crie um dedicado **sessão** para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="7399a-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="7399a-191">Subscrições de tópico voláteis não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="7399a-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="7399a-192">**MessageSelectors** não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="7399a-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="7399a-193">Destinos temporários; Por exemplo, **TemporaryQueue**, **TemporaryTopic** não são atualmente suportadas, juntamente com Olá **QueueRequestor** e **TopicRequestor**APIs que as utilizam.</span><span class="sxs-lookup"><span data-stu-id="7399a-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="7399a-194">Sessões transacionadas e transações distribuídas não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="7399a-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="7399a-195">Resumo</span><span class="sxs-lookup"><span data-stu-id="7399a-195">Summary</span></span>
<span data-ttu-id="7399a-196">Este tooguide como mostrou como toouse mediadas do Service Bus mensagens funcionalidades (filas e publicar/subscrever tópicos) de Java utilizando Olá populares JMS API e AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="7399a-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="7399a-197">Também pode utilizar o Service Bus AMQP 1.0 de outros idiomas, incluindo .NET, C, Python e PHP.</span><span class="sxs-lookup"><span data-stu-id="7399a-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="7399a-198">Componentes construido utilizando estes idiomas diferentes podem trocar mensagens fiável e em fidelidade completa utilizando o suporte de Olá AMQP 1.0 no Service Bus.</span><span class="sxs-lookup"><span data-stu-id="7399a-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7399a-199">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7399a-199">Next steps</span></span>
* [<span data-ttu-id="7399a-200">Suporte de AMQP 1.0 no Service Bus do Azure</span><span class="sxs-lookup"><span data-stu-id="7399a-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="7399a-201">Como toouse AMQP 1.0 com Olá API .NET do Service Bus</span><span class="sxs-lookup"><span data-stu-id="7399a-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="7399a-202">Service Bus AMQP 1.0 Guia para programadores</span><span class="sxs-lookup"><span data-stu-id="7399a-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="7399a-203">Introdução às filas do Service Bus</span><span class="sxs-lookup"><span data-stu-id="7399a-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="7399a-204">Centro de Programadores do Java</span><span class="sxs-lookup"><span data-stu-id="7399a-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

