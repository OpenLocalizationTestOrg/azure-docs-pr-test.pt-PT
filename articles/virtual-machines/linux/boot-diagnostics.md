---
title: "diagnóstico de aaaBoot para computadores virtuais Linux no Azure | Documentação da Microsoft"
description: "Descrição geral das funcionalidades depuração dois Olá para computadores virtuais Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a><span data-ttu-id="21c4a-103">Como toouse arranque diagnóstico tootroubleshoot máquinas de virtuais Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="21c4a-103">How toouse boot diagnostics tootroubleshoot Linux virtual machines in Azure</span></span>

<span data-ttu-id="21c4a-104">Está agora disponível o suporte de duas funcionalidades de depuração no Azure: Saída da Consola e Captura de Ecrã para o modelo de implementação das Máquinas Virtuais do Azure (Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="21c4a-104">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="21c4a-105">Quando o seus próprios tooAzure de imagem ou mesmo arrancar uma das imagens da plataforma de Olá, pode ser muitos motivos por que motivo uma Máquina Virtual obtém num Estado não arranque.</span><span class="sxs-lookup"><span data-stu-id="21c4a-105">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="21c4a-106">Ativar estas funcionalidades tooeasily diagnosticar e recuperar máquinas virtuais de falhas de arranque.</span><span class="sxs-lookup"><span data-stu-id="21c4a-106">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="21c4a-107">Para máquinas de virtuais do Linux, pode visualizar facilmente resultado Olá o início de sessão de consola do Olá Portal:</span><span class="sxs-lookup"><span data-stu-id="21c4a-107">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Portal do Azure](./media/boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="21c4a-109">No entanto, para o Windows e máquinas virtuais do Linux, Azure também permite toosee uma captura de ecrã de Olá VM de hipervisor Olá:</span><span class="sxs-lookup"><span data-stu-id="21c4a-109">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![Erro](./media/boot-diagnostics/screenshot2.png)

<span data-ttu-id="21c4a-111">Estas duas funcionalidades são suportadas para Máquinas Virtuais do Azure em todas as regiões.</span><span class="sxs-lookup"><span data-stu-id="21c4a-111">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="21c4a-112">Tenha em atenção, capturas de ecrã e de saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="21c4a-112">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="21c4a-113">Erros de arranque comuns</span><span class="sxs-lookup"><span data-stu-id="21c4a-113">Common boot errors</span></span>

- [<span data-ttu-id="21c4a-114">Problemas de sistema de ficheiros</span><span class="sxs-lookup"><span data-stu-id="21c4a-114">File system issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [<span data-ttu-id="21c4a-115">Problemas de kernel</span><span class="sxs-lookup"><span data-stu-id="21c4a-115">Kernel Issues</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [<span data-ttu-id="21c4a-116">Erros FSTAB</span><span class="sxs-lookup"><span data-stu-id="21c4a-116">FSTAB errors</span></span>](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="21c4a-117">Ativar o diagnóstico numa máquina virtual nova</span><span class="sxs-lookup"><span data-stu-id="21c4a-117">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="21c4a-118">Quando criar uma nova máquina Virtual do Portal de pré-visualização de Olá, selecione Olá **do Azure Resource Manager** da lista pendente de modelo de implementação Olá:</span><span class="sxs-lookup"><span data-stu-id="21c4a-118">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="21c4a-120">Configure Olá monitorização opção tooselect Olá conta do storage onde pretende que tooplace estes ficheiros de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="21c4a-120">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![Criar VM](./media/boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="21c4a-122">Se estiver a implementar a partir de um modelo Azure Resource Manager, navegue até tooyour recurso de Máquina Virtual e de acréscimo secção de perfil de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="21c4a-122">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="21c4a-123">Lembre-se o cabeçalho de versão de API do toouse Olá "2015-06-15".</span><span class="sxs-lookup"><span data-stu-id="21c4a-123">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="21c4a-124">perfil de diagnóstico de Olá permite-lhe conta do storage tooselect olá onde pretende tooput estes registos.</span><span class="sxs-lookup"><span data-stu-id="21c4a-124">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="21c4a-125">Atualizar uma máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="21c4a-125">Update an existing virtual machine</span></span>

<span data-ttu-id="21c4a-126">diagnóstico de arranque tooenable através do portal Olá, também pode atualizar uma máquina virtual existente através do portal Olá.</span><span class="sxs-lookup"><span data-stu-id="21c4a-126">tooenable boot diagnostics through hello portal, you can also update an existing virtual machine through hello portal.</span></span> <span data-ttu-id="21c4a-127">Selecione Olá opção de diagnóstico de arranque e de guardar.</span><span class="sxs-lookup"><span data-stu-id="21c4a-127">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="21c4a-128">Reinicie o efeito de tootake Olá VM.</span><span class="sxs-lookup"><span data-stu-id="21c4a-128">Restart hello VM tootake effect.</span></span>

![Atualizar VM Existente](./media/boot-diagnostics/screenshot5.png)