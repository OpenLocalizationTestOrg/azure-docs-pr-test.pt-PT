---
title: "referência de aaaPart para o estruturador de vistas no OMS Log Analytics | Microsoft Docs"
description: "Estruturador de vistas no Log Analytics permite-lhe toocreate personalizada vistas na consola do OMS Olá que contenham visualizações diferentes dos dados no repositório do Olá OMS. Este artigo fornece uma referência de definições de Olá para cada um dos Olá visualização partes toouse disponível no seu vistas personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Referência de parte de visualização do estruturador de vistas de análise de registo
Olá estruturador de vistas no Log Analytics permite-lhe toocreate vistas personalizadas na consola do OMS Olá que contêm visualizações diferentes dos dados a partir do repositório OMS Olá. Este artigo fornece uma referência de definições de Olá para cada um dos Olá visualização partes toouse disponível no seu vistas personalizadas.

Outros artigos disponíveis para o estruturador de vistas são:

* [Ver Designer](log-analytics-view-designer.md) -descrição geral de Olá estruturador de vistas e procedimentos para criar e editar vistas personalizadas.
* [Mosaico referência](log-analytics-view-designer-tiles.md) -referência das definições de Olá para cada um dos Olá os mosaicos toouse disponível no seu vistas personalizadas.

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, as consultas em todas as vistas têm de ser escritas na Olá [novo idioma de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas as vistas que foram criadas para a área de trabalho de Olá foi atualizada será automtically convertido.

Olá tabela seguinte descreve Olá diferentes tipos de mosaicos disponíveis no Olá estruturador de vistas.  as secções de Olá abaixo descrevem cada tipo de mosaico detalhes e as respetivas propriedades.

| Tipo de vista | Descrição |
|:--- |:--- |
| [Lista de consultas](#list-of-queries-part) |Mostra uma lista de consultas de pesquisa de registo.  utilizador Olá pode clicar em cada consulta toodisplay dos resultados. |
| [Número & lista](#number-amp-list-part) |Cabeçalho tem um único número que mostra número de registos por uma consulta de pesquisa de registo.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo. |
| [Dois números & lista](#two-numbers-amp-list-part) |Cabeçalho tem dois números que mostra a contagem de registos de consultas de pesquisa de registo separados.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo. |
| [& Lista dos anel](#donut-amp-list-part) |Cabeçalho apresenta um número único resumido a partir da coluna valor de uma consulta de registo.  anel Olá graficamente apresenta resultados de registos de três principais Olá. |
| [Duas linhas cronológicas & lista](#two-timelines-amp-list-part) |Cabeçalho apresenta Olá resultados de consultas de registo de dois ao longo do tempo como gráficos de colunas com uma chamada apresentar um único número resumidos a partir de uma coluna de valor de uma consulta de registo.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo. |
| [Informações](#information-part) |Cabeçalho mostra texto estático e uma ligação opcional.  Lista apresenta um ou mais itens com texto estático e título. |
| [Gráfico de linhas, chamada & lista](#line-chart-callout-amp-list-part) |Cabeçalho apresenta um gráfico de linhas com várias séries por uma consulta de registo ao longo do tempo e uma chamada com um valor resumido.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo. |
| [Gráfico de linhas & lista](#line-chart-amp-list-part) |Cabeçalho apresenta um gráfico de linhas com várias séries por uma consulta de registo ao longo do tempo.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo. |
| [Pilha da peça de gráficos de linha](#stack-of-line-charts-part) |Apresenta os três separado gráficos de linhas com várias séries por uma consulta de registo ao longo do tempo. |

## <a name="list-of-queries-part"></a>Lista de parte de consultas
Mostra uma lista de consultas de pesquisa de registo.  utilizador Olá pode clicar em cada consulta toodisplay dos resultados.  Vista de Olá incluirá uma única consulta por predefinição e pode clicar em **+ consulta** consultas adicionais tooadd.

![Lista de vista de consultas](media/log-analytics-view-designer/view-list-queries.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título |Toodisplay de texto na parte superior de Olá da vista de Olá. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Filtros previamente selecionados |Lista delimitada por vírgulas de propriedades tooinclude no painel de filtro esquerdo Olá quando o utilizador Olá seleciona uma consulta. |
| Modo de composição |Vista inicial apresentada quando a consulta de Olá está selecionada.  utilizador Olá pode selecionar qualquer vistas disponíveis depois de abrir a consulta de Olá. |
| **Consultas** | |
| Consulta de pesquisa |Toorun de consulta. |
| Nome amigável |Nome descritivo do utilizador do Olá consulta toodisplay toohello. |

## <a name="number--list-part"></a>Número & lista parte
Cabeçalho tem um único número que mostra número de registos por uma consulta de pesquisa de registo.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo.

![Lista de vista de consultas](media/log-analytics-view-designer/view-number-list.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Toodisplay de texto na parte superior de Olá da vista de Olá. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| Ícone de utilização |Selecione a apresentação de ícone de Olá toohave. |
| **Título** | |
| Legenda |Texto toodisplay, Olá parte superior do cabeçalho de Olá. |
| Consulta |Toorun de consulta para o cabeçalho de Olá.  Contagem de Olá do número de Olá de registos devolvidos pela consulta Olá será apresentada. |
| **Lista** | |
| Consulta |Toorun de consulta para obter a lista de Olá.  Olá primeiro duas propriedades para hello registos primeiro dez nos resultados de Olá serão apresentados.  propriedade primeiro Olá deve ser um valor e Olá segunda propriedade text um valor numérico.  São criadas automaticamente com base no valor de relativo Olá da coluna numérica Olá barras.<br><br>Utilize o comando de ordenação de Olá no Olá toosort Olá os registos de consulta na lista de Olá.  Olá utilizador pode clicar em ver todos os toorun Olá, consultar e devolver todos os registos. |
| Ocultar gráfico |Selecione o direito de toohello do toodisable Olá gráfico da coluna numérica Olá. |
| Ativar sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Cor |Cor de barras de Olá ou sparklines. |
| Nome e valor de separação |Delimitador de carácter único se quiser propriedade de texto de Olá tooparse em vários valores.  Consulte [definições comuns](#name-value-separator) para obter mais detalhes. |
| Consulta de navegação |Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Consulte [definições comuns](#navigation-query) para obter mais detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de Olá da primeira coluna de Olá da lista de Olá. |
| Valor |Toodisplay de texto na parte superior de Olá da segunda coluna de Olá da lista de Olá. |
| **Lista** |**> Limiares** |
| Ativar os limiares |Selecione tooenable limiares.  Consulte [definições comuns](#thresholds) para obter mais detalhes. |

## <a name="two-numbers--list-part"></a>Dois números & parte da lista
Cabeçalho tem dois números que mostra a contagem de registos de consultas de pesquisa de registo separados.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo.

![& Vista de lista de dois números](media/log-analytics-view-designer/view-two-numbers-list.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Toodisplay de texto na parte superior de Olá da vista de Olá. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| Ícone de utilização |Selecione a apresentação de ícone de Olá toohave. |
| **Título** | |
| Legenda |Texto toodisplay, Olá parte superior do cabeçalho de Olá. |
| Consulta |Toorun de consulta para o cabeçalho de Olá.  Contagem de Olá do número de Olá de registos devolvidos pela consulta Olá será apresentada. |
| **Lista** | |
| Consulta |Toorun de consulta para obter a lista de Olá.  Olá primeiro duas propriedades para hello registos primeiro dez nos resultados de Olá serão apresentados.  propriedade primeiro Olá deve ser um valor e Olá segunda propriedade text um valor numérico.  São criadas automaticamente com base no valor de relativo Olá da coluna numérica Olá barras.<br><br>Utilize o comando de ordenação de Olá no Olá toosort Olá os registos de consulta na lista de Olá.  Olá utilizador pode clicar em ver todos os toorun Olá, consultar e devolver todos os registos. |
| Ocultar gráfico |Selecione o direito de toohello do toodisable Olá gráfico da coluna numérica Olá. |
| Ativar sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Cor |Cor de barras de Olá ou sparklines. |
| Operação |Operação tooperform para gráfico sparkline de Olá.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Nome e valor de separação |Delimitador de carácter único se quiser propriedade de texto de Olá tooparse em vários valores.  Consulte [definições comuns](#name-value-separator) para obter mais detalhes. |
| Consulta de navegação |Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Consulte [definições comuns](#navigation-query) para obter mais detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de Olá da primeira coluna de Olá da lista de Olá. |
| Valor |Toodisplay de texto na parte superior de Olá da segunda coluna de Olá da lista de Olá. |
| **Lista** |**> Limiares** |
| Ativar os limiares |Selecione tooenable limiares.  Consulte [definições comuns](#thresholds) para obter mais detalhes. |

## <a name="donut--list-part"></a>Parte de anel & lista
Cabeçalho apresenta um número único resumido a partir da coluna valor de uma consulta de registo.  anel Olá graficamente apresenta resultados de registos de três principais Olá.

![Vista de anel & lista](media/log-analytics-view-designer/view-donut-list.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Texto toodisplay, Olá parte superior do Olá mosaico. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| Ícone de utilização |Selecione a apresentação de ícone de Olá toohave. |
| **Cabeçalho** | |
| Título |Texto toodisplay, Olá parte superior do cabeçalho de Olá. |
| Subtítulo do |Texto toodisplay em Olá título na parte superior de Olá de cabeçalho de Olá. |
| **Anel** | |
| Consulta |Consulta toorun para anel Olá.  propriedade primeiro Olá deve ser um valor e Olá segunda propriedade text um valor numérico. |
| **Anel** |**> Center** |
| Texto |Texto toodisplay em valor Olá Olá anel. |
| Operação |Olá operação tooperform no Olá valor toosummarize tooa único valor da propriedade.<br><br>-Soma: Adicione valores de Olá de todos os registos.<br>-Percentagem: Percentagem de registos de Olá devolvidos por valores Olá **resultar valores utilizados na operação de center** toohello total de registos na consulta de Olá. |
| Valores de resultado utilizados na operação do System center |Opcionalmente, clique em Olá sinal tooadd um ou mais valores.  Olá os resultados da consulta de Olá será limitado toorecords com valores de propriedade Olá que especificar.  Se não existem valores são adicionados, todos os registos estão incluídos na consulta de Olá. |
| **Opções adicionais** |**> Cores** |
| Cor 1<br>Cor 2<br>Cor 3 |Selecione a cor de Olá para Olá dos valores de Olá apresentado no anel Olá. |
| **Opções adicionais** |**> Mapeamento de cor avançadas** |
| Valor do campo |Nome do tipo Olá de um campo toodisplay-o como uma cor diferente se está incluído no anel Olá. |
| Cor |Selecione a cor de Olá para campo exclusivo Olá. |
| **Lista** | |
| Consulta |Toorun de consulta para obter a lista de Olá.  Contagem de Olá do número de Olá de registos devolvidos pela consulta Olá será apresentada. |
| Ocultar gráfico |Selecione o direito de toohello do toodisable Olá gráfico da coluna numérica Olá. |
| Ativar sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Cor |Cor de barras de Olá ou sparklines. |
| Operação |Operação tooperform para gráfico sparkline de Olá.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Nome e valor de separação |Delimitador de carácter único se quiser propriedade de texto de Olá tooparse em vários valores.  Consulte [definições comuns](#name-value-separator) para obter mais detalhes. |
| Consulta de navegação |Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Consulte [definições comuns](#navigation-query) para obter mais detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de Olá da primeira coluna de Olá da lista de Olá. |
| Valor |Toodisplay de texto na parte superior de Olá da segunda coluna de Olá da lista de Olá. |
| **Lista** |**> Limiares** |
| Ativar os limiares |Selecione tooenable limiares.  Consulte [definições comuns](#thresholds) para obter mais detalhes. |

## <a name="two-timelines--list-part"></a>Dois parte linhas cronológicas & lista
Cabeçalho apresenta Olá resultados de consultas de registo de dois ao longo do tempo como gráficos de colunas com uma chamada apresentar um único número resumidos a partir de uma coluna de valor de uma consulta de registo.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo.

![Duas linhas cronológicas & lista ver](media/log-analytics-view-designer/view-two-timelines-list.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Texto toodisplay, Olá parte superior do Olá mosaico. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| Ícone de utilização |Selecione a apresentação de ícone de Olá toohave. |
| **Primeiro gráfico<br>segundo gráfico** | |
| Legenda |Texto toodisplay em Olá chamada para a série primeiro Olá. |
| Cor |Cor toouse para colunas de Olá na série de Olá. |
| Consulta |Consulta toorun para série primeiro Olá.  Contagem de Olá do número de Olá de registos ao longo de cada intervalo de tempo será representada por colunas de gráfico de Olá. |
| Operação |Olá operação tooperform no Olá valor toosummarize tooa único valor da propriedade Olá chamada.<br><br>-Soma: Soma do valor de Olá de todos os registos.<br>-Média: A média do valor de Olá de todos os registos.<br>-Última amostra: Valor no último intervalo de Olá incluído no gráfico de Olá.<br>-O primeiro exemplo: O valor do primeiro intervalo de Olá incluído no gráfico de Olá.<br>-Contagem: Contagem de todos os registos devolvidos pela consulta Olá. |
| **Lista** | |
| Consulta |Toorun de consulta para obter a lista de Olá.  Contagem de Olá do número de Olá de registos devolvidos pela consulta Olá será apresentada. |
| Ocultar gráfico |Selecione o direito de toohello do toodisable Olá gráfico da coluna numérica Olá. |
| Ativar sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Cor |Cor de barras de Olá ou sparklines. |
| Operação |Operação tooperform para gráfico sparkline de Olá.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Consulta de navegação |Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Consulte [definições comuns](#navigation-query) para obter mais detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de Olá da primeira coluna de Olá da lista de Olá. |
| Valor |Toodisplay de texto na parte superior de Olá da segunda coluna de Olá da lista de Olá. |
| **Lista** |**> Limiares** |
| Ativar os limiares |Selecione tooenable limiares.  Consulte [definições comuns](#thresholds) para obter mais detalhes. |

## <a name="information-part"></a>Parte de informações
Cabeçalho mostra texto estático e uma ligação opcional.  Lista apresenta um ou mais itens com texto estático e título.

![Vista de informações](media/log-analytics-view-designer/view-information.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Texto toodisplay, Olá parte superior do Olá mosaico. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Cor |Cor de fundo do cabeçalho de Olá. |
| **Cabeçalho** | |
| Imagem |Toodisplay do ficheiro de imagem no cabeçalho de Olá. |
| Etiqueta |Toodisplay de texto no cabeçalho de Olá. |
| **Cabeçalho** |**> Ligação de** |
| Etiqueta |Texto da hiperligação. |
| Url |URL da ligação. |
| **Itens de informações** | |
| Título |Toodisplay de texto para o título de cada item. |
| Conteúdo |Texto toodisplay para cada item. |

## <a name="line-chart-callout--list-part"></a>Gráfico de linhas, chamada & parte da lista
Cabeçalho apresenta um gráfico de linhas com várias séries por uma consulta de registo ao longo do tempo e uma chamada com um valor resumido.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo.

![Gráfico de linhas, chamada & vista de lista](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Texto toodisplay, Olá parte superior do Olá mosaico. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| Ícone de utilização |Selecione a apresentação de ícone de Olá toohave. |
| **Cabeçalho** | |
| Título |Texto toodisplay, Olá parte superior do cabeçalho de Olá. |
| Subtítulo do |Texto toodisplay em Olá título na parte superior de Olá de cabeçalho de Olá. |
| **Gráfico de linhas** | |
| Consulta |Consulta toorun para gráfico de linhas de Olá.  propriedade primeiro Olá deve ser um valor e Olá segunda propriedade text um valor numérico.  Isto é normalmente uma consulta que utiliza Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta de Olá utiliza Olá **intervalo** palavra-chave, em seguida, Olá eixo x do gráfico Olá irá utilizar este intervalo de tempo.  Se a consulta de Olá não incluir Olá **intervalo** intervalos de palavra-chave e a hora a hora são utilizados para Olá eixo x. |
| **Gráfico de linhas** |**> Chamada** |
| Título da chamada |Texto toodisplay acima valor de chamada de Olá. |
| Nome da série |Valor da propriedade Olá toouse de série para o valor de chamada de Olá.  Se não for fornecido nenhum série, todos os registos da consulta hello são utilizados. |
| Operação |Olá operação tooperform no Olá valor toosummarize tooa único valor da propriedade Olá chamada.<br><br>-Média: A média do valor de Olá de todos os registos.<br>-Contagem de contagem de todos os registos devolvidos pela consulta Olá.<br>-Última amostra: Valor no último intervalo de Olá incluído no gráfico de Olá.<br>-Máximo: O valor máximo de intervalos de Olá incluído no gráfico de Olá.<br>-Mínimo: O valor mínimo de intervalos de Olá incluído no gráfico de Olá.<br>-Soma: Soma do valor de Olá de todos os registos. |
| **Gráfico de linhas** |**> Eixo Y** |
| Utilizar escala logarítmica |Selecione toouse uma escala logarítmica para Olá eixo y. |
| Unidades |Especifique unidades Olá para os valores de Olá devolvidos pela consulta Olá.  Estas informações são utilizadas toodisplay etiquetas no gráfico de Olá com a indicação de tipos de valor de Olá e, opcionalmente, para converter valores Olá.  Olá um tipo de unidade Especifica a categoria de Olá da unidade de Olá e define os valores do tipo de unidade atual Olá que estão disponíveis.  Se selecionar um valor em converter toothen Olá numérico valores são convertidos do Olá unidade atual tipo toohello converter tootype. |
| Etiqueta personalizada |Texto toodisplay para Olá Y seguinte toohello etiqueta do eixo de um tipo de unidade Olá.  Não se for especificada nenhuma etiqueta, apenas um tipo de unidade Olá é apresentado. |
| **Lista** | |
| Consulta |Toorun de consulta para obter a lista de Olá.  Contagem de Olá do número de Olá de registos devolvidos pela consulta Olá será apresentada. |
| Ocultar gráfico |Selecione o direito de toohello do toodisable Olá gráfico da coluna numérica Olá. |
| Ativar sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Cor |Cor de barras de Olá ou sparklines. |
| Operação |Operação tooperform para gráfico sparkline de Olá.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Nome e valor de separação |Delimitador de carácter único se quiser propriedade de texto de Olá tooparse em vários valores.  Consulte [definições comuns](#name-value-separator) para obter mais detalhes. |
| Consulta de navegação |Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Consulte [definições comuns](#navigation-query) para obter mais detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de Olá da primeira coluna de Olá da lista de Olá. |
| Valor |Toodisplay de texto na parte superior de Olá da segunda coluna de Olá da lista de Olá. |
| **Lista** |**> Limiares** |
| Ativar os limiares |Selecione tooenable limiares.  Consulte [definições comuns](#thresholds) para obter mais detalhes. |

## <a name="line-chart--list-part"></a>Parte de gráfico & lista de linha
Cabeçalho apresenta um gráfico de linhas com várias séries por uma consulta de registo ao longo do tempo.  Lista apresenta os resultados de dez principais Olá por uma consulta com um gráfico com a indicação de Olá relativo valor uma coluna numérica ou respetivas alterações ao longo do tempo.

![Vista de gráfico & lista de linha](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Texto toodisplay, Olá parte superior do Olá mosaico. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| Ícone de utilização |Selecione a apresentação de ícone de Olá toohave. |
| **Cabeçalho** | |
| Título |Texto toodisplay, Olá parte superior do cabeçalho de Olá. |
| Subtítulo do |Texto toodisplay em Olá título na parte superior de Olá de cabeçalho de Olá. |
| **Gráfico de linhas** | |
| Consulta |Consulta toorun para gráfico de linhas de Olá.  propriedade primeiro Olá deve ser um valor e Olá segunda propriedade text um valor numérico.  Isto é normalmente uma consulta que utiliza Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta de Olá utiliza Olá **intervalo** palavra-chave, em seguida, Olá eixo x do gráfico Olá irá utilizar este intervalo de tempo.  Se a consulta de Olá não incluir Olá **intervalo** intervalos de palavra-chave e a hora a hora são utilizados para Olá eixo x. |
| **Gráfico de linhas** |**> Eixo Y** |
| Utilizar escala logarítmica |Selecione toouse uma escala logarítmica para Olá eixo y. |
| Unidades |Especifique unidades Olá para os valores de Olá devolvidos pela consulta Olá.  Estas informações são utilizadas toodisplay etiquetas no gráfico de Olá com a indicação de tipos de valor de Olá e, opcionalmente, para converter valores Olá.  Olá um tipo de unidade Especifica a categoria de Olá da unidade de Olá e define os valores do tipo de unidade atual Olá que estão disponíveis.  Se selecionar um valor em converter toothen Olá numérico valores são convertidos do Olá unidade atual tipo toohello converter tootype. |
| Etiqueta personalizada |Texto toodisplay para Olá Y seguinte toohello etiqueta do eixo de um tipo de unidade Olá.  Não se for especificada nenhuma etiqueta, apenas um tipo de unidade Olá é apresentado. |
| **Lista** | |
| Consulta |Toorun de consulta para obter a lista de Olá.  Contagem de Olá do número de Olá de registos devolvidos pela consulta Olá será apresentada. |
| Ocultar gráfico |Selecione o direito de toohello do toodisable Olá gráfico da coluna numérica Olá. |
| Ativar sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Cor |Cor de barras de Olá ou sparklines. |
| Operação |Operação tooperform para gráfico sparkline de Olá.  Consulte [definições comuns](#sparklines) para obter mais detalhes. |
| Nome e valor de separação |Delimitador de carácter único se quiser propriedade de texto de Olá tooparse em vários valores.  Consulte [definições comuns](#name-value-separator) para obter mais detalhes. |
| Consulta de navegação |Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Consulte [definições comuns](#navigation-query) para obter mais detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de Olá da primeira coluna de Olá da lista de Olá. |
| Valor |Toodisplay de texto na parte superior de Olá da segunda coluna de Olá da lista de Olá. |
| **Lista** |**> Limiares** |
| Ativar os limiares |Selecione tooenable limiares.  Consulte [definições comuns](#thresholds) para obter mais detalhes. |

## <a name="stack-of-line-charts-part"></a>Pilha da peça de gráficos de linha
Apresenta os três separado gráficos de linhas com várias séries por uma consulta de registo ao longo do tempo.

![Pilha de gráficos de linha](media/log-analytics-view-designer/view-stack-line-charts.png)

| Definição | Descrição |
|:--- |:--- |
| **Geral** | |
| Título de grupo |Texto toodisplay, Olá parte superior do Olá mosaico. |
| Novo grupo |Selecione toocreate um novo grupo na vista de Olá começando vista atual Olá. |
| Ícone |Imagem ficheiro toodisplay seguinte toohello resultado no cabeçalho de Olá. |
| **Gráfico 1<br>gráfico 2<br>gráfico 3** |**> Cabeçalho** |
| Título |Texto toodisplay, Olá parte superior do gráfico Olá. |
| Subtítulo do |Texto toodisplay em Olá título na parte superior de Olá de gráfico de Olá. |
| **Gráfico 1<br>gráfico 2<br>gráfico 3** |**Gráfico de linhas** |
| Consulta |Consulta toorun para gráfico de linhas de Olá.  propriedade primeiro Olá deve ser um valor e Olá segunda propriedade text um valor numérico.  Isto é normalmente uma consulta que utiliza Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta de Olá utiliza Olá **intervalo** palavra-chave, em seguida, Olá eixo x do gráfico Olá irá utilizar este intervalo de tempo.  Se a consulta de Olá não incluir Olá **intervalo** intervalos de palavra-chave e a hora a hora são utilizados para Olá eixo x. |
| **Gráfico** |**> Eixo Y** |
| Utilizar escala logarítmica |Selecione toouse uma escala logarítmica para Olá eixo y. |
| Unidades |Especifique unidades Olá para os valores de Olá devolvidos pela consulta Olá.  Estas informações são utilizadas toodisplay etiquetas no gráfico de Olá com a indicação de tipos de valor de Olá e, opcionalmente, para converter valores Olá.  Olá um tipo de unidade Especifica a categoria de Olá da unidade de Olá e define os valores do tipo de unidade atual Olá que estão disponíveis.  Se selecionar um valor em converter toothen Olá numérico valores são convertidos do Olá unidade atual tipo toohello converter tootype. |
| Etiqueta personalizada |Texto toodisplay para Olá Y seguinte toohello etiqueta do eixo de um tipo de unidade Olá.  Não se for especificada nenhuma etiqueta, apenas um tipo de unidade Olá é apresentado. |

## <a name="common-settings"></a>Definições comuns
Olá secções a seguir descreve as partes de visualização de tooseveral definições comuns.

### <a name="name-value-separator">Nome e valor de separação</a>
Delimitador de carácter único se quiser propriedade de texto de Olá tooparse por uma consulta de lista para valores múltiplos.  Se especificar um delimitador, pode fornecer nomes para cada campo separados por Olá mesmo delimitador na caixa de nome de Olá.

Por exemplo, considere uma propriedade denominada *localização* que incluídos como valores *Redmond edifício 41* e *Bellevue Building12*.  Pode especificar – para Olá nome & separador de valor e *cidade edifício* para Olá nome.  Isto seria analisar cada valor em duas propriedades chamadas *Cidade* e *edifício*.

### <a name="navigation-query">Consulta de navegação</a>
Consultar toorun quando o utilizador Olá seleciona um item na lista de Olá.  Utilize *{item selecionado}* tooinclude sintaxe Olá item Olá utilizador selecionado.

Por exemplo, se hello consulta tem uma coluna chamada *computador* e consulta de navegação de Olá *{item selecionado}*, uma consulta, tais como *computador = "MyComputer"* iria ser executado quando utilizador Olá selecionado um computador.  Se a consulta de navegação Olá é *tipo = eventos {item selecionado}* , em seguida, consulta de Olá *tipo = evento computador = "MyComputer"* iria ser executado.

### <a name="sparklines">Sparklines</a>
Um gráfico sparkline é um gráfico de linhas pequenas que ilustra o valor de Olá de uma entrada da lista ao longo do tempo.  Para visualização as partes com uma lista, pode selecionar se toodisplay um horizontal barra que indica Olá valor relativo de uma coluna numérica ou um gráfico sparkline que indica o valor ao longo do tempo.

Olá a tabela seguinte descreve as definições de Olá para sparklines.

| Definição | Descrição |
|:--- |:--- |
| Ativar Sparklines |Selecione toodisplay gráfico sparkline em vez de barras horizontais. |
| Operação |Se sparklines estiverem ativados, este é Olá operação tooperform em cada propriedade na Olá toocalculate Olá os valores da lista para gráfico sparkline de Olá.<br><br>-Última amostra: Último valor para a série de Olá ao longo do intervalo de tempo de Olá.<br>-Máximo: O valor máximo para série Olá ao longo do intervalo de tempo de Olá.<br>-Mínimo: O valor mínimo para série Olá ao longo do intervalo de tempo de Olá.<br>-Soma: Soma dos valores para a série de Olá ao longo do intervalo de tempo de Olá.<br>-Resumo: Utiliza Olá mesmo comando de medida como consulta Olá no cabeçalho de Olá. |

### <a name="thresholds">Limiares</a>
Limiares permitem-lhe toodisplay um item tooeach seguinte ícone coloridos numa lista dando-lhe um indicador de visual rápido dos itens que exceder um valor específico ou enquadram-se dentro de um intervalo específico.  Por exemplo, foi possível apresentar um ícone verde para itens com um valor aceitável, amarelo, se o valor de Olá se encontra num intervalo que indica um aviso e vermelho, se exceder um valor de erro.

Quando ativar os limiares de uma parte, tem de especificar um ou mais limiares.  Se o valor de Olá de um item é maior do que um valor de limiar e inferior ao valor de limiar seguinte Olá, esse cor é utilizado.  Se o item de Olá é superior ao valor de limiar, em seguida, mais elevado, esse cor está definido.   

Cada conjunto de limiar tem um limiar com um valor de **predefinido**.  Esta é a cor de Olá definida se não existem outros valores for excedidos.  Pode adicionar ou remover limiares clicando Olá  **+**  ou **x** botão.

Olá a tabela seguinte descreve as definições de Olá para tresholds.

| Definição | Descrição |
|:--- |:--- |
| Ativar os limiares |Selecione toodisplay que um toohello de ícone cor à esquerda de cada valor que indica que os limiares de toospecified relativo de estado de funcionamento. |
| Nome |Valor de limiar do nome tooidentify Olá. |
| Limiar |Valor de limiar de Olá.  cor de estado de funcionamento de Olá para cada item da lista é definida toohello cor de Olá maior valor de limiar excedido pelo valor do item de Olá.  Não há um limiar de predefinido que é a cor de Olá se não existem valores de limiar for excedidos. |
| Cor |Cor para o valor de limiar de Olá. |

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [pesquisas de registo](log-analytics-log-searches.md) toosupport consultas Olá partes de visualização.
