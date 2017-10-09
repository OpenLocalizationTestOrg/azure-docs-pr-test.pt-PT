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
# <a name="how-toosend-email-using-sendgrid-from-java"></a><span data-ttu-id="a211a-104">Como tooSend SendGrid de E-Mail através do Java</span><span class="sxs-lookup"><span data-stu-id="a211a-104">How tooSend Email Using SendGrid from Java</span></span>
<span data-ttu-id="a211a-105">Este guia demonstra como de programação de tarefas comuns tooperform com o SendGrid e-mail serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="a211a-105">This guide demonstrates how tooperform common programming tasks with the SendGrid email service on Azure.</span></span> <span data-ttu-id="a211a-106">Exemplos de Olá são escritos em Java.</span><span class="sxs-lookup"><span data-stu-id="a211a-106">hello samples are written in Java.</span></span> <span data-ttu-id="a211a-107">Olá os cenários abrangidos incluem **construir e-mail**, **enviar correio eletrónico**, **adicionar anexos**, **utilizando filtros**e **atualizar propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a211a-107">hello scenarios covered include **constructing email**, **sending email**, **adding attachments**, **using filters**, and **updating properties**.</span></span> <span data-ttu-id="a211a-108">Para obter mais informações sobre SendGrid e enviar correio eletrónico, consulte Olá [passos](#next-steps) secção.</span><span class="sxs-lookup"><span data-stu-id="a211a-108">For more information on SendGrid and sending email, see hello [Next steps](#next-steps) section.</span></span>

## <a name="what-is-hello-sendgrid-email-service"></a><span data-ttu-id="a211a-109">O que é Olá SendGrid serviço de E-Mail?</span><span class="sxs-lookup"><span data-stu-id="a211a-109">What is hello SendGrid Email Service?</span></span>
<span data-ttu-id="a211a-110">SendGrid é um [serviço baseado na nuvem e-mail] que fornece fiável [entrega de correio eletrónico transacional], escalabilidade e a análise em tempo real, juntamente com APIs flexíveis que o facilitar a integração personalizados.</span><span class="sxs-lookup"><span data-stu-id="a211a-110">SendGrid is a [cloud-based email service] that provides reliable [transactional email delivery], scalability, and real-time analytics along with flexible APIs that make custom integration easy.</span></span> <span data-ttu-id="a211a-111">Cenários comuns de utilização do SendGrid incluem:</span><span class="sxs-lookup"><span data-stu-id="a211a-111">Common SendGrid usage scenarios include:</span></span>

* <span data-ttu-id="a211a-112">Enviar automaticamente os recibos toocustomers</span><span class="sxs-lookup"><span data-stu-id="a211a-112">Automatically sending receipts toocustomers</span></span>
* <span data-ttu-id="a211a-113">Administrar distribuição lista para enviar aos clientes i-fliers mensais e ofertas especiais</span><span class="sxs-lookup"><span data-stu-id="a211a-113">Administering distribution lists for sending customers monthly e-fliers and special offers</span></span>
* <span data-ttu-id="a211a-114">Recolher métricas em tempo real para coisas como bloqueado por correio eletrónico e a capacidade de resposta do cliente</span><span class="sxs-lookup"><span data-stu-id="a211a-114">Collecting real-time metrics for things like blocked e-mail, and customer responsiveness</span></span>
* <span data-ttu-id="a211a-115">Gerar relatórios toohelp identificar tendências</span><span class="sxs-lookup"><span data-stu-id="a211a-115">Generating reports toohelp identify trends</span></span>
* <span data-ttu-id="a211a-116">Pedidos de cliente de reencaminhamento</span><span class="sxs-lookup"><span data-stu-id="a211a-116">Forwarding customer inquiries</span></span>
* <span data-ttu-id="a211a-117">Notificações de correio eletrónico da sua aplicação</span><span class="sxs-lookup"><span data-stu-id="a211a-117">Email notifications from your application</span></span>

<span data-ttu-id="a211a-118">Para obter mais informações, consulte <http://sendgrid.com>.</span><span class="sxs-lookup"><span data-stu-id="a211a-118">For more information, see <http://sendgrid.com>.</span></span>

