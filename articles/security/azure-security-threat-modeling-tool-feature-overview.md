---
title: "aaaMicrosoft ferramenta modelação de ameaça - Azure | Microsoft Docs"
description: "Saiba mais sobre todas as funcionalidades de Olá disponíveis no Olá ferramenta modelação de ameaça"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Descrição geral da funcionalidade de ferramenta modelação de ameaça

Estamos satisfeitos por que escolheu toouse Olá ferramenta modelação de ameaça para a necessidades de modelação de ameaça! Se ainda não o feito, visite  **[introdução Olá ferramenta modelação de ameaça](./azure-security-threat-modeling-tool-getting-started.md)**  Noções básicas de Olá toolearn.

> A nossa ferramenta é atualizada frequentemente, por isso este guia, muitas vezes, toosee nosso funcionalidades e melhorias mais recentes.

Clicar no botão de "Criar um novo modelo" Olá abre uma página de início em branco, semelhante toohello imagem abaixo:

![Página de início em branco](./media/azure-security-threat-modeling-tool/tmtstart.png)

Utilizar o modelo de ameaça Olá criados pela nossa equipa em Olá  **[introdução](./azure-security-threat-modeling-tool-getting-started.md)**  exemplo, vamos Consulte todas as funcionalidades de Olá disponíveis na ferramenta de Olá ainda hoje.

