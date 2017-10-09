---
title: "aaaHow tooConfigure autenticação mútua do TLS para a aplicação Web"
description: "Saiba como tooconfigure o aplicação web toouse cliente autenticação de certificado no TLS."
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: cd1d15d3-2d9e-4502-9f11-a306dac4453a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2016
ms.author: naziml
ms.openlocfilehash: 8aeb9b35058fac50b8b38f6428207ad4a82d8637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-tls-mutual-authentication-for-web-app"></a>Como tooConfigure autenticação mútua do TLS para a aplicação Web
## <a name="overview"></a>Descrição geral
Pode restringir a aplicação de web do Azure do acesso tooyour Ativando a diferentes tipos de autenticação para o mesmo. Por isso, toodo unidirecional é tooauthenticate a utilizar um certificado de cliente, quando pedido Olá é efetuada através de TLS/SSL. Este mecanismo denomina-se a autenticação mútua TLS ou autenticação de certificado de cliente e apresenta em pormenor neste artigo como toosetup a autenticação de certificados de cliente de toouse de aplicação de web.

> **Nota:** se aceder ao site por HTTP e HTTPS não, não irá receber qualquer certificado de cliente. Por isso, se a sua aplicação precisar de certificados de cliente, deve não permitem que pedidos tooyour aplicação através de HTTP.
> 
> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="configure-web-app-for-client-certificate-authentication"></a>Configurar aplicação Web para autenticação de certificados de cliente
toosetup os certificados de cliente do toorequire do web aplicação que terá tooadd Olá clientCertEnabled site definição para a sua aplicação web e configurá-lo tootrue. Esta definição não está atualmente disponível através de experiência de gestão de Olá no Olá Portal e Olá REST API irá precisar tooaccomplish toobe utilizado.

