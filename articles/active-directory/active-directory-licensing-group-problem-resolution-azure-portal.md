---
title: "problemas de licença aaaResolve para um grupo no Azure Active Directory | Microsoft Docs"
description: "Como tooidentify e resolva licença problemas de atribuição ao utilizar o Azure Active Directory baseadas em grupos de licenciamento"
services: active-directory
keywords: Licenciamento do Azure AD
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/05/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ec9c74214a9e246f21fcf767b0bbd586ae702445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="identify-and-resolve-license-assignment-problems-for-a-group-in-azure-active-directory"></a>Identificar e resolver problemas de atribuição de licença para um grupo no Azure Active Directory

Com base no grupo de licenciamento no Azure Active Directory (Azure AD) apresenta o conceito de Olá de utilizadores num Estado de erro licenciamento. Neste artigo, vamos explicar motivos Olá motivo pelo qual os utilizadores poderão ficar neste estado.

Ao atribuir licenças de utilizadores de tooindividual diretamente, sem utilizar baseadas em grupos de licenciamento, a operação de atribuição de Olá poderá falhar. Por exemplo, quando executar cmdlet do PowerShell Olá `Set-MsolUserLicense` num utilizador, o cmdlet Olá pode falhar por uma série de razões que estão relacionados toobusiness lógica. Por exemplo, poderá existir um número insuficiente de licenças ou um conflito entre duas planos de serviço que não é possível atribuir ao hello mesmo tempo. Olá problema imediatamente comunicado fazer uma cópia tooyou.

Quando estiver a utilizar com base no grupo de licenciamento, Olá mesmos erros podem ocorrer, mas acontecer em segundo plano de Olá quando Olá serviço Azure AD é atribuir licenças. Por este motivo, erros de Olá não podem ser comunicada tooyou imediatamente. Em vez disso, serem registadas no objeto de utilizador Olá e, em seguida, comunicados através do portal administrativo Olá. Tenha em atenção que o utilizador de Olá original toolicense intenção Olá nunca é perdido, mas é registada em estado de erro para investigação futura e resolução.

## <a name="how-toofind-license-assignment-errors"></a>Como toofind licença erros de atribuição

1. utilizadores de toofind num Estado de erro num grupo específico, o painel de Olá aberta para o grupo de Olá. Em **licenças**, existirá uma notificação apresentada se existirem quaisquer utilizadores num Estado de erro.

![Notificação do grupo, erro](media/active-directory-licensing-group-problem-resolution-azure-portal/group-error-notification.png)

2. Clique em Olá notificação tooopen uma lista de todos os utilizadores afetados. Pode clicar em cada utilizador individualmente toosee mais detalhes.

![Grupo, lista de utilizadores num Estado de erro](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-users-with-errors.png)

3. toofind todos os grupos que contém pelo menos um erro no Olá **do Azure Active Directory** painel selecione **licenças** e, em seguida, **descrição geral**. É apresentada uma caixa de informações quando alguns grupos necessitam da sua atenção.

![Descrição geral, informações sobre os grupos no estado de erro](media/active-directory-licensing-group-problem-resolution-azure-portal/group-errors-widget.png)

4. Clique em Olá caixa toosee uma lista de todos os grupos com erros. Pode clicar em cada grupo para obter mais detalhes.

![Descrição geral, a lista de grupos de erros](media/active-directory-licensing-group-problem-resolution-azure-portal/list-of-groups-with-errors.png)


Segue-se uma descrição de cada tooresolve de forma potencial problema e Olá-lo.

## <a name="not-enough-licenses"></a>Licenças não suficientes

**Problema:** não sabemos de licenças suficientes disponíveis para um dos produtos de Olá especificada no grupo de Olá. Terá de tooeither adquira mais licenças para o produto Olá ou liberte licenças por utilizar de outros utilizadores ou grupos.

toosee quantas licenças estão disponíveis, visite demasiado**do Azure Active Directory** > **licenças** > **todos os produtos**.

