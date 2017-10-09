---
title: aaaConnect tooyour remotamente o dispositivo StorSimple | Microsoft Docs
description: "Explica como tooconfigure o dispositivo para a gestão remota e como tooconnect tooWindows do PowerShell para StorSimple através de HTTP ou HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Ligar remotamente o dispositivo de série de tooyour 8000 do StorSimple

## <a name="overview"></a>Descrição geral
Pode utilizar o dispositivo do Windows PowerShell remota tooconnect tooyour StorSimple. Quando se liga desta forma, não verá um menu. (Pode ver um menu apenas se utilizar a consola de série de Olá no Olá dispositivo tooconnect.) Com comunicação remota do Windows PowerShell, ligar específico tooa de espaço de execução. Também pode especificar o idioma de apresentação de Olá. 

Para mais informações sobre como utilizar o seu dispositivo toomanage de comunicação remota do Windows PowerShell, visite demasiado[utilize o Windows PowerShell para StorSimple tooadminister o dispositivo StorSimple](storsimple-windows-powershell-administration.md).

Este tutorial explica como tooconfigure o dispositivo para a gestão remota e, em seguida, tooconnect tooWindows do PowerShell para StorSimple. Pode utilizar HTTP ou HTTPS tooconnect através de comunicação remota do Windows PowerShell. No entanto, quando decidir como tooconnect tooWindows do PowerShell para StorSimple, considere o seguinte Olá: 

* Ligar diretamente toohello a consola de série do dispositivo é segura, mas a ligação consola de série de toohello através de comutadores de rede não está. Tenha cuidado Olá riscos de segurança ao ligar a consola de série do dispositivo de toohello através de comutadores de rede. 
* Ligar através de uma sessão HTTP poderá oferecem mais segurança ao ligar através da consola de série de Olá rede Olá. Embora não seja método mais seguro Olá, é aceitável em redes fidedignas. 
* Ligar através de uma sessão HTTPS com um certificado auto-assinado é Olá mais segura e Olá opção recomendada.

Pode ligar remotamente interface do Windows PowerShell toohello. No entanto, o dispositivo StorSimple de tooyour de acesso remoto através da interface do Windows PowerShell Olá não está ativado por predefinição. Precisar tooenable gestão remota no dispositivo Olá primeiro e, em seguida, no Olá cliente que é utilizado tooaccess seu dispositivo.

passos de Olá descritos neste artigo foram executados num sistema anfitrião com o Windows Server 2012 R2.

## <a name="connect-through-http"></a>Ligar através de HTTP
Ligar tooWindows do PowerShell para StorSimple através de uma sessão HTTP oferece mais segurança a que se ligam através da consola de série de Olá do dispositivo StorSimple. Embora não seja método mais seguro Olá, é aceitável em redes fidedignas.

Pode utilizar o Olá portal clássico do Azure ou a gestão remota do Olá consola de série tooconfigure. Selecione uma das Olá os seguintes procedimentos:

