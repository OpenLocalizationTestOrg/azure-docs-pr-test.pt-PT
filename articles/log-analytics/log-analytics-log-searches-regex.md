---
title: "pesquisas de registo de expressões de aaaRegular na análise de registos do OMS | Microsoft Docs"
description: "Pode utilizar a palavra-chave RegEx de Olá na análise de registos registo pesquisas toohello Olá resultados do filtro de acordo com tooa de expressão regular.  Este artigo fornece sintaxe Olá para estas expressões com vários exemplos."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>Registo utilizando expressões regulares toofilter procura na análise de registos

[Inicie sessão pesquisas](log-analytics-log-searches.md) permitem-lhe informações tooextract do repositório de análise de registos de Olá.  [Expressões de filtro](log-analytics-search-reference.md#filter-expressions) permitem-lhe resultados de Olá toofilter da pesquisa de Olá toospecific critérios de acordo com.  Olá **RegEx** palavra-chave permite-lhe toospecify uma expressão regular para o filtro.  

Este artigo fornece detalhes sobre a sintaxe de expressão regular Olá utilizado pela análise de registos.

> [!NOTE]
> Só pode utilizar o RegEx com campos pesquisáveis.  Para obter mais informações sobre campos pesquisáveis, consulte **tipos de campo** no [localizar dados através de pesquisas de registo na análise de registos](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>Palavra-chave do RegEx

Olá de utilização seguintes Olá de toouse sintaxe **RegEx** palavra-chave na pesquisa de registo.  Pode utilizar Olá noutras secções na sintaxe de Olá artigo toodetermine Olá regular própria expressão.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Por exemplo, um alerta de tooreturn de expressão regular de toouse regista com um tipo de *aviso* ou *erro*, teria de utilizar Olá seguir pesquisa de registo.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Correspondências parciais
Tenha em atenção que expressão regular Olá tem de corresponder ao texto completo de Olá da propriedade Olá.  Correspondências parciais não irão devolver quaisquer registos.  Por exemplo, se foram tentar tooreturn registos de um computador com o nome srv01.contoso.com, Olá seguir pesquisa registo seria **não** devolver quaisquer registos.

    Computer=RegEx("srv..")

Isto acontece porque apenas Olá primeira parte do nome de Olá corresponde à expressão regular Olá.  Olá pesquisas de registo de dois seguintes devolvam registos deste computador porque que corresponde ao nome completo Olá.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Carateres
Especifique outros carateres.

| Caráter | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| A | Uma ocorrência do caráter Olá. | Computer=RegEx("Srv01.contoso.com") | Srv01.contoso.com |
| . | Um único caráter. | Computer=RegEx("SRV...contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| um? | Zero ou uma ocorrência do caráter Olá. | Computador = RegEx ("srv01?. contoso.com") | srv0.contoso.com<br>Srv01.contoso.com |
| um * | Zero ou mais ocorrências do caráter Olá. | Computer=RegEx("Srv01*.contoso.com") | srv0.contoso.com<br>Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| um + | Um ou mais ocorrências do caráter Olá. | Computer=RegEx("Srv01+.contoso.com") | Srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Corresponder a um único caráter entre parênteses Retos Olá | Computer=RegEx("srv0[123].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [*um*-*z*] | Corresponde a um único caráter no intervalo de Olá.  Pode incluir vários intervalos. | Computer=RegEx("srv0[1-3].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Nenhum dos carateres Olá entre parênteses Retos Olá | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [^*um*-*z*] | Nenhum dos carateres Olá no intervalo de Olá. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>SRV06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Corresponde a um intervalo de carateres numéricos. | Computer=RegEx("SRV[01-03].contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |
| @ | Qualquer cadeia de carateres. | Computador = RegEx ("srv@.contoso.com") | Srv01.contoso.com<br>SRV02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Vários occurences do caráter
Especifique as múltiplas ocorrências de um determinado carateres.

| Caráter | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| {n} |  *n*ocorrências do caráter Olá. | Computer=RegEx("BW-Win-sc01{3}.bwren.Lab") | BW-win-sc0111.bwren.lab |
| {n} |  *n*ou mais ocorrências do caráter Olá. | Computer=RegEx("BW-Win-sc01{3,}.bwren.Lab") | BW-win-sc0111.bwren.lab<br>BW-win-sc01111.bwren.lab<br>BW-win-sc011111.bwren.lab<br>BW-win-sc0111111.bwren.lab |
| {n, m} |  *n*demasiado*m* ocorrências do caráter Olá. | Computer=RegEx("BW-Win-sc01{3,5}.bwren.Lab") | BW-win-sc0111.bwren.lab<br>BW-win-sc01111.bwren.lab<br>BW-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Expressões lógicas
Selecione a partir de vários valores.

| Caráter | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| &#124; | OU lógico.  Devolve o resultado se corresponder a expressão. | Tipo = AlertSeverity alerta = RegEx ("aviso &#124; Erro") | Aviso<br>Erro |
| & | AND. lógica  Devolve o resultado se correspondem em ambas as expressões | EventData = regex ("(segurança.\* &. \*com êxito. \*)") | Segurança de auditoria com êxito |


## <a name="literals"></a>Literais
Converta carateres de tooliteral carateres especiais.  Isto inclui carateres que fornecem funcionalidades tooregular expressões como?-\*^\[\]{}\(\)+\|. &.

| Caráter | Descrição | Exemplo | Correspondências de exemplo |
|:--|:--|:--|:--|
| \\ | Converte um literal de tooa caráter especial. | Status_CF =\\[erro\\] @<br>Status_CF = erro\\-@ | [Erro] Ficheiro não encontrado.<br>Ficheiro de erros não encontrado. |


## <a name="next-steps"></a>Passos Seguintes

* Familiarizar com [pesquisas de registo](log-analytics-log-searches.md) tooview e analisar dados no repositório de análise de registos de Olá.
