---
title: "Sincronização do Azure AD Connect: Noções sobre a arquitetura de Olá | Microsoft Docs"
description: "Este tópico descreve a arquitetura de Olá de sincronização do Azure AD Connect e explica Olá termos utilizados."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Sincronização do Azure AD Connect: Noções sobre a arquitetura de Olá
Este tópico abrange a arquitetura básica do Olá para sincronização do Azure AD Connect. Em muitos aspetos, é semelhante tooits antecessores, MIIS 2003, ILM 2007 e FIM 2010. Sincronização do Azure AD Connect é a evolução de Olá destas tecnologias. Se estiver familiarizado com qualquer uma destas tecnologias anterior, o conteúdo de Olá deste tópico estará familiarizado tooyou bem. Se forem toosynchronization nova, em seguida, este tópico é que o utilizador. No entanto não é um detalhes de Olá tooknow requisito de toobe este tópico bem-sucedida efetuar personalizações tooAzure AD Connect sincronização (motor de sincronização chamado neste tópico).

## <a name="architecture"></a>Arquitetura
motor de sincronização de Olá cria uma vista integrada dos objetos que estão armazenados em várias origens de dados ligada e gere informações de identidade dessas origens de dados. Esta vista integrada é determinada pelo informações de identidade de Olá obtidas a partir de origens de dados e um conjunto de regras que determinam como tooprocess estas informações.

### <a name="connected-data-sources-and-connectors"></a>Conetores e origens de dados
o motor de sincronização de Olá processa as informações de identidade de repositórios de dados diferentes, tais como o Active Directory ou uma base de dados do SQL Server. Cada repositório de dados que organiza os respetivos dados num formato semelhante a base de dados e que fornece métodos padrão de acesso de dados é um potencial candidato de origem de dados para o motor de sincronização de Olá. repositórios de dados de Olá que estão sincronizados com o motor de sincronização são denominados **ligado a origens de dados** ou **ligado diretórios** (CD).

o motor de sincronização de Olá encapsula interação com uma origem de dados ligada dentro de um módulo chamado um **conector**. Cada tipo de origem de dados ligada tem um conector específico. Olá conector traduz uma operação necessária num formato de Olá Olá dados ligada compreende origem.

Conectores efetuar chamadas de API tooexchange informações de identidade (de leitura e escrita) com uma origem de dados ligada. Também é possível tooadd um Conetor personalizado utilizando Olá conectividade extensível framework. Olá ilustração seguinte mostra como um conector se liga um motor de sincronização de toohello de origem de dados ligada.

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Podem do fluxo de dados em qualquer direção, mas não é possível flua em ambas as direções em simultâneo. Por outras palavras, um conector pode ser configurado tooallow tooflow de dados do motor de toosync de origem de dados ligada Olá ou a partir da origem de dados ligada de toohello de motor de sincronização, mas apenas um dessas operações pode ocorrer num dado momento para um objeto e um atributo. direção de Olá pode ser diferente para diferentes objetos e atributos diferentes.

tooconfigure um conector, especifique que pretende que o toosynchronize de tipos de objeto de Olá. Especificar os tipos de objeto Olá define o âmbito de Olá de objetos que estão incluídos no processo de sincronização de Olá. Olá passo seguinte consiste em tooselect Olá atributos toosynchronize, que é conhecido como uma lista de inclusão de atributo. Estas definições podem ser alteradas a qualquer altura nas regras de negócio resposta toochanges tooyour. Quando utiliza o Assistente de instalação do Azure AD Connect Olá, estas definições são configuradas por si.

origem de dados ligada do tooexport objetos tooa, lista de inclusão de atributo Olá tem de incluir, pelo menos, Olá mínimo atributos toocreate necessário um objeto específico escreva uma origem de dados ligada. Por exemplo, Olá **sAMAccountName** atributo tem de ser incluído no tooexport de lista de inclusão de atributo Olá de um utilizador objeto tooActive diretório porque todos os objetos de utilizador no Active Directory tem de ter um **sAMAccountName**  atributo definido. Novamente, o Assistente de instalação de Olá efetuar esta configuração para si.

