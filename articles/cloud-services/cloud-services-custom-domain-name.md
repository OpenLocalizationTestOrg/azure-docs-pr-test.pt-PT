---
title: "aaaConfigure um nome de domínio personalizado nos serviços em nuvem | Microsoft Docs"
description: "Saiba como tooexpose a aplicação do Azure ou dados de um domínio personalizado ao configurar as definições de DNS."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Configurar um nome de domínio personalizado para um serviço em nuvem do Azure
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-custom-domain-name-portal.md)
> * [Portal Clássico do Azure](cloud-services-custom-domain-name.md)
> 
> 

Quando cria um serviço em nuvem, o Azure atribui-subdomínio tooa cloudapp.net. Por exemplo, se o seu serviço em nuvem com o nome "contoso", os utilizadores irão ser capaz de tooaccess a aplicação num URL como http://contoso.cloudapp.net. Azure também atribui um endereço IP virtual.

No entanto, também pode expor a aplicação no seu próprio nome de domínio, tal como contoso.com. Este artigo explica como tooreserve ou configurar um nome de domínio personalizado para funções da web de serviço em nuvem.

Já compreender quais são CNAME e registos? [Ir passado Olá explicação](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> Obter vai mais rapidamente! Olá de utilização do Azure [orientado instruções](http://support.microsoft.com/kb/2990804). Faz a associação de um nome de domínio personalizado e proteger a comunicação (SSL) com Cloud Services do Azure ou Web sites do Azure com um snap.
> 
> 

<p/>

> [!NOTE]
> procedimentos de Olá nesta tarefa aplicam-se os serviços de Cloud tooAzure. Para os serviços de aplicação, consulte [isto](../app-service-web/web-sites-custom-domain-name.md). Para contas do storage, consulte [isto](../storage/blobs/storage-custom-domain-name.md).
> 
> 

## <a name="understand-cname-and-a-records"></a>Compreender os registos CNAME e A
CNAME (ou os registos de alias) e registos ambos permitem-lhe tooassociate um nome de domínio com um servidor específico (ou serviço neste caso,) no entanto, funcionam de forma diferente. Também existem algumas considerações específicas ao utilizar registos com os serviços de nuvem do Azure que deve considerar antes de decidir qual toouse.

### <a name="cname-or-alias-record"></a>Registo CNAME ou Alias
Um registo CNAME mapeia um *específico* domínio, como **contoso.com** ou **www.contoso.com**, nome de domínio canónico tooa. Neste caso, o nome de domínio canónico Olá é Olá **[myapp] .cloudapp .net** nome de domínio do seu Azure alojada a aplicação. Depois de criado, Olá CNAME cria um alias para Olá **[myapp] .cloudapp .net**. Olá entrada CNAME irá resolver o endereço IP toohello do seu **[myapp] .cloudapp .net** service automaticamente, se alterar o endereço IP Olá do serviço de nuvem Olá, não terá tootake qualquer ação.

> [!NOTE]
> Alguns registrars de domínio apenas lhe permitam toomap subdomínios quando utilizar um registo CNAME, como www.contoso.com e não os nomes de raiz, tal como contoso.com. Para obter mais informações sobre registos CNAME, consulte a documentação de Olá fornecida pela sua entidade de registo, [Olá Wikipedia entrada no registo CNAME](http://en.wikipedia.org/wiki/CNAME_record), ou Olá [IETF os nomes de domínio - implementação e a especificação de](http://tools.ietf.org/html/rfc1035) documento.
> 
> 

### <a name="a-record"></a>Um registo
Um registo mapeia um domínio, tal como **contoso.com** ou **www.contoso.com**, *ou de um domínio de caráter universal* como  **\*. contoso.com**, tooan endereço IP. No caso de Olá de um serviço em nuvem do Azure, Olá IP virtual do serviço de Olá. Por isso vantagem principal de Olá de um registo através de um registo CNAME é que pode fazer com que uma entrada que utiliza um caráter universal, tais como \* **. contoso.com**, que seria processar pedidos de subdomínios vários como  **Mail.contoso.com**, **login.contoso.com**, ou **www.contso.com**.

> [!NOTE]
> Uma vez que está mapeado um registo tooa o endereço IP estático, não é possível resolver automaticamente alterações toohello endereço IP do seu serviço de nuvem. Olá atribuir endereço IP utilizado pelo seu serviço em nuvem é Olá pela primeira vez que implementar tooan ranhura vazia (produção ou transição.) Se eliminar a implementação de Olá para a ranhura de Olá, endereço IP de Olá é libertado pelo Azure e qualquer bloco de toohello implementações futuras pode ser atribuído um novo endereço IP.
> 
> Comodamente, endereço IP Olá de uma ranhura de implementação fornecido (produção ou transição) é mantido ao trocar entre testes e implementações de produção ou efetuar uma atualização direta de uma implementação existente. Para obter mais informações sobre estas ações a efetuar, consulte [como serviços em nuvem toomanage](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Adicionar um registo CNAME para o domínio personalizado
toocreate um registo CNAME, tem de adicionar uma nova entrada na tabela DNS Olá para o seu domínio personalizado utilizando ferramentas de Olá fornecidas pelo sua entidade de registo. Cada entidade de registo tem um método semelhante, mas ligeiramente diferente de especificação de um registo CNAME, mas Olá conceitos Olá mesmo.

1. Utilize um dos Olá de toofind métodos **. cloudapp.net** atribuído tooyour o serviço em nuvem do nome de domínio.
   
   * Início de sessão toohello [portal clássico do Azure], selecione o seu serviço em nuvem, selecione **Dashboard**e, em seguida, determinar Olá **URL do Site** entrada no Olá **leitura rápida**  secção.
     
       ![secção de leitura rápida, que mostra o URL do site Olá][csurl]
     
       **OU**  
   * Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, utilize Olá seguinte comando:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Guarde o nome de domínio de Olá utilizado no URL Olá devolvido por qualquer um dos métodos, como precisará ao criar um registo CNAME.
2. Inicie sessão no Web site de tooyour DNS da entidade de registo e aceda toohello página para gerir o DNS. Procure ligações ou áreas do site de Olá identificados como **nome de domínio**, **DNS**, ou **nome do servidor de gestão**.
3. Localize agora onde pode selecionar ou introduzir do CNAME. Pode ter o registo de Olá tooselect tipo de uma lista pendente, ou vá tooan avançadas a página de definições. Deve procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.
4. Tem também de fornecer domínio Olá ou subdomínio alias para Olá CNAME, tais como **www** se quiser toocreate um alias para **www.customdomain.com**. Se quiser toocreate um alias para o domínio de raiz de Olá, podem ser apresentado como Olá '**@**' símbolo nas ferramentas DNS da sua entidade de registo.
5. Em seguida, tem de fornecer um nome de anfitrião canónico, que é a sua aplicação **cloudapp.net** domínio neste caso.

Por exemplo, Olá seguir registo CNAME reencaminha todo o tráfego de **www.contoso.com** demasiado**contoso.cloudapp.net**, nome de domínio personalizado de Olá da sua aplicação implementada:

| Nome de alias/anfitrião/subdomínio | Domínio canónico |
| --- | --- |
| www |contoso.cloudapp.NET |

Visitantes de **www.contoso.com** nunca irá ver o anfitrião de verdadeiro Olá (contoso.cloudapp.net) pelo processo de reencaminhamento de Olá é toothe invisível final utilizador.

> [!NOTE]
> Olá exemplo acima só se aplica tootraffic em Olá **www** subdomínio. Uma vez que não é possível utilizar carateres universais com registos CNAME, tem de criar um CNAME para cada domínio/subdomínio. Se pretender que o tráfego de toodirect de subdomínios, tais como \*. contoso.com, tooyour cloudapp.net endereço, pode configurar um **URL de redirecionamento** ou **URL reencaminhar** entrada nas suas definições de DNS, ou Crie um registo.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Adicionar um registo a para o domínio personalizado
toocreate um um registo, tem primeiro de encontrar Olá um endereço IP virtual do seu serviço de nuvem. Em seguida, adicione uma nova entrada na tabela DNS Olá para o seu domínio personalizado utilizando ferramentas de Olá fornecidas pelo sua entidade de registo. Cada entidade de registo tem um método semelhante, mas ligeiramente diferente de especificação de um registo, mas Olá conceitos Olá mesmo.

1. Utilize um dos Olá seguinte endereço IP do métodos tooget Olá do seu serviço de nuvem.
   
   * início de sessão toohello [portal clássico do Azure], selecione o seu serviço em nuvem, selecione **Dashboard**e, em seguida, determinar Olá **endereço IP Virtual público (VIP)** entrada no Olá **leitura rápida** secção.
     
       ![secção de leitura rápida Mostrar Olá VIP][vip]
     
       **OU**  
   * Instalar e configurar [Azure Powershell](/powershell/azure/overview), e, em seguida, utilize Olá seguinte comando:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Se tiver vários pontos finais associados com o serviço de nuvem, receberá várias linhas que contém o endereço IP Olá, mas todas as devem apresentar Olá mesmo endereço.
     
     Guarde o endereço IP Olá, pois irá precisar ao criar um registo.
2. Inicie sessão no Web site de tooyour DNS da entidade de registo e aceda toohello página para gerir o DNS. Procure ligações ou áreas do site de Olá identificados como **nome de domínio**, **DNS**, ou **nome do servidor de gestão**.
3. Localize agora onde pode selecionar ou introduzir um registo. Pode ter o registo de Olá tooselect tipo de uma lista pendente, ou vá tooan avançadas a página de definições.
4. Selecione ou introduza o domínio de Olá ou subdomínio que irá utilizar este registo. Por exemplo, seleccione **www** se quiser toocreate um alias para **www.customdomain.com**. Se pretender toocreate uma entrada de caráter universal para todos os subdomínios, introduza '__*__'. Este irá cobrir todos os subdomínios como **mail.customdomain.com**, **login.customdomain.com**, e **www.customdomain.com**.
   
    Se quiser toocreate um um registo para o domínio de raiz de Olá, podem ser apresentado como Olá '**@**' símbolo nas ferramentas DNS da sua entidade de registo.
5. Introduza o endereço IP de Olá do seu serviço em nuvem no Olá fornecido campo. Isto associa a entrada de domínio de Olá utilizada no Olá um registo com o endereço IP Olá da sua implementação do serviço de nuvem.

Por exemplo, Olá seguir um registo reencaminha todo o tráfego de **contoso.com** demasiado**137.135.70.239**, Olá endereço IP da sua aplicação implementada:

| Nome do anfitrião/subdomínio | Endereço IP |
| --- | --- |
| @ |137.135.70.239 |

O exemplo mostra como criar um registo para o domínio de raiz de Olá. Se desejar toocreate um toocover de entrada universal todos os subdomínios, introduziria '__*__' como subdomínio Olá.

> [!WARNING]
> Endereços IP no Azure são dinâmicos por predefinição. Provavelmente pretenderá toouse um [reservado de endereços IP](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure não alterar o seu endereço IP.
> 
> 

## <a name="next-steps"></a>Passos seguintes
* [Como tooManage Cloud Services](cloud-services-how-to-manage.md)
* [Como tooMap conteúdo do CDN tooa domínio personalizado](../cdn/cdn-map-content-to-custom-domain.md)
* [Configuração geral do seu serviço de nuvem](cloud-services-how-to-configure.md).
* Saiba como demasiado[implementar um serviço em nuvem](cloud-services-how-to-create-deploy.md).
* Configurar [certificados ssl](cloud-services-configure-ssl-certificate.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[portal clássico do Azure]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
