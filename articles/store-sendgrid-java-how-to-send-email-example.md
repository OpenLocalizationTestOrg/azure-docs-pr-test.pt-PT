---
title: aaastore-sendgrid-Java-How-to-send-email-example
description: "Como toosend e-mail utilizando SendGrid de Java numa implementação do Azure"
services: 
documentationcenter: java
author: thinkingserious
manager: sendgrid
editor: mollybos
ms.assetid: af096a73-6985-4350-92e4-ce1722c8d72f
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 10/30/2014
ms.author: vibhork;dominic.may@sendgrid.com;elmer.thomas@sendgrid.com
ms.openlocfilehash: 51fde1fc71467f8252532b30d2f87856ec25067b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-java-in-an-azure-deployment"></a>Como tooSend SendGrid de E-Mail através do Java numa implementação do Azure
Olá exemplo seguinte mostra como pode utilizar SendGrid toosend e-mails de uma página web alojado no Azure. aplicação resultante Olá pedirá utilizador Olá para os valores de e-mail, conforme mostrado na seguinte captura de ecrã de Olá.

![Formato de correio eletrónico][emailform]

Olá resultante e-mail terá um aspeto semelhante toohello seguinte captura de ecrã.

![Mensagem de correio eletrónico][emailsent]

Vai precisar toodo Olá seguinte código de Olá toouse neste tópico:

1. Obter Olá javax.mail V7, por exemplo a partir de <http://www.oracle.com/technetwork/java/javamail/index.html>.
2. Adicione Olá v7 tooyour caminho de compilação de Java.
3. Se estiver a utilizar Eclipse toocreate esta aplicação de Java, pode incluir as bibliotecas do SendGrid Olá no seu ficheiro de implementação de aplicação (WAR) utilizando a funcionalidade de assemblagem de implementação do Eclipse. Se não estiver a utilizar Eclipse toocreate esta aplicação de Java, certifique-se de bibliotecas de Olá estão incluídas no Olá mesma função do Azure como o caminho de classe de aplicação e adicionado toohello Java da sua aplicação.

Também tem de ter os seus próprios SendGrid nome de utilizador e palavra-passe, correio eletrónico do toobe toosend capaz de Olá. tooget começar SendGrid, consulte [como toosend e-mail utilizando SendGrid de Java](store-sendgrid-java-how-to-send-email.md).

