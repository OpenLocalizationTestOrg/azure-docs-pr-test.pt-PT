---
title: aaaPrepare tooAzure de tooupload um VHD do Windows | Microsoft Docs
description: Como tooprepare um VHD do Windows ou o VHDX antes de carregar tooAzure
services: virtual-machines-windows
documentationcenter: 
author: glimoli
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: genli
ms.openlocfilehash: 530390e4c6a4f66ddfd4da23338f9bb3708c299f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-a-windows-vhd-or-vhdx-tooupload-tooazure"></a>Preparar uma tooAzure de tooupload Windows VHD ou VHDX
Antes de carregar uma Windows as máquinas virtuais (VM) de tooMicrosoft no local do Azure, tem de preparar Olá disco de rígido virtual (VHD ou VHDX). Azure suporta apenas as VMs de geração 1 que estão no formato de ficheiro VHD Olá e tem um disco de tamanho fixo. tamanho máximo de Olá permitido para Olá que VHD é 1,023 GB. Pode converter uma geração 1 VM a partir de Olá VHDX tooVHD de sistema de ficheiros e de expansão dinâmica disco toofixed dimensão. Mas não é possível alterar a geração de uma VM. Para obter mais informações, consulte [devo criar uma geração 1 ou 2 VM no Hyper-V](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).

