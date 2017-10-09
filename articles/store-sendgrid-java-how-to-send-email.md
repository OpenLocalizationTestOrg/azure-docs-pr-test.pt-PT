---
title: "aaaHow toouse Olá serviço de e-mail do SendGrid (Java) | Microsoft Docs"
description: "Saiba como enviar correio eletrónico com Olá serviço de e-mail do SendGrid no Azure. Exemplos de código escrito em Java."
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: cc75c43e-ede9-492b-98c2-9147fcb92c21
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: elmer.thomas@sendgrid.com; erika.berkland@sendgrid.com; vibhork
ms.openlocfilehash: 542ce0003e94fc8f5551487d5a3cd6f75d27e8cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java"></a>Como tooSend SendGrid de E-Mail através do Java
Este guia demonstra como de programação de tarefas comuns tooperform com o SendGrid e-mail serviço no Azure. Exemplos de Olá são escritos em Java. Olá os cenários abrangidos incluem **construir e-mail**, **enviar correio eletrónico**, **adicionar anexos**, **utilizando filtros**e **atualizar propriedades**. Para obter mais informações sobre SendGrid e enviar correio eletrónico, consulte Olá [passos](#next-steps) secção.

## <a name="what-is-hello-sendgrid-email-service"></a>O que é Olá SendGrid serviço de E-Mail?
SendGrid é um [serviço baseado na nuvem e-mail] que fornece fiável [entrega de correio eletrónico transacional], escalabilidade e a análise em tempo real, juntamente com APIs flexíveis que o facilitar a integração personalizados. Cenários comuns de utilização do SendGrid incluem:

* Enviar automaticamente os recibos toocustomers
* Administrar distribuição lista para enviar aos clientes i-fliers mensais e ofertas especiais
* Recolher métricas em tempo real para coisas como bloqueado por correio eletrónico e a capacidade de resposta do cliente
* Gerar relatórios toohelp identificar tendências
* Pedidos de cliente de reencaminhamento
* Notificações de correio eletrónico da sua aplicação

Para obter mais informações, consulte <http://sendgrid.com>.

## <a name="create-a-sendgrid-account"></a>Criar uma conta do SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a>Como: utilizar Olá javax.mail bibliotecas
Obtenha as bibliotecas de javax.mail Olá, por exemplo do <http://www.oracle.com/technetwork/java/javamail> e importe-as para o seu código. A um nível elevado, hello processo para utilizar Olá javax.mail biblioteca toosend e-mail através de SMTP é seguinte de Olá toodo:

1. Especifique os valores de SMTP Olá, incluindo o servidor de SMTP Olá, que para SendGrid smtp.sendgrid.net.

```
        import java.util.Properties;
        import javax.activation.*;
        import javax.mail.*;
        import javax.mail.internet.*;

        public class MyEmailer {
           private static final String SMTP_HOST_NAME = "smtp.sendgrid.net";
           private static final String SMTP_AUTH_USER = "your_sendgrid_username";
           private static final String SMTP_AUTH_PWD = "your_sendgrid_password";

           public static void main(String[] args) throws Exception{
               new MyEmailer().SendMail();
           }

           public void SendMail() throws Exception
           {
              Properties properties = new Properties();
                 properties.put("mail.transport.protocol", "smtp");
                 properties.put("mail.smtp.host", SMTP_HOST_NAME);
                 properties.put("mail.smtp.port", 587);
                 properties.put("mail.smtp.auth", "true");
                 // …
```

1. Expandir Olá *javax.mail.Authenticator* classe e na sua implementação do *getPasswordAuthentication* método, devolver o nome de utilizador do SendGrid e a palavra-passe.  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. Criar uma sessão de e-mail autenticado através de um *javax.mail.Session* objeto.  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. Crie a sua mensagem e atribuir **para**, **de**, **requerente** e valores de conteúdo. Isto é apresentado na Olá [como: criar uma mensagem de E-Mail](#how-to-create-an-email) secção.
4. Enviar mensagem de saudação através de um *javax.mail.Transport* objeto. Isto é apresentado na Olá [como: enviar um E-Mail] [como: enviar um E-Mail] secção.

## <a name="how-to-create-an-email"></a>Como: criar uma mensagem de e-mail
seguinte Olá mostra como toospecify valores para uma mensagem de e-mail.

    MimeMessage message = new MimeMessage(mailSession);
    Multipart multipart = new MimeMultipart("alternative");
    BodyPart part1 = new MimeBodyPart();
    part1.setText("Hello, Your Contoso order has shipped. Thank you, John");
    BodyPart part2 = new MimeBodyPart();
    part2.setContent(
        "<p>Hello,</p>
        <p>Your Contoso order has <b>shipped</b>.</p>
        <p>Thank you,<br>John</br></p>",
        "text/html");
    multipart.addBodyPart(part1);
    multipart.addBodyPart(part2);
    message.setFrom(new InternetAddress("john@contoso.com"));
    message.addRecipient(Message.RecipientType.TO,
       new InternetAddress("someone@example.com"));
    message.setSubject("Your recent order");
    message.setContent(multipart);

## <a name="how-to-send-an-email"></a>Como: enviar uma mensagem de e-mail
Olá a seguir mostra como toosend uma mensagem de e-mail.

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a>Como: adicionar um anexo
Olá código seguinte mostra como tooadd um anexo.

    // Local file name and path.
    String attachmentName = "myfile.zip";
    String attachmentPath = "c:\\myfiles\\";
    MimeBodyPart attachmentPart = new MimeBodyPart();
    // Specify hello local file tooattach.
    DataSource source = new FileDataSource(attachmentPath + attachmentName);
    attachmentPart.setDataHandler(new DataHandler(source));
    // This example uses hello local file name as hello attachment name.
    // They could be different if you prefer.
    attachmentPart.setFileName(attachmentName);
    multipart.addBodyPart(attachmentPart);

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a>Como: utilizar filtra tooenable rodapés de página, controlo e análise
SendGrid fornece funcionalidades de e-mail adicionais através da utilização de Olá de *filtros*. Estas são as definições que podem ser adicionadas tooan mensagem de e-mail para ativar a funcionalidade específica, como ativar o controlo de clique, do Google analytics, subscrição de controlo, e assim sucessivamente. Para obter uma lista completa de filtros, consulte [definições de filtro][Filter Settings].

* seguinte Olá mostra como tooinsert um rodapé filtrar que resulta na apresentação na parte inferior de Olá do correio eletrónico Olá enviado de texto HTML.

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* Outro exemplo de um filtro é clique controlo. Digamos que o texto de e-mail contém uma hiperligação, tais como hello seguinte e pretender que tootrack Olá clique taxa:

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* Olá tooenable clique controlo Olá utilize seguinte código:

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a>Como: propriedades de correio eletrónico de atualização
Algumas propriedades de correio eletrónico podem ser substituídas utilizando  **definir*propriedade** * ou estar anexados utilizando  **adicionar*propriedade** *.

Por exemplo, toospecify **ReplyTo** endereços, utilize o seguinte Olá:

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

tooadd um **Cc** seguinte de Olá do destinatário, utilize:

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a>Como: utilizar os serviços do SendGrid adicionais
SendGrid oferece as APIs baseadas na web que pode utilizar a funcionalidade de SendGrid adicional tooleverage da sua aplicação do Azure. Para mais informações, consulte Olá [documentação da API do SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu as noções básicas de Olá de Olá serviço de E-Mail do SendGrid, siga estes toolearn ligações mais.

* Amostra que demonstra utilizando SendGrid numa implementação do Azure: [como toosend e-mail utilizando SendGrid de Java numa implementação do Azure](store-sendgrid-java-how-to-send-email-example.md)
* SDK de Java do SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html>
* Documentação da API do SendGrid: <https://sendgrid.com/docs/API_Reference/index.html>
* Oferta especial de SendGrid para clientes do Azure: <https://sendgrid.com/windowsazure.html>

[http://sendgrid.com]: https://sendgrid.com
[http://sendgrid.com/pricing.html]: http://sendgrid.com/pricing.html
[http://www.sendgrid.com/azure.html]: https://www.sendgrid.com/windowsazure.html
[http://sendgrid.com/features]: https://sendgrid.com/features
[http://www.oracle.com/technetwork/java/javamail]: http://www.oracle.com/technetwork/java/javamail/index.html
[Filter Settings]: https://sendgrid.com/docs/API_Reference/Web_API/filter_settings.html
[SendGrid API documentation]: https://sendgrid.com/docs/API_Reference/index.html
[http://sendgrid.com/azure.html]: https://sendgrid.com/windowsazure.html
[serviço baseado na nuvem e-mail]: https://sendgrid.com/email-solutions
[entrega de correio eletrónico transacional]: https://sendgrid.com/transactional-email
