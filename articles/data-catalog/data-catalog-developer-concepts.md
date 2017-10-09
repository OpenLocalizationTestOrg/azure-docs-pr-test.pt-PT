---
title: "conceitos do programador aaaData catálogo | Microsoft Docs"
description: "Introdução toohello conceitos-chave no modelo conceptual do catálogo de dados do Azure, exposto através de Olá API REST do catálogo."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Conceitos do Programador de catálogo de dados do Azure
Microsoft **catálogo de dados do Azure** é um serviço em nuvem completamente gerido que fornece capacidades de deteção de origem de dados e para fazer crowdsourcing de metadados de origem de dados. Os programadores podem utilizar o serviço de Olá através das respetivas APIs REST. Noções sobre conceitos Olá implementados no serviço de Olá é importante para os programadores que integram toosuccessfully **catálogo de dados do Azure**.

## <a name="key-concepts"></a>Conceitos-chave
Olá **catálogo de dados do Azure** modelo concetual baseia-se em quatro conceitos chave: Olá **catálogo**, **utilizadores**, **ativos**e **Anotações**.

![Conceito][1]

*Figura 1 - modelo concetual simplificada de catálogo de dados do Azure*

### <a name="catalog"></a>Catálogo
A **catálogo** é o contentor de nível superior de Olá para todos os Olá metadados armazena uma organização. Há um **catálogo** permitido por conta do Azure. Catálogos são associada tooan subscrição do Azure, mas apenas um **catálogo** podem ser criados para qualquer conta do Azure especificada, apesar de uma conta pode ter várias subscrições.

Contém um catálogo **utilizadores** e **ativos**.

### <a name="users"></a>Utilizadores
Os utilizadores são os principais de segurança que têm permissões tooperform ações (pesquisar o catálogo de Olá, adicionar, editar ou remover itens, etc.) na Olá catálogo.

Existem várias funções diferentes que pode ter um utilizador. Para informações sobre as funções, consulte a secção de Olá funções e a autorização.

Utilizadores individuais e grupos de segurança podem ser adicionados.

Catálogo de dados do Azure utiliza o Azure Active Directory para gestão de identidades e acesso. Cada utilizador de catálogo tem de ser um membro de Olá do Active Directory para a conta de Olá.

### <a name="assets"></a>Elementos
A **catálogo** contém recursos de dados. **Ativos** são unidade Olá de gerido pelo catálogo Olá de granularidade.

granularidade de Olá de um ativo varia de acordo com a origem de dados. Para SQL Server ou base de dados Oracle, um recurso pode ser uma tabela ou numa vista. Para SQL Server Analysis Services, um recurso pode ser uma medida, uma dimensão ou um indicador chave de desempenho (KPI). Para SQL Server Reporting Services, um recurso é um relatório.

Um **Asset** é coisa Olá adicionar ou remover um catálogo. É unidade Olá do resultado voltar de **pesquisa**.

Um **Asset** é efetuada cópia de segurança do respetivo nome, localização e tipo e anotações mais descrevem-lo.

### <a name="annotations"></a>Anotações
As anotações são itens que representam os metadados sobre recursos.

Exemplos de anotações são descrição, etiquetas, esquema, documentação, etc. Uma lista completa dos tipos de recurso de Olá e tipos de anotação são Olá secção de modelo de objeto de recurso.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Crowdsourcing anotações e perspetiva do utilizador (multiplicidade da opinião)
Um aspeto chave do catálogo de dados do Azure é como suporta Olá crowdsourcing de metadados no sistema de Olá. Como tooa oposição ao wiki abordagem – onde há apenas um opinião e Olá wins escritor último – modelo de catálogo de dados do Azure Olá permite vários opinions toolive lado no sistema de Olá.

Esta abordagem reflete Olá mundo real dos dados empresariais quais diferentes utilizadores podem ter diferentes perspetivas sobre um determinado recurso:

* Um administrador da base de dados pode fornecer informações sobre contratos de nível de serviço ou a janela de processamento disponíveis Olá para operações de ETL em massa
* Um steward de dados pode fornecer informações sobre o recurso de Olá de toowhich de processos de negócio de Olá aplicam-se ou classificações Olá Olá negócio tenha aplicada tooit
* Um analista do departamento financeiro pode fornecer informações sobre como os dados de Olá são utilizados durante o fim do período tarefas relatórios

toosupport neste exemplo, cada utilizador – Olá DBA, steward de dados de Olá e analista Olá – pode adicionar uma descrição tooa única tabela que foi registada no Olá catálogo. Todas as descrições são mantidas no sistema de Olá e, no portal do catálogo de dados do Azure de Olá todas as descrições são apresentadas.

