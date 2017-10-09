---
title: "aaaSet segurança proxy web para um dispositivo StorSimple | Microsoft Docs"
description: "Saiba como toouse do Windows PowerShell para StorSimple tooconfigure web as definições de proxy para o dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Configurar o proxy web para o dispositivo StorSimple
## <a name="overview"></a>Descrição geral
Este tutorial descreve como toouse do Windows PowerShell para StorSimple tooconfigure e vista web as definições de proxy para o dispositivo StorSimple. as definições de proxy de web Hello são utilizadas por dispositivo do StorSimple Olá ao comunicar com a nuvem de Olá. Um servidor proxy web é utilizada tooadd outra camada de segurança, filtrar o conteúdo, os requisitos de largura de banda tooease em cache ou inclusivamente ajudar Analytics.

Web proxy é uma configuração opcional para o dispositivo StorSimple. Pode configurar o proxy de web apenas através do Windows PowerShell para StorSimple. configuração de Olá é um processo de dois passos da seguinte forma:

1. Configurar definições de proxy web através do Assistente de configuração de Olá ou o Windows PowerShell para StorSimple cmdlets primeiro.
2. Em seguida, ativar definições de proxy de web do Olá configurado através do Windows PowerShell para StorSimple cmdlets.

Após a conclusão da configuração do proxy web Olá, pode ver as definições de proxy de web Olá configurada no serviço do Microsoft Azure StorSimple Manager de Olá e Olá do Windows PowerShell para StorSimple. 

Depois de ler este tutorial, será capaz de:

* Configurar o web proxy utilizando o Assistente de configuração e cmdlets
* Ativar o proxy da web através de cmdlets
* Ver as definições de proxy web no Olá portal clássico do Azure
* Resolver erros durante a configuração do proxy web

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configurar o proxy web através do Windows PowerShell para StorSimple
Utilização de uma Olá as definições de proxy de web tooconfigure os seguintes:

* Configurar assistente tooguide Olá passos de configuração.
* Cmdlets do Windows PowerShell para StorSimple.

Cada um destes métodos é abordada em Olá secções a seguir.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Configurar o proxy web através do Assistente de configuração de Olá
Pode utilizar tooguide de Assistente de configuração de Olá, através de Olá passos de configuração do proxy web. Efetue Olá proxy de web de tooconfigure passos a seguir no seu dispositivo.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>proxy de web tooconfigure através do Assistente de configuração de Olá
1. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total** e fornecer Olá **palavra-passe de administrador do dispositivo**. Seguinte Olá de tipo de comando toostart uma sessão de Assistente de configuração:
   
    `Invoke-HcsSetupWizard`
