---
title: "aaaManage acesso toocloud aplicações restringindo inquilinos - Azure | Microsoft Docs"
description: "Como toouse restrições de inquilino toomanage quais os utilizadores podem aceder a aplicações com base no seu inquilino do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: kgremban
ms.openlocfilehash: 6470fa217738b29104353ae17a2f53216f825c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-tenant-restrictions-toomanage-access-toosaas-cloud-applications"></a>Utilizar aplicações do inquilino restrições toomanage acesso tooSaaS em nuvem

Grandes organizações destacar segurança pretendem toomove toocloud serviços como o Office 365, mas tooknow necessário que os utilizadores só podem aceder a recursos de aprovados. Tradicionalmente, as empresas restringir os nomes de domínio ou endereços IP, quando pretendem toomanage acesso. Esta abordagem ocorrer uma falha de um universo de onde as aplicações SaaS estão alojadas numa nuvem pública, em execução em nomes de domínio partilhado como outlook.office.com e login.microsoftonline.com. Bloquear estes endereços seria manter os utilizadores acedam ao Outlook na web Olá completamente, em vez de restringir-os simplesmente tooapproved identidades e de recursos.

Desafio de toothis de solução do Azure do Active Directory é uma funcionalidade denominada restrições de inquilino. Inquilino restrições permite que as organizações toocontrol acesso tooSaaS nuvem aplicações, com base na utilização de aplicações do Olá do Azure AD inquilino Olá para o início de sessão único. Por exemplo, poderá pretender que as aplicações do Office 365 de tooallow acesso tooyour organização, impedindo simultaneamente as instâncias acesso tooother organizações destas mesmas aplicações.  

Fornecem as organizações Olá capacidade toospecify Olá lista de restrições de inquilinos que os utilizadores permitidos tooaccess de inquilino. Azure AD, em seguida, só concede acesso toothese permitido inquilinos.