Se a origem de dados ligada Olá utiliza estruturais componentes, tais como objetos tooorganize partições ou de contentores, pode limitar as áreas de Olá na origem de dados ligada Olá, que são utilizadas para uma determinada solução.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Estrutura interna de espaço de nomes de motor de sincronização de Olá
espaço de nomes de motor de sincronização completa de Olá é constituído por dois espaços de nomes que armazenam informações de identidade Olá. Olá dois espaços de nomes são:

* espaço de conector Olá (CS)
* Olá metaverso (MV)

Olá **espaço de conector** é uma área de transição que contém representações Olá designado objetos a partir de um atributos de origem e Olá de dados ligada especificada na lista de inclusão de atributo Olá. o motor de sincronização de Olá utiliza toodetermine de espaço de conector Olá o que mudou nas Olá ligado origem e toostage entradas alterações de dados. o motor de sincronização de Olá também utiliza toostage de espaço de conector Olá alterações para a origem de dados ligada toohello de exportação de saída. o motor de sincronização de Olá mantém um espaço de conector distintos como uma área de transição para cada conector.

Através da utilização de uma área de transição, o motor de sincronização de Olá permanece independente Olá ligado de origens de dados e não é afetada por disponibilidade e acessibilidade. Como resultado, pode processar as informações de identidade em qualquer altura utilizando dados Olá na área de transição de Olá. o motor de sincronização de Olá pode pedir apenas Olá as alterações feitas no interior da origem de dados ligada Olá desde Olá última de comunicação de sessão terminada ou push apenas Olá alterações tooidentity informações que Olá origem de dados ligada não ainda recebeu, o que reduz o tráfego de rede de Olá entre o motor de sincronização de Olá e origem de dados ligada Olá.

Além disso, o motor de sincronização armazena informações de estado sobre todos os objetos que prepara-lo no espaço de conector Olá. Quando são recebidos novos dados, o motor de sincronização avalia sempre se os dados de Olá já foram sincronizados.

Olá **metaverso** é uma área de armazenamento que contém informações de identidade Olá agregado de várias origens de dados ligada, criando uma vista única global, integrada de todos os objetos combinadas. Objetos de Metaverso são criados com base nas informações de identidade Olá que são obtidas a partir de origens de dados de Olá ligado e um conjunto de regras que permitem o processo de sincronização de Olá toocustomize.

Olá ilustração seguinte mostra espaço de nomes de espaço de conector de Olá e espaço de nomes de metaverso de Olá dentro do motor de sincronização de Olá.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Objetos de identidade do motor de sincronização
objetos de Olá no motor de sincronização de Olá são representações de qualquer um dos objetos de origem de dados ligada Olá ou hello vista integrada que o motor de sincronização tem desses objetos. Todos os objetos do motor de sincronização tem de ter um identificador exclusivo global (GUID). GUIDs fornecem integridade dos dados e rápidas relações entre objetos.

### <a name="connector-space-objects"></a>Objetos de espaço de conector
Quando o motor de sincronização comunica com uma origem de dados ligada, lê as informações de identidade Olá na origem de dados ligada Olá e utiliza essa toocreate informações uma representação de objeto de identidade Olá no espaço de conector Olá. Não é possível criar ou eliminar estes objetos individualmente. No entanto, pode eliminar manualmente todos os objetos num espaço de conector.

Todos os objetos no espaço de conector Olá tem dois atributos:

* Um identificador exclusivo global (GUID)
* Um nome exclusivo (também conhecido como DN)

Se ligado Olá origem de dados atribui um objeto de toohello atributo exclusivo e objetos no espaço de conector Olá também podem ter um atributo âncora. atributo de âncora Olá identifica exclusivamente um objeto na origem de dados ligada Olá. o motor de sincronização de Olá utiliza Olá âncora toolocate Olá correspondente representação deste objeto na origem de dados ligada Olá. Motor de sincronização assume que âncora Olá de um objeto nunca alterações ao longo da duração Olá de objeto de Olá.

