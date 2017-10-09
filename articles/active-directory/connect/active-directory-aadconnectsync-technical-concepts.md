---
title: "Sincronização do Azure AD Connect: conceitos técnicos | Microsoft Docs"
description: "Explica os conceitos técnicos do Olá de sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 731cfeb3-beaf-4d02-aef4-b02a8f99fd11
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: c6309bb9be462fb3d49c5b6ab302d4327ce4b7be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-technical-concepts"></a>Sincronização do Azure AD Connect: Conceitos Técnicos
Este artigo é um resumo de tópico Olá [arquitetura de compreender](active-directory-aadconnectsync-technical-concepts.md).

Sincronização do Azure AD Connect baseia-se na plataforma de sincronização de metadiretório sólida.
Olá secções a seguir apresenta conceitos Olá para a sincronização de metadiretório.
Criar após MIIS, ILM e FIM, serviços de sincronização de diretório Active Directory do Olá do Azure fornece Olá seguinte plataforma para ligação toodata origens, sincronizar dados entre origens de dados, bem como Olá aprovisionamento e desaprovisionamento das identidades.

![Conceitos Técnicos](./media/active-directory-aadconnectsync-technical-concepts/scenario.png)

Olá seguintes secções fornece mais detalhes sobre Olá aspetos do serviço de sincronização do FIM de Olá os seguintes:

* conector
* Fluxo de atributos
* Espaço de conector
* Metaverso
* Aprovisionamento

## <a name="connector"></a>conector
módulos de código Olá, que são utilizado toocommunicate com um diretório ligado são denominados conectores (anteriormente conhecidos como agentes de gestão (MAs)).

Estão instalados no computador de Olá com a sincronização do Azure AD Connect. os conectores de Olá fornecem Olá capacidade sem agente tooconverse ao utilizar protocolos de sistema remoto em vez de depender de implementação de Olá de agentes especializados. Isto significa menor risco e tempos de implementação, especialmente quando lidar com sistemas e aplicações críticas.

Imagem de Olá acima, o conector Olá é synonymous com o espaço de conector Olá mas abrange todas as comunicações com o sistema externo Olá.

Olá conector é responsável para todos os importam e exportar sistema toohello de funcionalidade e liberta os programadores necessidade toounderstand como tooconnect tooeach sistema nativamente quando utilizar transformações de dados toocustomize aprovisionamento declarativo.

Importa e exporta apenas ocorre quando agendada, permitindo ainda mais insulation de alterações a ocorrerem no sistema de Olá, uma vez que as alterações não automaticamente propagadas toohello origem de dados ligada. Além disso, os programadores também podem criar os seus próprios conectores para ligar toovirtually qualquer origem de dados.

## <a name="attribute-flow"></a>Fluxo de atributos
Olá metaverso é Olá consolidado vista de todas as identidades associados a um de circundantes espaços conectores. Na figura de Olá acima, o fluxo de atributos é descrito por linhas com arrowheads do fluxo de entrada e saída. Fluxo de atributos é o processo de Olá de copiar ou transformar dados a partir de um sistema tooanother e todos os fluxos (entrados ou saídos) de atributos.

Fluxo de atributos ocorre entre o espaço de conector Olá e Olá metaverso bidirecionalmente quando operações de sincronização (completo ou delta) são toorun agendada.

Fluxo de atributos ocorre apenas quando estes sincronizações são executadas. Fluxos de atributos são definidos nas regras de sincronização. Estes podem ser (ISR imagem Olá acima) entrada ou saída (OSR imagem Olá acima).

## <a name="connected-system"></a>Sistema ligado
Sistema ligado (também conhecido como diretório ligado) faz referência toohello sistema remoto do Azure AD Connect sincronização estabeleceu tooand leitura e escrita tooand de dados de identidade do.

## <a name="connector-space"></a>Espaço de conector
Cada origem de dados ligada é representada como um subconjunto de objetos de Olá e atributos no espaço de conector Olá filtrado.
Isto permite toooperate de serviço de sincronização de Olá localmente sem sistema remoto do Olá necessidade toocontact Olá ao sincronizar objetos Olá e restringe tooimports interação e exporta apenas.

Quando a origem de dados de Olá e conector Olá tiverem Olá capacidade tooprovide uma lista de alterações (uma importação delta), em seguida, Olá eficiência operacional aumenta significativamente como apenas as alterações desde a última consulta de Olá ciclo é trocada. espaço de conector Olá insulates origem de dados ligada Olá de alterações propagar-se automaticamente ao exigir que agenda de conector Olá importa e exportações. Este insurance adicionado concede tranquilidade durante o teste, pré-visualização ou confirmar a atualização seguinte Olá.

## <a name="metaverse"></a>Metaverso
Olá metaverso é Olá consolidado vista de todas as identidades associados a um de circundantes espaços conectores.

Como identidades ligadas em conjunto e autoridade é atribuída para vários atributos através de mapeamentos de fluxo de importação, o objeto de metaverso central Olá começa tooaggregate informações de vários sistemas. Deste fluxo de atributos de objeto, mapeamentos transportem os sistemas de toooutbound de informações.

Objetos são criados quando um sistema autoritativo projetos-los para Olá metaverso. Assim que todas as ligações são removidas, objeto de metaverso Olá é eliminado.

Objetos no metaverso Olá não podem ser editados diretamente. Todos os dados no objeto de Olá tem contribuíram através do fluxo de atributos. Olá metaverso mantém persistentes conectores com cada espaço de conector. Estes conectores não necessitam de reavaliação para cada sincronização executar. Isto significa que sincronização do Azure AD Connect não ter toolocate Olá correspondente remoto objeto sempre. Isto evita Olá necessário para agentes dispendiosas tooprevent alterações tooattributes que normalmente seriam responsável por correlacionando objetos Olá.

Quando detetar origens de dados novos que possam ter pré-existentes objetos que necessitam de toobe gerido, utiliza de sincronização do Azure AD Connect um processo chamado uma associação regra tooevaluate possíveis candidatos com que tooestablish uma ligação.
Depois de estabelecer a ligação de Olá, esta avaliação não acionador e fluxo de atributos normal pode ocorrer entre a origem de dados ligada remoto Olá e Olá metaverso.

## <a name="provisioning"></a>Aprovisionamento
Quando um projetos de origem autoritária pode ser criado um novo objeto para o metaverso de Olá um novo objeto de espaço de conector no outro conector que representa uma origem de dados ligada a jusante.

Isto inerentemente estabelece uma ligação e fluxo de atributos para poder continuar bidirecional.

Sempre que uma regra determina se um novo objeto de espaço de conector tem de toobe criado, é chamado de aprovisionamento. No entanto, porque esta operação só ocorre dentro do espaço de conector Olá, este não passa na origem de dados ligada Olá até uma exportação é executada.

## <a name="additional-resources"></a>Recursos Adicionais
* [Sincronização do Azure AD Connect: Personalizar as opções de sincronização](active-directory-aadconnectsync-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)

<!--Image references-->
[1]: ./media/active-directory-aadsync-technical-concepts/ic750598.png
