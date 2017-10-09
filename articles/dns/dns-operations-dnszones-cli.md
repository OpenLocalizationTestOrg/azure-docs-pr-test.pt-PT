---
title: aaaManage DNS zonas no DNS do Azure - Azure CLI 2.0 | Microsoft Docs
description: Pode gerir zonas DNS a utilizar o Azure CLI 2.0. Este artigo mostra como tooupdate, eliminar e criar zonas DNS no DNS do Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 8ab63bc4-5135-4ed8-8c0b-5f0712b9afed
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: gwallace
ms.openlocfilehash: 3945a558b2db3490e50678d8395a47e55a85c8fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-azure-dns-using-hello-azure-cli-20"></a>Como toomanage zonas de DNS no DNS do Azure utilizando Olá Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [CLI do Azure 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [CLI 2.0 do Azure](dns-operations-dnszones-cli.md)


Este guia mostra como toomanage seu DNS zonas utilizando Olá entre plataformas CLI do Azure, que está disponível para o Windows, Mac e Linux. Também pode gerir as zonas DNS utilizando [Azure PowerShell](dns-operations-dnszones.md) ou Olá portal do Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá

Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

* [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md) -nosso CLI para Olá clássica e resource Gestão modelos de implementação.
* [Azure CLI 2.0](dns-operations-dnszones-cli.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá.

## <a name="introduction"></a>Introdução

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-20-for-azure-dns"></a>Configurar a CLI 2.0 do Azure para o Azure DNS

### <a name="before-you-begin"></a>Antes de começar

Certifique-se de que tem Olá seguintes itens antes de iniciar a configuração.

* Uma subscrição do Azure. Se ainda não tiver uma subscrição do Azure, pode ativar os [Benefícios de subscritor do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou inscrever-se numa [conta gratuita](https://azure.microsoft.com/pricing/free-trial/).

* Instale a versão mais recente do Olá do Olá 2.0 CLI do Azure, disponível para Windows, Linux ou Mac. Estão disponíveis mais informações no [Olá de instalação do Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

### <a name="sign-in-tooyour-azure-account"></a>Inicie sessão no tooyour a conta do Azure

Abra uma janela de consola e autentique com as suas credenciais. Para obter mais informações, consulte o registo no tooAzure de Olá CLI do Azure

```
az login
```

### <a name="select-hello-subscription"></a>Selecione a subscrição de Olá

Verifique Olá subscrições para a conta de Olá.

```
az account list
```

Escolha qual das suas toouse de subscrições do Azure.

```azurecli
az account set --subscription "subscription name"
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos

O Azure Resource Manager requer que todos os grupos de recursos especifiquem uma localização, Isto é utilizado como localização predefinida de Olá para recursos nesse grupo de recursos. No entanto, uma vez que todos os recursos DNS são globais, não regionais, escolha de Olá de localização do grupo de recursos não tem impacto no DNS do Azure.

Pode ignorar este passo se estiver a utilizar um grupo de recursos existente.

```azurecli
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>Obter ajuda

Todos os comandos de CLI 2.0 referentes tooAzure DNS começar a utilizar `az network dns`. Ajuda está disponível para cada comando utilizando Olá `--help` opção (formato curto `-h`).  Por exemplo:

```azurecli
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>Criar uma zona DNS

Uma zona DNS é criada utilizando Olá `az network dns zone create` comando. Para obter ajuda, consulte `az network dns zone create -h`.

Olá exemplo seguinte cria uma zona DNS denominada *contoso.com* no grupo de recursos de Olá denominado *MyResourceGroup*:

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="toocreate-a-dns-zone-with-tags"></a>toocreate uma zona DNS com etiquetas

Olá exemplo seguinte mostra como toocreate um DNS zona com dois [etiquetas do Azure Resource Manager](dns-zones-records.md#tags), *projeto = demonstração* e *env = test*, utilizando Olá `--tags` parâmetro (formato curto `-t`):

```azurecli
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>Obter uma zona DNS

tooretrieve uma zona DNS, utilize `az network dns zone show`. Para obter ajuda, consulte `az network dns zone show --help`.

Olá exemplo seguinte devolve zona DNS Olá *contoso.com* e os respetivos dados associados do grupo de recursos *MyResourceGroup*. 

```azurecli
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

Olá seguinte o exemplo é resposta Olá.

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

Tenha em atenção que os registos DNS não são devolvidos pelo `az network dns zone show`. Utilize registos DNS toolist, `az network dns record-set list`.


## <a name="list-dns-zones"></a>Zonas DNS de lista

tooenumerate zonas DNS, utilize `az network dns zone list`. Para obter ajuda, consulte `az network dns zone list --help`.

Grupo de recursos de Olá especificação lista apenas dessas zonas dentro do grupo de recursos de Olá:

```azurecli
az network dns zone list --resource-group MyResourceGroup
```

Grupo de recursos de Olá omitindo apresenta uma lista de todas as zonas na subscrição Olá:

```azurecli
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>Atualize uma zona DNS

Tooa alterações recursos de zona DNS podem ser efetuados utilizando `az network dns zone update`. Para obter ajuda, consulte `az network dns zone update --help`.

Este comando não atualizar qualquer um dos conjuntos de registos DNS Olá dentro da zona de Olá (consulte [como registos DNS tooManage](dns-operations-recordsets-cli.md)). É tooupdate utilizados apenas propriedades de recurso de zona de Olá próprio. Estas propriedades são actualmente limitada toohello [do Azure Resource Manager 'etiquetas'](dns-zones-records.md#tags) para o recurso de zona Olá.

Olá exemplo seguinte mostra como Olá tooupdate etiquetas numa zona DNS. etiquetas existente Olá são substituídas pelos Olá valor especificado.

```azurecli
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>Eliminar uma zona DNS

Zonas DNS podem ser eliminadas utilizando `az network dns zone delete`. Para obter ajuda, consulte `az network dns zone delete --help`.

> [!NOTE]
> Também eliminar uma zona DNS elimina todos os registos DNS na zona de Olá. Esta operação não pode ser anulada. Se a zona DNS Olá está a ser utilizado, serviços, utilizando a zona de Olá irão falhar quando zona Olá é eliminada.
>
>tooprotect contra eliminação acidental de zona, consulte [como tooprotect DNS zonas e regista](dns-protect-zones-recordsets.md).

Este comando solicita a confirmação. Olá opcional `--yes` comutador suprime esta linha de comandos.

Olá exemplo seguinte mostra como toodelete Olá zona *contoso.com* do grupo de recursos *MyResourceGroup*.

```azurecli
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>Passos seguintes

Saiba como demasiado[gerir conjuntos de registos e registos](dns-getstarted-create-recordset-cli.md) na sua zona DNS.

Saiba como demasiado[delegar a tooAzure de domínio DNS](dns-domain-delegation.md).