Este artigo incida no inquilino restrições para o Office 365, mas a funcionalidade de Olá deverá trabalhar com qualquer aplicação de cloud de SaaS que utiliza protocolos de autenticação moderna com o Azure AD para o início de sessão único. Se utilizar aplicações com um diferente do Azure AD de inquilino do inquilino de Olá utilizado pelo Office 365 de SaaS, certifique-se de que todas as necessárias inquilinos são permitidos. Para obter mais informações sobre as aplicações de cloud de SaaS, consulte Olá [Active Directory Marketplace](https://azure.microsoft.com/en-us/marketplace/active-directory/).

## <a name="how-it-works"></a>Como funciona

Olá global solução é composta por Olá os seguintes componentes: 

1. **Azure AD** – se hello `Restrict-Access-To-Tenants: <permitted tenant list>` está presente, Azure AD apenas tokens de segurança de problemas para Olá permitido inquilinos. 

2. **Infraestrutura de servidor de proxy no local** – um dispositivo de proxy com capacidade de inspeção SSL de cabeçalho de Olá tooinsert configurado que contém a lista de Olá de permitido inquilinos para o tráfego destinado para o Azure AD. 

3. **Software de cliente** – toosupport restrições de inquilino, software de cliente tem de pedir tokens diretamente a partir do Azure AD, para que o tráfego pode ser intercetado por infraestrutura do proxy de Olá. Restrições de inquilino é atualmente suportado por aplicações do Office 365 baseada no browser e pelos clientes do Office quando é utilizada a autenticação moderna (por exemplo, o OAuth 2.0). 

4. **A autenticação moderna** – cloud services tem de utilizar a autenticação moderna toouse restrições de inquilino e bloquear o acesso a tooall não permitido inquilinos. Serviços do Office 365 na nuvem tem de ser protocolos de autenticação moderna toouse configurado por predefinição. Para Olá mais recentes informações sobre o suporte para a autenticação moderna do Office 365, leia o artigo [autenticação moderna do Office 365 atualizado](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/).

Olá seguinte diagrama ilustra o fluxo de tráfego de alto nível de Olá. Inspeção SSL é necessário apenas nos tráfego tooAzure AD, não toohello serviços de nuvem do Office 365. Este distinção é importante porque o volume de tráfego de Olá para autenticação tooAzure AD é normalmente muito menor aplicações tooSaaS de volume de tráfego, como o Exchange Online e SharePoint Online.

![Fluxo de tráfego de restrições de inquilino - diagrama](./media/active-directory-tenant-restrictions/traffic-flow.png)

## <a name="set-up-tenant-restrictions"></a>Configurar restrições de inquilino

Existem dois passos tooget, que foi iniciado com restrições de inquilino. Step-by-Olá primeiro passo é toomake se de que os clientes podem ligar toohello de endereços correta. Olá segundo é tooconfigure a infraestrutura de proxy.

### <a name="urls-and-ip-addresses"></a>Os URLs e endereços IP

toouse restrições de inquilino, os clientes têm de ser toohello tooconnect consegue os seguintes URLs do Azure AD tooauthenticate: login.microsoftonline.com, login.microsoft.com e login.windows.net. Além disso, tooaccess do Office 365, os clientes também tem de ser capaz de tooconnect toohello FQDNs/URLs e endereços IP definidos no [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2). 

### <a name="proxy-configuration-and-requirements"></a>Configuração de proxy e de requisitos

Olá seguir configuração é necessária tooenable restrições de inquilino através da infraestrutura de proxy. Esta orientação é genérica, pelo que deve consulte a documentação do fornecedor de proxy a tooyour para obter os passos de implementação específicos.

#### <a name="prerequisites"></a>Pré-requisitos

- proxy Olá tem de ser capaz de tooperform interception de SSL, inserção de cabeçalho HTTP e destinos de filtro utilizando FQDNs/URLs. 

- Os clientes têm de confiar cadeia de certificados de Olá apresentada pelo proxy de Olá para as comunicações SSL. Por exemplo, se forem utilizados certificados a partir de uma PKI interna, Olá interno emissora certificado autoridade certificado de raiz tem de ser fidedigno.

- Esta funcionalidade está incluída em subscrições do Office 365, mas se pretender que as aplicações de SaaS de tooother toocontrol acesso toouse restrições de inquilino são necessárias, em seguida, licenças do Azure AD Premium 1.

#### <a name="configuration"></a>Configuração

Para cada entrada toologin.microsoftonline.com de pedido, login.microsoft.com e login.windows.net, insira dois cabeçalhos HTTP: *restringir acesso para inquilinos* e *contexto de restringir acesso*.

cabeçalhos de Olá devem incluir Olá seguintes elementos: 
- Para *restringir acesso para inquilinos*, um valor de \<permitido lista inquilino\>, que é uma lista separada por vírgulas de inquilinos que pretende tooallow tooaccess de utilizadores. Qualquer domínio que está registado com um inquilino pode ser o inquilino de Olá tooidentify utilizado nesta lista. Por exemplo, toopermit aceder tooboth Contoso e Fabrikam inquilinos, Olá procura do par nome/valor como:`Restrict-Access-To-Tenants: contoso.onmicrosoft.com,fabrikam.onmicrosoft.com` 
- Para *contexto de restringir acesso*, um valor de um ID de diretório única, declarar que inquilino é definir Olá restrições de inquilino. Por exemplo, toodeclare Contoso inquilino Olá que definir Olá política de restrições de inquilino, par nome/valor de Olá aspeto:`Restrict-Access-Context: 456ff232-35l2-5h23-b3b3-3236w0826f3d`  

> [!TIP]
> Pode encontrar o ID de diretório no Olá [portal do Azure](https://portal.azure.com). Inicie sessão como administrador, selecione **do Azure Active Directory**, em seguida, selecione **propriedades**.

utilizadores de tooprevent de inserir os seus próprios cabeçalho HTTP com inquilinos não aprovado, Olá proxy tem de cabeçalho de restringir acesso para inquilinos tooreplace Olá se já se encontra presente no pedido recebido Olá. 

Os clientes tem de ser forçada toouse Olá proxy para todos os pedidos toologin.microsoftonline.com, login.microsoft.com e login.windows.net. Por exemplo, se os ficheiros PAC são utilizados toodirect clientes toouse Olá proxy, os utilizadores finais não deve ser capaz de tooedit nem desativar ficheiros Olá PAC.

## <a name="hello-user-experience"></a>experiência de utilizador Olá

Esta secção mostra experiência Olá para os utilizadores finais e administradores.

### <a name="end-user-experience"></a>Experiência do utilizador final

Um utilizador de exemplo é na rede de Contoso Olá, mas está a tentar tooaccess Olá Fabrikam instância uma partilhado aplicação SaaS, como o Outlook online. Se a Contoso é um inquilino não permitido para essa instância, o utilizador de Olá vê Olá seguinte página:

![Acesso negado página utilizadores inquilinos não permitido](./media/active-directory-tenant-restrictions/end-user-denied.png)

### <a name="admin-experience"></a>Experiência da administração

Enquanto a configuração de restrições de inquilino é efetuada na infraestrutura de proxy empresarial Olá, administradores podem aceder a relatórios de restrições de inquilino Olá no Olá portal do Azure diretamente. Olá tooview relatórios, visite a página de descrição de geral do Azure Active Directory toohello, em seguida, procure em 'Outras capacidades' '.

Olá, admin para o inquilino Olá especificado como inquilino Olá contexto de acesso restrito pode utilizar este toosee relatório todos os inícios de sessão bloqueado devido a Olá política de restrições de inquilino, incluindo a identidade de Olá utilizada e ID de diretório de destino Olá.

![Utilizar tooview portal do Azure restringida tentativas Olá de início de sessão](./media/active-directory-tenant-restrictions/portal-report.png)

Como outros relatórios no Olá portal do Azure, pode utilizar filtros toospecify Olá âmbito do seu relatório. Pode filtrar por um utilizador específico, a aplicação, o cliente ou o intervalo de tempo.

## <a name="office-365-support"></a>Suporte do Office 365

Aplicações do Office 365 tem de cumprir dois critérios de suporte de toofully restrições do inquilino:

1. cliente de Olá utilizado suporta a autenticação moderna
2. A autenticação moderna está ativada como protocolo de autenticação predefinido de Olá para o serviço de nuvem Olá.

Consulte demasiado[autenticação moderna do Office 365 atualizado](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/) para informações mais recentes Olá no qual Office os clientes suportam atualmente a autenticação moderna. Nessa página também inclui ligações tooinstructions para ativar a autenticação moderna específico Exchange Online e Skype para empresas Online aos inquilinos. A autenticação moderna já está ativada por predefinição no SharePoint Online.

Restrições de inquilino é atualmente suportado por aplicações baseadas no browser do Office 365 (Olá SharePoint do Portal do Office, Yammer, sites, o Outlook no Olá Web, etc.). Para clientes Espesso (Outlook, Skype para empresas, Word, Excel, PowerPoint, etc.) Restrições de inquilino podem ser impostas apenas quando é utilizada a autenticação moderna.  

Outlook e o Skype para clientes de negócio que suportam a autenticação moderna são ainda consegue toouse protocolos legados contra inquilinos em que a autenticação moderna não está ativada, ignorando eficazmente as restrições de inquilino. Para o Outlook no Windows, os clientes podem optar restrições tooimplement a impedir que os utilizadores finais adicionar perfis de tootheir de contas de correio não aprovado. Por exemplo, consulte Olá [impedir adicionar contas de Exchange não predefinidas](http://gpsearch.azurewebsites.net/default.aspx?ref=1) definição de política de grupo. Para o Outlook em plataformas não sejam Windows e para o Skype para empresas em todas as plataformas, suporte completo de restrições de inquilino não está atualmente disponível.

## <a name="testing"></a>Testes

Se quiser tootry saída restrições de inquilino antes de a implementar para toda a organização, existem duas opções: uma abordagem baseada em anfitrião utilizando uma ferramenta como o Fiddler ou uma implementação faseada de definições de proxy.

### <a name="fiddler-for-a-host-based-approach"></a>Fiddler para uma abordagem baseada no anfitrião

Fiddler é uma web livre depuração proxy que pode ser utilizado toocapture e modificam o tráfego HTTP/HTTPS, incluindo a inserir os cabeçalhos de HTTP. tooconfigure Fiddler tootest restrições de inquilino, execute Olá os seguintes passos:

1.  [Transfira e instale o Fiddler](http://www.telerik.com/fiddler).
2.  Configurar o tráfego HTTPS de toodecrypt Fiddler, por [documentação de ajuda do Fiddler](http://docs.telerik.com/fiddler/Configure-Fiddler/Tasks/DecryptHTTPS).
3.  Configurar Olá de tooinsert Fiddler *restringir acesso para inquilinos* e *contexto de restringir acesso* cabeçalhos utilizando regras personalizadas:
  1. Na ferramenta de depurador de Web Fiddler Olá, selecione Olá **regras** menu e selecione **personalizar regras...** ficheiro de CustomRules Olá tooopen.
  2. Adicionar Olá seguintes linhas no início Olá Olá *OnBeforeRequest* função. Substitua \<domínio de inquilino\> com um domínio registado seu inquilino, por exemplo, contoso.onmicrosoft.com. Substitua \<ID de diretório\> com o identificador do seu inquilino do Azure AD GUID.

  ```
  if (oSession.HostnameIs("login.microsoftonline.com") || oSession.HostnameIs("login.microsoft.com") || oSession.HostnameIs("login.windows.net")){      oSession.oRequest["Restrict-Access-To-Tenants"] = "<tenant domain>";      oSession.oRequest["Restrict-Access-Context"] = "<directory ID>";}
  ```

  Se precisar de tooallow vários inquilinos, utilize nomes de inquilino uma vírgula tooseparate Olá. Por exemplo:

  ```
  oSession.oRequest["Restrict-Access-To-Tenants"] = "contoso.onmicrosoft.com,fabrikam.onmicrosoft.com";
  ```

4. Guarde e feche o ficheiro de CustomRules Olá.

Depois de configurar o Fiddler, pode capturar o tráfego por vai toohello **ficheiro** menu e selecionando **capturar tráfego**.

### <a name="staged-rollout-of-proxy-settings"></a>Implementação faseada de definições de proxy

Consoante as capacidades de Olá da sua infraestrutura de proxy, poderá ser toostage capaz de implementação de Olá de utilizadores de tooyour de definições. Seguem-se algumas opções de alto nível para consideração:

1.  Utilize PAC ficheiros toopoint teste utilizadores tooa teste infraestrutura do proxy, enquanto os utilizadores normais continuam a infraestrutura do proxy de toouse Olá produção.
2.  Alguns servidores proxy podem suportar utilizar grupos de configurações diferentes.

Consulte a documentação do servidor de proxy de tooyour para obter detalhes específicos.

## <a name="next-steps"></a>Passos seguintes

- Leia sobre [autenticação moderna do Office 365 atualizado](https://blogs.office.com/2015/11/19/updated-office-365-modern-authentication-public-preview/)

- Olá revisão [intervalos de endereços IP e URLs do Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
