---
title: aaaIntegrate DNS do Azure com os recursos do Azure | Microsoft Docs
description: Saiba como toouse DNS do Azure ao longo de tooprovide DNS para os seus recursos do Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Utilizar as definições de domínio personalizado de tooprovide de DNS do Azure para um serviço do Azure

O DNS do Azure fornece DNS para um domínio personalizado para qualquer um dos seus recursos do Azure que suporte de domínios personalizados ou que têm um nome de domínio completamente qualificado (FQDN). Um exemplo é tiver uma aplicação web do Azure e pretende que o seu tooaccess utilizadores-lo ao utilizar contoso.com ou www.contoso.com como um FQDN. Este artigo explica como configurar o serviço do Azure com o DNS do Azure para a utilização de domínios personalizados.

## <a name="prerequisites"></a>Pré-requisitos

Na ordem toouse DNS do Azure para o seu domínio personalizado, tem primeiro de delegar a tooAzure de domínio DNS. Visite [delegar tooAzure um domínio DNS](./dns-delegate-domain-azure-dns.md) para obter instruções sobre como tooconfigure os servidores de nome para delegação. Assim que o seu domínio for tooyour delegado zona de DNS do Azure, são registos DNS tooconfigure capaz de Olá necessários.

Pode configurar um domínio personalizado para ou [aplicações de função do Azure](#azure-function-app), [Azure IoT](#azure-iot), [endereços IP públicos](#public-ip-address), [do serviço de aplicações (aplicações Web)](#app-service-web-apps), [Armazenamento de BLOBs](#blob-storage), e [CDN do Azure](#azure-cdn).

## <a name="azure-function-app"></a>Aplicação de função do Azure

tooconfigure um domínio personalizado para aplicações de função do Azure, é criado um registo CNAME, bem como a configuração de aplicação de função Olá em si.
 
Navegue demasiado**outros** > **aplicação de função** e selecione a sua aplicação de função. Clique em **funcionalidades da plataforma** e, em **redes** clique **domínios personalizados**.

![Painel de aplicação de função](./media/dns-custom-domain/functionapp.png)

Tenha em atenção o atual url de Olá no Olá **domínios personalizados** painel, este endereço é utilizada como alias Olá para registo DNS Olá criado.

![Painel de domínio personalizado](./media/dns-custom-domain/functionshostname.png)

Navegue tooyour zona de DNS e clique em **+ conjunto de registos**. Preencha Olá seguindo as informações do Olá **adicionar conjunto de registos** painel e clique em **OK** toocreate-lo.

|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | myfunctionapp        | Este valor, juntamente com a etiqueta do nome de domínio de Olá é Olá FQDN para o nome de domínio personalizado de Olá.        |
|Tipo     | CNAME        | Utilize um registo CNAME está a utilizar um alias.        |
|VALOR DE TTL     | 1        | 1 é utilizado para 1 hora        |
|Unidade TTL     | Horas        | Horas são utilizadas como medida de tempo de Olá         |
|Alias     | adatumfunction.azurewebsites.NET        | nome DNS Olá que está a criar alias de Olá, neste exemplo é Olá adatumfunction.azurewebsites.net DNS nome fornecida pela aplicação de função toohello predefinido.        |

Navegue até a aplicação de função tooyour anterior, clique em **funcionalidades da plataforma**e, em **redes** clique **domínios personalizados**, em seguida, em **Hostnames**clique **+ adicionar hostname**.

No Olá **adicionar hostname** painel, introduza Registro CNAME Olá Olá **hostname** campo de texto e clique em **validar**. Se o registo de Olá foi toobe possam localizar, Olá **adicionar hostname** botão aparece. Clique em **adicionar hostname** alias de Olá tooadd.

![Painel de nome de anfitrião de adicionar a função aplicações](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>IoT do Azure

IoT do Azure não tem quaisquer personalizações que são necessárias no serviço de Olá próprio. é necessário toouse um domínio personalizado com um IoT Hub apenas um registo CNAME indicada toohello recursos.

Navegue demasiado**Internet das coisas** > **IoT Hub** e selecione o seu IoT hub. No Olá **descrição geral** painel, Olá nota FQDN do hub IoT de Olá.

![Painel do hub IoT](./media/dns-custom-domain/iot.png)

Em seguida, navegue até tooyour zona de DNS e clique em **+ conjunto de registos**. Preencha Olá seguindo as informações do Olá **adicionar conjunto de registos** painel e clique em **OK** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | myiothub        | Este valor, juntamente com a etiqueta do nome de domínio de Olá é Olá FQDN para o IoT hub do Olá.        |
|Tipo     | CNAME        | Utilize um registo CNAME está a utilizar um alias.
|VALOR DE TTL     | 1        | 1 é utilizado para 1 hora        |
|Unidade TTL     | Horas        | Horas são utilizadas como medida de tempo de Olá         |
|Alias     | adatumIOT.azure devices.net        | nome DNS Olá que está a criar alias de Olá, neste exemplo é Olá adatumIOT.azure devices.net anfitrião nome fornecido pelo IoT hub do Olá.

Assim que for criado o registo de Olá, testar a resolução de nomes com a utilização de registo do Olá CNAME`nslookup`

## <a name="public-ip-address"></a>Endereço IP público

tooconfigure um domínio personalizado para serviços que utilizam um IP público endereço recursos, tais como o serviço em nuvem do Gateway de aplicação, o Balanceador de carga, VMs do Gestor de recursos, e, VMs clássicas, um registo CNAME utilizado.

Navegue demasiado**redes** > **endereço IP público**, selecione o recurso de IP público Olá e clique em **configuração**. Notate endereço IP Olá mostrado.

![painel do ip público](./media/dns-custom-domain/publicip.png)

Navegue tooyour zona de DNS e clique em **+ conjunto de registos**. Preencha Olá seguindo as informações do Olá **adicionar conjunto de registos** painel e clique em **OK** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | mywebserver        | Este valor, juntamente com a etiqueta do nome de domínio de Olá é Olá FQDN para o nome de domínio personalizado de Olá.        |
|Tipo     | A        | Utilize um registo como recurso de Olá é um endereço IP.        |
|VALOR DE TTL     | 1        | 1 é utilizado para 1 hora        |
|Unidade TTL     | Horas        | Horas são utilizadas como medida de tempo de Olá         |
|Endereço IP     | <your ip address>       | endereço IP público Olá.|

![criar um registo](./media/dns-custom-domain/arecord.png)

Assim que for criado o registo de Olá A, execute `nslookup` registo de Olá toovalidate resolve.

![pesquisa de dns do ip público](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>Serviço de aplicações (aplicações Web)

Olá passos seguintes acompanham-configurar um domínio personalizado para uma aplicação de web do serviço de aplicações.

Navegue demasiado**Web & Mobile** > **do serviço de aplicações** e selecione Olá de recursos que está a configurar um nome de domínio personalizado e clique em **domínios personalizados**.

Tenha em atenção o atual url de Olá no Olá **domínios personalizados** painel, este endereço é utilizada como alias Olá para registo DNS Olá criado.

![Painel de domínios personalizados](./media/dns-custom-domain/url.png)

Navegue tooyour zona de DNS e clique em **+ conjunto de registos**. Preencha Olá seguindo as informações do Olá **adicionar conjunto de registos** painel e clique em **OK** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | mywebserver        | Este valor, juntamente com a etiqueta do nome de domínio de Olá é Olá FQDN para o nome de domínio personalizado de Olá.        |
|Tipo     | CNAME        | Utilize um registo CNAME está a utilizar um alias. Se o recurso de Olá utilizado um endereço IP, um registo seria utilizado.        |
|VALOR DE TTL     | 1        | 1 é utilizado para 1 hora        |
|Unidade TTL     | Horas        | Horas são utilizadas como medida de tempo de Olá         |
|Alias     | WebServer.azurewebsites.NET        | nome DNS Olá que está a criar alias de Olá, neste exemplo é Olá webserver.azurewebsites.net DNS nome fornecida pela aplicação de web de toohello predefinido.        |


![Crie um registo CNAME](./media/dns-custom-domain/createcnamerecord.png)

Navegue toohello anterior do serviço de aplicações que está configurado para o nome de domínio personalizado de Olá. Clique em **domínios personalizados**, em seguida, clique em **Hostnames**. registo CNAME tooadd Olá que criou, clique em **+ adicionar hostname**.

![figura 1](./media/dns-custom-domain/figure1.png)

Após a conclusão do processo de Olá, execute **nslookup** toovalidate resolução de nomes está a funcionar.

![figura 1](./media/dns-custom-domain/finalnslookup.png)

toolearn mais informações sobre o mapeamento de um domínio personalizado de tooApp serviço, visite [mapear um existente personalizado DNS nome tooAzure Web Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Se precisar de toopurchase um domínio personalizado, visite [comprar um nome de domínio personalizado para Web Apps do Azure](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn mais informações sobre domínios de serviço de aplicações.

## <a name="blob-storage"></a>Armazenamento de blobs

Olá passos seguintes acompanham-configurar um registo CNAME para uma conta do blob storage utilizando Olá asverify método. Este método garante que não há nenhum período de indisponibilidade.

Navegue demasiado**armazenamento** > **contas do Storage**, selecione a sua conta de armazenamento e, em **domínio personalizado**. Notate Olá FQDN no passo 2, este valor é utilizado toocreate Olá primeiro Registro CNAME

![domínio personalizado de armazenamento de BLOBs](./media/dns-custom-domain/blobcustomdomain.png)

Navegue tooyour zona de DNS e clique em **+ conjunto de registos**. Preencha Olá seguindo as informações do Olá **adicionar conjunto de registos** painel e clique em **OK** toocreate-lo.


|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | asverify.mystorageaccount        | Este valor, juntamente com a etiqueta do nome de domínio de Olá é Olá FQDN para o nome de domínio personalizado de Olá.        |
|Tipo     | CNAME        | Utilize um registo CNAME está a utilizar um alias.        |
|VALOR DE TTL     | 1        | 1 é utilizado para 1 hora        |
|Unidade TTL     | Horas        | Horas são utilizadas como medida de tempo de Olá         |
|Alias     | asverify.adatumfunctiona9ed.blob.Core.Windows.NET        | nome DNS Olá que está a criar alias de Olá, neste exemplo é Olá asverify.adatumfunctiona9ed.blob.core.windows.net DNS nome fornecida a conta do storage predefinida toohello.        |

Navegue até a conta de armazenamento de back-tooyour clicando **armazenamento** > **contas do Storage**, selecione a sua conta de armazenamento e clique em **domínio personalizado**. Tipo de Olá alias criado sem o prefixo de asverify Olá na caixa de texto de Olá, verificação * * Utilizar validação de CNAME indireta e clique em **guardar**. Depois de concluída este passo, devolva tooyour zona DNS e crie um registo CNAME sem o prefixo de asverify Olá.  Depois de que o ponto, é seguro toodelete Olá Registro CNAME com o prefixo de cdnverify Olá.

![domínio personalizado de armazenamento de BLOBs](./media/dns-custom-domain/indirectvalidate.png)

Validar a resolução de DNS ao executar`nslookup`

toolearn mais informações sobre o mapeamento de um domínio personalizado tooa armazenamento ponto final do blob visitam [configurar um nome de domínio personalizado para o ponto de final do Blob storage](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>CDN do Azure

Olá passos seguintes acompanham-na configurar um registo CNAME para um ponto final de CDN utilizando Olá cdnverify método. Este método garante que não há nenhum período de indisponibilidade.

Navegue demasiado**redes** > **perfis da CDN**, selecione o perfil de CDN e clique em **pontos finais** em **geral**.

Selecione o ponto final de Olá que estiver a trabalhar com e clique em **+ domínio personalizado**. Olá nota **nome de anfitrião de ponto final** como este valor é registo Olá Registro CNAME que Olá aponta para.

![Domínio personalizado de CDN](./media/dns-custom-domain/endpointcustomdomain.png)

Navegue tooyour zona de DNS e clique em **+ conjunto de registos**. Preencha Olá seguindo as informações do Olá **adicionar conjunto de registos** painel e clique em **OK** toocreate-lo.

|Propriedade  |Valor  |Descrição  |
|---------|---------|---------|
|Nome     | cdnverify.mycdnendpoint        | Este valor, juntamente com a etiqueta do nome de domínio de Olá é Olá FQDN para o nome de domínio personalizado de Olá.        |
|Tipo     | CNAME        | Utilize um registo CNAME está a utilizar um alias.        |
|VALOR DE TTL     | 1        | 1 é utilizado para 1 hora        |
|Unidade TTL     | Horas        | Horas são utilizadas como medida de tempo de Olá         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.NET        | nome DNS Olá que está a criar alias de Olá, neste exemplo é Olá cdnverify.adatumcdnendpoint.azureedge.net DNS nome fornecida a conta do storage predefinida toohello.        |

Navegue até o ponto final de CDN back tooyour clicando **redes** > **perfis da CDN**e selecione o perfil de CDN. Clique em **+ domínio personalizado** e introduza o seu alias de registo CNAME sem o prefixo de cdnverify Olá e clique em **adicionar**.

Depois de concluída este passo, devolva tooyour zona DNS e crie um registo CNAME sem o prefixo de cdnverify Olá.  Depois de que o ponto, é seguro toodelete Olá Registro CNAME com o prefixo de cdnverify Olá. Para mais informações sobre a CDN e como tooconfigure visitar um domínio personalizado sem passo de registo intermédio Olá [domínio personalizado do mapa do Azure CDN tooa conteúdo](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Passos seguintes

Saiba como demasiado[configurar inversa de DNS para serviços alojados no Azure](dns-reverse-dns-for-azure-services.md).
