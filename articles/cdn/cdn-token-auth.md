---
title: "recursos do Azure CDN aaaSecuring com autenticação de token | Microsoft Docs"
description: "A utilizar a autenticação de token toosecure acesso aos tooyour CDN do Azure recursos."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Proteger recursos da CDN do Azure com a autenticação de token

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Descrição geral

Autenticação de token é um mecanismo que lhe permite tooprevent CDN do Azure de que os clientes de toounauthorized serve ativos.  Isto é feito normalmente tooprevent "hotlinking" do conteúdo, em que um Web site diferente, muitas vezes, uma placa de mensagem, utilize os recursos sem permissão.  Isto pode ter um impacto nos custos de entrega de conteúdos. Ao ativar esta funcionalidade na CDN, os pedidos serão autenticados pelo limite CDN POPs antes de entregar o conteúdo de Olá. 

## <a name="how-it-works"></a>Como funciona

Autenticação de token verifica pedidos são gerados por um site fidedigno, exigindo que os pedidos toocontain um valor de token que contém codificadas informações sobre o autor do pedido Olá. Conteúdo será apenas servido toorequester quando Olá codificado requisitos de Olá às informações, caso contrário pedidos serão rejeitados. Pode configurar o requisito de Olá utilizando um ou vários parâmetros abaixo.

