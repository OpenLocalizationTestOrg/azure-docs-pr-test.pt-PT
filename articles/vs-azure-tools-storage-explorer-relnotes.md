---
title: "notas de versão aaaMicrosoft Explorador de armazenamento do Azure (pré-visualização) | Microsoft Docs"
description: "Notas de versão do Explorador de armazenamento do Microsoft Azure (pré-visualização)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Notas de versão do Explorador de armazenamento do Microsoft Azure (pré-visualização)

Este artigo contém a versão de Olá notas do Explorador de armazenamento do Azure 0.8.16 (pré-visualização) da versão, bem como as notas de versão para versões anteriores.

[Explorador de armazenamento do Microsoft Azure (pré-visualização)](./vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma que lhe permite tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux.

## <a name="version-0816-preview"></a>Versão 0.8.16 (pré-visualização)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Transferir o Explorador de armazenamento do Azure 0.8.16 (pré-visualização)
- [Explorador de armazenamento do Azure 0.8.16 (pré-visualização) para Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Explorador de armazenamento do Azure 0.8.16 (pré-visualização) para Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Explorador de armazenamento do Azure 0.8.16 (pré-visualização) para Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>novo
* Quando abre um blob, Explorador de armazenamento solicitará tooupload Olá transferido ficheiros se for detetada alguma alteração
* Pilha de Azure início de sessão experiência melhorada
* Desempenho melhorado Olá de carregamento/transferência pequena muitos ficheiros no Olá mesmo tempo


### <a name="fixes"></a>Correções
* Para alguns tipos de BLOBs, escolher demasiado "substituir" durante um conflito de carregamento, por vezes, resultaria em carregamento Olá a ser reiniciado. 
* Na versão 0.8.15, carregamentos, por vezes, seriam compartimento de 99%.
* Ao carregar a partilha de ficheiros de tooa de ficheiros, se tiver escolhido o diretório de tooa tooupload que ainda não existe, o carregamento irão falhar.
* Explorador de armazenamento foi incorretamente gerar carimbos de data / hora para assinaturas de acesso partilhado e consultas de tabela.


Problemas conhecidos
* Atualmente, o utilizando um nome e a cadeia de ligação de chave não funcionam. -Será corrigida na versão seguinte Olá. Até que, em seguida, pode utilizar anexar com nome e chave.
* Se tentar tooopen um ficheiro com um nome de ficheiro do Windows inválido, transferências de Olá resultará num ficheiro não foi encontrado o erro.
* Depois de clicar em "Cancelar" uma tarefa, pode demorar um pouco para toocancel essa tarefa. Esta é uma limitação da biblioteca de nó de armazenamento do Azure Olá.
* Depois de concluir o carregamento de um blob, separador de Olá que iniciado o carregamento de Olá seja atualizada. Esta é uma alteração do comportamento anterior e também fará com que toobe direcionado novamente toohello raiz do contentor de Olá que estiver no.
* Se optar por Olá certificado incorreto de PIN/smart card, em seguida, terá de toorestart na ordem toohave Explorador de armazenamento se esqueça de que decisão.
* Painel de definições de conta Olá pode mostrar que precisa de subscrições de toofilter tooreenter credenciais.
* Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos. Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.
* Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada.
* Para os utilizadores no Ubuntu 14.04, terá de tooensure GCC está a funcionar toodate - Isto pode ser feito através da execução Olá os seguintes comandos e, em seguida, reiniciar o computador:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Para os utilizadores no Ubuntu 17.04, terá de tooinstall GConf - Isto pode ser feito Olá os seguintes comandos e, em seguida, reiniciar o computador a executar:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Versão 0.8.14 (pré-visualização)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização)
* [Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização) para Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização) para Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Transferir o Explorador de armazenamento do Azure 0.8.14 (pré-visualização) para Linux](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>novo

* Atualizado too1.7.2 de versão Electron na vantagem de tootake de ordem de várias atualizações de segurança críticas
* -Pode agora aceder rapidamente ao guia de resolução de problemas online Olá menu Ajuda Olá
* Explorador de armazenamento de resolução de problemas [guia][2]
* [Instruções] [ 3] sobre a ligação de subscrição do Azure pilha tooan

### <a name="known-issues"></a>Problemas conhecidos

* Botões de caixa de diálogo de confirmação do Olá Eliminar pasta não registar Olá cliques do rato no Linux. Solução é a chave do toouse Olá Enter
* Se optar por Olá certificado incorreto de PIN/smart card, em seguida, terá de toorestart na ordem toohave Explorador de armazenamento se esquecer da decisão de Olá
* Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros
* Painel de definições de conta Olá pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem
* Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos. Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.
* Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada. 
* Ubuntu 14.04 tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Versões anteriores

* [Versão 0.8.13](#version-0813)
* [Versão 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Versão 0.8.9 / 0.8.8](#version-089--088)
* [Versão 0.8.7](#version-087)
* [Versão 0.8.6](#version-086)
* [Versão 0.8.5](#version-085)
* [Versão 0.8.4](#version-084)
* [Versão 0.8.3](#version-083)
* [Versão 0.8.2](#version-082)
* [Versão 0.8.0](#version-080)
* [Versão 0.7.20160509.0](#version-07201605090)
* [Versão 0.7.20160325.0](#version-07201603250)
* [Versão 0.7.20160129.1](#version-07201601291)
* [Versão 0.7.20160105.0](#version-07201601050)
* [Versão 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Versão 0.8.13
05/12/2017

#### <a name="new"></a>novo

* Explorador de armazenamento de resolução de problemas [guia][2]
* [Instruções] [ 3] sobre a ligação de subscrição do Azure pilha tooan

#### <a name="fixes"></a>Correções

* Corrigido: O carregamento de ficheiros tinha uma elevada probabilidade de causar um fora de erro de memória
* Fixo: Pode agora iniciar sessão com PIN/smart card
* Corrigido: Abrir no Portal agora funciona com o Azure China, Datacenters do Azure, Azure US Government e pilha do Azure
* Corrigido: Ao carregar um contentor do blob tooa pasta, um erro de "Operação ilegal", por vezes, ocorreriam
* Corrigido: Selecionar tudo foi desativado durante a gestão de instantâneos
* Fixo: Olá metadados do blob base Olá podem obter substituídos depois de visualizar propriedades Olá dos respetivos instantâneos.

#### <a name="known-issues"></a>Problemas conhecidos

* Se optar por Olá certificado incorreto de PIN/smart card, em seguida, terá de toorestart na ordem toohave Explorador de armazenamento se esquecer da decisão de Olá
* Enquanto ampliado ou reduzir, o nível de zoom Olá momentaneamente pode repor nível predefinido de toohello
* Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros
* Painel de definições de conta Olá pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem
* Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos. Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.
* Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada. 
* Ubuntu 14.04 tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Versão 0.8.12 / 0.8.11 / 0.8.10
04/07/2017

#### <a name="new"></a>novo

* Explorador de armazenamento agora será fechada automaticamente quando instala uma atualização de notificação de atualização de Olá
* Acesso rápido no local fornece uma experiência melhorada para trabalhar com os recursos acedidos com frequência
* No editor de contentor do Blob Olá, agora, pode ver que o virtual machine um blob em leasing pertence
* Agora pode fechar o painel do lado esquerdo de Olá
* Deteção agora é executado em Olá mesmo tempo como transferência
* Estatísticas de utilização no contentor de BLOBs, a partilha de ficheiros e a tabela editores toosee Olá tamanho dos seus recursos ou a seleção de Olá
* Pode agora o início de sessão tooAzure Active Directory (AAD) com base em contas de pilha do Azure. 
* Pode agora mais 32 MB tooPremium as contas de armazenamento de ficheiros de arquivo de carregamento
* Suporte de acessibilidade de melhorada
* Agora pode adicionar fidedigna de Base-64 codificado certificados x. 509 SSL por vai tooEdit -&gt; certificados SSL -&gt; importar certificados

#### <a name="fixes"></a>Correções

* Fixo: depois de atualizar as credenciais de uma conta, vista de árvore Olá seria, por vezes, não atualiza automaticamente
* Corrigido: gerar uma SAS para tabelas e filas de emulador resultaria num URL inválido
* Fixo: contas de armazenamento premium podem agora ser expandidas enquanto um proxy está ativado
* Corrigido: Olá aplicar botão em contas de Olá página de gestão não funciona se tiver selecionadas de contas de 1 ou 0
* Fixo: carregar blobs que necessitam de resoluções de conflito poderão falhar - fixo em 0.8.11 
* Corrigido: enviar comentários foi quebrada em 0.8.11 - fixo em 0.8.12 

#### <a name="known-issues"></a>Problemas conhecidos

* Após a atualização too0.8.10, terá de toorefresh todas as suas credenciais.
* Enquanto ampliado ou reduzir, o nível de zoom Olá pode repor momentaneamente nível predefinido de toohello.
* Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá causar erros.
* Painel de definições de conta Olá pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem.
* Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos. Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome.
* Embora a pilha do Azure atualmente não suporta partilhas de ficheiros, um nó de partilhas de ficheiros continua a aparecer sob uma conta de armazenamento de pilha do Azure ligada. 
* Ubuntu 14.04 tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Versão 0.8.9 / 0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>novo

* Explorador de armazenamento 0.8.9 irá transferir automaticamente a versão mais recente do Olá para atualizações.
* CORREÇÃO: utilizar um portal gerado tooattach URI de SAS que uma conta de armazenamento resulta num erro.
* Agora pode criar, gerir e promover instantâneos do blob.
* Pode agora iniciar sessão em contas de tooAzure China, Datacenters do Azure e Azure US Government.
* Agora, pode alterar o nível de zoom Olá. Utilize as opções de Olá Olá vista menu tooZoom no Zoom Out e repor Zoom.
* Carateres Unicode já são suportados nos metadados de utilizador para os blobs e de ficheiros.
* Melhoramentos de acessibilidade.
* notas de versão do Olá próxima versão podem ser visualizadas de notificação de atualização de Olá. Também pode ver Olá atual notas de versão do menu de ajuda de Olá.

#### <a name="fixes"></a>Correções

* Fixo: número de versão Olá é agora apresentado corretamente no painel de controlo do Windows
* Corrigido: pesquisa já não se encontra limitada too50, 000 nós
* Fixo: partilha de ficheiros do carregamento tooa puserem para sempre se o diretório de destino Olá já não existe
* Fixa: estabilidade melhorada para carregamentos de tempo e as transferências

#### <a name="known-issues"></a>Problemas conhecidos

* Enquanto ampliado ou reduzir, o nível de zoom Olá pode repor momentaneamente nível predefinido de toohello.
* Acesso rápido só funciona com itens de subscrição com base. Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão.
* -Pode demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos tem acesso rápido.
* Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá causar erros.

12/16/2016
### <a name="version-087"></a>Versão 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>novo

* Pode escolher como tooresolve conflitos no início de Olá de uma atualização, transferir ou copiar sessão numa janela de atividades de Olá
* Coloque o cursor sobre um separador toosee Olá caminho completo do recurso de armazenamento Olá
* Ao clicar num separador, sincronizar com a localização no painel de navegação do lado esquerdo de Olá

#### <a name="fixes"></a>Correções

* Fixo: Explorador de armazenamento é agora uma aplicação fidedigna no Mac
* Fixo: Ubuntu 14.04 é novamente suportada
* Fixo:, Por vezes, Olá adicionar a conta está intermitente IU ao carregar as subscrições
* Fixo:, Por vezes, nem todos os recursos de armazenamento foram listados no painel de navegação do lado esquerdo de Olá
* Fixo: painel de ações de Olá por vezes apresentado ações vazias
* Fixo: tamanho da janela Olá da sessão de Olá fechada pela última vez é agora retido
* Corrigido: Pode abrir vários separadores para Olá mesmo recurso utilizando o menu de contexto de Olá

#### <a name="known-issues"></a>Problemas conhecidos

* Acesso rápido só funciona com itens de subscrição com base. Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão
* Poderá demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos possui um acesso rápido
* Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros
* Os identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado ou pode fazer com que a exceção não processada
* Para Olá pela primeira vez utilizando Olá Explorador de armazenamento no macOS, poderá ver vários pedidos solicitando a keychain de tooaccess de permissão do utilizador. Sugerimos que selecionou permitir sempre que, de modo linha Olá não apresentar novamente

11/18/2016
### <a name="version-086"></a>Versão 0.8.6

#### <a name="new"></a>novo

* Pode agora pin utilizado mais frequentemente serviços toohello acesso rápido para navegação fácil
* Pode agora abrir editores vários separadores diferentes. Tooopen um separador temporário; de clique único Faça duplo clique tooopen um separador permanente. Pode também clicar em Olá separador temporário toomake-um separador permanente
* Efetuamos desempenho percetível e melhoramentos estabilidade para carregamentos e transferências, especialmente para ficheiros grandes em máquinas rápidas
* Pastas "virtuais" vazias agora podem ser criadas em contentores de BLOBs
* Ter novamente introduzimos pesquisa de âmbito com a nossa nova pesquisa avançada subcadeia, pelo que tem agora duas opções para procurar: 
    * Global pesquisar - basta introduzir um termo de pesquisa na caixa de texto de pesquisa de Olá
    * Pesquisa de âmbito - clique Olá Lupa ícone tooa nó seguinte, em seguida, adicionar um end de toohello termo de pesquisa do caminho de Olá, ou com o botão direito e selecione "Pesquisa de aqui"
* Foi adicionado temas vários: claro (predefinição), escuros, elevado contraste negra e elevado contraste em branco. Aceda tooEdit -&gt; temas toochange sua preferência de temas
* Pode modificar as propriedades de Blob e ficheiro
* Agora suportamos o codificado (base64) e não codificado de fila de mensagens
* No Linux, um SO de 64 bits é agora necessário. Para esta versão suportamos apenas 64 bits Ubuntu 16.04.1 LTS
* Iremos foi atualizado com a nossa logótipo!

#### <a name="fixes"></a>Correções

* Corrigido: Ecrã freezing problemas
* Fixo: Segurança avançada
* Corrigido: Contas anexadas, por vezes, duplicadas foi apresentada
* Fixo: Um blob com um tipo de conteúdo foi possível gerar uma exceção
* Fixo: Olá de abrir o painel de consulta numa tabela vazia não foi possível
* Fixo: Erros na pesquisa de varia
* Fixo: Aumentar o número de Olá de recursos carregado a partir de 50 too100 quando clicar em "Mais carga"
* Corrigido: Na primeira execução, se uma conta é iniciada, iremos agora selecionar todas as subscrições para essa conta por predefinição 

#### <a name="known-issues"></a>Problemas conhecidos

* Esta versão do Olá Explorador de armazenamento não é executado no Ubuntu 14.04
* tooopen vários separadores para Olá mesmo recurso, efetue não continuamente, clique em Olá mesmo recurso. Clique no outro recurso e, em seguida, volte atrás e, em seguida, clique em Olá original recursos tooopen-lo novamente no outro separador 
* Acesso rápido só funciona com itens de subscrição com base. Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão
* Poderá demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos possui um acesso rápido
* Ter mais de 3 grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá fazer com erros
* Os identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado ou pode fazer com que a exceção não processada

10/03/2016
### <a name="version-085"></a>Versão 0.8.5

#### <a name="new"></a>novo

* Pode agora utilizar SAS gerado pelo Portal chaves tooattach tooStorage contas e recursos

#### <a name="fixes"></a>Correções

* Corrigido: condição provável de antecipação durante a pesquisa, por vezes, causado toobecome de nós não é possível expandir
* Fixo: "Utilizar HTTP" não funciona ao ligar a contas tooStorage com nome de conta e chave
* Fixo: Chaves SAS (especialmente gerado pelo Portal aqueles) devolverem um erro de "à direita barra"
* Fixo: tabela importar problemas
    * Por vezes, a chave de partição e a chave de linha foram inversa
    * Não é possível tooread "nulo" chaves de partição

#### <a name="known-issues"></a>Problemas conhecidos

* Identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado
* Pilha do Azure não suporta atualmente a ficheiros, pelo que tentar ficheiros tooexpand irá mostrar um erro

09/12/2016
### <a name="version-084"></a>Versão 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>novo

* Gerar contas de toostorage hiperligações diretas, contentores, filas, tabelas, ou partilhas de ficheiros para a partilha e fácil acedem a recursos de tooyour - Windows e Mac OS suporta
* Procure os contentores de BLOBs, tabelas, filas, partilhas de ficheiros ou as contas do storage a partir da caixa de pesquisa de Olá
* Agora pode agrupar cláusulas no construtor de consultas de tabela Olá
* Mudar o nome e copiar/colar contentores de BLOBs, partilhas de ficheiros, tabelas, blobs, blob pastas, ficheiros e diretórios de contas ligados por SAS e contentores
* Mudar o nome e a cópia dos contentores de BLOBs e partilhas de ficheiros agora preservar as propriedades e os metadados

#### <a name="fixes"></a>Correções

* Fixo: não é possível editar as entidades da tabela se contiverem propriedades booleanos ou binárias

#### <a name="known-issues"></a>Problemas conhecidos

* Identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado

08/03/2016
### <a name="version-083"></a>Versão 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>novo

* Mudar o nome de contentores, tabelas, partilhas de ficheiros
* Experiência melhorada de construtor de consultas
* Consultas de toosave e carga de capacidade
* Direcionar ligações toostorage contas ou contentores, filas, tabelas ou partilhas para a partilha e facilmente aceder aos seus recursos de ficheiros (apenas Windows - macOS suportam disponível em breve!)
* Capacidade toomanage e configurar as regras CORS

#### <a name="fixes"></a>Correções

* Fixo: Accounts Microsoft requerem reautenticação cada 8-12 horas

#### <a name="known-issues"></a>Problemas conhecidos

* Por vezes, hello IU pode aparecer congelada - maximizando a janela de Olá ajuda a resolver este problema
* instalação de macOS pode necessitar de permissões elevadas
* Painel de definições de conta pode mostrar que precisa de credenciais tooreenter em subscrições toofilter de ordem
* Partilhas de ficheiros de mudança de nome contentores de BLOBs, tabelas e não preservar metadados ou outras propriedades no contentor de Olá, tais como a quota de partilha de ficheiros, um nível de acesso público ou políticas de acesso
* Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos. Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome
* Copiar ou mudar o nome de recursos não funciona no contas ligados por SAS

07/07/2016
### <a name="version-082"></a>Versão 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>novo

* As contas de armazenamento estão agrupadas por subscrições; armazenamento de desenvolvimento e de recursos ligados através de SAS ou de chave são apresentados no nó (locais e anexadas)
* Terminar sessão das contas no painel de "Definições de conta do Azure"
* Configurar tooenable de definições de proxy e gerir o início de sessão
* Criar e quebra de concessões de blob
* Contentores de BLOBs aberta, filas, tabelas e os ficheiros de clique único

#### <a name="fixes"></a>Correções

* Corrigido: inseridas com bibliotecas .NET ou Java de fila de mensagens não é corretamente descodificar a partir de base64
* Fixo: $metrics tabelas não são apresentadas para contas do Blob Storage
* Fixo: nó de tabelas não funciona para o armazenamento (desenvolvimento) local

#### <a name="known-issues"></a>Problemas conhecidos

* instalação de macOS pode necessitar de permissões elevadas

06/15/2016
### <a name="version-080"></a>Versão 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>novo

* Suporte de partilha de ficheiros: ver, carregar, transferir, copiar ficheiros e diretórios, SAS URIs (criar e ligar)
* Experiência de utilizador para ligar tooStorage com SAS URIs ou chaves de conta melhorada
* Exportar os resultados da consulta de tabela
* Reordenação de coluna de tabela e personalização
* Ver os contentores de BLOBs de $logs e $metrics tabelas para contas de armazenamento com a métrica ativada
* Melhorado exportar e importar o comportamento, inclui agora o tipo de valor de propriedade

#### <a name="fixes"></a>Correções

* Fixo: carregar ou transferir blobs grandes pode resultar em carregamentos/transferências incompletas
* Editar fixo:, adicionar ou importar uma entidade com um valor de cadeia numérica ("1") irá convertê-lo toodouble
* Fixo: Não é possível tooexpand nó de tabela de Olá no ambiente de desenvolvimento local Olá

#### <a name="known-issues"></a>Problemas conhecidos

* $metrics tabelas não estão visíveis para contas do Blob Storage
* Fila de mensagens através de programação adicionadas não pode ser apresentada corretamente se mensagens hello são codificadas com codificação Base64

05/17/2016
### <a name="version-07201605090"></a>Versão 0.7.20160509.0

#### <a name="new"></a>novo

* Falhas de processamento para a aplicação de erros melhor

#### <a name="fixes"></a>Correções

* Erros fixo onde as mensagens de barra de informações por vezes, não apareçam quando as credenciais de início de sessão eram necessárias

#### <a name="known-issues"></a>Problemas conhecidos

* Tabelas: Adicionar, editar, ou importar uma entidade que tem uma propriedade com um valor numérico ambiguously, tais como "1" ou "1.0", e Olá utilizador tenta toosend-o como um `Edm.String`, valor de Olá regressará através do cliente de Olá API como um Edm.Double

03/31/2016

### <a name="version-07201603250"></a>Versão 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>novo

* Suporte de tabela: visualização, consultar, exportação, importar e as operações CRUD de entidades
* Suporte da fila: visualizar, adicionar, dequeueing mensagens
* Gerar o URI SAS para contas de armazenamento
* Ligar a contas de tooStorage URIs SAS
* Notificações de atualização para atualizações futuras tooStorage Explorer
* Atualizado para o aspeto e funcionalidade

#### <a name="fixes"></a>Correções

* Melhorias de desempenho e fiabilidade

### <a name="known-issues-amp-mitigations"></a>Problemas conhecidos &amp; mitigações

* Transferência de ficheiros grandes blob não funciona corretamente - é recomendável utilizar o AzCopy enquanto foi resolver este problema 
* As credenciais da conta não serão possível obter nem em cache se a pasta raiz de Olá não é possível localizar ou não pode ser escrita
* Se podemos são adicionar, editar ou importar uma entidade que tem uma propriedade com um valor numérico ambiguously, tais como "1" ou "1.0", e o utilizador Olá tenta toosend-o como um `Edm.String`, valor de Olá regressará através do cliente de Olá API como um Edm.Double
* Quando importar os ficheiros CSV com os registos de múltiplas linhas, os dados de Olá poderão obter chopped ou scrambled

02/03/2016

### <a name="version-07201601291"></a>Versão 0.7.20160129.1

#### <a name="fixes"></a>Correções

* Melhoria do desempenho global quando o carregamento, a transferência e copiar os blobs

01/14/2016

### <a name="version-07201601050"></a>Versão 0.7.20160105.0

#### <a name="new"></a>novo

* Apoio técnico para Linux (paridade funcionalidades tooOSX)
* Adicionar contentores de Blobs com a chave de assinaturas de acesso partilhado (SAS)
* Adicionar contas de armazenamento para o Azure China
* Adicionar contas de armazenamento com os pontos finais personalizados
* Abra e visualize os blobs de texto e imagem de conteúdo de Olá
* Ver e editar propriedades de BLOBs e metadados

#### <a name="fixes"></a>Correções

* Corrigido: carregamento ou transferência um grande número de blobs (500 +) pode, por vezes, fazer com que Olá aplicação toohave um ecrã branco 
* Fixo: quando definir o nível de acesso de público do contentor de blob, valor novo Olá não é atualizada até que defina novamente Olá focarem-se no contentor de Olá. Além disso, caixa de diálogo Olá sempre predefinições demasiado "não público aceder" e não Olá atual valor real.
* Geral melhor teclado acessibilidade e IU de suporte
* Texto de histórico de navegação estrutural encapsula num wrapper quando é longo com espaço em branco
* Caixa de diálogo SAS suporta a validação de entrada
* Armazenamento local continua toobe disponível mesmo se as credenciais de utilizador expiraram
* Quando é eliminado um contentor de blob aberta, o Explorador de blob Olá no lado direito de Olá está fechado

#### <a name="known-issues"></a>Problemas conhecidos

* Linux tem de instalar a versão do gcc atualizado ou atualizado – passos tooupgrade é abaixo: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>Versão 0.7.20151116.0

#### <a name="new"></a>novo

* macOS e as versões do Windows
* A iniciar sessão tooview as contas do Storage – utilizar a sua conta da organização, Account Microsoft, 2FA, etc.
* Armazenamento de desenvolvimento local (utilizar o emulador do storage apenas de Windows)
* Suporte de recursos do Azure Resource Manager e clássico
* Criar e eliminar blobs, filas ou tabelas
* Procurar blobs específicos, filas ou tabelas
* Explore os conteúdos de Olá de contentores de BLOBs
* Ver e navegar através de diretórios
* Carregar, transferir e eliminar os blobs e pastas
* Ver e editar propriedades de BLOBs e metadados
* Gerar chaves SAS
* Gerir e criar políticas de acesso armazenada (SAP)
* Procurar blobs pelo prefixo
* Arraste 'n drop tooupload de ficheiros ou transferir

#### <a name="known-issues"></a>Problemas conhecidos

* Ao definir o nível de acesso de público do contentor de blob, valor novo Olá não for atualizado até que defina novamente Olá focarem-se no contentor de Olá
* Quando abrir o nível de acesso público Olá diálogo tooset Olá, indica sempre "Sem acesso de público" como predefinição de Olá e não Olá atual valor real
* Não é possível mudar o nome de blobs transferidos
* Quando ocorre um erro e não é apresentado o erro de Olá de estado de entradas de registo de atividade será, por vezes, obter "presa" num em curso
* Por vezes, falhas ou activa completamente branco quando tenta tooupload ou transferir um grande número de blobs
* Por vezes, cancelar uma operação de cópia não funciona
* Durante a criação de um contentor (tabela/fila/BLOBs), se introduzir um nome inválido e continuar toocreate outro sob um tipo de contentor diferente, não é possível definir o foco no novo tipo de Olá
* Não é possível criar uma nova pasta ou mudar o nome de pasta




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md