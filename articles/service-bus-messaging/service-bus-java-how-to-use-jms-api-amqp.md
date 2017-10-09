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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Como toouse Olá Java mensagem de serviço (JMS) API com o Service Bus e AMQP 1.0
Olá avançadas mensagem colocação protocolo (AMQP) 1.0 é um protocolo de mensagens económicos, fiável e nível de rede que pode utilizar aplicações mensagens toobuild robusta, entre plataformas.

Suporte para AMQP 1.0 no Service Bus significa que pode utilizar Olá colocação e publica/subscreve funcionalidades de mensagens mediadas de uma variedade de plataformas utilizando um protocolo de binário eficiente. Além disso, pode criar aplicações compostas por componentes construido utilizando uma combinação de idiomas, estruturas e sistemas operativos.

Este artigo explica como toouse Service Bus mensagens funcionalidades (filas e publicar/subscrever tópicos) de aplicações Java utilizando Olá populares Java mensagem de serviço (JMS) API padrão. Não existe um [artigo complementar](service-bus-amqp-dotnet.md) que explica como toodo Olá mesmo utilizando Olá API .NET do Service Bus. Pode utilizar estes toolearn em conjunto de dois guias sobre plataforma mensagens através de AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Introdução ao Service Bus
Este guia pressupõe que já tem um espaço de nomes de barramento de serviço que contém uma fila com o nome **queue1**. Se não o fizer, em seguida, pode [criar espaço de nomes de Olá e fila](service-bus-create-namespace-portal.md) utilizando Olá [portal do Azure](https://portal.azure.com). Para obter mais informações sobre como espaços de nomes de barramento de serviço de toocreate e as filas, consulte [introdução às filas do Service Bus](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Particionada filas e tópicos também suportam AMQP. Para obter mais informações, consulte [entidades de mensagens Particionadas](service-bus-partitioning.md) e [AMQP 1.0 suporte para o Service Bus particionada filas e tópicos](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Transferir a biblioteca de cliente AMQP 1.0 JMS Olá
Para obter informações sobre onde toodownload Olá a versão mais recente da biblioteca de clientes Olá Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Tem de adicionar Olá seguintes quatro ficheiros JAR de Olá Apache Qpid JMS AMQP 1.0 distribuição arquivo toohello Java CLASSPATH quando criar e executar aplicações de JMS com o Service Bus:

* geronimo jms\_1.1\_spec 1.0.jar
* qpid-amqp-1-0-Client-[Version].JAR
* qpid-amqp-1-0-Client-jms-[Version].JAR
* qpid-amqp-1-0-Common-[Version].JAR

## <a name="coding-java-applications"></a>Programação de aplicações Java
### <a name="java-naming-and-directory-interface-jndi"></a>Atribuição de nomes de Java e Interface de diretório (JNDI)
JMS utiliza Olá atribuição de nomes de Java e diretório de Interface (JNDI) toocreate uma separação entre nomes de lógicos e físico. Dois tipos de objetos JMS são resolvidos utilizando JNDI: ConnectionFactory e de destino. JNDI utiliza um modelo de fornecedor na qual pode fixação deveres de resolução do nome do diretório diferente serviços toohandle. Olá Apache Qpid JMS AMQP 1.0 biblioteca é fornecido com um simples propriedades fornecedor JNDI baseados em ficheiros, que é configurado através de um ficheiro as propriedades seguintes Olá formato:

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

#### <a name="configure-hello-connectionfactory"></a>Configurar Olá ConnectionFactory
Olá toodefine de entrada utilizada um **ConnectionFactory** no Olá Qpid do fornecedor JNDI do ficheiro de propriedades é dos Olá seguinte formato:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Onde **[jndi_name]** e **[ConnectionURL]** ter Olá significados os seguintes:

* **[jndi_name]** : nome lógico do Olá de Olá ConnectionFactory. Este é o nome de Olá que será resolvido numa aplicação de Java Olá utilizando Olá JNDI IntialContext.lookup() método.
* **[ConnectionURL]** : Um URL que fornece a biblioteca JMS Olá com informações de Olá necessário toohello mediador AMQP.

formato de Olá de Olá **ConnectionURL** é o seguinte:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Onde **[espaço de nomes]**, **[SASPolicyName]** e **[SASPolicyKey]** ter Olá significados os seguintes:

* **[espaço de nomes]** : Olá espaço de nomes do Service Bus.
* **[SASPolicyName]** : nome da política de assinatura de acesso partilhado fila Olá.
* **[SASPolicyKey]** : chave de política de assinatura de acesso partilhado da fila de Olá.

> [!NOTE]
> Terá de codificar o URL a palavra-passe de Olá manualmente. Um utilitário de codificação do URL útil está disponível em [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Configurar destinos
entrada de Olá utilizados toodefine que tem um destino no fornecedor de JNDI Olá Qpid propriedades ficheiros Olá seguir o formato:

```
queue.[jndi_name] = [physical_name]
```

ou

```
topic.[jndi_name] = [physical_name]
```

Onde **[jndi\_nome]** e **[físico\_nome]** ter Olá significados os seguintes:

* **[jndi_name]** : nome lógico do Olá do destino de Olá. Este é o nome de Olá que será resolvido numa aplicação de Java Olá utilizando Olá JNDI IntialContext.lookup() método.
* **[physical_name]** : nome Olá Olá aplicação Olá do Service Bus entidade toowhich envia ou receber mensagens.

> [!NOTE]
> Se receber de uma subscrição de tópico de barramento de serviço, nome físico Olá especificado no JNDI deve ser o nome de Olá tópico Olá. nome da subscrição Olá é fornecida quando subscrição durável Olá for criada num Olá código da aplicação JMS. Olá [guia para programadores 1.0 AMQP Bus Service](service-bus-amqp-dotnet.md) fornece mais detalhes sobre como trabalhar com tópicos do Service Bus do JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Escrever Olá JMS aplicação
Não são especial APIs ou opções obrigatório quando usar JMS com o Service Bus. No entanto, existem algumas restrições que vai ser abordadas mais tarde. Como com qualquer aplicação JMS, Olá primeiro thing necessária é a configuração do ambiente de JNDI Olá, tooresolve capaz de toobe um **ConnectionFactory** e destinos.

#### <a name="configure-hello-jndi-initialcontext"></a>Configurar Olá JNDI InitialContext
ambiente de JNDI Olá é configurada através da transmissão de uma tabela hash de informações de configuração para o construtor de Olá da classe de javax.naming.InitialContext Olá. dois elementos necessários Olá na tabela hash de Olá são nome de classe de Olá da Olá inicial fábrica de contexto e Olá URL do fornecedor. Olá código seguinte mostra como tooconfigure Olá JNDI ambiente toouse Olá Qpid propriedades baseada em ficheiros JNDI fornecedor com um ficheiro de propriedades com o nome **servicebus.properties**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Uma aplicação de JMS simples utilizando uma fila do Service Bus
Hello do programa seguinte exemplo envia JMS TextMessages tooa fila do Service Bus com o nome lógico de JNDI Olá da fila e recebe mensagens hello do novamente.

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

### <a name="run-hello-application"></a>Executar a aplicação Olá
Executar a aplicação Olá produz saída de formulário Olá:

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

## <a name="cross-platform-messaging-between-jms-and-net"></a>Plataforma de mensagens entre JMS e .NET
Este guia mostrado como toosend e receber mensagens tooand do Service Bus utilizando JMS. No entanto, uma das principais vantagens Olá AMQP 1.0 é o que permite a toobe de aplicações criado a partir do componentes escritos em idiomas diferentes, com mensagens trocadas em fidelidade completa e fiável.

Utilizando a aplicação de JMS de exemplo de Olá descrito acima e uma aplicação .NET semelhante obtidas a partir de um artigo complementar, [utilizando o Service Bus a partir do .NET com AMQP 1.0](service-bus-amqp-dotnet.md), podem trocar mensagens entre .NET e Java. Leia este artigo para obter mais informações sobre os detalhes de Olá de plataforma mensagens utilizando o Service Bus e AMQP 1.0.

### <a name="jms-toonet"></a>JMS too.NET
toodemonstrate JMS too.NET mensagens:

* Inicie a aplicação de exemplo Olá .NET sem quaisquer argumentos da linha de comandos.
* Inicie a aplicação de exemplo Olá Java com o argumento da linha de comandos do Olá "sendonly". Neste modo, hello aplicações não irão receber mensagens da fila de Olá, só irá enviar.
* Prima **Enter** algumas vezes na consola de aplicação de Java Olá, que fará com que toobe de mensagens enviada.
* Estas mensagens são recebidas pelo Olá aplicação .NET.

#### <a name="output-from-jms-application"></a>Resultado da aplicação JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Resultado da aplicação .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>TooJMS de .NET
toodemonstrate tooJMS de .NET de mensagens:

* Inicie a aplicação de exemplo Olá .NET com o argumento da linha de comandos do Olá "sendonly". Neste modo, hello aplicações não irão receber mensagens da fila de Olá, só irá enviar.
* Inicie a aplicação de exemplo Olá Java sem quaisquer argumentos da linha de comandos.
* Prima **Enter** algumas vezes na consola de aplicação .NET de Olá, que fará com que toobe de mensagens enviada.
* Estas mensagens são recebidas pelo Olá aplicação Java.

#### <a name="output-from-net-application"></a>Resultado da aplicação .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Resultado da aplicação JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Restrições e funcionalidades não suportadas
Olá seguintes restrições existe quando utilizar JMS através de AMQP 1.0 com o Service Bus, nomeadamente:

* Apenas um **MessageProducer** ou **MessageConsumer** é permitida por **sessão**. Se precisar de toocreate vários **MessageProducers** ou **MessageConsumers** numa aplicação, crie um dedicado **sessão** para cada um deles.
* Subscrições de tópico voláteis não são atualmente suportadas.
* **MessageSelectors** não são atualmente suportadas.
* Destinos temporários; Por exemplo, **TemporaryQueue**, **TemporaryTopic** não são atualmente suportadas, juntamente com Olá **QueueRequestor** e **TopicRequestor**APIs que as utilizam.
* Sessões transacionadas e transações distribuídas não são suportadas.

## <a name="summary"></a>Resumo
Este tooguide como mostrou como toouse mediadas do Service Bus mensagens funcionalidades (filas e publicar/subscrever tópicos) de Java utilizando Olá populares JMS API e AMQP 1.0.

Também pode utilizar o Service Bus AMQP 1.0 de outros idiomas, incluindo .NET, C, Python e PHP. Componentes construido utilizando estes idiomas diferentes podem trocar mensagens fiável e em fidelidade completa utilizando o suporte de Olá AMQP 1.0 no Service Bus.

## <a name="next-steps"></a>Passos seguintes
* [Suporte de AMQP 1.0 no Service Bus do Azure](service-bus-amqp-overview.md)
* [Como toouse AMQP 1.0 com Olá API .NET do Service Bus](service-bus-dotnet-advanced-message-queuing.md)
* [Service Bus AMQP 1.0 Guia para programadores](service-bus-amqp-dotnet.md)
* [Introdução às filas do Service Bus](service-bus-dotnet-get-started-with-queues.md)
* [Centro de Programadores do Java](https://azure.microsoft.com/develop/java/)

