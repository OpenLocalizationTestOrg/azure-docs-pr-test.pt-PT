---
title: aaaCreate um ambiente de App Service do Azure utilizando um modelo do Resource Manager
description: Explica como toocreate um ambiente externo ou o App Service do Azure ILB utilizando um modelo do Resource Manager
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Criar ASE utilizando um modelo Azure Resource Manager

## <a name="overview"></a>Descrição geral
Ambientes do App Service do Azure (ASEs) podem ser criados com um ponto final acessível através da internet ou de um ponto final de um endereço interno numa rede virtual do Azure (VNet). Quando é criado com um ponto final interno, esse ponto final é fornecida por um Azure componente chamado um balanceador de carga interno (ILB). Olá ASE num endereço IP é denominado ILB ASE. Olá ASE com um ponto final público é denominado ASE externo. 

ASE pode ser criado utilizando Olá portal do Azure ou um modelo Azure Resource Manager. Este artigo explica os passos de Olá e sintaxe terá toocreate um ASE externo ou o ILB ASE com modelos do Resource Manager. toolearn como toocreate ASE no Olá portal do Azure, consulte [tornar ASE externo] [ MakeExternalASE] ou [tornar ILB ASE][MakeILBASE].

Quando cria ASE no Olá portal do Azure, pode criar a VNet em Olá mesmo tempo ou escolha um toodeploy VNet preexistentes em. Quando cria o ASE a partir de um modelo, tem de começar com: 

* Uma VNet do Resource Manager.
* Uma sub-rede essa VNet. Recomendamos um tamanho de sub-rede ASE de `/25` com o crescimento futuro do tooaccomodate 128 endereços. Depois de criado ASE Olá, não é possível alterar o tamanho de Olá.
* ID de recurso de Olá da sua VNet. Pode obter estas informações de Olá portal do Azure com as propriedades de rede virtual.
* subscrição Olá que pretende toodeploy em.
* Olá localização toodeploy em.

tooautomate criação da ASE:

1. Crie Olá ASE a partir de um modelo. Se criar ASE externo, tiver terminado, após este passo. Se criar ILB ASE, existem alguns toodo coisas mais.

2. Depois de criar o ILB ASE, um certificado SSL que corresponda ao seu domínio ILB ASE é carregado.

