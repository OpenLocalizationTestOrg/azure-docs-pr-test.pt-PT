---
title: "aaaAzure encriptação do serviço de armazenamento utilizar o cliente chaves geridas no Cofre de chaves do Azure | Microsoft Docs"
description: "Utilize tooencrypt de funcionalidade de encriptação do serviço de armazenamento de Azure Olá o armazenamento de Blobs do Azure no lado do serviço de Olá ao armazenar dados de Olá e desencriptá-lo ao obter dados de Olá com cliente chaves geridas."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: eb2e0ad27df40e61f9c08b9db7ca7a7568adad9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Encriptação do serviço de armazenamento utilizando o cliente chaves geridas no Cofre de chaves do Azure

Microsoft Azure está consolidada toohelping proteger e salvaguardar o dados toomeet seus compromissos de conformidade e segurança organizacional.  Uma forma de poder proteger os dados Inativos é toouse armazenamento serviço encriptação (SSE), que automaticamente encripta os dados ao escrever o mesmo toostorage e desencripta os dados ao obtê-lo. Olá, encriptação e desencriptação é completamente transparente, automática e utiliza 256 bits [encriptação AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), um bloco maior Olá cifras disponíveis.

Pode utilizar as chaves de encriptação gerida pela Microsoft com SSE ou pode utilizar as suas próprias chaves de encriptação. Este artigo aborda Olá anterior será ignorada. Para obter mais informações sobre a utilização de chaves gerida pela Microsoft, ou SSE no geral, consulte [encriptação do serviço de armazenamento para dados Inativos](../storage-service-encryption.md).

tooprovide toouse capacidade Olá as suas próprias chaves de encriptação, SSE para o Blob storage é integrado com o Cofre de chaves do Azure (AKV). Pode criar as suas próprias chaves de encriptação e armazená-las num AKV, ou pode utilizar as chaves de encriptação do AKV APIs toogenerate. Não só AKV permitem-lhe toomanage e controlar as chaves, também lhe permite tooaudit a utilização da chave. 

Motivo pelo qual pretenda que toocreate as suas próprias chaves? Proporciona uma maior flexibilidade, permitindo-lhe toocreate, rodar, desativar e definir os controlos de acesso. Também permite que as chaves de encriptação de Olá tooaudit utilizou tooprotect os dados.

## <a name="sse-with-customer-managed-keys-preview"></a>SSE pré-visualização do cliente chaves geridas

Esta funcionalidade encontra-se em pré-visualização. toouse esta funcionalidade, terá de toocreate uma nova conta de armazenamento. Pode criar um novo cofre de chaves e chave ou utilizar um cofre de chaves e a chave. conta de armazenamento de Olá e Cofre de chaves Olá tem de constar Olá mesma região, mas podem estar em diferentes subscrições.

