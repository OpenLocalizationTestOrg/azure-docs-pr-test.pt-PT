---
title: "aaaCreate visualiza dados tooanalyze na análise de registos do OMS | Microsoft Docs"
description: "Estruturador de vistas no Log Analytics permite-lhe toocreate personalizada vistas que são apresentadas no portal de Olá OMS e o Azure e contenham visualizações diferentes dos dados no repositório do Olá OMS. Este artigo contém uma descrição geral do estruturador de vistas e procedimentos para criar e editar vistas personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>Utilizar vistas personalizadas do estruturador de vistas toocreate na análise de registos
Olá estruturador de vistas no [Log Analytics](log-analytics-overview.md) permite-lhe toocreate vistas personalizadas na consola do OMS Olá que contêm visualizações diferentes dos dados no repositório do Olá OMS. Este artigo contém uma descrição geral do estruturador de vistas e procedimentos para criar e editar vistas personalizadas.

Outros artigos disponíveis para o estruturador de vistas são:

* [Mosaico referência](log-analytics-view-designer-tiles.md) -referência das definições de Olá para cada um dos Olá os mosaicos toouse disponível no seu vistas personalizadas.
* [Referência de parte de visualização](log-analytics-view-designer-parts.md) -referência das definições de Olá para cada um dos Olá os mosaicos toouse disponível no seu vistas personalizadas.

>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, as consultas em todas as vistas têm de ser escritas na Olá [novo idioma de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas as vistas que foram criadas para a área de trabalho de Olá foi atualizada será automtically convertido.

## <a name="concepts"></a>Conceitos
Vistas criadas com o estruturador de vistas de Olá contém elementos Olá Olá a tabela seguinte.

| Parte | Descrição |
|:--- |:--- |
| Mosaico |Apresentado no dashboard de descrição geral da análise do registo principal Olá.  Inclui um visual resumir de informações de Olá incluídas no Olá vista personalizada.  Diferentes tipos de mosaico fornecem visualizações diferentes dos registos no repositório do Olá OMS.  Clique em Olá Olá tooopen do mosaico vista personalizada. |
| Vista personalizada |Apresentado quando o utilizador Olá clica na Olá mosaico.  Contém um ou mais peças de visualização. |
| Partes de visualização |Visualização de dados no repositório OMS Olá com base num ou vários [pesquisas de registo](log-analytics-log-searches.md).  A maioria das partes irão incluir um cabeçalho que fornece uma visualização de alto nível e uma lista de resultados principais Olá.  Tipos de outra parte fornecem visualizações diferentes dos registos no repositório do Olá OMS.  Clique em elementos de Olá parte tooperform uma pesquisa de registo que fornece registos detalhados. |

![Descrição geral do Designer de vista](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>Adicione a área de trabalho do estruturador de vistas tooyour
Enquanto o estruturador de vistas está em pré-visualização, tem de adicionar-área de trabalho tooyour selecionando **funcionalidades de pré-visualização** no Olá **definições** secção do portal do OMS Olá.

![Ativar a pré-visualização](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>Criação e edição de vistas
### <a name="create-a-new-view"></a>Criar uma nova vista
Abra uma nova vista no Olá **estruturador de vistas** ao clicar no estruturador de vistas de Olá mosaico no dashboard do Olá principal OMS.

![Mosaico de vista de Designer](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>Editar uma vista existente
tooedit uma vista existente na Olá estruturador de vistas, vista Olá aberta clicando no seu mosaico no dashboard do Olá principal OMS.  Em seguida, clique em Olá **editar** botão tooopen Olá vista no estruturador de vistas de Olá.

![Editar uma vista](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>Clonar uma vista existente
Ao clonar uma vista, cria uma nova vista e abre-o no Olá estruturador de vistas.  nova vista de Olá terão Olá mesmo nome como Olá original com "Copiar" toohello anexado fim.  tooclone uma vista, abra Olá vista existente ao clicar no seu mosaico no dashboard do Olá principal OMS.  Em seguida, clique em Olá **Clone** botão tooopen Olá vista no estruturador de vistas de Olá.

![Clonar uma vista](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>Eliminar uma vista existente
toodelete uma vista existente, vista Olá aberta clicando no seu mosaico no dashboard do Olá principal OMS.  Em seguida, clique em Olá **editar** botão tooopen Olá vista no estruturador de vistas de Olá e clique em **Eliminar vista**.

![Eliminar uma vista](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>Exportar uma vista existente
Pode exportar um ficheiro JSON tooa de vista que pode importar para outra área de trabalho ou utilize um [modelo Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).  tooexport uma vista existente, vista Olá aberta clicando no seu mosaico no dashboard do Olá principal OMS.  Em seguida, clique em Olá **exportar** botão toocreate um ficheiro na pasta de transferência do browser Olá.  nome de Olá do ficheiro de Olá será o nome de Olá da vista de Olá com a extensão de Olá *omsview*.

![Exportar uma vista](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>Importar uma vista existente
Pode importar um *omsview* ficheiro que tenha exportado a partir de outro grupo de gestão.  em primeiro lugar, tooimport uma vista existente, crie uma nova vista.  Em seguida, clique em Olá **importação** botão e selecione Olá *omsview* ficheiro.  configuração de Olá no ficheiro de Olá será copiada numa vista existente Olá.

![Exportar uma vista](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>Trabalhar com o estruturador de vistas
Olá estruturador de vistas tem três painéis.  Olá **Design** painel representa vista personalizada Olá.  Quando adicionar os mosaicos e partes do Olá **controlo** painel toohello **Design** painel são adicionados toohello vista.  Olá **propriedades** painel apresentará Olá as propriedades de mosaico Olá ou peça selecionada.

![Estruturador de Vista](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>Configurar o mosaico de vista
Uma vista personalizada pode ter apenas um único mosaico.  Selecione Olá **mosaico** separador Olá **controlo** painel tooview Olá atual mosaico ou selecione um alternativo.  Olá **propriedades** painel irá apresentar as propriedades de Olá para mosaico atual Olá.  Configurar propriedades de mosaico Olá toohello de acordo com informações em Olá detalhadas [mosaico referência](log-analytics-view-designer-tiles.md) e clique em **aplicar** toosave alterações.

### <a name="configure-visualization-parts"></a>Configurar partes de visualização
Uma vista pode incluir qualquer número de partes de visualização.  Selecione Olá **vista** separador e, em seguida, uma visualização de parte tooadd toohello vista.  Olá **propriedades** painel irá apresentar as propriedades de Olá para parte Olá selecionado.  Configurar Olá vista detalhada de propriedades toohello de acordo com as informações no Olá [referência de parte de visualização](log-analytics-view-designer-parts.md) e clique em **aplicar** toosave alterações.

### <a name="delete-a-visualization-part"></a>Eliminar uma peça de visualização
Pode remover uma parte de visualização da vista de Olá clicando Olá **X** botão no Olá canto superior direito da peça de Olá.

### <a name="rearrange-visualization-parts"></a>Reorganizar partes de visualização
Vistas tem apenas uma linha de partes de visualização.  Reorganizar partes existentes numa vista, clicando e arrastando-los tooa nova localização.

## <a name="next-steps"></a>Passos seguintes
* Adicionar [mosaicos](log-analytics-view-designer-tiles.md) tooyour de vista personalizada.
* Adicionar [partes de visualização](log-analytics-view-designer-parts.md) tooyour de vista personalizada.