## <a name="create-a-sendgrid-account"></a><span data-ttu-id="a211a-119">Criar uma conta do SendGrid</span><span class="sxs-lookup"><span data-stu-id="a211a-119">Create a SendGrid account</span></span>
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="how-to-use-hello-javaxmail-libraries"></a><span data-ttu-id="a211a-120">Como: utilizar Olá javax.mail bibliotecas</span><span class="sxs-lookup"><span data-stu-id="a211a-120">How to: Use hello javax.mail libraries</span></span>
<span data-ttu-id="a211a-121">Obtenha as bibliotecas de javax.mail Olá, por exemplo do <http://www.oracle.com/technetwork/java/javamail> e importe-as para o seu código.</span><span class="sxs-lookup"><span data-stu-id="a211a-121">Obtain hello javax.mail libraries, for example from <http://www.oracle.com/technetwork/java/javamail> and import them into your code.</span></span> <span data-ttu-id="a211a-122">A um nível elevado, hello processo para utilizar Olá javax.mail biblioteca toosend e-mail através de SMTP é seguinte de Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="a211a-122">At a high-level, hello process for using hello javax.mail library toosend email using SMTP is toodo hello following:</span></span>

1. <span data-ttu-id="a211a-123">Especifique os valores de SMTP Olá, incluindo o servidor de SMTP Olá, que para SendGrid smtp.sendgrid.net.</span><span class="sxs-lookup"><span data-stu-id="a211a-123">Specify hello SMTP values, including hello SMTP server, which for SendGrid is smtp.sendgrid.net.</span></span>

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

