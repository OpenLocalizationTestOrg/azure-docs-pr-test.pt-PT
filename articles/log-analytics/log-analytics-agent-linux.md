---
title: aaaConnect tooOperations os computadores com Linux Management Suite (OMS) | Microsoft Docs
description: "Este artigo descreve como os computadores com Linux tooconnect alojada no Azure, outros cloud ou o tooOMS no local utilizando Olá agente do OMS para Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: cb4fc671d0678f9fadc689c6ba7d719213aa61b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toooperations-management-suite-oms"></a>Ligar o seu tooOperations de computadores com Linux Management Suite (OMS) 

Com o Microsoft Operations Management Suite (OMS), pode recolher e atuar sobre dados gerados a partir de computadores com Linux e soluções de contentor como Docker, que reside no seu centro de dados no local, como servidores físicos ou máquinas virtuais, máquinas virtuais num serviço alojado na nuvem como Amazon Web Services (AWS) ou o Microsoft Azure. Também pode utilizar as soluções de gestão disponíveis na OMS, tais como controlo de alterações, as alterações de configuração de tooidentify, e tooproactively de atualizações de software do gestão de atualizações toomanage gerir Olá ciclo de vida das suas VMs do Linux. 

Olá agente do OMS Linux comunica saída com Olá serviço OMS através da porta TCP 443, e, se o computador de Olá se liga toocommunicate de servidor de firewall ou proxy tooa através do Olá Internet, reveja [configurar o agente de Olá para utilização com um proxy HTTP servidor ou Gateway do OMS](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) toounderstand que configuração é alterada, será necessário toobe aplicada.  Se estiver a monitorizar o computador de Olá com o System Center 2016 - Operations Manager ou do Operations Manager 2012 R2, pode ser multihomed com Olá OMS do serviço toocollect a dados e o serviço de reencaminhamento toohello e ainda ser monitorizado pelo Operations Manager.  Computadores com Linux monitorizados por um grupo de gestão do Operations Manager que está integrado com o OMS não receber a configuração de origens de dados e reencaminhar recolhidos dados através do grupo de gestão Olá.  agente do OMS Olá não pode ser configurado tooreport toomore a uma área de trabalho.  

Se as políticas de segurança de TI não permitir que os computadores no seu toohello tooconnect de rede à Internet, o agente de Olá pode ser configurado tooconnect toohello OMS Gateway tooreceive as informações de configuração e enviar os dados recolhidos, consoante a solução Olá que tiver ativado. Para obter mais informações e passos sobre como tooconfigure toocommunicate o agente do OMS Linux através do serviço OMS toohello um Gateway do OMS, consulte o artigo [ligar tooOMS de computadores utilizando Olá OMS Gateway](log-analytics-oms-gateway.md).  

Olá diagrama seguinte ilustra ligação Olá entre computadores com Linux geridos por agente Olá e OMS, incluindo direção Olá e portas.

![comunicação do agente direta com diagrama do OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a>Requisitos de sistema
Antes de começar, reveja Olá tooverify detalhes cumpre os pré-requisitos de Olá a seguir.

### <a name="supported-linux-operating-systems"></a>Sistemas operativos Linux suportados
Olá, seguindo as distribuições do Linux oficialmente é suportada.  No entanto, Olá agente do OMS para Linux também pode executar nos outras distribuições não listadas.

* Amazon Linux 2012.09 too2015.09 (x86/x64)
* CentOS Linux 5, 6 e 7 (x86/x64)
* Oracle Linux 5, 6 e 7 (x86/x64)
* Red Hat Enterprise Linux Server 5, 6 e 7 (x86/x64)
* Debian GNU/Linux 6, 7 e 8 (x86/x64)
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)
* SUSE Linux Enterprise Server 11 e 12 (x86/x64)

### <a name="network"></a>Rede
informações de Olá abaixo proxy Olá de lista e informações de configuração de firewall necessárias para Olá toocommunicate de agente do Linux com o OMS. O tráfego é de saída do seu serviço do rede toohello OMS. 

|Recursos do Agente| Portas |  
|------|---------|  
|*.ods.opinsights.azure.com | Porta 443|   
|*.oms.opinsights.azure.com | Porta 443|   
|*.blob.Core.Windows.NET/ | Porta 443|   
|*.azure-automation.net | Porta 443|  

### <a name="package-requirements"></a>Requisitos do pacote

 **Pacote necessário**   | **Descrição**   | **Versão mínima**
--------------------- | --------------------- | -------------------
Glibc | Biblioteca de C GNU   | 2.5-12 
OpenSSL | Bibliotecas de OpenSSL | 0.9.8E ou 1.0
Curl | cURL web cliente | 7.15.5
Python ctypes | | 
PAM | Módulos de autenticação incorporável | 

