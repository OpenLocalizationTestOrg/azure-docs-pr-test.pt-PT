---
title: "aaaConfigure SSL para um serviço em nuvem | Microsoft Docs"
description: "Saiba como toospecify um ponto final de HTTPS para uma função da web e como tooupload um SSL certificados toosecure a aplicação. Estes exemplos utilizam Olá portal do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>Configurar o SSL para uma aplicação no Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-configure-ssl-certificate-portal.md)
> * [Portal Clássico do Azure](cloud-services-configure-ssl-certificate.md)
>

Encriptação do Secure Socket Layer (SSL) é o método de Olá normalmente utilizada de proteger os dados enviados entre Olá internet. Esta tarefa comuns aborda como toospecify um ponto final de HTTPS para uma função da web e como tooupload um SSL certificados toosecure a aplicação.

> [!NOTE]
> procedimentos de Olá nesta tarefa aplicam-se os serviços de nuvem tooAzure; para os serviços de aplicação, consulte [isto](../app-service-web/web-sites-configure-ssl-certificate.md).
>

Esta tarefa utiliza uma implementação de produção. Informações sobre como utilizar uma implementação de teste são fornecidas no fim de Olá deste tópico.

Leitura [isto](cloud-services-how-to-create-deploy-portal.md) primeiro se ainda não tiver criado um serviço em nuvem.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Passo 1: Obter um certificado SSL
tooconfigure SSL para uma aplicação, terá primeiro tooget um certificado SSL assinado por uma autoridade de certificação (CA), uma terceiros fidedigna, que emite certificados para esta finalidade. Se já tiver uma, terá de tooobtain um de uma empresa que sells certificados SSL.

certificado Olá tem de cumprir os requisitos para certificados SSL no Azure de Olá:

* certificado de Olá tem de conter uma chave privada.
* certificado de Olá tem de ser criado para a troca de chaves, tooa exportável ficheiro Personal Information Exchange (. pfx).
* Olá nome do requerente do certificado deve corresponder ao serviço de nuvem do Olá domínio utilizado tooaccess Olá. Não é possível obter um certificado SSL a partir de uma autoridade de certificação (AC) para o domínio de cloudapp.net Olá. Tem de adquirir uma toouse de nome de domínio personalizado ao seu serviço de acesso. Quando solicitar um certificado a partir de uma AC, nome do requerente do certificado Olá tem de corresponder ao hello domínio personalizado nome utilizado tooaccess a aplicação. Por exemplo, se o nome de domínio personalizado for **contoso.com** seria pedir um certificado da AC para ***. contoso.com** ou **www.contoso.com**.
* certificado de Olá tem de utilizar um mínimo de encriptação de 2048 bits.

Para fins de teste, pode [criar](cloud-services-certs-create.md) e utilizar um certificado autoassinado. Um certificado autoassinado não é autenticado através de uma AC e pode utilizar o domínio de cloudapp.net Olá como Olá URL do site. Por exemplo, hello tarefa seguinte utiliza um certificado autoassinado que Olá nome comum (CN) utilizado no certificado Olá é **sslexample.cloudapp.net**.

Em seguida, tem de incluir informações sobre o certificado de Olá na sua definição de serviço e os ficheiros de configuração de serviço.

<a name="modify"> </a>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Passo 2: Modificar Olá de ficheiros de configuração e definição de serviço
A aplicação tem de ser configurado toouse certificado de Olá e um ponto final de HTTPS tem de ser adicionado. Como resultado, hello definição de serviço e os ficheiros de configuração de serviço necessário toobe atualizado.

1. No seu ambiente de desenvolvimento, abra o ficheiro de definição de serviço Olá (. CSDEF), adicione um **certificados** secção dentro Olá **WebRole** secção e incluir Olá seguintes informações o certificado (e certificados intermediários):

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   Olá **certificados** secção define o nome de Olá do nosso certificado, a localização e o nome de Olá do arquivo de olá onde está localizado.

   As permissões (`permisionLevel` atributo) pode ser tooone de conjunto de Olá os seguintes valores:

   | Valor de permissão | Descrição |
   | --- | --- |
   | limitedOrElevated |**(Predefinição)**  Todos os processos de função podem aceder à chave privada Olá. |
   | elevada |Apenas os processos elevados podem aceder à chave privada Olá. |