* [Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTP](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [Utilize a gestão remota do Olá consola de série tooenable através de HTTP](#use-the-serial-console-to-enable-remote-management-over-http)

Depois de ativar a gestão remota, utilize Olá seguir o cliente de Olá tooprepare procedimento para uma ligação remota.

* [Preparar o cliente Olá de ligação remota](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTP
Efetue Olá seguindo os passos na gestão remota do Olá tooenable de portal clássico do Azure através de HTTP.

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>gestão remota do tooenable através do Olá portal clássico do Azure
1. Acesso **dispositivos** > **configurar** para o seu dispositivo.
2. Desloque para baixo toohello **gestão remota** secção.
3. Definir **ativar a gestão remota** demasiado**Sim**.
4. Agora, pode escolher tooconnect através de HTTP. (a predefinição de Olá é tooconnect através de HTTPS.) Certifique-se de que o HTTP está selecionado.
   
   > [!NOTE]
   > A ligação através de HTTP é aceitável apenas em redes fidedignas.
   > 
   > 
5. Clique em **guardar** em Olá parte inferior da página Olá.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>Utilize a gestão remota do Olá consola de série tooenable através de HTTP
Efetue Olá os seguintes passos Olá gestão de dispositivos consola de série tooenable remoto.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>gestão remota do tooenable através da consola de série do dispositivo de Olá
1. No menu da consola de série de Olá, selecione a opção 1. Para mais informações sobre como utilizar a consola de série de Olá no dispositivo Olá, visite demasiado[ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Na linha de Olá, escreva:`Enable-HcsRemoteManagement –AllowHttp`
3. Será notificado sobre vulnerabilidades de segurança de Olá de utilizar HTTP tooconnect toohello dispositivo. Quando lhe for solicitado, confirme escrevendo **Y**.
4. Certifique-se de que está ativado HTTP escrevendo:`Get-HcsSystem`
5. Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsAndHttpEnabled**.hello seguinte ilustração mostra estas definições no PuTTY.
   
     ![Série HTTPS e HTTP ativada](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>Preparar o cliente Olá de ligação remota
Efetue Olá seguindo os passos na gestão remota do Olá cliente tooenable.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>cliente de Olá tooprepare para ligação remota
1. Inicie uma sessão do Windows PowerShell como administrador.
2. Escreva Olá seguinte endereço IP do comando tooadd Olá da lista de anfitriões fidedignos Olá StorSimple dispositivo toohello do cliente: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Substitua <*device_ip*> com o endereço IP Olá do seu dispositivo; por exemplo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Escreva Olá credenciais de dispositivo do comando toosave Olá numa variável os seguintes: 
   
    ```
    $cred = Get-Credential
    ```
    
4. Na caixa de diálogo de Olá que é apresentado:
   
   1. Nome de utilizador do tipo Olá neste formato: *device_ip\SSAdmin*.
   2. Escrever Olá dispositivo administrador palavra-passe que foi definido quando o dispositivo de Olá foi configurado com o Assistente de configuração de Olá. palavra-passe predefinida de Olá é *Password1*.
5. Inicie uma sessão do Windows PowerShell no dispositivo Olá escrevendo este comando:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate uma sessão do Windows PowerShell para utilização com Olá do dispositivo virtual StorSimple, acrescentar Olá `–Port` parâmetro e especifique a porta pública Olá configurada no sistema de interação remota para o dispositivo Virtual StorSimple.
   > 
   > 
   
     Nesta fase, deve ter uma Active Directory remota do Windows PowerShell sessão toohello do dispositivo.
   
    ![Comunicação remota do PowerShell através de HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>Ligar através de HTTPS
Ligar tooWindows do PowerShell para StorSimple através de uma sessão HTTPS é Olá mais segura e recomendada método do dispositivo de Microsoft Azure StorSimple tooyour remotamente ao ligar. Olá procedimentos a seguir explica como tooset segurança Olá série consola e dos computadores cliente para que possa utilizar HTTPS tooconnect tooWindows do PowerShell para StorSimple.

Pode utilizar o Olá portal clássico do Azure ou a gestão remota do Olá consola de série tooconfigure. Selecione uma das Olá os seguintes procedimentos:

* [Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTPS](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [Utilize a gestão remota do Olá consola de série tooenable através de HTTPS](#use-the-serial-console-to-enable-remote-management-over-https)

Depois de ativar a gestão remota, utilize Olá seguir o anfitrião de Olá tooprepare procedimentos para um gestão remota e ligar o dispositivo de toohello de anfitrião remoto Olá.

* [Preparar o anfitrião de Olá para a gestão remota](#prepare-the-host-for-remote-management)
* [Ligar dispositivo toohello de anfitrião remoto Olá](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>Utilize a gestão remota do Olá tooenable de portal clássico do Azure através de HTTPS
Efetue Olá seguindo os passos na gestão remota do Olá tooenable de portal clássico do Azure através de HTTPS.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>gestão remota tooenable através de HTTPS de Olá portal clássico do Azure
1. Acesso **dispositivos** > **configurar** para o seu dispositivo.
2. Desloque para baixo toohello **gestão remota** secção.
3. Definir **ativar a gestão remota** demasiado**Sim**.
4. Agora, pode escolher tooconnect através de HTTPS. (a predefinição de Olá é tooconnect através de HTTPS.) Certifique-se de que o HTTPS é selecionado. 
5. Clique em **Transferir certificado de gestão remota**. Especifique uma localização toosave este ficheiro. Terá de tooinstall este certificado no computador de cliente ou anfitrião Olá que irá utilizar tooconnect toohello dispositivo.
6. Clique em **guardar** em Olá parte inferior da página Olá.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>Utilize a gestão remota do Olá consola de série tooenable através de HTTPS
Efetue Olá os seguintes passos Olá gestão de dispositivos consola de série tooenable remoto.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>gestão remota do tooenable através da consola de série do dispositivo de Olá
1. No menu da consola de série de Olá, selecione a opção 1. Para mais informações sobre como utilizar a consola de série de Olá no dispositivo Olá, visite demasiado[ligar tooWindows do PowerShell para StorSimple através da consola de série do dispositivo](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Na linha de Olá, escreva: 
   
     `Enable-HcsRemoteManagement`
   
    Isto deve ativar HTTPS no seu dispositivo.
3. Certifique-se de que foi ativado HTTPS, escrevendo: 
   
     `Get-HcsSystem`
   
    Certifique-se de que Olá **RemoteManagementMode** campo mostra **HttpsEnabled**.hello seguinte ilustração mostra estas definições no PuTTY.
   
     ![Série ativadas por HTTPS](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Da saída de Olá de `Get-HcsSystem`, copie Olá o número de série do dispositivo Olá e guardá-lo para utilização posterior.
   
   > [!NOTE]
   > número de série de Olá mapeia o nome CN de toohello no certificado Olá.
   > 
   > 
5. Obter um certificado de gestão remota, escrevendo: 
   
     `Get-HcsRemoteManagementCert`
   
    Será apresentada a seguinte de toohello semelhante um certificado.
   
    ![Obter o certificado de gestão remota](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Copiar as informações de Olá certificado Olá **---BEGIN CERTIFICATE---** demasiado**---fim certificado---** num editor de texto, como o bloco de notas e guarde-como um ficheiro. cer. (Vai copiar este anfitrião remoto da tooyour de ficheiro ao preparar o anfitrião de Olá.)
   
   > [!NOTE]
   > toogenerate um novo certificado, utilize Olá `Set-HcsRemoteManagementCert` cmdlet.
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>Preparar o anfitrião de Olá para a gestão remota
computador de anfitrião de Olá tooprepare para uma ligação remota que utiliza uma sessão HTTPS, execute Olá os seguintes procedimentos:

* [Ficheiro. cer de Olá de importação para arquivo de raiz de hello do cliente Olá ou anfitrião remoto](#to-import-the-certificate-on-the-remote-host).
* [Adicionar ficheiro hosts toohello de números de série de dispositivos de Olá no seu anfitrião remoto](#to-add-device-serial-numbers-to-the-remote-host).

Cada um destes procedimentos é descrita abaixo.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>certificado de Olá tooimport no anfitrião remoto Olá
1. Clique no ficheiro. cer de Olá e selecione **instalar certificado**. Esta ação iniciará Olá Assistente para importar certificados.
   
    ![Assistente de importação de certificados 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. Para **localização do arquivo**, selecione **máquina Local**e, em seguida, clique em **seguinte**.
3. Selecione **colocar todos os certificados no Olá seguir arquivo**e, em seguida, clique em **procurar**. Navegue toohello o arquivo de raiz do seu anfitrião remoto e, em seguida, clique em **seguinte**.
   
    ![Assistente de importação de certificados 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. Clique em **Concluir**. É apresentada uma mensagem que indica que a importação de Olá foi concluída com êxito.
   
    ![Assistente de importação de certificados 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>anfitrião remoto de toohello números de série de dispositivo tooadd
1. Inicie o bloco de notas como administrador e, em seguida, abra o ficheiro de anfitriões de Olá localizado em \Windows\System32\Drivers\etc.
2. Adicionar Olá seguintes três ficheiro de anfitriões de tooyour entradas: **endereço IP de dados 0**, **endereço de IP fixo do controlador 0**, e **endereço IP fixo do controlador 1**.
3. Introduza o número de série do dispositivo Olá que guardou anteriormente. Mapear este endereço IP toohello conforme mostrado no Olá seguinte imagem. Para o controlador 0 e 1 de controlador, acrescentar **Controller0** e **Controller1** no fim de Olá do número de série de Olá (nome CN).
   
    ![Adicionar nome CN toohosts ficheiro](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Ficheiro de anfitriões de Olá guardado.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Ligar dispositivo toohello de anfitrião remoto Olá
Utilizar o Windows PowerShell e do SSL tooenter uma sessão de SSAdmin no seu dispositivo a partir de um anfitrião remoto ou o cliente. sessão de SSAdmin Olá mapeia toooption 1 na Olá [consola de série](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu do seu dispositivo.

Efetue Olá seguir o procedimento no computador de Olá partir do qual pretende que a ligação do toomake Olá remota do Windows PowerShell.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>tooenter uma sessão de SSAdmin no dispositivo de Olá através do Windows PowerShell e do SSL
1. Inicie uma sessão do Windows PowerShell como administrador.
2. Adicione anfitriões fidedignos Olá dispositivo IP endereço toohello do cliente, escrevendo:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Onde <*device_ip*> é o endereço IP Olá do seu dispositivo; por exemplo: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Crie uma credencial nova escrevendo: 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Onde <*IP do dispositivo-alvo*> é o endereço IP Olá de dados 0 para o seu dispositivo; por exemplo, **10.126.173.90** conforme mostrado no Olá anterior a imagem do ficheiro de anfitriões de Olá. Além disso, forneça a palavra-passe de administrador de Olá para o seu dispositivo.
4. Crie uma sessão introduzindo:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Para o parâmetro - ComputerName de Olá no cmdlet Olá, fornecer Olá <*número de série do dispositivo-alvo*>. Este número de série foi mapeado toohello endereço IP de dados 0 no ficheiro de anfitriões de Olá no seu anfitrião remoto; Por exemplo, **SHX0991003G44MT** conforme mostrado no Olá seguinte imagem.
5. Escreva: 
   
     `Enter-PSSession $session`
6. Terá de toowait uns minutos e, em seguida, será dispositivo tooyour ligado através de HTTPS através de SSL. Verá uma mensagem que indica que está ligado tooyour dispositivo.
   
    ![Comunicação remota do PowerShell através de HTTPS e SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [através do Windows PowerShell tooadminister o dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Saiba mais sobre [utilizando Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