Muitos dos conectores Olá utilizam toogenerate um identificador exclusivo conhecidos uma âncora automaticamente para cada objeto quando for importado. Por exemplo, Olá conector do Active Directory utiliza Olá **objectGUID** atributo para uma âncora. Para origens de dados que não fornecem um identificador exclusivo claramente definido, pode especificar a geração de âncora como parte da configuração do conector Olá.

Nesse caso, âncora Olá baseia-se de um ou mais atributos exclusivos de um objeto de tipo, nem de as alterações e que exclusivamente identifica o objeto de Olá no espaço de conector Olá (por exemplo, um número de empregado ou um ID de utilizador).

Um objeto de espaço de conector pode ser um dos seguintes Olá:

* Um objeto de teste
* Um marcador de posição

### <a name="staging-objects"></a>Objetos de transição
Um objeto de transição representa uma instância de Olá designado tipos de objeto de origem de dados ligada Olá. Além disso toohello GUID e o nome distinto Olá, um objeto de teste tem sempre um valor que indica o tipo de objeto Olá.

Objetos de teste que tenham sido importados sempre de ter um valor para o atributo de âncora Olá. Objetos de teste que foram recentemente aprovisionados pelo motor de sincronização e estão no processo de Olá de que está a ser criado na origem de dados ligada Olá não tem um valor para o atributo de âncora Olá.

Objetos de transição também transportem os valores atuais de atributos de negócio e as informações operacionais necessários pelo motor tooperform Olá sincronização do processo de sincronização. Informações operacionais incluem sinalizadores que indicam o tipo de Olá das atualizações que são testados nos Olá objeto de teste. Se um objeto de teste tiver recebido novas informações de identidade da origem de dados ligada Olá que ainda não foram processada, objeto Olá está assinalado como **importação pendente**. Se um objeto de teste tiver novas informações de identidade que ainda não foi exportado toohello origem de dados ligada, está assinalado como **pendentes exportação**.

Um objeto de teste pode ser um objeto de importação ou um objeto de exportação. o motor de sincronização de Olá cria um objeto de importação utilizando as informações do objeto recebidas a partir da origem de dados ligada Olá. Quando o motor de sincronização recebe informações sobre a existência de Olá de um novo objeto a que corresponda a um dos tipos de objeto de Olá selecionados na Olá conector, cria um objeto de importação no espaço de conector Olá como uma representação do objeto de Olá na origem de dados ligada Olá.

Olá seguinte ilustração mostra um objeto de importação que representa um objeto na origem de dados ligada Olá.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

motor de sincronização de Olá cria um objeto de exportação utilizando as informações de objetos no metaverso Olá. Os objetos de exportação são origem de dados ligada toohello exportado durante Olá próxima sessão de comunicação. Perspetiva Olá do motor de sincronização de Olá, objetos de exportação não existe na origem de dados ligada Olá ainda. Por conseguinte, o atributo de âncora Olá para um objeto de exportação não está disponível. Depois de receber o objeto de Olá do motor de sincronização, a origem de dados ligada Olá cria um valor exclusivo para o atributo de âncora Olá do objeto de Olá.

Olá ilustração seguinte mostra como é criado um objecto de exportação utilizando as informações de identidade no metaverso Olá.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

motor de sincronização de Olá confirma que a exportação de Olá do objeto de Olá por objeto Olá da origem de dados ligada Olá voltar a importar. Exportar objetos tornar-se importar objetos quando o motor de sincronização recebe-los durante a importação de seguinte Olá do que a origem de dados ligada.