Este padrão está aplicado toomost Olá de itens de no modelo de objeto Olá, pelo que os tipos de objeto no payload JSON de Olá são, muitas vezes, matrizes de propriedades onde poderá esperar um singleton.

Por exemplo, sob o elemento de Olá raiz é uma matriz de objetos de descrição. propriedade de matriz Olá é denominada "descrições". Um objeto de descrição tem uma propriedade - descrição. padrão de Olá é que cada utilizador que descrição tipos obtém um objeto de descrição criados para o valor de Olá fornecido pelo utilizador Olá.

Olá UX, em seguida, pode escolher como toodisplay Olá combinação. Existem três padrões diferentes para apresentação.

* padrão de mais simples de Olá é "Mostrar tudo". Neste padrão, são apresentados todos os objetos de Olá numa vista de lista. portal do catálogo de dados do Azure de Olá UX utiliza este padrão para a descrição.
* Padrão de outra é "Merge". Neste padrão, em conjunto, todos os valores de Olá dos utilizadores de diferentes Olá são intercalados com os duplicados removidos. Os exemplos deste padrão no portal do catálogo de dados do Azure de Olá UX são propriedades de etiquetas e especialistas de Olá.
* Um terceiro padrão é "último wins de escritor". Neste padrão, é apresentado apenas Olá valor mais recente digitado. friendlyName é um exemplo deste padrão.

## <a name="asset-object-model"></a>Modelo de objeto de elemento
Conforme apresentado na secção de conceitos chave Olá, Olá **catálogo de dados do Azure** modelo de objetos incluem itens, o que podem ser ativos ou anotações. Itens têm propriedades, o que podem ser necessária ou opcional. Algumas propriedades aplicam tooall itens. Algumas propriedades aplicam tooall ativos. Algumas propriedades aplicam toospecific apenas os tipos de recurso.

### <a name="system-properties"></a>Propriedades do sistema
<table><tr><td><b>Nome da propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr><tr><td>carimbo de data/hora</td><td>DateTime</td><td>Olá último tempo Olá item foi modificado. Este campo é gerado pelo servidor Olá quando um item é inserido e sempre que um item é atualizado. Olá valor desta propriedade é ignorada na entrada de publicar operações.</td></tr><tr><td>ID</td><td>URI</td><td>Url absoluto do item de Olá (só de leitura). É Olá URI endereçável exclusivo para o item de Olá.  Olá valor desta propriedade é ignorada na entrada de publicar operações.</td></tr><tr><td>tipo</td><td>Cadeia</td><td>tipo de Olá do recurso de Olá (só de leitura).</td></tr><tr><td>ETag</td><td>Cadeia</td><td>Uma cadeia toohello versão correspondente do item de Olá que pode ser utilizada para controlo de simultaneidade otimista quando executar operações que atualizam itens no catálogo de Olá. "*" pode ser utilizado toomatch qualquer valor.</td></tr></table>

### <a name="common-properties"></a>Propriedades comuns
Estas propriedades aplicam tipos de elemento de raiz tooall e todos os tipos de anotação.

<table>
<tr><td><b>Nome da propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>
<tr><td>fromSourceSystem</td><td>Valor booleano</td><td>Indica se os dados do item são derivados de um sistema de origem (por exemplo, o servidor de base de dados Sql, base de dados Oracle) ou criados por um utilizador.</td></tr>
</table>

### <a name="common-root-properties"></a>Propriedades comuns de raiz
<p>
Estas propriedades são aplicáveis a tipos de elemento de raiz tooall.

<table><tr><td><b>Nome da propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr><tr><td>nome</td><td>Cadeia</td><td>Um nome derivado de informações de localização de origem de dados de Olá</td></tr><tr><td>DSL</td><td>DataSourceLocation</td><td>Exclusivamente descreve a origem de dados de Olá e é um dos identificadores de Olá para o recurso de Olá. (Consulte a secção identidade dupla).  estrutura de Olá de Olá dsl varia consoante o protocolo de Olá e tipo de origem.</td></tr><tr><td>origem de dados</td><td>DataSourceInfo</td><td>Mais detalhadamente no tipo de Olá do recurso.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Descreve Olá utilizador recentemente registado este recurso.  Contém um id exclusivo Olá para utilizador Olá (Olá upn) e um nome a apresentar (lastName e firstName).</td></tr><tr><td>ID do contentor</td><td>Cadeia</td><td>ID do recurso de contentor Olá Olá origem de dados. Esta propriedade não é suportada para Olá o tipo de contentor.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Propriedades comuns de anotação não singleton
Estas propriedades aplicam tipos de anotação não singleton tooall (anotações, o que permitido toobe vários por ativo).

