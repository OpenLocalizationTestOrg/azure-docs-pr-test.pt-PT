---
title: aaaMap um DNS personalizado existente nome tooAzure Web Apps | Microsoft Docs
description: "Saiba como o nome de tooadd um domínio DNS personalizado existente (domínio intuitivos) tooa web app, back-end da aplicação móvel ou aplicação API no App Service do Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Mapear um existente personalizado DNS nome tooAzure aplicações Web

[As Aplicações Web do Azure](app-service-web-overview.md) fornecem um serviço de alojamento na Web altamente dimensionável e com correção automática. Este tutorial mostra como toomap um DNS personalizado existente nome tooAzure Web Apps.

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Mapear um subdomínio (por exemplo, `www.contoso.com`) através da utilização de um registo CNAME
> * Mapear um domínio de raiz (por exemplo, `contoso.com`) através da utilização de um registo
> * Mapear um domínio de caráter universal (por exemplo, `*.contoso.com`) através da utilização de um registo CNAME
> * Mapeamento de domínio com scripts de automatizar

Pode utilizar tanto um **registo CNAME** ou um **um registo** toomap um DNS personalizado nome tooApp serviço. 

> [!NOTE]
> Recomendamos que utilize um CNAME para todos os nomes DNS personalizados, exceto um domínio de raiz (por exemplo, `contoso.com`).