### <a name="placeholders"></a>Marcadores de posição
o motor de sincronização de Olá utiliza objetos de toostore um espaço de nomes simples. No entanto, algumas origens de dados como o Active Directory utilizam um espaço de nomes hierárquico. tootransform informações a partir de um espaço de nomes hierárquica para um espaço de nomes simples, o motor de sincronização utiliza hierarquia de Olá toopreserve de marcadores de posição.

Cada marcador de posição representa um componente (por exemplo, uma unidade organizacional), do nome de hierárquica de um objeto que não tenha sido importado para o motor de sincronização, mas é necessário tooconstruct Olá hierárquica nome. Estes preencher lacunas criadas pelo referências tooobjects de origem de dados de Olá ligado não são objetos no espaço de conector Olá de teste.

motor de sincronização de Olá também utiliza objetos de toostore referenciado marcadores de posição que ainda não tiverem sido importados. Por exemplo, se a sincronização é configurado tooinclude Olá manager o atributo para Olá *Abbie Spencer* de objeto e hello valor recebido é um objeto que não foi importado ainda, tal como *CN = Nogueira Sperry, CN = utilizadores, DC = fabrikam, DC = com*, informações do Gestor de Olá são armazenadas como marcadores de posição no espaço de conector Olá. Se o objecto do Gestor de Olá mais tarde é importado, objeto de marcador de posição de Olá é substituído pela Olá objeto que representa o Gestor de Olá de teste.

### <a name="metaverse-objects"></a>Objetos de Metaverso
Um objeto de metaverso contém Olá agregado vista desse motor de sincronização tem de Olá objetos no espaço de conector Olá de teste. Motor de sincronização cria objetos de metaverso utilizando informações Olá em objetos de importação. Vários objetos de espaço de conector podem ser objeto de metaverso único tooa ligado, mas um objeto de espaço de conector não pode ser toomore ligado a um objeto de metaverso.

Objetos de Metaverso não podem ser manualmente criados ou eliminados. o motor de sincronização de Olá elimina automaticamente os objetos de metaverso que não dispõe de um objeto de espaço de conector de tooany de ligação no espaço de conector Olá.

objetos de toomap dentro de um ligado origem tooa correspondente objeto tipo de dados dentro do metaverso Olá, o motor de sincronização fornece um esquema extensível com um conjunto predefinido de tipos de objetos e atributos associados. Pode criar novos tipos de objeto e os atributos de objetos de metaverso. Os atributos podem ser único ou com múltiplos valores e tipos de atributo Olá podem ser cadeias, referências, números e os valores booleanos.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relações entre objetos de transição e objetos de metaverso
Dentro do espaço de nomes do motor do sincronização de Olá, o fluxo de dados de Olá está ativado por relação de ligação de Olá entre objetos de transição e objetos de metaverso. Uma transição de objeto que é o objeto de metaverso tooa ligado é chamado um **associado ao objeto** (ou **objecto do conector**). Um objeto de teste que não é o objeto de metaverso tooa ligado é chamado um **desagregado objeto** (ou **objetos de seccionador**). termos de Olá associado e desassociada são toonot preferencial confunda com Olá conectores responsáveis por importar e exportar dados a partir de um diretório ligado.

Marcadores de posição nunca são objeto de metaverso tooa ligado

Um objeto associado a um é composto por um objeto de transição e o respetivo objeto de metaverso único tooa relação ligado. Objetos associados são utilizados toosynchronize valores de atributos entre um objeto de espaço de conector e um objeto de metaverso.

Quando um objeto de transição torna-se um objeto associado ao durante a sincronização, os atributos possam circular entre Olá objeto e o objeto de metaverso Olá de teste. Fluxo de atributos é bidirecional e é configurado utilizando regras de atributo de importação e exportação atributo regras.

Um objeto de espaço de conector única pode ser objeto de metaverso um tooonly ligado. No entanto, cada objeto de metaverso pode ser objetos de espaço de conector toomultiple ligado no mesmo Olá ou nos espaços de conector diferentes, conforme mostrado na seguinte ilustração de Olá.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Olá ligados relação entre Olá objeto de teste e um objeto de metaverso é persistente e pode ser removido apenas por regras que especificar.