<table>
<tr><td><b>Nome da propriedade</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>
<tr><td>key</td><td>Cadeia</td><td>Um utilizador especificado chave, que identifica exclusivamente anotação Olá na coleção atual Olá. comprimento de chave Olá não pode exceder os 256 carateres.</td></tr>
</table>

### <a name="root-asset-types"></a>Tipos de elemento de raiz
Tipos de recurso de raiz são os tipos que representam Olá vários tipos de recursos de dados que podem ser registados no catálogo de Olá. Para cada tipo de raiz, há uma vista, que descreve os ativos e anotações incluídas na vista de Olá. Nome da vista deve ser utilizado num segmento de url de {view_name} Olá correspondente ao publicar um elemento com a REST API.

<table><tr><td><b>Tipo de recurso (nome de vista)</b></td><td><b>Propriedades adicionais</b></td><td><b>Tipo de dados</b></td><td><b>Anotações permitidas</b></td><td><b>Comentários</b></td></tr><tr><td>Tabela ("tabelas")</td><td></td><td></td><td>Descrição<p>friendlyName<p>Etiqueta<p>Esquema<p>ColumnDescription<p>ColumnTag<p> disponibilizamos<p>Pré-visualização<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Documentação<p></td><td>Uma tabela representa dados de tabela.  Por exemplo: SQL tabela, vista SQL, tabela em tabela do Analysis Services, Analysis Services Multidimensional de dimensão, Oracle tabela, etc.   </td></tr><tr><td>Medidas ("medidas")</td><td></td><td></td><td>Descrição<p>friendlyName<p>Etiqueta<p>disponibilizamos<p>AccessInstruction<p>Documentação<p></td><td>Este tipo representa uma medida de Analysis Services.</td></tr><tr><td></td><td>medidas</td><td>Coluna</td><td></td><td>Medida de Olá com descrição de metadados</td></tr><tr><td></td><td>isCalculated </td><td>Valor booleano</td><td></td><td>Especifica se a medida de Olá é calculada ou não.</td></tr><tr><td></td><td>Grupo de medidas</td><td>Cadeia</td><td></td><td>Contentor de físico para a medida</td></tr><td>KPI ("kpis")</td><td></td><td></td><td>Descrição<p>friendlyName<p>Etiqueta<p>disponibilizamos<p>AccessInstruction<p>Documentação</td><td></td></tr><tr><td></td><td>Grupo de medidas</td><td>Cadeia</td><td></td><td>Contentor de físico para a medida</td></tr><tr><td></td><td>goalExpression</td><td>Cadeia</td><td></td><td>Uma expressão numérica MDX ou um cálculo que devolve o valor de destino Olá de Olá KPI.</td></tr><tr><td></td><td>valueExpression</td><td>Cadeia</td><td></td><td>Uma expressão MDX numérica que devolve o valor real Olá Olá KPI.</td></tr><tr><td></td><td>statusExpression</td><td>Cadeia</td><td></td><td>Uma expressão MDX que representa o estado de Olá Olá KPI num especificado ponto no tempo.</td></tr><tr><td></td><td>trendExpression</td><td>Cadeia</td><td></td><td>Uma expressão MDX que avalia o valor Olá Olá KPI ao longo do tempo. tendência de Olá pode ser qualquer critério baseados no tempo que é útil num contexto empresariais específicos.</td>
<tr><td>Relatórios "(relatórios)</td><td></td><td></td><td>Descrição<p>friendlyName<p>Etiqueta<p>disponibilizamos<p>AccessInstruction<p>Documentação<p></td><td>Este tipo representa um relatório do SQL Server Reporting Services </td></tr><tr><td></td><td>assetCreatedDate</td><td>Cadeia</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Cadeia</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Cadeia</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Cadeia</td><td></td><td></td></tr><tr><td>Contentor ("contentores")</td><td></td><td></td><td>Descrição<p>friendlyName<p>Etiqueta<p>disponibilizamos<p>AccessInstruction<p>Documentação<p></td><td>Este tipo representa um contentor de outros recursos, tais como uma base de dados do SQL Server, um contentor de Blobs do Azure ou um modelo de Analysis Services.</td></tr></table>

### <a name="annotation-types"></a>Tipos de anotação
Tipos de anotação representam os tipos de metadados que podem ser atribuídos tooother tipos dentro do catálogo de Olá.