toosee que utilizadores e grupos que está a consumir licenças, clique num produto. Em **licenciado a utilizadores**, verá todos os utilizadores que já teve atribuídas diretamente ou através de um ou mais grupos de licenças. Em **licenciado grupos**, verá todos os grupos que têm esse produto atribuído.

**PowerShell:** cmdlets do PowerShell comunique este erro como _CountViolation_.

## <a name="conflicting-service-plans"></a>Planos de serviços em conflito

**Problema:** um dos produtos de Olá especificada no grupo de Olá contém um plano de serviço está em conflito com outro plano de serviço que já está atribuído toohello utilizador através de um produto diferente. Alguns planos de serviço estão configurados de forma a que estes não podem ser atribuídos toohello mesmo utilizador outro plano de serviço relacionado.

Considere o seguinte exemplo de Olá. Um utilizador tenha uma licença para o Office 365 Enterprise **E1** atribuídos diretamente, com todos os planos de Olá ativados. Olá utilizador foi adicionado tooa grupo que tenha Olá Office 365 Enterprise **E3** tooit produto atribuído. Este produto contém planos de serviço que não se podem sobrepor com planos de Olá incluídos no E1, pelo que a atribuição de licenças do grupo de Olá irá falhar com Olá erro "Em conflito os planos de serviço". Neste exemplo, os planos de serviços em conflito Olá são:

-   SharePoint Online (planear 2) está em conflito com o SharePoint Online (planear 1).
-   Exchange Online (planear 2) está em conflito com o Exchange Online (planear 1).

toosolve este conflito, terá de toodisable os planos de dois em Olá E1 de licença da toohello diretamente atribuída utilizador. Em alternativa, tem de atribuição de licenças do toomodify Olá grupo inteiro e desative os planos de Olá na licença de E3 Olá. Em alternativa, poderá decidir licença de E1 Olá tooremove de utilizador de Olá se for redundante no contexto de Olá da licença de E3 Olá.

Decisão de Olá sobre como o produto em conflito tooresolve licenças sempre pertence toohello administrador. Azure AD automaticamente não resolve conflitos de licença.

**PowerShell:** cmdlets do PowerShell comunique este erro como _MutuallyExclusiveViolation_.

## <a name="other-products-depend-on-this-license"></a>Outros produtos dependem esta licença

**Problema:** um dos produtos de Olá especificada no grupo de Olá contém um plano de serviço que deve estar ativado para outro plano de serviço, no outro produto, para a função. Este erro ocorre quando o Azure AD tenta plano de serviço do tooremove Olá subjacente. Por exemplo, isto pode acontecer devido a utilizador Olá a ser removido do grupo de Olá.

toosolve este problema, tem de certificar-se de que plano de necessário Olá ainda se encontrar atribuído toousers através de algum outro método, ou que os serviços dependentes Olá estão desativados para esses utilizadores toomake. Depois de fazer, pode remover corretamente licença do grupo de Olá esses utilizadores.

**PowerShell:** cmdlets do PowerShell comunique este erro como _DependencyViolation_.

## <a name="usage-location-isnt-allowed"></a>Não é permitida a localização de utilização

**Problema:** alguns serviços da Microsoft não estão disponíveis em todas as localizações devido ao locais leis e regulamentos. Antes de pode atribuir um utilizador de tooa de licença, tem de propriedade de "Localização de utilização" Olá toospecify para utilizador Olá. Pode fazê-lo em Olá **utilizador** > **perfil** > **definições** secção Olá portal do Azure.

Quando o Azure AD tenta tooassign grupo licença tooa utilizador cuja localização de utilização não é suportada, irá falhar e registe este erro utilizador Olá.

toosolve este problema, remova utilizadores a partir de localizações nonsupported do grupo de Olá licenciado. Em alternativa, se os valores de localização de utilização atuais Olá não representam a localização de utilizador reais Olá, pode modificá-los para que Olá são atribuídas as licenças corretamente próxima vez (se a nova localização de hello é suportada).

**PowerShell:** cmdlets do PowerShell comunique este erro como _ProhibitedInUsageLocationViolation_.