tooparticipate pré-visualização de Olá, contacte [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Podemos irá fornecer tooparticipate uma ligação em pré-visualização Olá.

toolearn mais, consulte toohello [FAQ](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Tem de inscrever-se para Olá preview anteriores toofollowing Olá passos descritos neste artigo. Sem acesso de pré-visualização, não poderá ser capaz de tooenable esta funcionalidade no portal de Olá.

## <a name="getting-started"></a>Introdução
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Passo 1: [criar uma nova conta de armazenamento](../storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>Passo 2: Encriptação ativar
Pode ativar SSE para a conta de armazenamento de Olá utilizando Olá [portal do Azure](https://portal.azure.com). No painel de definições de Olá Olá conta de armazenamento, procure Olá secção de serviço Blob conforme mostrado no Olá figura a seguir e clique em encriptação.

![Portal captura de ecrã com a opção de encriptação](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)
<br/>*Ativar SSE para o serviço Blob*

Se pretender tooprogrammatically ativar ou desativar Olá encriptação do serviço de armazenamento numa conta de armazenamento, pode utilizar Olá [API de REST do fornecedor de recursos do Azure Storage](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), Olá [biblioteca de cliente do fornecedor de recursos de armazenamento para o .NET](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), ou Olá [CLI do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

Neste ecrã, se não forem apresentadas Olá "utilizar a sua própria chave" caixa de verificação, a não foram aprovada para pré-visualização Olá. Enviar um e-mail demasiado[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) e solicitar a aprovação.

![Portal captura de ecrã que mostra a pré-visualização de encriptação](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Por predefinição, SSE utiliza chaves gerida pela Microsoft. toouse as suas próprias chaves, selecione a caixa de Olá. Em seguida, pode especificar a chave de URI, ou selecione um cofre de chaves e uma chave de selecionador de Olá.

## <a name="step-3-select-your-key"></a>Passo 3: Selecione a sua chave

![Utilizam o portal encriptações de captura de ecrã com a suas próprias chave opção](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Captura de ecrã Portal, com encriptação com introduzir uri chave opção](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Se a conta de armazenamento Olá não tiver acesso toohello Cofre de chaves, pode executar o seguinte Olá comando com o Azure Powershell toogrant acesso toohello contas do storage toohello necessário Cofre de chaves.

![Captura de ecrã portal com acesso negado para o Cofre de chaves](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

Também pode conceder acesso via Olá portal do Azure ao vai toohello Cofre de chaves do Azure no portal do Azure de Olá e conceder a conta de armazenamento de toohello de acesso.

## <a name="step-4-copy-data-toostorage-account"></a>Passo 4: Copiar conta toostorage de dados
Se gostaria de tootransfer dados na sua nova conta de armazenamento, de modo a que está encriptada, consulte demasiado[passo 3 de introdução na encriptação do serviço de armazenamento para dados Inativos](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>Passo 5: Consultar o estado de Olá do Olá dados encriptados
Estado de Olá tooquery de Olá dados encriptados, consulte demasiado[passo 4 de introdução na encriptação do serviço de armazenamento para dados Inativos](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Perguntas mais frequentes sobre a encriptação do serviço de armazenamento para dados Inativos
**P: Posso estou a utilizar o Premium storage; Pode utilizar SSE com chaves cliente gerido?**

R: Sim, SSE com gerida pela Microsoft e cliente chaves geridas é suportado no armazenamento Standard e Premium storage. 

**P: Posso criar novas contas de armazenamento com SSE com chaves de cliente gerido ativadas com o Azure PowerShell e da CLI do Azure?**

R: Sim.

**P: quanto mais efetua um custo de armazenamento do Azure se chaves geridas de SSE com o cliente está ativado?**

R: não há um custo associado para utilizar o Cofre de chaves do Azure. Para obter mais detalhes visitam [preços do Cofre de chave](https://azure.microsoft.com/en-us/pricing/details/key-vault/). Não há sem custos adicionais para a utilização de SSE.

**P: revogar as chaves de encriptação do acesso toohello?**

R: Sim, pode revogar o acesso em qualquer altura. Existem várias formas toorevoke tooyour as chaves de acesso. Consulte demasiado[PowerShell do Cofre de chaves do Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) e [CLI do Azure chave de cofre](https://docs.microsoft.com/en-us/cli/azure/keyvault) para obter mais detalhes. Revogar o acesso será eficazmente blobs de blocos acesso tooall na conta do storage Olá como Olá chave de encriptação da conta não está acessível ao Storage do Azure.

**P: Posso criar uma conta de armazenamento e a chave numa região diferente?**

R: não, a conta de armazenamento de Olá e a necessidade de chave/chave de cofre toobe no Olá mesma região. 

**P: posso ativar SSE com cliente gerido chaves ao criar a conta de armazenamento Olá?**

R: um número de Quando ativar SSE ao criar a conta de armazenamento Olá, só pode utilizar as chaves Microsoft gerida. Se pretender que as chaves de cliente gerido toouse, tem de atualizar propriedades da conta de armazenamento Olá. Pode utilizar REST ou Olá armazenamento cliente bibliotecas tooprogrammatically atualizar a sua conta de armazenamento, ou atualizar propriedades da conta de armazenamento de Olá utilizando Olá portal do Azure depois de criar a conta de Olá.

**P: posso desativar a encriptação enquanto utilizar SSE com o cliente chaves geridas?**

R: não, não é possível desativar a encriptação enquanto utilizar SSE com o cliente chaves geridas. encriptação de toodisable, tem de trocar toousing gerida pela Microsoft chaves. Pode fazê-lo utilizando o Olá portal do Azure ou o PowerShell.

**P: é SSE ativada por predefinição, quando criar uma nova conta de armazenamento?**

R: SSE não está ativada por predefinição; Pode utilizar Olá tooenable portal do Azure-lo. Através de programação também pode ativar esta funcionalidade utilizando Olá API de REST do fornecedor de recursos do Storage. 

**P: Posso não é possível ativar a encriptação na minha conta de armazenamento.**

R: é uma conta de armazenamento do Resource Manager? Contas de armazenamento clássicas não são suportadas. SSE com chaves de cliente gerido também pode ser ativado apenas em contas de armazenamento recentemente criada do Gestor de recursos.

**P: É SSE com o cliente gerido chaves só é permitidas em regiões específicas?**

R: SSE está disponível apenas determinados regiões para armazenamento de BLOBs para esta pré-visualização. E-mail [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck para disponibilidade e detalhes sobre a pré-visualização. 

**P: como posso o contacto certo se posso ter algum problema ou quiser tooprovide comentários?**

R: contacto [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) para quaisquer problemas relacionados com tooStorage encriptação do serviço. 

## <a name="next-steps"></a>Passos seguintes

*   Para mais informações sobre o conjunto completo de Olá de segurança capacidades que ajudam os programadores criem aplicações seguras, consulte Olá [manual de segurança de armazenamento](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Para obter informações gerais sobre o Cofre de chaves do Azure, consulte [que é o Cofre de chaves do Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?
*   Para começar a trabalhar no Cofre de chaves do Azure, consulte [introdução ao Cofre de chaves do Azure](../../key-vault/key-vault-get-started.md).