> [!NOTE]
>  Rsyslog ou syslog ng é necessária toocollect mensagens syslog. daemon de syslog Olá predefinição na versão 5 do Red Hat Enterprise Linux, CentOS, Oracle Linux versão e (sysklog) não é suportado para a recolha de eventos do syslog. dados de syslog toocollect de nesta versão destes distribuições Olá rsyslog daemon deve ser instalado e configurado tooreplace sysklog, 

agente de Olá inclui vários pacotes. Olá ficheiro versão contém Olá pacotes, disponíveis por pacote de shell Olá em execução com os seguintes `--extract`:

**Pacote** | **Versão** | **Descrição**
----------- | ----------- | --------------
omsagent | 1.4.0 | Olá agente do Operations Management Suite para Linux
omsconfig | 1.1.1 | Agente de configuração para Olá agente do OMS
OMI | 1.2.0 | Abra o Management Infrastructure (OMI) - uma simples de servidor CIM
scx | 1.6.3 | Fornecedores de CIM OMI para as métricas de desempenho do sistema operativo
Apache cimprov | 1.0.1 | Fornecedor para OMI de monitorização do desempenho Apache HTTP Server. Instalado se for detetado Apache HTTP Server.
MySQL cimprov | 1.0.1 | Desempenho do servidor de MySQL monitorização fornecedor para OMI. Instalado se for detetado MySQL/MariaDB servidor.
docker cimprov | 1.0.0 | Fornecedor de docker para OMI. Instalado se for detetado Docker.

### <a name="compatibility-with-system-center-operations-manager"></a>Compatibilidade com o System Center Operations Manager
Olá agente do OMS para Linux partilha binários do agente com o agente do System Center Operations Manager Olá. Se instalar Olá agente do OMS para Linux num sistema atualmente gerido pelo Operations Manager, Olá OMI e SCX pacotes na versão mais recente do Olá computador tooa. Esta versão, Olá OMS e System Center 2016 - agentes do Operations Manager/Operations Manager 2012 R2 para Linux são compatíveis. 

> [!NOTE]
> System Center 2012 SP1 e versões anteriores atualmente não são compatíveis ou suportado com Olá agente do OMS para Linux.<br>
> Se Olá agente do OMS para Linux é computador tooa instalados que não monitorizado pelo Operations Manager e pretende, em seguida, o computador de Olá toomonitor com o Operations Manager, tem de modificar Olá [configuração OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) anterior computador de Olá toodiscovering. **Este passo é *não* necessário se o agente do Operations Manager Olá está instalado antes de Olá agente do OMS para Linux.**

### <a name="system-configuration-changes"></a>Alterações de configuração do sistema
Depois de instalar Olá agente do OMS para pacotes de Linux, hello seguintes alterações de configuração de todo sistema adicionais são aplicadas. Destes artefactos são removidos quando Olá omsagent pacote foi desinstalado.

* Um utilizador sem privilégios com o nome: `omsagent` é criado. Este é Olá conta Olá omsagent daemon é executada como.
* É criado um ficheiro de "incluem" de sudoers em /etc/sudoers.d/omsagent. Autoriza o omsagent toorestart Olá syslog e omsagent daemons. Se o sudo "incluem" diretivas não são suportadas na versão de Olá instalado de sudo, estas entradas são escritas demasiado/etc/sudoers.
* a configuração de syslog Olá é modificado tooforward um subconjunto do agente de toohello de eventos. Para obter mais informações, consulte Olá **configurar recolha de dados** secção abaixo

### <a name="upgrade-from-a-previous-release"></a>Atualizar a partir de uma versão anterior
Atualizar a partir de versões anteriores daquele 1.0.0-47 é suportada nesta versão. Efetuar a instalação de Olá com Olá `--upgrade` comando atualiza todos os componentes do Olá toohello mais recente a versão do agente.

## <a name="installing-hello-agent"></a>Instalar agente Olá

Esta secção descreve como tooinstall Olá agente do OMS para Linux utilizando um bunndle, que contém Debian e RPM pacotes para cada um dos componentes do agente Olá.  Este pode ser instalado diretamente ou extrair pacotes individuais de Olá tooretrieve.  

