---
title: "aaaAzure FAQ de encriptação de disco | Microsoft Docs"
description: "Este artigo fornece respostas toofrequently mais frequentes sobre o Microsoft Azure disco encriptação para o Windows e as VMs de IaaS Linux."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 17f084628ba4ef22e9d37dd3052ef10f8eb2cd7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Encriptação de disco do Azure perguntas mais frequentes (FAQ)

Estas perguntas mais frequentes respondem a dúvidas sobre a encriptação de disco do Azure para o Windows e as VMs de IaaS Linux, para obter mais informações sobre este serviço, leia [encriptação de disco do Azure para Windows e as VMs de IaaS Linux](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Perguntas gerais
**P.** Cada região é a encriptação de disco do Azure em GA?

**R:** encriptação de disco do Azure para o Windows e as VMs de IaaS Linux está disponível no GA em todas as regiões públicas do Azure.

**P:** ocorre com o qual o utilizador que estão disponíveis com a Azure Disk Encryption?

**R:** GA de encriptação de disco do Azure suporta modelos Azure Resource Manager, do PowerShell do Azure, CLI do Azure. Isto dá-lhe muita flexibilidade em que tem três opções diferentes para ativar a encriptação de disco para as suas VMs de IaaS. Obter mais detalhes sobre a experiência de utilizador Olá e orientação passo a passo está disponível em cenários de implementação do Azure Disk Encryption Olá e experiências.

**P:** quanto does Azure Disk Encryption custo?

**R:** há sem qualquer encargo para encriptar os discos da VM com o Azure Disk Encryption.

**P:** as camadas de máquina virtual posso utilizar o Azure Disk Encryption com?

**R:** Azure Disk Encryption só está disponível no padrão de camada de VMs, incluindo [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) e assim sucessivamente VMs de IaaS de série, incluindo VMs com o armazenamento premium. Não está disponível em VMs de escalão básicas.

**P:** as distribuições do Linux que são suportadas pelo Azure Disk Encryption?

**R:** Azure Disk Encryption é suportada em Olá seguir as distribuições de servidor Linux e versões:

| Distribuição de Linux | Versão | Tipo de volume suportado para a encriptação|
| --- | --- |--- |
| Ubuntu | 16.04-DIARIAMENTE-LTS | Disco do SO e dados |
| Ubuntu | 14.04.5-DAILY-LTS | Disco do SO e dados |
| RHEL | 7.3 | Disco do SO e dados |
| RHEL | 7.2 | Disco do SO e dados |
| RHEL | 6.8 | Disco do SO e dados |
| RHEL | 6.7 | Disco de dados |
| CentOS | 7.3 | Disco do SO e dados |
| CentOS | 7.2N | Disco do SO e dados |
| CentOS | 6.8 | Disco do SO e dados |
| CentOS | 7.1 | Disco de dados |
| CentOS | 7.0 | Disco de dados |
| CentOS | 6.7 | Disco de dados |
| CentOS | 6.6 | Disco de dados |
| CentOS | 6.5 | Disco de dados |
| openSUSE | 13.2 | Disco de dados |
| SLES | 12 SP1 | Disco de dados |
| SLES | Prioridade: 12-SP1 | Disco de dados |
| SLES | HPC 12 | Disco de dados |
| SLES | Prioridade: 11-SP4 | Disco de dados |
| SLES | 11 SP4 | Disco de dados |

**P:** como pode começar a utilizar com o Azure Disk Encryption?

**R:** clientes podem saber como tooget iniciado por leitura Olá documento técnico da Azure Disk Encryption localizado [aqui](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**P:** pode encriptar volumes de arranque e dados com o Azure Disk Encryption?

**R:** Sim, pode encriptar volumes de arranque e de dados para o Windows e as VMs de IaaS Linux. Para VMs do Windows, não é possível encriptar dados Olá sem primeiro encrpting Olá volume do SO. Para VMs com Linux, pode encriptar o volume de dados de Olá sem encryptinng Olá volume do SO primeiro. Assim que encriptou volume Olá SO para Liux, a desativação da encriptação num volume SO para as VMs de IaaS Linux não é suportada

**P:** Does Azure Disk Encryption ativar um "traga a sua própria chave" capacidade (BYOK)?

**R:** Sim, pode fornecer as suas próprias chaves de encriptação de chaves. Essas chaves são salvaguardadas no Cofre de chaves do Azure, que é o armazenamento de chaves Olá para Azure Disk Encryption. Para obter mais detalhes sobre a chave de encriptação de chaves Olá suporta cenários, consulte experiências e cenários de implementação do Azure Disk Encryption Olá

**P:** posso utilizar uma chave de encriptação de chaves do Azure-criar?

**R:** Sim, pode utilizar a chave de encriptação de chaves do Azure chave cofre toogenerate para utilização de encriptação de disco do Azure. Essas chaves são salvaguardadas no Cofre de chaves do Azure, que é o armazenamento de chaves Olá para Azure Disk Encryption. Para obter mais detalhes sobre a chave de encriptação de chaves Olá suporta cenários, consulte experiências e cenários de implementação do Azure Disk Encryption Olá

**P:** posso utilizar chaves de encriptação de Olá de serviço/HSM toosafeguard gestão de chaves no local?

**R:** não é possível utilizar chaves de encriptação de Olá gestão de chaves HSM/serviço toosafeguard Olá no local com a encriptação de disco do Azure. Só pode utilizar chaves de encriptação de Olá serviço toosafeguard Olá Cofre de chaves do Azure. Para obter mais detalhes sobre a chave de encriptação de chaves Olá suporta cenários, consulte experiências e cenários de implementação do Azure Disk Encryption Olá

**P:** quais são encriptação de disco do Azure de tooconfigure de pré-requisitos de Olá?

**R:** Olá disco Azure encriptação pré-requisitos PowerShell toocreate AAD aplicação de scripts, crie o novo cofre de chaves ou Cofre de chaves para disco encriptação acesso tooenable encriptação e salvaguarda segredos e a chave de configuração.  Para obter mais detalhes sobre a chave de encriptação de chaves de Olá suporta cenários, consulte os pré-requisitos do Azure Disk Encryption de Olá e experiências e cenários de implementação

**P:** onde pode obter mais informações sobre como toouse do PowerShell para configurar a Azure Disk Encryption?

**R:** temos algumas excelente artigos sobre a forma como pode efetuar tarefas básicas do Azure Disk Encryption, bem como em cenários mais avançados. Para as tarefas básico Olá, veja a explorar [Azure Disk Encryption com o Azure PowerShell - parte 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Para cenários mais avançados, consulte explorar [Azure Disk Encryption com o Azure PowerShell – parte 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**P:** que versão do PowerShell do Azure é suportado pelo Azure Disk Encryption?

**R:** versão mais recente do Olá de utilização do SDK do Azure PowerShell versão tooconfigure Azure Disk Encryption. Transferir a versão mais recente do Olá do [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Encriptação de disco do Azure não é suportada pelo Azure SDK versão 1.1.0.

> [!NOTE]
> Olá extensão de pré-visualização do Azure de Linux disco encriptação foi preterido. Para obter detalhes, consulte toodocumentation [aqui](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**P:** pode aplicar encriptação de disco do Azure no meu imagem personalizada do Linux?

**R:** não é possível aplicar encriptação de disco do Azure na sua imagem personalizada do Linux. Suportamos apenas imagens de Linux de galeria Olá para distros Olá suportado descritas acima. Não é suportada atualmente imagens personalizadas do Linux

**P:** posso aplicar atualizações tooa Linux Red Hat VM com a atualização Yum?

**R:** Sim, pode efetuar a atualização e ou correção uma VM do Red Hat Linnux seguir as orientações documentadas [aqui](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**P:** onde pode posso aceder tooask pergunta ou enviar comentários

**R:** pode fornecer colocar questões ou comentários no fórum de encriptação de disco do Azure Olá [aqui](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Consultar também
Neste documento, aprendeu mais sobre Olá mais frequente perguntas relacionadas tooAzure encriptação de disco, para obter mais informações sobre este serviço e a capacidade de leitura:

- [Aplicar a encriptação de disco no Centro de segurança do Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Encriptar uma Máquina Virtual do Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Dados do Azure encriptação em Rest](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
