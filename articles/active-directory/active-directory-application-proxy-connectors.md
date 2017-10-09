---
title: "os conectores de Proxy de aplicações do Azure AD portais aaaClassic | Microsoft Docs"
description: "Abrange como toocreate e gerir grupos de conectores no Proxy de aplicações do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publicar aplicações em redes separadas e localizações utilizar grupos de conector
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portal Clássico do Azure](active-directory-application-proxy-connectors.md)
>
>

Grupos de conector são úteis para vários cenários, incluindo:

* Sites com vários centros de dados interligados. Neste caso, pretende tookeep o mesmo tráfego num centro de dados de Olá possível porque as ligações do Centro de dados entre são dispendiosas e lenta. Pode implementar conectores em cada datacenter tooserve apenas Olá aplicações que residem no Olá Centro de dados. Esta abordagem minimiza o Centro de dados entre ligações e fornece uma experiência totalmente transparente tooyour utilizadores.
* Gerir aplicações instaladas em redes isoladas que não fazem parte da rede empresarial principal de Olá. Pode utilizar os conectores do conector grupos tooinstall dedicada na rede de toohello redes isoladas tooalso isolar aplicações.
* Para as aplicações instaladas no IaaS para acesso à nuvem, os grupos de conector fornecem um serviço toosecure Olá acesso tooall Olá aplicações comuns. Grupos de conector não criar dependência adicional na sua rede empresarial ou experiência de aplicação Olá de fragmento. Os conectores podem ser instalados em todos os centros de dados de nuvem e servem apenas as aplicações que residem nesta rede. Pode instalar vários conectores tooachieve elevada disponibilidade.
* Suporte para ambientes de várias florestas que conectores específicos podem ser implementados por floresta e tooserve de aplicações específicas.
* Grupos de conector podem ser utilizados em locais de recuperação após desastre tooeither detetar ativação pós-falha ou como cópia de segurança para Olá principal site.
* Grupos de conector também podem ser utilizado tooserve várias empresas a partir de um único inquilino.

## <a name="prerequisite-create-your-connectors"></a>Pré-requisito: Criar a sua conectores
toogroup os conectores, [instalar vários conectores](active-directory-application-proxy-enable.md), em seguida, atribua um nome e agrupá-los. Por fim tiver tooassign toospecific aplicações-los.

## <a name="step-1-create-connector-groups"></a>Passo 1: Criar grupos de conector
Pode criar grupos de conector tantos conforme pretender. Criação do conector de grupo é efetuada no Olá portal clássico do Azure.

1. Selecione o diretório e clique em **configurar**.  
    ![Proxy de aplicações, configure a captura de ecrã - clique em Gerir grupos de conetor](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. No Proxy de aplicações, clique em **gerir grupos de conector** e criar um grupo de conector, concedendo um nome de grupo Olá.  
    ![Captura de ecrã - novo grupo de nome de grupos do conector do proxy da aplicação](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Passo 2: Atribuir conectores tooyour grupos
Depois de Olá conector grupos são criados, mova grupo adequado do Olá conectores toohello.

1. Em **Proxy de aplicações**, clique em **gerir conectores**.
2. Em **grupo**, selecione o grupo de Olá que pretende para cada conector. Poderá demorar conectores Olá segurança too10 minutos toobecome ativos no novo grupo de Olá.  
    ![Captura de conectores ecrã aplicação proxy - selecione grupo a partir do menu pendente](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Passo 3: Atribuir aplicações tooyour grupos de conetor
último passo de Olá é tooset cada grupo de conector de toohello de aplicação que serve-lo.

1. No Olá portal clássico do Azure, no seu diretório, selecione Olá a aplicação que pretende tooassign toohello grupo e clique em **configurar**.
2. Em **grupo conector**, selecione o grupo de Olá pretende Olá toouse de aplicação. Esta alteração será imediatamente aplicada.  
    ![Aplicação proxy conector grupo captura de ecrã - selecione grupo a partir do menu pendente](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Consultar também
* [Ativar o Proxy da aplicação](active-directory-application-proxy-enable.md)
* [Ativar o início de sessão único](active-directory-application-proxy-sso-using-kcd.md)
* [Ativar o acesso condicional](active-directory-application-proxy-conditional-access.md)
* [Resolver problemas com o Proxy da aplicação](active-directory-application-proxy-troubleshoot.md)

Para obter notícias mais recentes Olá e atualizações, consulte Olá [blogue do Proxy da aplicação](http://blogs.technet.com/b/applicationproxyblog/)