<table>
<tr><td><b>Tipo de anotação (nome de vista aninhadas)</b></td><td><b>Propriedades adicionais</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>

<tr><td>Descrição ("descrições")</td><td></td><td></td><td>Esta propriedade contém uma descrição para um recurso. Cada utilizador do sistema de Olá pode adicionar as seus próprios descrição.  Apenas esse utilizador pode editar o objeto de descrição de Olá.  (Os proprietários de recursos e administradores podem eliminar Olá descrição objeto, mas não editá-lo). sistema de Olá mantém as descrições dos utilizadores em separado.  Deste modo, é uma matriz de descrições de cada recurso (um para cada utilizador que tem contribuíram os seus conhecimentos sobre o recurso de Olá, na toopossibly adição que contenha informações derivada da origem de dados de Olá).</td></tr>
<tr><td></td><td>descrição</td><td>Cadeia</td><td>Uma descrição breve (linhas 2-3) do recurso de Olá</td></tr>

<tr><td>Etiqueta ("etiquetas")</td><td></td><td></td><td>Esta propriedade define uma etiqueta para um recurso. Cada utilizador do sistema de Olá pode adicionar várias etiquetas para um recurso.  Apenas o utilizador de Olá que criar objetos de etiqueta pode editá-los.  (Os proprietários de recursos e administradores podem eliminar Olá Tag objeto, mas não editá-lo). sistema de Olá mantém etiquetas dos utilizadores em separado.  Deste modo, é uma matriz de objetos de Tag em cada recurso.</td></tr>
<tr><td></td><td>Etiqueta</td><td>Cadeia</td><td>Um recurso de Olá com descrição de etiqueta.</td></tr>

<tr><td>FriendlyName ("friendlyName")</td><td></td><td></td><td>Esta propriedade contém um nome amigável para um recurso. FriendlyName é uma anotação singleton - FriendlyName apenas uma pode ser adicionada tooan ativo.  Apenas o utilizador de Olá que criou FriendlyName objeto pode editá-lo. (Os proprietários de recursos e administradores podem eliminar Olá FriendlyName objeto, mas não editá-lo). sistema de Olá mantém nomes amigáveis dos utilizadores em separado.</td></tr>
<tr><td></td><td>friendlyName</td><td>Cadeia</td><td>Um nome amigável do recurso de Olá.</td></tr>

<tr><td>Esquema ("schema")</td><td></td><td></td><td>Olá esquema descreve a estrutura de Olá dos dados de Olá.  -Apresenta uma lista de nomes de atributo (coluna, atributo, campo, etc.) Olá, tipos, bem como outros metadados.  Esta informação é obtida a partir da origem de dados de Olá.  Esquema é uma anotação singleton - apenas um esquema que pode ser adicionada para um recurso.</td></tr>
<tr><td></td><td>colunas</td><td>Coluna []</td><td>Uma matriz de objetos de coluna. Descrevem coluna Olá com informações derivadas Olá da origem de dados.</td></tr>

<tr><td>ColumnDescription ("columnDescriptions")</td><td></td><td></td><td>Esta propriedade contém uma descrição para uma coluna.  Cada utilizador do sistema de Olá pode adicionar as seus próprios descrições para várias colunas (um por coluna). Apenas o utilizador de Olá que criou objetos ColumnDescription pode editá-los.  (Os proprietários de recursos e administradores podem eliminar Olá ColumnDescription objeto, mas não editá-lo). sistema de Olá mantém descrições das colunas destas utilizador separadamente.  Deste modo, não há uma matriz de objetos de ColumnDescription em cada recurso (um por cada coluna para cada utilizador que tem contribuíram os seus conhecimentos sobre a coluna de Olá além disso toopossibly que contenha informações derivadas da origem de dados de Olá).  Olá ColumnDescription é aproximadamente ligado vinculada toohello esquema, pelo que pode obter fora de sincronização. Olá ColumnDescription poderá descrever uma coluna que já não existe no esquema Olá.  Está a funcionar descrição do toohello escritor tookeep e esquema sincronizada.  origem de dados de Olá pode também ter informações de descrição de colunas e são objetos ColumnDescription adicionais que seriam possível criar ao executar a ferramenta de Olá.</td></tr>
<tr><td></td><td>columnName</td><td>Cadeia</td><td>nome de Olá da coluna de Olá que esta descrição refere-se a.</td></tr>
<tr><td></td><td>descrição</td><td>Cadeia</td><td>uma descrição breve (2-3 linhas) da coluna de Olá.</td></tr>

