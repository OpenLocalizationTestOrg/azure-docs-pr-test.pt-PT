---
title: "localizações de aaaNamed no Azure Active Directory | Microsoft Docs"
description: "Ao configurar a chamada localizações, pode evitar a necessidade de IP endereços que são proprietário pela sua organização geram falsos positivos para localizações de tooatypical Olá impossível o risco de tipo de evento."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 591e4b94b2ec9d45e20c01711e922f9972e047e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="named-locations-in-azure-active-directory"></a>Localizações nomeadas no Azure Active Directory

Com Olá com o nome da funcionalidade de localizações do Azure Active Directory, pode Etiquetar intervalos de endereços IP fidedignos nas suas organizações. No seu ambiente, pode utilizar localizações chamadas no contexto de Olá deteção Olá de [eventos de risco](active-directory-reporting-risk-events.md). funcionalidade de Olá ajuda a reduzir o número de Olá de comunicado falsos positivos para Olá *impossível tooatypical localizações* o risco de tipo de evento. 

## <a name="configuration"></a>Configuração

tooconfigure uma localização com nome:

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) como administrador global.

2. No painel esquerdo Olá, clique em **do Azure Active Directory**.

    ![ligação do Azure Active Directory Olá no painel esquerdo Olá](./media/active-directory-named-locations/01.png)

3. No Olá **do Azure Active Directory** painel, no Olá **segurança** secção, clique em **acesso condicional**.

    ![Olá comandos de acesso condicional](./media/active-directory-named-locations/05.png)


4. No Olá **acesso condicional** painel, no Olá **gerir** secção, clique em **denominado localizações**.

    ![Olá denominado localizações comando](./media/active-directory-named-locations/06.png)


5. No Olá **denominado localizações** painel, clique em **nova localização**.

    ![Olá novo comando localização](./media/active-directory-named-locations/07.png)


6. No Olá **novo** painel, Olá a seguir:

    ![Painel nova Olá](./media/active-directory-named-locations/08.png)

    a. No Olá **nome** caixa, escreva um nome para a sua localização com nome.

    b. No Olá **intervalos IP** caixa, escreva um intervalo de IP. intervalo IP Olá tem toobe no Olá *encaminhamento-Classless Inter-Domain* formato (CIDR).  

    c. Clique em **Criar**.



## <a name="what-you-should-know"></a>O que deve conhecer

**Em massa atualizações**: ao criar ou atualizar localizações com nome, para as atualizações em massa, pode carregar ou transferir um ficheiro CSV com intervalos IP Olá. Um carregamento adiciona os intervalos IP Olá na lista de toohello Olá ficheiros em vez de substituir a lista de Olá.

![Olá carregar e transferir ligações](./media/active-directory-named-locations/09.png)


**Limitações**: pode definir um máximo de 60 localizações com nome, com um tooeach de intervalo atribuído de IP dos mesmos. Se tiver apenas uma localização com nome configurada, pode definir too500 intervalos IP para o mesmo.


## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre eventos de risco, consulte [eventos de risco do Azure Active Directory](active-directory-reporting-risk-events.md).

