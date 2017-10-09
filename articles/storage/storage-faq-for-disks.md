---
title: Perguntas mais frequentes (FAQ) acerca dos discos de VM do IaaS do Azure | Microsoft Docs
description: "Perguntas mais frequentes sobre os discos de VM do IaaS do Azure e os discos premium (geridos e não gerido)"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Perguntas mais frequentes sobre os discos de VM do IaaS do Azure e os discos premium geridas e não geridas

Este artigo responde a algumas perguntas mais frequentes sobre discos gerida do Azure e o Premium Storage do Azure.

## <a name="managed-disks"></a>Managed Disks

**O que é discos gerida do Azure?**

Discos geridos é uma funcionalidade que simplifica a gestão de discos para VMs IaaS do Azure, processando gestão de contas de armazenamento para si. Para obter mais informações, consulte Olá [descrição geral de discos geridos](storage-managed-disks-overview.md).

**Se criar um disco gerido standard de um VHD existente que é 80 GB, quanto será que custo-me?**

Um disco gerido standard criado a partir de um VHD de 80 GB é tratado como o tamanho de disco padrão disponível seguinte Olá, que é um disco de S10. Está a cobrada de acordo com toohello S10 disco preços. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Existem quaisquer custos de transação para discos geridos padrão?**

Sim. Está a cobrado para cada transação. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Para um disco gerido standard, será posso cobrado para o tamanho real do Olá dos dados de Olá no disco Olá ou para a capacidade de Olá aprovisionado de disco Olá?**

Está a cobrados com base na capacidade de Olá aprovisionado de disco de Olá. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Como é preços dos discos premium gerido diferente dos discos não geridos?**

Olá preços dos discos premium gerido é Olá, mesmo que os discos premium não gerido.

**Pode alterar Olá armazenamento tipo de conta (Standard ou Premium) do meu discos geridos?**

Sim. Pode alterar o tipo de conta de armazenamento Olá dos seus discos geridos utilizando Olá portal do Azure, PowerShell ou Olá CLI do Azure.

**Existe alguma forma posso pode copiar ou exportar uma conta de armazenamento privada do disco gerido tooa?**

Sim. Pode exportar os discos geridos utilizando Olá portal do Azure, PowerShell ou Olá CLI do Azure.

**Pode utilizar um ficheiro VHD num toocreate de conta de armazenamento do Azure um disco gerido com uma subscrição diferente?**

Não.

**Pode utilizar um ficheiro VHD num toocreate de conta de armazenamento do Azure um disco gerido numa região diferente?**

Não.

**Existem algumas limitações de dimensionamento para os clientes que utilizam discos geridos?**

Discos geridos elimina os limites de Olá associados a contas de armazenamento. No entanto, o número de Olá de gerido discos por subscrição é limitado too2, 000 por predefinição. Pode chamar suporte tooincrease este número.

**Pode tirar um instantâneo incremental de um disco gerido?**

Não. capacidade de instantâneos atual Olá faz uma cópia completa de um disco gerido. No entanto, iremos estiver a planear toosupport instantâneos incrementais no Olá futura.

**VMs num conjunto de disponibilidade podem consistir de uma combinação de discos geridos e?**

Não. Olá VMs num conjunto de disponibilidade tem de utilizar discos de todos os geridos ou todos os discos não geridos. Quando criar um conjunto de disponibilidade, pode escolher o tipo de discos que pretende toouse.

**É a opção de predefinida de Olá de gerido discos no Olá portal do Azure?**

Atualmente não, mas irá tornar-se predefinição de Olá no Olá futura.

**Pode criar um disco vazio gerido?**

Sim. Pode criar um disco vazio. Um disco gerido pode ser criado independentemente de uma VM, por exemplo, sem tooa VM a ligá-la.

**O que é o número de domínios de falhas de Olá suportada para um conjunto de disponibilidade que utiliza discos geridos?**

Consoante a região de olá onde está localizado o conjunto de disponibilidade de Olá que utiliza discos geridos, o número de domínios de falhas de Olá suportado é 2 ou 3.

**Como é a conta de armazenamento standard Olá para configurar o diagnóstico?**

Configurar uma conta de armazenamento privada para diagnósticos da VM. Olá futura, vamos planear tooswitch diagnóstico tooManaged discos bem.

**Que tipo de suporte de controlo de acesso baseado em funções está disponível para discos geridos?**

Gerido funções do discos suporta três predefinido de chaves:

* O proprietário: Podem gerir tudo, incluindo o acesso
* Contribuidor: Podem gerir tudo, exceto acesso
* Leitor: Podem ver tudo, mas não é possível efetuar alterações