Além disso, familiaridade com informações Olá [criar uma aplicação de Olá mundo do Azure no Eclipse](http://msdn.microsoft.com/library/windowsazure/hh690944), ou com outras técnicas para alojar aplicações Java no Azure, se não estiver a utilizar Eclipse, é vivamente recomendável.

## <a name="create-a-web-form-for-sending-email"></a>Criar um formulário web para enviar correio eletrónico
Olá código a seguir mostra como toocreate uma web formam tooretrieve dados de utilizador para enviar correio eletrónico. Para efeitos deste conteúdo, é denominado o ficheiro JSP Olá **emailform.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email form</title>
    </head>
    <body>
     <p>Fill in all fields and click <b>Send this email</b>.</p>
     <br/>
      <form action="sendemail.jsp" method="post">
       <table>
         <tr>
           <td>To:</td>
           <td><input type="text" size=50 name="emailTo">
           </td>
         </tr>
         <tr>
           <td>From:</td>
           <td><input type="text" size=50 name="emailFrom">
           </td>
         </tr>
         <tr>
           <td>Subject:</td>
           <td><input type="text" size=100 name="emailSubject" value="My email subject">
           </td>
         </tr>
         <tr>
           <td>Text:</td>
           <td><input type="text" size=400 name="emailText" value="Hello,<p>This is my message.</p>Thank you." />
           </td>
         </tr>
         <tr>
           <td>SendGrid user name:</td>
           <td><input type="text" name="sendGridUser">
           </td>
         </tr>
         <tr>
           <td>SendGrid password:</td>
           <td><input type="password" name="sendGridPassword">
           </td>
         </tr>
         <tr>
           <td colspan=2><input type="submit" value="Send this email">
           </td>
         </tr>
       </table>
     </form>
     <br/>
    </body>
    </html>

## <a name="create-hello-code-toosend-hello-email"></a>Criar Olá código toosend Olá e-mail
Olá código seguinte, que é chamado quando concluir o formulário de Olá na emailform.jsp, cria a mensagem de correio eletrónico Olá e envia-a. Para efeitos deste conteúdo, é denominado o ficheiro JSP Olá **sendemail.jsp**.

    <%@ page language="java" contentType="text/html; charset=ISO-8859-1"
        pageEncoding="ISO-8859-1" import="javax.activation.*, javax.mail.*, javax.mail.internet.*, java.util.Date, java.util.Properties" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Email processing happens here</title>
    </head>
    <body>
        <b>This is my send mail page.</b><p/>
     <%

     final String sendGridUser = request.getParameter("sendGridUser");
     final String sendGridPassword = request.getParameter("sendGridPassword");

     class SMTPAuthenticator extends Authenticator
     {
       public PasswordAuthentication getPasswordAuthentication()
       {
            String username = sendGridUser;
            String password = sendGridPassword;

            return new PasswordAuthentication(username, password);   
       }
     }
     try
     {

         // hello SendGrid SMTP server.
         String SMTP_HOST_NAME = "smtp.sendgrid.net";

         Properties properties;

         properties = new Properties();

         // Specify SMTP values.
         properties.put("mail.transport.protocol", "smtp");
         properties.put("mail.smtp.host", SMTP_HOST_NAME);
         properties.put("mail.smtp.port", 587);
         properties.put("mail.smtp.auth", "true");

         // Display hello email fields entered by hello user. 
         out.println("Value entered for email Subject: " + request.getParameter("emailSubject") + "<br/>");        
         out.println("Value entered for email      To: " + request.getParameter("emailTo") + "<br/>");
         out.println("Value entered for email    From: " + request.getParameter("emailFrom") + "<br/>");
         out.println("Value entered for email    Text: " + "<br/>" + request.getParameter("emailText") + "<br/>");

         // Create hello authenticator object.
         Authenticator authenticator = new SMTPAuthenticator();

         // Create hello mail session object.
         Session mailSession;
         mailSession = Session.getDefaultInstance(properties, authenticator);

         // Display debug information toostdout, useful when using the
         // compute emulator during development.
         mailSession.setDebug(true);

         // Create hello message and message part objects.
         MimeMessage message;
         Multipart multipart;
         MimeBodyPart messagePart; 

         message = new MimeMessage(mailSession);

         multipart = new MimeMultipart("alternative");
         messagePart = new MimeBodyPart();
         messagePart.setContent(request.getParameter("emailText"), "text/html");
         multipart.addBodyPart(messagePart);            

         // Specify hello email To, From, Subject and Content. 
         message.setFrom(new InternetAddress(request.getParameter("emailFrom")));
         message.addRecipient(Message.RecipientType.TO, new InternetAddress(request.getParameter("emailTo")));
         message.setSubject(request.getParameter("emailSubject")); 
         message.setContent(multipart);

         // Uncomment hello following if you want tooadd a footer.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"footer\": {\"settings\": {\"enable\":1,\"text/html\": \"<html>This is my <b>email footer</b>.</html>\"}}}}");

         // Uncomment hello following if you want tooenable click tracking.
         // message.addHeader("X-SMTPAPI", "{\"filters\": {\"clicktrack\": {\"settings\": {\"enable\":1}}}}");

         Transport transport;
         transport = mailSession.getTransport();
         // Connect hello transport object.
         transport.connect();
         // Send hello message.
         transport.sendMessage(message,  message.getRecipients(Message.RecipientType.TO));
         // Close hello connection.
         transport.close();

        out.println("<p>Email processing completed.</p>");

     }
     catch (Exception e)
     {
         out.println("<p>Exception encountered: " + 
                            e.getMessage()     +
                            "</p>");   
     }
    %>

    </body>
    </html>

Além disso toosending Olá e-mail, o emailform.jsp fornece um resultado para o utilizador Olá; um exemplo é Olá captura de ecrã a seguir:

![Enviar o resultado de correio][emailresult]

## <a name="next-steps"></a>Passos seguintes
Implementar o emulador de computação de toohello de aplicação e dentro de um browser executar emailform.jsp, introduza valores no formulário de Olá, clique em **envie este e-mail**e, em seguida, ver os resultados no sendemail.jsp.

Este código foi fornecido tooshow como toouse SendGrid em Java no Azure. Antes de implementar tooAzure na produção, poderá ser útil tooadd mais processamento de erros ou outras funcionalidades. Por exemplo: 

* Pode utilizar blobs de armazenamento do Azure ou endereços de correio eletrónico toostore de base de dados SQL e mensagens de e-mail, em vez de utilizar um formulário web. Para obter informações sobre a utilização de blobs de armazenamento do Azure em Java, consulte [como tooUse Olá o serviço de armazenamento de BLOBs de Java](https://azure.microsoft.com/develop/java/how-to-guides/blob-storage/). Para obter informações sobre como utilizar a base de dados do SQL em Java, consulte [utilizando a base de dados SQL em Java](https://azure.microsoft.com/develop/java/how-to-guides/using-sql-azure-in-java/).
* Pode utilizar `RoleEnvironment.getConfigurationSettings` tooretrieve Olá SendGrid username e a palavra-passe de definições de configuração da implementação, em vez de utilizar Olá tooretrieve de formulário web esses valores. Para obter informações sobre Olá `RoleEnvironment` classe, consulte [Using Olá biblioteca de tempo de execução do serviço do Azure no JSP](http://msdn.microsoft.com/library/windowsazure/hh690948) e a documentação do pacote de Runtime do serviço de Azure Olá em <http://dl.windowsazure.com/javadoc>.
* Para obter mais informações sobre a utilização do SendGrid em Java, consulte [como toosend e-mail utilizando SendGrid de Java](store-sendgrid-java-how-to-send-email.md).

[emailform]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailform.jpg
[emailsent]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaEmailSent.jpg
[emailresult]: ./media/store-sendgrid-java-how-to-send-email-example/SendGridJavaResult.jpg
