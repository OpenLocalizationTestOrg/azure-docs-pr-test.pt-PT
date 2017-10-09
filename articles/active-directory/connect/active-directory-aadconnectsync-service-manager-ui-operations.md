---
title: "Operações de Gestor do serviço de sincronização do Azure AD Connect | Microsoft Docs"
description: "Compreenda o separador operações Olá Olá Synchronization Service Manager do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Utilizar Olá separador operações de Gestor do serviço de sincronização

![Gestor do serviço de sincronização](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

separador de operações de Olá mostra resultados de Olá de operações de Olá mais recentes. Este separador é toounderstand chave e resolver problemas.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Compreender as informações de Olá visíveis no separador de operações de Olá
metade superior Olá mostra todas as execuções por ordem cronológica. Por predefinição, registo de operações de Olá mantém informações sobre Olá últimos sete dias, mas esta definição pode ser alterada com Olá [programador](active-directory-aadconnectsync-feature-scheduler.md). Pretende toolook para qualquer execução que mostram um Estado de êxito. Pode alterar Olá ordenação clicando cabeçalhos Olá.

Olá **estado** coluna é informações mais importantes Olá e mostra hello mais grave problema para a execução. Eis um resumo rápido das Estados mais comuns de Olá por ordem de prioridade tooinvestigate (onde * indicar vários cadeias de erro possíveis).

| Estado | Comentário |
| --- | --- |
| parado-* |Não foi possível concluir a Olá executar. Por exemplo, se hello sistema remoto não está disponível e não pode ser contactado. |
| parado-erro-limite |Existem mais de 5.000 erros. Olá executar automaticamente foi parado devido toohello grande número de erros. |
| concluída -\*-erros |Olá execute concluída, mas existem erros (menos de 5000) que devem ser investigados. |
| concluída -\*-avisos |Olá executar concluída, mas alguns dados não estão num Estado de Olá esperado. Se tiver de erros, em seguida, esta mensagem é, normalmente, apenas um sintoma. Até ter resolvidas erros, não deve investigar avisos. |
| exito |Não existem problemas. |

Quando seleciona uma linha, na parte inferior do Olá atualizações tooshow Olá detalhes que são executados. toohello extremidade esquerda do inferior Olá, poderá ter uma indicação de lista **passo n. º**. Esta lista aparece apenas se tiver vários domínios na floresta onde cada domínio é representado por um passo. nome de domínio Olá pode ser encontrado no cabeçalho de Olá **partição**. Em **estatísticas de sincronização**, pode encontrar mais informações sobre o número de Olá de alterações que foram processados. Pode clicar em Olá ligações tooget uma lista de objetos de Olá alterado. Se tiver de objetos com erros, esses surgem erros em **erros de sincronização**.

Para obter mais informações, consulte [resolver problemas de um objeto que não está a sincronizar](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).
