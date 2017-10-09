---
title: "aaaMicrosoft Explorador de armazenamento do Azure 0.8.7 (pré-visualização) | Microsoft Docs"
description: "Notas de versão do Explorador de armazenamento do Microsoft Azure 0.8.7 (pré-visualização)"
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Explorador de armazenamento do Microsoft Azure 0.8.7 (pré-visualização)
## <a name="overview"></a>Descrição geral
Este artigo contém notas de versão Olá para versão de pré-visualização do Explorador de armazenamento do Azure 0.8.7.

[Explorador de armazenamento do Microsoft Azure (pré-visualização)](./vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma que lhe permite tooeasily trabalho com dados de armazenamento do Azure no Windows, macOS e Linux.

## <a name="azure-storage-explorer-087-preview"></a>Explorador de armazenamento do Azure 0.8.7 (pré-visualização)
### <a name="download-azure-storage-explorer-087-preview"></a>Transferir o Explorador de armazenamento do Azure 0.8.7 (pré-visualização)
- [Pré-visualização 0.8.7 do Explorador de armazenamento do Azure para Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Pré-visualização 0.8.7 do Explorador de armazenamento do Azure para Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Pré-visualização 0.8.7 do Explorador de armazenamento do Azure para Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Novas atualizações
* Pode escolher como tooresolve conflitos no início de Olá de uma atualização, transferir ou copiar sessão Olá **atividades** janela.
* Coloque o cursor sobre um separador toosee Olá caminho completo do recurso de armazenamento Olá.
* Ao clicar num separador, sincroniza-se com a localização no painel de navegação do lado esquerdo de Olá.

### <a name="fixes"></a>Correções
* Fixo: Explorador de armazenamento agora é uma aplicação no macOS fidedigna.
* Fixo: Ubuntu 14.04 é novamente suportado.
* Fixo:, Por vezes, hello adicionar IU da conta está intermitente ao carregar as subscrições.
* Fixo:, Por vezes, nem todos os recursos de armazenamento foram listados no painel de navegação esquerda Olá.
* Fixo: painel de ações de Olá por vezes apresentado ações vazias.
* Fixo: tamanho da janela Olá da sessão de Olá fechada pela última vez é agora retido.
* Corrigido: Pode abrir vários separadores para Olá mesmo recurso utilizando o menu de contexto de Olá.

### <a name="known-issues"></a>Problemas conhecidos
* Acesso rápido funciona apenas com itens de subscrição. Recursos locais ou recursos ligados através de chave ou o SAS token não são suportados nesta versão.
* -Pode demorar alguns segundos toonavigate toohello recurso de destino, dependendo da quantidade de recursos tem acesso rápido.
* Ter mais de três grupos de blobs ou ficheiros de carregamento no Olá mesmo tempo poderá causar erros.
* Os identificadores de pesquisa procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado ou pode fazer com que exceções não processadas.
* Para Olá pela primeira vez utilizando Olá Explorador de armazenamento no macOS, poderá ver vários pedidos solicitando a keychain de Olá de tooaccess de permissão do utilizador. Sugerimos que selecionou **permitir sempre** para linha hello não voltar a apresentar

## <a name="previous-releases"></a>Versões anteriores
### <a name="features"></a>Funcionalidades
#### <a name="main-features"></a>Principais funcionalidades
* macOS, Linux e as versões do Windows
* A iniciar sessão tooview as contas de armazenamento agrupados por subscrição:
    * Utilize a sua conta da organização, Account Microsoft, 2FA, etc.
    * Configurar e gerir as definições de proxy
    * Remover as contas ao terminar a sessão
* Ligar a contas tooStorage utilizando:
    * Nome da conta e chave
    * Pontos finais personalizados (incluindo o Azure China)
    * URI de SAS para contas de armazenamento
* Suporte do Azure Resource Manager e o armazenamento clássico
* Gerar chaves de SAS para blobs, contentores de BLOBs, filas, tabelas ou partilhas de ficheiros
* Ligar tooblob contentores, filas, tabelas ou partilhas de ficheiros com a chave de assinaturas de acesso partilhado (SAS)
* Gerir políticas de acesso armazenada para contentores de BLOBs, filas, tabelas ou partilhas de ficheiros
* Armazenamento de desenvolvimento local com o emulador de armazenamento (apenas Windows)
* Criar e eliminar contentores de BLOBs, filas ou tabelas
* Os contentores de BLOBs de vista $logs e $metrics tabelas
* Procure específicos blobs, filas, tabelas ou partilhas de ficheiros
* Contas de toostorage hiperligações diretas ou contentores, filas, tabelas ou ficheiro partilha para a partilha e facilmente aceder aos seus recursos
* Mudar o nome de contentores de BLOBs, tabelas, partilhas de ficheiros
* Capacidade toomanage e configurar as regras CORS
* Copiar facilmente a chave primária e secundária para contas de armazenamento
* MD5 verifica no carregamento e transferência para a integridade dos dados e consistência
* Procure os contentores de BLOBs, tabelas, filas, partilhas de ficheiros ou as contas do storage a partir da caixa de pesquisa de Olá
* Pode agora pin utilizado mais frequentemente serviços toohello acesso rápido para navegação fácil
* Pode agora abrir editores vários separadores diferentes. Tooopen um separador temporário; de clique único Faça duplo clique tooopen um separador permanente. Também pode clicar em Olá separador temporário toomake um separador permanente
* Melhorias de desempenho e a estabilidade percetível para carregamentos e transferências, especialmente para ficheiros grandes em máquinas rápidas
* Iremos são reintroducing procura avançada de âmbito Olá e o conceito de Olá adicionado de controlo de âmbito. Introduza o nó de tooa Olá caminho através do ícone de passagem de Olá, clique direito -> "Pesquisa de aqui", ou manualmente tooscope nesse nó. Depois de um âmbito, pode adicionar um end de toohello termo de pesquisa de pesquisa de toodeep Olá caminho a partir desse nó
* Foi adicionado temas vários: claro (predefinição), escuros, elevado contraste negra e elevado contraste em branco.
* Aceda tooEdit -> temas toochange sua preferência de temas
* No Linux, um SO de 64 bits é agora necessário
* Iremos foi atualizado com a nossa logótipo!
#### <a name="blobs"></a>Blobs
* Ver os blobs e navegar através de diretórios
* Carregar, transferir, eliminar e copiar os blobs e pastas
* Abra e visualize os blobs de texto e imagem de conteúdo de Olá
* Ver e editar propriedades de BLOBs e metadados
* Procurar blobs pelo prefixo
* Criar e quebra de concessões de blobs e contentores de BLOBs
* Arraste 'n drop tooupload de ficheiros
* Mudar o nome de blobs e pastas
* Pastas "virtuais" vazias agora podem ser criadas em contentores de BLOBs
* Pode modificar propriedades de Blob e o ficheiro de Olá
#### <a name="tables"></a>Tabelas
* Ver e consultar entidades com ODATA ou utilizar consultas complexas de toocreate do construtor de consultas
* Adicionar, editar, eliminar entidades
* Importar e exportar os conteúdos de tabela num formato CSV (incluindo a exportar resultados de consulta)
* Personalizar a ordem das colunas
* Consultas de toosave de capacidade
#### <a name="queues"></a>Filas
* Pré-visualizar as 32 mensagens mais recentes
* Adicionar, anular, ver as mensagens
* Limpar fila
* Tornamos-possíveis para toodecide se pretende que tooencode/decode a fila de mensagens
#### <a name="file-shares"></a>Partilhas de Ficheiros
* Ver os ficheiros e navegue através de diretórios
* Carregar, transferir, eliminar e copiar ficheiros e diretórios
* Ver propriedades de ficheiro
* Mudar o nome de ficheiros e diretórios

### <a name="bug-fixes"></a>Correções de erros
* Corrigido: Ecrã freezing problemas
* Fixo: Segurança avançada

### <a name="known-issues"></a>Problemas conhecidos
* Pesquisa de identificadores de procura em aproximadamente 50 000 nós - depois da primeira, o desempenho pode ser afetado macOS instalação pode necessitar de permissões elevadas
* Painel de definições de conta pode mostrar que precisa de subscrições de toofilter tooreenter credenciais
* Mudar o nome de blobs (individualmente ou dentro de um contentor do blob cujo nome foi alterado) não preserva a instantâneos. Todas as outras propriedades e metadados para blobs, ficheiros e entidades são preservados durante uma mudança de nome
* Pilha do Azure não suporta atualmente os ficheiros, por isso tentar tooexpand Olá **ficheiros** nó resulta num erro
* Instalação de Linux 14.04 tem de versão do gcc atualizado ou atualizado. Olá passos seguintes mostram como tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Versões anteriores
#### <a name="october-2016-release-version-085"></a>Versão de Outubro de 2016 (versão 0.8.5)
* [Transferir para o Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Transferir para Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Transferir para Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
