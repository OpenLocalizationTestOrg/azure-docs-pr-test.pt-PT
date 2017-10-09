---
title: "domínio personalizado de tooa conteúdo do CDN do Azure de aaaMap | Microsoft Docs"
description: "Saiba como o domínio personalizado tooa de conteúdo de toomap CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Domínio personalizado de tooa conteúdo do CDN do Azure de mapa
Pode mapear um domínio personalizado tooa CDN no ponto final em ordem toouse seu próprio nome de domínio no URLs toocached conteúdo em vez de utilizar um subdomínio azureedge.net.

Existem duas formas toomap domínio personalizado tooa ponto final de CDN:

1. [Criar um registo CNAME com o registo de domínios e mapear personalizado domínios e subdomínios toohello ponto final de CDN](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Um registo CNAME é uma funcionalidade DNS que mapeia um domínio de origem, como `www.contosocdn.com` ou `cdn.contoso.com`, tooa domínio de destino. Neste caso, o domínio de origem Olá é o domínio personalizado e o subdomínio (um subdomínio, como **www** ou **cdn** é sempre necessário). domínio de destino Olá é o ponto final de CDN.  
   
    processo de Olá de mapeamento de domínio personalizado tooyour ponto final de CDN, no entanto, resultem num breve período de tempo de inatividade para o domínio de Olá enquanto está a registar o domínio de Olá Olá Portal do Azure.
2. [Adicionar um passo de registo intermédio **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Se o domínio personalizado é atualmente suportar uma aplicação com um contrato de nível de serviço (SLA) que requer que não existe nenhum período de indisponibilidade de ser, em seguida, pode utilizar Olá Azure **cdnverify** subdomínio tooprovide um registo intermédio passo para que os utilizadores serão capazes tooaccess o domínio ao hello ocorra de mapeamento de DNS.  

Depois de registar o domínio personalizado utilizando um dos Olá acima procedimentos, deverá demasiado[Certifique-se de que o ponto final de CDN faz referência a esse subdomínio personalizado de Olá](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> Tem de criar um registo CNAME com o toomap de entidade de registo do domínio domínio toohello ponto final de CDN. Registos CNAME mapeiam subdomínios específicos, tais como `www.contoso.com` ou `cdn.contoso.com`. Não é possível toomap um domínio de raiz de tooa registos CNAME, tais como `contoso.com`.
> 
> Um subdomínio só pode ser associado a um ponto final da CDN. Olá registo CNAME que criar irá encaminhar todo o tráfego endereçado toohello subdomínio toohello especificado ponto final.  Por exemplo, se associar `www.contoso.com` com o ponto final de CDN, em seguida, não pode associá-la a outros pontos finais do Azure, tal como um ponto final de conta de armazenamento ou um ponto final de serviço de nuvem. No entanto, pode utilizar diferentes subdomínios de Olá mesmo domínio para pontos finais de serviço diferente. Também pode mapear os subdomínios diferentes toohello mesmo ponto final da CDN.
> 
> Para **CDN do Azure da Verizon** pontos finais (Standard e Premium), tenha em atenção que este ocupa demasiado**90 minutos** para nós de limite de tooCDN toopropagate de alterações de domínio personalizado.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Registar um domínio personalizado para um ponto final de CDN do Azure
1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).
2. Clique em **procurar**, em seguida, **perfis da CDN**, Olá, em seguida, o perfil de CDN com o ponto final de Olá pretende que o domínio personalizado de tooa toomap.  
3. No Olá **perfil da CDN** painel, clique em ponto final de CDN Olá com a qual pretende que o subdomínio de Olá tooassociate.
4. Olá parte superior do painel de ponto final de Olá, clique em Olá **Adicionar domínio personalizado** botão.  No Olá **adicionar um domínio personalizado** painel, irá ver o nome de anfitrião de ponto final de Olá, derivado do ponto final de CDN, toouse na criação de um registo CNAME novo. formato de Olá do endereço de nome de anfitrião Olá aparecerão como  **&lt;EndpointName >. azureedge.net**.  Pode copiar este toouse de nome de anfitrião na criação de registro CNAME Olá.  
5. Navegue de web site do tooyour de domínios e localize a secção de Olá para criar registos DNS. Poderá encontrar isto numa secção como **Nome de Domínio**, **DNS** ou **Gestão de Nome de Servidor**.
6. Localize a secção de Olá para a gestão de CNAMEs. Pode ter a página de definições avançadas de tooan toogo e procurar palavras Olá CNAME, Alias ou subdomínios.
7. Criar um novo registo CNAME, que mapeia o subdomínio escolhido (por exemplo, **www** ou **cdn**) nome de anfitrião de toohello fornecido no Olá **adicionar um domínio personalizado** painel. 
8. Devolver toohello **adicionar um domínio personalizado** painel e introduza o seu domínio personalizado, incluindo o subdomínio Olá, na caixa de diálogo Olá. Por exemplo, introduza o nome de domínio Olá no formato de Olá `www.contoso.com` ou `cdn.contoso.com`.   
   
   Azure irá verificar se o registo CNAME Olá existe Olá nome de domínio que introduziu. Se Olá CNAME estiver correto, o domínio personalizado é validado.  Para **CDN do Azure da Verizon** pontos finais (Standard e Premium), poderá demorar até too90 minutos para domínio personalizado definições toopropagate tooall CDN edge nós, no entanto.  
   
   Tenha em atenção que, em alguns casos, pode demorar tempo para Olá CNAME toopropagate registos tooname servidores no Olá Internet. Se o domínio não é validado imediatamente e considerar Olá registo CNAME está correto, em seguida, aguarde alguns minutos e tente novamente.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Registar um domínio personalizado para um ponto final de CDN do Azure utilizando o subdomínio de cdnverify intermediário Olá
1. Iniciar sessão Olá [Portal do Azure](https://portal.azure.com/).
2. Clique em **procurar**, em seguida, **perfis da CDN**, Olá, em seguida, o perfil de CDN com o ponto final de Olá pretende que o domínio personalizado de tooa toomap.  
3. No Olá **perfil da CDN** painel, clique em ponto final de CDN Olá com a qual pretende que o subdomínio de Olá tooassociate.
4. Olá parte superior do painel de ponto final de Olá, clique em Olá **Adicionar domínio personalizado** botão.  No Olá **adicionar um domínio personalizado** painel, irá ver o nome de anfitrião de ponto final de Olá, derivado do ponto final de CDN, toouse na criação de um registo CNAME novo. formato de Olá do endereço de nome de anfitrião Olá aparecerão como  **&lt;EndpointName >. azureedge.net**.  Pode copiar este toouse de nome de anfitrião na criação de registro CNAME Olá.
5. Navegue de web site do tooyour de domínios e localize a secção de Olá para criar registos DNS. Poderá encontrar isto numa secção como **Nome de Domínio**, **DNS** ou **Gestão de Nome de Servidor**.
6. Localize a secção de Olá para a gestão de CNAMEs. Pode ter a página de definições avançadas de tooan toogo e procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.
7. Criar um novo registo CNAME e fornecer um alias de subdomínio, que inclui Olá **cdnverify** subdomínio. Por exemplo, subdomínio Olá que especificar estará no formato de Olá **cdnverify.www** ou **cdnverify.cdn**. Em seguida, forneça o nome de anfitrião de Olá, que é o ponto final de CDN, no formato de Olá **cdnverify.&lt; EndpointName >. azureedge.net**. O mapeamento de DNS deve ter o seguinte aspeto:`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Devolver toohello **adicionar um domínio personalizado** painel e introduza o seu domínio personalizado, incluindo o subdomínio Olá, na caixa de diálogo Olá. Por exemplo, introduza o nome de domínio Olá no formato de Olá `www.contoso.com` ou `cdn.contoso.com`. Tenha em atenção que neste passo, não precisa de subdomínio de Olá toopreface com **cdnverify**.  
   
    Azure irá verificar se o registo CNAME Olá existe Olá cdnverify nome de domínio que introduziu.
9. Neste momento, o domínio personalizado foi verificado pelo Azure, mas o domínio de tooyour tráfego não ainda se encontra ponto final de CDN tooyour encaminhadas. Após uma espera suficientemente longa toopropagate de definições de domínio personalizado de Olá tooallow toohello CDN contorno nós (90 minutos para **CDN do Azure da Verizon**, 1-2 minutos para **CDN do Azure da Akamai**), devolver tooyour DNS web site da entidade de registo e crie outro registo CNAME, que mapeia o subdomínio tooyour ponto final de CDN. Por exemplo, especifique subdomínio Olá como **www** ou **cdn**, e Olá hostname como  **&lt;EndpointName >. azureedge.net**. Neste passo, o registo de Olá do seu domínio personalizado está concluído.
10. Por fim, pode eliminar Olá Registro CNAME que criou com **cdnverify**, tal como estava necessária apenas como um passo intermediário.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Certifique-se de que subdomínio personalizado de Olá referencia o ponto final de CDN
* Depois de concluir o registo de Olá do seu domínio personalizado, pode aceder a conteúdo que é colocado em cache no ponto final de CDN com o domínio personalizado Olá.
  Em primeiro lugar, certifique-se de que tem conteúdo público, que é colocado em cache ponto final de Olá. Por exemplo, se o ponto final de CDN está associado uma conta de armazenamento, Olá CDN coloca em cache conteúdo nos contentores do blob público. domínio personalizado do Olá tootest, certifique-se de que o seu contentor é definido tooallow acesso de público e que este contém pelo menos um blob.
* No seu browser, navegue toohello endereço de blob Olá utilização Olá de domínio personalizado. Por exemplo, se o domínio personalizado é `cdn.contoso.com`, blob em cache do Olá URL tooa será semelhante toohello seguinte URL: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Veja Também
[Como tooEnable Olá rede de entrega de conteúdos (CDN) do Azure](cdn-create-new-endpoint.md)  