**Existe alguma forma posso pode copiar ou exportar uma conta de armazenamento privada do disco gerido tooa?**

Pode obter uma assinatura de acesso partilhado só de leitura URI para Olá gerido em disco e utilizá-la toocopy Olá conteúdo tooa armazenamento privada conta local ou na armazenamento.

**Pode criar uma cópia do meu disco gerido?**

Os clientes podem tirar um instantâneo os respetivos discos geridos e, em seguida, utilizar Olá instantâneo toocreate outro disco gerido.

**Os discos não geridos ainda são suportados?**

Sim. Suportamos discos não geridos e geridos. Recomendamos que utilize discos geridos para novas cargas de trabalho e migre os discos de toomanaged cargas de trabalho atual.


**Se criar um disco de 128 GB e, em seguida, aumentar Olá tamanho too130 GB, será posso cobrado Olá seguinte tamanho do disco (GB de 512)?**

Sim.

**Posso criar armazenamento localmente redundante, armazenamento georredundante, e discos geridos pelo armazenamento com redundância de zona?**

Discos gerida do Azure suporta atualmente os discos de armazenamento apenas localmente redundante gerido.

**Pode reduzir ou downsize meu discos geridos?**

Não. Esta funcionalidade não é suportada atualmente. 

**Posso alterar as propriedades de nome de computador Olá quando um especializadas (não criada utilizando a ferramenta de preparação do sistema de Olá ou generalizado) disco do sistema de operativo tooprovision utilizado uma VM?**

Não. Não é possível atualizar a propriedade de nome de computador Olá. Olá nova VM herda-Olá VM principal, que era o disco do sistema operativo utilizada toocreate Olá. 

