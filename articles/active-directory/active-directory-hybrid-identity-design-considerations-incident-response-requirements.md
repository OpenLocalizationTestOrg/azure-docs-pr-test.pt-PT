---
title: "considerações de design do aaaAzure do Active Directory híbrida identidade - determinar os requisitos de incidente rResponse | Microsoft Docs"
description: "Determinar as capacidades de monitorização e relatórios para a solução de identidade híbrida do Olá que podem ser aproveitadas pelas IT tootake ações tooidentify e mitigar uma potenciais ameaças"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 7084096f318ef461e8331fb6edde1b77d4108466
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a>Determinar os requisitos de resposta a incidentes para a sua solução de identidade híbrida
As organizações de médias ou grandes provavelmente terá um [resposta a incidentes segurança](https://technet.microsoft.com/library/cc700825.aspx) no local toohelp IT executar ações em conformidade toohello nível do incidente. sistema de gestão de identidade Olá é um componente importante no processo de resposta a incidentes de Olá porque pode ser utilizado toohelp identificar quem efetuou uma ação específica contra o destino de Olá. solução de identidade híbrida Olá tem de ser capaz de tooprovide monitorização capacidades e relatórios que podem ser aproveitadas pelas IT tootake ações tooidentify e mitigar uma potencial ameaça. Um plano de resposta a incidentes típico terá Olá seguintes fases como parte do plano de Olá:

1. Avaliação inicial.
2. Comunicação de incidente.
3. Controlo de danos e redução do risco.
4. Identificação dos quais foi comprometida e a gravidade.
5. Preservação de prova.
6. Partes de tooappropriate de notificação.
7. Recuperação de sistema.
8. Documentação.
9. Avaliação de danos e o custo.
10. Revisão de processo e o plano.

Durante a identificação de Olá dos qual it foi comprometida e a fase de gravidade, será necessário tooidentify Olá sistemas que tem sido comprometidos, os ficheiros que tenham sido acedidos e determinam a sensibilidade Olá desses ficheiros. O sistema de identidade híbrida deve ser capaz de toofulfill tooassist estes requisitos a identificar o utilizador de Olá que efetuou essas alterações. 

## <a name="monitoring-and-reporting"></a>Monitorização e relatórios
Sistema de identidade do número de vezes Olá também pode ajudar na fase de avaliação inicial, principalmente se o sistema de Olá criada na auditoria e capacidades de relatórios. Durante a avaliação inicial Olá, administrador de TI tem de ser capaz de tooidentify uma atividade suspeita ou sistema Olá deve ser capaz de tootrigger automaticamente com base numa tarefa de pré-configurada. Muitas atividades pode indicar um ataque possíveis, no entanto, noutros casos, um sistema configurado incorretamente pode originar tooa número de falsos positivos num sistema de deteção de intrusões. 

sistema de gestão de identidade Olá deve ajudar IT admins tooidentify e comunicar essas atividades suspeitas. Normalmente, estes requisitos técnicos podem ser cumpridos através da monitorização de todos os sistemas e ter uma capacidade de relatórios que pode realçar potenciais ameaças. Utilizar perguntas de Olá abaixo toohelp a sua solução de identidade híbrida ao colocar em requisitos de resposta a incidentes de consideração de design:

* Da sua empresa tem uma resposta de incidente de segurança no local?
  * Se Sim, é hello atual sistema de gestão de identidade utilizado como parte do processo de Olá?
* A sua empresa precisa de tooidentify tentativas de início de sessão suspeitos dos utilizadores entre vários dispositivos?
* A sua empresa precisa de toodetect potenciais comprometido credenciais do utilizador?
* A sua empresa precisa de acesso e a ação do utilizador de tooaudit?
* A sua empresa precisa de tooknow quando um utilizador repor a palavra-passe?

## <a name="policy-enforcement"></a>Imposição de política
Durante o controlo de danos e a fase de redução do risco, é importante tooquickly reduzir os efeitos de real e potenciais Olá de um ataque. Neste momento, essa ação que irá demorar pode tornar diferença Olá entre uma secundária e um principal. resposta exata Olá dependerá-se a sua organização e a natureza Olá de ataque de Olá enfrentam. Se a avaliação inicial Olá concluir que uma conta foi comprometida, terá de tooenforce política tooblock esta conta. É apenas um exemplo onde irá ser aproveitado sistema de gestão de identidade Olá. Utilize perguntas de Olá abaixo toohelp que estruturar a solução de identidade híbrida enquanto tendo em consideração, como será políticas impostas tooreact tooan em curso incidente:

* A sua empresa tem políticas local tooblock utilizadores a partir da rede de Olá acesso se necessário?
  * Se Sim, Olá atual solução integrada com o sistema de gestão de identidade do Olá híbridos que são curso tooadopt?
* A sua empresa precisa de acesso condicional tooenforce para utilizadores que estão em quarentena? 

> [!NOTE]
> Certifique-se de que tootake notas de cada resposta e compreender a lógica por detrás de Olá atrás de resposta de Olá. [Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) abordará as opções de Olá disponíveis e as vantagens/desvantagens de cada opção.  Ao responder a estas questões, vai selecionar que opções melhor se adapta às sua empresa precisa.
> 
> 

## <a name="next-steps"></a>Passos seguintes
[Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a>Veja Também
[Descrição geral das considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