3. Olá carregado certificado SSL é atribuído toohello ILB ASE como o certificado SSL "predefinida".  Este certificado é utilizado para tráfego SSL tooapps no Olá ILB ASE quando utilizarem Olá comuns domínio de raiz que está atribuído toohello ASE (por exemplo, https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Criar Olá ASE
Um modelo do Resource Manager, que cria o ficheiro de parâmetros associados e ASE está disponível [um exemplo] [ quickstartasev2create] no GitHub.

Se quiser toomake ILB ASE, utilize estes modelo do Resource Manager [exemplos][quickstartilbasecreate]. Estes aparência toothat caso de utilização. Maioria dos parâmetros Olá Olá *azuredeploy.parameters.json* ficheiro são comuns toohello criação do ILB ASEs e ASEs externo. Olá lista seguinte chama os parâmetros de nota especial ou que são exclusivos, quando criar ILB ASE:

* *interalLoadBalancingMode*: na maioria dos casos, defina este too3, o que significa que o tráfego HTTP/HTTPS em portas 80/443, e portas de canal de dados do controlo de Olá listened tooby serviço Olá FTP Olá ASE, será vinculado tooan atribuído o ILB rede virtual endereço interno. Se esta propriedade é definida too2, apenas Olá FTP relacionados com o serviço portas (canais de controlo e dados) são endereços ILB tooan vinculado. Olá tráfego HTTP/HTTPS permanece no Olá público VIP.
* *dnsSuffix*: este parâmetro define o domínio de raiz do Olá predefinido que é atribuído toohello ASE. A variação pública Olá do App Service do Azure, domínio de raiz do Olá predefinido para todas as aplicações web é *azurewebsites.net*. Uma vez ILB ASE é a rede virtual do cliente tooa interno, não certifique-domínio de raiz do sentido toouse Olá público do serviço predefinido. Em vez disso, ILB ASE deve ter um domínio de raiz predefinido que faz sentido para utilização na rede virtual interna de uma empresa. Por exemplo, Contoso Corporation poderá utilizar um domínio de raiz da predefinição de *interna contoso.com* para aplicações que estão toobe pretendido resolvível e é acessível apenas dentro da rede virtual da Contoso. 
* *ipSslAddressCount*: este parâmetro assume a predefinição automaticamente tooa o valor 0 no Olá *azuredeploy. JSON* ficheiro porque o ILB ASEs ter apenas um único endereço ILB. Não existem nenhum endereços de IP-SSL explícitos para ILB ASE. Por conseguinte, Olá conjunto de endereços IP SSL para ILB ASE tem de ser definida toozero. Caso contrário, ocorre um erro de aprovisionamento. 

Depois de Olá *azuredeploy.parameters.json* ficheiro é preenchido, crie Olá ASE utilizando o fragmento de código do PowerShell Olá. Alterar Olá caminhos toomatch Olá Resource Manager ficheiro de modelo localizações de ficheiros no seu computador. Não se esqueça toosupply os seus próprios valores para o nome da implementação do Resource Manager Olá e nome do grupo de recursos de Olá:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Demora cerca de uma hora para Olá ASE toobe criado. Em seguida, Olá ASE aparece no portal de Olá na lista de Olá de ASEs para a subscrição de Olá que acionou a implementação de Olá.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Carregar e configurar um certificado SSL Olá "predefinido"
Um certificado SSL tem de estar associado a Olá ASE como Olá "predefinido" certificado SSL utilizado tooestablish SSL ligações tooapps. Se o sufixo DNS do Olá do ASE predefinido é *interna contoso.com*, uma ligação toohttps://some-random-app.internal-contoso.com requer um certificado SSL que é válido para **.internal contoso.com* . 

Obter um certificado SSL válido ao utilizar autoridades de certificação interna, comprar um certificado de um emissor externo ou utilizar um certificado autoassinado. Independentemente da origem de Olá do certificado SSL Olá, Olá seguintes atributos do certificado deve ser feita corretamente:

* **Requerente**: este atributo deve ser definido demasiado **.your-raiz-domínio-here.com*.
* **Nome alternativo do requerente**: este atributo tem de incluir os **.your-raiz-domínio-here.com* e **.scm.your-raiz-domínio-here.com*. Toohello de ligações de SSL site SCM/Kudu associado a cada aplicação utilizar um endereço de formulário Olá *your-app-name.scm.your-root-domain-here.com*.

Com um certificado SSL válido mão, são necessários dois passos preparatórios adicionais. Converter/guardar o certificado de SSL Olá como um ficheiro. pfx. Lembre-se de que o ficheiro. pfx Olá tem de incluir todos os intermédio e certificados de raiz. Proteja-a com uma palavra-passe.

ficheiro. pfx Olá tem toobe convertido numa cadeia base64 porque o certificado SSL Olá é carregado utilizando um modelo do Resource Manager. Porque os modelos do Resource Manager são ficheiros de texto, o ficheiro. pfx Olá tem de ser convertido numa cadeia base64. Desta forma pode ser incluído como um parâmetro de modelo de Olá.

Utilize Olá fragmento de código do PowerShell para os seguintes:

* Gere um certificado autoassinado.
* Exporte o certificado de Olá como um ficheiro. pfx.
* Converta o ficheiro. pfx Olá numa cadeia com codificação base64.
* Guarde o ficheiro separado do Olá cadeia com codificação base64 tooa. 

Este código do PowerShell para codificação base64 foi adaptado de Olá [blogue de scripts do PowerShell][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Depois certificado SSL Olá é gerado com êxito e converter a cadeia de com codificação base64 tooa, utilize o modelo de Gestor de recursos de exemplo de Olá [certificado SSL do configurar Olá predefinido] [ quickstartconfiguressl] no GitHub. 

Olá parâmetros Olá *azuredeploy.parameters.json* ficheiro estão listados aqui:

* *appServiceEnvironmentName*: nome Olá Olá ASE ILB a ser configurado.
* *existingAseLocation*: cadeia de texto que contém Olá região do Azure onde hello ILB ASE foi implementada.  Por exemplo: "Sul Central EUA".
* *pfxBlobString*: Olá representação de cadeia com codificação based64 do ficheiro. pfx Olá. Utilize o fragmento de código Olá apresentado anteriormente e copie a cadeia de Olá contida em "exportedcert.pfx.b64". Cole-a no como valor Olá Olá *pfxBlobString* atributo.
* *palavra-passe*: Olá palavra-passe utilizada toosecure Olá arquivo. pfx.
* *certificateThumbprint*: Olá thumbprint do certificado. Se é possível obter este valor a partir do PowerShell (por exemplo, *$certificate. Thumbprint* de Olá fragmento de código anterior), pode utilizar valor Olá como está. Se copiar o valor de Olá de caixa de diálogo de certificado de Windows hello, lembre-se toostrip saída espaços supérfluas Olá. Olá *certificateThumbprint* deve ter um aspeto semelhante AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *certificateName*: um identificador de cadeia amigável da sua própria escolha utilizado o certificado de Olá tooidentity. nome de Olá é utilizado como parte do identificador do Gestor de recursos exclusiva Olá para Olá *Microsoft.Web/certificates* entidade que representa o certificado SSL Olá. nome de Olá *tem* terminar com Olá seguintes sufixos: \_yourASENameHere_InternalLoadBalancingASE. Olá portal do Azure utiliza este sufixo como um indicador que Olá certificado é utilizado toosecure ASE ativado o ILB.

Um exemplo de abreviado *azuredeploy.parameters.json* é mostrada aqui:

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

Depois de Olá *azuredeploy.parameters.json* ficheiro é preenchido, configure o certificado SSL Olá predefinido utilizando o fragmento de código do PowerShell Olá. Alterar toomatch de caminhos de ficheiro de olá onde os ficheiros de modelo do Resource Manager Olá estão localizados no seu computador. Não se esqueça toosupply os seus próprios valores para o nome da implementação do Resource Manager Olá e nome do grupo de recursos de Olá:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Demora cerca de 40 minutos por ASE front-end tooapply Olá de alterações. Por exemplo, para ASE tamanho predefinido que utiliza dois front-ends, o modelo de Olá demorará em torno de uma hora e 20 minutos toocomplete. Enquanto o modelo de Olá está em execução, não é possível aumentar Olá ASE.  

Após a conclusão do modelo de Olá, as aplicações em Olá ILB ASE podem ser acedidas através de HTTPS. ligações de Olá são protegidas através da utilização de certificado SSL Olá predefinido. certificado SSL Olá predefinido é utilizado quando as aplicações em Olá ILB ASE são resolvidas utilizando uma combinação do nome da aplicação Olá, nome de anfitrião do Olá predefinido. Por exemplo, https://mycustomapp.internal-contoso.com utiliza o certificado SSL Olá predefinido para **.internal contoso.com*.

No entanto, tal como as aplicações que são executados no serviço de multi-inquilino público Olá, os programadores podem configurar os nomes de anfitrião personalizado para aplicações individuais. Também pode configurar enlaces de certificado de SNI SSL exclusivos para aplicações individuais.

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicações v1 ##
Ambiente de serviço de aplicações tem duas versões: ASEv1 e ASEv2. Olá anterior a informação foi com base no ASEv2. Esta secção apresenta o Olá diferenças entre ASEv1 e ASEv2.

No ASEv1, pode gere todos os recursos de Olá manualmente. Que inclui extremidades front-Olá, funcionários e endereços IP utilizados para SSL baseado em IP. Antes de pode ampliar o plano de serviço de aplicações, tem aumentar horizontalmente o conjunto de trabalho de Olá que pretende que o toohost-lo.

ASEv1 utiliza um modelo de preços diferentes de ASEv2. ASEv1, paga para cada núcleos alocados. Isto inclui núcleos que são utilizados para front-ends ou trabalhadores que não alojam quaisquer cargas de trabalho. ASEv1, tamanho de dimensionamento máximo predefinido Olá de ASE é 55 total de anfitriões. Que inclui os trabalhadores e front-ends. Uma vantagem tooASEv1 é que pode ser implementada numa rede virtual clássica e uma rede virtual do Gestor de recursos. toolearn mais informações sobre ASEv1, consulte [introdução do ambiente de serviço de aplicações v1][ASEv1Intro].

toocreate um ASEv1 utilizando um modelo do Resource Manager, consulte [criar v1 um ILB ASE com um modelo do Resource Manager][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
