---
title: "aaaHow tooCreate um ILB ASE através do Azure modelos do Resource Manager | Microsoft Docs"
description: Saiba como toocreate um interno carregar ASE balanceador utilizando os modelos Azure Resource Manager.
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Como tooCreate um ILB ASE utilizando o Gestor de recursos modelos do Azure

> [!NOTE] 
> Este artigo é sobre Olá v1 de ambiente de serviço de aplicações. Há uma versão mais recente Olá ambiente de serviço de aplicações que é mais fácil toouse e é executada na infraestrutura mais poderosa. toolearn mais informações sobre a nova versão de Olá começar a utilizar Olá [introdução toohello ambiente de serviço de aplicações](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Descrição geral
Ambientes de serviço de aplicações podem ser criados com um endereço interno da rede virtual em vez de um VIP público.  Este endereço interno é fornecido por um componente do Azure chamado Balanceador de carga interno (ILB) do Olá.  ILB ASE podem ser criada utilizando Olá portal do Azure.  Pode também ser criado através da automatização através de modelos Azure Resource Manager.  Este artigo explica os passos de Olá e sintaxe necessárias toocreate ASE ILB com modelos Azure Resource Manager.

Existem três passos envolvidos na criação de ILB ASE a automatizar:

1. Primeiro Olá ASE de base é criado numa rede virtual com um endereço de Balanceador de carga interno em vez de um VIP público.  Como parte deste passo, um nome de domínio de raiz é atribuído toohello ILB ASE.
2. Uma vez Olá que ASE do ILB for criado, um certificado SSL é carregado.  
3. Olá carregado certificado SSL é explicitamente atribuído toohello ILB ASE como o certificado SSL "predefinida".  Este certificado SSL será utilizado para tráfego SSL tooapps no Olá ILB ASE quando Olá aplicações são resolvidas utilizando Olá comuns raiz domínio atribuído toohello ASE (por exemplo, https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Criar Olá Base ILB ASE
Um modelo do Azure Resource Manager de exemplo e o respetivo ficheiro de parâmetros associados, estão disponíveis no GitHub [aqui][quickstartilbasecreate].

Maioria dos parâmetros Olá Olá *azuredeploy.parameters.json* ficheiro é comuns toocreating ASEs ambas ILB, bem como ASEs vinculado tooa público VIP.  lista de Olá abaixo chama os parâmetros de nota especial ou que são exclusivos, quando criar ILB ASE:

* *interalLoadBalancingMode*: na maioria dos casos, defina este too3, o que significa que o tráfego HTTP/HTTPS em portas 80/443, e portas de canal de dados do controlo de Olá listened tooby serviço Olá FTP Olá ASE, será vinculado tooan ILB atribuído a rede virtual endereço interno.  Se esta propriedade está definida em vez disso, too2, em seguida, Olá apenas o serviço FTP relacionadas com portas (canais de controlo e dados) serão vinculadas endereços tooan ILB, enquanto permanecem no VIP público Olá Olá tráfego HTTP/HTTPS.
* *dnsSuffix*: este parâmetro define o domínio de raiz do Olá predefinido que será atribuído toohello ASE.  A variação pública Olá do App Service do Azure, domínio de raiz do Olá predefinido para todas as aplicações web é *azurewebsites.net*.  No entanto, uma vez que ILB ASE rede virtual do cliente tooa interno, não se domínio de raiz do sentido toouse Olá público do serviço predefinido.  Em vez disso, ILB ASE deve ter um domínio de raiz predefinido que faz sentido para utilização na rede virtual interna de uma empresa.  Por exemplo, um Contoso Corporation hipotético poderá utilizar um domínio de raiz da predefinição de *interna contoso.com* para aplicações que são tooonly pretendido de ser resolvível e é acessível na rede virtual da Contoso. 
* *ipSslAddressCount*: este parâmetro é automaticamente predefinidas tooa o valor 0 no Olá *azuredeploy. JSON* ficheiro porque o ILB ASEs ter apenas um único endereço ILB.  Existem sem endereços de IP-SSL explícitos para ILB ASE, e, por conseguinte, Olá conjunto de endereços IP SSL para ILB ASE deve ser definido toozero, caso contrário, ocorrerá um erro de aprovisionamento. 

Uma vez Olá *azuredeploy.parameters.json* ficheiro tiver sido preenchido para ASE ILB, Olá ASE do ILB, em seguida, podem ser criada utilizando Olá seguinte fragmento de código do Powershell.  Altere toomatch de caminhos de ficheiro de olá onde os ficheiros de modelo do Azure Resource Manager Olá estão localizados no seu computador.  Lembre-se também toosupply os seus próprios valores para o nome da implementação Olá do Azure Resource Manager e o nome do grupo de recursos.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Depois de Olá do Azure Resource Manager modelo é submetido irá demorar algumas horas para Olá ILB ASE toobe criado.  Depois de concluída a criação de Olá, Olá ILB ASE irá aparecer no portal de Olá UX na lista de Olá de ambientes do App Service para a subscrição de Olá que acionou a implementação de Olá.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Carregar e configurar Olá "Predefinido" certificado de SSL
Uma vez Olá que ILB ASE é criado, um certificado SSL deve ser associado com ASE Olá como Olá "predefinido" utilização de certificado SSL para estabelecer tooapps de ligações de SSL.  Continuar com o exemplo de Contoso Corporation hipotético Olá, se Olá do ASE predefinido DNS sufixo é *interna contoso.com*, em seguida, uma ligação demasiado*https://some-random-app.internal-contoso.com*requer um certificado SSL que é válido para **.internal contoso.com*. 

Existem várias formas tooobtain um certificado SSL válido, incluindo ACs internas, comprar um certificado de um emissor externo e a utilizar um certificado autoassinado.  Independentemente da origem de Olá do certificado SSL Olá, hello seguintes atributos de certificado necessário toobe corretamente configurada:

* *Requerente*: este atributo deve ser definido demasiado **.your-raiz-domínio-here.com*
* *Nome alternativo do requerente*: este atributo tem de incluir os **.your-raiz-domínio-here.com*, e **.scm.your-raiz-domínio-here.com*.  Olá razão para a entrada segundo Olá é essa toohello de ligações de SSL site SCM/Kudu associado a cada aplicação será efetuada utilizando um endereço de formulário Olá *your-app-name.scm.your-root-domain-here.com*.

Com um certificado SSL válido mão, são necessários dois passos preparatórios adicionais.  tem de certificado SSL de Olá toobe convertido/guardada como um ficheiro. pfx.  Lembre-se de que o ficheiro. pfx Olá precisa tooinclude todos os intermédio e certificados de raiz e tem também de toobe protegido com uma palavra-passe.

Em seguida, Olá resultantes. pfx tem toobe convertido numa cadeia base64 porque o certificado SSL Olá será carregado através de um modelo Azure Resource Manager.  Uma vez que modelos Azure Resource Manager são ficheiros de texto, o ficheiro. pfx Olá tem toobe convertido numa cadeia base64, pelo que pode ser incluído como um parâmetro de modelo de Olá.

Olá Powershell o fragmento de código abaixo mostra um exemplo de gerar um certificado autoassinado, exportar certificado Olá como um ficheiro. pfx, ao converter o ficheiro. pfx Olá num base64 cadeia codificada e, em seguida, guarde Olá base64 codificado ficheiro separado de tooa de cadeia.  Olá código do Powershell para codificação base64 foi adaptada de Olá [blogue de Scripts do Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Depois do certificado SSL Olá foi gerado com êxito e tooa convertida base64 cadeia codificada, Olá modelo Azure Resource Manager de exemplo no GitHub para [configurar o certificado SSL Olá predefinido] [ configuringDefaultSSLCertificate] pode ser utilizado.

Olá parâmetros Olá *azuredeploy.parameters.json* ficheiro estão listados abaixo:

* *appServiceEnvironmentName*: nome Olá Olá ASE ILB a ser configurado.
* *existingAseLocation*: cadeia de texto que contém Olá região do Azure onde hello ILB ASE foi implementada.  Por exemplo: "Sul Central EUA".
* *pfxBlobString*: Olá based64 codificado representação de cadeia de ficheiro. pfx Olá.  A utilizar o fragmento de código Olá apresentado anteriormente, seria copie a cadeia de Olá contida em "exportedcert.pfx.b64" e cole-a no como valor Olá Olá *pfxBlobString* atributo.
* *palavra-passe*: Olá palavra-passe utilizada toosecure Olá arquivo. pfx.
* *certificateThumbprint*: Olá thumbprint do certificado.  Se é possível obter este valor a partir do Powershell (por exemplo, *$certificate. Thumbprint* de Olá fragmento de código anterior), pode utilizar o valor de Olá como-é.  No entanto se copiar o valor de Olá caixa de diálogo de certificado do Windows hello, lembre-se toostrip saída espaços supérfluas Olá.  Olá *certificateThumbprint* deve ter um aspeto semelhante: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: um identificador de cadeia amigável da sua própria escolha utilizado o certificado de Olá tooidentity.  nome de Olá é utilizado como parte do identificador de Azure Resource Manager exclusivo Olá para Olá *Microsoft.Web/certificates* entidade que representa o certificado SSL Olá.  nome de Olá **tem** terminar com Olá seguintes sufixos: \_yourASENameHere_InternalLoadBalancingASE.  Este sufixo é utilizado pelo portal Olá como um indicador que Olá certificado é utilizado para proteger ASE ativado o ILB.

Um exemplo de abreviado *azuredeploy.parameters.json* é mostrado abaixo:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Uma vez Olá *azuredeploy.parameters.json* ficheiro tiver sido preenchido, certificado SSL Olá predefinido pode ser configurado com Olá seguinte fragmento de código do Powershell.  Altere toomatch de caminhos de ficheiro de olá onde os ficheiros de modelo do Azure Resource Manager Olá estão localizados no seu computador.  Lembre-se também toosupply os seus próprios valores para o nome da implementação Olá do Azure Resource Manager e o nome do grupo de recursos.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Depois de Olá do Azure Resource Manager modelo é submetido demorará aproximadamente minutos forty minutos por alteração de Olá ASE tooapply front-end.  Por exemplo, com uma predefinição ASE tamanho utilizando dois frente-ends, modelo Olá irá demorar uma hora e twenty toocomplete de minutos.  Enquanto está a executar o modelo de Olá Olá ASE não será capaz de tooscaled.  

Após a conclusão do modelo de Olá, as aplicações em Olá ILB ASE podem ser acedidas através de HTTPS e ligações Olá irão ser protegidas utilizando o certificado SSL Olá predefinido.  certificado SSL Olá predefinida será utilizado quando as aplicações em Olá ILB ASE são resolvidas utilizando uma combinação do nome da aplicação Olá, o nome de anfitrião do Olá predefinido.  Por exemplo *https://mycustomapp.internal-contoso.com* utilizaria o certificado SSL Olá predefinido para **.internal contoso.com*.

No entanto, tal como aplicações em execução no serviço de multi-inquilino público Olá, os programadores podem também configurar os nomes de anfitrião personalizado para aplicações individuais e, em seguida, configure os enlaces de certificado de SNI SSL exclusivos para aplicações individuais.  

## <a name="getting-started"></a>Introdução
tooget começar a utilizar ambientes do App Service, consulte [introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

Todos os artigos e como-a para ambientes de serviço de aplicações estão disponíveis no Olá [Leia-me para ambientes de serviço de aplicações](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

