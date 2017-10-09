---
title: "aaaHow tooconfigure um serviço em nuvem (portal) | Microsoft Docs"
description: "Saiba como tooconfigure cloud services no Azure. Obter a configuração do serviço de nuvem do tooupdate Olá e configurar as instâncias de toorole de acesso remoto. Estes exemplos utilizam Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Como tooConfigure Cloud Services
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-configure-portal.md)
> * [Portal Clássico do Azure](cloud-services-how-to-configure.md)
>
>

Pode configurar as definições de Olá normalmente utilizada para um serviço em nuvem no Olá portal do Azure. Ou, se pretender tooupdate diretamente, os ficheiros de configuração transfira um tooupdate de ficheiro de configuração de serviço e, em seguida, carregue Olá atualizado de ficheiros e atualização Olá serviço em nuvem com alterações de configuração de Olá. Qualquer forma, as atualizações de configuração de Olá são instalados sem solicitação tooall instâncias de função.

Também pode gerir instâncias Olá das suas funções de serviço na nuvem ou ambiente de trabalho remoto em-los.

Azure pode apenas Certifique-se de disponibilidade do serviço de percentagem de 99,95 durante Olá atualizações de configuração se tiver, pelo menos, duas instâncias de função para cada função. Que permite que uma máquina virtual tooprocess os pedidos de cliente enquanto Olá outro está a ser atualizado. Para obter mais informações, consulte [contratos de nível de serviço](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Alterar um serviço em nuvem
Após a abertura Olá [portal do Azure](https://portal.azure.com/), navegue até tooyour o serviço em nuvem. Aqui, gerir vários aspetos do mesmo.

![Página de definições](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Olá **definições** ou **todas as definições** irão abrir ligações Olá **definições** painel onde pode alterar Olá **propriedades**, alterar Olá **Configuração**, gerir Olá **certificados**, configuração **regras de alerta**e gerir Olá **utilizadores** quem tem acesso o serviço em nuvem toothis.

![Painel de definições de serviço em nuvem do Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Gerir a versão de SO convidado

Por predefinição, o Azure atualiza periodicamente a convidado toohello mais recente suportada imagem do SO no Olá família de SO especificadas na sua configuração de serviço (. cscfg), como o Windows Server 2016.

Se precisar de tootarget uma versão de SO específica, pode defini-lo no Olá **configuração** painel.

![Definir a versão de SO](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Escolher que uma versão de SO específica desativa SO automático de atualizações e faz a responsabilidade de aplicação de patches. Tem de garantir que as instâncias da função estão a receber atualizações ou pode expor as vulnerabilidades de toosecurity de aplicação.

## <a name="monitoring"></a>Monitorização
Pode adicionar o serviço de nuvem tooyour de alertas. Clique em **definições** > **regras de alerta** > **Adicionar alerta**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Aqui, pode configurar um alerta. Com Olá **métrica** pendente caixa, pode configurar um alerta para Olá tipos de dados seguintes.

* Lidos de disco
* Escrita de disco
* Rede no
* Limite de rede
* Percentagem de CPU

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Configurar a monitorização a partir de um mosaico métrico
Em vez de utilizar **definições** > **regras de alerta**, pode clicar dos mosaicos de métrica de Olá no Olá **monitorização** secção Olá **na nuvem serviço** painel.

![Monitorização do serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

Aqui pode personalizar o gráfico de Olá utilizado com o mosaico Olá ou adicionar uma regra de alerta.

## <a name="reboot-reimage-or-remote-desktop"></a>Reiniciar o computador, a recriação de imagem ou o ambiente de trabalho remoto
Neste momento, não é possível configurar o ambiente de trabalho remoto utilizando Olá **portal do Azure**. No entanto, pode configurá-lo através de Olá [portal clássico do Azure](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), ou através de [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Em primeiro lugar, clique na instância do serviço de nuvem de Olá.

![Instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance.png)

De Olá painel que abre-se de pode iniciar uma ligação de ambiente de trabalho remota, reiniciar remotamente Olá instâncias, ou remotamente recriação de imagem (começar com uma nova imagem) Olá.

![Botões de instância de serviço de nuvem](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Reconfigure o. cscfg
Poderá ser necessário tooreconfigure o serviço de nuvem através de Olá [a configuração do serviço (. cscfg)](cloud-services-model-and-package.md#cscfg) ficheiro. Primeiro tem de toodownload o. cscfg do ficheiro, modificá-lo, em seguida, carregá-la.

1. Clique em Olá **definições** ícone ou Olá **todas as definições** ligação tooopen segurança Olá **definições** painel.

    ![Página de definições](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Clique em Olá **configuração** item.

    ![Painel de configuração](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Clique em Olá **transferir** botão.

    ![Transferência](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Depois de atualizar o ficheiro de configuração do serviço de Olá, carregar e aplicar atualizações de configuração de Olá:

    ![Carregar](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Selecione o ficheiro. cscfg Olá e clique em **OK**.

## <a name="next-steps"></a>Passos seguintes
* Saiba como demasiado[implementar um serviço em nuvem](cloud-services-how-to-create-deploy-portal.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).
* [Gerir o serviço de nuvem](cloud-services-how-to-manage-portal.md).
* Configurar [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).