toomigrate um site em direto e o respetivo tooApp de nome de domínio DNS serviço, consulte o artigo [migrar um Active Directory tooAzure de nome DNS do serviço de aplicações](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial:

* [Criar uma aplicação do app Service](/azure/app-service/), ou utilizar uma aplicação que criou para outro tutorial.
* Adquira um nome de domínio e certifique-se de que tem registo DNS toohello de acesso para o seu fornecedor de domínio (por exemplo, a GoDaddy).

  Por exemplo, tooadd as entradas de DNS para `contoso.com` e `www.contoso.com`, tem de ser capaz de tooconfigure definições de DNS de Olá para Olá `contoso.com` domínio de raiz.

  > [!NOTE]
  > Se não tiver um domínio existente, nome, considere [aquisição de um domínio utilizando Olá portal do Azure](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Preparar a aplicação Olá

toomap um personalizado DNS nome tooa da aplicação web, aplicação web de Olá [plano do App Service](https://azure.microsoft.com/pricing/details/app-service/) tem de ser uma camada paga (**partilhados**, **básico**, **padrão**, ou  **Premium**). Neste passo, certifique-se de que Olá aplicação fica no Olá do serviço de aplicações suportadas escalão de preço.

### <a name="sign-in-tooazure"></a>Inicie sessão no tooAzure

Abra Olá [portal do Azure](https://portal.azure.com) e inicie sessão com a sua conta do Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navegue até a aplicação de toohello no Olá portal do Azure

No menu à esquerda de Olá, selecione **serviços aplicacionais**e, em seguida, selecione o nome de Olá da aplicação Olá.

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/select-app.png)

Pode ver a página de gestão de Olá de Olá aplicação do app Service.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Verifique Olá escalão de preço

No Olá deixado de navegação da página da aplicação Olá, desloque toohello **definições** secção e selecione **aumentar verticalmente (plano do App Service)**.

![Menu de dimensionamento](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

escalão atual da aplicação Olá é realçado por um limite azul. Verifique se essa aplicação Olá não está a ser Olá toomake **livres** camada. DNS personalizado não é suportado no Olá **livres** camada. 

![Verifique o escalão de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Se hello plano do App Service não está **livres**, fechar Olá **escolher o escalão de preço** página e ignorar demasiado[mapear um registo CNAME](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Aumentar verticalmente Olá plano do App Service

Selecione qualquer uma das camadas de não livre Olá (**partilhados**, **básico**, **padrão**, ou **Premium**). 

Clique em **Selecionar**.

![Verifique o escalão de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Quando vir Olá seguir notificação, a operação de dimensionamento de Olá está concluída.

![Confirmação de operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Mapear um registo CNAME

Exemplo de tutorial Olá, adicione um registo CNAME para Olá `www` subdomínio (por exemplo, `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Criar registo CNAME de Olá

Adicionar um toomap de registo CNAME hostname predefinido de um subdomínio toohello aplicação (`<app_name>.azurewebsites.net`).

Para Olá `www.contoso.com` exemplo de domínio, adicione um registo CNAME, que mapeia o nome de Olá `www` demasiado`<app_name>.azurewebsites.net`.

Depois de adicionar Olá CNAME, página de registos DNS Olá aspeto Olá seguinte exemplo:

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Ativar mapeamento de registo CNAME Olá no Azure

No Olá deixada de navegação da página da aplicação Olá num Olá portal do Azure, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

No Olá **domínios personalizados** página da aplicação Olá, adicionar Olá personalizado nome de DNS completamente qualificado (`www.contoso.com`) toohello lista.

Selecione Olá  **+**  ícone seguinte demasiado**adicionar hostname**.

![Adicione o nome de anfitrião](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Nome de domínio completamente qualificado do tipo Olá que adicionou um registo CNAME, tais como `www.contoso.com`. 

Selecione **validar**.

Olá **adicionar hostname** botão está ativado. 

Certifique-se de que **tipo de registo de nome de anfitrião** estiver definido demasiado**CNAME (www.example.com ou qualquer subdomínio)**.

Selecione **adicionar hostname**.

![Adicionar a aplicação de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Poderá demorar algum tempo para toobe Olá novo nome do anfitrião serão refletida da aplicação Olá **domínios personalizados** página. Tente atualizar Olá browser tooupdate Olá dados.

![Registo CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Se em falta um passo ou enganou algures anteriormente, verá um erro de verificação em Olá parte inferior da página Olá.

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Mapear um registo

Exemplo de tutorial Olá, adicione um registo para o domínio de raiz de Olá (por exemplo, `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Copie o endereço IP da aplicação Olá

toomap um um registo, terá de endereço IP externo da aplicação Olá. Pode encontrar este endereço IP da aplicação Olá **domínios personalizados** página Olá portal do Azure.

No Olá deixada de navegação da página da aplicação Olá num Olá portal do Azure, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

No Olá **domínios personalizados** página, copie o endereço IP da aplicação Olá.

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Criar registo Olá

toomap um um registo tooan aplicação, serviço de aplicações requer **dois** registos DNS:

- Um **A** registar o endereço IP da aplicação toohello toomap.
- A **TXT** registe o nome de anfitrião da aplicação toohello toomap predefinido `<app_name>.azurewebsites.net`. Serviço de aplicações utiliza este registo apenas no momento da configuração, tooverify que é seu domínio personalizado Olá. Depois do domínio personalizado é validado e configurado no App Service, pode eliminar este registo TXT. 

Para Olá `contoso.com` exemplo de domínio, criar registos de A e TXT de Olá toohello a tabela seguinte de acordo com (`@` normalmente representa Olá domínio de raiz). 

| Tipo de registo | Anfitrião | Valor |
| - | - | - |
| A | `@` | Endereço IP de [endereço IP da aplicação Olá cópia](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Quando são adicionados registos Olá, Olá página de registos DNS aspeto Olá seguinte exemplo:

![Página de registos DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Ativar Olá um mapeamento de registo na aplicação Olá

Novamente da aplicação Olá **domínios personalizados** página no portal do Azure de Olá, adicione Olá personalizado nome de DNS completamente qualificado (por exemplo, `contoso.com`) toohello lista.

Selecione Olá  **+**  ícone seguinte demasiado**adicionar hostname**.

![Adicione o nome de anfitrião](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Nome de domínio completamente qualificado do tipo Olá que configurou Olá um registo, tais como `contoso.com`.

Selecione **validar**.

Olá **adicionar hostname** botão está ativado. 

Certifique-se de que **tipo de registo de nome de anfitrião** estiver definido demasiado**um registo (example.com)**.

Selecione **adicionar hostname**.

![Adicionar a aplicação de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Poderá demorar algum tempo para toobe Olá novo nome do anfitrião serão refletida da aplicação Olá **domínios personalizados** página. Tente atualizar Olá browser tooupdate Olá dados.

![Um registo adicionado](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Se em falta um passo ou enganou algures anteriormente, verá um erro de verificação em Olá parte inferior da página Olá.

![Erro de verificação](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Mapear um domínio de caráter universal

Exemplo de tutorial Olá, mapear uma [nome DNS com carateres universais](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (por exemplo, `*.contoso.com`) toohello aplicação do app Service ao adicionar um registo CNAME. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Criar registo CNAME de Olá

Adicionar um toomap de registo CNAME hostname de predefinida da aplicação um caráter universal nome toohello (`<app_name>.azurewebsites.net`).

Para Olá `*.contoso.com` exemplo de domínio, Olá registo CNAME será mapear o nome de Olá `*` demasiado`<app_name>.azurewebsites.net`.

Quando é adicionado Olá CNAME, Olá página de registos DNS aspeto Olá seguinte exemplo:

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Ativar mapeamento de registo CNAME Olá na aplicação Olá

Agora pode adicionar qualquer subdomínio que corresponda à aplicação de toohello de nome de caráter universal Olá (por exemplo, `sub1.contoso.com` e `sub2.contoso.com` corresponder `*.contoso.com`). 

No Olá deixada de navegação da página da aplicação Olá num Olá portal do Azure, selecione **domínios personalizados**. 

![Menu de domínio personalizado](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Selecione Olá  **+**  ícone seguinte demasiado**adicionar hostname**.

![Adicione o nome de anfitrião](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Escreva um nome de domínio completamente qualificado que corresponde ao domínio de caráter universal Olá (por exemplo, `sub1.contoso.com`) e, em seguida, selecione **validar**.

Olá **adicionar hostname** botão está ativado. 

Certifique-se de que **tipo de registo de nome de anfitrião** estiver definido demasiado**registo CNAME (www.example.com ou qualquer subdomínio)**.

Selecione **adicionar hostname**.

![Adicionar a aplicação de toohello de nome DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Poderá demorar algum tempo para toobe Olá novo nome do anfitrião serão refletida da aplicação Olá **domínios personalizados** página. Tente atualizar Olá browser tooupdate Olá dados.

Selecione Olá  **+**  ícone novamente tooadd outro nome de anfitrião, que corresponde ao domínio de caráter universal Olá. Por exemplo, adicionar `sub2.contoso.com`.

![Registo CNAME adicionado](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>Teste no browser

Procurar toohello nomes DNS que configurou anteriormente (por exemplo, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, e `sub2.contoso.com`).

![Aplicação de tooAzure de navegação do portal](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Automatizar com scripts

Pode automatizar a gestão de domínios personalizados com scripts, utilizando Olá [CLI do Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>CLI do Azure 

Olá comando a seguir adiciona um configurado personalizado DNS nome tooan aplicação do app Service. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Para obter mais informações, consulte [mapear uma aplicação de web do domínio personalizado tooa](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Olá comando a seguir adiciona um configurado personalizado DNS nome tooan aplicação do app Service. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Para obter mais informações, consulte [atribuir uma aplicação de web do domínio personalizado tooa](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Mapear um subdomínio através da utilização de um registo CNAME
> * Mapear um domínio de raiz utilizando um registo
> * Mapear um domínio de caráter universal, utilizando um registo CNAME
> * Mapeamento de domínio com scripts de automatizar

Avançar toohello toolearn de tutorial seguinte como toobind um SSL personalizado certificado tooa web app.

> [!div class="nextstepaction"]
> [Vincular um existente personalizado SSL certificado tooAzure aplicações Web](app-service-web-tutorial-custom-ssl.md)