2. No seu ficheiro de definição de serviço, adicione um **InputEndpoint** elemento Olá **pontos finais** secção tooenable HTTPS:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. No seu ficheiro de definição de serviço, adicione um **enlace** elemento Olá **Sites** secção. Este elemento adiciona um toomap de enlace de HTTPS do site do ponto final tooyour:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   Todos os Olá as alterações necessárias toohello ficheiro de definição serviço foram concluídas; No entanto, ainda precisa de informações do certificado de Olá tooadd para o ficheiro de configuração do serviço de Olá.
4. No seu ficheiro de configuração serviço (CSCFG), Serviceconfiguration, adicione um **certificados** valor com que o certificado. Olá exemplo de código seguinte fornece detalhes de Olá **certificados** secção, exceto o valor do thumbprint Olá.

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(Este exemplo utiliza **sha1** para o algoritmo de thumbprint Olá. Especificar valor adequado de Olá para o algoritmo de thumbprint do certificado.)

Agora que foram atualizados Olá serviço definição e o serviço de ficheiros de configuração, a implementação do carregamento tooAzure do pacote. Se estiver a utilizar **cspack**, não utilize o **/generateConfigurationFile** sinalizador, como o que irá substituir as informações do certificado que acabou de inserir.

## <a name="step-3-upload-a-certificate"></a>Passo 3: Carregar um certificado
Ligar toohello portal do Azure e...

1. No Olá **todos os recursos** secção Olá Portal, selecione o seu serviço de nuvem.

    ![Publicar o seu serviço em nuvem](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Clique em **certificados**.

    ![Clique Olá certificados ícone](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Clique em **carregar** em Olá parte superior da área de certificados de Olá.

    ![Clique em item de menu de carregamento de Olá](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Fornecer Olá **ficheiro**, **palavra-passe**, em seguida, clique em **carregar** na parte inferior de Olá da área de entrada de dados de Olá.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Passo 4: Ligar a instância de função toohello através de HTTPS
Agora que a implementação está a funcionar no Azure, pode ligar tooit através de HTTPS.

1. Clique em Olá **URL do Site** tooopen segurança browser da web Olá.

   ![Clique em Olá URL do Site](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. No seu browser, modificar Olá ligação toouse **https** em vez de **http**e, em seguida, visitar a página Olá.

   > [!NOTE]
   > Se estiver a utilizar um certificado autoassinado, ao procurar o ponto final de HTTPS de tooan associado ao certificado autoassinado Olá vir um erro de certificado no browser Olá. Utilizar um certificado assinado por uma autoridade de certificação fidedignas elimina este problema; no Olá entretanto, pode ignorar o erro de Olá. (Outra opção é o arquivo de certificados de autoridade de certificação fidedigna tooadd Olá certificado autoassinado toohello do utilizador.)
   >
   >

   ![Pré-visualização do site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Se quiser toouse SSL para uma implementação de teste em vez de uma implementação de produção, terá primeiro de toodetermine Olá URL utilizado para Olá implementação de teste. Depois de ter sido implementado o seu serviço em nuvem, Olá URL toohello ambiente de teste é determinado pelo Olá **ID de implementação** GUID neste formato:`https://deployment-id.cloudapp.net/`  
   >
   > Criar um certificado com Olá comum nome (CN) toohello igual baseado no GUID URL (por exemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**). Utilize Olá portal tooadd Olá certificado tooyour testado serviço em nuvem. Em seguida, adicionar Olá informações tooyour CSDEF e CSCFG ficheiros de certificado, Empacote novamente esta aplicação e atualizar a sua implementação faseada toouse Olá novo pacote.
   >

## <a name="next-steps"></a>Passos seguintes
* [Configuração geral do seu serviço de nuvem](cloud-services-how-to-configure-portal.md).
* Saiba como demasiado[implementar um serviço em nuvem](cloud-services-how-to-create-deploy-portal.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).
* [Gerir o serviço de nuvem](cloud-services-how-to-manage-portal.md).
