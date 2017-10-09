---
title: infraestrutura aaaAzure nomenclatura diretrizes - Windows | Microsoft Docs
description: "Saiba mais sobre Olá chaves design e implementação diretrizes de nomenclatura nos serviços de infraestrutura do Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a>Infraestrutura do Azure diretrizes de nomenclatura para VMs do Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Este artigo foca-se em compreender como as convenções de nomenclatura tooapproach para todos os seus toobuild de recursos do Azure vários a lógica e facilmente identificável conjunto de recursos em todo o ambiente.

## <a name="implementation-guidelines-for-naming-conventions"></a>Diretrizes de implementação para as convenções de nomenclatura
Decisões:

* Quais são as convenções de nomenclatura para recursos do Azure?

Tarefas:

* Defina Olá affixes toouse entre a consistência de toomaintain de recursos.
* Defina a conta de armazenamento nomes fornecidos Olá requisito para os mesmos toobe globalmente exclusivo.
* Olá documento toobe Convenção de nomenclatura utilizado e distribuir tooall entidades envolvidas tooensure consistência entre implementações.

## <a name="naming-conventions"></a>Convenções de nomenclatura
Deve ter uma convenção de nomenclatura boa no local antes de criar nada no Azure. Uma convenção de nomenclatura garante que todos os recursos de Olá têm um nome previsível, que ajuda-o fardo administrativo inferior do Olá, associado à gestão esses recursos.

Poderá escolher toofollow um conjunto específico de convenções de nomenclatura definidos para toda a organização ou para uma subscrição do Azure específica ou a conta. Embora seja mais fácil para os indivíduos dentro das regras implícita de organizações tooestablish ao trabalhar com recursos do Azure, quando precisa de uma equipa toowork num projeto no Azure, esse modelo não dimensiona bem.

Aceita num conjunto de convenções de nomenclatura adiantado. Existem algumas considerações sobre as convenções de nomenclatura que cortar entre este conjunto de regras.

## <a name="affixes"></a>Affixes
Como ver toodefine uma convenção de nomenclatura, uma decisão vem se affix Olá é:

* início de Olá do nome de Olá (prefixo)
* fim de Olá do nome de Olá (sufixo)

Por exemplo, seguem-se dois nomes possíveis para um grupo de recursos com Olá `rg` affix:

* RG-WebApp (prefixo)
* WebApp-Rg (sufixo)

Affixes podem referir-se toodifferent aspetos que descrevem a recursos específicos Olá. Olá tabela seguinte mostra alguns exemplos normalmente utilizados.

| Aspeto | Exemplos | Notas |
|:--- |:--- |:--- |
| Ambiente |Dev, stg, prod |Consoante o objetivo de Olá e o nome de cada ambiente. |
| Localização |usw (EUA oeste), utilize (EUA Leste 2) |Consoante a região de Olá Olá datacenter ou a região de Olá da organização Olá do. |
| Componente do Azure, serviço ou produto |RG para o grupo de recursos, VNet para a rede virtual |Consoante o produto de Olá para que Olá recurso fornece suporte. |
| Função |SQL Server, ora, sp, iis |Dependendo da função de Olá da máquina virtual de Olá. |
| Instância |01, 02, 03, etc. |Para os recursos que tem mais do que uma instância. Por exemplo, com balanceamento de carga servidores web num serviço em nuvem. |

Ao estabelecer as convenções de nomenclatura, certifique-se de que estes claramente que affixes toouse para cada tipo de recurso e, na qual posição (sufixo de vs prefixo).

## <a name="dates"></a>datas
É, frequentemente, data de Olá toodetermine importante da criação do nome de Olá de um recurso. Recomendamos que o formato de data do Olá AAAAMMDD. Este formato garante que não só data completa Olá é registada, mas também que dois recursos cujos nomes só diferem data Olá é ordenada alfabeticamente e chronologically em Olá mesmo tempo.

## <a name="naming-resources"></a>Recursos de atribuição de nomes
Defina cada tipo de recurso na Convenção de nomenclatura Olá, que deve ter regras que definem como tooassign os nomes de recursos de tooeach que é criado. Estas regras devem ser aplicada tooall tipos de recursos, por exemplo:

* Subscrições
* Contas
* Contas de armazenamento
* Redes virtuais
* Sub-redes
* Conjuntos de disponibilidade
* Grupos de recursos
* Máquinas virtuais
* Pontos Finais
* Grupos de segurança de rede
* Funções

tooensure Olá nome fornece suficiente recursos toowhich do toodetermine de informações refere-se, deverá utilizar nomes descritivos.

## <a name="computer-names"></a>Nomes de computador
Quando cria uma máquina virtual (VM), o Microsoft Azure requer um nome de VM de cópia de segurança too15 carateres que é utilizado Olá no nome de recurso. Azure utiliza Olá o mesmo nome para o sistema de operativo Olá instalado no Olá VM. No entanto, estes nomes poderá não sempre ser Olá mesmo.

No caso de uma VM é criada a partir de um ficheiro de imagem VHD que já contém um sistema operativo, nome da VM Olá no Azure pode ser diferente do Olá nome de computador do sistema operativo da VM. Esta situação pode adicionar um grau de gestão de tooVM dificuldade em, que, por conseguinte, não é recomendada. Atribua Olá Olá de recurso de VM do Azure mesmo nome como nome do computador Olá que atribuir o sistema operativo toohello essa VM.

Recomendamos que esse nome de VM do Azure Olá é Olá igual Olá subjacente nome de computador do sistema operativo.

## <a name="storage-account-names"></a>Nomes das contas de armazenamento
Esta secção não se aplica demasiado[Azure geridos discos](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), uma vez que não crie uma conta de armazenamento separada. Para discos não geridos, as contas de armazenamento têm regras especiais que rege os respetivos nomes. Pode utilizar apenas letras minúsculas e números. Para obter mais informações, consulte [criar uma conta de armazenamento](../../storage/storage-create-storage-account.md#create-a-storage-account). Além disso, o nome de conta do storage Olá, juntamente com core.windows.net, deve ser um nome DNS globalmente válido e exclusivo. Por exemplo, se a conta de armazenamento Olá for chamada mystorageaccount, hello seguintes nomes de DNS resultantes devem ser exclusivos:

* mystorageaccount.blob.Core.Windows.NET
* mystorageaccount.TABLE.Core.Windows.NET
* mystorageaccount.Queue.Core.Windows.NET

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

