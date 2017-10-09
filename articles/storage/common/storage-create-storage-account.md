---
title: "aaaHow toocreate, gerir ou eliminar uma conta de armazenamento no portal do Azure de Olá | Microsoft Docs"
description: "Criar uma nova conta de armazenamento, gerir as chaves de acesso da conta ou elimine uma conta de armazenamento no Olá portal do Azure. Saiba mais sobre contas do Storage standard e premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Acerca das contas do Storage do Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Descrição geral
Uma conta de armazenamento do Azure fornece um espaço de nomes exclusivo toostore e aceder aos seus objetos de dados do Storage do Azure. Todos os objetos numa conta do Storage são faturados em conjunto como um grupo. Por predefinição, os dados de Olá na sua conta são tooyou apenas disponível, proprietário da conta Olá.

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Faturação da conta do Storage
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Quando cria uma máquina virtual do Azure, uma conta de armazenamento é criada por si automaticamente na localização de implementação de Olá se que ainda não tiver uma conta do storage nessa localização. Por isso, não é necessário toofollow Olá passos seguintes toocreate uma conta de armazenamento para os discos da máquina virtual. o nome de conta do storage Olá será baseado no nome da máquina virtual Olá. Consulte Olá [documentação de Virtual Machines do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) para obter mais detalhes.
> 
> 

## <a name="storage-account-endpoints"></a>Pontos finais da conta do Storage
Todos os objetos que armazena no Storage do Azure têm um endereço de URL exclusivo. formulários de nome de conta de armazenamento Olá Olá subdomínio desse endereço. Olá combinação de nome de domínio e subdomínio, que é específica tooeach serviço, forma um *endpoint* para a sua conta de armazenamento.

Por exemplo, se a sua conta do storage é denominada *mystorageaccount*, Olá os pontos finais predefinidos para a sua conta de armazenamento são:

* Serviço Blob: http://*mystorageaccount*.blob.core.windows.net
* Serviço Tabela: http://*mystorageaccount*.table.core.windows.net
* Serviço Fila: http://*mystorageaccount*.queue.core.windows.net
* Serviço Ficheiro: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Conta do Blob storage expõe apenas o ponto final de serviço do Olá Blob.
> 
> 

Olá URL para aceder a um objeto numa conta do storage é criado ao acrescentar a localização de um objeto de Olá num ponto final do toohello de conta de armazenamento do Olá. Por exemplo, um endereço de blob pode ter este formato: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