![Modelo de ameaça básico](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Navegação

Antes de explorar as funcionalidades integradas Olá, vamos abordar componentes principais Olá encontrados na ferramenta de Olá

### <a name="menu-items"></a>Itens de menu

experiência de Olá deve ser produtos da Microsoft tooother semelhantes. Vamos começar por percorrer os itens de menu de nível superior de Olá:

![Itens de menu](./media/azure-security-threat-modeling-tool/menuitems.png)

| Etiqueta                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Ficheiro** | <ul><li>Abrir, guardar e fechar ficheiros</li><li>Contas de início de sessão In/Out do OneDrive</li><li>Ligações de partilha (vista + editar)</li><li>Ver informações de ficheiro</li><li>Aplique o novo modelo tooExisting modelos</li></ul> |
| **Editar** | Anulação/Refazer ações, como também uma cópia, colar e delete |
| **Vista** | <ul><li>Alternar entre **Analysis** e **Design** vistas</li><li>Abra windows fechados (e.g.stencils, propriedades de elemento e mensagens)</li><li>Repor as definições de toodefault de esquema</li></ul> |
| **Diagrama** | Adicionar/eliminar diagramas e navegar pelas "Separadores" de diagramas |
| **Relatórios** | Criar HTML relatórios tooshare com outras pessoas |
| **Ajuda** | Orienta toohelp é utilizar a ferramenta de Olá |

ícones de Olá são os atalhos para os menus de nível superior de Olá:

| Ícone                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Abrir** | É aberto um novo ficheiro |
| **Guardar** | Guarda o ficheiro atual |
| **Design** | Entrar em vista de estrutura, onde pode criar modelos |
| **Analisar** | Mostra gerado ameaças e as respetivas propriedades |
| **Adicionar diagrama** | Adiciona o novo diagrama (semelhante toonew separadores no Excel) |
| **Eliminar diagrama** | Elimina o diagrama atual |
| **Cortar/copiar/colar** | Cópias/cuts/cola sobre elementos |
| **Anulação/Refazer** | Ações anular/efectuar novamente |
| **Ampliar / reduzir** | Amplia inteira dentro ou fora do diagrama de Olá para uma melhor vista |
| **Comentários** | Abre Olá fórum MSDN |

### <a name="canvas"></a>Tela

espaço de olá onde pode arrastar e largar os elementos no. Arrastar e largar é Olá mais rápida e modelos de toobuild de forma mais eficientes. Também pode clique com o botão direito e selecione menu Olá, que adiciona genéricas versões dos elementos de Olá que estiver a utilizar, conforme mostrado abaixo.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Remover stencil Olá numa tela Olá

![Largar tela](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Clicar no stencil Olá

![Propriedades de elemento](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Stencils

Onde pode encontrar todos os stencils toouse disponível com base no modelo de Olá selecionado. Se não conseguir localizar os elementos à direita Olá, tente utilizar outro modelo ou modificar um toofit às suas necessidades. Geralmente, deve ser capaz de toofind uma combinação de categorias, como Olá aqueles abaixo:

| Nome de stencil                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Processo** | Aplicações, plug-ins do Browser, Threads, máquinas virtuais |
| **Interactor externo** | Fornecedores de autenticação, os Browsers, utilizadores, aplicações Web |
| **Arquivo de dados** | Registo de ficheiros, bases de dados de configuração de cache, armazenamento, |
| **Fluxo de dados** | Binários, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, com o nome Pipe, RPC/DCOM, SMB, UDP |
| **Limites de linha/limite de fidedignidade** | Redes empresariais, Internet, máquina, Sandbox, de modo Kernel/utilizador |

### <a name="notesmessages"></a>Notas/mensagens

| Componente                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Mensagens** | Lógica de ferramenta interno que os utilizadores de alertas sempre que há um erro, como não existem fluxos de dados entre elementos |
| **Notas** | Notas de ficheiro toohello adicionado por equipas de engenharia completamente Olá design e rever o processo manuais |

### <a name="element-properties"></a>Propriedades de elemento

Estes variam consoante a elementos Olá selecionados. Para além dos limites de fidedignidade, todos os outros elementos contenham 3 seleções gerais:

| Propriedade de elemento                               | Detalhes      |
| --------------------------------------- | ------------ |
| **Nome** | Útil para atribuir nomes a sua toobe processos, arquivos, interactors e fluxos facilmente reconhecido |
| **Fora do âmbito** | Se selecionado, o elemento de Olá é retirado matriz de geração de ameaça Olá (não recomendado) |
| **Razão para fora do âmbito** | Os utilizadores de toolet do campo justificação saber porquê fora do âmbito selecionado |

As propriedades são alteradas em cada categoria de elemento. Clique em cada elemento tooinspect Olá as opções disponíveis, ou abra Olá modelo toolearn mais. Vamos colocar no funcionalidades Olá.

## <a name="welcome-screen"></a>Ecrã de boas-vindas

ecrã de boas-vindas Olá é Olá primeira coisa que vê se abrir a aplicação Olá.

### <a name="open-a-model"></a>Abra um modelo

Posicionado sobre o botão "Abrir um modelo" mostra 2 opções ocultas: "Aberta de neste computador" e "Aberta do OneDrive." Olá abre pela primeira vez o ecrã de ficheiros abertos Olá, enquanto Olá segundo leva-o através do processo de início de sessão Olá para o OneDrive, permitindo-lhe toopick pastas e ficheiros após uma autenticação com êxito.

![Modelo aberto](./media/azure-security-threat-modeling-tool/openmodel.png)

![Abra do computador ou do OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Comentários, problemas e sugestões

A seleção desta opção irá demorar toohello fóruns do MSDN para SDL ferramentas. É toocheck uma excelente forma saída que outras pessoas são indicar sobre a ferramenta de Olá, incluindo soluções e ideias de novo.

![Comentários](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Vista de estrutura

Sempre que abrir ou criar um novo modelo, será direcionado toohello vista de estrutura.

### <a name="adding-elements"></a>A adição de elementos

Existem 2 formas tooadd elementos na grelha de Olá:

- **Arrastar e largar** – arraste grelha de toohello de elemento pretendido Olá, em seguida, utilize Olá elemento propriedades tooprovide obter informações adicionais.
- **Clique com o botão direito** – clique em qualquer lugar em grelha Olá e selecione a partir do menu de lista pendente de Olá. Será apresentada uma representação genérica de que o elemento no ecrã de Olá.

### <a name="connecting-elements"></a>Elementos de ligação

Existem 2 formas tooconnect elementos na ferramenta de Olá:

- **Arrastar e largar** – arraste grelha de toohello Olá pretendida do fluxo de dados e ligar-se ambos os elementos de adequado toohello termina.
- **Clique em + deslocar** – clique no primeiro elemento de Olá (enviar dados), prima e mantenha premido Olá Shift chave e o segundo elemento de Olá selecione (receber dados). Clique com o botão direito e selecione "Ligar". Se estiver a utilizar um fluxo de dados bidirecional, ordem de Olá não é tão importante.

### <a name="properties"></a>Propriedades

Mostra todas as propriedades de Olá que podem ser modificadas no stencils Olá colocados no diagrama de Olá. Propriedades de Olá toosee, basta clicar no stencil Olá e informações de Olá preenchidas em conformidade. exemplo de Olá abaixo mostra antes e depois de um "base de dados" stencil é arrastar diagrama Olá:

#### <a name="before"></a>Antes de

![Antes de](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Após

![Após](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>Mensagens

Se criar um modelo de ameaça e se esqueça de fluem de dados de tooconnect tooelements, janela de mensagem de Olá notifica tooact. Pode escolher tooignore-lo ou siga Olá problema de Olá toofix de instruções. 

![Mensagens](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Notas

Mudar os separadores de mensagens tooNotes permite todos os seus pensamentos de modo tooadd notas tooyour diagrama toocapture

## <a name="analysis-view"></a>Vista de análise

Depois de concluir a criação do diagrama, comutador através de vista tooanalysis ao vai toohello seleções de menu superior e escolha a paleta de paint de toohello seguinte do Olá Lupa.

![Vista de análise](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Seleção de ameaça gerado

Ao clicar numa ameaça, pode tirar partido das três funções únicas:

| Funcionalidade                               | Informações      |
| --------------------------------------- | ------------ |
| **Indicador de leitura** | <p>Ameaças agora está marcada como de leitura, que pode facilmente ajudar a manter um registo dos itens de Olá que já frequentou através de</p><p>![Indicador Unread/leitura](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Interação foco** | <p>Interação no diagrama de Olá que pertencem a ameaça de toothat é realçada</p><p>![Interação foco](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Propriedades de ameaça** | <p>Informações adicionais sobre ameaças Olá são preenchidas na janela de propriedades de ameaça Olá</p><p>![Propriedades de ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Alteração da prioridade

Alterar o nível de prioridade de Olá de cada ameaça gerado também altera as respetivas toomake cores-ameaças de prioridade alta, média e baixa tooidentify fácil.

![Alteração da prioridade](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Campos de editáveis de propriedades de ameaça

Como mostrado na imagem de Olá acima, os utilizadores podem alterar as informações de Olá geradas pela ferramenta de Olá um também adicionar campos de toocertain de informações, tais como justificação. Estes campos são gerados pelo modelo de Olá, pelo que se precisar de mais informações para cada ameaça, pode toomake encorajados modificações.

![Propriedades de ameaça](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Relatórios

Quando tiver terminado a alteração de prioridades e atualização Olá estado de cada gerado ameaça, pode guardar o ficheiro de Olá e/ou imprimir um relatório por ficar demasiado "relatório" e, em seguida, "Criar relatório completo." Relatório de Olá tooname irá ser mais frequentes e quando o fizer, deverá ver algo semelhante imagem toohello abaixo:

![Relatório](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Passos seguintes

toocontribute um modelo para a Comunidade Olá, visite tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  página. **[Transferir](https://aka.ms/tmtpreview)**  Olá ferramenta tooget iniciada atualmente.