<tr><td>ColumnTag ("columnTags")</td><td></td><td></td><td>Esta propriedade contém uma tag para uma coluna. Cada utilizador do sistema de Olá pode adicionar várias etiquetas para uma determinada coluna e pode adicionar etiquetas de várias colunas. Apenas o utilizador de Olá que criou objetos ColumnTag pode editá-los. (Os proprietários de recursos e administradores podem eliminar Olá ColumnTag objeto, mas não editá-lo). sistema de Olá mantém as etiquetas de coluna dos utilizadores, estes separadamente.  Deste modo, é uma matriz de objetos de ColumnTag em cada recurso.  Olá ColumnTag é aproximadamente ligado vinculada toohello esquema, pelo que pode obter fora de sincronização. Olá ColumnTag poderá descrever uma coluna que já não existe no esquema Olá.  Está a funcionar etiquetas de coluna toohello escritor tookeep e esquema sincronizada.</td></tr>
<tr><td></td><td>columnName</td><td>Cadeia</td><td>nome de Olá da coluna de Olá que esta etiqueta refere-se a.</td></tr>
<tr><td></td><td>Etiqueta</td><td>Cadeia</td><td>Uma coluna de Olá com descrição de etiqueta.</td></tr>

<tr><td>Especialista ("especialistas")</td><td></td><td></td><td>Esta propriedade contém um utilizador que é considerado um especialista no conjunto de dados de Olá. Olá opinions(descriptions) bolha toohello parte superior dos especialistas do Olá UX quando listar as descrições. Cada utilizador pode especificar as seus próprios especialistas. Apenas esse utilizador pode editar o objeto de especialistas Olá. (Os proprietários de recursos e administradores podem eliminar objetos especialista Olá, mas não editá-lo).</td></tr>
<tr><td></td><td>disponibilizamos</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Pré-visualização ("pré-visualizações")</td><td></td><td></td><td>pré-visualização de Olá contém um instantâneo de Olá superior 20 as linhas de dados para o recurso de Olá. Pré-visualização só fazem sentido para alguns tipos de recursos (faz sentido para a tabela, mas não para a medida).</td></tr>
<tr><td></td><td>pré-visualização</td><td>[] do objeto</td><td>Matriz de objetos que representam uma coluna.  Cada objeto tem uma propriedade tooa coluna com um valor para essa coluna para a linha de Olá de mapeamento.</td></tr>

<tr><td>AccessInstruction ("accessInstructions")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>Cadeia</td><td>tipo de mime de Olá de conteúdo de Olá.</td></tr>
<tr><td></td><td>Conteúdo</td><td>Cadeia</td><td>instruções de Olá para como tooget aceder toothis recurso de dados. conteúdo de Olá pode ser um URL, um endereço de e-mail ou um conjunto de instruções.</td></tr>