Um objeto disjoined é um objeto de teste que não é o objeto de metaverso tooany ligado. atributo de Olá valores de um objeto disjoined não são processados qualquer adicional no metaverso Olá. Olá atributo valores do Olá objeto correspondente na origem de dados ligada Olá não são atualizados pelo motor de sincronização.

Ao utilizar objetos desagregados, pode armazenar as informações de identidade no motor de sincronização e processá-la mais tarde. Manter um objeto de teste como um objeto disjoined no espaço de conector Olá tem muitas vantagens. Porque o sistema Olá já tiver testado Olá necessário obter informações sobre este objeto, não é necessário toocreate uma representação deste objeto novamente durante Olá importar junto da origem de dados ligada Olá. Desta forma, o motor de sincronização tem sempre um instantâneo completo Olá ligados da origem de dados, mesmo se não houver nenhuma origem de dados ligada toohello de ligação atual. Objetos desagregados podem ser convertidos em objetos associados e vice versa, consoante as regras de Olá que especificou.

É criado um objeto de importação como um objeto disjoined. Um objeto de exportação tem de ser um objeto associado. lógica de sistema Olá impõe a esta regra e elimina todos os objetos de exportação não é um objeto associado.

## <a name="sync-engine-identity-management-process"></a>Processo de gestão de identidade de motor de sincronização
processo de gestão de identidade Olá controla a forma como as informações de identidade são atualizadas entre origens de dados diferentes. Gestão de identidades ocorre em três processos:

* Importar
* Sincronização
* Exportar

Durante o processo de importação de Olá, o motor de sincronização avalia Olá receber as informações de identidade de uma origem de dados ligada. Quando são detetadas alterações, este cria novos objetos de transição ou objetos transição existentes no espaço de conector Olá para a sincronização de atualizações.

Durante o processo de sincronização de Olá, o motor de sincronização das atualizações Olá metaverso tooreflect as alterações ocorridas no espaço de conector Olá e atualiza Olá conector espaço tooreflect alterações ocorridas no metaverso Olá.

Durante o processo de exportação de Olá, motor de sincronização envia as alterações que são testados nos objetos de teste e que estão sinalizadas como pendente de exportação.

Olá seguinte ilustração mostra onde cada um dos processos de Olá ocorre como fluxos de informações de identidade do tooanother da origem de dados ligada um.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Processo de importação
Durante o processo de importação de Olá, o motor de sincronização avalia atualizações tooidentity informações. Motor de Sincronização compara as informações de identidade Olá recebidas a partir da origem de dados ligada Olá com informações de identidade Olá sobre um objeto de transição e determina se Olá objeto de teste necessita de atualizações. Se for Olá tooupdate necessário objeto com novos dados de teste, Olá objeto de transição está assinalado como pendente importar.

Por objetos no espaço de conector Olá antes da sincronização de teste, o motor de sincronização pode processar apenas Olá informações de identidade que foi alterado. Este processo fornece Olá seguintes vantagens:

* **Sincronização eficiente**. quantidade de Olá de processamento durante a sincronização de dados é minimizada.
* **A ressincronização eficiente**. Pode alterar como o motor de sincronização processa as informações de identidade sem restabelecer a ligação origem de dados de toohello do Olá sincronização motor.
* **Sincronização de toopreview oportunidade**. Pode pré-visualizar tooverify de sincronização que sua pressupostos sobre o processo de gestão de identidade Olá estão corretos.

Para cada objeto especificado num Olá conector, o motor de sincronização de Olá tenta primeiro toolocate uma representação de objeto de Olá no espaço de conector Olá do Olá conector. Motor de sincronização analisa todos os objetos de testes no espaço de conector Olá e tenta toofind um objeto de transição correspondente que tem um atributo âncora correspondente. Se nenhum objeto de teste existente tem uma correspondência ancorar atributo, sincronizar motor tenta toofind um objeto de transição correspondente com Olá nome mesmo único.

