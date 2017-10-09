---
title: "servidores de aaaRemove e desative a proteção | Microsoft Docs"
description: "Este artigo descreve como servidores de toounregister a partir de uma recuperação de Site do cofre e toodisable proteção para máquinas virtuais e servidores físicos."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Remover servidores e desativar proteção

Olá serviço Azure Site Recovery contribui tooyour continuidade do negócio e a estratégia de recuperação (BCDR) de desastre. serviço de Olá orquestra a replicação, ativação pós-falha e recuperação de máquinas virtuais e servidores físicos. As máquinas podem ser replicada tooAzure ou centro de dados do tooa secundário no local. Para uma descrição geral, leia [O que é o Azure Site Recovery?](site-recovery-overview.md)

Este artigo descreve como servidores de toounregister nos serviços de recuperação do cofre no Olá portal do Azure e como toodisable proteção para máquinas protegidas pela recuperação de sites.

Publique comentários ou perguntas na parte inferior de Olá deste artigo ou no Olá [fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Anular o registo de um servidor de configuração ligada

Se replicar VMs de VMware ou tooAzure de servidores físicos Windows/Linux, pode anular registo um servidor de configuração ligada de um cofre da seguinte forma:

1. Desative a proteção da máquina. No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.
2. Desassocie todas as políticas. No **infraestrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **políticas de replicação**, faça duplo clique em Olá política associada. Servidor de configuração do contexto Olá > **Disassociate**.
3. Remova quaisquer processos adicionais no local ou servidores de destino principal. No **infraestrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de Olá de contexto > **Eliminar**.
4. Elimine o servidor de configuração de Olá.
5. Desinstale manualmente o serviço de mobilidade de Olá em execução no servidor de destino mestre Olá (isto será um separado ou servidor ou em execução no servidor de configuração de Olá).
6. Desinstale todos os servidores adicionais do processo.
7. Desinstale o servidor de configuração de Olá.
8. No servidor de configuração de Olá, desinstale instância Olá MySQL que tenha sido instalado pelo Site Recovery.
9. No registo de hello do servidor de configuração de Olá eliminar a chave de Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Anular o registo de um servidor de configuração desligado

Se replicar VMs de VMware ou tooAzure de servidores físicos Windows/Linux, pode anular registo um servidor de configuração desligado de um cofre da seguinte forma:

1. Desative a proteção da máquina. No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**. Selecione **parar de gerir a máquina Olá**.
2. Remova quaisquer processos adicionais no local ou servidores de destino principal. No **infraestrutura de recuperação de Site** > **para VMWare e máquinas físicas** > **servidores de configuração**, servidor de Olá de contexto > **Eliminar**.
3. Elimine o servidor de configuração de Olá.
4. Desinstale manualmente o serviço de mobilidade de Olá em execução no servidor de destino mestre Olá (isto será um separado ou servidor ou em execução no servidor de configuração de Olá).
5. Desinstale todos os servidores adicionais do processo.
6. Desinstale o servidor de configuração de Olá.
7. No servidor de configuração de Olá, desinstale instância Olá MySQL que tenha sido instalado pelo Site Recovery.
8. No registo de hello do servidor de configuração de Olá eliminar a chave de Olá ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Anular o registo de um ligado ao servidor do VMM

Como melhor prática, recomendamos que pode anular o registo do servidor do VMM Olá quando estabeleceu tooAzure. Isto garante que limpar as definições nos servidores do VMM Olá (e noutros servidores do VMM com nuvens emparelhadas) são corretamente. Só deve remover um servidor de desligado, se existir um problema com conectividade permanente. Se o servidor do VMM Olá não está ligado, será necessário toomanually executar tooclean um script das definições.

1. Pare a replicar VMs em nuvens no Olá pretende tooremove de servidor do VMM.
2. Elimine quaisquer mapeamentos de rede utilizados pelo nuvens no Olá pretende toodelete de servidor do VMM. No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento da rede**, faça duplo clique mapeamento da rede Olá >  **Eliminar**.
3. Desassocie políticas de replicação das nuvens no Olá pretende tooremove de servidor do VMM.  No **infraestrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, faça duplo clique Olá associado à política. Faça duplo clique na nuvem de Olá > **Disassociate**.
4. Elimine o servidor do VMM Olá ou o nó ativo do VMM. No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **servidores VMM**, servidor de Olá contexto >  **Eliminar**.
5. Desinstale Olá fornecedor manualmente no servidor do VMM Olá. Se tiver um cluster, remova todos os nós.
6. Se estiver a replicar tooAzure, remova manualmente o agente de serviços de recuperação do Microsoft de Olá dos anfitriões Hyper-V em nuvens Olá eliminado.



### <a name="unregister-an-unconnected-vmm-server"></a>Anular o registo de um servidor VMM desligado

1. Pare a replicar VMs em nuvens no Olá pretende tooremove de servidor do VMM.
2. Elimine quaisquer mapeamentos de rede utilizados pelo nuvens no servidor do VMM Olá que pretende que o toodelete. No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **mapeamento da rede**, faça duplo clique mapeamento da rede Olá >  **Eliminar**.
3. Tenha em atenção Olá ID hello do servidor de VMM.
4. Desassocie políticas de replicação das nuvens no Olá pretende tooremove de servidor do VMM.  No **infraestrutura de recuperação de Site** > **para o System Center VMM** >  **políticas de replicação**, faça duplo clique Olá associado à política. Faça duplo clique na nuvem de Olá > **Disassociate**.
5. Elimine o servidor do VMM Olá ou o nó ativo. No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **servidores VMM**, servidor de Olá contexto >  **Eliminar**.
6. Transferir e executar Olá [script de limpeza](http://aka.ms/asr-cleanup-script-vmm) no servidor do VMM Olá. Abra o PowerShell com Olá **executar como administrador** opção, a política de execução de Olá toochange para âmbito do Olá predefinido (LocalMachine). No script de Olá, especifique o ID de Olá de Olá pretende tooremove de servidor do VMM. script de Olá remove informações do servidor de Olá de emparelhamento da nuvem e de registo.
5. Execute script de limpeza de Olá noutros servidores do VMM que contêm as nuvens que estão associadas a nuvens no Olá pretende tooremove de servidor do VMM.
6. Execute script de limpeza de Olá em qualquer outros passivos VMM nós de cluster que tenham Olá que fornecedor instalado.
7. Desinstale Olá fornecedor manualmente no servidor do VMM Olá. Se tiver um cluster, remova todos os nós.
8. Se replicar tooAzure, pode remover agente de serviços de recuperação do Microsoft Olá dos anfitriões Hyper-V em nuvens Olá eliminado.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Anular o registo de um anfitrião de Hyper-V num Site Hyper-V

Anfitriões Hyper-V que não são geridas pelo VMM foram recolhidas para um site de Hyper-V. Remova um anfitrião num site Hyper-V da seguinte forma:

1. Desative a replicação para as VMs de Hyper-V localizada num anfitrião Olá.
2. Desassocie políticas para o site de Hyper-V Olá. No **infraestrutura de recuperação de Site** > **para Sites de Hyper-V** >  **políticas de replicação**, faça duplo clique Olá associado à política. Site do contexto Olá > **Disassociate**.
3. Elimine anfitriões Hyper-V. No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **anfitriões Hyper-V**, servidor de Olá contexto >  **Eliminar**.
4. Elimine o site de Olá Hyper-V depois de todos os anfitriões foram removidos do mesmo. No **infraestrutura de recuperação de Site** > **para o System Center VMM** > **Sites Hyper-V**, site do contexto Olá >  **Eliminar**.
5. Execute o seguinte script em cada anfitrião de Hyper-V que removeu de Olá. script de Olá limpa as definições no servidor de Olá e anula o registo do Cofre de Olá.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping hello Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Desative a proteção para uma VM de VMware ou o servidor físico

1. No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.
2. No **remover máquina**, selecione uma destas opções:
    - **Desative a proteção da máquina de Olá (recomendada)**. Utilize este toostop opção máquina Olá a replicar. Definições de recuperação de site serão limpa automaticamente. Apenas será apresentada esta opção no Olá seguintes circunstâncias:
        - **Foi redimensionado volume VM Olá**— quando redimensionar um Olá volume virtual máquina entra no estado crítico. Selecione esta proteção de toodisables opção, mantendo o pontos de recuperação no Azure. Quando ativar a proteção da máquina de Olá novamente, Olá para volume Olá redimensionado serão dados tooAzure transferido.
        - **Recentemente tiver executar uma ativação pós-falha**— após executar uma ativação pós-falha tootest seu ambiente, selecione toostart esta opção proteger novamente máquinas no local. Desativa a cada máquina virtual e, em seguida, terá proteção tooenable para os mesmos novamente. A desativação Olá máquina com esta definição não afeta a máquina virtual de réplica de Olá no Azure. Não desinstale o serviço de mobilidade Olá da máquina de Olá.
    - **Parar de gerir a máquina Olá**. Se selecionar esta opção, máquina Olá só será removida do Cofre de Olá. As definições de proteção no local para a máquina Olá não serão afetadas. tooremove definições na máquina de Olá e a máquina de Olá tooremove do Olá subscrição do Azure, terá das definições de Olá tooclean por desinstalar o serviço de mobilidade Olá.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Desative a proteção para uma VM de Hyper-V numa nuvem VMM

1. No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.
2. No **remover máquina**, selecione uma destas opções:

    - **Desative a proteção da máquina de Olá (recomendada)**. Utilize este toostop opção máquina Olá a replicar. Definições de recuperação de site serão limpa automaticamente.
    - **Parar de gerir a máquina Olá**. Se selecionar esta opção, máquina Olá só será removida do Cofre de Olá. As definições de proteção no local para a máquina Olá não serão afetadas. tooremove definições na máquina de Olá e a máquina de Olá tooremove do Olá subscrição do Azure, terá das definições de Olá tooclean cópias de segurança manualmente, utilizando instruções Olá abaixo. Tenha em atenção que se selecionar toodelete Olá máquina e os respetivos discos rígidos, irá ser removidos do localização de destino Olá.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Limpar as definições de proteção - replicação tooa site secundário do VMM

Se tiver selecionado **parar de gerir a máquina Olá** e pode replicar tooa o site secundário, execute este script no servidor primário de Olá tooclean segurança Olá as definições de máquina virtual primária de Olá. Na consola do VMM Olá clique consola do VMM PowerShell de Olá tooopen Olá PowerShell botão. Substitua SQLVM1 com o nome de Olá da sua máquina virtual.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Servidor do VMM secundário Olá execute tooclean este script segurança Olá as definições de máquina virtual secundária de Olá:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Olá VMM do servidor secundário, atualize Olá máquinas de virtuais no servidor de anfitrião de Hyper-V Olá, para que hello VM secundário obtém detetado novamente na consola do VMM Olá.
4. Olá os passos acima limpar as definições de replicação de Olá no servidor do VMM Olá. Se pretender que a replicação da máquina virtual de Olá, execute o seguinte script esqueceu de Olá toostop Olá VMs primários e secundários. Substitua SQLVM1 com o nome de Olá da sua máquina virtual.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Limpar as definições de proteção - tooAzure de replicação

1. Se tiver selecionado **parar de gerir a máquina Olá** e replicar tooAzure, execute este script no servidor VMM de origem Olá, utilizando o PowerShell a partir da consola do VMM Olá.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Olá os passos acima limpar as definições de replicação de Olá no servidor do VMM Olá. toostop replicação da máquina virtual de Olá em execução no servidor de anfitrião de Hyper-V Olá, execute este script. Substitua SQLVM1 nome Olá da sua máquina virtual e host01.contoso.com com o nome de Olá Olá Hyper-V do servidor de anfitrião.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Desative a proteção para uma VM de Hyper-V num Site Hyper-V

Utilize este procedimento se está a replicar VMs Hyper-V tooAzure sem um servidor do VMM.

1. No **itens protegidos** > **itens replicados**, máquina do contexto Olá > **eliminar**.
2. No **remover máquina**, pode selecionar Olá seguintes opções:

   - **Desative a proteção da máquina de Olá (recomendada)**. Utilize este toostop opção máquina Olá a replicar. Definições de recuperação de site serão limpa automaticamente.
   - **Parar de gerir a máquina Olá**. Se selecionar esta opção máquina Olá só será removida do Cofre de Olá. As definições de proteção no local para a máquina Olá não serão afetadas. definições de tooremove máquina Olá e tooremove Olá excluir máquina virtual de Olá subscrição do Azure, terá das definições de Olá tooclean cópias de segurança manualmente. Se selecionar toodelete Olá máquina e os respetivos discos rígidos serão removidos da localização de destino Olá.
3. Se tiver selecionado **parar de gerir a máquina Olá**, execute este script no servidor de anfitrião do Hyper-V de origem Olá, tooremove replicação da máquina virtual de Olá. Substitua SQLVM1 com o nome de Olá da sua máquina virtual.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