- País: permitir ou negar pedidos que teve origem países especificados.  [Lista de indicativos de país válido.](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL: permitir apenas toorequest asset ou o caminho especificado.  
- Anfitrião: permitir ou negar pedidos utilizando anfitriões especificados no cabeçalho de pedido de Olá.
- Referência: permitir ou negar toorequest de referência especificado.
- Endereço IP: permitir apenas pedidos que teve origem do endereço IP específico ou a sub-rede IP.
- Permitir o protocolo: ou pedidos de blocos com base no protocolo Olá utilizado conteúdo de Olá toorequest.
- Hora de expiração: atribuir uma data e hora tooensure período que uma ligação apenas permanece válida durante um período de tempo limitado.

Consulte o exemplo de configuração detalhadas de cada um dos parâmetros.

## <a name="reference-architecture"></a>Arquitetura de referência

Veja a seguir uma arquitetura de referência de configuração de autenticação com token na CDN toowork com a sua aplicação Web.

![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Lógica de validação de token no ponto final de CDN
    
Este gráfico descreve a forma como o CDN do Azure valida pedido de cliente quando a autenticação de token está configurada no ponto final de CDN.

![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Ao configurar a autenticação de token

1. De Olá [portal do Azure](https://portal.azure.com), procure o perfil da CDN tooyour e, em seguida, clique em Olá **gerir** portal suplementar do botão toolaunch Olá.

    ![Botão de gerir do painel do perfil da CDN](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Coloque o cursor sobre **HTTP grande**e, em seguida, clique em **Token Auth** no Olá flyout. Irá configurar parâmetros de encriptação neste separador e chave de encriptação.

    1. Introduza uma chave de encriptação exclusivo para **chave primária**.  Introduza outra para **chave de cópia de segurança**

        ![Chave de configuração de autenticação de token de CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Configurar parâmetros de encriptação com a ferramenta de encriptação (permitir ou negar pedidos com base no tempo de expiração, país, referência, protocolo, IP de cliente. Pode utilizar qualquer combinação.)

        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - EC-expirar: atribui uma hora de expiração de um token após um período de tempo especificado. Pedidos submetidos após a hora de expiração de Olá será rejeitada. Este parâmetro utiliza Unix timestamp (em segundos desde a época padrão de 1/1/1970 00:00:00 GMT. Pode utilizar a conversão de tooprovide ferramentas online entre a hora padrão e a hora de Unix.)  Por exemplo, se quiser tooset segurança toobe token Olá expirou em 31/12/2016 12:00:00 GMT, utilize Olá Unix tempo: 1483185600 como abaixo:
    
        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - permitir que o url de EC: permite que o recurso do tootailor tokens tooa específica ou um caminho. Restringe toorequests acesso cujo URL começar com um caminho relativo específico. Pode introduzir vários caminhos separando cada caminho com uma vírgula. Os URLs são maiúsculas e minúsculas. Dependendo do requisito de Olá, pode configurar diferentes valor tooprovide um nível diferente de acesso. Seguem-se alguns cenários:
        
            Se tiver um URL: http://www.mydomain.com/pictures/city/strasbourg.png. Consulte o valor de entrada "" e o acesso de nível em conformidade

            1. Valor de entrada "/": todos os pedidos serão permitidos
            2. Valor de entrada "/ imagens": Olá todos os seguintes pedidos permitirá
            
                - http://www.mydomain.com/Pictures.png
                - http://www.mydomain.com/Pictures/City/Strasbourg.png
                - http://www.mydomain.com/picturesnew/City/strasbourgh.png
            3. Introduza o valor "imagens /": apenas os pedidos de /pictures/ será permitida
            4. Valor de entrada "/ pictures/city/strasbourg.png": só permite-lhe pedido para este recurso
    
        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - permitir que o EC-país: apenas permite pedidos provenientes de uma ou mais países especificados. Pedidos provenientes de todos os outros países serão rejeitados. Utilize código de país tooset dos parâmetros de Olá e separando cada código de país com uma vírgula. Por exemplo, se pretender que o acesso de tooallow dos Estados Unidos e França, de entrada US, FR coluna Olá como abaixo.  
        
        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - Negar EC-país: nega pedidos teve um ou mais países especificados. Serão permitidos pedidos provenientes de todos os outros países. Utilize código de país tooset dos parâmetros de Olá e separando cada código de país com uma vírgula. Por exemplo, se pretender que o acesso de toodeny dos Estados Unidos e França, de entrada US, FR na coluna de Olá.
    
        - permitir que o EC-ref: apenas permite pedidos de referência especificada. Uma referência identifica Olá URL da página web Olá que ligado recursos toohello que está a ser solicitado. valor do parâmetro de referência de Olá não deve incluir o protocolo de Olá. Pode introduzir um nome de anfitrião e/ou um caminho específico nesse nome de anfitrião. Também pode adicionar vários referrers dentro de um único parâmetro separando cada um com uma vírgula. Se tiver especificado um valor de referência, mas as informações de referência de Olá não são enviadas no pedido de Olá devido a configuração do browser toosome, estes pedidos serão rejeitados por predefinição. Pode atribuir "Em falta" ou um valor em branco no Olá parâmetro tooallow estes pedidos com informações de referência em falta. Também pode utilizar "*. consoto.com" tooallow todos os subdomínios de consoto.com.  Por exemplo, se pretender que o acesso de tooallow para pedidos de www.consoto.com, todos os subdomínios em consoto2.com e erquests com reffers em branco ou em falta, valor de entrada abaixo:
        
        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - Negar EC-ref: nega pedidos de referência especificada. Consulte toodetails e exemplo no parâmetro "ec-ref-permitir".
         
        - permitir-EC proto: apenas permite pedidos do protocolo especificado. Por exemplo, http ou https.
        
        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - Negar-EC proto: nega pedidos de protocolo especificado. Por exemplo, http ou https.
    
        - EC clientip: restringe o endereço IP de acesso toospecified autor do pedido. São suportados IPV4 e IPV6. Pode especificar o endereço IP único pedido ou a sub-rede IP.
            
        ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Pode testar o seu token com a ferramenta de decription Olá.

    4. Também pode personalizar o tipo de Olá da resposta que vai ser devolvido toouser quando o pedido é negado. Por predefinição, podemos utilizar 403.

3. Agora, clique em **motor de regras** separador em **HTTP grande**. Irá utilizar esta funcionalidade de Olá do separador toodefine caminhos tooapply, ativar a funcionalidade de autenticação de token de Olá e ativar a autenticação de token adicional relacionados com capacidades.

    - Utilize o recurso de toodefine de coluna "Se" ou o caminho que pretende que a autenticação com token tooapply. 
    - Clique em tooadd "Autenticação de Token" de Olá funcionalidade pendente tooenable autenticação com token.
        
    ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. No Olá **motor de regras** separador, existem algumas capacidades adicionais, pode ativar.
    
    - Código de recusa de autenticação de token: determina o tipo de Olá da resposta que vai ser devolvido toouser quando um pedido é negado. As regras que definir aqui substituirá a definição de código de recusa de Olá no separador de autenticação de token de Olá.
    - Ignorar a autenticação de token: determina se o URL utilizado toovalidate token vai ser sensíveis a maiúsculas e minúsculas.
    - Parâmetro de token de autenticação: mudar o nome da consulta de autenticação de token de Olá parâmetro de cadeia que mostra na Olá pedida URL. 
        
    ![Botão de gerir do painel do perfil da CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Pode personalizar o seu token que é uma aplicação que gera o token para as funcionalidades de autenticação baseada em tokens. Código de origem pode ser acedido aqui no [GitHub](https://github.com/VerizonDigital/ectoken).
Idiomas disponíveis incluem:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Funcionalidades da CDN do Azure e o fornecedor de preços

Consulte Olá [descrição geral da CDN](cdn-overview.md) tópico.