Quando o motor de sincronização encontra um objeto de teste que corresponde ao nome único, mas não por âncora, hello especial ocorre seguinte comportamento:

* Se o objeto de Olá localizado no espaço de conector Olá não tem nenhuma âncora, em seguida, motor de sincronização remove este objeto do espaço de conector Olá e marcas Olá objeto de metaverso é tooas ligado **novamente executada a próxima sincronização de aprovisionamento**. Em seguida, cria um novo objeto de importação Olá.
* Se o objeto de Olá localizado no espaço de conector Olá tiver uma âncora de, em seguida, motor de sincronização parte do princípio de que este objeto foi mudado ou eliminado no diretório ligado Olá. Atribui um nome distinto temporário, os novo para o objeto de espaço de conector Olá, para que pode testar objeto Olá de entrada. Olá objeto antigo de, em seguida, fica **transitório**, aguardar Olá conector tooimport Olá mudar o nome ou eliminação tooresolve Olá situação.

Se o motor de sincronização localiza um objeto de teste que corresponde ao objecto de toohello especificado no Olá conector, determina o tipo de tooapply de alterações. Por exemplo, motor de sincronização pode mudar o nome ou eliminar o objeto de Olá na origem de dados ligada Olá ou que apenas pode atualizar os valores de atributo do objeto de Olá.

Objetos de teste com dados atualizados são marcados como pendente importar. Estão disponíveis diferentes tipos de pendentes importações. Consoante o resultado de Olá do processo de importação de Olá, um objeto de teste no espaço de conector Olá tem um dos seguintes tipos de importação pendente de Olá:

* **Nenhuma**. Nenhum tooany de alterações de atributos de Olá do objeto de teste de Olá estão disponíveis. Motor de sincronização não sinalizador este tipo como pendente importar.
* **Adicionar**. Olá, objeto de transição é um novo objeto de importação no espaço de conector Olá. Motor de sincronização sinalizadores este tipo como pendente importar para processamento adicional no metaverso Olá.
* **Atualização**. Motor de sincronização localiza um objeto de transição correspondente no espaço de conector Olá e sinaliza este tipo como importação pendente para que as atualizações toohello atributos podem ser processados no metaverso Olá. As atualizações incluem mudar o nome do objeto.
* **Eliminar**. Motor de sincronização localiza um objeto de transição correspondente no espaço de conector Olá e sinaliza este tipo como importação pendente para que hello associados a um objeto pode ser eliminado.
* **Eliminar/adicionar**. Motor de sincronização localiza um objeto de transição correspondente no espaço de conector Olá, mas os tipos de objeto de Olá não correspondem. Neste caso, um eliminar-adicionar modificação é testada. Um eliminar-adicionar modificação indica toohello motor de sincronização que tem de ocorrer uma ressincronização completa deste objeto porque a diferentes conjuntos de regras de aplicam toothis objeto quando o tipo de objeto Olá é alterado.

Por definição Olá pendentes estado de importação de um objeto de teste, é possível tooreduce Olá significativamente a quantidade de dados processadas durante a sincronização porque fazê-lo, por isso, permite que Olá sistema tooprocess apenas os objetos que tenham dados atualizados.

### <a name="synchronization-process"></a>Processo de sincronização
Sincronização é composto por dois processos relacionados:

* Sincronização de entrada, quando o conteúdo de Olá do metaverso Olá é atualizado utilizando dados de Olá no espaço de conector Olá.
* Sincronização de saída, quando o conteúdo de Olá de espaço de conector Olá é atualizado através da utilização de dados no metaverso Olá.

Ao utilizar as informações de Olá testadas no espaço de conector Olá, hello processo de sincronização de entrada cria Olá metaverso Olá integrado vista dos dados de Olá que esteja armazenados em origens de dados de Olá ligado. Todos os objetos de transição ou apenas as informações de importação pendente estão agregadas, dependendo de como as regras de Olá estão configuradas.