Também pode configurar um toouse de nome de domínio personalizado com a sua conta de armazenamento. Para obter mais informações, veja [Configurar um nome de domínio personalizado para o Ponto Final do Armazenamento de Blobs](../blobs/storage-custom-domain-name.md). Também pode configurá-lo com o PowerShell. Para obter mais informações, consulte Olá [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet.  


## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com).
2. No menu do Hub de Olá, selecione **novo** -> **armazenamento** -> **conta de armazenamento**.
3. Introduza um nome para a conta do Storage. Consulte [pontos finais da conta de armazenamento](#storage-account-endpoints) para obter detalhes sobre como o nome de conta do storage Olá será utilizado tooaddress os seus objetos no Storage do Azure.
   
   > [!NOTE]
   > Os nomes das contas do Storage devem ter entre 3 e 24 carateres de comprimento e apenas podem conter números e letras minúsculas.
   > 
   > O nome da sua conta do Storage tem de ser exclusivo no Azure. Olá portal do Azure indica se o nome de conta do storage Olá que selecionou já está em utilização.
   > 
   > 
4. Especifique toobe de modelo de implementação de Olá utilizada: **Resource Manager** ou **clássico**. **Gestor de recursos** Olá recomenda-se modelo de implementação. Para obter mais informações, consulte [Compreender a implementação do Resource Manager e a implementação clássica](../../azure-resource-manager/resource-manager-deployment-model.md).
   
   > [!NOTE]
   > Contas do blob storage só podem ser criadas utilizando o modelo de implementação do Resource Manager Olá.

5. Selecionar tipo de Olá da conta de armazenamento: **fins gerais** ou **armazenamento de BLOBs**. **Objetivo geral** Olá predefinido.
   
    Se **fins gerais** foi selecionado, em seguida, especifique a camada de desempenho de Olá: **padrão** ou **Premium**. predefinição de Olá é **padrão**. Para obter mais detalhes sobre as contas do storage standard e premium, consulte [introdução tooMicrosoft Storage do Azure](storage-introduction.md) e [Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](storage-premium-storage.md).
   
    Se **Blob Storage** foi selecionado, em seguida, especifique a camada de acesso de Olá: **frequente** ou **frios**. predefinição de Olá é **frequente**. Consulte [Blob Storage do Azure: camadas de acesso frequente e esporádico](../blobs/storage-blob-storage-tiers.md) para obter mais detalhes.
6. Selecione a opção de replicação de Olá Olá conta de armazenamento: **LRS**, **GRS**, **RA-GRS**, ou **ZRS**. predefinição de Olá é **RA-GRS**. Consulte [Replicação do Storage do Azure](storage-redundancy.md) para obter detalhes adicionais sobre as opções de replicação do Storage do Azure.
7. Selecione a subscrição de Olá em que pretende toocreate Olá nova conta do storage.
8. Especifique um novo grupo de recursos ou selecione um grupo de recursos existente. Para obter mais informações sobre os grupos de recursos, veja [Descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).
9. Selecione Olá localização geográfica para a sua conta de armazenamento. Veja [Regiões do Azure](https://azure.microsoft.com/regions/#services) para obter mais informações sobre os serviços que estão disponíveis em cada região.
10. Clique em **criar** conta de armazenamento de Olá toocreate.

## <a name="manage-your-storage-account"></a>Gerir a conta do Storage
### <a name="change-your-account-configuration"></a>Alterar a configuração da conta
Depois de criar a sua conta do storage, pode modificar a respetiva configuração, tal como alterar a opção de replicação de Olá utilizada para a conta de Olá ou camada de acesso de Olá mudança para uma conta do Blob storage. No Olá [portal do Azure](https://portal.azure.com), navegue até a conta de armazenamento tooyour, localizar e clique em **configuração** em **definições** tooview e/ou alterar a configuração da conta Olá.

> [!NOTE]
> Consoante a camada de desempenho Olá que escolheu ao criar a conta de armazenamento Olá, algumas opções de replicação podem não estar disponíveis.
> 
> 

Alterar a opção de replicação de Olá alterar seus preços. Para obter mais detalhes, consulte a página [Preços do Storage do Azure](https://azure.microsoft.com/pricing/details/storage/).

Para os BLOBs em contas do storage, alterar a camada de acesso de Olá podem implicar custos de Olá alterar além toochanging seus preços. Consulte Olá [contas do Blob storage – preços e faturação](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) para obter mais detalhes.

### <a name="manage-your-storage-access-keys"></a>Gerir as chaves de acesso ao armazenamento
Quando criar uma conta de armazenamento, o Azure gera duas chaves de acesso de armazenamento de 512 bits, que são utilizadas para autenticação quando aceder a conta de armazenamento Olá. Ao fornecer duas chaves de acesso de armazenamento, o Azure permite-lhe as chaves de Olá tooregenerate sem qualquer serviço de armazenamento de tooyour de interrupção ou o serviço de acesso a toothat.

> [!NOTE]
> Recomendamos que evite partilhar as chaves de acesso ao armazenamento com outras pessoas. aceder a toopermit toostorage recursos sem fornecer as chaves de acesso, pode utilizar um *assinatura de acesso partilhado*. Uma assinatura de acesso partilhado fornece acesso tooa recurso na sua conta para um intervalo que definir e com permissões de Olá que especificar. Veja [Utilizar Assinaturas de Acesso Partilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para obter mais informações.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Ver e copiar chaves de acesso ao armazenamento
No Olá [portal do Azure](https://portal.azure.com), navegue até tooyour conta de armazenamento, clique em **todas as definições** e, em seguida, clique em **chaves de acesso** tooview, copiar e regenerar as chaves de acesso da conta. Olá **chaves de acesso** painel também inclui cadeias de ligação pré-configuradas com as chaves primárias e secundárias que pode copiar toouse nas suas aplicações.

#### <a name="regenerate-storage-access-keys"></a>Voltar a gerar chaves de acesso ao armazenamento
Recomendamos que altere as chaves de acesso de Olá tooyour armazenamento periodicamente conta keep toohelp as ligações de armazenamento seguro. Duas chaves de acesso são atribuídas, de modo a que possa manter conta de armazenamento de toohello ligações através da utilização de uma chave de acesso enquanto volta a gerar Olá outra chave de acesso.

> [!WARNING]
> A regenerar as chaves de acesso pode afetar os serviços no Azure, bem como as suas próprias aplicações que são dependentes da conta de armazenamento Olá. Todos os clientes que utilizam a conta de armazenamento do Olá acesso à chave tooaccess Olá tem de ser nova chave Olá de toouse atualizado.
> 
> 

**Os Media services** -se tiver media services dependentes da sua conta de armazenamento, deve sincronizar novamente as chaves de acesso de Olá com o serviço de multimédia depois de voltar a gerar chaves de Olá.

**Aplicações** – se tiver aplicações web ou essa conta do storage Olá utilização dos serviços de nuvem, perderá Olá ligações se voltar a gerar chaves, a menos que reverta as chaves.

**Exploradores de armazenamento** - se estiver a utilizar quaisquer [aplicações de Explorador de armazenamento](storage-explorers.md), provavelmente terá de chave de armazenamento tooupdate Olá utilizada por essas aplicações.

Eis o processo de Olá para rodar as chaves de acesso de armazenamento:

1. Atualize as cadeias de ligação de Olá na sua chave de acesso secundária de Olá do aplicação código tooreference Olá da conta de armazenamento.
2. Regenere a chave de acesso primária de Olá para a sua conta de armazenamento. No Olá **chaves de acesso** painel, clique em **voltar a gerar chave1**e, em seguida, clique em **Sim** tooconfirm que pretende que o toogenerate uma nova chave.
3. Atualize as cadeias de ligação de Olá na sua chave de acesso primária novo do código tooreference Olá.
4. Chave de acesso secundária de voltar a gerar Olá no Olá mesma forma.

## <a name="delete-a-storage-account"></a>Eliminar uma conta do Storage
tooremove uma conta de armazenamento que já não estiver a utilizar, navegue até a conta de armazenamento toohello no Olá [portal do Azure](https://portal.azure.com)e clique em **eliminar**. Eliminar uma conta do storage elimina Olá toda conta, incluindo todos os dados na conta de Olá.

> [!WARNING]
> É toorestore não é possível uma conta do storage eliminada ou obter conteúdos de Olá que esta continha antes da eliminação. Ser tooback se a cópia de segurança nada quiser toosave antes de eliminar Olá conta. Isto também se aplica a quaisquer recursos na conta de Olá — depois de eliminar um blob, tabela, fila ou ficheiro, este é eliminado permanentemente.
> 

Se tentar toodelete uma conta de armazenamento associada a uma máquina virtual do Azure, poderá receber um erro sobre a conta de armazenamento de Olá ainda estão a ser utilizados. Para ajudar a resolver este erro, veja [Resolver erros ao eliminar as contas de armazenamento](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

## <a name="next-steps"></a>Passos seguintes
* [Explorador de armazenamento do Microsoft Azure](../../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.
* [Armazenamento de Blobs do Azure: camadas de acesso Frequente e Esporádico](../blobs/storage-blob-storage-tiers.md)
* [Replicação do Armazenamento do Azure](storage-redundancy.md)
* [Configurar Cadeias de Ligação do Armazenamento do Azure](../storage-configure-connection-string.md)
* [Transferência de dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md)
* Visite Olá [blogue da equipa de armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/).