2. Se este for Olá pela primeira vez que utiliza o Assistente de configuração de Olá para registo de dispositivos, precisa de tooconfigure todas as definições de rede de Olá necessário até chegar à configuração do proxy web Olá. Se o dispositivo já está registado, pode aceitar todas as definições de rede de Olá configurado até chegar à configuração do proxy web Olá. No Assistente de configuração de Olá, quando pedido tooconfigure web as definições de proxy, introduza **Sim**.
3. Para Olá **URL do Web Proxy**, especifique o endereço IP Olá ou Olá o nome de domínio completamente qualificado (FQDN) do seu web proxy servidor e Olá número da porta TCP que gostaria de toouse seu dispositivo quando comunica com a nuvem de Olá. Utilize Olá seguinte formato:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Por predefinição, é especificado o número da porta TCP 8080.
4. Escolha o tipo de autenticação de Olá como **NTLM**, **básico**, ou **nenhum**. Qual é o básico Olá authentication menos segura para a configuração de servidor de proxy de Olá. NT LAN Manager (NTLM) é um protocolo de autenticação altamente seguro e complexas que utiliza um sistema de mensagens de três vias (por vezes, quatro se for necessária a integridade adicional) tooauthenticate um utilizador. a autenticação de predefinição Olá é NTLM. Para obter mais informações, consulte [básico](http://hc.apache.org/httpclient-3.x/authentication.html) e [autenticação NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Olá serviço StorSimple Manager, gráficos de monitorização de dispositivos de Olá não funcionam quando básica ou autenticação de NTLM está ativada na configuração de servidor de proxy Olá para dispositivo Olá. Para Olá monitorização toowork gráficos, terá de tooensure que a autenticação está definida tooNONE.**
   > 
   > 
5. Se estiver a utilizar a autenticação, forneça um **nome de utilizador de Proxy de Web** e um **palavra-passe do Web Proxy**. Também terá de palavra-passe do tooconfirm Olá.
   
    ![Configurar o Web Proxy Device1 do StorSimple](./media/storsimple-configure-web-proxy/IC751830.png)

Se estiver a registar o dispositivo para Olá pela primeira vez, continue com o registo de Olá. Se o dispositivo já estava registado, o Assistente de Olá será fechada. Olá configurado configurações serão guardadas.

Web proxy será agora também ativado. Pode ignorar Olá [ativar o web proxy](#enable-web-proxy) passo e aceda diretamente demasiado[ver as definições de proxy web no portal clássico do Azure de Olá](#view-web-proxy-settings-in-the-azure-classic-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configurar o proxy web através do Windows PowerShell para StorSimple cmdlets
Definições de proxy uma maneira alternativa tooconfigure web é através de Olá do Windows PowerShell para StorSimple cmdlets. Efetue Olá proxy de web de tooconfigure passos a seguir.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>proxy de web tooconfigure através de cmdlets
1. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**. Quando solicitado, forneça Olá **palavra-passe de administrador do dispositivo**. palavra-passe predefinida de Olá é `Password1`.
2. Na linha de comandos Olá, escreva:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Forneça e confirme a palavra-passe Olá quando lhe for pedido, conforme mostrado abaixo.
   
    ![Configurar o Web Proxy Device3 do StorSimple](./media/storsimple-configure-web-proxy/IC751831.png)

proxy de web de Olá está agora configurado e tem de toobe ativada.

## <a name="enable-web-proxy"></a>Ativar o proxy da web
Web proxy está desativado por predefinição. Depois de configurar as definições de proxy de web Olá no dispositivo StorSimple, precisa toouse Olá do Windows PowerShell para StorSimple tooenable Olá web as definições de proxy.

> [!NOTE]
> **Este passo não será necessário se tiver utilizado o proxy de web de tooconfigure de Assistente de configuração de Olá. Web proxy automaticamente está ativado por predefinição, depois de uma sessão de Assistente de configuração.**
> 
> 

Execute os seguintes passos no Windows PowerShell para StorSimple tooenable proxy da web no seu dispositivo de Olá:

#### <a name="tooenable-web-proxy"></a>proxy de web tooenable
1. No menu da consola de série de Olá, selecione a opção 1, **iniciar sessão com acesso total**. Quando solicitado, forneça Olá **palavra-passe de administrador do dispositivo**. palavra-passe predefinida de Olá é `Password1`.
2. Na linha de comandos Olá, escreva:
   
    `Enable-HcsWebProxy`
   
    Agora ativou a configuração do proxy web Olá no dispositivo StorSimple.
   
    ![Configurar o Web Proxy Device4 do StorSimple](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>Ver as definições de proxy web no Olá portal clássico do Azure
as definições de proxy de web de Olá são configuradas através da interface do Windows PowerShell Olá e não é possível ser alteradas a partir do portal clássico Olá. No entanto, pode ver estas definições configuradas no portal clássico Olá. Efetue Olá proxy de web de tooview passos a seguir.

#### <a name="tooview-web-proxy-settings"></a>definições de proxy de web tooview
1. Navegue demasiado**serviço StorSimple Manager > dispositivos**. Selecione e clique no dispositivo e, em seguida, aceda demasiado**configurar**.
2. Desloque para baixo no Olá **configurar** página demasiado**as definições de proxy de Web** secção. Pode ver as definições de proxy de web Olá configurada no dispositivo StorSimple, conforme mostrado abaixo.
   
    ![Vista Web Proxy no Portal de gestão](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>Erros durante a configuração do proxy web
Se as definições de proxy de web Olá foram configuradas incorretamente, mensagens de erro será apresentada toohello utilizador no Windows PowerShell para StorSimple. Olá, a tabela seguinte explica alguns destas mensagens de erro, as causas prováveis e ações recomendadas.

| Série não. | Erro HRESULT código | Causa possível | Ação recomendada |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Comando é executado a partir do controlador passivo Olá e não é possível toocommunicate com controlador ativo Olá. |Execute o comando de Olá no controlador de Olá Active Directory. comando de Olá toorun do controlador passivo Olá, será precisa de conectividade de Olá toofix do controlador de tooactive passiva. Precisa de tooengage Support da Microsoft se este conectividade está danificada. |
| 2. |0x800710dd - o identificador da operação Olá não é válido |Definições de proxy não são suportadas no dispositivo virtual StorSimple. |Definições de proxy não são suportadas no dispositivo virtual StorSimple. Só podem ser configurados num dispositivo físico StorSimple. |
| 3. |0x80070057 - parâmetro inválido |Um dos parâmetros de Olá fornecidos para as definições de proxy Olá não é válido. |Olá URI não é fornecido no formato correto. Utilize Olá seguinte formato:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706BA - servidor de RPC não está disponível |causa de raiz de Olá é uma das seguintes Olá:</br></br>Cluster não está operacional.</br></br>Serviço de DataPath não está em execução.</br></br>comando Olá é executado a partir do controlador passivo e não é capaz de toocommunicate com controlador ativo Olá. |. Levar a cabo tooensure Support da Microsoft que Olá cluster está operacional e datapath serviço está em execução.</br></br>Execute o comando de Olá do controlador ativo Olá. Se pretender que o comando de Olá toorun do controlador passivo Olá, terá de tooensure controlador passivo Olá consegue comunicar com o controlador Olá de Active Directory. Precisa de tooengage Support da Microsoft se este conectividade está danificada. |
| 5. |0x800706be - falha de chamada RPC |Cluster está inativo. |. Levar a cabo tooensure Support da Microsoft que Olá cluster está a funcionar. |
| 6. |0x8007138f - recurso de cluster não encontrado |Recurso de cluster do serviço de plataforma não foi encontrado. Isto pode acontecer quando a instalação de Olá não estava correta. |Poderá ser necessário tooperform uma reposição de fábrica no dispositivo. Poderá ser necessário toocreate um recurso de plataforma. Contacte Support da Microsoft para os passos seguintes. |
| 7. |0x8007138c - recurso de cluster não online |Plataforma ou datapath recursos do cluster não estão online. |Contacto Microsoft Support toohelp Certifique-se que o recurso de serviço de plataforma e datapath Olá estão online. |

> [!NOTE]
> * Não é exaustiva Olá acima lista de mensagens de erro. 
> * As definições de proxy de tooweb relacionados erros não serão apresentadas na Olá portal clássico do Azure no serviço StorSimple Manager. Se houver um problema com o web proxy depois de concluída a configuração de Olá, estado do dispositivo Olá mudará demasiado**Offline** no portal clássico Olá. |
> 
> 

## <a name="next-steps"></a>Passos Seguintes
* Se ocorrer algum problema ao implementar o seu dispositivo ou configurar as definições de proxy web, consulte demasiado[resolver problemas relacionados com a implementação do dispositivo StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn como toouse Olá serviço StorSimple Manager, aceda demasiado[utilize Olá tooadminister de serviço StorSimple Manager, o dispositivo StorSimple](storsimple-manager-service-administration.md).