as atualizações do processo de sincronização de saída Olá exportar objetos quando forem efetuadas alterações de objetos de metaverso.

Sincronização de entrada cria a vista de Olá integrado no metaverso Olá de informações de identidade Olá que são recebidos Olá ligado das origens de dados. Motor de sincronização pode processar as informações de identidade em qualquer altura utilizando Olá mais recentes informações de identidade que tem de Olá ligado origem de dados.

**Sincronização de entrada**

Sincronização de entrada inclui Olá seguintes processos:

* **Aprovisionar** (também denominado **projecção** se for importante toodistinguish este processo de aprovisionamento de sincronização de saída). o motor de sincronização de Olá cria um novo objeto de metaverso com base num objeto de transição e liga-los. Aprovisionar é uma operação de ao nível do objeto.
* **Associar**. o motor de sincronização de Olá liga um transição objeto tooan existente objeto de metaverso. Uma associação é uma operação de ao nível do objeto.
* **Importar o fluxo de atributos**. Motor de sincronização de atualizações de valores de atributo Olá, denominados de fluxo de atributos de objeto de Olá no metaverso Olá. Fluxo de atributos de importação é uma operação de nível de atributo que requer uma ligação entre um objeto de transição e um objeto de metaverso.

Aprovisionar é o processo de apenas de Olá que cria os objetos no metaverso Olá. Aprovisionar afeta apenas os objetos de importação que estão desagregados objetos. Durante o aprovisionamento, o motor de sincronização cria um objeto de metaverso que corresponde ao tipo de objeto toohello do objeto de importação de Olá e estabelece uma ligação entre os dois objetos, assim, criar um objeto associado a um.

processo de associação de Olá também estabelece uma ligação entre objetos de importação e um objeto de metaverso. diferença de Olá entre associação e aprovisionar é que o processo de associação de Olá requer esse objeto de importação de Olá são tooan ligado existente objeto de metaverso, onde o processo de aprovisionamento de Olá cria um novo objeto de metaverso.

Motor de sincronização tenta toojoin um objeto de metaverso de tooa de objeto de importação utilizando critérios que é especificado na configuração de regra de sincronização de Olá.

Durante o aprovisionamento de Olá e processos de associação, o motor de sincronização liga um objeto de metaverso desagregado objeto tooa, torná-los associado. Depois de concluídos estes operações ao nível do objeto, o motor de sincronização pode atualizar valores de atributo de Olá do objeto de metaverso associado Olá. Este processo é denominado o fluxo de atributos de importação.

Fluxo de atributos de importação ocorre em todos os objetos de importação que transportem novos dados e são objeto de metaverso tooa ligado.

**Sincronização de saída**

Atualizações de sincronização de saída exportar objetos quando um objeto de metaverso alterar, mas não é eliminado. objetivo do Olá de sincronização de saída é tooevaluate se os objetos de toometaverse alterações necessitam de atualizações toostaging objetos nos espaços de conector Olá. Em alguns casos, ser atualizado Olá alterações podem exigir que os objetos de teste em todos os espaços de conector. Objetos de teste que são alterados são sinalizados como pendente de exportação, torná-los exportar objetos. Estes objetos são mais tarde instalados sem solicitação origem de dados ligada toohello durante o processo de exportação de Olá a exportação.

Sincronização de saída tem três processos:

* **Aprovisionamento**
* **Desaprovisionamento**
* **Fluxo de atributos de exportação**

Aprovisionamento e desaprovisionamento são ambas as operações ao nível do objeto. Desaprovisionamento depende do aprovisionamento porque apenas aprovisionamento pode iniciá-lo. Desaprovisionamento é acionado quando aprovisionar remove Olá ligação entre um objeto de metaverso e um objeto de exportação.