Pode utilizar Olá [ARMClient ferramenta](https://github.com/projectkudu/ARMClient) toomake-toocraft fácil Olá chamada da REST API. Depois de iniciar sessão com a ferramenta de Olá, terá de Olá tooissue os seguintes comandos:

    ARMClient PUT subscriptions/{Subscription Id}/resourcegroups/{Resource Group Name}/providers/Microsoft.Web/sites/{Website Name}?api-version=2015-04-01 @enableclientcert.json -verbose

Substituir tudo na {} com informações da sua aplicação web e criar um ficheiro chamado enableclientcert.json com Olá seguinte JSON conteúdo:

    {
        "location": "My Web App Location",
        "properties": {
            "clientCertEnabled": true
        }
    }

Certifique-se toochange valor Olá toowherever "localização" a aplicação web está localizado por exemplo, Norte Central nos ou oeste E.U.A. etc.

Também pode utilizar https://resources.azure.com tooflip Olá `clientCertEnabled` propriedade demasiado`true`.

> **Nota:** se executar ARMClient a partir do Powershell, terá de Olá tooescape símbolo @ para o ficheiro JSON Olá com um back-marcas de escala '.
> 
> 

## <a name="accessing-hello-client-certificate-from-your-web-app"></a>Aceder ao hello do cliente certificado da sua aplicação Web
Se estiver a utilizar o ASP.NET e configurar a autenticação de certificados de cliente de toouse de aplicação, o certificado de Olá estará disponível através de Olá **HttpRequest.ClientCertificate** propriedade. Para outras pilhas de aplicação, certificados de cliente Olá estarão disponíveis na sua aplicação através de um valor de codificado em base64 no cabeçalho de pedido de "X-ARR-ClientCert" Olá. A aplicação pode criar um certificado a partir deste valor e, em seguida, utilizá-lo para efeitos de autenticação e autorização na sua aplicação.

## <a name="special-considerations-for-certificate-validation"></a>Considerações especiais sobre a validação de certificado
certificado de cliente Olá, que é enviado toohello aplicação não seguir qualquer validação pela plataforma de Web Apps do Azure Olá. Validar este certificado é a responsabilidade de Olá da aplicação web de Olá. Eis o código de ASP.NET de exemplo que valida as propriedades do certificado para efeitos de autenticação.

    using System;
    using System.Collections.Specialized;
    using System.Security.Cryptography.X509Certificates;
    using System.Web;

    namespace ClientCertificateUsageSample
    {
        public partial class cert : System.Web.UI.Page
        {
            public string certHeader = "";
            public string errorString = "";
            private X509Certificate2 certificate = null;
            public string certThumbprint = "";
            public string certSubject = "";
            public string certIssuer = "";
            public string certSignatureAlg = "";
            public string certIssueDate = "";
            public string certExpiryDate = "";
            public bool isValidCert = false;

            //
            // Read hello certificate from hello header into an X509Certificate2 object
            // Display properties of hello certificate on hello page
            //
            protected void Page_Load(object sender, EventArgs e)
            {
                NameValueCollection headers = base.Request.Headers;
                certHeader = headers["X-ARR-ClientCert"];
                if (!String.IsNullOrEmpty(certHeader))
                {
                    try
                    {
                        byte[] clientCertBytes = Convert.FromBase64String(certHeader);
                        certificate = new X509Certificate2(clientCertBytes);
                        certSubject = certificate.Subject;
                        certIssuer = certificate.Issuer;
                        certThumbprint = certificate.Thumbprint;
                        certSignatureAlg = certificate.SignatureAlgorithm.FriendlyName;
                        certIssueDate = certificate.NotBefore.ToShortDateString() + " " + certificate.NotBefore.ToShortTimeString();
                        certExpiryDate = certificate.NotAfter.ToShortDateString() + " " + certificate.NotAfter.ToShortTimeString();
                    }
                    catch (Exception ex)
                    {
                        errorString = ex.ToString();
                    }
                    finally 
                    {
                        isValidCert = IsValidClientCertificate();
                        if (!isValidCert) Response.StatusCode = 403;
                        else Response.StatusCode = 200;
                    }
                }
                else
                {
                    certHeader = "";
                }
            }

            //
            // This is a SAMPLE verification routine. Depending on your application logic and security requirements, 
            // you should modify this method
            //
            private bool IsValidClientCertificate()
            {
                // In this example we will only accept hello certificate as a valid certificate if all hello conditions below are met:
                // 1. hello certificate is not expired and is active for hello current time on server.
                // 2. hello subject name of hello certificate has hello common name nildevecc
                // 3. hello issuer name of hello certificate has hello common name nildevecc and organization name Microsoft Corp
                // 4. hello thumbprint of hello certificate is 30757A2E831977D8BD9C8496E4C99AB26CB9622B
                //
                // This example does NOT test that this certificate is chained tooa Trusted Root Authority (or revoked) on hello server 
                // and it allows for self signed certificates
                //

                if (certificate == null || !String.IsNullOrEmpty(errorString)) return false;

                // 1. Check time validity of certificate
                if (DateTime.Compare(DateTime.Now, certificate.NotBefore) < 0 || DateTime.Compare(DateTime.Now, certificate.NotAfter) > 0) return false;

                // 2. Check subject name of certificate
                bool foundSubject = false;
                string[] certSubjectData = certificate.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certSubjectData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundSubject = true;
                        break;
                    }
                }
                if (!foundSubject) return false;

                // 3. Check issuer name of certificate
                bool foundIssuerCN = false, foundIssuerO = false;
                string[] certIssuerData = certificate.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
                foreach (string s in certIssuerData)
                {
                    if (String.Compare(s.Trim(), "CN=nildevecc") == 0)
                    {
                        foundIssuerCN = true;
                        if (foundIssuerO) break;
                    }

                    if (String.Compare(s.Trim(), "O=Microsoft Corp") == 0)
                    {
                        foundIssuerO = true;
                        if (foundIssuerCN) break;
                    }
                }

                if (!foundIssuerCN || !foundIssuerO) return false;

                // 4. Check thumprint of certificate
                if (String.Compare(certificate.Thumbprint.Trim().ToUpper(), "30757A2E831977D8BD9C8496E4C99AB26CB9622B") != 0) return false;

                // If you also want tootest if hello certificate chains tooa Trusted Root Authority you can uncomment hello code below
                //
                //X509Chain certChain = new X509Chain();
                //certChain.Build(certificate);
                //bool isValidCertChain = true;
                //foreach (X509ChainElement chElement in certChain.ChainElements)
                //{
                //    if (!chElement.Certificate.Verify())
                //    {
                //        isValidCertChain = false;
                //        break;
                //    }
                //}
                //if (!isValidCertChain) return false;

                return true;
            }
        }
    }