1. <span data-ttu-id="a211a-124">Expandir Olá *javax.mail.Authenticator* classe e na sua implementação do *getPasswordAuthentication* método, devolver o nome de utilizador do SendGrid e a palavra-passe.</span><span class="sxs-lookup"><span data-stu-id="a211a-124">Extend hello *javax.mail.Authenticator* class, and in your implementation of the *getPasswordAuthentication* method, return your SendGrid user name and password.</span></span>  

       private class SMTPAuthenticator extends javax.mail.Authenticator {
       public PasswordAuthentication getPasswordAuthentication() {
          String username = SMTP_AUTH_USER;
          String password = SMTP_AUTH_PWD;
          return new PasswordAuthentication(username, password);
       }
2. <span data-ttu-id="a211a-125">Criar uma sessão de e-mail autenticado através de um *javax.mail.Session* objeto.</span><span class="sxs-lookup"><span data-stu-id="a211a-125">Create an authenticated email session through a *javax.mail.Session* object.</span></span>  

       Authenticator auth = new SMTPAuthenticator();
       Session mailSession = Session.getDefaultInstance(properties, auth);
3. <span data-ttu-id="a211a-126">Crie a sua mensagem e atribuir **para**, **de**, **requerente** e valores de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a211a-126">Create your message and assign **To**, **From**, **Subject** and content values.</span></span> <span data-ttu-id="a211a-127">Isto é apresentado na Olá [como: criar uma mensagem de E-Mail](#how-to-create-an-email) secção.</span><span class="sxs-lookup"><span data-stu-id="a211a-127">This is shown in hello [How To: Create an Email](#how-to-create-an-email) section.</span></span>
4. <span data-ttu-id="a211a-128">Enviar mensagem de saudação através de um *javax.mail.Transport* objeto.</span><span class="sxs-lookup"><span data-stu-id="a211a-128">Send hello message through a *javax.mail.Transport* object.</span></span> <span data-ttu-id="a211a-129">Isto é apresentado na Olá [como: enviar um E-Mail] [como: enviar um E-Mail] secção.</span><span class="sxs-lookup"><span data-stu-id="a211a-129">This is shown in hello [How To: Send an Email][How to: Send an Email] section.</span></span>

## <a name="how-to-create-an-email"></a><span data-ttu-id="a211a-130">Como: criar uma mensagem de e-mail</span><span class="sxs-lookup"><span data-stu-id="a211a-130">How to: Create an email</span></span>
<span data-ttu-id="a211a-131">seguinte Olá mostra como toospecify valores para uma mensagem de e-mail.</span><span class="sxs-lookup"><span data-stu-id="a211a-131">hello following shows how toospecify values for an email.</span></span>

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

## <a name="how-to-send-an-email"></a><span data-ttu-id="a211a-132">Como: enviar uma mensagem de e-mail</span><span class="sxs-lookup"><span data-stu-id="a211a-132">How to: Send an email</span></span>
<span data-ttu-id="a211a-133">Olá a seguir mostra como toosend uma mensagem de e-mail.</span><span class="sxs-lookup"><span data-stu-id="a211a-133">hello following shows how toosend an email.</span></span>

    Transport transport = mailSession.getTransport();
    // Connect hello transport object.
    transport.connect();
    // Send hello message.
    transport.sendMessage(message, message.getAllRecipients());
    // Close hello connection.
    transport.close();

## <a name="how-to-add-an-attachment"></a><span data-ttu-id="a211a-134">Como: adicionar um anexo</span><span class="sxs-lookup"><span data-stu-id="a211a-134">How to: Add an attachment</span></span>
<span data-ttu-id="a211a-135">Olá código seguinte mostra como tooadd um anexo.</span><span class="sxs-lookup"><span data-stu-id="a211a-135">hello following code shows you how tooadd an attachment.</span></span>

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

## <a name="how-to-use-filters-tooenable-footers-tracking-and-analytics"></a><span data-ttu-id="a211a-136">Como: utilizar filtra tooenable rodapés de página, controlo e análise</span><span class="sxs-lookup"><span data-stu-id="a211a-136">How to: Use filters tooenable footers, tracking, and analytics</span></span>
<span data-ttu-id="a211a-137">SendGrid fornece funcionalidades de e-mail adicionais através da utilização de Olá de *filtros*.</span><span class="sxs-lookup"><span data-stu-id="a211a-137">SendGrid provides additional email functionality through hello use of *filters*.</span></span> <span data-ttu-id="a211a-138">Estas são as definições que podem ser adicionadas tooan mensagem de e-mail para ativar a funcionalidade específica, como ativar o controlo de clique, do Google analytics, subscrição de controlo, e assim sucessivamente.</span><span class="sxs-lookup"><span data-stu-id="a211a-138">These are settings that can be added tooan email message to enable specific functionality such as enabling click tracking, Google analytics, subscription tracking, and so on.</span></span> <span data-ttu-id="a211a-139">Para obter uma lista completa de filtros, consulte [definições de filtro][Filter Settings].</span><span class="sxs-lookup"><span data-stu-id="a211a-139">For a full list of filters, see [Filter Settings][Filter Settings].</span></span>

* <span data-ttu-id="a211a-140">seguinte Olá mostra como tooinsert um rodapé filtrar que resulta na apresentação na parte inferior de Olá do correio eletrónico Olá enviado de texto HTML.</span><span class="sxs-lookup"><span data-stu-id="a211a-140">hello following shows how tooinsert a footer filter that results in HTML text appearing at hello bottom of hello email being sent.</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"footer\":
          {\"settings\":
          {\"enable\":1,\"text/html\":
          \"<html><b>Thank you</b> for your business.</html>\"}}}}");
* <span data-ttu-id="a211a-141">Outro exemplo de um filtro é clique controlo.</span><span class="sxs-lookup"><span data-stu-id="a211a-141">Another example of a filter is click tracking.</span></span> <span data-ttu-id="a211a-142">Digamos que o texto de e-mail contém uma hiperligação, tais como hello seguinte e pretender que tootrack Olá clique taxa:</span><span class="sxs-lookup"><span data-stu-id="a211a-142">Let’s say that your email text contains a hyperlink, such as hello following, and you want tootrack hello click rate:</span></span>

      messagePart.setContent(
          "Hello,
          <p>This is hello body of hello message. Visit
          <a href='http://www.contoso.com'>http://www.contoso.com</a>.</p>
          Thank you.",
          "text/html");
* <span data-ttu-id="a211a-143">Olá tooenable clique controlo Olá utilize seguinte código:</span><span class="sxs-lookup"><span data-stu-id="a211a-143">tooenable hello click tracking, use hello following code:</span></span>

      message.addHeader("X-SMTPAPI",
          "{\"filters\":
          {\"clicktrack\":
          {\"settings\":
          {\"enable\":1}}}}");

## <a name="how-to-update-email-properties"></a><span data-ttu-id="a211a-144">Como: propriedades de correio eletrónico de atualização</span><span class="sxs-lookup"><span data-stu-id="a211a-144">How to: Update email properties</span></span>
<span data-ttu-id="a211a-145">Algumas propriedades de correio eletrónico podem ser substituídas utilizando  **definir*propriedade** * ou estar anexados utilizando  **adicionar*propriedade** *.</span><span class="sxs-lookup"><span data-stu-id="a211a-145">Some email properties can be overwritten using **set*Property*** or appended using **add*Property***.</span></span>

<span data-ttu-id="a211a-146">Por exemplo, toospecify **ReplyTo** endereços, utilize o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="a211a-146">For example, toospecify **ReplyTo** addresses, use hello following:</span></span>

    InternetAddress addresses[] =
        { new InternetAddress("john@contoso.com"),
          new InternetAddress("wendy@contoso.com") };

    message.setReplyTo(addresses);

<span data-ttu-id="a211a-147">tooadd um **Cc** seguinte de Olá do destinatário, utilize:</span><span class="sxs-lookup"><span data-stu-id="a211a-147">tooadd a **Cc** recipient, use hello following:</span></span>

    message.addRecipient(Message.RecipientType.CC, new
    InternetAddress("john@contoso.com"));

## <a name="how-to-use-additional-sendgrid-services"></a><span data-ttu-id="a211a-148">Como: utilizar os serviços do SendGrid adicionais</span><span class="sxs-lookup"><span data-stu-id="a211a-148">How to: Use additional SendGrid services</span></span>
<span data-ttu-id="a211a-149">SendGrid oferece as APIs baseadas na web que pode utilizar a funcionalidade de SendGrid adicional tooleverage da sua aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="a211a-149">SendGrid offers web-based APIs that you can use tooleverage additional SendGrid functionality from your Azure application.</span></span> <span data-ttu-id="a211a-150">Para mais informações, consulte Olá [documentação da API do SendGrid][SendGrid API documentation].</span><span class="sxs-lookup"><span data-stu-id="a211a-150">For full details, see hello [SendGrid API documentation][SendGrid API documentation].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a211a-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a211a-151">Next steps</span></span>
<span data-ttu-id="a211a-152">Agora que aprendeu as noções básicas de Olá de Olá serviço de E-Mail do SendGrid, siga estes toolearn ligações mais.</span><span class="sxs-lookup"><span data-stu-id="a211a-152">Now that you’ve learned hello basics of hello SendGrid Email service, follow these links toolearn more.</span></span>

* <span data-ttu-id="a211a-153">Amostra que demonstra utilizando SendGrid numa implementação do Azure: [como toosend e-mail utilizando SendGrid de Java numa implementação do Azure](store-sendgrid-java-how-to-send-email-example.md)</span><span class="sxs-lookup"><span data-stu-id="a211a-153">Sample that demonstrates using SendGrid in an Azure deployment: [How toosend email using SendGrid from Java in an Azure deployment](store-sendgrid-java-how-to-send-email-example.md)</span></span>
* <span data-ttu-id="a211a-154">SDK de Java do SendGrid: <https://sendgrid.com/docs/Code_Examples/java.html></span><span class="sxs-lookup"><span data-stu-id="a211a-154">SendGrid Java SDK: <https://sendgrid.com/docs/Code_Examples/java.html></span></span>
* <span data-ttu-id="a211a-155">Documentação da API do SendGrid: <https://sendgrid.com/docs/API_Reference/index.html></span><span class="sxs-lookup"><span data-stu-id="a211a-155">SendGrid API documentation: <https://sendgrid.com/docs/API_Reference/index.html></span></span>
* <span data-ttu-id="a211a-156">Oferta especial de SendGrid para clientes do Azure: <https://sendgrid.com/windowsazure.html></span><span class="sxs-lookup"><span data-stu-id="a211a-156">SendGrid special offer for Azure customers: <https://sendgrid.com/windowsazure.html></span></span>

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
