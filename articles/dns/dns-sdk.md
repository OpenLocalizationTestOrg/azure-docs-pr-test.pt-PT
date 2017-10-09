---
title: "zonas DNS aaaCreate e conjuntos de registos no DNS do Azure utilizando Olá .NET SDK | Microsoft Docs"
description: "Como zonas DNS toocreate registos e conjuntos no DNS do Azure utilizando Olá .NET SDK."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Criar zonas DNS e conjuntos de registos utilizando Olá .NET SDK

Pode automatizar operações toocreate, delete ou update zonas DNS, os conjuntos de registos e registos utilizando o SDK de DNS com a biblioteca de gestão de DNS do .NET. Um projeto do Visual Studio completo está disponível [aqui.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)

## <a name="create-a-service-principal-account"></a>Criar uma conta do principal de serviço

Normalmente, é concedido acesso programático a recursos de tooAzure através de uma conta dedicada em vez das suas próprias credenciais de utilizador. Estas contas dedicadas são denominadas contas 'principal de serviço'. projeto de exemplo de Olá toouse SDK de DNS do Azure, primeiro precisa toocreate uma conta do principal de serviço e atribua-lhe permissões corretas Olá.

1. Siga [estas instruções](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate uma conta do principal de serviço (o projeto de exemplo do SDK de DNS do Azure Olá pressupõe autenticação baseada em palavra-passe).
2. Criar um grupo de recursos ([Eis como](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Utilização do Azure RBAC toogrant Olá serviço conta do principal 'Contribuinte da zona de DNS' permissões toohello grupo de recursos ([Eis como](../active-directory/role-based-access-control-configure.md).)
4. Se utilizar o projeto de exemplo Olá SDK de DNS do Azure, edite ficheiro de 'program.cs' Olá da seguinte forma:

   * Inserir valores corretos a Olá para tenantId Olá, clientId (também conhecido como ID de conta), o segredo (service principal conta palavra-passe) e subscriptionId como utilizada no passo 1.
   * Introduza o nome de grupo de recursos de Olá escolhido no passo 2.
   * Introduza um nome de zona DNS da sua preferência.

## <a name="nuget-packages-and-namespace-declarations"></a>Pacotes de NuGet e declarações de espaço de nomes

toouse Olá DNS do Azure .NET SDK, precisa de tooinstall Olá **biblioteca de gestão do DNS do Azure** pacote NuGet e outros necessitem pacotes do Azure.

1. No **Visual Studio**, abra um projeto ou um novo projeto.
2. Aceda demasiado**ferramentas**  **>**  **Gestor de pacotes NuGet**  **>**  **gerir pacotes NuGet para Solução...** .
3. Clique em **procurar**, ativar Olá **incluir pré-lançamento** caixa de verificação e escreva **Microsoft.Azure.Management.Dns** na caixa de pesquisa de Olá.
4. Selecione o pacote de Olá e clique em **instalar** tooadd-tooyour projeto do Visual Studio.
5. Repita o processo Olá acima tooalso Olá de instalar os seguintes pacotes: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Adicionar declarações de espaço de nomes

Adicione as seguintes declarações de espaço de nomes de Olá

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Inicializar o cliente de gestão do DNS Olá

Olá *DnsManagementClient* contém métodos Olá e as propriedades necessárias para gerir zonas DNS e recordsets.  Olá seguinte código regista na conta do principal de serviço toohello e cria um objeto de DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Criar ou atualizar uma zona DNS

toocreate uma zona DNS, primeiro "Zona" é criado um objeto parâmetros de zona DNS de Olá toocontain. Como zonas DNS não são região específica tooa ligado, a localização Olá está definida too'global'. Neste exemplo, um [do Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) também é adicionada toohello zona.

Criar tooactually ou atualização Olá zona no DNS do Azure, o objeto de zona Olá que contém os parâmetros de zona Olá é transmitida toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* método.

> [!NOTE]
> DnsManagementClient suporta três modos de funcionamento: síncrona ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrona com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').  Pode escolher qualquer um dos modos destas, dependendo das necessidades da sua aplicação.

O DNS do Azure suporta simultaneidade otimista, denominada [Etags](dns-getstarted-create-dnszone.md). Neste exemplo, especificar "*" para o cabeçalho de Olá 'If-None-Match' diz ao DNS do Azure toocreate uma zona DNS se ainda não existir.  Falha na chamada de Olá se já existir uma zona com o nome fornecido Olá na Olá dado o grupo de recursos.

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a>Criar conjuntos de registos de DNS e registos

Registos DNS são geridos como um conjunto de registos. Um conjunto de registos é um conjunto de registos com Olá mesmo nome e registe tipo dentro de uma zona.  nome do conjunto de registos de Olá é o nome da zona toohello relativo, não Olá nome DNS completamente qualificado.

toocreate ou atualização de um conjunto de registos, um objeto de parâmetros de "RecordSet" é criado e passou demasiado*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Como com zonas DNS, existem três modos de funcionamento: síncrona ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrona com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').

Tal como acontece com zonas DNS, operações em conjuntos de registos incluem suporte para simultaneidade otimista.  Neste exemplo, uma vez que não 'If-Match' nem 'If-None-Match' é especificados, conjunto de registos de Olá é sempre criado.  Esta chamada substitui quaisquer existente conjunto de registos com Olá mesmo nome e registe tipo nesta zona DNS.

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a>Obter conjuntos de registos e zonas

Olá *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* métodos obter zonas individuais e conjuntos de registos, respetivamente. RecordSets são identificados pelo respetivo tipo, o nome e o grupo de recursos e horário de Olá existam na. Zonas são identificadas pelo respetivo grupo de recursos de nome e Olá existam na.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Atualize um conjunto de registos existente

tooupdate um registo DNS existente definido, obtenha primeiro o conjunto de registos de Olá, em seguida, atualização Olá registo defina conteúdo, em seguida, submeter alteração Olá.  Neste exemplo, especificamos Olá 'Etag' a partir de Olá obter conjunto de registos no parâmetro de 'If-Match' Olá. chamada de Olá falha se uma operação simultânea alterou Olá conjunto de registos no Olá entretanto.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Os conjuntos de registos e zonas de lista

zonas toolist, utilize Olá *DnsManagementClient.Zones.List...*  métodos, que suportam a listar o todas as zonas de um grupo de recursos específico ou todas as zonas de uma determinada subscrição do Azure (em ficheiros de recursos grupos.) toolist os conjuntos de registos, utilizam *DnsManagementClient.RecordSets.List...*  métodos, que suportam a listagem de todos os conjuntos de registos numa determinada zona ou apenas os conjuntos de registos de um tipo específico.

Tenha em atenção quando listar zonas e poderão ser paginated conjuntos de registos resultante.  Olá seguinte exemplo mostra como tooiterate através de Olá nas páginas de resultados. (Um tamanho de página artificialmente pequeno de '2' utilizado tooforce paginação; na prática, este parâmetro deve ser omitido e Olá tamanho da página predefinido utilizado.)

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a>Passos seguintes

Transferir Olá [projeto de exemplo do SDK .NET da Azure DNS](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que inclui mais exemplos de como toouse Olá SDK .NET de DNS do Azure, incluindo exemplos para outros tipos de registos de DNS.
