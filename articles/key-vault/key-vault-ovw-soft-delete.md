---
ms.assetid: 
title: "eliminação de forma recuperável do Cofre de chaves de aaaAzure | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Descrição geral da eliminação de forma recuperável Cofre de chaves do Azure

A funcionalidade de eliminação de forma recuperável do Cofre de chave permite a recuperação de cofres de Olá eliminado e objetos do cofre, conhecidos como eliminar de forma recuperável. Especificamente, vamos abordar Olá os seguintes cenários:

- Suporte para eliminação recuperável de um cofre de chaves
- Suporte para eliminação recuperável de objetos do Cofre de chaves (ex. as chaves, segredos, certificados)

## <a name="supporting-interfaces"></a>Interfaces de suporte

Olá funcionalidade de eliminação de forma recuperável está inicialmente disponível através do Olá REST, .NET / interfaces de c# e PowerShell. Consulte toohello referências para obter mais detalhes, [referência do Cofre de chave](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Cenários

Cofres de chaves do Azure são recursos controlados, geridos pelo Gestor de recursos do Azure. O Azure Resource Manager também especifica um comportamento definido especificamente para eliminação, o que necessita que uma operação de eliminação com êxito têm de resultar nesse recurso não estão a ser acessível já. endereços de funcionalidade de eliminação de forma recuperável Olá Olá recuperação de objeto de Olá eliminado, se a eliminação de Olá foi acidental ou intencional.

1. Cenário de típico Olá, um utilizador pode ter inadvertidamente eliminado um cofre de chaves ou um objeto do Cofre de chaves; Se esse cofre de chaves ou chave de cofre objeto foram toobe recuperável durante um período predeterminado, utilizador de Olá pode anular eliminação Olá e recuperar os seus dados.

2. Num cenário de diferentes, um utilizador não autorizado pode tentar toodelete um cofre de chaves ou um objeto de Cofre de chaves, tal como uma chave no interior de um cofre, toocause uma interrupção de negócios. Separação de eliminação de Olá do Cofre de chaves Olá ou o objeto do Cofre de chaves contra eliminação real de Olá de Olá subjacente dados pode ser utilizada como uma medida de segurança ao, por exemplo, restringir permissões num tooa de eliminação de dados diferente, fidedigna função. Esta abordagem requer efetivamente quórum para uma operação que caso contrário, poderá resultar em perda de dados de imediato.

### <a name="soft-delete-behavior"></a>Comportamento de eliminação de forma recuperável

Com esta funcionalidade, Olá operação eliminar um cofre de chaves ou o objeto do Cofre de chaves é soft eliminar eficazmente que está a reter recursos Olá durante um período de retenção especificado, enquanto a dar aspeto Olá esse objeto Olá é eliminada. serviço de Olá mais fornece um mecanismo para recuperar o objeto de Olá eliminado, essencialmente undoing eliminação Olá. 

Eliminar de forma recuperável é um comportamento opcional do Cofre de chaves e é **não ativada por predefinição** nesta versão. Para obter detalhes sobre como ativar a eliminação de forma recuperável para o seu Cofre de chaves, consulte orientações específicas do Olá numa referência de Olá para a interface de Olá à sua escolha, [referência do Cofre de chave](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Recuperação do Cofre de chaves

Após eliminar um cofre de chaves, o serviço de Olá cria um recurso de proxy na subscrição Olá, adicionar metadados suficientes para recuperação. recurso de proxy de Olá é um objeto armazenado, disponível no Olá mesma localização do Cofre de chaves Olá eliminado. 

### <a name="key-vault-object-recovery"></a>Recuperação de objeto do Cofre de chaves

Após eliminar um objeto de Cofre de chaves, tal como uma chave de serviço Olá colocará objeto Olá num Estado eliminado, deste modo, tornando-operações de obtenção de tooany inacessível. Enquanto estiver neste estado, objeto do Cofre de chaves de Olá pode apenas ser apresentado, recuperado ou forçadamente/permanentemente eliminado. 

Em Olá mesmo Cofre de chave, tempo irá agendar a eliminação de Olá de Olá subjacente toohello correspondente de dados eliminada Cofre de chaves ou objeto de Cofre de chaves para execução após um intervalo de retenção predeterminada. Olá DNS registo toohello cofre correspondente também é mantida durante Olá do intervalo de retenção de Olá.

### <a name="soft-delete-retention-period"></a>Período de retenção de eliminação de forma recuperável

Recursos eliminados de forma recuperável são retidos durante um período de tempo, 90 dias definido. Durante o intervalo de retenção de eliminação de forma recuperável Olá, Olá aplicar os seguintes:

- Pode listar todos os cofres de chaves Olá e objetos do Cofre de chaves num Estado de eliminação de forma recuperável Olá para a sua subscrição, bem como informações de recuperação e eliminação de acesso sobre os mesmos.
    - Apenas os utilizadores com permissões especiais podem listar os cofres eliminados. Recomendamos que os nossos utilizadores criar uma função personalizada com estas permissões especiais para processamento eliminado cofres.
- Um cofre de chaves com Olá não é possível criar o mesmo nome no Olá mesma localização; proporcionalmente, um objeto do Cofre de chaves não é possível criar um cofre fornecido se esse cofre de chaves contém um objeto com Olá mesmo nome e a que se encontra no Estado eliminado 
- Apenas um utilizador especificamente com privilégios poderá restaurar um cofre de chaves ou o objeto de Cofre de chaves ao emitir um comando de recuperar no recurso de proxy Olá correspondente.
    - utilizador Olá, membro de função personalizada Olá, que tem o privilégio de Olá toocreate um cofre de chaves de grupo de recursos de Olá pode restaurar cofre Olá.
- Apenas um utilizador especificamente com privilégios a forçar a pode eliminar um cofre de chaves ou o objeto de Cofre de chaves ao emitir um comando de eliminação no recurso de proxy Olá correspondente.

A menos que um cofre de chaves ou o objeto de Cofre de chaves é recuperado, em Olá final do serviço de Olá de intervalo de retenção de Olá efetua uma remoção do Cofre de chaves Olá eliminados de forma recuperável ou o objeto do Cofre de chaves e o respetivo conteúdo. Eliminação de recurso não pode ser reagendada.

### <a name="permitted-purge"></a>Remoção permitida

Permanentemente a eliminar, remover, um cofre de chaves é possível através de uma operação POST no recurso de proxy de Olá e necessita de privilégios especiais. Geralmente, apenas o proprietário de subscrição Olá será capaz de toopurge um cofre de chaves. acionadores de operação de POST Olá Olá eliminação imediata e irrecuperável de que o cofre. 

Uma exceção toothis for o caso de Olá quando Olá subscrição do Azure tiver sido marcada como *undeletable*. Neste caso, apenas os serviço Olá, em seguida, podem efetuar a eliminação real Olá e é feito como um processo agendado. 