Para obter mais informações sobre a política de suporte de Olá para a VM do Azure, consulte [servidor software o suporte da Microsoft para as VMs do Microsoft Azure](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

> [!Note]
> instruções de Olá neste artigo aplicam-se toohello versão de 64 bits do Windows Server 2008 R2 e o sistema de operativo posterior do Windows server. Para obter informações sobre a versão de 32 bits em execução do sistema operativo no Azure, consulte [suporte para sistemas operativos de 32 bits em máquinas virtuais do Azure](https://support.microsoft.com/help/4021388/support-for-32-bit-operating-systems-in-azure-virtual-machines).

## <a name="convert-hello-virtual-disk-toovhd-and-fixed-size-disk"></a>Converter disco de tamanho fixo e Olá tooVHD de disco virtual 
Se precisar de tooconvert toohello o disco virtual necessário formato para o Azure, utilize um dos métodos de Olá nesta secção. Cópia de segurança Olá VM antes de executar o processo de conversão do disco virtual Olá e certifique-se de que Olá que VHD do Windows funciona corretamente no servidor local Olá. Resolva os eventuais erros no Olá própria VM antes de tentar tooconvert ou tooAzure a carregá-la.

Depois de converter disco de Olá, crie uma VM que utiliza Olá convertida disco. Abra e inicie sessão no toohello VM toofinish preparar Olá VM para o carregamento.

### <a name="convert-disk-using-hyper-v-manager"></a>Converter disco com o Gestor de Hyper-V
1. Abra o Gestor de Hyper-V e selecione o seu computador local Olá esquerda. No menu de Olá acima lista do computador Olá, clique em **ação** > **editar disco**.
2. No Olá **localizar disco rígido Virtual** ecrã, localize e selecione o disco virtual.
3. No Olá **selecionar ação** ecrã e, em seguida, selecione **converter** e **seguinte**.
4. Se precisar de tooconvert do VHDX, selecione **VHD** e, em seguida, clique em **seguinte**
5. Se precisar de tooconvert a partir de um disco de expansão dinâmica, selecione **um tamanho fixo** e, em seguida, clique em **seguinte**
6. Localize e selecione um caminho toosave Olá novo ficheiro VHD para.
7. Clique em **Concluir**.

>[!NOTE]
>comandos de Olá neste artigo tem de ser executados numa sessão do PowerShell elevada.

### <a name="convert-disk-by-using-powershell"></a>Converter disco utilizando o PowerShell
Pode converter um disco virtual através da utilização de Olá [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) comando no Windows PowerShell. Selecione **executar como administrador** quando inicie o PowerShell. 

Olá comando de exemplo seguinte converte VHDX tooVHD e um expansão dinâmica toofixed-tamanho do disco:

```Powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
Neste comando, substitua o valor de Olá para "-caminho" com Olá caminho toohello disco rígido virtual que pretende que o valor tooconvert e Olá para "-DestinationPath" com o novo caminho de Olá e o nome de Olá Converter disco.

### <a name="convert-from-vmware-vmdk-disk-format"></a>Converter o formato de disco VMDK de VMware
Se tiver uma imagem de VM do Windows hello [formato de ficheiro VMDK](https://en.wikipedia.org/wiki/VMDK), converta-tooa VHD utilizando Olá [Microsoft VM conversor](https://www.microsoft.com/download/details.aspx?id=42497). Para obter mais informações, consulte o artigo de blogue de Olá [como tooConvert um VMware VMDK tooHyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).

## <a name="set-windows-configurations-for-azure"></a>Definir as configurações do Windows para o Azure

No Olá VM que planeia tooAzure tooupload, execute todos os comandos no seguinte Olá os passos de uma [janela de linha de comandos elevada](https://technet.microsoft.com/library/cc947813.aspx):

1. Remova quaisquer rota estática persistente na tabela de encaminhamento Olá:
   
   * tabela de rotas de Olá tooview, execute `route print` Olá linha de comandos.
   * Verifique Olá **rotas de persistência** secções. Se existir uma rota persistente, utilize [rota eliminar](https://technet.microsoft.com/library/cc739598.apx) tooremove-lo.
2. Remova o proxy de WinHTTP Olá:
   
    ```PowerShell
    netsh winhttp reset proxy
    ```
3. Definir a política de SAN de disco de Olá demasiado[Onlineall](https://technet.microsoft.com/library/gg252636.aspx). 
   
    ```PowerShell
    diskpart 
    ```
    Na janela de linha de comandos aberta Olá, escreva Olá os seguintes comandos:

     ```DISKPART
    san policy=onlineall
    exit   
    ```

4. Definir o tempo de hora Universal Coordenada (UTC) para Windows e Olá o tipo de arranque de Olá serviço de hora do Windows (w32time) demasiado**automaticamente**:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation' -name "RealTimeIsUniversal" 1 -Type DWord

    Set-Service -Name w32time -StartupType Auto
    ```
5. Definir Olá energia perfil toohello **elevado desempenho**:

    ```PowerShell
    powercfg /setactive SCHEME_MIN
    ```

## <a name="check-hello-windows-services"></a>Verificação de serviços do Windows hello
Certifique-se de que cada um dos Olá os seguintes serviços do Windows está definida toohello **valores predefinidos do Windows**. Estes são os números de mínimo Olá de serviços que devem ser configurados toomake se que esse Olá VM tem conetividade. tooreset Olá arranque definições, executadas Olá os seguintes comandos:
   
```PowerShell
Set-Service -Name bfe -StartupType Auto
Set-Service -Name dhcp -StartupType Auto
Set-Service -Name dnscache -StartupType Auto
Set-Service -Name IKEEXT -StartupType Auto
Set-Service -Name iphlpsvc -StartupType Auto
Set-Service -Name netlogon -StartupType Manual
Set-Service -Name netman -StartupType Manual
Set-Service -Name nsi -StartupType Auto
Set-Service -Name termService -StartupType Manual
Set-Service -Name MpsSvc -StartupType Auto
Set-Service -Name RemoteRegistry -StartupType Auto
```

## <a name="update-remote-desktop-registry-settings"></a>Atualizar as definições de registo do ambiente de trabalho remoto
Certifique-se de que Olá seguintes definições estão configuradas corretamente para ligação ao ambiente de trabalho remoto:

>[!Note] 
>Poderá receber uma mensagem de erro quando executa Olá **Set ItemProperty-caminho ' HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal serviços - nome &lt;nome do objeto&gt; &lt;valor&gt;** nestes passos. mensagem de erro de saudação pode ser ignorada. Isto significa que apenas esse domínio Olá não é usada pelo que a configuração através de um objeto de política de grupo.
>
>

1. Protocolo RDP (Remote Desktop Protocol) está ativado:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDenyTSConnections" -Value 0 -Type DWord
    ```
   
2. Olá porta RDP está corretamente definida (porta 3389 predefinida):
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "PortNumber" 3389 -Type DWord
    ```
    Quando implementar uma VM, regras de predefinidas Olá são criadas em relação a porta 3389. Se pretender que o número da porta toochange Olá, fazê-lo Depois de Olá VM é implementado no Azure.

3. serviço de escuta de Olá está à escuta em cada interface de rede:
   
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "LanAdapter" 0 -Type DWord
   ```
4. Configure o modo de autenticação de nível de rede Olá nas ligações RDP Olá:
   
    ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SecurityLayer" 1 -Type DWord

    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "fAllowSecProtocolNegotiation" 1 -Type DWord
     ```

5. Defina o valor de ligação keep-alive Olá:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveEnable" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "KeepAliveInterval" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "KeepAliveTimeout" 1 -Type DWord
    ```
6. Restabeleça a ligação:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services' -name "fDisableAutoReconnect" 0 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fInheritReconnectSame" 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "fReconnectSame" 0 -Type DWord
    ```
7. Número de Olá de limite de ligações simultâneas:
    
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp' -name "MaxInstanceCount" 4294967295 -Type DWord
    ```
8. Se existirem que quaisquer certificados autoassinados associado o serviço de escuta do toohello RDP, remova-as:
    
    ```PowerShell
    Remove-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "SSLCertificateSHA1Hash"
    ```
    Este é toomake se de que pode ligar início Olá quando implementar Olá VM. Também pode rever este numa fase posterior após Olá que VM é implementada no Azure, se necessário.

9. Se Olá VM for parte de um domínio, certifique-se que todos os Olá seguir definições toomake certificar-se de que as definições anteriores Olá não são revertidas. políticas de Olá que tem de ser verificadas são seguinte Olá:
    
    - RDP está ativado:

         Computador Configuration\Policies\Windows Settings\Administrative Templates\ Components\Remote Services\Remote de ambiente de trabalho sessão de ambiente de trabalho Host\Connections:
         
         **Permitir que os utilizadores tooconnect remotamente utilizando o ambiente de trabalho remoto**

    - Política de grupo NLA:

        Settings\Administrative Host\Security de sessão de ambiente de trabalho de ambiente de trabalho Services\Remote Templates\Components\Remote: 
        
        **Exigir autenticação de utilizador para ligações remotas utilizando a autenticação de nível de rede**
    
    - Manter as definições de Alive:

        Computador Configuration\Policies\Windows Settings\Administrative administrativos\Componentes Components\Remote Services\Remote de ambiente de trabalho sessão de ambiente de trabalho Host\Connections: 
        
        **Configurar o intervalo de ligação keep-alive**

    - Definições de restabelecimento de ligação:

        Computador Configuration\Policies\Windows Settings\Administrative administrativos\Componentes Components\Remote Services\Remote de ambiente de trabalho sessão de ambiente de trabalho Host\Connections: 
        
        **Restabelecimento de ligação automático**

    - Limitar o número de Olá das definições de ligações:

        Computador Configuration\Policies\Windows Settings\Administrative administrativos\Componentes Components\Remote Services\Remote de ambiente de trabalho sessão de ambiente de trabalho Host\Connections: 
        
        **Limitar o número de ligações**

## <a name="configure-windows-firewall-rules"></a>Configurar regras de Firewall do Windows
1. Ative Firewall do Windows nos perfis de Olá três (domínio, Standard e público):

   ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\DomainProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\PublicProfile' -name "EnableFirewall" -Value 1 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\services\SharedAccess\Parameters\FirewallPolicy\Standardprofile' -name "EnableFirewall" -Value 1 -Type DWord
   ```

2. Execute Olá os seguintes comandos no PowerShell tooallow WinRM através de perfis de firewall de Olá três (domínio, privados e público) e ative Olá serviço remota do PowerShell:
   
   ```PowerShell
    Enable-PSRemoting -force
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
    netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
3. Ativar Olá seguir o tráfego RDP de Olá de tooallow de regras de firewall 

   ```PowerShell
    netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   ```   
4. Ative Olá ficheiro e a regra de partilha de impressoras para que hello VM possam responder comandos de ping tooa dentro Olá rede Virtual:

   ```PowerShell
    netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   ``` 
5. Se Olá VM irá fazer parte de um domínio, verifique Olá seguir definições toomake certificar-se de que as definições anteriores Olá não são revertidas. políticas de Olá AD tem de ser verificadas são seguinte Olá:

    - Ativar perfis de Firewall do Windows hello

        Computador Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **proteger todas as ligações de rede**

       Computador Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **proteger todas as ligações de rede**

    - Ativar RDP 

        Computador Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **permitir entradas exceções de ambiente de trabalho remoto**

        Computador Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **permitir entradas exceções de ambiente de trabalho remoto**

    - Ativar o ICMP V4

        Computador Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Domain Profile\Windows Firewall: **permitir exceções de ICMP**

        Computador Configuration\Policies\Windows Settings\Administrative Templates\Network\Network Connection\Windows Firewall\Standard Profile\Windows Firewall: **permitir exceções de ICMP**

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a>Certifique-se de que a VM está em bom estado, segura e acessível com RDP 
1. toomake se Olá disco se encontra em bom estado e consistente, execute uma operação de verificação do disco durante o reinício VM seguinte Olá:

    ```PowerShell
    Chkdsk /f
    ```
    Certifique-se de que o relatório de Olá mostra um disco limpo e bom estado de funcionamento.

2. Defina as definições de dados de configuração de arranque (BCD) Olá. 

    > [!Note]
    > Certifique-se de executar estes comandos na janela CMD elevada e **não** no PowerShell:
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. Certifique-se de que repositório de Instrumentations de gestão do Windows hello é consistente. tooperform, Olá execute os seguintes comandos:

    ```PowerShell
    winmgmt /verifyrepository
    ```
    Se o repositório de Olá está danificado, consulte o artigo [WMI: existência de danos no repositório, ou não](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not).

4. Certifique-se de que qualquer outra aplicação não está a utilizar a porta 3389 Olá. Esta porta é utilizada para Olá serviço RDP no Azure. Pode executar **netstat - anob** toosee que portas são utilizadas no Olá VM:

    ```PowerShell
    netstat -anob
    ```

5. Se Olá VHD do Windows que pretende que o tooupload for um controlador de domínio, em seguida, siga estes passos:

    A. Siga [estes passos Extras](https://support.microsoft.com/kb/2904015) disco de Olá tooprepare.

    B. Certifique-se de que sabe a palavra-passe DSRM Olá no caso de ter toostart Olá VM no DSRM, a determinada altura. Poderá ser útil toorefer toothis ligação tooset Olá [palavra-passe DSRM](https://technet.microsoft.com/library/cc754363(v=ws.11).aspx).

6. Certifique-se de que a conta de administrador incorporada Olá e a palavra-passe são conhecidos tooyou. Poderá pretender tooreset Olá administrador local palavra-passe atual e certifique-se de que pode utilizar esta conta toosign tooWindows através de Olá ligação RDP. Esta permissão de acesso é controlada por objeto de política de grupo "Permitir início de sessão através dos serviços de ambiente de trabalho remotos" Olá. Pode ver este objeto no Editor de políticas de Grupo Local de Olá em:

    Configuração de computador Definições Settings\Local Policies\User Rights Assignment

7. Verifique Olá seguir AD políticas toomake certificar-se de que não estão a bloquear o acesso RDP através de RDP nem a partir da rede Olá:

    - Computador configuração definições Settings\Local Policies\User Rights Assignment\Deny acesso toothis computador a partir da rede Olá

    - Registo de configuração definições Settings\Local Policies\User Rights Assignment\Deny do computador no através dos serviços de ambiente de trabalho remoto


8. Reinício Olá VM toomake se de que o Windows é bom ainda pode ser contactado através da utilização de ligação de RDP Olá. Neste momento, pode pretender toocreate uma VM no seu local Hyper-V toomake se Olá que VM está a iniciar completamente e, em seguida, testar, se se trata de RDP acessível.

9. Remover quaisquer filtros de Interface de controlador de transporte adicionais, como o software que analisa TCP pacotes ou firewalls adicionais. Também pode rever este numa fase posterior após Olá que VM é implementada no Azure, se necessário.

10. Desinstale qualquer software de terceiros e controladores que seja componentes relacionados toophysical ou qualquer outra tecnologia de virtualização.

### <a name="install-windows-updates"></a>Instalar atualizações do Windows
a configuração ideal Olá é demasiado**ter um nível de patch da máquina de Olá em Olá mais recente Olá**. Se não for possível, certifique-se de que Olá seguintes atualizações são instaladas:

|                       |                   |           |                                       Versão de ficheiro mínimo x64       |                                      |                                      |                            |
|-------------------------|-------------------|------------------------------------|---------------------------------------------|--------------------------------------|--------------------------------------|----------------------------|
| Componente               | Binário            | Windows 7 e Windows Server 2008 R2 | Windows 8 e Windows Server 2012             | Windows 8.1 e Windows Server 2012 R2 | Windows 10 e Windows Server 2016 RS1 | Windows 10 RS2             |
| Armazenamento                 | Disk.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17638 / 6.2.9200.21757 - KB3137061 | 6.3.9600.18203 - KB3137061           | -                                    | -                          |
|                         | Storport.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17188 / 6.2.9200.21306 - KB3018489 | 6.3.9600.18573 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.332             |
|                         | NTFS.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17623 / 6.2.9200.21743 - KB3121255 | 6.3.9600.18654 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.447             |
|                         | Iologmsg.dll      | 6.1.7601.23403 - KB3125574         | 6.2.9200.16384 - KB2995387                  | -                                    | -                                    | -                          |
|                         | Classpnp.sys      | 6.1.7601.23403 - KB3125574         | 6.2.9200.17061 / 6.2.9200.21180 - KB2995387 | 6.3.9600.18334 - KB3172614           | 10.0.14393.953 - KB4022715           | -                          |
|                         | Volsnap.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17047 / 6.2.9200.21165 - KB2975331 | 6.3.9600.18265 - KB3145384           | -                                    | 10.0.15063.0               |
|                         | partmgr.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.16681 - KB2877114                  | 6.3.9600.17401 - KB3000850           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | volmgr.sys        |                                    |                                             |                                      |                                      | 10.0.15063.0               |
|                         | Volmgrx.sys       | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | 10.0.15063.0               |
|                         | Msiscsi.sys       | 6.1.7601.23403 - KB3125574         | 6.2.9200.21006 - KB2955163                  | 6.3.9600.18624 - KB4022726           | 10.0.14393.1066 - KB4022715          | 10.0.15063.447             |
|                         | MSDSM.sys         | 6.1.7601.23403 - KB3125574         | 6.2.9200.21474 - KB3046101                  | 6.3.9600.18592 - KB4022726           | -                                    | -                          |
|                         | MPIO.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.21190 - KB3046101                  | 6.3.9600.18616 - KB4022726           | 10.0.14393.1198 - KB4022715          | -                          |
|                         | Fveapi.dll        | 6.1.7601.23311 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.18294 - KB3172614           | 10.0.14393.576 - KB4022715           | -                          |
|                         | Fveapibase.dll    | 6.1.7601.23403 - KB3125574         | 6.2.9200.20930 - KB2930244                  | 6.3.9600.17415 - KB3172614           | 10.0.14393.206 - KB4022715           | -                          |
| Rede                 | netvsc.sys        | -                                  | -                                           | -                                    | 10.0.14393.1198 - KB4022715          | 10.0.15063.250 - KB4020001 |
|                         | mrxsmb10.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.22108 - KB4022724                  | 6.3.9600.18603 - KB4022726           | 10.0.14393.479 - KB4022715           | 10.0.15063.483             |
|                         | mrxsmb20.sys      | 6.1.7601.23816 - KB4022722         | 6.2.9200.21548 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.483             |
|                         | Mrxsmb.sys        | 6.1.7601.23816 - KB4022722         | 6.2.9200.22074 - KB4022724                  | 6.3.9600.18586 - KB4022726           | 10.0.14393.953 - KB4022715           | 10.0.15063.0               |
|                         | Tcpip.sys         | 6.1.7601.23761 - KB4022722         | 6.2.9200.22070 - KB4022724                  | 6.3.9600.18478 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.447             |
|                         | http.sys          | 6.1.7601.23403 - KB3125574         | 6.2.9200.17285 - KB3042553                  | 6.3.9600.18574 - KB4022726           | 10.0.14393.251 - KB4022715           | 10.0.15063.483             |
|                         | vmswitch.sys      | 6.1.7601.23727 - KB4022719         | 6.2.9200.22117 - KB4022724                  | 6.3.9600.18654 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.138             |
| Principal                    | Ntoskrnl.exe      | 6.1.7601.23807 - KB4022719         | 6.2.9200.22170 - KB4022718                  | 6.3.9600.18696 - KB4022726           | 10.0.14393.1358 - KB4022715          | 10.0.15063.483             |
| Serviços de Ambiente de Trabalho Remoto | rdpcorets.dll     | 6.2.9200.21506 - KB4022719         | 6.2.9200.22104 - KB4022724                  | 6.3.9600.18619 - KB4022726           | 10.0.14393.1198 - KB4022715          | 10.0.15063.0               |
|                         | TERMSRV.dll       | 6.1.7601.23403 - KB3125574         | 6.2.9200.17048 - KB2973501                  | 6.3.9600.17415 - KB3000850           | 10.0.14393.0 - KB4022715             | 10.0.15063.0               |
|                         | termdd.sys        | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Win32k.sys        | 6.1.7601.23807 - KB4022719         | 6.2.9200.22168 - KB4022718                  | 6.3.9600.18698 - KB4022726           | 10.0.14393.594 - KB4022715           | -                          |
|                         | rdpdd.dll         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
|                         | Rdpwd.sys         | 6.1.7601.23403 - KB3125574         | -                                           | -                                    | -                                    | -                          |
| Segurança                | TooWannaCrypt devida | KB4012212                          | KB4012213                                   | KB4012213                            | KB4012606                            | KB4012606                  |
|                         |                   |                                    | KB4012216                                   |                                      | KB4013198                            | KB4013198                  |
|                         |                   | KB4012215                          | KB4012214                                   | KB4012216                            | KB4013429                            | KB4013429                  |
|                         |                   |                                    | KB4012217                                   |                                      | KB4013429                            | KB4013429                  |
       
### Quando toouse sysprep<a id="step23"></a>    

Sysprep é um processo que é possível executar para uma instalação do windows que irá repor a instalação de Olá do sistema de Olá e irá fornecer um "Box Olá experience", removendo todos os dados pessoais e reponha vários componentes. Fazê-lo, normalmente, se quiser toocreate um modelo a partir da qual pode implementar várias outras VMs que tiverem uma configuração específica. Esta opção é denominada uma **generalizado imagem**.

Se, em vez disso, pretende apenas toocreate um VM a partir de um disco, não tem toouse sysprep. Nesta situação, pode pois criar simplesmente Olá VM a partir do qual é conhecido como um **imagem especializada**.

Para obter mais informações sobre como toocreate uma VM a partir de um disco especializada, consulte:

- [Criar uma VM a partir de um disco especializado](create-vm-specialized.md)
- [Criar uma VM a partir de um disco especializado do VHD](https://azure.microsoft.com/resources/templates/201-vm-specialized-vhd/)

Se quiser toocreate uma imagem generalizada, terá de toorun sysprep. Para obter mais informações sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx). 

Nem todas as funções ou aplicação que é instalada num computador baseado em Windows suporta este generalização. Por isso, antes do executar este procedimento, consulte toohello seguinte artigo toomake se essa função Olá desse computador é suportada pelo sysprep. Para obter mais informações, [suporte de Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

### <a name="steps-toogeneralize-a-vhd"></a>Passos toogeneralize um VHD

>[!NOTE]
> Depois de executar o sysprep.exe como Olá especificado nos seguintes passos, desligue Olá VM e não ativá-la novamente até que crie uma imagem do mesmo no Azure.

1. Inicie sessão no toohello VM do Windows.
2. Executar **linha de comandos** como administrador. 
3. Diretório de Olá alterar para: **%windir%\system32\sysprep**e, em seguida, execute **sysprep.exe**.
3. No Olá **ferramenta de preparação de sistema** caixa de diálogo, selecione **introduza sistema Out-of-Box experiência (OOBE)**e certifique-se de que Olá **Generalize** caixa de verificação está selecionada.

    ![Ferramenta de preparação do sistema](media/prepare-for-upload-vhd-image/syspre.png)
4. No **as opções de encerramento**, selecione **encerramento**.
5. Clique em **OK**.
6. Quando tiver concluído o Sysprep, encerre Olá VM. Não utilize **reiniciar** tooshut baixo Olá VM.
7. Olá VHD está agora pronto toobe carregado. Para obter mais informações sobre como toocreate uma VM a partir de um disco generalizado, consulte o artigo [carregar um VHD generalizado e utilizá-la toocreate um novas VMs no Azure](sa-upload-generalized.md).


## <a name="complete-recommended-configurations"></a>Conclua as configurações recomendadas
Olá seguintes definições não afeta a carregar o VHD. No entanto, recomendamos vivamente que configurou-los.

* Instalar Olá [o agente de VMs do Azure](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Em seguida, pode ativar as extensões de VM. extensões VM Olá implementam a maioria das funcionalidades de crítico Olá, que poderá pretender toouse com as suas VMs tal como repor palavras-passe, configurar o RDP e assim sucessivamente. Para obter mais informações, consulte:

    - [Agente da VM e extensões – parte 1](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-1/)
    - [Extensões – parte 2 e o agente da VM](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/)
* registo de captura Olá pode ser úteis na resolução de problemas de falha do Windows. Ative a recolha de registos de informação de Olá:
  
    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "AutoReboot" -Value 0 -Type DWord
    New-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps'
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    New-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
    Se receber erros durante a qualquer um dos procedimentos Olá os passos neste artigo, isto significa que as chaves de registo Olá já existe. Nesta situação, utilize Olá em vez disso, os seguintes comandos:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "CrashDumpEnable" -Value "2" -Type DWord
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\CrashControl' -name "DumpFile" -Value "%SystemRoot%\MEMORY.DMP"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpFolder" -Value "c:\CrashDumps"
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpCount" -Value 10 -Type DWord
    Set-ItemProperty -Path 'HKLM:\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps' -name "DumpType" -Value 2 -Type DWord
    Set-Service -Name WerSvc -StartupType Manual
    ```
*  Depois de Olá VM é criada no Azure, recomendamos que colocou o ficheiro de paginação Olá no desempenho de tooimprove Olá "Unidade Temporal" volume. Pode configurar esta da seguinte forma:

    ```PowerShell
    Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management' -name "PagingFiles" -Value "D:\pagefile"
    ```
Se não houver qualquer disco de dados que é anexado toohello VM, a letra de unidade do volume de unidade Temporal Olá é, geralmente, "D." Este designação pode ser diferente, dependendo do número de Olá de unidades disponíveis e as definições de Olá que efetuar.

## <a name="next-steps"></a>Passos seguintes
* [Carregar um tooAzure de imagem de VM do Windows para implementações do Resource Manager](upload-generalized-managed.md)

