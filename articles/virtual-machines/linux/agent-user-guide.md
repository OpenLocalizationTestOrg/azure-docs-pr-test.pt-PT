---
title: "aaaAzure descrição geral do agente de VM Linux | Microsoft Docs"
description: "Saiba como tooinstall e configurar o agente Linux (waagent) toomanage interação da sua máquina virtual com o controlador de recursos de infraestrutura do Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Compreensão e utilização de Olá agente Linux do Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Introdução
Olá Linux agente do Microsoft Azure (waagent) gere o Linux e FreeBSD aprovisionamento e interação de VM com Olá controlador de recursos do Azure. Fornece Olá funcionalidade para implementações de Linux e FreeBSD IaaS os seguintes:

> [!NOTE]
> Consulte o agente Linux do Azure de Olá [Leia-me](https://github.com/Azure/WALinuxAgent/blob/master/README.md) para obter detalhes adicionais.
> 
> 

* **Imagem de aprovisionamento**
  
  * Criação de uma conta de utilizador
  * Configurar tipos de autenticação SSH
  * Implementação de chaves públicas SSH e pares de chaves
  * Nome da definição Olá anfitrião
  * Publicação Olá nome toohello a plataforma de anfitrião DNS
  * Plataforma do toohello de impressão digital de chave de anfitrião do Reporting Services SSH
  * Gestão de discos de recursos
  * Formatação e montar o disco de recursos de Olá
  * Configurar o espaço de comutação
* **Redes**
  
  * Gere as rotas tooimprove compatibilidade com servidores DHCP de plataforma
  * Garante estabilidade Olá do nome de interface de rede Olá
* **Kernel**
  
  * Configura o virtual NUMA (desativar kernel < 2.6.37)
  * Consome entropia de Hyper-V para /dev/random
  * Configura os tempos limite de SCSI para o dispositivo de raiz de Olá (que pode ser remoto)
* **Diagnóstico**
  
  * Consola toohello de redirecionamento porta série
* **Implementações do SCVMM**
  
  * Deteta e bootstraps o agente do VMM Olá para Linux quando executado num ambiente do System Center Virtual Machine Manager 2012 R2
* **Extensão da VM**
  
  * Inserir componentes criados pela Microsoft e parceiros para a automatização de software e configuração de tooenable de VM com Linux (IaaS)
  * Implementação de referência de extensão da VM no [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Comunicação
fluxo de informações de Olá Olá plataforma toohello pelo agente ocorre através de dois canais:

* Um momento do arranque ligados DVD para implementações IaaS. DVD inclui um ficheiro de configuração compatível com OVF, que inclui todas as informações de aprovisionamento que não sejam Olá real keypairs SSH.
* Um ponto final TCP expor uma API REST utilizado tooobtain implementação e configuração da topologia.

## <a name="requirements"></a>Requisitos
Olá sistemas seguintes foram testados e são conhecidos toowork com Olá agente Linux do Azure:

> [!NOTE]
> Esta lista poderá ser diferente da lista oficial do Olá dos sistemas suportados no Olá plataforma do Microsoft Azure, conforme descrito aqui: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3 +
* Red Hat Enterprise Linux 6.7 +
* Debian 7.0 +
* Ubuntu 12.04 +
* openSUSE 12.3 +
* SLES 11 SP3 +
* Oracle Linux 6.4 +

Outros sistemas suportados:

* FreeBSD 10 + (agente Linux do Azure v2.0.10 +)

agente do Linux Olá depende alguns pacotes de sistema na ordem toofunction corretamente:

* Python 2.6 +
* OpenSSL 1.0 +
* OpenSSH 5.3 +
* Utilitários de sistema de ficheiros: sfdisk fdisk, mkfs, parted
* Ferramentas de palavra-passe: chpasswd, sudo
* Ferramentas de processamento de texto: PO, grep
* Ferramentas de rede: rota ip
* Suporta kernel para montar a sistemas de ficheiros instalados UDF.

## <a name="installation"></a>Instalação
Instalação a utilizar um RPM ou um pacote de DEB no repositório de pacotes a distribuição é o método de Olá preferido de instalação e atualização Olá agente Linux do Azure. Todos os Olá [aprovadas fornecedores de distribuição](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrar o pacote de agente Linux do Azure Olá as imagens e repositórios.

Consulte a documentação do toohello no Olá [repo do agente Linux do Azure no GitHub](https://github.com/Azure/WALinuxAgent) para opções de instalação avançadas, tais como instalar a partir de localizações de origem ou toocustom ou prefixos.

## <a name="command-line-options"></a>Opções de linha de comandos
### <a name="flags"></a>Sinalizadores
* verboso: aumentar a verbosidade do comando especificado
* forçar: Ignorar confirmação interativa para alguns comandos

### <a name="commands"></a>Comandos
* ajudar: apresenta uma lista de comandos de Olá suportado e sinalizadores.
* deprovision: tentativa de sistema de Olá tooclean e torná-lo adequado para o aprovisionamento de novamente. Esta operação eliminados seguinte Olá:
  
  * Todas as chaves de anfitrião SSH (se Provisioning.RegenerateSshHostKeyPair 'y' no ficheiro de configuração de Olá)
  * Configuração de NameServer no /etc/resolv.conf
  * Palavra-passe de raiz do /etc/shadow (se Provisioning.DeleteRootPassword 'y' no ficheiro de configuração de Olá)
  * Concessões de cliente DHCP em cache
  * Reposições toolocalhost.localdomain de nome de anfitrião

> [!WARNING]
> Desaprovisionamento garante que dessa imagem Olá é limpa de todas as informações confidenciais e adequado para a redistribuição.
> 
> 

* deprovision + utilizador: efetua tudo em - deprovision (acima) e também elimina Olá último aprovisionado conta de utilizador (obtida /var/lib/waagent) e dados associados. Este parâmetro é quando uma imagem que foi anteriormente aprovisionamento no Azure, pelo que podem ser capturada e novamente utilizado de aprovisionamento automatizados.
* versão: versão de Olá apresenta de waagent
* serialconsole: Configura GRUB toomark ttyS0 (Olá a primeira porta série) como a consola de arranque Olá. Isto garante que os registos do kernel lido enviados toothe de porta série e disponibilizados para depuração.
* o daemon: executar waagent como uma interação de toomanage daemon com a plataforma de Olá. Este argumento é toowaagent especificado no script de init Olá waagent.
* iniciar: executar waagent como um processo em segundo plano

## <a name="configuration"></a>Configuração
Um ficheiro de configuração (/ etc/waagent.conf) controlos Olá ações de waagent. Um ficheiro de configuração de exemplo é mostrado abaixo:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Olá que várias opções de configuração são descritas detalhadamente abaixo. Opções de configuração são dos três tipos; Valor booleano, cadeia ou número inteiro. Opções de configuração booleano Olá podem ser especificadas como "y" ou "n". Olá especial palavra-chave "None" podem ser utilizadas para alguns cadeia tipo entradas de configuração conforme especificado abaixo.

**Provisioning.Enabled:**  
Tipo: booleano  
Predefinição: y

Isto permite Olá utilizador tooenable ou desativar Olá no agente Olá a funcionalidade de aprovisionamento. Os valores válidos são "y" ou "n". Se o aprovisionamento estiver desativado, chaves de anfitrião e o utilizador SSH na imagem de Olá são preservadas e qualquer configuração especificada no Olá API de aprovisionamento do Azure é ignorada.

> [!NOTE]
> Olá `Provisioning.Enabled` demasiado "n" no Ubuntu nuvem imagens que utilizam a nuvem init para o aprovisionamento de predefinições de parâmetros.
> 
> 

**Provisioning.DeleteRootPassword:**  
Tipo: booleano  
Predefinição: n

Se o conjunto de palavra-passe de raiz de Olá no ficheiro Olá etc/sombra é apagado durante Olá o processo de aprovisionamento.

**Provisioning.RegenerateSshHostKeyPair:**  
Tipo: booleano  
Predefinição: y

Olá, se o conjunto de todos os SSH anfitrião pares de chaves (ecdsa, dsa e rsa) é eliminado durante o processo de aprovisionamento de /etc/hosts ssh /. E é gerado um par de chaves de raiz único.

tipo de encriptação de Olá par chave de raiz Olá é configurável pelo Olá Provisioning.SshHostKeyPairType entrada. Tenha em atenção que algumas distribuições recriará pares de chaves SSH para todos os tipos de encriptação em falta quando daemon de SSH Olá é reiniciado (por exemplo, após um reinício).

**Provisioning.SshHostKeyPairType:**  
Tipo: Cadeia  
Predefinição: rsa

Isto pode ser definido tipo de algoritmos de encriptação tooan que é suportado pelo daemon de SSH Olá na máquina virtual de Olá. valores de Olá normalmente suportado são "rsa", "dsa" e "ecdsa". Tenha em atenção que "putty.exe" no Windows não suporta "ecdsa". Por isso, se tenciona toouse putty.exe no Windows tooconnect tooa implementação Linux, utilize "rsa" ou "dsa".

**Provisioning.MonitorHostName:**  
Tipo: booleano  
Predefinição: y

Se definido, waagent irá monitorizar Olá máquina de virtual com Linux para que as alterações de nome de anfitrião (tal como devolvido pelo comando de "hostname" Olá) e atualizar automaticamente a configuração da rede Olá Olá imagem tooreflect Olá de alterações do. No nome do ordem toopush Olá alterar toohello servidores DNS, rede será reiniciada na máquina virtual de Olá. Este procedimento resultará na brief perda de conectividade à Internet.

**Provisioning.DecodeCustomData**  
Tipo: booleano  
Predefinição: n

Se definido, waagent será descodificar CustomData a partir de Base64.

**Provisioning.ExecuteCustomData**  
Tipo: booleano  
Predefinição: n

Se definido, waagent executará CustomData após o aprovisionamento.

**Provisioning.PasswordCryptId**  
Tipo: cadeia  
Predefinição: 6

Algoritmo utilizado pela crypt ao gerar o hash de palavra-passe.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Tipo: cadeia  
Predefinição: 10

Comprimento de salt aleatório utilizado ao gerar o hash de palavra-passe.

**ResourceDisk.Format:**  
Tipo: booleano  
Predefinição: y

Se definido, disco de recursos de Olá fornecido pela plataforma de Olá será formatado e montado pelas waagent se o tipo de sistema de ficheiros de Olá pedido pelo utilizador Olá "ResourceDisk.Filesystem" é diferente de "ntfs". Uma única partição do tipo Linux (83) será disponibilizada no disco Olá. Tenha em atenção que esta partição não será formatada se podem ser montados com êxito.

**ResourceDisk.Filesystem:**  
Tipo: Cadeia  
Predefinição: ext4

Esta ação Especifica o tipo de sistema de ficheiros de Olá para o disco de recursos de Olá. Os valores suportados variam consoante a distribuição de Linux. Se a cadeia de Olá é X, em seguida, mkfs. X deve estar presente na imagem de Linux Olá. SLES 11 imagens, normalmente, devem utilizar 'ext3'. Imagens de FreeBSD devem utilizar aqui 'ufs2'.

**ResourceDisk.MountPoint:**  
Tipo: Cadeia  
Predefinição: recursos/mnt / 

Esta ação Especifica o caminho de Olá que Olá recurso disco se encontra instalado. Tenha em atenção de que esse disco de recursos de Olá é um *temporário* disco e poderá ser esvaziada quando Olá VM é desaprovisionada.

**ResourceDisk.MountOptions**  
Tipo: Cadeia  
Predefinição: nenhuma

Especifica o disco montagem opções toobe transmitido toohello montagem -o comando. Esta é uma lista separada por vírgulas de valores, por ex. 'nodev, nosuid'. Consulte mount(8) para obter mais detalhes.

**ResourceDisk.EnableSwap:**  
Tipo: booleano  
Predefinição: n

Se definir um ficheiro de comutação (/ swapfile) é criado no disco de recursos de Olá e adicionar espaço de comutação do sistema toohello.

**ResourceDisk.SwapSizeMB:**  
Tipo: número inteiro  
Predefinição: 0

tamanho de Olá do ficheiro de comutação Olá em megabytes.

**Logs.Verbose:**  
Tipo: booleano  
Predefinição: n

Se o conjunto de verbosidade do registo é elevado. Waagent regista too/var/log/waagent.log e tira partido Olá logrotate funcionalidade toorotate os registos de sistema.

**SO. EnableRDMA**  
Tipo: booleano  
Predefinição: n

Se definido, agente Olá irá tentar tooinstall e, em seguida, carregar um controlador de kernel RDMA que corresponde à versão de Olá do firmware de Olá do Olá subjacente hardware.

**SO. RootDeviceScsiTimeout:**  
Tipo: número inteiro  
Predefinição: 300

Esta ação configura o tempo limite de SCSI Olá em segundos em unidades de disco e os dados de Olá SO. Se não for definido, sistema hello são utilizadas as predefinições.

**SO. OpensslPath:**  
Tipo: Cadeia  
Predefinição: nenhuma

Isto pode ser utilizado toospecify um caminho alternativo para Olá toouse binário do openssl para operações de criptografia.

**HttpProxy.Host, HttpProxy.Port**  
Tipo: Cadeia  
Predefinição: nenhuma

Se definido, Olá agente irá utilizar este proxy server tooaccess Olá internet. 

## <a name="ubuntu-cloud-images"></a>Ubuntu nuvem imagens
Tenha em atenção que utilizar imagens de nuvem Ubuntu [nuvem init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform Olá de muitas tarefas de configuração que caso contrário, teriam de ser geridas pelo agente Linux do Azure.  Tenha em atenção Olá seguintes diferenças:

* **Provisioning.Enabled** predefinições demasiado "n" no Ubuntu nuvem imagens que utilizam tooperform nuvem init aprovisionamento tarefas.
* Olá seguir os parâmetros de configuração não tem qualquer efeito nas imagens de nuvem Ubuntu que utilizam nuvem init toomanage Olá recurso disco e a comutação espaço:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* . Consulte Olá seguir o ponto de montagem do disco de recursos do recursos tooconfigure Olá e espaço no Ubuntu nuvem imagens de comutação durante o aprovisionamento:
  
  * [Ubuntu Wiki: Configurar partições de comutação](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Dados personalizados inserirem-se para uma Máquina Virtual do Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