Primeiro tem do ID da área de trabalho OMS e a chave, o que pode encontrar ao mudar toohello [portal clássico do OMS](https://mms.microsoft.com).  No Olá **descrição geral** página, no menu superior, Olá selecione **definições**e, em seguida, navegue até demasiado**ligado servidores de Sources\Linux**.  Pode ver Olá valor toohello de **ID da área de trabalho** e **chave primária**.  Copie e cole-o no seu editor favorito.    

1. Transferência Olá mais recente [agente do OMS para Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) ou [agente do OMS para Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) a partir do GitHub.  
2. Transferência de Olá pacote adequado (x86 ou x64) tooyour computador Linux utilizando scp/sftp.
3. Instalar o pacote de Olá utilizando Olá `--install` ou `--upgrade` argumento. 

    > [!NOTE]
    > Se estiverem instalados quaisquer pacotes existentes, como quando o agente do System Center Operations Manager Olá para Linux já está instalado, utilize Olá `--upgrade` argumento. tooconnect tooOperations Management Suite durante a instalação, fornecer Olá `-w <WorkspaceID>` e `-s <Shared Key>` parâmetros.


#### <a name="tooinstall-and-onboard-directly"></a>tooinstall e do carregar diretamente
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="tooupgrade-hello-agent-package"></a>pacote de agente de Olá tooupgrade
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="tooinstall-and-onboard-tooa-workspace-in-us-government-cloud"></a>tooinstall e carregar tooa área de trabalho na US Government nuvem
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-hello-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a>Configurar o agente de Olá para utilização com um servidor de proxy HTTP ou Gateway do OMS
Olá agente do OMS para Linux suporta comunicar através de um serviço OMS de toohello do OMS Gateway ou servidor de proxy HTTP ou HTTPS.  Autenticação básica e anónima (nome de utilizador/palavra-passe) é suportada.  

### <a name="proxy-configuration"></a>Configuração de proxy
valor de configuração de proxy Olá tem Olá sintaxe:

`[protocol://][user:password@]proxyhost[:port]`

Propriedade|Descrição
-|-
Protocolo|http ou https
utilizador|Nome de utilizador opcional para a autenticação de proxy
palavra-passe|Palavra-passe opcional para a autenticação de proxy
proxyhost|Endereço ou o FQDN do servidor do proxy de Olá/OMS Gateway
porta|Número de porta opcional para o servidor do proxy de Olá/OMS Gateway

Por exemplo: `http://user01:password@proxy01.contoso.com:8080`

servidor de proxy de Olá pode ser especificado durante a instalação ou ao modificar o ficheiro de configuração de proxy.conf Olá após a instalação.   

### <a name="specify-proxy-configuration-during-installation"></a>Especificar a configuração de proxy durante a instalação
Olá `-p` ou `--proxy` argumento do pacote de instalação de omsagent Olá Especifica toouse de configuração de proxy Olá. 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-hello-proxy-configuration-in-a-file"></a>Definir a configuração de proxy de Olá num ficheiro
configuração de proxy de Olá pode ser definida nos ficheiros de Olá `/etc/opt/microsoft/omsagent/proxy.conf` e `/etc/opt/microsoft/omsagent/conf/proxy.conf `. ficheiros de Olá podem ser criados ou editados diretamente, mas as respetivas permissões tem de ser utilizador omiuser Olá de toogrant atualizado permissão de leitura nos ficheiros de Olá. Por exemplo:
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-hello-proxy-configuration"></a>A remover configuração de proxy de Olá
tooremove uma configuração de proxy definida anteriormente e reverter toodirect conectividade, remova Olá proxy.conf ficheiro:
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a>Integração com o Operations Management Suite
Se uma ID da área de trabalho e a chave não foram fornecidas durante a instalação do pacote Olá, os agentes de Olá tem de estar registado, subsequentemente, com o Operations Management Suite.

### <a name="onboarding-using-hello-command-line"></a>Integração com linha de comandos Olá
Execute Olá omsadmin.sh comando fornecer o id da área de trabalho de Olá e da chave para a sua área de trabalho. Este comando deve ser executado como raiz (com elevação de sudo):
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a>Integração utilizando um ficheiro
1.  Criar ficheiro de Olá `/etc/omsagent-onboard.conf`. ficheiro de Olá tem de ser legível e gravável para a raiz.
`sudo vi /etc/omsagent-onboard.conf`
2.  Inserir Olá seguintes linhas no ficheiro de Olá com o ID e a chave partilhada:

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  Execute Olá tooOMS tooOnboard de comando a seguir:`sudo /opt/microsoft/omsagent/bin/omsadmin.sh`
4.  ficheiro de Olá é eliminado do integração com êxito.

## <a name="enable-hello-oms-agent-for-linux-tooreport-toosystem-center-operations-manager"></a>Ativar Olá agente do OMS para Linux tooreport tooSystem Center Operations Manager
Efetue Olá os seguintes passos tooconfigure Olá agente do OMS para o grupo de gestão do Linux tooreport tooa System Center Operations Manager.  

1. Edite o ficheiro de Olá`/etc/opt/omi/conf/omiserver.conf`
2. Certifique-se de que Olá linha a partir **httpsport =** define a porta de Olá 1270. Tal como:`httpsport=1270`
3. Reinicie o servidor OMI Olá:`sudo /opt/omi/bin/service_control restart`

## <a name="agent-logs"></a>Registos do agente
Olá registos para Olá agente do OMS para Linux pode ser encontrado em: `/var/opt/microsoft/omsagent/<workspace id>/log/` Olá registos para o programa do Olá omsconfig (configuração do agente) pode ser encontrado em: `/var/opt/microsoft/omsconfig/log/` registos de componentes da OMI e SCX Olá (que fornecem dados de métricas de desempenho) podem ser encontrados em:`/var/opt/omi/log/ and /var/opt/microsoft/scx/log`

### <a name="log-rotation-configuration"></a>Registo rotação configuração # #
Olá registo rodar configuração omsagent pode ser encontrada em:`/etc/logrotate.d/omsagent-<workspace id>`

Olá predefinições são: 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-hello-oms-agent-for-linux"></a>Desinstalar o agente do OMS de Olá para Linux
Olá pacotes de agente podem ser desinstaladas através da execução Olá .sh ficheiro com Olá `--purge` argumento, o que remove completamente agente Olá e a respetiva configuração do computador Olá.   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a>Resolução de problemas

### <a name="issue-unable-tooconnect-through-proxy-toooms"></a>Problema: Tooconnect não é possível através do proxy tooOMS

#### <a name="probable-causes"></a>Causas prováveis
* proxy de Olá especificado durante a integração estava incorreta
* pontos finais de serviço do OMS Olá não são whitelistested no seu centro de dados 

#### <a name="resolutions"></a>Resoluções
1. Reonboard toohello OMS serviço com Olá agente do OMS para Linux ao utilizar Olá os seguintes comandos com a opção de Olá `-v` ativada. Isto permite uma saída verbosa do agente de Olá ligar através do proxy de Olá toohello serviço OMS. 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. Reveja a secção de Olá [configurar o agente de Olá para utilização com um proxy HTTP server(#configuring the-agent-for-use-with-a-http-proxy-server) tooverify configurou corretamente Olá agente toocommunicate através de um servidor proxy.    
* Verificação de duplo Olá os seguintes pontos finais de serviço do OMS estão na lista de permissões:

    |Recursos do Agente| Portas |  
    |------|---------|  
    |*.ods.opinsights.azure.com | Porta 443|   
    |*.oms.opinsights.azure.com | Porta 443|   
    |ods.systemcenteradvisor.com | Porta 443|   
    |*.blob.Core.Windows.NET/ | Porta 443|   

### <a name="issue-you-receive-a-403-error-when-trying-tooonboard"></a>Problema: Recebe um erro 403 quando tenta tooonboard

#### <a name="probable-causes"></a>Causas prováveis
* Data e hora está incorreta no servidor do Linux 
* ID de área de trabalho e a chave de área de trabalho utilizado não estão corretos

#### <a name="resolution"></a>Resolução

1. Verificar o tempo de Olá no seu servidor Linux com data de comando Olá. Se houver tempo Olá + /-15 minutos da hora atual, em seguida, integração irá falhar. toocorrect esta atualização Olá data e/ou o fuso horário do servidor Linux. 
2. Certifique-se de que instalou a versão mais recente do Olá do Olá agente do OMS para Linux.  versão mais recente Olá agora notifica-o se tempo dissimetrias está a causar falhas de inclusão de Olá.
3. Reonboard utilizando correto ID e a chave de área de trabalho seguir as instruções de instalação de Olá anterior deste tópico.

### <a name="issue-you-see-a-500-and-404-error-in-hello-log-file-right-after-onboarding"></a>Problema: Vir um erro 404 e 500 no ficheiro de registo Olá imediatamente após a integração
Este é um problema conhecido que ocorre no primeiro carregamento de dados de Linux para uma área de trabalho do OMS. Isto não afeta os dados que está a ser enviada ou serviço experiência.

### <a name="issue--you-are-not-seeing-any-data-in-hello-oms-portal"></a>Problema: Não vir quaisquer dados no portal do OMS Olá

#### <a name="probable-causes"></a>Causas prováveis

- Falha de serviço do OMS toohello de integração
- Ligação toohello OMS serviço está bloqueada
- Agente do OMS Linux dados de cópia de segurança

#### <a name="resolutions"></a>Resoluções
1. Verifique se integração Olá OMS serviço foi concluída com êxito, verificando se hello seguinte ficheiro:`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`
2. Reonboard utilizando Olá `omsadmin.sh` instruções da linha de comandos
3. Se utilizar um proxy, consulte os passos de resolução de proxy de toohello fornecidos anteriormente.
4. Em alguns casos, quando Olá agente do OMS para Linux não consegue comunicar com Olá serviço OMS, os dados no agente Olá são toohello em fila o tamanho da memória intermédia completa, que é 50 MB. Olá agente do OMS para Linux deve ser reiniciado executando Olá os seguintes comandos: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`. 

    >[!NOTE]
    >Este problema ser corrigido 1.1.0-28 de versão do agente e mais tarde.
> 