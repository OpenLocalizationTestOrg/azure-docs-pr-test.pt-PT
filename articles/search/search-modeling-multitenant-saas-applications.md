---
title: aaaModeling arquitetura "multitenancy" na Azure Search | Microsoft Docs
description: "Saiba mais sobre os padrões de conceção comuns para aplicações de SaaS multi-inquilino durante a utilização da Azure Search."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Padrões para aplicações de SaaS multi-inquilino e da Azure Search de conceção
Uma aplicação multi-inquilino é aquele que fornece Olá mesmo o número de tooany de serviços e as capacidades de inquilinos que não é possível ver ou partilhar dados Olá de qualquer outro inquilino. Este documento descreve as estratégias de isolamento de inquilino para multi-inquilino aplicações criadas com a Azure Search.

## <a name="azure-search-concepts"></a>Conceitos de pesquisa do Azure
Como uma solução de pesquisa-como-um-serviço da Azure Search permite pesquisa avançada de tooadd programadores experiências tooapplications sem qualquer infraestrutura de gestão ou se tornar um especialista na pesquisa. Os dados são carregados toohello serviço e depois armazenadas na nuvem de Olá. Utilizar toohello pedidos simples API da Azure Search, dados Olá podem, em seguida, ser modificados e pesquisados. Pode encontrar uma descrição geral do serviço de Olá [neste artigo](http://aka.ms/whatisazsearch). Antes de debater padrões de conceção, é importante toounderstand alguns conceitos na Azure Search.

### <a name="search-services-indexes-fields-and-documents"></a>Serviços de pesquisa, índices, campos e documentos
Ao utilizar a pesquisa do Azure, uma subscreve tooa *serviço de pesquisa*. Como os dados são carregado tooAzure pesquisa, são armazenados num *índice* no âmbito do serviço de pesquisa de Olá. Pode ser um número de índices dentro de um único serviço. toouse Olá familiar os conceitos das bases de dados, o serviço de pesquisa de Olá pode ser likened tooa base de dados enquanto índices Olá dentro de um serviço podem ser tootables likened dentro de uma base de dados.

Cada índice dentro de um serviço de pesquisa tem o seu próprio esquema, que é definida por um número de personalizável *campos*. Dados são adicionados tooan o índice da Azure Search no formato Olá indivíduo *documentos*. Cada documento tem de ser índice específico tooa carregado e deve encaixar-se do esquema que indexar. Quando procurar dados de utilização da Azure Search, consultas de pesquisa em texto completo Olá são emitidas em relação a um índice específico.  toocompare toothose estes conceitos de uma base de dados, campos podem ser toocolumns likened numa tabela e documentos podem ser likened toorows.

### <a name="scalability"></a>Escalabilidade
Qualquer serviço da Azure Search no Olá padrão [escalão de preço](https://azure.microsoft.com/pricing/details/search/) pode dimensionar de duas dimensões: armazenamento e disponibilidade.

* *As partições* podem ser adicionados armazenamento de Olá tooincrease de um serviço de pesquisa.
* *Réplicas* podem ser adicionados tooa serviço tooincrease Olá débito pedidos que pode processar um serviço de pesquisa.

Adicionar e remover as partições e réplicas permitirá capacidade Olá Olá toogrow de serviço de pesquisa com a quantidade de Olá de dados e o tráfego de exigências de aplicação Olá. Na ordem para um tooachieve do serviço de pesquisa, uma leitura [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), necessita de duas réplicas. Na ordem para um serviço tooachieve uma leitura e escrita [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), necessita de três réplicas.

### <a name="service-and-index-limits-in-azure-search"></a>Limites de serviço e o índice da Azure Search
Existem algumas diferentes [escalões de preço](https://azure.microsoft.com/pricing/details/search/) na Azure Search, cada um dos escalões de Olá tem diferentes [limites e quotas](search-limits-quotas-capacity.md). Alguns destes limites tenham Olá nível de serviço, alguns são ao nível de índice Olá e alguns são ao nível de partição Olá.

|  | Básica | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Réplicas máximas por serviço |3 |12 |12 |12 |12 |
| Partições máximas por serviço |1 |12 |12 |12 |1 |
| Unidades de pesquisa máximo (réplicas * partições) por serviço |3 |36 |36 |36 |36 (máximas 3 partições) |
| Documentos máximos por serviço |1 milhão |180 milhões |milhões de 720 |1.4 milhões |milhões de 600 |
| Armazenamento máximo por serviço |2GB |300 GB |1.2 TB |2.4 TB |600 GB |
| Documentos máximos por partição |1 milhão |milhões de 15 |milhões de 60 |milhões de 120 |milhões de 200 |
| Armazenamento máximo por partição |2GB |25 GB |100 GB |200 GB |200 GB |
| Índices máximos por serviço |5 |50 |200 |200 |3000 (máximo 1000 índices/partição) |

#### <a name="s3-high-density"></a>S3 Alta densidade '
No escalão de preço S3 da Azure Search, há uma opção para o modo de alta densidade (HD) Olá concebido especificamente para cenários de multi-inquilino. Em muitos casos, é necessário toosupport um grande número de inquilinos mais pequenos em vantagens de Olá de tooachieve um único serviço de eficiência de simplicidade e o custo.

S3 HD permite Olá vários índices pequeno toobe sob gestão Olá de um serviço de procura única criados pelo assiste comerciais Olá capacidade tooscale enviados os índices com partições para Olá capacidade toohost mais índices num único serviço.

Concretely, um serviço de S3 ter entre 1 e 200 índices que em conjunto, podem alojar cópias de segurança billion documentos too1.4. Um HD S3 no Olá por outro lado permitiria índices individuais tooonly aceda dos milhões documentos too1, mas pode processar dos índices too1000 por partição (cópia de segurança too3000 por serviço) com uma contagem de total de documento de milhões de 200 por partição (cópia de segurança too600 milhões por serviço).

## <a name="considerations-for-multitenant-applications"></a>Considerações para aplicações multi-inquilino
Aplicações multi-inquilino tem distribuir eficazmente recursos entre inquilinos Olá preservando algum nível de privacidade entre Olá vários inquilinos. Existem algumas considerações ao estruturar a arquitetura de Olá para uma aplicação desse tipo:

* *Isolamento de inquilinos:* tootake medidas adequadas tooensure que nenhum inquilinos tem não autorizado ou indesejável toohello de aceder aos dados de outros inquilinos tem dos programadores de aplicações. Para além da perspetiva de Olá de privacidade dos dados, estratégias de isolamento de inquilino necessitam de uma gestão eficaz da proteção de vizinhos inúteis e de recursos partilhados.
* *Custo de recursos de nuvem:* como com qualquer outra aplicação, as soluções de software têm de permanecer custo competitiva como um componente de uma aplicação multi-inquilino.
* *Facilidade de operações:* quando desenvolver uma arquitetura multi-inquilino, Olá impacto nas operações da aplicação Olá e complexidade é uma consideração importante. A pesquisa do Azure tem um [SLA de 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Requisitos de espaço global:* aplicações multi-inquilino, poderão ter tooeffectively servirem inquilinos que estão distribuídos globo Olá.
* *Escalabilidade:* os programadores de aplicações têm de tooconsider como de reconciliar entre manter um nível de complexidade de aplicação suficientemente baixa e estruturar Olá tooscale de aplicação com o número de inquilinos e Olá tamanho dos dados dos inquilinos e carga de trabalho.

A Azure Search oferece limites alguns que podem ser dados dos inquilinos tooisolate utilizados e a carga de trabalho.

## <a name="modeling-multitenancy-with-azure-search"></a>Modelação de arquitetura "multitenancy" com a pesquisa do Azure
No caso de Olá de um cenário de multi-inquilino, o programador da aplicação Olá consome um ou mais serviços de pesquisa e dividir os seus inquilinos entre serviços, índices ou ambos. A pesquisa do Azure tem alguns padrões comuns quando um cenário de multi-inquilino de modelação:

1. *Índice por inquilino:* cada inquilino tem a suas próprias índice dentro de um serviço de pesquisa que é partilhado com outros inquilinos.
2. *Serviço por inquilino:* cada inquilino tem o seu próprio serviço de pesquisa do Azure dedicada, oferta nível mais elevado de separação de dados e a carga de trabalho.
3. *A combinação de ambos:* inquilinos maiores e mais-Active Directory estão atribuídos serviços dedicados enquanto inquilinos mais pequenos são atribuídos índices individuais dentro de serviços partilhados.

## <a name="1-index-per-tenant"></a>1. Índice por inquilino
![Um portrayal do modelo de índice por inquilino Olá](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

Um modelo de índice por inquilino, vários inquilinos ocupam um único serviço de pesquisa do Azure onde cada inquilino tem os seus próprios índice.

Os inquilinos alcançarem isolamento de dados, uma vez que todos os pedidos de pesquisa e operações de documento são emitidas um nível de índice da Azure Search. Na camada da aplicação Olá, há deteção necessidade de Olá toodirect Olá índices adequada de toohello do tráfego de vários inquilinos, enquanto também gere recursos ao nível de serviço Olá em todos os inquilinos.

Um atributo chave do modelo de índice por inquilino Olá é a capacidade de Olá para a capacidade Olá toooversubscribe de Programador de aplicações de Olá de um serviço de pesquisa entre inquilinos da aplicação Olá. Se tem de inquilinos Olá uma distribuição desigual da carga de trabalho, combinação ideal de Olá de inquilinos pode ser distribuídas por um serviço de pesquisa indexa tooaccommodate um número de inquilinos altamente Active Directory, consome enquanto processa em simultâneo uma cauda longa do inquilinos menos ativos. compromisso de Olá é a impossibilidade de Olá situações Olá modelo toohandle onde cada inquilino seja o simultaneamente altamente Active Directory.

modelo de índice por inquilino Olá fornece a base de Olá para um modelo de custo de variável, onde um todo o serviço da Azure Search é comprou prévio e, em seguida, subsequentemente, preenchida com inquilinos. Isto permite toobe de capacidade não utilizada designado para as avaliações e as contas gratuitas.

Para aplicações com um requisitos de espaço global, o modelo de índice por inquilino Olá não pode ser Olá mais eficiente. Se os inquilinos de uma aplicação estão distribuídos globo Olá, um serviço separado poderá ser necessário para cada região que pode duplicar os custos em cada um deles.

A pesquisa do Azure permite a escala de Olá de índices individuais Olá e o número total de Olá de toogrow de índices. Se um preço adequado camada é escolhido, partições e réplicas podem ser adicionadas toohello o serviço de pesquisa completa quando um índice individuais no âmbito do serviço de Olá ficar demasiado grande em termos de armazenamento ou de tráfego.

Se o número total de Olá dos índices ficar demasiado grande para um único serviço, o serviço de outro tem tooaccommodate toobe aprovisionado Olá novos inquilinos. Se índices tiverem toobe movido entre serviços de pesquisa, à medida que são adicionados novos serviços, dados de Olá desde o índice de Olá tem toobe manualmente copiada de um índice toohello outras como toobe um índice movida não permite a pesquisa do Azure.

## <a name="2-service-per-tenant"></a>2. Serviço por inquilino
![Um portrayal do modelo de serviço por inquilino Olá](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

Numa arquitetura por-inquilino de serviço, cada inquilino tem o seu próprio serviço de pesquisa.

Neste modelo, a aplicação Olá distribui nível máximo de Olá de isolamento para os seus inquilinos. Cada serviço tem dedicada de armazenamento e débito para processar o pedido de pesquisa, bem como as chaves de API separadas.

Para aplicações onde cada inquilino tem requisitos de espaço de grandes dimensões ou carga de trabalho Olá tem pouco variabilidade do inquilino tootenant, modelo de serviço por inquilino Olá é uma opção efetiva como recursos não são partilhados entre as cargas de trabalho de vários inquilinos.

Um serviço por modelo de inquilino também oferece o benefício de Olá de um modelo de custo previsível, fixos. Há um investimento prévio num serviço de pesquisa de todo, até um toofill de inquilino, no entanto Olá custo por inquilino é superior a um modelo de índice por inquilino.

modelo de serviço por inquilino Olá é uma escolha eficiente para aplicações com um requisitos de espaço global. Com inquilinos distribuída geograficamente, é fácil toohave serviço cada inquilino na região adequado Olá.

desafios de Olá Dimensionar este padrão surgem quando individuais inquilinos outgrow o seu serviço. A pesquisa do Azure não suporta atualmente a atualizar Olá camada de um serviço de pesquisa de preços para que todos os dados teria toobe copiado manualmente tooa novo serviço.

## <a name="3-mixing-both-models"></a>3. A combinação de ambos os modelos
Outro padrão para a modelação de arquitetura "multitenancy" é a combinação de estratégias de índice por inquilino e serviço por inquilino.

Ao combinar padrões de Olá dois, inquilinos maiores de uma aplicação podem ocupam serviços dedicados enquanto Olá longa seguimento de menos Active Directory, mais pequenos de inquilinos pode ocupam índices num serviço partilhado. Este modelo assegura que inquilinos maiores Olá têm consistentemente elevado desempenho do serviço de Olá ajudando tooprotect Olá inquilinos inferior de qualquer vizinhos inúteis.

No entanto, implementar esta estratégia baseia-se prospeção no prever que os inquilinos necessitam de um serviço dedicada versus um índice num serviço partilhado. Aumenta a complexidade de aplicação com Olá necessidade toomanage ambas destes modelos de arquitetura "multitenancy".

## <a name="achieving-even-finer-granularity"></a>Alcançar granularidade mesmo melhorar
Olá acima cenários multi-inquilino do toomodel de padrões de conceção da Azure Search partem do princípio de um âmbito uniform onde cada inquilino seja uma instância completa de uma aplicação. No entanto, as aplicações, por vezes, podem processar vários âmbitos mais pequenos.

Se os modelos de serviço por inquilino e índice por inquilino não são suficientemente pequenos âmbitos, é possível toomodel tooachieve um índice um grau mesmo melhorar de granularidade.

toohave num índice único comportar-se de forma diferente de pontos finais de cliente diferente, um campo pode ser adicionado tooan índice que designa um determinado valor para cada cliente possíveis. Sempre que um cliente chama tooquery de pesquisa do Azure ou modificar um índice, código Olá da aplicação de cliente Olá Especifica o valor adequado de Olá para esse campo através da Azure Search [filtro](https://msdn.microsoft.com/library/azure/dn798921.aspx) capacidade no momento da consulta.

Este método pode ser tooachieve utilizado a funcionalidade de contas de utilizador em separado, níveis de permissão separada e até mesmo completamente independente aplicações.

> [!NOTE]
> Utilizar a abordagem de Olá descrito acima tooconfigure tooserve um único índice relevância de Olá do inquilinos afeta várias dos resultados da pesquisa. Pesquisa relevância pontuações são calculadas um âmbito de nível de índice, não é um âmbito de nível de inquilino, para que os dados de todos os inquilinos incorporados nas estatísticas de subjacente dos pontuações relevância Olá, tais como a frequência de prazo.
> 
> 

## <a name="next-steps"></a>Passos seguintes
A pesquisa do Azure é uma escolha apelativa para muitas aplicações, [ler mais sobre as capacidades do serviço de Olá robustas](http://aka.ms/whatisazsearch). Quando avaliar Olá várias padrões para aplicações multi-inquilino de conceção, considere Olá [vários escalões de preços](https://azure.microsoft.com/pricing/details/search/) e respetiva Olá [os limites de serviço](search-limits-quotas-capacity.md) toobest personalizar toofit de pesquisa do Azure e arquiteturas de todos os tamanhos de cargas de trabalho da aplicação.

Quaisquer perguntas sobre a Azure Search e cenários de multi-inquilino podem ser direcionadas tooazuresearch_contact@microsoft.com.