<tr><td>TableDataProfile ("tableDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>Int</td><td>número de Olá de linhas no conjunto de dados de Olá</td></tr>
<tr><td></td><td>Tamanho</td><td>longa</td><td>tamanho de Olá de conjunto de dados de Olá em bytes.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>Cadeia</td><td>esquema de Olá de tempo Olá última modificação</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>Cadeia</td><td>conjunto de dados de Olá Olá última hora foi modificado (dados foi adicionados, modificados, ou eliminar)</td></tr>

<tr><td>ColumnsDataProfile ("columnsDataProfiles")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>colunas</td></td><td>ColumnDataProfile []</td><td>Uma matriz de perfis de dados da coluna.</td></tr>

<tr><td>ColumnDataClassification ("columnDataClassifications")</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>Cadeia</td><td>nome de Olá da coluna de Olá que referencia esta classificação.</td></tr>
<tr><td></td><td>Classificação</td><td>Cadeia</td><td>classificação de Olá dos dados de Olá nesta coluna.</td></tr>

<tr><td>Documentação ("documentação")</td><td></td><td></td><td>Um determinado elemento pode ter apenas uma documentação associada à mesma.</td></tr>
<tr><td></td><td>mimeType</td><td>Cadeia</td><td>tipo de mime de Olá de conteúdo de Olá.</td></tr>
<tr><td></td><td>Conteúdo</td><td>Cadeia</td><td>conteúdo de documentation Olá.</td></tr>

</table>

### <a name="common-types"></a>Tipos comuns
Tipos comuns podem ser utilizados como tipos de Olá para propriedades, mas não são itens.

<table>
<tr><td><b>Tipo comum</b></td><td><b>Propriedades</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>SourceType</td><td>Cadeia</td><td>Descreve o tipo de Olá da origem de dados.  Por exemplo: SQL Server, a base de dados Oracle, etc.  </td></tr>
<tr><td></td><td>objectType</td><td>Cadeia</td><td>Descreve o tipo de Olá de objeto da origem de dados de Olá. Por exemplo: tabela, ver para o SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Protocolo</td><td>Cadeia</td><td>Necessário. Descreve um toocommunicate protocolo utilizado com a origem de dados de Olá. Por exemplo: "tds" para o SQl Server, "oracle" para Oracle, etc. Consulte demasiado[especificação de referência - DSL estrutura de origem de dados](data-catalog-dsr.md) para Olá obter lista de protocolos atualmente suportados.</td></tr>
<tr><td></td><td>Endereço</td><td>Dicionário<string, object></td><td>Necessário. O endereço é um conjunto de protocolo de toohello específicos de dados que é a origem de dados utilizados tooidentify Olá referenciada. dados de endereço de Olá confinados tooa protocolo específico, ou seja, são sem significado sem saberem a protocolo Olá.</td></tr>
<tr><td></td><td>Autenticação</td><td>Cadeia</td><td>Opcional. esquema de autenticação de Olá utilizado toocommunicate com a origem de dados de Olá. Por exemplo: windows, oauth, etc.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Dicionário<string, object></td><td>Opcional. Informações adicionais sobre como origem de dados de tooa tooconnect.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>back-end de Olá não efetua qualquer validação das propriedades fornecidas contra AAD durante a publicação.</td></tr>
<tr><td></td><td>UPN</td><td>Cadeia</td><td>Endereço de e-mail exclusivo do utilizador. Tem de ser especificado se não for fornecido objectId ou no contexto de Olá da propriedade "lastRegisteredBy", caso contrário, opcional.</td></tr>
<tr><td></td><td>objectId</td><td>GUID</td><td>Identidade AAD de grupo ou utilizador administrativo. Opcional. Tem de ser especificado se upn não for fornecido, caso contrário, opcional.</td></tr>
<tr><td></td><td>Nome próprio</td><td>Cadeia</td><td>Nome próprio do utilizador (para efeitos de apresentação). Opcional. Só é válido no contexto de Olá da propriedade "lastRegisteredBy". Não é possível especificar ao fornecer o principal de segurança para "funções", "permissões" e "especialistas".</td></tr>
<tr><td></td><td>Apelido</td><td>Cadeia</td><td>Apelido do utilizador (para efeitos de apresentação). Opcional. Só é válido no contexto de Olá da propriedade "lastRegisteredBy". Não é possível especificar ao fornecer o principal de segurança para "funções", "permissões" e "especialistas".</td></tr>

<tr><td>Coluna</td><td></td><td></td><td></td></tr>
<tr><td></td><td>nome</td><td>Cadeia</td><td>Nome da coluna de Olá ou atributo.</td></tr>
<tr><td></td><td>tipo</td><td>Cadeia</td><td>tipo de dados da coluna de Olá ou atributo. os tipos permitidos Olá dependem sourceType de dados de ativo Olá.  Apenas um subconjunto dos tipos é suportado.</td></tr>
<tr><td></td><td>maxLength</td><td>Int</td><td>comprimento de máximo Olá permitido para a coluna de Olá ou atributo. Derivado da origem de dados. Apenas os tipos de origem toosome aplicável.</td></tr>
<tr><td></td><td>precisão</td><td>Bytes</td><td>precisão Olá para coluna Olá ou atributo. Derivado da origem de dados. Apenas os tipos de origem toosome aplicável.</td></tr>
<tr><td></td><td>isNullable</td><td>Valor booleano</td><td>Indica se a coluna de Olá é permitida toohave um valor nulo ou não. Derivado da origem de dados. Apenas os tipos de origem toosome aplicável.</td></tr>
<tr><td></td><td>expressão</td><td>Cadeia</td><td>Se o valor de Olá é uma coluna calculada, este campo contém expressão Olá expresse precisa valor Olá. Derivado da origem de dados. Apenas os tipos de origem toosome aplicável.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>Cadeia</td><td>nome de Olá da coluna de Olá</td></tr>
<tr><td></td><td>tipo </td><td>Cadeia</td><td>tipo de Olá da coluna de Olá</td></tr>
<tr><td></td><td>min. </td><td>Cadeia</td><td>valor mínimo de Olá no conjunto de dados de Olá</td></tr>
<tr><td></td><td>Máx. </td><td>Cadeia</td><td>valor máximo de Olá no conjunto de dados de Olá</td></tr>
<tr><td></td><td>média </td><td>duplo</td><td>valor médio do Olá no conjunto de dados de Olá</td></tr>
<tr><td></td><td>StDev </td><td>duplo</td><td>desvio-padrão de Olá Olá conjunto de dados</td></tr>
<tr><td></td><td>nullCount </td><td>Int</td><td>Contagem de Olá de valores nulos existentes no conjunto de dados de Olá</td></tr>
<tr><td></td><td>distinctCount  </td><td>Int</td><td>Contagem de Olá de valores distintos no conjunto de dados de Olá</td></tr>


</table>

## <a name="asset-identity"></a>Identidade de recurso
Catálogo de dados do Azure utiliza "protocolo" e propriedades de identidade de Olá "endereço" matriz de propriedades de identidade do Olá DataSourceLocation "dsl" propriedade toogenerate do elemento de Olá, que é utilizado tooaddress Olá asset dentro Olá catálogo.
Por exemplo, o protocolo de "tds" Olá tem propriedades de identidade "server", "base de dados", "schema" e "objeto". combinações de Olá do protocolo de Olá e propriedades de identidade hello são utilizadas toogenerate Olá identidade de Olá elemento de tabela do SQL Server.
Catálogo de dados do Azure fornece vários protocolos de origem de dados incorporada, que estão listados em [especificação de referência - DSL estrutura de origem de dados](data-catalog-dsr.md).
Olá conjunto de protocolos suportados pode ser expandido através de programação (consulte a referência da API de REST do catálogo tooData). Os administradores de Olá catálogo podem registar os protocolos de origem de dados personalizados. Olá tabela seguinte descreve Olá propriedades necessárias tooregister um protocolo personalizado.

### <a name="custom-data-source-protocol-specification"></a>Especificação de protocolo de origem de dados personalizada
<table>
<tr><td><b>Tipo</b></td><td><b>Propriedades</b></td><td><b>Tipo de dados</b></td><td><b>Comentários</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Espaço de nomes</td><td>Cadeia</td><td>espaço de nomes de Olá do protocolo de Olá. Espaço de nomes tem de ser de 1 too255 carateres e conter um ou mais partes vazios separadas por ponto (.). Cada parte tem de ter entre 1 too255 carateres, começar com uma letra e conter apenas letras e números.</td></tr>
<tr><td></td><td>nome</td><td>Cadeia</td><td>nome do protocolo de Olá Olá. Nome tem de ter entre 1 too255 carateres, começar com uma letra e conter apenas letras, números e caráter de travessão (-) Olá.</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty []</td><td>Lista de propriedades de identidade, tem de conter pelo menos, mas não existem propriedades mais de 20. Por exemplo: "server", "base de dados", "schema", "objeto" é propriedades de identidade do protocolo de "tds" Olá.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet []</td><td>Lista de conjuntos de identidade. Define os conjuntos de propriedades de identidade, o que representam a identidade de recurso válido. Tem de conter pelo menos, mas não existem conjuntos mais de 20. Por exemplo: {"server", "base de dados", "schema" e "objeto"} é uma identidade definida para o protocolo "tds", que define a identidade do elemento de tabela do Sql Server.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>nome</td><td>Cadeia</td><td>nome da propriedade Olá Olá. Nome tem de ter entre 1 too100 carateres, começar com uma letra e só pode conter letras e números.</td></tr>
<tr><td></td><td>tipo</td><td>Cadeia</td><td>tipo da propriedade Olá Olá. Valores suportados: "bool" booleano ","byte","guid","int","inteiros","período de tempo","cadeia","url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>bool</td><td>Indica se devem ser ignorada maiúsculas e minúsculas, ao utilizar o valor da propriedade. Só pode ser especificado para propriedades com o tipo "cadeia". Valor predefinido é falso.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool []</td><td>Indica se as maiúsculas e minúsculas devem ser ignorada para cada segmento do caminho do url de Olá. Só pode ser especificado para propriedades com o tipo de "url". Valor predefinido é [false].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>nome</td><td>Cadeia</td><td>o nome da identidade de Olá Olá definido.</td></tr>
<tr><td></td><td>propriedades</td><td>String]</td><td>definir a lista de Olá de propriedades de identidade incluído nesta identidade. Não pode conter duplicados. Cada propriedade referenciada pelo conjunto de identidade tem de ser definida na lista de Olá de "identityProperties" do protocolo de Olá.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Funções e autorização
Catálogo de dados do Microsoft Azure fornece capacidades de autorização para operações CRUD de elementos e anotações.

