---
title: "aaaOffline sincronização de dados no Azure Mobile Apps | Microsoft Docs"
description: "Referência conceptual e descrição geral da funcionalidade de sincronização de dados offline Olá para Mobile Apps do Azure"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Sincronização de Dados Offline nas Aplicações Móveis do Azure
## <a name="what-is-offline-data-sync"></a>O que é a sincronização de dados offline?
Sincronização de dados offline é um cliente e servidor funcionalidade SDK do Azure Mobile Apps que torna mais fácil para os programadores toocreate aplicações que estão funcionais sem uma ligação de rede.

Quando a aplicação está no modo offline, pode ainda criar e modificar dados, que são guardados arquivo local tooa. Quando estiver novamente online aplicação Olá, este possa sincronizar alterações locais com o back-end da aplicação móvel do Azure. funcionalidade de Olá também inclui suporte para detetar conflitos quando Olá registo mesmo é alterado em ambos hello do cliente e Olá back-end. Em seguida, podem ser processados conflitos no servidor de Olá ou cliente Olá.

Sincronização offline tem várias vantagens:

* Melhorar a capacidade de resposta da aplicação ao colocar em cache dados de servidor localmente no dispositivo de Olá
* Criar aplicações robustas que permanecem útil quando existem problemas de rede
* Permitir toocreate dos utilizadores finais e modificar dados, mesmo quando há sem acesso de rede, o suporte para cenários com pouca ou nenhuma conectividade
* Sincronizar os dados em vários dispositivos e detetar conflitos quando hello registo mesmo é modificado pelo dois dispositivos
* Limitar a utilização de rede em redes de alta latência ou com tráfego limitado

Olá seguintes tutoriais mostra como tooadd offline Sincronizar clientes móveis tooyour utilizar Mobile Apps do Azure:

* [Android: Ativar a sincronização offline]
* [Apache Cordova: Ativar a sincronização offline](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS: Ativar a sincronização offline]
* [Xamarin iOS: Ativar a sincronização offline]
* [Xamarin Android: Ativar a sincronização offline]
* [Xamarin. Forms: Sincronização offline ativar](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [plataforma Universal do Windows: Ativar a sincronização offline]

## <a name="what-is-a-sync-table"></a>O que é uma tabela de sincronização?
tooaccess Olá "/ tabelas" ponto final, cliente do Azure Mobile Olá SDKs fornecem interfaces como `IMobileServiceTable` (cliente SDK do .NET) ou `MSTable` (iOS cliente). Estas APIs se ligue diretamente toohello back-end da aplicação móvel do Azure e falharem se o dispositivo de cliente Olá não tem uma ligação de rede.

utilização offline toosupport, a aplicação em vez disso, deve utilizar Olá *tabela sincronização* APIs, tais como `IMobileServiceSyncTable` (cliente SDK do .NET) ou `MSSyncTable` (iOS cliente). Olá todas as mesmas operações CRUD (criar, ler, atualizar, eliminar) funcionam com sincronização de APIs de tabela, exceto agora ler a partir de ou escrever tooa *arquivo local*. Antes de quaisquer operações de tabela de sincronização podem ser efetuadas, o arquivo local Olá tem de ser inicializado.

## <a name="what-is-a-local-store"></a>O que é um arquivo local?
Um arquivo local é Olá camada de persistência de dados no dispositivo de cliente Olá. cliente de Mobile Apps do Azure Olá SDKs fornecem uma predefinição local armazenar implementação. No Windows, Xamarin e Android, se baseia no SQLite. No iOS, se baseia nos dados de núcleos.

toouse Olá SQLite implementação baseada no Windows Phone ou loja Windows 8.1, tem de tooinstall uma extensão do SQLite. Para obter mais informações, consulte [plataforma Universal do Windows: Ativar a sincronização offline]. Android e iOS são enviados juntamente com uma versão do SQLite no dispositivo Olá sistema operativo, pelo que não é necessário tooreference sua própria versão do SQLite.

Os programadores também podem implementar os seus próprios arquivo local. Por exemplo, se desejar toostore dados num formato encriptado no cliente para dispositivos móveis Olá, pode definir um arquivo local que utiliza SQLCipher para encriptação.

## <a name="what-is-a-sync-context"></a>O que é um contexto de sincronização?
A *contexto de sincronização* está associado um objeto de cliente móvel (tais como `IMobileServiceClient` ou `MSClient`) e regista as alterações efetuadas com tabelas de sincronização. contexto de sincronização de Olá mantém um *fila operação*, que mantém uma lista ordenada de operações de CUD (criação, atualização, eliminação) que seja posterior enviado toohello servidor.

Um arquivo local está associado com o contexto de sincronização de Olá utilizando um método de inicialização, tais como `IMobileServicesSyncContext.InitializeAsync(localstore)` no Olá [SDK de cliente .NET].

## <a name="how-sync-works"></a>Funciona como offline de sincronização
Quando utilizar tabelas de sincronização, o código de cliente controla quando alterações locais sejam sincronizadas com um back-end de aplicação móvel do Azure. Nada é enviado back-end de toohello até uma chamada demasiado*push* alterações locais. Da mesma forma, o arquivo local Olá é preenchido com novos dados apenas quando existe uma chamada demasiado*solicitação* dados.

* **Push**: Push é uma operação no contexto de sincronização de Olá e envia todas as alterações CUD desde push último Olá. Tenha em atenção que é toosend não é possível apenas alterações de uma tabela individuais, porque, caso contrário operações foi enviadas fora de ordem. Push executa uma série de REST chamadas tooyour aplicação móvel do Azure back-end, que por sua vez modifica a base de dados do servidor.
* **Solicitar**: solicitação é executada numa base por tabela e podem ser personalizadas com uma consulta tooretrieve apenas um subconjunto de dados do servidor Olá. Olá SDKs de cliente do Azure Mobile e inserir dados resultantes Olá no arquivo local Olá.
* **Pushes implícitas**: se uma solicitação for executada em relação a uma tabela que tem atualizações locais pendentes, extração de Olá primeiro executa um `push()` no contexto de sincronização de Olá. Este push ajuda a minimizar conflitos entre as alterações que já estão a ser colocados em fila e novos dados a partir do servidor de Olá.
* **Sincronização incremental**: Olá primeiro parâmetro toohello solicitação operação é um *nome da consulta* que é utilizado apenas no cliente Olá. Se utilizar um nome de consulta não nulo, Olá SDK do Azure Mobile efetua uma *sincronização incremental*. Sempre que uma operação de solicitação devolve um conjunto de resultados, hello mais recente `updatedAt` timestamp desse conjunto de resultados é armazenado nas tabelas de sistema local Olá SDK. Operações de extração subsequentes obter registos apenas após esse timestamp.

  a sincronização incremental toouse, o servidor tem de devolver significativo `updatedAt` os valores e também tem de suportar ordenar por este campo. No entanto, uma vez que Olá SDK adiciona o seu próprio ordenação no campo de updatedAt Olá, não é possível utilizar uma consulta de extração que tenha a sua própria `orderBy` cláusula.

  nome da consulta Olá pode ser qualquer cadeia que escolher, mas tem de ser exclusivo para cada consulta na sua aplicação lógica.
  Caso contrário, as operações de extração diferente foi substituir Olá mesmo timestamp de sincronização incremental e as suas consultas podem devolver resultados incorretos.

  Se a consulta de Olá tem um parâmetro, toocreate unidirecional um nome exclusivo de consulta é o valor do parâmetro Olá tooincorporate.
  Por exemplo, se está a filtrar no ID de utilizador, o nome da consulta foi constar da seguinte forma (c#):

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Se quiser tooopt fora de sincronização incremental, transmitir `null` como Olá ID de consulta. Neste caso, todos os registos da mesma são obtidos em cada chamada demasiado`PullAsync`, que é potencialmente ineficaz.
* **Remover**: pode apagar conteúdo de Olá da utilização de arquivo local Olá `IMobileServiceSyncTable.PurgeAsync`.
  Remover poderá ser necessário se tiver dados obsoletos na base de dados de cliente de hello, ou se quiser toodiscard todas as alterações pendentes.

  Uma remoção limpa uma tabela a partir do arquivo local Olá. Se existirem operações a aguardar sincronização com Olá servidor da base de dados, gera de remoção de Olá uma exceção a menos que Olá *Forçar remoção* parâmetro está definido.

  Como um exemplo de dados obsoletos no cliente Olá, suponha que no exemplo de "lista de tarefas" Olá, Device1 obtém apenas os itens que não estão concluídas. Um todoitem "Comprar milk" está marcado como foi concluído no servidor de Olá por outro dispositivo. No entanto, Device1 ainda tem Olá "Comprar milk" todoitem no arquivo local porque-lo é extrair apenas itens que não estão marcado concluída. Uma remoção limpa este item obsoleto.

## <a name="next-steps"></a>Passos seguintes
* [iOS: Ativar a sincronização offline]
* [Xamarin iOS: Ativar a sincronização offline]
* [Xamarin Android: Ativar a sincronização offline]
* [plataforma Universal do Windows: Ativar a sincronização offline]

<!-- Links -->
[SDK de cliente .NET]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android: Ativar a sincronização offline]: app-service-mobile-android-get-started-offline-data.md
[iOS: Ativar a sincronização offline]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS: Ativar a sincronização offline]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android: Ativar a sincronização offline]: app-service-mobile-xamarin-android-get-started-offline-data.md
[plataforma Universal do Windows: Ativar a sincronização offline]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
