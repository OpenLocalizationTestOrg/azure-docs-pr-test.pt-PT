---
title: "problemas de implementação do StorSimple aaaTroubleshoot | Microsoft Docs"
description: Descreve como toodiagnose e corrija erros ocorridos ao primeiro implementar StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Resolver problemas de implementação do dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Este artigo fornece orientação de resolução de problemas úteis para a sua implementação do Microsoft Azure StorSimple. Descreve problemas comuns, as causas possíveis e toohelp passos recomendados que resolver problemas que podem ocorrer quando configurar StorSimple. Estas informações aplicam-se o dispositivo virtual StorSimple Olá e o dispositivo físico do tooboth Olá StorSimple no local.

> [!NOTE]
> Problemas relacionados com a configuração de dispositivos pode enfrentam podem ocorrer quando implementar o dispositivo Olá Olá pela primeira vez, ou pode ocorrem mais tarde, quando o dispositivo de Olá está operacional. Este artigo foca-se na resolução de problemas de implementação da primeira vez. tootroubleshoot um dispositivo operacional, aceda demasiado[resolver problemas com dispositivos operacional](storsimple-troubleshoot-operational-device.md).
> 
> 

Este artigo também descreve ferramentas Olá para resolução de problemas de implementações do StorSimple e fornece um exemplo de resolução de problemas passo a passo.

## <a name="first-time-deployment-issues"></a>Problemas de implementação da primeira vez
Caso se depare com um problema ao implementar o seu dispositivo para Olá pela primeira vez, considere o seguinte Olá:

* Se estiver a resolver um dispositivo físico, certifique-se de que foi instalado e configurado conforme descrito em hardware de Olá [instalar o seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar o seu dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
* Verificar os pré-requisitos para a implementação. Certifique-se de que todas as informações de Olá descritas Olá [lista de verificação de configuração de implementação](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Reveja Olá notas de versão do StorSimple toosee se o problema de Olá é descrito. notas de versão Olá incluem soluções para problemas conhecidos de instalação. 

Durante a implementação do dispositivo, Olá mais comuns problemas que os utilizadores enfrentam ocorrer quando o Assistente de configuração de Olá são executados e, quando estes registar o dispositivo de Olá através do Windows PowerShell para StorSimple. (Pode utiliza o Windows PowerShell para StorSimple tooregister e configurar o dispositivo StorSimple. Para obter mais informações sobre o registo de dispositivos, consulte [passo 3: configurar e registar o dispositivo através do Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Olá seguintes secções pode ajudar a resolver problemas que encontrar quando configurou o dispositivo StorSimple Olá para Olá pela primeira vez.

## <a name="first-time-setup-wizard-process"></a>Processo do Assistente de configuração da primeira vez
Olá, os passos seguintes resume o processo do Assistente de configuração de Olá. Para informações de configuração detalhadas, consulte [implementar o dispositivo StorSimple no local](storsimple-deployment-walkthrough.md).

1. Executar Olá [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) cmdlet toostart Olá Assistente de configuração que irá guiá-lo Olá restantes passos. 
2. Configurar rede Olá: Assistente de configuração de Olá permite-lhe configurar definições de rede para Olá interface rede DATA 0 no dispositivo StorSimple. Estas definições incluem o seguinte Olá:
   * Virtual IP (VIP), máscara de sub-rede e gateway – Olá [conjunto HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet é executado em segundo plano de Olá. Configura o endereço IP Olá, máscara de sub-rede e gateway Olá dados 0 interface de rede no dispositivo StorSimple.
   * Servidor DNS primário – Olá [conjunto HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet é executado em segundo plano de Olá. Configura as definições de DNS de Olá para a sua solução StorSimple.
   * Servidor NTP – Olá [conjunto HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet é executado em segundo plano de Olá. Configura definições do servidor NTP Olá para a sua solução StorSimple.
   * Opcional web proxy – hello [conjunto HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet é executado em segundo plano de Olá. É também define e permite Olá configuração de proxy web para a sua solução StorSimple.
3. Configurar palavras-passe de Olá: Olá passo seguinte consiste em tooset segurança administrador de dispositivos e as palavras-passe do Snapshot Manager do StorSimple. Se estiver a executar o Update 1, em seguida, não será necessário tooset segurança palavra-passe do Olá Snapshot Manager do StorSimple.
   
   * palavra-passe de administrador de dispositivo Olá é toolog utilizado no dispositivo tooyour. palavra-passe de dispositivo do Olá predefinida é **Password1**.
   * palavra-passe do Olá Snapshot Manager do StorSimple é necessária quando configura um toouse dispositivo Snapshot Manager do StorSimple. Precisa de toofirst definir Olá palavra-passe no Assistente de configuração de Olá, e, em seguida, pode definir e alterá-la a partir de Olá serviço StorSimple Manager. Esta palavra-passe autentica o dispositivo de Olá com Snapshot Manager do StorSimple.
     
     > [!IMPORTANT]
     > As palavras-passe são recolhidas antes do registo, mas aplicadas apenas depois de registar o dispositivo de Olá com êxito. Se existir uma falha tooapply uma palavra-passe, será palavra-passe do pedido toosupply Olá novamente até que Olá necessárias palavras-passe (que cumpre os requisitos de complexidade de Olá) são recolhidas.
     > 
     > 
4. Registar o dispositivo de Olá: passo final Olá é o dispositivo de Olá tooregister com o serviço do StorSimple Manager Olá em execução no Microsoft Azure. registo de Olá requer demasiado[obter chave de registo do serviço de Olá](storsimple-manage-service.md#get-the-service-registration-key) de Olá portal clássico do Azure e fornecê-lo no Assistente de configuração de Olá. Depois do dispositivo de Olá for registado com êxito, uma chave de encriptação de dados do serviço é fornecida tooyou. Lembre-se de que tookeep esta encriptação de chave numa localização segura porque será necessário tooregister todos os dispositivos subsequentes com o serviço de Olá.

## <a name="common-errors-during-device-deployment"></a>Erros comuns durante a implementação do dispositivo
Olá seguintes tabelas lista Olá erros comuns que poderão surgir quando tiver:

* Configure as definições de rede de Olá necessário.
* Configure as definições de proxy de web opcional Olá.
* Configure o administrador de dispositivos de Olá e palavras-passe do Snapshot Manager do StorSimple. 
* Registar o dispositivo Olá. 

## <a name="errors-during-hello-required-network-settings"></a>Erros durante a Olá necessário as definições de rede
| Não. | Mensagem de erro | Causas possíveis | Ação recomendada |
| --- | --- | --- | --- |
| 1 |Invocar HcsSetupWizard: Este comando só pode ser executado num controlador de Olá Active Directory. |Configuração estava a ser efetuada num controlador de Olá passiva. |Execute este comando a partir do controlador ativo Olá. Para obter mais informações, consulte [identificar um controlador de Active Directory no seu dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invocar HcsSetupWizard: Dispositivo não preparado. |Existem problemas com a conectividade de rede Olá nos dados 0. |Verifique a conectividade de rede física Olá nos dados 0. |
| 3 |Invocar HcsSetupWizard: Há um conflito de endereços IP com outro sistema na rede de Olá (excepção de HRESULT: 0x80070263). |IP Olá fornecido para DATA 0 já estava a ser utilizado por outro sistema. |Forneça um novo IP que não está em utilização. |
| 4 |Invocar HcsSetupWizard: Falha de um recurso de cluster. (Excepção de HRESULT: 0x800713AE). |VIP duplicado. IP Olá fornecido já se encontra em utilização. |Forneça um novo IP que não está em utilização. |
| 5 |Invocar HcsSetupWizard: Endereço de IPv4 inválida. |endereço IP Olá é fornecido num formato incorreto. |Verifique o formato de Olá e forneça o seu endereço IP novamente. Para obter mais informações, consulte [endereçamento Ipv4][1]. |
| 6 |Invocar HcsSetupWizard: Endereço de IPv6 inválida. |endereço IP Olá é fornecido num formato incorreto. |Verifique o formato de Olá e forneça o seu endereço IP novamente. Para obter mais informações, consulte [Ipv6 endereçamento][2]. |
| 7 |Invocar HcsSetupWizard: Não existem não existem pontos finais mais disponível a partir do mapeador de ponto final de Olá. (Excepção de HRESULT: 0x800706D9) |a funcionalidade de cluster Olá não está a funcionar. |[Contacte o Support Microsoft](storsimple-contact-microsoft-support.md) para passos seguintes. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Erros durante a definições de proxy de web opcional Olá
| Não. | Mensagem de erro | Causas possíveis | Ação recomendada |
| --- | --- | --- | --- |
| 1 |Invocar HcsSetupWizard: Parâmetro inválido (excepção de HRESULT: 0x80070057) |Um dos parâmetros de Olá fornecidos para as definições de proxy Olá não é válido. |Olá URI não é fornecido no formato correto Olá. Olá utilize seguinte formato: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invocar HcsSetupWizard: Servidor de RPC não está disponível (excepção de HRESULT: 0x800706ba) |causa de raiz de Olá é uma das seguintes Olá:<ol><li>cluster de Olá não está ativo.</li><li>controlador passivo Olá não consegue comunicar com o controlador de Active Directory Olá e comandos de Olá é executado a partir do controlador passivo.</li></ol> |Dependendo da causa de raiz de Olá:<ol><li>[Contacte o Support Microsoft](storsimple-contact-microsoft-support.md) toomake se esse cluster Olá está a funcionar.</li><li>Execute o comando de Olá do controlador ativo Olá. Se pretender que o comando de Olá toorun do controlador passivo Olá, terá de tooensure desse controlador passivo Olá consegue comunicar com o controlador Olá de Active Directory. Terá de demasiado[contacte a Microsoft Support](storsimple-contact-microsoft-support.md) se este conectividade está danificada.</li></ol> |
| 3 |HcsSetupWizard invocar: Falha de chamada RPC (excepção de HRESULT: 0x800706be) |Cluster está inativo. |[Contacte o Support Microsoft](storsimple-contact-microsoft-support.md) toomake se esse cluster Olá está a funcionar. |
| 4 |Invocar HcsSetupWizard: Não foi encontrado do recurso de Cluster (excepção de HRESULT: 0x8007138f) |recurso de cluster Olá não foi encontrado. Isto pode acontecer quando a instalação de Olá não estava correta. |Poderá ser necessário tooreset Olá dispositivo toohello predefinições de fábrica. [Contacte o Support Microsoft](storsimple-contact-microsoft-support.md) toocreate um recurso de cluster. |
| 5 |Invocar HcsSetupWizard: Não online do recurso de Cluster (excepção de HRESULT: 0x8007138c) |Os recursos do cluster não estão online. |[Contacte o Support Microsoft](storsimple-contact-microsoft-support.md) para passos seguintes. |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Erros relacionados com o administrador de toodevice e palavras-passe do Snapshot Manager do StorSimple
palavra-passe de administrador de dispositivo de predefinição Olá é **Password1**. Esta palavra-passe expira após Olá primeiro início de sessão; Por conseguinte, terá de toochange de Assistente de configuração de Olá toouse-lo. Tem de fornecer uma palavra-passe do novo dispositivo administrador quando registar o dispositivo de Olá para Olá pela primeira vez. 

Se utilizar o software de Snapshot Manager do StorSimple Olá em execução no dispositivo de Olá de toomanage do anfitrião do Windows Server de Olá, em seguida, tem também de fornecer uma palavra-passe do Snapshot Manager do StorSimple durante o registo da primeira vez. 

Certifique-se de que as palavras-passe cumprem os requisitos de Olá:

* A palavra-passe de administrador do dispositivo deve ter entre 8 e 15 carateres.
* A palavra-passe do Snapshot Manager do StorSimple deve ser entre 14 e 15 carateres.
* As palavras-passe devem conter 3 dos Olá 4 tipos de carateres seguintes: minúsculas, maiúsculas, numérico e especiais. 
* A palavra-passe não pode ser Olá igual à Olá últimas 24 palavras-passe.

Além disso, tenha em atenção que as palavras-passe expirarem todos os anos e pode ser alterada apenas depois de registar o dispositivo de Olá com êxito. Se o registo de Olá falhar por algum motivo, as palavras-passe de Olá não serão alteradas. Para obter mais informações sobre o administrador do dispositivo e as palavras-passe do Snapshot Manager do StorSimple, visite demasiado[utilize Olá toochange de serviço StorSimple Manager as palavras-passe do StorSimple](storsimple-change-passwords.md).

Pode encontrar um ou mais dos Olá seguintes erros ao definir administrador do dispositivo Olá e palavras-passe do Snapshot Manager do StorSimple.

| Não. | Mensagem de erro | Ação recomendada |
| --- | --- | --- |
| 1 |palavra-passe de Olá excede o comprimento de máximo de Olá. |Utilize uma palavra-passe que cumpra estes requisitos:<ul><li>A palavra-passe de administrador do dispositivo tem de ter entre 8 e 15 carateres.</li><li>A palavra-passe do Snapshot Manager do StorSimple tem de ser entre 14 e 15 carateres.</li></ul> |
| 2 |palavra-passe de Olá não cumpre o comprimento de Olá necessário. |Utilize uma palavra-passe que cumpra estes requisitos:<ul><li>A palavra-passe de administrador do dispositivo tem de ter entre 8 e 15 carateres.</li><li>A palavra-passe do Snapshot Manager do StorSimple tem de ser entre 14 e 15 carateres.</lu></ul> |
| 3 |palavra-passe de Olá tem de conter carateres minúsculos. |As palavras-passe tem de conter 3 dos Olá 4 tipos de carateres seguintes: minúsculas, maiúsculas, numérico e especiais. Certifique-se de que a palavra-passe cumpra estes requisitos. |
| 4 |palavra-passe de Olá tem de conter carateres. |As palavras-passe tem de conter 3 dos Olá 4 tipos de carateres seguintes: minúsculas, maiúsculas, numérico e especiais. Certifique-se de que a palavra-passe cumpra estes requisitos. |
| 5 |palavra-passe de Olá tem de conter carateres especiais. |As palavras-passe tem de conter 3 dos Olá 4 tipos de carateres seguintes: minúsculas, maiúsculas, numérico e especiais. Certifique-se de que a palavra-passe cumpra estes requisitos. |
| 6 |Olá palavra-passe tem de conter 3 dos Olá 4 tipos de carateres seguintes: maiúsculas, minúsculas, numérico e especiais. |A palavra-passe não contém tipos de Olá necessário de carateres. Certifique-se de que a palavra-passe cumpra estes requisitos. |
| 7 |Parâmetro não corresponde a confirmação. |Certifique-se de que a palavra-passe cumpre todos os requisitos e que introduziu corretamente. |
| 8 |A palavra-passe não pode corresponder a predefinição de Olá. |palavra-passe predefinida de Olá é *Password1*. Terá de toochange esta palavra-passe depois de iniciar sessão para Olá pela primeira vez. |
| 9 |palavra-passe de Olá que introduziu não corresponde à palavra-passe de dispositivo Olá. . Reescreva a palavra-passe de Olá. |Verifique a palavra-passe de Olá e escrevê-lo novamente. |

As palavras-passe são recolhidas antes do dispositivo de Olá está registado, mas são aplicadas apenas após o registo com êxito. fluxo de trabalho de recuperação de palavra-passe de Olá requer Olá toobe de dispositivo registado. 

> [!IMPORTANT]
> Em geral, se uma tentativa de tooapply uma palavra-passe falha, em seguida, o software de Olá tenta repetidamente palavra-passe do toocollect Olá até ter êxito. Em situações raras, não é possível aplicar a palavra-passe de Olá. Nesta situação, pode registar o dispositivo de Olá e prosseguir, no entanto palavras-passe de Olá não serão alteradas. Não receberá nenhuma indicação como palavra-passe de toowhich não foi alterada — palavra-passe de administrador de dispositivo Olá ou palavra-passe do Olá Snapshot Manager do StorSimple. Se esta situação ocorrer, recomendamos que altere ambas as palavras-passe.
> 
> 

Só pode repor Olá palavras-passe em Olá portal clássico do Azure através de Olá serviço StorSimple Manager. Para obter mais informações, aceda a: 

* [Palavra-passe de administrador de dispositivo de Olá alteração](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Alterar palavra-passe Snapshot Manager do StorSimple Olá](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Erros durante o registo de dispositivos
Utilizar o serviço do StorSimple Manager Olá em execução no dispositivo do Microsoft Azure tooregister Olá. Foi possível encontrar um ou mais dos Olá os seguintes problemas durante o registo do dispositivo.

| Não. | Mensagem de erro | Causas possíveis | Ação recomendada |
| --- | --- | --- | --- |
| 1 |Erro 350027: Falha ao dispositivo de Olá tooregister com Olá StorSimple Manager. | |Aguarde alguns minutos e, em seguida, repita a operação Olá. Se Olá problema persistir, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md). |
| 2 |Erro 350013: Ocorreu um erro no dispositivo Olá a registar. Isto pode ser devido a chave de registo do serviço de tooincorrect. | |Registe o dispositivo de Olá novamente com a chave de registo do serviço correto Olá. Para obter mais informações, consulte [chave de registo do serviço de Olá Get.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Erro 350063: Foi transmitida autenticação tooStorSimple Manager service, mas falha do registo. Repita a operação de Olá após algum tempo. |Este erro indica que a autenticação com ACS foi efectuada com êxito, mas Olá register chamada efetuada toohello serviço falhou. Isto pode ser um resultado de uma falha de rede esporádicas. |Se o problema de Olá situação persistir, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md). |
| 4 |Erro 350049: não foi possível aceder o serviço de Olá durante o registo. |Quando é efetuada a chamada de Olá a toohello serviço, é recebeu uma exceção da web. Em alguns casos, isto poderá obter fixo com repetir Olá operação mais tarde. |Verifique o endereço IP e nome DNS e, em seguida, repita a operação de Olá. Se Olá problema persistir, [contacte Support da Microsoft.](storsimple-contact-microsoft-support.md) |
| 5 |Erro 350031: dispositivo Olá já foi registado. | |Nenhuma ação necessária. |
| 6 |Erro 350016: Falha de registo de dispositivos. | |Certifique-se a chave de registo do Olá está correto. |
| 7 |Invocar HcsSetupWizard: Ocorreu um erro ao registar o seu dispositivo; Isto pode dever-se devido tooincorrect endereço IP ou nome de DNS. Verifique as definições de rede e tente novamente. Se Olá problema persistir, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md). (Erro 350050) |Certifique-se de que o dispositivo pode enviar ping Olá fora da rede. Se não tiver rede toooutside de conectividade, registo de Olá pode falhar com este erro. Este erro pode ser uma combinação de um ou mais dos seguintes Olá:<ul><li>IP incorreto</li><li>Sub-rede incorreto</li><li>Gateway incorreto</li><li>Definições de DNS incorretas</li></ul> |Consulte Olá os passos em Olá [exemplo passo a passo de resolução de problemas](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invocar HcsSetupWizard: Olá operação atual falhou devido a erro no serviço interno tooan [0x1FBE2]. Repita a operação de Olá após algum tempo. Se Olá problema persistir, contacte Support da Microsoft. |Este é um erro genérico emitido para todos os erros de invisível de utilizador do serviço ou o agente. razão mais comum Olá poderá verificar que a autenticação Olá ACS falhou. Uma causa possível para falha de Olá é que existem problemas com a configuração de servidor NTP Olá e hora no dispositivo Olá não está definida corretamente. |Corrija o tempo de Olá (se existirem problemas) e, em seguida, repita a operação de registo de Olá. Se utilizar Olá Set HcsSystem - fuso horário comando tooadjust Olá fuso horário, capitalize cada palavra Olá fuso horário (por exemplo "Hora padrão do Pacífico").  Se o problema persistir, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md) para passos seguintes. |
| 9 |Aviso: Não foi possível activar o dispositivo de Olá. O administrador do dispositivo e as palavras-passe do Snapshot Manager do StorSimple não foram alteradas. |Se o registo de Olá falhar, o administrador de dispositivos de Olá e palavras-passe do Snapshot Manager do StorSimple não são alteradas. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Ferramentas para resolução de problemas de implementações do StorSimple
StorSimple inclui várias ferramentas que pode ser utilizado tootroubleshoot solução StorSimple. Estas incluem:

* Pacotes de suporte e registos de dispositivos 
* Cmdlets concebidos especificamente para resolução de problemas 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Suportar pacotes e registos de dispositivos disponíveis para resolução de problemas
Um pacote de suporte contém todos os registos relevantes Olá que podem ajudar a equipa do Microsoft Support Olá com a resolução de problemas do dispositivo. Pode utilizar o Windows PowerShell para StorSimple toogenerate um pacote de suporte encriptado, em seguida, pode partilhar com o suporte técnico.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>pacote de suporte de tooview Olá registos ou o conteúdo Olá Olá
1. Utilizar o Windows PowerShell para StorSimple toogenerate um pacote de suporte, tal como descrito no [criar e gerir um pacote de suporte](storsimple-create-manage-support-package.md).
2. Transferir Olá [script de desencriptação](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localmente no computador cliente.
3. Utilize esta opção [procedimento passo a passo](storsimple-create-manage-support-package.md#edit-a-support-package) tooopen e desencriptar Olá suporte do pacote.
4. Olá desencriptar registos estão no formato de etw/etvx de pacote de suporte. Pode efetuar Olá tooview passos a seguir estes ficheiros no Visualizador de eventos do Windows:
   
   1. Executar Olá **eventvwr** comando no cliente Windows. Esta ação iniciará Olá Visualizador de eventos.
   2. No Olá **ações** painel, clique em **registo guardado abertos** e ficheiros de registo toohello de ponto no formato etvx/etw (pacote de suporte de Olá). Agora, pode ver o ficheiro de Olá. Depois de abrir o ficheiro de Olá, pode com o botão direito e guarde o ficheiro de Olá como texto.
      
      > [!IMPORTANT]
      > Também pode utilizar Olá **Get-WinEvent** cmdlet tooopen estes ficheiros no Windows PowerShell. Para obter mais informações, consulte [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) no Olá documentação de referência de cmdlet do Windows PowerShell.
      > 
      > 
5. Quando abrir Olá registos no Visualizador de eventos, procure Olá seguintes registos que contêm problemas relacionados com toohello a configuração do dispositivo:
   
   * hcs_pfconfig/Operational registo
   * hcs_pfconfig/configuração
6. Nos ficheiros de registo de Olá, procure cadeias cmdlets relacionados toohello chamados pelo Assistente de configuração de Olá. Consulte [processo do Assistente de configuração de hora da primeira](#first-time-setup-wizard-process) para obter uma lista destes cmdlets. 
7. Se não for capaz de toofigure causa Olá problema Olá, pode [contacte a Microsoft Support](storsimple-contact-microsoft-support.md) para passos seguintes. Olá utilize os passos em [criar um pedido de suporte](storsimple-contact-microsoft-support.md#create-a-support-request) quando contactar o Support da Microsoft para obter assistência.

## <a name="cmdlets-available-for-troubleshooting"></a>Cmdlets disponíveis para resolução de problemas
Utilize Olá os seguintes erros de conectividade de toodetect de cmdlets do Windows PowerShell.

* `Get-NetAdapter`: Utilize este cmdlet toodetect Olá estado de funcionamento de interfaces de rede. 
* `Test-Connection`: Utilize este cmdlet toocheck Olá conectividade de rede dentro e fora da rede Olá.
* `Test-HcsmConnection`: Utilize este cmdlet toocheck Olá a conectividade num dispositivo registado com êxito.

Se estiver a executar atualização 1 no dispositivo StorSimple, Olá os seguintes cmdlets diagnóstico também está disponível.

* `Sync-HcsTime`: Utilize o cmdlet toodisplay dispositivo de momento e forçar uma sincronização de hora com o servidor NTP Olá.
* `Enable-HcsPing`e `Disable-HcsPing`: utilizar estes cmdlets tooallow Olá anfitriões tooping Olá as interfaces de rede no dispositivo StorSimple. Por predefinição, as interfaces de rede do StorSimple Olá responde a pedidos de tooping.
* `Trace-HcsRoute`: Utilize este cmdlet como uma ferramenta de rastreio de rota. Envia o router de tooeach de pacotes no destino final do Olá forma tooa durante um período de tempo e, em seguida, calcula os resultados com base nos pacotes hello a devolvidos por cada hop. Uma vez que `Trace-HcsRoute` mostra o grau de Olá de perda de pacotes em qualquer router especificado ou a ligação, pode identificar os routers ou ligações poderão estar a causar problemas de rede. 
* `Get-HcsRoutingTable`: Utilize este cmdlet toodisplay Olá local tabela de encaminhamento IP.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Resolver problemas com o cmdlet Get-NetAdapter de Olá
Quando configurar as interfaces de rede para uma implementação de tempo do primeiro dispositivo, estado do hardware Olá não está disponível no Olá da IU do serviço StorSimple Manager porque o dispositivo de Olá ainda não está registado com o serviço de Olá. Além disso, página de estado do Hardware Olá poderá não sempre corretamente refletir Olá estado do dispositivo Olá, especialmente se existirem problemas que afetam a sincronização de serviço. Nestas situações, pode utilizar Olá `Get-NetAdapter` cmdlet toodetermine Olá funcionamento e o estado das suas interfaces de rede.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee uma lista de todos os adaptadores de rede de Olá no seu dispositivo
1. Inicie o Windows PowerShell para StorSimple e, em seguida, escreva `Get-NetAdapter`. 
2. Utilizar o resultado Olá Olá `Get-NetAdapter` cmdlet e Olá seguir diretrizes toounderstand Olá estado da sua interface de rede.
   
   * Se a interface de Olá é bom estado de funcionamento e ativada, Olá **ifIndex** estado é mostrado como **segurança**.
   * Se a interface de Olá está em bom estado, mas não é fisicamente ligado (através de um cabo de rede), Olá **ifIndex** é mostrado como **desativado**.
   * Se a interface de Olá está em bom estado, mas não ativado, Olá **ifIndex** estado é mostrado como **NotPresent**.
   * Se a interface de Olá não existe, se não for apresentada nesta lista. Olá serviço StorSimple Manager IU ainda aparecer nesta interface em estado de falha.

Para obter mais informações sobre como toouse este cmdlet, aceda demasiado[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) no Olá referência de cmdlets do Windows PowerShell. 

Olá secções seguintes mostram os exemplos de saída de Olá `Get-NetAdapter` cmdlet. 

 Estes exemplos, o controlador 0 foi controlador passivo Olá e foi configurado da seguinte forma:

* DATA 0, 1 de dados, dados 2 e rede de dados 3 interfaces existiam no dispositivo Olá.
* DADOS 4 e 5 dados placas de interface de rede não estavam presentes; Por conseguinte, não estão listadas na saída de Olá.
* DATA 0 foi ativada.

O controlador 1 foi controlador ativo Olá e foi configurado da seguinte forma:

* DATA 0, 1 de dados, dados 2, dados 3, 4 de dados e rede de dados 5 interfaces existiam no dispositivo Olá.
* DATA 0 foi ativada.

**Saída exemplo – controlador 0**

Olá que se segue saída Olá do controlador 0 (controlador de passivo Olá). DADOS 1, dados 2 e 3 de dados não estão ligados. DADOS 4 e 5 de dados não estão listadas porque não estão presentes no dispositivo Olá. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Saída exemplo – controlador 1**

Olá que se segue saída Olá do controlador 1 (controlador ativo Olá). Apenas Olá dados 0 interface de rede no dispositivo Olá está configurada e a funcionar.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Resolver problemas com o cmdlet Test-Connection de Olá
Pode utilizar Olá `Test-Connection` cmdlet toodetermine se o dispositivo StorSimple pode ligar toohello fora da rede. Se todos os parâmetros de rede da Olá, incluindo Olá DNS, estão configurados corretamente no Assistente de configuração de Olá, pode utilizar Olá `Test-Connection` cmdlet tooping um endereço conhecido fora da rede Olá, tais como outlook.com. 

Deve ativar problemas de conectividade de tootroubleshoot ping com este cmdlet se ping está desativado.

Consulte Olá seguintes exemplos de saída de Olá `Test-Connection` cmdlet. 

> [!NOTE]
> Exemplo de primeiro Olá, o dispositivo Olá está configurado com um DNS incorreto. Exemplo de segundo Olá, Olá DNS está correta.
> 
> 

**Saída exemplo – DNS incorretas**

No seguinte exemplo de Olá, não há nenhuma saída para endereços IPV4 e IPV6 Olá, que indica que Olá que DNS não está resolvido. Isto significa que não existe nenhum toohello conectividade fora da rede e necessita de um DNS correto toobe fornecido. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Saída exemplo – DNS correto**

No seguinte exemplo de Olá, Olá DNS devolve Olá endereço IPV4, indicando que Olá que DNS está configurado corretamente. Isto confirma que há toohello conectividade fora da rede. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Resolver problemas com o cmdlet Test-HcsmConnection de Olá
Olá utilize `Test-HcsmConnection` cmdlet para um dispositivo que já se encontra ligado tooand registado no serviço StorSimple Manager. Este cmdlet ajuda-o a verificar a conectividade de Olá entre um dispositivo registado e Olá correspondente serviço StorSimple Manager. Pode executar este comando no Windows PowerShell para StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>toorun Olá Test-HcsmConnection cmdlet
1. Certifique-se de que o dispositivo Olá está registado.
2. Verifique o estado do dispositivo Olá. Se o dispositivo de Olá está desativado no modo de manutenção ou offline, poderá ver Olá seguintes erros: 
   
   * ErrorCode.CiSDeviceDecommissioned – Isto indica que o dispositivo Olá está desativado.
   * ErrorCode.DeviceNotReady – Isto indica que o dispositivo Olá está no modo de manutenção.
   * ErrorCode.DeviceNotReady – Isto indica que o dispositivo Olá não está online.
3. Certifique-se de que Olá serviço StorSimple Manager está em execução (utilizar Olá [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet). Se o serviço de Olá não está em execução, poderá ver Olá seguintes erros:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError – Isto indica que ocorreu uma exceção quando executou Get ClusterResource.
4. Verifique o token de serviço de controlo de acesso (ACS) de Olá. Se, emite uma exceção da web, poderá ser Olá resultado de um problema de gateway, uma autenticação de proxy em falta, um DNS incorreto ou uma falha de autenticação. Poderá ver Olá seguintes erros:
   
   * ErrorCode.CiSApplianceGateway – Isto indica uma exceção de HttpStatusCode.BadGateway: serviço de resolução de nome de Olá não foi possível resolver o nome de anfitrião Olá. 
   * ErrorCode.CiSApplianceProxy – Isto indica uma exceção de HttpStatusCode.ProxyAuthenticationRequired (código de estado HTTP 407): o cliente de Olá não conseguiu autenticar com o servidor de proxy de Olá. 
   * ErrorCode.CiSApplianceDNSError – Isto indica uma exceção de WebExceptionStatus.NameResolutionFailure: serviço de resolução de nome de Olá não foi possível resolver o nome de anfitrião Olá.
   * ErrorCode.CiSApplianceACSError – Isto indica que o serviço de Olá devolveu um erro de autenticação, mas não existe conectividade.
     
     Se não inicia uma exceção da web, verifique a existência de ErrorCode.CiSApplianceFailure. Isto indica que aplicação Olá falhou.
5. Verifique a conectividade de serviço de nuvem Olá. Se o serviço de Olá emite uma exceção da web, poderá ver Olá seguintes erros:
   
   * ErrorCode.CiSApplianceGateway – Isto indica uma exceção de HttpStatusCode.BadGateway: um servidor proxy intermédio recebeu um pedido incorreto de outro proxy ou de servidor original Olá.
   * ErrorCode.CiSApplianceProxy – Isto indica uma exceção de HttpStatusCode.ProxyAuthenticationRequired (código de estado HTTP 407): o cliente de Olá não conseguiu autenticar com o servidor de proxy de Olá. 
   * ErrorCode.CiSApplianceDNSError – Isto indica uma exceção de WebExceptionStatus.NameResolutionFailure: serviço de resolução de nome de Olá não foi possível resolver o nome de anfitrião Olá.
   * ErrorCode.CiSApplianceACSError – Isto indica que o serviço de Olá devolveu um erro de autenticação, mas não existe conectividade.
     
     Se não inicia uma exceção da web, verifique a existência de ErrorCode.CiSApplianceSaasServiceError. Isto indica um problema com Olá serviço StorSimple Manager.
6. Verifique a conectividade do Service Bus do Azure. ErrorCode.CiSApplianceServiceBusError indica que o dispositivo Olá não é possível ligar toohello Service Bus.

Olá, ficheiros de registo CiSCommandletLog0Curr.errlog e CiSAgentsvc0Curr.errlog terá mais informações, tais como os detalhes da exceção. 

Para obter mais informações sobre como toouse Olá cmdlet, visite demasiado[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) no Olá do Windows PowerShell documentação de referência.

> [!IMPORTANT]
> Pode executar este cmdlet para Olá Active Directory e controlador passivo Olá. 
> 
> 

Consulte Olá seguintes exemplos de saída de Olá `Test-HcsmConnection` cmdlet. 

**Exemplo de saída – dispositivo registado com êxito com a versão do StorSimple (Julho de 2014)**

exemplo de primeiro Olá é de um dispositivo que está registado com êxito com Olá serviço StorSimple Manager e tem sem problemas de conectividade. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Saída de exemplo – dispositivo registado com êxito com o Update 1 do StorSimple**

Se estiver a executar o Update 1 no dispositivo StorSimple, não terá toorun-lo com o comutador verboso Olá.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Exemplo de saída – offline dispositivos a executar a versão do StorSimple (Julho de 2014)**

Este exemplo está a partir de um dispositivo que tem um Estado de **Offline** no Olá portal clássico do Azure.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

dispositivo Olá não conseguiu estabelecer ligação utilizando a configuração de proxy web de Olá atual. Isto pode ser um problema com a configuração do proxy web Olá ou um problema de conectividade de rede. Neste caso, certifique-se de que as definições de proxy web estão corretas e os servidores de proxy web estão online e acessível. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Resolver problemas com o cmdlet de sincronização HcsTime Olá
Utilize o cmdlet toodisplay Olá dispositivo de momento. Se a hora de dispositivo Olá tem um desvio com o servidor NTP Olá, em seguida, pode utilizar este cmdlet tooforce-sincronizar a hora de Olá com o seu servidor NTP. Se o desvio Olá entre o dispositivo de Olá e servidor NTP for superior a cinco minutos, irá ver um aviso. Se Olá desvio excede 15 minutos, o dispositivo de Olá será fique offline. Pode continuar a utilizar este cmdlet tooforce uma sincronização de hora. No entanto, se Olá desvio excede 15 horas, em seguida, não será capaz de sincronização de tooforce Olá momento e será apresentada uma mensagem de erro.

**Saída de exemplo – utilizando HcsTime de sincronização de sincronização de hora forçada**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Resolver problemas com Olá HcsPing ativar e desativar HcsPing cmdlets
Utilize estas tooensure de cmdlets que interfaces de rede Olá no seu dispositivo respondem a pedidos de ping tooICMP. Por predefinição, as interfaces de rede do StorSimple Olá não responder tooping pedidos. Utilizar este cmdlet é Olá tooknow de forma mais fácil se o dispositivo está online e acessível.  

**Saída de exemplo – HcsPing ativar e desativar HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Resolver problemas com o cmdlet de rastreio HcsRoute Olá
Utilize este cmdlet como uma ferramenta de rastreio de rota. Envia o router de tooeach de pacotes no destino final do Olá forma tooa durante um período de tempo e, em seguida, calcula os resultados com base nos pacotes hello a devolvidos por cada hop. Porque o cmdlet Olá mostra o grau de Olá de perda de pacotes em qualquer router especificado ou a ligação, pode identificar os routers ou ligações poderão estar a causar problemas de rede.

**Saída de exemplo que mostra como tootrace Olá rota de um pacote com o rastreio HcsRoute**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Resolver problemas com o cmdlet Get-HcsRoutingTable de Olá
Utilize esta tabela de encaminhamento de Olá do cmdlet tooview para o dispositivo StorSimple. Uma tabela de encaminhamento é um conjunto de regras que podem ajudar a determinar onde serão direcionados pacotes de dados estiverem em deslocação através de uma rede de Internet Protocol (IP). 

Olá tabela de encaminhamento apresenta Olá interfaces e hello que rotas Olá dados toohello especificado gateway redes. Também proporciona métrica de encaminhamento Olá que é decisor Olá para Olá caminho tomado tooreach um destino específico. Olá inferior Olá encaminhamento métrica, Olá Olá preferência superior. 

Por exemplo, se tiver 2 interfaces de rede, dados 2 e dados 3, toohello ligado à Internet. Se as métricas de encaminhamento Olá para dados 2 e dados 3 15 e 261 respetivamente, em seguida, 2 de dados com a métrica de encaminhamento inferior Olá é interface preferida Olá utilizada tooreach Olá Internet.

Se estiver a executar atualização 1 no dispositivo StorSimple, o seu interface rede DATA 0 possui preferência mais elevada do Olá para o tráfego de nuvem Olá. Isto implica que, mesmo se existirem outras interfaces ativado para a nuvem, o tráfego de nuvem de Olá seria encaminhado através de dados 0. 

Se executar Olá `Get-HcsRoutingTable` cmdlet sem especificar quaisquer parâmetros (como Olá seguinte exemplo mostra), Olá cmdlet irá tabelas de encaminhamento IPv4 e IPv6 de saída. Em alternativa, pode especificar `Get-HcsRoutingTable -IPv4` ou `Get-HcsRoutingTable -IPv6` tooget uma tabela de encaminhamento relevante.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Passo a passo exemplo de resolução de problemas do StorSimple
Olá exemplo seguinte mostra passo a passo de resolução de problemas de uma implementação do StorSimple. Cenário de exemplo de Olá, o registo de dispositivos irá falhar com uma mensagem de erro a indicar que as definições de rede Olá ou nome DNS Olá está incorreto.

Olá mensagem de erro devolvida é:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Erro de Olá pode ser causado por Olá seguinte:

* Instalação de hardware incorreto
* Interfaces de rede defeituoso
* Endereço IP incorreto, máscara de sub-rede, gateway, servidor DNS primário ou web proxy
* Chave de registo incorreto
* Definições de firewall incorreta

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate e corrigir problemas de registo de dispositivo Olá
1. Verifique a configuração do dispositivo: no controlador ativo Olá, execute `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Assistente de configuração de Olá tem de executar no controlador ativo Olá. tooverify que estão ligados toohello Active Directory controlador, de olhos a faixa de Olá apresentado na consola de série de Olá. faixa de Olá indica se encontram ligado toocontroller 0 ou 1 do controlador e, se o controlador de Olá é ativas ou passivas. Para mais informações, visite demasiado[identificar um controlador de Active Directory no seu dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Certifique-se de que o dispositivo Olá é instalou os cabos do corretamente: Verifique rede Olá cablagem no dispositivo Olá plane novamente. Olá cablagem é o modelo do dispositivo toohello específico. Para mais informações, visite demasiado[instalar o seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md) ou [instalar o seu dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Se estiver a utilizar portas de rede 10 GbE, terá de Olá toouse fornecido adaptadores QSFP SFP e cabos SFP. Para obter mais informações, consulte Olá [lista de cabos, comutadores e transcetores recomendados para as portas do Olá 10 GbE](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Verifique o estado de funcionamento de Olá Olá da interface de rede:
   
   * Utilize Olá Get-NetAdapter cmdlet toodetect Olá estado de funcionamento das interfaces de rede Olá para DATA 0. 
   * Se a ligação de Olá não está a funcionar, Olá **ifindex** estado irá indicar essa interface de Olá está inativo. Em seguida, irá necessitar de ligação de rede de Olá toocheck de dispositivo do Olá porta toohello e toohello comutador. Também terá de toorule saída cabos incorretos. 
   * Se suspeitar que Olá dados 0 porta no controlador ativo Olá falhou, pode confirmar isto, ligando-se a porta de dados 0 toohello no controlador 1. tooconfirm, desligue o cabo de rede Olá Olá back of dispositivo Olá do controlador 0, ligue o cabo de Olá toocontroller 1 e, em seguida, volte a executar o cmdlet de Olá Get NetAdapter. 
     Se Olá dados 0 porta num controlador de falha, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md) para passos seguintes. Poderá ter de controlador de Olá tooreplace no seu sistema.
4. Certifique-se de comutador de toohello Olá conectividade:
   
   * Certifique-se de que as interfaces de rede 0 de dados no controlador 0 e o controlador 1 na sua inclusão principal estão em Olá mesma sub-rede. 
   * Verificação Olá hub ou do router. Normalmente, deve ligar os dois controladores toohello mesmo hub ou do router. 
   * Certifique-se de que os comutadores de Olá utiliza para a ligação de Olá dados 0 para ambos os controladores no Olá mesma vLAN.
5. Eliminar quaisquer erros de utilizador:
   
   * Executar novamente o Assistente de configuração de Olá (executar **Invoke-HcsSetupWizard**) e introduza Olá novamente valores toomake se existirem erros. 
   * Verifique o registo de Olá chave utilizada. Olá a mesma chave de registo pode ser utilizado tooconnect vários dispositivos tooa serviço StorSimple Manager. Utilize o procedimento Olá [chave de registo do serviço de Olá Get](storsimple-manage-service.md#get-the-service-registration-key) tooensure que está a utilizar Olá chave de registo correto.
     
     > [!IMPORTANT]
     > Se tiver múltiplos serviços em execução, terá de tooensure essa chave de registo Olá para serviço apropriado Olá é o dispositivo de Olá tooregister utilizados. Se registou um dispositivo com o serviço StorSimple Manager errado Olá, terá de demasiado[contacte a Microsoft Support](storsimple-contact-microsoft-support.md) para passos seguintes. Se possuir uma reposição de fábrica do dispositivo Olá (o que poderá resultar na perda de dados) tooperform toothen ligue-o serviço toohello pretendido.
     > 
     > 
6. Utilize Olá Test-Connection cmdlet tooverify tiver conectividade toohello fora da rede. Para mais informações, visite demasiado[resolver problemas com o cmdlet Olá Test-Connection](#troubleshoot-with-the-test-connection-cmdlet).
7. Verifique a existência de interferências de firewall. Se tiver verificado que Olá virtual definições de IP (VIP), sub-rede, gateway e DNS estão corretas e continuar a ver problemas de conectividade, em seguida, é possível que a firewall está a bloquear a comunicação entre o dispositivo e Olá fora da rede. É necessário tooensure que as portas 80 e 443 estão disponíveis no dispositivo StorSimple para comunicação de saída. Para obter mais informações, consulte [requisitos de rede para o dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Consulte os registos de Olá. Aceda demasiado[suportar pacotes e registos de dispositivos disponíveis para resolução de problemas](#support-packages-and-device-logs-available-for-troubleshooting).
9. Se hello passos anteriores não resolver o problema de Olá, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md) para obter assistência.

## <a name="next-steps"></a>Passos seguintes
[Saiba como tootroubleshoot um dispositivo operacional](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