## <a name="key-concepts"></a>Conceitos-chave
Olá catálogo de dados do Azure utiliza dois mecanismos de autorização:

* Autorização baseada em funções
* Autorização baseada em permissão

### <a name="roles"></a>Funções
Existem três funções: **administrador**, **proprietário**, e **contribuinte**.  Cada função tem o âmbito e direitos, que estão resumidos na Olá a tabela seguinte.

<table><tr><td><b>Função</b></td><td><b>Âmbito</b></td><td><b>Direitos</b></td></tr><tr><td>Administrador</td><td>Catálogo (todos os recursos/anotações do Olá catálogo)</td><td>ViewRoles de eliminação de leitura

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Proprietário</td><td>Cada elemento (item de raiz)</td><td>ViewRoles de eliminação de leitura

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Contribuinte</td><td>Cada recurso individual e anotação</td><td>Atualização de leitura eliminar ViewRoles Nota: todos os direitos de Olá são revogados se Olá ler direito no item de Olá é revogado a Olá contribuinte</td></tr></table>

> [!NOTE]
> **Leitura**, **atualização**, **eliminar**, **ViewRoles** direitos são aplicáveis tooany item (anotação ou de recurso) ao **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** são apenas o elemento de raiz toohello aplicável.
> 
> **Eliminar** aplica-se à direita tooan item e quaisquer subitems ou único item abaixo dele. Por exemplo, a eliminação de um recurso também elimina quaisquer anotações para esse recurso.
> 
> 