> [!NOTE]
> Quando o Azure AD atribui licenças de grupo, os utilizadores sem uma localização de utilização especificada herdam localização Olá do diretório de Olá. Recomendamos que os administradores definir utilização correta de Olá valores da localização em utilizadores antes de utilizar baseado no grupo de licenciamento toocomply com locais leis e regulamentos.

## <a name="what-happens-when-theres-more-than-one-product-license-on-a-group"></a>O que acontece quando existe mais do que uma licença do produto num grupo?

Pode atribuir mais de um grupo de tooa de licença de produto. Por exemplo, pode atribuir do Office 365 Enterprise E3 e Enterprise Mobility + segurança tooa grupo tooeasily ativar incluídos todos os serviços para os utilizadores.

Azure AD tenta tooassign todas as licenças que são especificadas no utilizador de tooeach Olá grupo. Se AD do Azure não é possível atribuir um dos produtos de Olá devido a problemas de lógica de negócio (por exemplo, se não existirem licenças suficientes para todos os, ou se existirem conflitos com outros serviços que estão ativados no utilizador Olá), não atribua Olá outras licenças no grupo de Olá ambos.

Será Olá toosee capaz de falha de utilizadores que não foi possível tooget atribuído e verifique quais produtos foram afetados por este.

## <a name="license-assignment-fails-silently-for-a-user-due-tooduplicate-proxy-addresses-in-exchange-online"></a>Atribuição de licenças silenciosamente falha por um utilizador que devem estar tooduplicate endereços de proxy no Exchange Online

Se estiver a utilizar o Exchange Online, alguns utilizadores no seu inquilino podem estar incorretamente configurados com Olá mesmo valor de endereço do proxy. Quando baseadas em grupos de licenciamento tenta tooassign toosuch uma licença um utilizador, este irá falhar e não irá registar um erro (ao contrário no Olá outros casos de erro descritos acima) - esta é uma limitação na versão de pré-visualização de Olá desta funcionalidade e iremos tooaddress-lo antes de  *Disponibilidade geral*.

> [!TIP]
> Se reparar em que alguns utilizadores não recebeu uma licença e que não existe nenhum erro registado nesses utilizadores, verifique primeiro se tiverem o endereço proxy duplicado.
> Pode fazê-lo executando Olá seguinte cmdlet do PowerShell no Exchange Online:
```
Run Get-Recipient | where {$_.EmailAddresses -match "user@contoso.onmicrosoft.com"} | fL Name, RecipientType,emailaddresses
```
> [Este artigo](https://support.microsoft.com/help/3042584/-proxy-address-address-is-already-being-used-error-message-in-exchange-online) contém mais detalhes sobre este problema, incluindo informações no [como tooExchange tooconnect Online com o PowerShell remoto](https://technet.microsoft.com/library/jj984289.aspx).

Depois de resolver problemas do proxy foram resolvidos para utilizadores Olá afetado, certifique-se de licença de tooforce processamento Olá grupo toomake se licenças podem agora ser aplicadas novamente.

## <a name="how-do-you-force-license-processing-in-a-group-tooresolve-errors"></a>Como forçar a licença do processamento de erros de tooresolve um grupo?

Consoante o que os passos tiver decorrido tooresolve erros, poderá ser necessário toomanually processamento de Acionador um grupo tooupdate Olá do Estado do utilizador.

Por exemplo, se libertado segurança algumas licenças removendo as atribuições de licenças direta de utilizadores, terá de processamento de tootrigger dos grupos que tenha falhado anteriormente toofully licença todos os membros de utilizador. Abra o toodo que, de localizar o painel do grupo de Olá, **licenças**e selecione Olá **Reprocessar** botão na toolbar Olá.

## <a name="next-steps"></a>Passos seguintes

toolearn mais informações sobre outros cenários para gestão de licenças através de grupos, consulte o artigo seguinte Olá:

* [Atribuição de licenças tooa grupo no Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [O que é o licenciamento no Azure Active Directory com base no grupo?](active-directory-licensing-whatis-azure-portal.md)
* [Como toomigrate indivíduo licenciado a utilizadores baseados em toogroup licenciamento no Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory baseadas em grupos licenciamento cenários adicionais](active-directory-licensing-group-advanced.md)
