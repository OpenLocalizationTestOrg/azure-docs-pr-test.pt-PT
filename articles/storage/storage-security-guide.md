---
title: "Guia de segurança de armazenamento aaaAzure | Microsoft Docs"
description: "Detalhes Olá vários métodos para proteger o Storage do Azure, incluindo mas não limitado tooRBAC, encriptação do serviço de armazenamento, encriptação do lado do cliente, SMB 3.0 e Azure Disk Encryption."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Guia de segurança de armazenamento do Azure
## <a name="overview"></a>Descrição geral
Storage do Azure fornece um conjunto completo de capacidades de segurança em conjunto, permitir que os programadores de aplicações seguras toobuild. conta de armazenamento de Olá próprio pode ser protegida utilizando o controlo de acesso baseado em funções e o Azure Active Directory. Dados podem ser protegidos em trânsito entre uma aplicação e o Azure utilizando [encriptação do lado do cliente](storage-client-side-encryption.md), HTTPS ou SMB 3.0. Dados podem ser definidos toobe encriptado automaticamente quando escritos utilizando o armazenamento tooAzure [encriptação de serviço de armazenamento (SSE)](storage-service-encryption.md). SO e discos de dados utilizados por máquinas virtuais podem ser definidos toobe encriptada utilizando [Azure Disk Encryption](../security/azure-security-disk-encryption.md). Podem ser concedidos acesso delegado toohello dados objetos no Storage do Azure utilizando [assinaturas de acesso partilhado](storage-dotnet-shared-access-signature-part-1.md).

Este artigo irá fornecer uma descrição geral de cada uma destas funcionalidades de segurança que podem ser utilizadas com o Storage do Azure. São fornecidas hiperligações tooarticles que irá fornecer detalhes de cada funcionalidade, pode facilmente fazê-lo de modo mais investigação em cada tópico.

Seguem-se Olá tópicos toobe abordada neste artigo:

* [Gestão Plane segurança](#management-plane-security) – proteger a sua conta de armazenamento

  plane de gestão de Olá é composta por Olá recursos utilizados toomanage sua conta do storage. Nesta secção, iremos falar sobre o modelo de implementação Azure Resource Manager Olá e como toocontrol de controlo de acesso baseado em funções (RBAC) toouse aceder tooyour contas de armazenamento. Também irá abordadas gerir as chaves de conta de armazenamento e como tooregenerate-los.
* [Segurança dos dados Plane](#data-plane-security) – tooYour de acesso de proteger dados

  Nesta secção, vamos ver que permite o acesso dos objetos de dados real toohello na sua conta de armazenamento, tais como blobs, ficheiros, filas e tabelas, utilizando as assinaturas de acesso partilhado e políticas de acesso armazenada. Abordaremos SAS de nível de serviço e o nível de conta SAS. Podemos também verá como toolimit aceder ao endereço IP específico do tooa (ou intervalo de endereços IP), como o protocolo de Olá toolimit utilizado tooHTTPS e como toorevoke uma assinatura de acesso partilhado sem aguardar-tooexpire.
* [Encriptação em Trânsito](#encryption-in-transit)

  Esta secção descreve como toosecure dados quando a transferência ou a sair do armazenamento do Azure. Iremos falar sobre Olá recomendado a utilização da encriptação de HTTPS e Olá utilizada pelo SMB 3.0 para partilhas de ficheiros do Azure. Iremos irá também observe encriptação do lado do cliente, que lhe permite tooencrypt Olá dados antes de é transferido para o armazenamento numa aplicação de cliente e dados de Olá toodecrypt depois de serem transferidos fora do armazenamento.
* [Encriptação Inativa](#encryption-at-rest)

  Serão abordadas encriptação de serviço de armazenamento (SSE), e como pode ativá-la para uma conta de armazenamento, resultando nos blobs de blocos, blobs de páginas a ser encriptados automaticamente de blobs de acréscimo quando escritos tooAzure armazenamento. Também veremos como pode utilizar o Azure Disk Encryption e explorar diferenças básico Olá e casos de encriptação de disco versus SSE versus encriptação do lado do cliente. Iremos brevemente abordar a conformidade FIPS para E.U.A. Computadores Government.
* Utilizar [análise de armazenamento](#storage-analytics) tooaudit acesso do Storage do Azure

  Esta secção descreve como toofind informações na análise de armazenamento Olá registos para um pedido. Vamos observe análise de armazenamento real dados de registo e ver como toodiscern se é efetuado um pedido com Olá armazenamento conta chave, com uma assinatura de acesso partilhado, ou anonimamente e se foi concluída com êxito ou falha.
* [A ativação baseada no Browser clientes utilizando a CORS](#Cross-Origin-Resource-Sharing-CORS)

  Esta secção aborda como tooallow transversal à partilha de recursos (CORS). Iremos falar sobre acesso entre domínios e como toohandle-lo com as capacidades CORS Olá incorporadas no armazenamento do Azure.

## <a name="management-plane-security"></a>Gestão Plane segurança
plane de gestão de Olá consiste em operações que afetam a conta de armazenamento de Olá próprio. Por exemplo, pode criar ou eliminar uma conta de armazenamento, obter uma lista de contas de armazenamento numa subscrição, obter chaves de conta de armazenamento Olá ou voltar a gerar chaves de conta de armazenamento Olá.

Quando cria uma nova conta de armazenamento, selecione um modelo de implementação de clássico ou do Resource Manager. modelo de clássico Olá de criação de recursos no Azure só permite a subscrição do acesso all-or-nothing toohello e Olá por sua vez, a conta de armazenamento.

Este guia centra-se no modelo do Resource Manager Olá que é Olá recomendado significa que para a criação de contas do storage. Com as contas de armazenamento do Resource Manager Olá, em vez de conceder acesso toohello toda a subscrição, pode controlar o acesso num plane mais finito de gestão de nível toohello utilizando o controlo de acesso baseado em funções (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Como toosecure o armazenamento de contas com controlo de acesso baseado em funções (RBAC)
Vamos falar sobre o que é o RBAC e como pode utilizá-lo. Cada subscrição do Azure tem um Azure Active Directory. Os utilizadores, grupos e aplicações a partir desse diretório podem ser concedidas acesso toomanage recursos Olá subscrição do Azure que utilizam o modelo de implementação do Resource Manager Olá. Este é referenciado tooas controlo de acesso baseado em funções (RBAC). toomanage isto aceder, pode utilizar Olá [portal do Azure](https://portal.azure.com/), Olá [ferramentas da CLI do Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou Olá [APIs de REST de fornecedor de recursos de armazenamento de Azure ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Com o modelo do Resource Manager Olá, coloque conta de armazenamento Olá num recurso grupo e o controlo de acesso toohello gestão plane dessa conta de armazenamento específico utilizando o Azure Active Directory do. Por exemplo, é possível conceder a utilizadores específicos Olá capacidade tooaccess Olá armazenamento chaves de conta, enquanto outros utilizadores podem ver informações sobre a conta de armazenamento Olá, mas não é possível aceder às chaves de conta de armazenamento Olá.

#### <a name="granting-access"></a>Conceder acesso
É concedido acesso ao atribuir Olá toousers de funções RBAC adequada, grupos e aplicações, no âmbito correto Olá. toogrant acesso toohello toda a subscrição, pode atribuir uma função ao nível da subscrição de Olá. Pode conceder acesso tooall dos recursos de Olá num grupo de recursos por grupo de recursos de toohello permissões próprio de concessão de permissões. Também pode atribuir funções específicas toospecific recursos, tais como contas de armazenamento.

Seguem-se os pontos principais Olá terá tooknow sobre como utilizar operações de gestão do RBAC tooaccess Olá de uma conta de armazenamento do Azure:

* Quando atribui acesso, basicamente atribuir uma conta de toohello de função que pretende que o acesso de toohave. Pode controlar o acesso toohello operações utilizados toomanage essa conta de armazenamento, mas não os dados toohello objetos na conta de Olá. Por exemplo, pode conceder permissão propriedades de Olá tooretrieve da conta de armazenamento de Olá (por exemplo, redundância), mas não tooa contentor ou de dados dentro de um contentor no Blob Storage.
* Alguém toohave permissão tooaccess Olá objetos de dados na conta de armazenamento de Olá, pode conceder-lhes chaves de conta de armazenamento de Olá tooread permissão e esse utilizador pode, em seguida, utilizar essas chaves tooaccess Olá blobs, filas, tabelas e os ficheiros.
* Podem ser atribuídas a funções de conta de utilizador específica tooa, um grupo de utilizadores ou aplicações específicos tooa.
* Cada função tem uma lista de ações e não as ações. Por exemplo, a função de contribuinte de Máquina Virtual de Olá tem uma ação de "listKeys" que lhe permite ler toobe de chaves de conta de armazenamento Olá. Olá contribuinte tem "Não ações" como atualizar acesso Olá para utilizadores na Olá do Active Directory.
* As funções de armazenamento incluem (mas não estarem limitadas aos) seguintes Olá:

  * Proprietário – podem gerir tudo, incluindo o acesso.
  * Contribuidor – que podem fazer nada proprietário Olá pode exceto atribuir acesso. Alguém com esta função pode ver e voltar a gerar chaves de conta de armazenamento Olá. Com chaves de conta de armazenamento Olá, eles podem aceder a objetos de dados de Olá.
  * Leitor – podem visualizar informações sobre a conta de armazenamento Olá, exceto os segredos. Por exemplo, se atribuir uma função com permissões leitor toosomeone de conta de armazenamento Olá, podem visualizar as propriedades de Olá Olá da conta de armazenamento, mas não é possível efetuar quaisquer alterações toohello propriedades ou visualizar chaves de conta de armazenamento Olá.
  * Contribuinte da conta de armazenamento – pode gerir conta de armazenamento Olá – podem ler Olá grupos de recursos da subscrição e os recursos e criar e gerir implementações do grupo de recursos de subscrição. Também pode aceder a chaves de conta do Olá armazenamento, que por sua vez, significa que possam aceder ao plane de dados de Olá.
  * Administrador de acesso do utilizador – podem gerir conta de armazenamento de toohello de acesso de utilizador. Por exemplo, estes podem conceder utilizador específico do leitor acesso tooa.
  * Contribuinte de máquina virtual – podem gerir máquinas virtuais, mas não Olá armazenamento conta toowhich que estão ligados. Esta função pode listar chaves de conta de armazenamento Olá, que significa que Olá toowhom utilizador atribuir esta função pode atualizar plane de dados de Olá.

    Ordem de para um utilizador de toocreate uma máquina virtual, têm de toobe toocreate capaz de Olá correspondente ficheiro VHD numa conta do storage. toodo que, necessitam de armazenamento de Olá toobe tooretrieve capaz de chave de conta e transmita-API toohello criar Olá VM. Por conseguinte, têm de ter esta permissão, de modo que podem listar chaves de conta de armazenamento Olá.
* funções personalizadas do Olá capacidade toodefine é uma funcionalidade que permite-lhe toocompose um conjunto de ações a partir de uma lista de ações disponíveis que podem ser executadas nos recursos do Azure.
* utilizador Olá tem toobe configurar no Azure Active Directory antes de pode atribuir um toothem de função.
* Pode criar um relatório de quem concedido/revogado que tipo de acesso para/de quem e no qual âmbito com o PowerShell ou Olá CLI do Azure.

#### <a name="resources"></a>Recursos
* [Controlo de Acesso Baseado em Funções do Azure Active Directory](../active-directory/role-based-access-control-configure.md)

  Este artigo explica Olá controlo de acesso baseado em função do Active Directory do Azure e como funciona.
* [RBAC: Funções Incorporadas](../active-directory/role-based-access-built-in-roles.md)

  Este artigo fornece detalhes sobre todas as funções incorporadas Olá disponíveis no RBAC.
* [Compreender a implementação do Resource Manager e a implementação clássica](../azure-resource-manager/resource-manager-deployment-model.md)

  Este artigo explica a implementação do Resource Manager Olá e modelos de implementação clássica e explica as vantagens de Olá da utilização de grupos de recursos e do Resource Manager Olá. Explica como funcionam os fornecedores de armazenamento, rede e Olá computação do Azure no modelo do Resource Manager Olá.
* [Gestão do controlo de acesso baseado em funções com Olá REST API](../active-directory/role-based-access-control-manage-access-rest.md)

  Este artigo mostra como toouse Olá REST API toomanage RBAC.
* [Referência de API de REST de fornecedor de recursos de armazenamento do Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Esta é a referência de Olá para Olá APIs que pode utilizar toomanage sua conta do storage através de programação.
* [Tooauth do Guia do programador com a API do Azure Resource Manager](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Este artigo mostra como utilizar tooauthenticate Olá APIs do Resource Manager.
* [Controlo de Acesso Baseado em Funções para o Microsoft Azure no Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Este é um tooa ligação vídeo no Channel 9 de conferências de Ignite Olá MS versão 2015. Nesta sessão falar sobre aceder a gestão e capacidades de relatórios no Azure e explorar as melhores práticas em torno de proteger o acesso subscrições tooAzure utilizando o Azure Active Directory.

### <a name="managing-your-storage-account-keys"></a>Gerir as chaves de conta de armazenamento
Conta de armazenamento chaves são cadeias de 512 bits criadas pelo Azure, que, juntamente com o armazenamento de Olá, o nome de conta pode ser tooaccess utilizados Olá dados objetos armazenados na conta do storage Olá, por exemplo, blobs, entidades dentro de uma tabela, fila de mensagens e ficheiros numa partilha de ficheiros do Azure. Controlar toohello armazenamento conta chaves controlos de acesso de acesso toohello plane de dados para essa conta de armazenamento.

Cada conta de armazenamento tem duas chaves que referida tooas "Chave 1" e «Chave 2» Olá [portal do Azure](http://portal.azure.com/) e no Olá cmdlets do PowerShell. Estes podem ser regenerados manualmente utilizando um dos vários métodos, incluindo, mas não limitado toousing Olá [portal do Azure](https://portal.azure.com/), PowerShell, Olá CLI do Azure ou através de programação utilizando Olá biblioteca de clientes do Storage .NET ou hello do Azure Serviços de armazenamento REST API.

Existem diversas razões tooregenerate as chaves de conta de armazenamento.

* Pode voltar a gerá-los de forma regular por motivos de segurança.
* Pretende voltar a gerar as chaves de conta de armazenamento se alguém geridos toohack numa aplicação e obter a chave de Olá que foi codificado ou guardada no ficheiro de configuração, concedendo-lhes a conta de armazenamento de tooyour acesso total.
* Outro cenário para regeneração da chave é se a equipa está a utilizar um Explorador de armazenamento de aplicação que mantém a chave de conta do storage Olá, e sai de um dos membros do agrupamento Olá. aplicação Olá continuaria toowork, concedendo-lhes acesso conta de armazenamento de tooyour depois forem removidos. Isto é, na verdade, Olá principal razão criaram assinaturas de acesso partilhado de nível de conta – pode utilizar um SAS de nível de conta em vez de armazenar chaves de acesso de Olá num ficheiro de configuração.

#### <a name="key-regeneration-plan"></a>Plano de regeneração da chave
Não quiser chave de voltar a gerar Olá toojust que estiver a utilizar sem algum planeamento. Se, fazê-lo, foi possível cortar desativar todas as acesso toothat conta de armazenamento, que pode provocar a interrupção principais. É por isso existem duas chaves. Deve voltar a gerar uma chave de cada vez.

Antes de voltar a gerar as chaves, lembre-se de que tem uma lista de todas as aplicações que são dependentes da conta de armazenamento Olá, bem como quaisquer outros serviços que está a utilizar no Azure. Por exemplo, se estiver a utilizar o Azure Media Services dependentes da sua conta do storage, deve sincronizar novamente as chaves de acesso de Olá com o serviço de multimédia depois de voltar a gerar chave Olá. Se estiver a utilizar quaisquer aplicações, tais como o Explorador de armazenamento, terá de tooprovide Olá novas chaves toothose aplicações bem. Tenha em atenção que se tiver VMs cujos ficheiros VHD são armazenados na conta do storage Olá, este será não ser afetado por regenerar chaves de conta de armazenamento Olá.

Pode voltar a gerar as chaves de Olá portal do Azure. Depois das chaves são regeneradas podem demorar até too10 minutos toobe sincronizados em todos os serviços de armazenamento.

Quando estiver pronto, eis o processo geral de Olá com detalhes sobre como deve alterar a chave. Neste caso, pressuposto Olá é que estiver a utilizar atualmente chave 1 e vai toochange tudo toouse chave 2 em vez disso.

1. Voltar a gerar chave 2 tooensure que é seguro. Pode fazê-lo no Olá portal do Azure.
2. Em todas as aplicações de olá onde está armazenada a chave de armazenamento de Olá, altere o valor novo do Olá armazenamento toouse chave chave 2. Testar e publicar a aplicação Olá.
3. Após todos os de Olá serviços e aplicações estão operacionais e em execução com êxito, voltar a gerar chave 1. Isto garante que qualquer pessoa toowhom expressamente não fornecidos nova chave de Olá deixará de ter aceder à conta de armazenamento toohello.

Se estiver a utilizar a chave 2, pode utilizar Olá mesmo processo, mas os nomes de chaves Olá inversa.

Pode migrar através de alguns dias, a alteração de cada aplicação toouse Olá nova chave e publicar. Depois de terminar, deve, em seguida, volte atrás e regenerar a chave de antigo Olá, pelo que já não funciona.

Outra opção é a chave da conta de armazenamento de Olá de tooput num [Cofre de chaves do Azure](https://azure.microsoft.com/services/key-vault/) como um segredo e ter a sua chave de Olá obter aplicações a partir daí. Em seguida, quando regenerar a chave de Olá e atualizar Olá Cofre de chaves do Azure, as aplicações de Olá não terá de toobe implementada novamente porque estes selecionará nova chave de Olá de Olá Cofre de chaves do Azure automaticamente. Tenha em atenção que pode fazer com que aplicação Olá ler a chave de Olá sempre que o ficheiro necessário ou -lo em cache na memória e se não conseguir ao utilizá-la, obter a chave de Olá novamente partir Olá Cofre de chaves do Azure.

Utilizar o Cofre de chaves do Azure também adiciona a outro nível de segurança para as chaves de armazenamento. Se utilizar este método, nunca terá codificado de chave de armazenamento de Olá num ficheiro de configuração, que elimina essa compromissos alguém obter acesso toohello chaves sem permissão específico.

Outra vantagem de utilizar o Cofre de chaves do Azure é que também pode controlar o acesso tooyour chaves utilizando o Azure Active Directory. Isto significa que pode conceder alguns toohello de acesso das aplicações que têm chaves de Olá tooretrieve partir do Cofre de chaves do Azure e saiba que outras aplicações não será capaz de tooaccess chaves de Olá sem conceder-lhes permissão especificamente.

Nota: é recomendável toouse apenas um dos Olá chaves em todas as aplicações em Olá mesmo tempo. Se utilizar a chave 1 em alguns locais e a chave 2 em outros, não poderá ser capaz de toorotate as chaves sem alguma perda de acesso de aplicação.

#### <a name="resources"></a>Recursos
* [Sobre as contas de armazenamento do Azure](storage-create-storage-account.md#regenerate-storage-access-keys)

  Este artigo fornece uma descrição geral de contas do storage e descreve ver, copiar e regenerar chaves de acesso de armazenamento.
* [Referência de API de REST de fornecedor de recursos de armazenamento do Azure](https://msdn.microsoft.com/library/mt163683.aspx)

  Este artigo contém artigos de toospecific ligações sobre obter chaves de conta de armazenamento de Olá e regenerar chaves de conta de armazenamento de Olá para uma conta do Azure utilizando Olá REST API. Nota: Isto é para contas de armazenamento do Resource Manager.
* [Operações em contas de armazenamento](https://msdn.microsoft.com/library/ee460790.aspx)

  Este artigo no Olá referência da API REST do serviço de armazenamento contém artigos toospecific de ligações em obter e regenerar chaves de conta de armazenamento de Olá utilizando Olá REST API. Nota: Isto é para contas do storage clássicas Olá.
* [Diga a gestão de tookey goodbye – gerir aceder a dados para armazenamento de tooAzure utilizar o Azure AD](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Este artigo mostra como toouse do Active Directory toocontrol aceder às chaves de armazenamento do Azure tooyour no Cofre de chaves do Azure. Também mostra como as chaves de Olá tooregenerate numa base horária da tarefa toouse uma automatização do Azure.

## <a name="data-plane-security"></a>Segurança dos dados Plane
Segurança dos dados Plane refere-se métodos toohello toosecure utilizados Olá dos objetos de dados armazenados no Storage do Azure – ficheiros, tabelas, filas e blobs Olá. Iremos viu dados de Olá tooencrypt de métodos e de segurança durante trânsito dos dados de Olá, mas como deve proceder permitir o acesso a objetos de toohello?

Basicamente, existem dois métodos para controlar acesso toohello dados próprios objetos. Olá é primeiro por controlar chaves de conta de armazenamento do acesso toohello e Olá segundo está a utilizar assinaturas de acesso partilhado toogrant acesso toospecific dos objetos de dados durante um período de tempo específico.

Uma exceção toonote é que pode permitir o acesso público tooyour blobs ao definir o nível de acesso de Olá para o contentor de Olá que contém blobs Olá em conformidade. Se definir o acesso a um contentor tooBlob ou contentor, permitirá o acesso de leitura público para Olá os blobs no contentor. Isto significa que qualquer pessoa com um URL que aponta tooa BLOBs no contentor pode abrir num browser sem utilizar uma assinatura de acesso partilhado ou ter chaves de conta de armazenamento Olá.

### <a name="storage-account-keys"></a>Chaves de Contas de Armazenamento
Chaves de conta de armazenamento são criadas pelo Azure que, juntamente com o nome da conta de armazenamento Olá, pode ser objetos de dados utilizados tooaccess Olá armazenados na conta do storage Olá de cadeias de 512 bits.

Por exemplo, pode de leitura de blobs, escrever tooqueues, criar tabelas e modifique os ficheiros. Muitas destas ações podem ser efetuadas através de Olá Azure portal ou utilizar uma das muitas aplicações de Explorador de armazenamento. Também poderá escrever Olá toouse do código REST API ou uma das Olá bibliotecas de cliente do armazenamento tooperform estas operações.

Tal como explicado na secção de Olá no Olá [gestão Plane segurança](#management-plane-security), chaves de armazenamento de toohello de acesso para uma conta de armazenamento clássicas pode ser concedida, concedendo acesso total toohello subscrição do Azure. Chaves de armazenamento de toohello de acesso para uma conta de armazenamento utilizando o modelo do Azure Resource Manager Olá podem ser controladas através de controlo de acesso baseado em funções (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Como toodelegate aceder tooobjects na sua conta utilizar assinaturas de acesso partilhado e armazenados políticas de acesso
Uma assinatura de acesso partilhado é uma cadeia contendo um token de segurança que pode ser anexados tooa URI que lhe permite objetos de toostorage toodelegate acesso e especificar as restrições, como o intervalo de data/hora Olá de acesso e permissões de Olá.

Pode conceder acesso tooblobs, contentores, mensagens de filas, ficheiros e tabelas. Com tabelas, pode, na verdade, conceder permissão tooaccess um intervalo de entidades na tabela de Olá especificando Olá partição e a linha de intervalos de chaves toowhich pretende Olá utilizador toohave aceder. Por exemplo, se tiver dados armazenados com uma chave de partição do Estado geográfica, pode dar alguém aceder a dados toojust Olá para Califórnia.

Noutro exemplo, pode dar um token SAS, que permite a fila de tooa toowrite entradas de uma aplicação web e atribuir uma função de trabalho aplicação de função um mensagens de token tooget SAS de Olá fila e processá-los. Ou, pode dar um cliente um token SAS, que podem utilizar o contentor de tooa tooupload imagens no Blob Storage e dê um tooread de permissão de aplicação web essas imagens. Em ambos os casos, há uma separação das preocupações – cada aplicação pode ser especificada o acesso apenas Olá que requerem na ordem tooperform as respetivas tarefas. Isto é possível através da utilização de Olá de assinaturas de acesso partilhado.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Motivo pelo qual pretende toouse assinaturas de acesso partilhado
Motivo pelo qual pretenda que toouse um SAS em vez de apenas dar a sua chave de conta do storage, o que é por isso, muito mais fácil? Dar a sua chave de conta do storage é como partilhar chaves de Olá do seu Unido de armazenamento. -Concede acesso completo. Alguém pode utilizar as chaves e carregue respetiva conta de armazenamento do música todo biblioteca tooyour. Que podem substituir os ficheiros infetados de vírus versões ou roubar os seus dados. Conta de armazenamento de tooyour acesso ilimitado a dar ausente é algo que não devem ser levados ligeiramente.

Com assinaturas de acesso partilhado, pode dar um cliente apenas Olá as permissões necessárias para um período limitado de tempo. Por exemplo, se alguém está a carregar uma conta do blob tooyour, pode conceder-lhes acesso de escrita para apenas suficiente blob Olá do tempo tooupload (consoante o tamanho do blob Olá, Olá obviamente). E se mudar de ideias, pode revogar esse acesso.

Além disso, pode especificar que pedidos efetuados com uma SAS restrito tooa determinada tooAzure externo do intervalo de endereços de endereço IP ou IP. Também pode exigir que são efetuados os pedidos de utilização de um protocolo específico (HTTPS ou HTTP/HTTPS). Isto significa que se pretende apenas o tráfego HTTPS de tooallow, pode definir apenas o tooHTTPS de protocolo Olá necessário e tráfego HTTP será bloqueado.

#### <a name="definition-of-a-shared-access-signature"></a>Definição de uma assinatura de acesso partilhado
Uma assinatura de acesso partilhado é que um conjunto de parâmetros de consulta anexado URL toohello apontar recursos Olá

que fornece informações sobre o acesso de Olá permitidos e Olá período de tempo para que Olá acesso é permitido. Eis um exemplo; Este URI fornece acesso de leitura tooa blob para cinco minutos. Tenha em atenção que SAS os parâmetros de consulta tem de ser codificados de URL, como % 3A para vírgula (:) ou % 20 para um espaço.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Como Olá assinatura de acesso partilhado é autenticada ao hello serviço Storage do Azure
Quando o serviço de armazenamento Olá recebe o pedido de Olá, aceita parâmetros de consulta de entrada Olá e cria uma assinatura utilizando Olá mesmo método como Olá programa de chamada. Em seguida, compara assinaturas hello de dois. Se estes concordarem, então, Olá serviço de armazenamento pode verificar Olá armazenamento serviço versão toomake se é válido, certifique-se de que hello data e hora atuais estão dentro da janela especificada Olá, acesso disponibilizar se Olá pedido corresponde toohello pedidos efetuados, etc.

Por exemplo, com os nosso URL acima, se o URL de Olá foi apontar tooa ficheiros em vez de um blob, este pedido irão falhar porque Especifica que Olá que assinatura de acesso partilhado é para um blob. Se Olá comando REST que está a ser chamado foi tooupdate um blob, irão falhar porque hello assinatura de acesso partilhado Especifica que o acesso de leitura apenas é permitido.

#### <a name="types-of-shared-access-signatures"></a>Tipos de assinaturas de acesso partilhado
* Uma SAS de nível de serviço podem ser utilizados tooaccess recursos específicos numa conta do storage. Alguns exemplos deste estão a obter uma lista de blobs num contentor, transferir um blob, atualizar uma entidade numa tabela, adicionar tooa a fila de mensagens ou carregar uma partilha de ficheiros de tooa do ficheiro.
* Uma SAS de nível de conta pode ser utilizado tooaccess tudo o que pode ser utilizado um SAS de nível de serviço para. Além disso, deu tooresources opções que não são permitidas com uma SAS de nível de serviço, como contentores de toocreate de capacidade de Olá, tabelas, filas e partilhas de ficheiros. Também pode especificar acesso toomultiple serviços em simultâneo. Por exemplo, pode dar alguém aceder a blobs tooboth e ficheiros na sua conta de armazenamento.

#### <a name="creating-an-sas-uri"></a>Criar um URI de SAS
1. Pode criar um URI ad hoc a pedido, definir todos os parâmetros de consulta Olá cada vez.

   Este é realmente flexível, mas se tiver um conjunto lógico de parâmetros que são semelhantes a cada hora, através de uma política de acesso armazenada uma ideia mais precisa.
2. Pode criar uma política de acesso armazenada para um contentor inteiro, a partilha de ficheiros, a tabela ou fila. Em seguida, pode utilizar isto como base Olá para Olá URI de SAS que cria. As permissões com base nas políticas de acesso armazenada podem ser facilmente revogadas. Pode configurar políticas de too5 definidas em cada contentor, fila, tabela ou partilha de ficheiros.

   Por exemplo, se foram vai toohave muitas pessoas de leitura de blobs de Olá num contentor específico, pode criar uma política de acesso armazenada que diz "conceder acesso de leitura" e outras definições que serão Olá mesmo cada vez. Em seguida, pode criar um URI de SAS utilizando definições Olá Olá política de acesso armazenada e especificando Olá data/hora de expiração. Olá partido desta situação é que não tem toospecify todas Olá parâmetros de consulta sempre.

#### <a name="revocation"></a>Revogação
Suponha o SAS tiver sido comprometido ou se quiser toochange-lo devido a requisitos de conformidade de regulamentação ou a segurança da empresa. Como revogar acesso tooa recurso utilizando esse SAS Depende de como criou Olá URI de SAS.

Se estiver a utilizar o ad hoc URI, tem três opções. Pode emitir tokens SAS com políticas de expiração curto e aguarde simplesmente Olá SAS tooexpire. Pode mudar o nome ou eliminar recurso Olá (partindo do princípio de token de Olá foi tooa âmbito único objeto). Pode alterar as chaves de conta de armazenamento Olá. Esta última opção pode ter um grande impacto, dependendo de quantos serviços utilizar essa conta de armazenamento e provavelmente não é algo que pretende toodo sem algum planeamento.

Se estiver a utilizar um SAS derivada de uma política de acesso armazenada, pode remover o acesso ao revogar Olá política de acesso armazenada – apenas pode alterá-la, pelo que já expirou ou pode removê-la completamente. Isto entra em vigor imediatamente e invalida todos os SAS criadas com essa política de acesso armazenada. Atualizar ou remover Olá armazenados a política de acesso poderá ter impacto em pessoas que acedem a esse contentor específico, a partilha de ficheiros, a tabela ou fila através de SAS, mas se hello clientes são escritos pelo solicitarem um SAS novo Olá antigo fica inválido, isto irá funcionar ajustar.

Uma vez com uma SAS derivada de uma política de acesso armazenada dá-lhe o Olá capacidade toorevoke que SAS imediatamente, é Olá recomendado melhor prática tooalways utilizar armazenadas as políticas de acesso sempre que possível.

#### <a name="resources"></a>Recursos
Para obter informações mais detalhadas sobre como utilizar assinaturas de acesso partilhado e armazenadas as políticas de acesso, completa com exemplos, consulte toohello seguintes artigos:

* Estes são os artigos de referência de Olá.

  * [Serviço SAS](https://msdn.microsoft.com/library/dn140256.aspx)

    Este artigo fornece exemplos de como utilizar um SAS de nível de serviço com ficheiros, intervalos de tabela, fila de mensagens e blobs.
  * [Construir um serviço SAS](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Construir uma conta SAS](https://msdn.microsoft.com/library/mt584140.aspx)
* Estes são os tutoriais para utilizar Olá .NET cliente biblioteca toocreate assinaturas de acesso partilhado e as políticas de acesso armazenada.

  * [Utilizar assinaturas de acesso partilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md)
  * [Partilhado assinaturas de acesso, parte 2: Criar e utilizar um SAS com Olá serviço Blob](storage-dotnet-shared-access-signature-part-2.md)

    Este artigo inclui uma explicação de modelo SAS Olá, exemplos de assinaturas de acesso partilhado, e recomendações para melhor prática de Olá a utilização de SAS. Também abordadas é revogação Olá da permissão de Olá concedido.
* Limitar o acesso por endereço IP (ACLs de IP)

  * [O que é um ponto final a lista de controlo de acesso (ACLs)?](../virtual-network/virtual-networks-acl.md)
  * [Construir um serviço SAS](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Este é o artigo de referência de Olá para o nível de serviço SAS; inclui um exemplo de ACL de IP da.
  * [Construir uma conta SAS](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Este é o artigo de referência de Olá para o nível de conta SAS; inclui um exemplo de ACL de IP da.
* Autenticação

  * [Autenticação para Olá dos serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Tutorial de introdução de assinaturas de acesso partilhado

  * [Tutorial de introdução de SAS](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Encriptação em trânsito
### <a name="transport-level-encryption--using-https"></a>Encriptação de nível de transporte – através de HTTPS
Outro passo que deve tomar a segurança de Olá tooensure dos seus dados de armazenamento do Azure é os dados de Olá tooencrypt entre o cliente de Olá e Storage do Azure. recomendação primeiro Olá é tooalways utilizar Olá [HTTPS](https://en.wikipedia.org/wiki/HTTPS) protocolo, que garante uma comunicação segura através de Olá Internet pública.

toohave um canal de comunicação segura, deve sempre utilizar HTTPS quando chamar Olá REST APIs ou aceder aos objetos no armazenamento. Além disso, **assinaturas de acesso partilhado**, que pode ser utilizado toodelegate tooAzure objetos de armazenamento de acesso, incluir uma opção toospecify esse Olá só pode ser utilizado o protocolo HTTPS quando utilizar assinaturas de acesso partilhado, garantindo que qualquer pessoa enviar ligações com SAS tokens irá utilizar o protocolo adequado Olá.

Pode impor a utilização Olá de HTTPS ao chamar objetos de tooaccess de REST APIs Olá em contas de armazenamento, permitindo [Secure transferência necessária](storage-require-secure-transfer.md) Olá conta de armazenamento. Ligações utilizando HTTP irão recusou-se quando esta estiver ativada.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Utilizar a encriptação durante trânsito com partilhas de ficheiros do Azure
File storage do Azure suporta HTTPS ao utilizar Olá REST API, mas é mais frequentemente utilizado como uma partilha de ficheiros SMB ligado tooa VM. SMB 2.1 não suporta encriptação, pelo que as ligações só são permitidas no Olá mesma região no Azure. No entanto, SMB 3.0 suporta a encriptação e está disponível no Windows Server 2012 R2, Windows 8, Windows 8.1 e Windows 10, permitindo por várias regiões aceder e até mesmo acesso no ambiente de trabalho Olá.

Tenha em atenção que enquanto partilhas de ficheiros do Azure podem ser utilizadas com o Unix, Olá cliente Linux SMB ainda não suporta encriptação, para que acesso só é permitido dentro de uma região do Azure. Suporte de encriptação de Linux está no plano de Olá de programadores de Linux responsáveis pela funcionalidade SMB. Quando adicionarem estes encriptação, terá de Olá a mesma capacidade para aceder a uma partilha de ficheiros do Azure no Linux, tal como para o Windows.

Pode impor a utilização de Olá de encriptação com Olá serviço de ficheiros do Azure Ativando [Secure transferência necessária](storage-require-secure-transfer.md) Olá conta de armazenamento. Se utilizar hello REST APIs, é necessário o HTTPs. Para SMB, apenas as ligações de SMB que suportem encriptação que irão estabelecer ligação com êxito.

#### <a name="resources"></a>Recursos
* [Como toouse File storage do Azure com o Linux](storage-how-to-use-files-linux.md)

  Este artigo mostra como toomount um ficheiro de Azure partilhar ficheiros de sistema e de carregamento/transferência de Linux.
* [Introdução ao Armazenamento de Ficheiros do Azure no Windows](storage-dotnet-how-to-use-files.md)

  Este artigo fornece uma descrição geral de partilhas de ficheiros do Azure e como toomount e utilizá-los com o PowerShell e .NET.
* [Inside Azure File storage](https://azure.microsoft.com/blog/inside-azure-file-storage/) (Por dentro do armazenamento de Ficheiros do Azure)

  Este artigo announces disponibilidade geral do Olá do File storage do Azure e fornece detalhes técnicos sobre a encriptação de Olá SMB 3.0.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>Utilizar dados de toosecure encriptação do lado do cliente que enviar toostorage
Outra opção que o ajuda a garantir que os dados estão seguros durante a transferência entre uma aplicação de cliente e o armazenamento é a encriptação do lado do cliente. dados de Olá são encriptados antes de serem transferidos para o armazenamento do Azure. Ao obter dados de Olá do armazenamento do Azure, Olá é desencriptar os dados depois de recebido do lado do cliente de Olá. Apesar de Olá os dados são encriptados vai entre a transmissão Olá, é recomendável que também utilizar HTTPS, porque tem verificações de integridade de dados incorporadas que ajudam a mitigar os erros de rede que afeta a integridade de Olá dos dados de Olá.

A encriptação do lado do cliente também é um método para encriptar os dados inativos, como dados de Olá são armazenados no respetivo formato encriptado. Iremos falar sobre esta mais detalhadamente na secção de Olá no [encriptação de Inativos](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Encriptação de Inativos
Existem três funcionalidades do Azure que fornecem encriptação de inativos. Encriptação de disco do Azure é utilizado tooencrypt Olá SO e discos de dados em máquinas de virtuais do IaaS. Olá outros dois – encriptação do lado do cliente e SSE – são ambos os dados de tooencrypt utilizados no armazenamento do Azure. Vamos examinar cada uma destas e, em seguida, não uma comparação e ver quando cada um deles pode ser utilizado.

Apesar de poder utilizar dados de Olá tooencrypt de encriptação do lado do cliente em trânsito (que também é armazenado no respetivo formato encriptado no armazenamento), poderá preferir toosimply utilize HTTPS durante a transferência de Olá e ter alguma forma para Olá dados toobe encriptado automaticamente quando é armazenados. Existem duas formas toodo isto – Azure Disk Encryption e SSE. Um é utilizado toodirectly encriptar os dados Olá SO e discos de dados utilizados por VMs, não sendo Olá outro dados de tooencrypt utilizados escritos tooAzure Blob Storage.

### <a name="storage-service-encryption-sse"></a>Encriptação do serviço de armazenamento (SSE)
SSE permite-lhe toorequest que o serviço de armazenamento Olá encripta automaticamente os dados de Olá quando escrita tooAzure armazenamento. Ao ler os dados de Olá do armazenamento do Azure, vai ser desencriptado pelo serviço de armazenamento Olá antes de a ser devolvido. Isto permite-lhe toosecure os dados sem ter toomodify code ou adicionar código tooany aplicações.

Esta é uma definição aplica-se a conta de armazenamento todo toohello. Pode ativar e desativar esta funcionalidade alterando o valor de Olá da definição de Olá. toodo, pode utilizar Olá de portal do Azure, PowerShell Olá CLI do Azure, Olá API de REST de fornecedor de recursos de armazenamento ou Olá biblioteca de clientes de armazenamento do .NET. Por predefinição, o SSE está desativada.

Neste momento, as chaves de Olá utilizadas para encriptação de Olá são geridas pela Microsoft. Iremos gerar chaves de Olá originalmente e gerir armazenamento seguro de Olá de chaves de Olá, bem como a rotação regular Olá conforme definido pela política interna do Microsoft. Olá futura, irá obter Olá capacidade toomanage as suas próprias chaves de encriptação e forneça um caminho de migração a partir das chaves gerida pela Microsoft geridos toocustomer chaves.

Esta funcionalidade está disponível para Standard e Premium Storage contas criadas utilizando o modelo de implementação do Resource Manager Olá. SSE aplica-se apenas tooblock os blobs, os blobs de páginas e blobs de acréscimo. Olá outros tipos de dados, incluindo tabelas, filas e ficheiros, não serão encriptados.

Dados apenas são encriptados quando SSE está ativada e dados de Olá são escritos tooBlob armazenamento. Ativar ou desativar SSE não afeta a dados existentes. Por outras palavras, quando ativar esta encriptação, possa não voltar atrás e encriptar os dados que já existe nem será-desencriptar dados Olá que já existe ao desativar SSE.

Se quiser toouse esta funcionalidade com uma conta do storage clássicas, pode criar uma nova conta de armazenamento do Resource Manager e utilizar o AzCopy toocopy Olá dados toohello nova conta.

### <a name="client-side-encryption"></a>Encriptação do lado do cliente
Encriptação do lado do cliente foi mencionado quando debater encriptação Olá dos dados de Olá em trânsito. Esta funcionalidade permite-lhe tooprogrammatically encripta os seus dados numa aplicação de cliente antes de a enviar em Olá durante a transmissão toobe escrito tooAzure armazenamento e tooprogrammatically desencriptar os dados após a obtenção-lo a partir do armazenamento do Azure.

Isto fornece encriptação em trânsito, mas também fornece funcionalidade de Olá de encriptação de inativos. Tenha em atenção que apesar dos dados de Olá são encriptados em trânsito, recomendamos a utilizar o HTTPS tootake advantage de verificações de integridade de dados incorporados Olá que ajudam a mitigar os erros de rede que afeta a integridade de Olá dos dados de Olá.

É um exemplo de onde pode utilizar esta opção se tiver uma aplicação web que armazena os blobs e obtém os blobs e pretender aplicação Olá e dados toobe como seguras quanto possível. Nesse caso, utilizaria encriptação do lado do cliente. tráfego de Olá entre Olá serviço Blob do Azure e o cliente Olá contém recursos Olá encriptado e ninguém pode interpretar dados Olá em trânsito e reconstitute-lo para os blobs privados.

Encriptação do lado do cliente está incorporada no Olá Java e Olá .NET armazenamento bibliotecas de cliente, que por sua vez utilizam Olá APIs de Cofre de chave do Azure, facilitando pretty para lhe tooimplement. processo de Olá de encriptação e desencriptação de dados de Olá utiliza técnica de envelope Olá e armazena os metadados utilizados pela encriptação de Olá em cada objeto de armazenamento. Por exemplo, para blobs, armazena-lo nos metadados do blob Olá, enquanto para filas, adiciona-tooeach mensagem da fila.

Para a encriptação de Olá em si, pode gerar e gerir as suas próprias chaves de encriptação. Também pode utilizar as chaves geradas pelo Olá biblioteca de clientes do Storage do Azure ou pode ter Olá Cofre de chaves do Azure gerar chaves de Olá. Pode armazenar as chaves de encriptação no seu armazenamento de chaves no local ou, pode armazená-las num cofre de chaves do Azure. O Cofre de chaves do Azure permite-lhe segredos de toohello toogrant acesso os utilizadores de toospecific do Cofre de chaves do Azure utilizando o Azure Active Directory. Isto significa que não apenas a qualquer pessoa pode ler Olá Cofre de chaves do Azure e obter chaves Olá que estiver a utilizar para a encriptação do lado do cliente.

#### <a name="resources"></a>Recursos
* [Encriptar e desencriptar blobs no armazenamento do Microsoft Azure com o Cofre de chaves do Azure](storage-encrypt-decrypt-blobs-key-vault.md)

  Este artigo mostra como encriptação do lado do cliente toouse com o Cofre de chaves do Azure, incluindo como toocreate Olá KEK e armazene-o num cofre Olá através do PowerShell.
* [Encriptação do lado do cliente e o Azure Cofre de chaves para o armazenamento do Microsoft Azure](storage-client-side-encryption.md)

  Este artigo fornece uma explicação de encriptação do lado do cliente e fornece exemplos de como utilizar Olá armazenamento cliente tooencrypt e desencriptar recursos de biblioteca Olá quatro dos serviços de armazenamento. Também aborda o Cofre de chaves do Azure.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>Utilizar o Azure Disk Encryption tooencrypt discos utilizados pela suas máquinas virtuais
Encriptação de disco do Azure é uma funcionalidade nova. Esta funcionalidade permite-lhe discos do tooencrypt Olá SO e discos de dados utilizados pela máquina Virtual IaaS. Para o Windows, Olá unidades são encriptadas utilizando a tecnologia de encriptação do BitLocker de norma da indústria. Para Linux, discos Olá são encriptados utilizando a tecnologia de Olá DM-Crypt. Este é integrado com o Cofre de chaves do Azure tooallow toocontrol e gerir chaves de encriptação de disco Olá.

solução Olá suporta Olá os seguintes cenários para VMs de IaaS quando são ativados no Microsoft Azure:

* Integração com o Cofre de chaves do Azure
* O escalão Standard VMs: [A, D, DS, G, GS e série Sim forth VMs do IaaS](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Ativar a encriptação em Windows e as VMs de IaaS Linux
* A desativação da encriptação nos dados e SO unidades para as VMs de IaaS Windows
* A desativação da encriptação em unidades de dados para as VMs de IaaS Linux
* Ativar a encriptação em VMs de IaaS que estão a executar SO de cliente do Windows
* Ativar a encriptação em volumes com caminhos de montagem
* Ativar a encriptação em VMs do Linux que estão configurados com o disco striping (RAID) utilizando mdadm
* Ativar a encriptação em VMs do Linux utilizando LVM para discos de dados
* Ativar a encriptação em VMs do Windows que são configuradas através da utilização de espaços de armazenamento
* Todas as regiões públicas do Azure são suportadas

solução Olá não suporta Olá os seguintes cenários, funcionalidades e tecnologias versão Olá:

* Escalão básico VMs do IaaS
* A desativação da encriptação numa unidade do SO para as VMs de IaaS Linux
* VMs de IaaS que são criados utilizando o método de criação de VM Olá clássico
* Integração com o serviço de gestão de chaves no local
* File storage do Azure (sistema de ficheiros partilhados), sistema de ficheiros de rede (NFS), volumes dinâmicos e VMs do Windows que estão configurados com sistemas RAID baseados em software


> [!NOTE]
> Encriptação de disco de SO Linux é atualmente suportada nas Olá seguir as distribuições do Linux: RHEL 7.2, CentOS 7.2n e Ubuntu 16.04.
>
>

Esta funcionalidade garante que todos os dados nos seus discos da máquina virtual são encriptados em pausa no armazenamento do Azure.

#### <a name="resources"></a>Recursos
* [Encriptação de disco do Azure para o Windows e as VMs de Linux IaaS](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Comparação de encriptação de disco do Azure, SSE e encriptação do lado do cliente
#### <a name="iaas-vms-and-their-vhd-files"></a>VMs de IaaS e os respetivos ficheiros VHD
Para discos utilizados por VMs de IaaS, recomendamos a utilização do Azure Disk Encryption. Pode ativar o SSE tooencrypt Olá de ficheiros VHD que são utilizado tooback destes discos no armazenamento do Azure, mas, encripta apenas dados recentemente gravados. Isto significa que se criar uma VM e, em seguida, ativar SSE na conta de armazenamento de Olá que contém o ficheiro VHD Olá, apenas as alterações de Olá serão encriptadas, não Olá ficheiro VHD original.

Se criar uma VM utilizando uma imagem de Olá Azure Marketplace, o Azure executa um [shallow cópia](https://en.wikipedia.org/wiki/Object_copying) de Olá imagem tooyour conta de armazenamento no armazenamento do Azure e não está encriptada, mesmo se tiver SSE ativada. Depois de cria Olá VM e começa a atualizar imagem Olá, SSE começará a encriptação de dados de Olá. Por este motivo, é melhor toouse que em VMs do Azure Disk Encryption criado a partir de imagens na Olá Azure Marketplace se de que quer que eles totalmente encriptados.

Se trouxer uma VM previamente encriptada no Azure no local, irá ser capaz de tooupload Olá encriptação chaves tooAzure Cofre de chaves e continuar a utilizar a encriptação de Olá para essa VM que estava a utilizar no local. Encriptação de disco do Azure está ativada toohandle neste cenário.

Se tiver o VHD não encriptadas no local, pode carregá-la na Galeria de Olá como uma imagem personalizada e aprovisionar uma VM a partir do mesmo. Se o fizer com modelos do Resource Manager Olá, pode colocar-tooturn no Azure Disk Encryption quando arrancarem Olá VM.

Quando adicionar um disco de dados e montá-la no Olá VM, pode ativar o Azure Disk Encryption esse disco de dados. Esta encriptará primeiro esse disco de dados localmente e, em seguida, camada de gestão do serviço de Olá irá efetuar uma operação de escrita em Diferido com o armazenamento para que Olá armazenamento conteúdo é encriptado.

#### <a name="client-side-encryption"></a>Encriptação do lado do cliente
Encriptação do lado do cliente é o método mais seguro do Olá de encriptar os dados, dado que encripta-a antes de trânsito e encripta Olá dados inativos. No entanto, requerem que aplicações tooyour de código a utilizar o armazenamento, o que poderá pretender que o adicione toodo. Nesses casos, pode utilizar o HTTPs para os dados em trânsito e SSE tooencrypt Olá dadosem rest.

Com a encriptação do lado do cliente, pode encriptar as entidades da tabela, fila de mensagens e os blobs. Com SSE, apenas pode encriptar blobs. Se precisar de tabela e fila toobe dados encriptado, deve utilizar a encriptação do lado do cliente.

Encriptação do lado do cliente é gerida completamente pelo aplicação Olá. Esta é a abordagem mais segura de Olá, mas necessita que a aplicação de tooyour toomake programático alterações e colocar os processos de gestão de chaves no local. Pretende utilizar este quando quiser Olá segurança adicional durante trânsito e pretender toobe os dados armazenados encriptado.

A encriptação do lado do cliente é mais carga no cliente Olá e tiver tooaccount para isto no seu plano de escalabilidade, especialmente se estiver a encriptação e a transferência de uma grande quantidade de dados.

#### <a name="storage-service-encryption-sse"></a>Encriptação do serviço de armazenamento (SSE)
SSE é gerida pelo armazenamento do Azure. Através de SSE não fornecem segurança Olá dos dados de Olá em trânsito, mas encriptar os dados de Olá como é escrito tooAzure armazenamento. Não há nenhum impacto no desempenho Olá quando utilizar esta funcionalidade.

Apenas pode encriptar blobs de blocos, blobs de acréscimo e utilizar SSE de blobs de páginas. Se precisar de dados da tabela tooencrypt ou dados de fila, deve considerar a utilização de encriptação do lado do cliente.

Se tiver um arquivo ou biblioteca de arquivos VHD que utilizar como base para a criação de novas máquinas virtuais, pode criar uma nova conta de armazenamento, ativar SSE e, em seguida, carregue a conta de toothat Olá VHD ficheiros. Esses ficheiros VHD serão encriptados pelo armazenamento do Azure.

Se tiver ativado para discos de Olá no SSE ativada numa conta de armazenamento de Olá que contém Olá ficheiros VHD e VM do Azure Disk Encryption, que funcionará ajustar; irá resultar num quaisquer dados escritos recentemente a ser encriptados duas vezes.

## <a name="storage-analytics"></a>Análise de Armazenamento
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>Utilizando o tipo de autorização de toomonitor de análise de armazenamento
Para cada conta de armazenamento, pode ativar o registo de tooperform de análise de armazenamento do Azure e armazenar dados de métricas. Esta é uma ótima ferramenta toouse quando pretende métricas de desempenho de Olá toocheck de uma conta de armazenamento ou, precisa tootroubleshoot uma conta de armazenamento porque estão a ter problemas de desempenho.

Outro conjunto de dados, pode ver nos registos de análise do armazenamento de Olá é o método de autenticação de Olá utilizado por outra quando acedem ao armazenamento. Por exemplo, com o Blob Storage, pode ver se utilizaram uma assinatura de acesso partilhado ou chaves de conta de armazenamento hello, ou se blob Olá acedido foi público.

Isto pode ser realmente útil se totalmente são guarding toostorage de acesso. Por exemplo, no Blob Storage pode definir todas Olá contentores tooprivate e implementar a utilização de Olá de um serviço SAS em toda as suas aplicações. Em seguida, pode verificar Olá os registos regularmente toosee se os blobs são acedidos através de chaves de conta do Olá armazenamento, que podem indicar uma violação de segurança, ou se blobs Olá são públicos, mas não deve ser.

#### <a name="what-do-hello-logs-look-like"></a>Hello registos aspeto?
Depois de ativar as métricas de conta do storage Olá e iniciar sessão através do portal do Azure de Olá, dados de análise serão iniciada tooaccumulate rapidamente. registo de Olá e métricas para cada serviço está separada; registo de Olá é escrito apenas quando existe atividade nessa conta de armazenamento, enquanto as métricas de Olá serão registadas a cada minuto, a cada hora ou todos os dias, dependendo de como configurar.

Olá registos são armazenados em blobs de blocos num contentor com o nome $logs na conta do storage Olá. Este contentor é criado automaticamente quando a análise de armazenamento está ativada. Uma vez criado neste contentor, que não é possível eliminá-lo, apesar de poder eliminar o respetivo conteúdo.

No recipiente Olá $logs, existe uma pasta para cada serviço, e, em seguida, existem subpastas para Olá ano/mês/dia/hora. Na hora, registos de Olá simplesmente são numerados. Trata-se de que Olá estrutura de diretórios terá um aspeto semelhante:

![Vista de ficheiros de registo](./media/storage-security-guide/image1.png)

Cada tooAzure pedido armazenamento é registado. Eis um instantâneo de um ficheiro de registo, que mostra Olá primeiro insuficiente de campos.

![Instantâneo de um ficheiro de registo](./media/storage-security-guide/image2.png)

Pode ver o que é possível utilizar Olá registos tootrack qualquer tipo de conta de armazenamento de tooa de chamadas.

#### <a name="what-are-all-of-those-fields-for"></a>Quais são todas essas campos para?
Não há um artigo listado em recursos de Olá abaixo, que fornece a lista de Olá de Olá muitos dos campos no Olá registos e o que são utilizadas. Eis Olá lista de campos por ordem:

![Instantâneo de campos num ficheiro de registo](./media/storage-security-guide/image3.png)

Estamos interessados em entradas de Olá para GetBlob e a forma como os que são autenticados, por isso, vamos precisar toolook entradas com "Get-BLOBs" de tipo de operação de e Olá-estado do pedido de verificação (4<sup>ésimo</sup> coluna) e o tipo de autorização Olá (8<sup>ésimo</sup> coluna).

Por exemplo, no Olá primeiro algumas linhas numa listagem de Olá acima, Olá-estado do pedido é "Êxito" e o tipo de autorização Olá é "autenticado". Isto significa que o pedido de Olá foi validado com a chave de conta do storage Olá.

#### <a name="how-are-my-blobs-being-authenticated"></a>Como são os meus blobs que está a ser autenticados?
Temos três cenários que, se estiver interessados em.

1. Olá do blob é público e é acedido através de um URL sem uma assinatura de acesso partilhado. Neste caso, Olá-estado do pedido é "AnonymousSuccess" e o tipo de autorização Olá é "anónimo".

   1.0; 2015-11-17T02:01:29.0488963Z; GetBlob; **AnonymousSuccess**200; 124; 37; **anónimo**; mystorage...
2. blob Olá é privado e foi utilizado com uma assinatura de acesso partilhado. Neste caso, Olá-estado do pedido é "SASSuccess" e o tipo de autorização Olá é "sas".

   1.0; 2015-11-16T18:30:05.6556115Z; GetBlob; **SASSuccess**; 200; 416 64; **SAs**; mystorage...
3. blob Olá é privado e chave de armazenamento Olá foi utilizado tooaccess-lo. Neste caso, o estado do Olá pedido é "**êxito**"e é do tipo de autorização Olá"**autenticado**".

   1.0; 2015-11-16T18:32:24.3174537Z; GetBlob; **Êxito**; 206; 59 22; **autenticado**; mystorage...

Pode utilizar Olá Microsoft Message Analyzer tooview e analisar estes registos. Inclui capacidades de pesquisa e filtrar. Por exemplo, poderá pretender toosearch para instâncias de GetBlob toosee se a utilização de Olá é o que esperar, ou seja, toomake se alguém é não aceder à sua conta do storage inadequada.

#### <a name="resources"></a>Recursos
* [Análise de Armazenamento](storage-analytics.md)

  Este artigo é uma descrição geral da análise de armazenamento e como tooenable-los.
* [Formato de registo de análise de armazenamento](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  Este artigo ilustra Olá formato de registo de análise de armazenamento e detalhes Olá campos disponíveis nas mesmas, incluindo tipo de autenticação, que indica o tipo de Olá de autenticação utilizado para Olá pedido.
* [Monitorizar uma conta de armazenamento no Olá portal do Azure](storage-monitor-storage-account.md)

  Este artigo mostra como tooconfigure monitorização das métricas e registo de uma conta de armazenamento.
* [Resolução de problemas de ponto-a-ponto utilizando as métricas do Storage do Azure e o registo, o AzCopy e o Message Analyzer](storage-e2e-troubleshooting.md)

  Este artigo aborda a resolução de problemas com Olá análise de armazenamento e mostra como toouse Olá Microsoft Message Analyzer.
* [Guia de funcionamento de analisador de mensagens da Microsoft](https://technet.microsoft.com/library/jj649776.aspx)

  Este artigo é uma referência de Olá para Olá Microsoft Message Analyzer e inclui tutorial tooa de ligações, o início rápido e o resumo da funcionalidade.

## <a name="cross-origin-resource-sharing-cors"></a>Partilha de Recursos Transversais à Origem (CORS)
### <a name="cross-domain-access-of-resources"></a>Acesso entre domínios de recursos
Quando um browser em execução num domínio faz um pedido HTTP para um recurso de outro domínio, isto denomina-se um pedido HTTP de várias origens. Por exemplo, uma página HTML servida a partir contoso.com faz um pedido para um jpeg alojado no fabrikam.blob.core.windows.net. Por motivos de segurança, os browsers restrinja os pedidos HTTP de várias origens iniciados a partir de scripts, como JavaScript. Isto significa que quando código JavaScript numa página web em contoso.com solicita que jpeg no fabrikam.blob.core.windows.net, browser Olá não permitirá que o pedido de Olá.

O que faz esta ter toodo com armazenamento do Azure? Se estiver a armazenar recursos estáticos, tais como ficheiros de dados JSON ou XML no Blob Storage através de uma conta de armazenamento denominado Fabrikam, domínio Olá para recursos de Olá fabrikam.blob.core.windows.net, e aplicação de web contoso.com Olá não será capaz de tooaccess-las utilizando o JavaScript porque domínios Olá são diferentes. Isto também se aplica se está a tentar toocall um Olá dos serviços de armazenamento do Azure – por exemplo, o Table Storage – que devolvem JSON dados toobe processado pelo cliente de JavaScript Olá.

#### <a name="possible-solutions"></a>Possíveis soluções
Uma forma tooresolve trata tooassign um domínio personalizado, como "storage.contoso.com" toofabrikam.blob.core.windows.net. problema de Olá é que só possa atribuir essa conta de armazenamento de tooone de domínio personalizado. E se os elementos de Olá são armazenados em várias contas de armazenamento?

Outra forma tooresolve este é o ato de aplicação web do toohave Olá como um proxy para Olá chamadas de armazenamento. Isto significa que o se estiver a carregar um ficheiro tooBlob armazenamento, aplicação web de Olá seria gravá-lo localmente e, em seguida, copie-tooBlob armazenamento ou seria possível ler todos os-la na memória e escrevem-tooBlob armazenamento. Em alternativa, pode escrever uma aplicação web dedicado (por exemplo, uma API Web) que carrega Olá ficheiros localmente e escreve-los tooBlob armazenamento. Qualquer forma, terá de tooaccount nessa função quando precisa de determinar escalabilidade de Olá.

#### <a name="how-can-cors-help"></a>Como pode ajudar a CORS?
Armazenamento do Azure permite-lhe tooenable CORS – cruzam a partilha de recursos de origem. Para cada conta de armazenamento, pode especificar os domínios que podem aceder a recursos de Olá nessa conta de armazenamento. Por exemplo, no nosso caso descrito acima, podemos pode ativar a CORS na conta de armazenamento de fabrikam.blob.core.windows.net Olá e configurá-lo tooallow acesso toocontoso.com. Em seguida, Olá web aplicação contoso.com pode aceder diretamente ao recursos Olá fabrikam.blob.core.windows.net.

Uma coisa toonote é que permite o acesso CORS, mas não fornece autenticação, o que é necessária para todos os não-acesso público de recursos de armazenamento. Isto significa que só pode aceder blobs se forem públicos ou incluir uma assinatura de acesso partilhado que lhe confere Olá permissões adequadas. As tabelas, filas e os ficheiros têm sem acesso de público e exigem uma SAS.

Por predefinição, a CORS está desativada em todos os serviços. Pode ativar a CORS utilizando Olá REST API ou Olá armazenamento cliente biblioteca toocall uma das políticas do serviço Olá métodos tooset Olá. Quando, fazê-lo, incluir uma regra CORS, que está a ser XML. Eis um exemplo de uma regra CORS que foi definida utilizando a operação definir propriedades de serviço Olá Olá serviço Blob para uma conta de armazenamento. Pode efetuar essa operação utilizando a biblioteca de clientes do storage Olá ou Olá REST APIs para o Storage do Azure.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Eis o que significa que cada linha:

* **AllowedOrigins** Isto indica quais os domínios que não correspondente podem pedir e receber dados a partir do serviço de armazenamento Olá. Isto indica que contoso.com e fabrikam.com podem pedir a dados de armazenamento de BLOBs para uma conta de armazenamento específico. Também pode definir esta universal tooa (\*) os pedidos de todos os domínios tooaccess tooallow.
* **AllowedMethods** se Olá lista de métodos (verbos de pedido HTTP) que podem ser utilizados quando efetua o pedido de Olá. Neste exemplo, são permitidas apenas PUT e GET. Pode definir esta universal tooa (\*) tooallow todos os métodos toobe utilizado.
* **AllowedHeaders** este é o pedido de Olá cabeçalhos Olá domínio de origem podem especificar quando efetua o pedido de Olá. Neste exemplo, todos os cabeçalhos de metadados a partir x-ms-meta-data, x-ms-meta-destino e x-ms-meta-abc permitidos. Olá caráter universal (\*) indica que o início qualquer cabeçalho com Olá especificado prefixo é permitido.
* **ExposedHeaders** Isto indica que os cabeçalhos de resposta devem ser expostos pelo emissor do Olá browser toohello pedido. Neste exemplo, qualquer cabeçalho começados por "x-ms - meta-" irá ser exposto.
* **MaxAgeInSeconds** trata Olá período de tempo máximo que um browser serão colocados em cache pedidos de opções de verificação prévia Olá. (Para obter mais informações sobre o pedido de verificação prévia de Olá, consulte o artigo primeiro Olá abaixo.)

#### <a name="resources"></a>Recursos
Para obter mais informações sobre a CORS e como tooenable-lo, consulte estes recursos.

* [Suporte de partilha de recursos de várias origens (CORS) para Olá dos serviços de armazenamento do Azure no Azure.com](storage-cors-support.md)

  Este artigo fornece uma descrição geral de CORS e como tooset Olá regras Olá diferentes dos serviços de armazenamento.
* [Suporte de partilha de recursos de várias origens (CORS) para Olá dos serviços de armazenamento do Azure no MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Esta é a documentação de referência de Olá para suporte de CORS Olá Azure dos serviços de armazenamento. Isto tem tooarticles ligações aplicar tooeach armazenamento e mostra um exemplo e explica cada elemento no ficheiro CORS Olá.
* [Storage do Microsoft Azure: CORS de introdução](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Este é um artigo de blogue inicial ligação toohello anunciar CORS e que mostra como toouse-lo.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Perguntas mais frequentes sobre a segurança de armazenamento do Azure
1. **Como verificar a integridade Olá de blobs de Olá que posso estou transferir ou a sair do armazenamento do Azure se não é possível utilizar o protocolo HTTPS de Olá?**

   Se por qualquer motivo, precisa de toouse HTTP em vez de HTTPS e estiver a trabalhar com blobs de blocos, pode utilizar a verificar o MD5 toohelp Verificar integridade Olá de blobs de Olá a serem transferidos. Isto irá ajudar com proteção de erros de camada de transporte/rede, mas não necessariamente com ataques intermediário.

   Se é possível utilizar HTTPS, que fornece segurança ao nível do transporte, em seguida, a utilização de MD5 a verificação é redundante e desnecessários.

   Para obter mais informações, consulte Olá [descrição geral do Azure Blob MD5](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **O que sobre a conformidade FIPS para Olá E.U.A. Governo dos EUA?**

   Olá dos Estados Unidos Federal Information processamento Standard (FIPS) define os algoritmos criptográficos aprovados para utilização pelos E.U.A. Governo Federal dos sistemas de para proteção de Olá de dados confidenciais. Ativar FIPS modo num ambiente de trabalho do Windows server ou indica Olá SO que devem ser utilizados apenas validados FIPS algoritmos criptográficos. Se uma aplicação utiliza algoritmos não conformes, aplicações de Olá irão interromper. Versões de With.NET Framework 4.5.2 ou superior, aplicação Olá automaticamente muda algoritmos de toouse compatíveis com FIPS de algoritmos de criptografia Olá quando o computador Olá está no modo FIPS.

   Microsoft mantém cópias de segurança tooeach cliente toodecide se tooenable o modo FIPS. Acreditamos que não é não existe nenhuma razão apelativa para os clientes que não são modo do requerente toogovernment regulamentos tooenable FIPS por predefinição.

   **Recursos**

* [Por que motivo está a não recomendamos "Modo FIPS" já](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  Este artigo de blogue fornece uma descrição geral do FIPS e explica por que motivo não ativar modo FIPS por predefinição.
* [O FIPS 140 validação](https://technet.microsoft.com/library/cc750357.aspx)

  Este artigo fornece informações sobre como produtos da Microsoft e os módulos criptográficos está em conformidade com a norma FIPS de Olá para Olá E.U.A. Governo Federal dos EUA.
* ["Criptografia de sistema: Utilize FIPS algoritmos compatíveis com para a encriptação, hashing e iniciar sessão" efeitos de definições de segurança no Windows XP e em versões posteriores do Windows](https://support.microsoft.com/kb/811833)

  Este artigo aborda utilização Olá modo FIPS no computadores mais antigas do Windows.
