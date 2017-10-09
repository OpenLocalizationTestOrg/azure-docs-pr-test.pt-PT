---
title: "aaaUnderstand partilhado endereços IP no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como Azure DevTest Labs utiliza partilhado IP endereços toominimize Olá pública IP endereços necessários tooaccess o laboratório VMs."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Compreender os endereços IP partilhados no Azure DevTest Labs

Laboratório de permite do Azure DevTest Labs VMs partilha Olá mesma pública IP endereço toominimize Olá diversas pública tooaccess necessária de endereços IP individuais laboratório VMs.  Este artigo descreve como partilhado de IPs de trabalho e as opções de configuração relacionados.

## <a name="shared-ip-setting"></a>Partilhado a definição de IP

Quando criar um laboratório, reside numa sub-rede de uma rede virtual.  Por predefinição, esta sub-rede é criada com **ativar partilhado IP público** definido demasiado*Sim*.  Esta configuração cria um endereço IP público para a sub-rede Olá de todo.  Para obter mais informações sobre como configurar redes virtuais e sub-redes, consulte [configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nova sub-rede de laboratório](media/devtest-lab-shared-ip/lab-subnet.png)

Para laboratórios existentes, pode ativar esta opção, selecionando **políticas de configuração e > redes virtuais**. Em seguida, selecione uma rede virtual da lista de Olá e escolha **ATIVAR PARTILHADO IP público** para uma sub-rede selecionada. Também pode desativar esta opção em qualquer laboratório se não quiser tooshare um endereço IP público em laboratório VMs.

Quaisquer VMs criadas no toousing de predefinição laboratório um IP partilhado.  Ao criar Olá VM, esta definição pode ser observada em Olá **definições avançadas** painel em **configuração do endereço IP**.

![Nova VM](media/devtest-lab-shared-ip/new-vm.png)

- **Partilhado:** todas as VMs criadas como **partilhados** são colocados de um grupo de recursos (RG). Um único endereço IP é atribuído para que o RG e todas as VMs no Olá RG irão utilizar esse endereço IP.
- **Público:** cada VM que cria tem o seu próprio endereço IP e é criado no seu próprio grupo de recursos.
- **Privados:** cada VM que criar utiliza um endereço IP privado. Não será capaz de tooconnect toothis VM diretamente a partir de Olá internet com o ambiente de trabalho remoto.

Sempre que uma VM com o IP partilhado ativada é adicionada toohello sub-rede, DevTest Labs adiciona o Balanceador de carga do Olá VM tooa automaticamente e atribui um número de porta TCP no endereço IP público Olá, reencaminhamento toohello porta RDP num Olá VM.  

## <a name="using-hello-shared-ip"></a>Utilizar Olá partilhado de IP

- **Os utilizadores do Linux:** SSH toohello VM utilizando o endereço IP Olá ou o nome de domínio completamente qualificado, seguido por um vírgula, seguido de porta de Olá. Por exemplo, numa imagem de Olá abaixo, Olá RDP endereços toohello tooconnect VM é `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Exemplo VM](media/devtest-lab-shared-ip/vm-info.png)

- **Utilizadores do Windows:** Olá selecione **Connect** botão no Olá toodownload portal do Azure, um ficheiro RDP previamente configurado e aceder Olá VM.

## <a name="next-steps"></a>Passos seguintes

* [Definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configurar uma rede virtual no Azure DevTest Labs](devtest-lab-configure-vnet.md)