### <a name="permissions"></a>Permissões
Permissão é como a lista de entradas de controlo de acesso. Cada entrada de controlo de acesso atribui conjunto direitos tooa do principal de segurança. Permissões só podem ser especificadas num recurso (ou seja, o item de raiz) e aplicam toohello asset e qualquer subitems.

Durante a Olá **catálogo de dados do Azure** pré-visualizar, apenas **leitura** direita é suportada no Olá permissões lista tooenable cenário toorestrict visibilidade de um ativo.

Por predefinição nenhum utilizador autenticado tem **leitura** botão direito do rato para qualquer item no catálogo de Olá, a menos que visibilidade restrita toohello conjunto de principais nas permissões de Olá.

## <a name="rest-api"></a>API REST
**COLOCAR** e **POST** item da vista de pedidos podem ser utilizados toocontrol funções e permissões: no payload de tooitem de adição, duas propriedades do sistema podem ser especificadas **funções** e  **permissões**.

> [!NOTE]
> **permissões** apenas o item de raiz tooa aplicável.
> 
> **Proprietário** item de raiz do função tooa apenas aplicável.
> 
> Por predefinição, quando um item é criado no catálogo de Olá respetivo **contribuinte** está definido o utilizador autenticado atualmente toohello. Se o item deverá ser atualizável por todas as pessoas, **contribuinte** deve ser definido demasiado&lt;todas as pessoas&gt; principal de segurança especial no Olá **funções** propriedade quando o item é publicada pela primeira vez ( Consulte toohello seguinte o exemplo). **Contribuidor** não pode ser alterada e permanece Olá mesmo durante o tempo de vida de um item (mesmo **administrador** ou **proprietário** não tem Olá toochange direito de Olá  **Contribuidor**). Olá, apenas um valor suportado para a definição explícita do Olá do Olá **contribuinte** é &lt;todas as pessoas&gt;: **contribuinte** só pode ser um utilizador que criou um item ou &lt; Todas as pessoas&gt;.
> 
> 

### <a name="examples"></a>Exemplos
**Definir contribuinte demasiado&lt;todas as pessoas&gt; ao publicar um item.**
O principal de segurança especial &lt;todas as pessoas&gt; tem objectId "00000000-0000-0000-0000-000000000201".
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Algumas implementações de cliente HTTP podem emitir automaticamente pedidos na resposta tooa 302 do servidor de Olá, mas normalmente da faixa cabeçalhos de autorização do pedido de Olá. Uma vez que o cabeçalho de autorização de Olá toomake necessário pedidos tooAzure catálogo de dados, certifique-se de cabeçalho de autorização de Olá ainda é fornecido quando emitir novamente numa localização de redirecionamento do pedido tooa especificada pelo catálogo de dados do Azure. Olá código de exemplo seguinte demonstra-lo utilizando o objeto de .NET HttpWebRequest Olá.
> 
> 

**Corpo**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Atribua os proprietários e restringir a visibilidade para um item de raiz existente**: **colocar** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> No PUT não seja necessário toospecify um payload de item no corpo de Olá: PUT pode ser funções apenas tooupdate utilizado e/ou permissões.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
