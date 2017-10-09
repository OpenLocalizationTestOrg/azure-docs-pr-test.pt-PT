---
title: "Azure AD Connect: Noções sobre aprovisionamento declarativo | Microsoft Docs"
description: "Explica Olá declarativa aprovisionamento modelo de configuração no Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Sincronização do Azure AD Connect: Noções sobre o aprovisionamento declarativo
Este tópico explica o modelo de configuração de Olá no Azure AD Connect. modelo de Olá é chamado aprovisionamento declarativo e permite-lhe toomake uma alteração de configuração com facilidade. Inúmeros aspetos descritos neste tópico estão avançados e não é necessário para a maioria dos cenários de cliente.

## <a name="overview"></a>Descrição geral
Aprovisionamento declarativo processamento objetos feitos um diretório de origem ligado e determina como devem ser transformados objeto Olá e atributos de um destino de tooa de origem. Um objeto é processado num pipeline sincronização e pipeline Olá é Olá mesmo para as regras de entrada e saídas. Uma regra de entrada provém de um metaverso de toohello de espaço de conector e uma regra de saída é a partir do espaço de conector Olá metaverso tooa.

![Pipeline de sincronização](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

pipeline de Olá tem vários módulos diferentes. Cada um deles é responsável por um conceito na sincronização de objetos.

![Pipeline de sincronização](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Origem de objeto de origem Olá
* [Âmbito](#scope), localiza todas as regras de sincronização que se encontrem no âmbito
* [Associar](#join), determina a relação entre o metaverso e espaço de conector
* [Transformar](#transform), Calculates como atributos devem ser transformados e fluxo
* [Precedência](#precedence), resolve em conflito contribuições de atributo
* Destino, o objeto de destino Olá

## <a name="scope"></a>Âmbito
módulo de âmbito de Olá está a avaliar um objeto e determina as regras de Olá que estejam no âmbito e devem ser incluídas no processamento de Olá. Dependendo de valores de atributos de Olá no objeto de Olá, regras de sincronização diferentes são avaliada toobe no âmbito. Por exemplo, um utilizador desativado com nenhuma caixa de correio do Exchange tem regras diferentes do que um utilizador ativado com uma caixa de correio.  
![Âmbito](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

âmbito de Olá está definido como grupos e cláusulas. cláusulas Olá estão dentro de um grupo. É utilizado um e lógica entre todas as cláusulas num grupo. Por exemplo, (departamento de TI e país de = = Dinamarca). É utilizado ou entre grupos.

![Âmbito](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
âmbito de Olá nesta imagem deve ser lido como (departamento de TI e país de = = Dinamarca) ou (país = Suécia). Se o grupo de 1 ou 2 é avaliada tootrue, regra Olá está no âmbito.

módulo de âmbito de Olá suporta Olá seguintes operações.

| Operação | Descrição |
| --- | --- |
| IGUAL, NOTEQUAL |Comparar uma cadeia que avalia se o valor for igual toohello no atributo Olá. Para atributos com múltiplos valores, consulte ISIN e ISNOTIN. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Comparar uma cadeia que avalia se o valor for less than do valor de Olá do atributo de Olá. |
| CONTÉM, NOTCONTAINS |Comparar uma cadeia que avalia se o valor pode ser encontrado algures no valor do atributo de Olá. |
| STARTSWITH, NOTSTARTSWITH |Comparar uma cadeia que avalia se o valor está no início de Olá do valor de Olá do atributo de Olá. |
| ENDSWITH, NOTENDSWITH |Comparar uma cadeia que avalia se o valor está no final de Olá do valor de Olá do atributo de Olá. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Comparar uma cadeia que avalia se o valor é superior do valor de Olá do atributo de Olá. |
| ISNULL, ISNOTNULL |Avalia se atributo Olá está ausente do objeto de Olá. Atributo de Olá não está presente e, por conseguinte, null, em seguida, regra Olá estiver no âmbito. |
| ISIN, ISNOTIN |Avalia se o valor de Olá está presente no atributo Olá definido. Esta operação é variação com múltiplos valores de Olá de igual e NOTEQUAL. atributo de Olá deveria toobe um atributo com múltiplos valor e se o valor de Olá pode ser encontrado em nenhum dos valores de atributo Olá, em seguida, regra Olá se encontra no âmbito. |
| ISBITSET, ISNOTBITSET |Avalia se um determinado bit estiver definido. Por exemplo, pode ser utilizado tooevaluate Olá bits no userAccountControl toosee se um utilizador está ativado ou desativado. |
| ISMEMBEROF, ISNOTMEMBEROF |valor de Olá deve conter um grupo de tooa DN no espaço de conector Olá. Se o objeto de Olá é um membro do grupo de Olá especificado, a regra de Olá se encontra no âmbito. |

## <a name="join"></a>Associar
módulo de associação de Olá no pipeline de sincronização de Olá é responsável por localizar a relação de Olá entre objeto Olá na origem de Olá e um objeto no destino Olá. Uma regra de entrada, esta relação seria um objeto num espaço de conector localizar um objeto de tooan de relação no metaverso Olá.  
![Associar entre cs e mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
objetivo Olá toosee se já houver um objeto no metaverso Olá, criado por outro conector, deve ser associado. Por exemplo, num recurso de conta de utilizador de Olá floresta da floresta de contas de Olá deve ser associado com utilizador Olá da floresta de recursos de Olá.

Associações são utilizadas principalmente em regras de entrada toojoin conector espaço objetos em conjunto toohello mesmo objeto de metaverso.

associações de Olá são definidas como um ou mais grupos. Dentro de um grupo, terá de cláusulas. É utilizado um e lógica entre todas as cláusulas num grupo. É utilizado ou entre grupos. grupos de Olá são processados por ordem de toobottom superior. Quando um grupo encontrou exatamente uma correspondência com um objeto no destino Olá, não existem outras regras de associação são avaliadas. Se zero ou mais do que é possível localizar um objeto, o processamento continua toohello grupo seguinte de regras. Por este motivo, as regras de Olá devem ser criadas na ordem Olá mais explícito primeiro e mais difusa no fim de Olá.  
![Definição de associação](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
associações de Olá nesta imagem são processadas de toobottom superior. Primeiro pipeline de sincronização de Olá verá se houver uma correspondência no campo IDdeEmpregado. Caso contrário, a segunda regra de Olá vê se o nome da conta Olá pode ser utilizados toojoin Olá objetos em conjunto. Se isto não for uma correspondência ou, Olá terceira e final de regras é uma correspondência mais difusa utilizando Olá nome de utilizador.

Se todas as regras de associação foram avaliadas e não existe não é exatamente uma correspondência, Olá **tipo de ligação** no Olá **Descrição** página é utilizada. Se esta opção estiver definida demasiado**aprovisionar**, em seguida, é criado um novo objeto no destino Olá.  
![Aprovisionar ou uma associação](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Um objeto deve ter apenas uma regra de sincronização único com regras de associação no âmbito. Se existirem várias regras de Sincronização quais está definida a associação, ocorre um erro. Precedência não é utilizado tooresolve conflitos de associação. Um objeto tem de ter uma regra de associação no âmbito de atributos tooflow com Olá mesma direção de entrada/saída. Se precisar de tooflow atributos de entrada e saída toohello mesmo objeto, tem de ter uma entrada e uma regra de sincronização de saída com associação.

Associação de saída tem um comportamento especial quando este tenta tooprovision um espaço de conector do objeto tooa destino. o atributo de Olá DN é utilizado toofirst tente uma associação inversa. Se já existir um objeto no espaço de conector de destino Olá com Olá DN mesmo, Olá objetos estão associados.

módulo de associação de Olá é avaliado apenas uma vez quando uma nova regra de sincronização é fornecido no âmbito. Quando tiver associado um objeto, não é disjoining, mesmo se os critérios de associação de Olá já não é satisfeita. Se quiser toodisjoin um objeto, regra de sincronização de Olá associados a objetos de Olá fique fora do âmbito.

### <a name="metaverse-delete"></a>Eliminação de Metaverso
Um objeto de metaverso permanece desde que não há uma regra de sincronização no âmbito com **tipo de ligação** definido demasiado**aprovisionar** ou **StickyJoin**. Um StickyJoin é utilizado quando um conector não é permitido tooprovision um novo objeto de metaverso toohello, mas quando foi associado, tem de ser eliminado na origem de Olá antes do objeto de metaverso Olá é eliminado.

Quando é eliminado um objeto de metaverso, todos os objetos associados uma regra de sincronização de saída marcado para **aprovisionar** estão marcados para um eliminar.

## <a name="transformations"></a>Transformações
transformações de Olá são toodefine utilizado como atributos devem fluxo a partir do destino de toohello Olá origem. Olá fluxos podem ter um dos seguintes Olá **fluxo tipos**: direta, constante ou expressão. Um valor de atributo como flui de um fluxo direto,-é com nenhuma transformações adicionais. Olá de define um valor constante valor especificado. Uma expressão utiliza Olá declarativa aprovisionamento expressão idioma tooexpress como transformação Olá deve ser. Olá detalhes para o idioma de expressão Olá pode ser encontrado na Olá [compreender o idioma de expressão de aprovisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) tópico.

![Aprovisionar ou uma associação](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Olá **aplicar uma vez** caixa de verificação define que Olá atributo só deve ser definido quando o objeto de Olá for criado inicialmente. Por exemplo, esta configuração pode ser utilizado tooset uma palavra-passe inicial para um novo objeto de utilizador.

### <a name="merging-attribute-values"></a>A intercalação de valores de atributo
Em fluxos de atributos de Olá é uma definição toodetermine se atributos com múltiplos valores devem ser intercalados de vários conectores diferentes. valor predefinido de Olá é **atualização**, que indica que regra de sincronização Olá com precedência mais elevada deve win.

![Tipos de intercalação](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Há também **intercalar** e **MergeCaseInsensitive**. Estas opções permitem toomerge valores de diferentes origens. Por exemplo, pode ser utilizado toomerge Olá membro proxyAddresses atributo ou de várias florestas diferentes. Quando utiliza esta opção, sincronizar todas as regras no âmbito para um objecto têm de utilizar Olá mesmo tipo de intercalação. Não é possível definir **atualização** de um conector e **intercalar** de outro. Se tentar, receberá um erro.

Olá diferença entre **intercalar** e **MergeCaseInsensitive** é como tooprocess duplicado valores de atributo. o motor de sincronização de Olá certifica-se de valores duplicados não estão a ser introduzidos no atributo de destino Olá. Com **MergeCaseInsensitive**, valores com apenas uma diferença de duplicados, no caso de não vai toobe presente. Por exemplo, não verá ambos "SMTP:bob@contoso.com"e"smtp:bob@contoso.com" do atributo de destino Olá. **Intercalar** é apenas observar valores exato Olá e vários valores onde existe apenas uma diferença nos casos poderão estar presente.

Olá opção **substituir** é Olá igual **atualização**, mas não está a ser utilizada.

### <a name="control-hello-attribute-flow-process"></a>Processo de fluxo de atributo do controlo Olá
Quando várias regras de sincronização de entrada estão configuradas toocontribute toohello mesmo atributo de metaverso e precedência é winner de Olá toodetermine utilizados. regra de sincronização de Olá com precedência mais elevada (menor valor numérico) vai valor de Olá toocontribute. Olá que mesmo acontece para regras de saída. regra de sincronização de Olá com precedência mais elevada wins e contribuir Olá toohello de valor diretório ligado.

Em alguns casos, em vez de um valor, a contribuir regra de sincronização de Olá deve determinar a forma como devem comportar-se outras regras. Existem algumas especial os literais que são utilizados para este cenário.

Para as regras de sincronização de entrada, Olá literal **nulo** podem ser utilizado tooindicate que o fluxo de Olá não tem toocontribute nenhum valor. Outra regra com precedência inferior pode contribuir um valor. Se nenhuma regra contribuíram um valor, atributo do metaverso Olá é removido. Para uma regra de saída, se **nulo** é valor final Olá depois de todas as regras de sincronização tem sido processadas, em seguida, o valor de Olá é removido no diretório ligado Olá.

Olá literal **AuthoritativeNull** é semelhante demasiado**nulo** mas com uma diferença Olá que não existem regras de precedência inferiores podem contribuir um valor.

Também pode utilizar um fluxo de atributos **IgnoreThisFlow**. É semelhante tooNULL no sentido de Olá que indica não há nada toocontribute. diferença de Olá é que não remove um valor já existente no destino Olá. É, tal como o fluxo de atributos de Olá nunca foi não existe.

Segue-se um exemplo:

No *saída tooAD - híbrida do Exchange do utilizador* Olá seguir fluxo pode ser encontrado:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Esta expressão deve ser lido como: se a caixa de correio do Olá utilizador estiver localizada no Azure AD, em seguida, fluxo de atributos de Olá de tooAD do Azure AD. Se não, não flua tooActive qualquer caráter back diretório. Neste caso,-manteria valor existente Olá no AD.

### <a name="importedvalue"></a>ImportedValue
a função de Olá ImportedValue é diferente de todas as outras funções, uma vez que o nome do atributo Olá deve estar entre aspas, em vez de parênteses Retos:  
`ImportedValue("proxyAddresses")`.

Normalmente durante a sincronização um atributo utiliza valor esperado de Olá, mesmo se ainda não foram exportado ainda ou foi recebido um erro durante a exportação ("parte superior da Torre de Olá"). Uma sincronização de entrada parte do princípio de que um atributo que ainda não chegaram, eventualmente, um diretório ligado atinja o. Em alguns casos, é importante tooonly sincronizar um valor que foi confirmado por Olá diretório ligado ("holograma e diferenças importar Torre").

Um exemplo desta função pode ser encontrado na Olá out-of-box regra de sincronização *do AD – utilizador comuns do Exchange*. No Exchange híbrida, valor de Olá adicionado pelo Exchange online apenas deve ser sincronizado quando confirmado de que o valor de Olá foi exportada com êxito:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Precedência
Quando várias regras de sincronização tentam toocontribute Olá mesmo destino de toohello de valor de atributo, valor de precedência de Olá winner de Olá toodetermine utilizados. regra de Olá com precedência mais elevada, mais baixa valor numérico, vai atributo de Olá toocontribute num conflito.

![Tipos de intercalação](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Esta ordem pode ser utilizado toodefine mais precisas fluxos para um pequeno subconjunto de objetos de atributos. Por exemplo, Olá fora-de-caixa-regras Certifique-se de que atributos a partir de uma conta ativada (**utilizador AccountEnabled**) têm precedência de outras contas.

Precedência pode ser definida entre os conectores. Que permite que os conectores com valores de toocontribute melhor dados pela primeira vez.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Olá, vários objetos do mesmo espaço de conector
Se tiver vários objetos em Olá conector mesmo espaço toohello associado ao objeto de metaverso mesmo, tem de ser ajustada precedência. Se vários objetos se encontram no âmbito de Olá mesma regra de sincronização, em seguida, o motor de sincronização de Olá não é possível toodetermine precedência. É ambígua o objeto de origem deve contribuir Olá valor toohello metaverso. Esta configuração é reportada como ambígua mesmo atributos Olá origem Olá têm Olá mesmo valor.  
![Vários objetos associados a um toohello mesmo objeto de mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

Para este cenário, terá de âmbito de Olá toochange de regras de sincronização de Olá, para que objetos de origem Olá tem regras de sincronização diferentes no âmbito. Que permite-lhe toodefine precedência de diferentes.  
![Vários objetos associados a um toohello mesmo objeto de mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre o idioma de expressão Olá no [expressões compreender de aprovisionamento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Consulte como declarativa de aprovisionamento é utilizado out-of-box no [configuração predefinida do compreender Olá](active-directory-aadconnectsync-understanding-default-configuration.md).
* Veja como toomake um práticos alterados utilizando o aprovisionamento declarativo no [como toomake toohello uma alteração predefinido configuração](active-directory-aadconnectsync-change-the-configuration.md).
* Continuar tooread como utilizadores e contactos trabalham em conjunto [entender utilizadores e contactos](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Tópicos de descrição geral**

* [Sincronização do Azure AD Connect: Noções e personalizar a sincronização](active-directory-aadconnectsync-whatis.md)
* [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md)

**Tópicos de referência**

* [Sincronização do Azure AD Connect: referência de funções](active-directory-aadconnectsync-functions-reference.md)