**Onde posso encontrar exemplo do Azure Resource Manager modelos toocreate VMs com discos geridos?**
* [Lista de modelos utilizando discos geridos](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Geridos discos e a encriptação do serviço de armazenamento 

**É encriptação do serviço de armazenamento do Azure ativada por predefinição quando criar um disco gerido?**

Sim.

**Quem gere as chaves de encriptação de Olá?**

Microsoft gere as chaves de encriptação de Olá.

**Pode desativar encriptação do serviço de armazenamento para os meus discos geridos?**

Não.

**Encriptação do serviço de armazenamento só está disponível em regiões específicas?**

Não. Está disponível em todas as regiões de olá onde discos geridos está disponível. Discos geridos está disponível em todas as regiões públicas e na Alemanha.

**Como posso saber se se o meu disco gerido é encriptado?**

Pode encontrar tempo Olá quando um disco gerido foi criado a partir Olá portal do Azure, Olá CLI do Azure e PowerShell. Se houver tempo Olá após 9 de Junho de 2017, o disco está encriptado. 

**Como encriptar o meu discos existentes que foram criados antes de 10 de Junho de 2017?**

A partir de 10 de Junho de 2017, os novos dados escritos discos tooexisting gerido é encriptados automaticamente. Podemos também estiver a planear tooencrypt de dados existente e encriptação Olá acontecerá assíncrona no fundo Olá. Se tem de encriptar dados existentes agora, crie uma cópia do seu disco. Novos discos serão encriptados.

* [Copiar discos geridos utilizando Olá CLI do Azure](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [Copiar discos geridos utilizando o PowerShell](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**São gerido instantâneos e imagens encriptadas?**

Sim. Gerido todos os instantâneos e as imagens criadas após 9 de Junho de 2017, são encriptadas automaticamente. 

**Pode converter VMs com discos não geridos que estão localizados em contas de armazenamento que estão ou que foram anteriormente encriptados toomanaged discos?**

Sim

**Será um VHD exportado a partir de um disco gerido ou um instantâneo também será encriptado?**

Não. Mas se exportar uma tooan VHD encriptados conta de armazenamento de um disco gerido encriptado ou instantâneos, em seguida, são encriptado. 

## <a name="premium-disks-managed-and-unmanaged"></a>Os discos Premium: geridos e não geridas

**Se uma VM utiliza uma série de tamanho que suporte o Premium Storage, tais como uma série DSv2, posso anexar os discos de dados standard e premium?** 

Sim.

**Posso anexar premium e série tamanho de tooa de discos de dados padrão que não suporta o Premium Storage, tais como a série de D, Dv2, G ou F?**

Não. Pode anexar apenas padrão a dados discos tooVMs que não utilizem uma série de tamanho que suporte o Premium Storage.

**Se criar um disco de dados premium a partir de um VHD existente que estava 80 GB, quanto será que custo?**

Um disco de dados premium criado a partir de um VHD de 80 GB é tratado como Olá disponível a seguinte tamanho do disco premium, que é um disco de P10. Está a cobrada de acordo com toohello P10 disco preços.

**Existem custos de transação toouse Premium Storage?**

Não há um custo fixo para cada tamanho de disco, o que é aprovisionado com limites específicos no IOPS e débito. Olá outros custos são largura de banda de saída e a capacidade de instantâneos, se aplicável. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).

**Quais são Olá os limites de IOPS e débito que pode receber de cache em disco Olá?**

Olá combinados limites para a cache e SSD local para uma série DS são 4000 IOPS por núcleos e 33 MB por segundo por núcleo. Olá série GS oferece 5000 IOPS por núcleos e 50 MB por segundo por núcleo.

**É Olá que local SSD suportado para uma VM de discos geridos?**

Olá local SSD é armazenamento temporário que está incluído com uma VM de discos geridos. Existe um custo extra para este armazenamento temporário. Recomendamos que não utilize este toostore SSD local os dados da aplicação porque este não é continuada no Blob storage do Azure.

**São não existe qualquer repercussions para Olá a utilização de operações de COMPACTAÇÃO em discos premium?**

Não há nenhuma utilização toohello downside cortar nos discos do Azure premium o ou os discos padrão.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Novos tamanhos de disco: geridos e não geridas

**O que é Olá maior tamanho do disco suportado para o sistema operativo e os discos de dados?**

tipo de partição de Olá que suporta o Azure para um disco de sistema operativo é registo Olá de arranque principal (MBR). formato MBR Olá suporta um tamanho de disco segurança too2 TB. Olá a maior dimensão possível que suporta o Azure para um disco de sistema operativo é 2 TB. Azure suporta até too4 TB para discos de dados. 

**O que é Olá maior blob tamanho de página que é suportado?**

Olá maior página tamanho do blob que suporte do Azure é de 8 TB (8,191 GB). Não é suportada com mais de 4 TB (4,095 GB) ligado tooa VM como discos de sistema operativo ou de dados de blobs de páginas.

**É necessário toouse uma nova versão das ferramentas do Azure toocreate, anexar, redimensionar e carregar discos superiores a 1 TB?**

Não precisa de tooupgrade sua toocreate de ferramentas do Azure existente, anexar ou redimensionar discos superiores a 1 TB. tooupload o VHD de ficheiros no local diretamente tooAzure como um blob de página ou disco não gerido, tem de conjuntos de ferramenta mais recentes do toouse Olá:

|Ferramentas do Azure      | Versões suportadas                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Número de versão 4.1.0: versão de Junho de 2017 ou posterior|
|CLI do Azure v1     | Número de versão 0.10.13: versão de Maio de 2017 ou posterior|
|AzCopy           | Número de versão 6.1.0: versão de Junho de 2017 ou posterior|

suporte de Olá para v2 CLI do Azure e o Explorador de armazenamento do Azure está disponível em breve. 

**P4 e P6 tamanhos de disco são suportados para os discos não geridos ou blobs de página?**

Não. P4 (32 GB) e P6 tamanhos de disco (64 GB) são suportados apenas para discos geridos. Suporte para discos não geridos e blobs de páginas está disponível em breve.

**Se a minha premium existente gerido disco inferior a 64 GB foi criado antes de disco pequeno Olá foi ativado (em torno do dia 15 de Junho de 2017), como é é faturada?**

Discos premium pequeno existentes inferior a 64 GB continuar toobe cobrado de acordo com toohello P10 escalão de preço. 

**Como posso mudar a camada de disco de Olá dos discos premium pequeno inferior a 64 GB de P10 tooP4 ou P6?**

Pode tirar um instantâneo os discos pequenos e, em seguida, criar um Olá de comutador do disco tooautomatically tooP4 do escalão de preço ou P6 com base no tamanho de Olá aprovisionado. 


## <a name="what-if-my-question-isnt-answered-here"></a>E se a minha pergunta não é atendida aqui?

Se a sua pergunta não está listada aqui, informe-nos e vamos ajudá-lo a encontrar uma resposta. Pode colocar uma pergunta no final deste artigo Olá nos comentários de Olá. tooengage com a equipa de armazenamento do Azure Olá e outros membros da Comunidade sobre neste artigo, utilize Olá MSDN [fórum de armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

funcionalidades de toorequest, submeter o pedidos e ideias toohello [fórum de comentários do Storage do Azure](https://feedback.azure.com/forums/217298-storage).