Aprovisionamento sempre é acionado quando as alterações serem aplicadas tooobjects no metaverso Olá. Quando são efetuadas alterações toometaverse objetos, o motor de sincronização pode efetuar qualquer uma das Olá seguir tarefas como parte do processo de aprovisionamento de Olá:

* Crie objetos associados, onde um objeto de metaverso é o objeto de exportação de tooa ligado recentemente criado.
* Mudar o nome de um objeto associado.
* Disjoin ligações entre um objeto de metaverso e objetos, criação de um objeto disjoined de teste.

Se o aprovisionamento requer o motor de sincronização toocreate um novo objeto de conector, Olá objeto de metaverso do objeto toowhich Olá de transição é ligado é sempre um objeto de exportação, porque o objeto de Olá não ainda existe na origem de dados ligada Olá.

Se o aprovisionamento requer toodisjoin de motor de sincronização um associado a um objeto, criação de um objeto disjoined, desaprovisionamento é acionado. Olá, processo de desaprovisionamento elimina objeto Olá.

Durante o desaprovisionamento, eliminar um objeto de exportação não fisicamente eliminar Olá objeto. Olá objeto está assinalado como **eliminado**, que significa que essa operação de eliminação de Olá é testado no objeto de Olá.

Fluxo de atributos de exportação também ocorre durante o processo de sincronização de saída de Olá, de forma semelhante toohello que importar fluxo de atributos ocorre durante a sincronização de entrada. Fluxo de atributos de exportação ocorre apenas entre objetos de metaverso e exportação que estão associados.

### <a name="export-process"></a>Processo de exportação
Durante o processo de exportação de Olá, motor de sincronização analisa todos os objetos de exportação que estão sinalizados como pendente exportação no espaço de conector Olá e, em seguida, envia atualizações toohello ligado a origem de dados.

o motor de sincronização de Olá pode determinar Olá com êxito de uma exportação mas suficientemente não consegue determinar que o processo de gestão de identidade Olá está concluído. Objetos da origem de dados ligada Olá podem sempre ser alterados por outros processos. Porque o motor de sincronização não tem uma origem de dados ligada toohello ligação persistente, não é suficiente toomake pressupostos sobre as propriedades de Olá de um objeto de origem de dados ligada Olá em apenas uma notificação de exportação com êxito.

Por exemplo, um processo no Olá ligado a origem de dados foi atributos de objetos de Olá a alteração de fazer uma cópia de valores originais tootheir (ou seja, origem de dados ligada Olá foi substituir valores Olá imediatamente após dados Olá é feito o Push terminar pelo motor de sincronização e com êxito aplicado na origem de dados ligada Olá).

arquivos de motor de sincronização de Olá exportar e importar informações de estado sobre cada objeto de teste. Se os valores de atributos de Olá especificadas na lista de inclusão de atributo Olá foram alterados desde a última exportação de Olá, Olá armazenamento de importação e exportação tooreact de motor de sincronização do Estado ativa adequadamente. Motor de sincronização utiliza Olá importação processo tooconfirm valores de atributos que tenham sido exportado toohello origem de dados ligada. Mostra uma comparação entre Olá importados e informações exportadas, conforme mostrado no Olá seguinte ilustração, permite toodetermine do motor de sincronização se exportar Olá foi concluída com êxito ou se necessita de toobe repetido.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Por exemplo, se o motor de sincronização exporta atributo C, que tem um valor de 5, tooa ligado a origem de dados, armazena C = 5 na respetiva memória de estado de exportação. Cada exportação adicional neste objecto resulta na origem de dados ligada tentativa de tooexport C = 5 toohello novamente porque o motor de sincronização parte do princípio de que este valor não foi o objeto de forma permanente aplicados toohello (ou seja, a menos que um valor diferente foi importado recentemente de Olá ligado origem de dados). memória de exportação de Olá será eliminada quando C = 5 é recebido durante uma operação de importação no objeto de Olá.

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre como [Integrar as identidades no local ao Azure Active Directory](active-directory-aadconnect.md).

