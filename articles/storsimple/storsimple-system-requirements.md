---
title: requisitos de sistema aaaStorSimple | Microsoft Docs
description: "Descreve o software, funcionamento em rede e os requisitos de elevada disponibilidade e melhores práticas para uma solução do Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>Software do StorSimple, elevada disponibilidade e requisitos de rede
## <a name="overview"></a>Descrição geral
Bem-vindo tooMicrosoft Azure StorSimple. Este artigo descreve os requisitos de sistema importantes e melhores práticas para o dispositivo StorSimple e para os clientes de armazenamento de Olá aceder ao dispositivo Olá. Recomendamos que reveja as informações de Olá cuidadosamente antes de implementar o sistema StorSimple e, em seguida, se referem novamente tooit conforme necessário durante a implementação e operação subsequente.

os requisitos de sistema Olá incluem:

* **Requisitos de software para clientes de armazenamento** -descreve os sistemas de operativos Olá suportada e quaisquer requisitos adicionais para nesses sistemas operativos.
* **Requisitos de rede do dispositivo do StorSimple Olá** -fornece informações sobre as portas de Olá toobe que é necessário abrir no seu tooallow de firewall para o tráfego de gestão, iSCSI ou em nuvem.
* **Requisitos de elevada disponibilidade para StorSimple** - descreve os requisitos de elevada disponibilidade e melhor práticas para o seu computador de anfitrião e o dispositivo StorSimple. 

## <a name="software-requirements-for-storage-clients"></a>Requisitos de software para clientes de armazenamento
Olá, os requisitos de software destinam-se a clientes de armazenamento de Olá que acedem ao seu dispositivo StorSimple.

| Sistemas operativos suportados | Versão necessária | Notas/requisitos adicionais |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012, 2012R2, 2016 |Volumes do StorSimple iSCSI são suportadas para utilização no apenas Olá os seguintes tipos de disco do Windows:<ul><li>Volume simples num disco básico</li><li>Volume Simple e espelhado no disco dinâmico</li></ul>Apenas Olá software iniciadores iSCSI presentes nativamente no sistema de operativo Olá são suportados. Os iniciadores iSCSI de hardware não são suportados.<br></br>Windows Server 2012 e 2016 o aprovisionamento dinâmico e funcionalidades ODX são suportadas se estiver a utilizar um volume do StorSimple iSCSI.<br><br>Criar StorSimple com aprovisionamento dinâmico e totalmente aprovisionado volumes. -Não é possível criar volumes parcialmente aprovisionados.<br><br>Reformatação de um volume com aprovisionamento dinâmico, pode demorar muito tempo. Recomendamos a eliminação volume Olá e, em seguida, criar um novo em vez de reformatação. No entanto, se ainda preferir tooreformat um volume:<ul><li>Execute Olá os seguintes comandos antes de atrasos de recuperação de espaço do Olá reformat tooavoid: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Depois de concluída a formatação Olá, de seguinte de Olá utilize comandos toore ativar recuperação de espaço:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Aplique a correção de Olá Windows Server 2012, conforme descrito em [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour computador de servidor do Windows.</li></ul></li></ul></ul> Se estiver a configurar o Snapshot Manager do StorSimple ou StorSimple adaptador para o SharePoint, vá demasiado[requisitos de Software para os componentes opcionais](#software-requirements-for-optional-components). |
| VMWare ESX |5.5 e 6.0 |Suportado com o VMWare vSphere como cliente de iSCSI. Funcionalidade de bloqueio VAAI é suportada com o VMware vSphere nos dispositivos StorSimple. |
| Linux RHEL/CentOS |5, 6 e 7 |Suporte para Linux iSCSI clientes com versões de iniciador do open iSCSI 5, 6 e 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX não é suportado com StorSimple.
> 
> 

## <a name="software-requirements-for-optional-components"></a>Requisitos de software para os componentes opcionais
Olá, os requisitos de software destinam-se a Olá StorSimple os componentes opcionais (Snapshot Manager do StorSimple e StorSimple adaptador para o SharePoint).

| Componente | Plataforma de anfitrião | Notas/requisitos adicionais |
| --- | --- | --- |
| Snapshot Manager do StorSimple |Windows Server 2008 R2 SP1, 2012, 2012R2 |Utilização do Snapshot Manager do StorSimple no Windows Server é necessária para a cópia de segurança/restauro de discos dinâmicos espelhados e para quaisquer cópias de segurança consistentes com aplicações.<br> Snapshot Manager do StorSimple é suportado apenas no Windows Server 2008 R2 SP1 (64 bits), o Windows 2012 R2 e o Windows Server 2012.<ul><li>Se estiver a utilizar janela Server 2012, tem de instalar o .NET 3.5 – 4.5 antes de instalar o Snapshot Manager do StorSimple.</li><li>Se estiver a utilizar o Windows Server 2008 R2 SP1, tem de instalar Windows Management Framework 3.0 antes de instalar o Snapshot Manager do StorSimple.</li></ul> |
| Adaptador do StorSimple para o SharePoint |Windows Server 2008 R2 SP1, 2012, 2012R2 |<ul><li>Placa StorSimple para SharePoint só é suportada no SharePoint 2010 e o SharePoint 2013.</li><li>RBS requer o SQL Server Enterprise Edition, versão 2008 R2 ou 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Requisitos de rede para o dispositivo StorSimple
O dispositivo StorSimple é um dispositivo bloqueado para / para baixo. No entanto, as portas necessário toobe aberto no seu tooallow de firewall para iSCSI, de nuvem e de tráfego de gestão. Olá tabela seguinte apresenta uma lista de portas de Olá que é necessário toobe aberta na firewall. Nesta tabela, *no* ou *entrada* refere-se a direção de toohello pedidos de cliente recebidos aceder a partir do qual o dispositivo. *Saída* ou *saída* refere-se a direção de toohello em que o dispositivo StorSimple envia dados externamente, para além de implementação de Olá: por exemplo, a saída toohello Internet.

| Um número de porta<sup>1,2</sup> | Entrada ou saída | Âmbito de porta | Necessário | Notas |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |Saída |WAN |Não |<ul><li>Porta de saída é utilizada para atualizações de tooretrieve de acesso à Internet.</li><li>proxy de web de saída de Olá é configurável de utilizador.</li><li>atualizações do sistema tooallow, esta porta têm de estar aberta para o controlador de Olá IPs fixo.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |Saída |WAN |Sim |<ul><li>Porta de saída é utilizada para aceder aos dados na nuvem de Olá.</li><li>proxy de web de saída de Olá é configurável de utilizador.</li><li>atualizações do sistema tooallow, esta porta têm de estar aberta para o controlador de Olá IPs fixo.</li><li>Esta porta é também utilizada em ambos os controladores de Olá para recolha de lixo.</li></ul> |
| UDP 53 (DNS) |Saída |WAN |Em alguns casos; consulte as notas. |Esta porta é necessária apenas se estiver a utilizar um servidor DNS baseado na Internet. |
| UDP 123 (NTP) |Saída |WAN |Em alguns casos; consulte as notas. |Esta porta é necessária apenas se estiver a utilizar um servidor NTP baseado na Internet. |
| TCP 9354 |Saída |WAN |Sim |porta de saída Olá é utilizada pelo Olá toocommunicate de dispositivo StorSimple com Olá serviço StorSimple Manager. |
| 3260 (iSCSI) |No |LAN |Não |Esta porta é utilizada tooaccess dados através de iSCSI. |
| 5985 |No |LAN |Não |Porta de entrada é utilizada pelo toocommunicate Snapshot Manager do StorSimple com o dispositivo StorSimple Olá.<br>Esta porta é também utilizada quando pode liga remotamente tooWindows do PowerShell para StorSimple através de HTTP. |
| 5986 |No |LAN |Não |Esta porta é utilizada quando pode liga remotamente tooWindows do PowerShell para StorSimple através de HTTPS. |

<sup>1</sup> não precisa de nenhuma porta de entrada toobe aberta no Olá Internet pública.

<sup>2</sup> se várias portas de efetuar uma configuração de gateway, ordem de saída tráfego encaminhado Olá será determinada com base na ordem de encaminhamento de porta de Olá descrito [porta encaminhamento](#routing-metric), abaixo.

<sup>3</sup> controlador Olá IPs fixo no dispositivo StorSimple tem de ser encaminhável e toohello tooconnect capaz de Internet diretamente ou através de Olá configurado o web proxy. endereços IP de Olá fixo são utilizados para a manutenção do dispositivo de toohello Olá atualizações. Se os controladores de dispositivo Olá não é possível ligar à Internet através de Olá IPs fixos do toohello, não será capaz de tooupdate o dispositivo StorSimple.

> [!IMPORTANT]
> Certifique-se de que a firewall Olá não modificar ou desencriptar qualquer tráfego SSL entre o dispositivo StorSimple Olá e o Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>Padrões de URL para as regras de firewall
Os administradores de rede, muitas vezes, podem configurar a firewall avançada regras com base no Olá de toofilter de padrões de URL Olá de entrada e Olá tráfego de saída. O dispositivo StorSimple e Olá serviço StorSimple Manager dependem outras aplicações da Microsoft, tais como o Service Bus do Azure, controlo de acesso do Azure Active Directory, as contas do storage e servidores do Microsoft Update. padrões de URL Olá associados estas aplicações podem ser utilizados tooconfigure regras de firewall. É importante toounderstand que podem alterar os padrões de URL Olá associados estas aplicações. Isto por sua vez irá exigir toomonitor de administrador de rede Olá e atualizar regras de firewall para o StorSimple como e quando necessário.

Recomendamos que defina as regras de firewall para o tráfego de saída, com base em endereços IP, fixos liberally na maioria dos casos do StorSimple. No entanto, pode utilizar informações de Olá abaixo tooset avançadas de regras de firewall que são ambientes segura toocreate necessários.

> [!NOTE]
> dispositivo Olá (origem) IPs deve ser sempre definido interfaces de rede tooall Olá ativada. destino de Olá IPs deve ser definido demasiado[intervalos IP do datacenter do Azure](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>Padrões de URL para o portal do Azure
| Padrão de URL | Componente/funcionalidade | IPs de dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |Serviço StorSimple Manager<br>Serviço de Controlo de Acesso<br>Service Bus do Azure |Interfaces de rede com capacidade de nuvem |
| `https://*.backup.windowsazure.com` |Registo de dispositivo |Apenas dados 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revogação de certificados |Interfaces de rede com capacidade de nuvem |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Monitorização e de contas do storage do Azure |Interfaces de rede com capacidade de nuvem |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores do Microsoft Update<br> |IPs fixos do controlador só |
| `http://*.deploy.akamaitechnologies.com` |CDN da Akamai |IPs fixos do controlador só |
| `https://*.partners.extranet.microsoft.com/*` |Pacote de suporte |Interfaces de rede com capacidade de nuvem |

#### <a name="url-patterns-for-azure-government-portal"></a>Padrões de URL para o portal do Azure Government
| Padrão de URL | Componente/funcionalidade | IPs de dispositivo |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |Serviço StorSimple Manager<br>Serviço de Controlo de Acesso<br>Service Bus do Azure |Interfaces de rede com capacidade de nuvem |
| `https://*.backup.windowsazure.us` |Registo de dispositivo |Apenas dados 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Revogação de certificados |Interfaces de rede com capacidade de nuvem |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Monitorização e de contas do storage do Azure |Interfaces de rede com capacidade de nuvem |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Servidores do Microsoft Update<br> |IPs fixos do controlador só |
| `http://*.deploy.akamaitechnologies.com` |CDN da Akamai |IPs fixos do controlador só |
| `https://*.partners.extranet.microsoft.com/*` |Pacote de suporte |Interfaces de rede com capacidade de nuvem |

### <a name="routing-metric"></a>Métrica de encaminhamento
Uma métrica de encaminhamento está associada a interfaces de Olá e gateway de Olá que encaminhar Olá dados toohello especificado redes. Métrica de encaminhamento é utilizada pelo Olá encaminhamento protocolo toocalculate Olá melhor caminho tooa fornecido destino, se aprende as vários caminhos existem toohello mesmo destino. Olá inferior Olá encaminhamento métrica, Olá Olá preferência superior.

Olá contexto do StorSimple, se várias interfaces de rede e gateways são configurados toochannel tráfego, métricas de encaminhamento Olá serão entrem em play toodetermine Olá relativo ordem na qual Olá interfaces irão obter utilizadas. métricas de encaminhamento Olá não podem ser alteradas pelo utilizador Olá. No entanto pode utilizar Olá `Get-HcsRoutingTable` cmdlet tooprint saída Olá e tabela de encaminhamento (métricas) no dispositivo StorSimple. Obter mais informações sobre o cmdlet Get-HcsRoutingTable no [StorSimple de resolução de problemas de implementação](storsimple-troubleshoot-deployment.md).

Olá encaminhamento métricos algoritmos é diferente dependendo da versão do software Olá em execução no dispositivo StorSimple.

**Versões anterior tooUpdate 1**

Isto inclui a versão de tooUpdate anteriores 1 como Olá DG, 0.1, 0,2 ou 0,3 de versões de software. ordem de Olá com base nas métricas de encaminhamento é o seguinte:

   *Última configurado interface de rede 10 GbE > interface de rede de outros 10 GbE > pela última vez configurado 1 interface de rede GbE > interface de rede de outro 1 GbE*

**Versões a partir de 1 de atualização e tooUpdate anterior 2**

Isto inclui as versões de software, como 1, 1.1 ou 1.2. ordem de Olá com base nas métricas de encaminhamento é decidido da seguinte forma:

   *DATA 0 > pela última vez configurado o interface de rede 10 GbE > interface de rede de outros 10 GbE > pela última vez configurado 1 interface de rede GbE > interface de rede de outro 1 GbE*

   Na atualização 1, métrica de encaminhamento de Olá da DATA 0 é efetuada Olá mais baixo; Por conseguinte, todas as Olá nuvem-tráfego é encaminhado através de dados 0. Tome nota deste se existirem mais de uma interface de rede de nuvem ativada no dispositivo StorSimple.

**Versões iniciados a partir da atualização 2**

A atualização 2 tem vários melhoramentos relacionado com redes e métricas de encaminhamento Olá foi alterada. comportamento de Olá pode ser explicado da seguinte forma.

* Foram atribuídos um conjunto de valores predeterminados toonetwork interfaces.     
* Considere uma tabela de exemplo abaixo com valores atribuídos toohello várias interfaces de rede quando estão preparados para nuvem ou em nuvem-desativado, mas com um gateway configurado. Os valores de Olá de nota atribuídos aqui são apenas valores de exemplo.

    | Interface de rede | Capacidade de nuvem | Nuvem-desativado com gateway |
    |-----|---------------|---------------------------|
    | Dados 0  | 1            | -                        |
    | Dados 1  | 2            | 20                       |
    | Dados 2  | 3            | 30                       |
    | Dados 3  | 4            | 40                       |
    | Dados 4  | 5            | 50                       |
    | Dados 5  | 6            | 60                       |


* ordem de Olá em que o tráfego de nuvem Olá será encaminhado através de interfaces de rede Olá é:
  
    *Dados 0 > dados 1 > data 2 > dados 3 > dados 4 > dados 5*
  
    Isto pode ser explicado pelos Olá seguinte exemplo.
  
    Considere um dispositivo StorSimple com duas interfaces de rede ativado para a nuvem, dados 0 e 5 de dados. Dados 1 a 4 de dados são nuvem-desativado, mas tem um gateway configurado. ordem de Olá em que o tráfego será encaminhado para este dispositivo será:
  
    *Dados 0 (1) > dados 5 (6) > dados 1 (20) > dados 2 (30) > dados 3 (40) > dados 4 (50)*
  
    *onde Olá números parênteses indicam as métricas de encaminhamento respetivos Olá.*
  
    Se falhar a Data 0, o tráfego de nuvem de Olá irá obter encaminhado através de dados 5. Uma vez que um gateway está configurado em todos os outro rede, se a Data 0 e 5 de dados foram toofail, tráfego de nuvem Olá passarão 1 de dados.
* Se falhar uma interface de rede ativado para a nuvem, em seguida, são 3 repetições com uma 30 segundo atraso tooconnect toohello interface. Se todas as tentativas de Olá falharem, tráfego Olá é encaminhado toohello seguinte disponível ativado para a nuvem a interface conforme determinado pela tabela de encaminhamento Olá. Se todos os Olá ativado para a nuvem interfaces de rede falharem, então dispositivo Olá serão ativadas pós-falha toohello outro controlador (sem reinício neste caso).
* Se existir uma falha de VIP para uma interface de rede com o iSCSI, vai ser 3 repetições com um atraso de 2 segundos. Este comportamento tem stayed Olá mesmo a partir de versões anteriores do Olá. Se todas as interfaces de rede de iSCSI Olá falharem, irá ocorrer uma ativação pós-falha de controlador (accompanied por um reinício).
* É também desencadeado um alerta no dispositivo StorSimple quando ocorre uma falha de VIP. Para mais informações, visite demasiado[referência rápida de alerta](storsimple-manage-alerts.md).
* Em termos de tentativas, iSCSI terá precedência sobre na nuvem.
  
    Considere o seguinte exemplo de Olá: StorSimple de um dispositivo tem duas interfaces de rede ativadas, os dados 0 e 1 de dados. Data 0 é ativado para a nuvem enquanto 1 de dados é tanto na nuvem e o iSCSI ativado. Outras interfaces de rede neste dispositivo estão ativados para a nuvem ou de iSCSI.
  
    Se falhar de dados 1, dado é a interface de rede iSCSI último Olá, tal resultará num tooData de ativação pós-falha do controlador 1 Olá no outro controlador.

### <a name="networking-best-practices"></a>Melhores práticas de rede
Além disso toohello acima requisitos de rede, para um desempenho ideal Olá da solução StorSimple, respeitar toohello seguir as melhores práticas:

* Certifique-se de que o dispositivo StorSimple tem uma largura de banda Mbps dedicado 40 (ou mais) disponível em todas as vezes. Não deve ser partilhada este largura de banda (ou alocação deve ser garantida através da utilização de Olá de políticas de QoS) com outras aplicações.
* Certifique-se de conectividade de rede toohello Internet está disponível em todas as vezes. Esporádicas ou pouco fiáveis Internet ligações toohello dispositivos, incluindo sem conectividade Internet contratutal, irão resultar numa configuração não suportada.
* Isole o tráfego de iSCSI e na nuvem de Olá por ter dedicados interfaces de rede no seu dispositivo para o acesso de iSCSI e na nuvem. Para obter mais informações, consulte como demasiado[modificar interfaces de rede](storsimple-modify-device-config.md#modify-network-interfaces) no dispositivo StorSimple.
* Não utilize uma configuração de protocolo de controlo de agregação de ligação (LACP) para as interfaces de rede. Esta é uma configuração suportada.

## <a name="high-availability-requirements-for-storsimple"></a>Requisitos de elevada disponibilidade do StorSimple
plataforma de hardware de Olá que está incluída com a solução do StorSimple Olá tem disponibilidade e fiabilidade funcionalidades que fornecem uma foundation para uma infraestrutura de armazenamento de elevada disponibilidade, com tolerância a falhas no seu centro de dados. No entanto, existem requisitos e melhores práticas que devem estar em conformidade com toohelp garantir a disponibilidade de Olá da solução StorSimple. Antes de implementar StorSimple, reveja com atenção Olá os seguintes requisitos e melhores práticas para o dispositivo StorSimple Olá e ligados computadores anfitriões.

Para mais informações sobre como monitorizar e manter os componentes de hardware de Olá do dispositivo StorSimple, visite demasiado[utilizar Olá StorSimple Manager serviço toomonitor os componentes de hardware e estado](storsimple-monitor-hardware-status.md) e [StorSimple substituição de componente de hardware](storsimple-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Requisitos de elevada disponibilidade e procedimentos para o dispositivo StorSimple
Olá Reveja com atenção os seguintes informações de elevada disponibilidade da tooensure Olá do dispositivo StorSimple.

#### <a name="pcms"></a>PCMs
Dispositivos StorSimple incluem redundante, frequente-swappable energia e arrefecimento módulos (PCMs). Cada PCM tem suficiente serviço tooprovide de capacidade para chassis todo Olá. tooensure elevada disponibilidade, ambos os PCMs tem de estar instalada.

* Ligar a disponibilidade de tooprovide origens de energia do PCMs toodifferent se falhar de uma origem de energia.
* Se um PCM falhar, pedir imediatamente uma substituição.
* Remover um PCM falhada apenas quando tiver substituição Olá e estão pronto tooinstall-lo.
* Não remova ambas PCMs em simultâneo. o módulo PCM de Olá inclui o módulo de cópia de segurança de bateria Olá. Remover ambos de Olá PCMs irá resultar num encerramento sem proteção de bateria e o estado do dispositivo Olá não será guardado. Para obter mais informações sobre bateria Olá, visite demasiado[módulo de cópia de segurança de bateria manter Olá](storsimple-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Módulos de controlador
Dispositivos StorSimple incluem módulos do controlador de acesso frequente-swappable, redundante. módulos de controlador Olá funcionam de forma ativo/passivo. Em qualquer momento, um módulo de controlador está ativo e está a fornecer serviço, ao hello outro módulo controlador passivo. módulo de controlador passivo Olá está ligado e se fica operacional se o módulo de controlador ativo Olá falha ou for removido. Cada módulo controlador tem suficiente serviço tooprovide de capacidade para chassis todo Olá. Ambos os módulos de controlador têm de ser instalado tooensure elevada disponibilidade.

* Certifique-se de que ambos os módulos de controlador estão instalados em qualquer momento.
* Se falhar um módulo de controlador, pedir imediatamente uma substituição.
* Remove um módulo de controlador falhada apenas quando tiver substituição Olá e estão pronto tooinstall-lo. Remover um módulo por períodos prolongados afetam airflow Olá e, por conseguinte, Olá arrefecimento do sistema de Olá.
* Certifique-se de que os módulos de controlador de tooboth de ligações de rede de Olá são idênticos e hello interfaces de rede ligados têm uma configuração de rede idênticas.
* Se um módulo de controlador falha ou tiver substituição, certifique-se de que Olá outro módulo controlador está num estado Active Directory antes de substituir o módulo de controlador falhada Olá. tooverify que um controlador está ativo, aceda demasiado[identificar controlador ativo do Olá no seu dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Não remova ambos os módulos de controlador em Olá mesmo tempo. Se uma ativação pós-falha controlador está em curso, não encerrar o módulo de controlador em modo de espera de Olá ou removê-la de chassis Olá.
* Após uma ativação pós-falha de controlador, aguarde, pelo menos, cinco minutos antes de remover o módulo de controlador.

#### <a name="network-interfaces"></a>Interfaces de rede
StorSimple controlador módulos do dispositivo cada tem quatro de 1 Gigabit e 10 de duas interfaces de rede de Gigabit Ethernet.

* Certifique-se de que os módulos de controlador de tooboth de ligações de rede de Olá são idênticos e interfaces de rede de Olá que interfaces de módulo Olá controlador estão ligado toohave uma configuração de rede idênticas.
* Sempre que possível, implemente ligações de rede entre a disponibilidade do serviço tooensure comutadores diferentes no evento Olá de falha de um dispositivo de rede.
* Quando desligar Olá apenas ou Olá último restantes interface preparada para iSCSI (com IPs atribuídos), desative primeiro a interface de Olá e, em seguida, desligue os cabos de Olá. Se a interface de Olá primeiro está desligada, em seguida, fará com que Olá controlador ativo toofail através de controlador passivo toohello. Se o controlador passivo Olá tem também as interfaces correspondentes desligadas, tanto os controladores de Olá irão reiniciar várias vezes antes de settling num controlador de um.
* Ligar a rede do toohello pelo menos duas interfaces de dados de cada módulo de controlador.
* Se tiver ativado as interfaces do Olá dois 10 GbE, implementá-los através de comutadores diferentes.
* Sempre que possível, utilize o MPIO no tooensure de servidores que os servidores de Olá podem tolerar uma ligação, a rede ou a falha de interface.

Para mais informações sobre o seu dispositivo para elevada disponibilidade e desempenho de rede, visite demasiado[instalar o seu dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [instalar o seu dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>SSDs e HDDs
Dispositivos StorSimple incluem discos de estado sólido (SSDs) e unidades de disco rígido (HDDs) que estão protegidas utilizando espelhada espaços. Utilização de espaços espelhados assegura que o dispositivo Olá tootolerate capaz de Olá falha uma ou mais SSDs ou HDDs.

* Certifique-se de que todos os módulos SSD e HDD estão instalados.
* Se falhar um SSD ou HDD, pedir imediatamente uma substituição.
* Se um SSD ou HDD falha ou necessita de substituição, certifique-se de que remova apenas Olá SSD ou HDD que necessita de substituição.
* Não remova mais do que um SSD ou HDD sistema Olá em qualquer ponto no tempo.
  Uma falha de 2 ou mais discos de determinado tipo (HDD, SSD) ou falha consecutivo dentro de um curto período de tempo pode resultar na perda de dados de avaria e potenciais do sistema. Se isto ocorrer, [contacte a Microsoft Support](storsimple-contact-microsoft-support.md) para obter assistência.
* Durante a substituição, monitorizar Olá **estado do Hardware** no Olá **manutenção** página para Olá unidades na Olá SSDs e HDDs. Um Estado de verificação verde indica que discos Olá estão em bom estado ou OK, enquanto que o ponto de exclamação uma vermelha indica uma falha SSD ou HDD.
* Recomendamos que configure instantâneos de nuvem para todos os volumes que precisa de tooprotect em caso de falha de sistema.

#### <a name="ebod-enclosure"></a>Inclusão EBOD
Modelo do dispositivo StorSimple 8600 inclui um bastidor expandido Bunch de discos (EBOD) no bastidor de principal de toohello de adição. Um EBOD contém controladores EBOD e unidades de disco rígido (HDDs) que estão protegidas utilizando espelhada espaços. Utilização de espaços espelhados assegura que o dispositivo Olá falha de Olá tootolerate capacidade dos HDDs de um ou mais. Olá bastidor EBOD é inclusão principal do toohello ligado através de cabos SAS redundantes.

* Certifique-se de que ambos os módulos de controlador de inclusão EBOD, cabos SAS e todas as unidades de disco de rígido Olá estão instalados em qualquer momento.
* Se um módulo de controlador de inclusão EBOD falhar, pedir imediatamente uma substituição.
* Se um módulo de controlador de inclusão EBOD falhar, certifique-se de que Olá outro módulo controlador está ativo antes de substituir o módulo Olá de falha. tooverify que um controlador está ativo, aceda demasiado[identificar controlador ativo do Olá no seu dispositivo](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Durante a substituição de módulo de controlador um EBOD, monitorizar continuamente o estado de Olá do componente de Olá no Olá serviço StorSimple Manager acedendo **manutenção** > **estado do Hardware**.
* Se um cabo SAS falha ou necessita de substituição (Support da Microsoft deve ser toomake envolvido essa uma determinação), certifique-se de que remova apenas Olá SAS cabo que necessita de substituição.
* Não em simultâneo remova os dois cabos SAS do sistema Olá em qualquer ponto no tempo.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Recomendações de elevada disponibilidade para os seus computadores de anfitrião
Reveja com atenção estas melhores práticas tooensure Olá elevada disponibilidade do dispositivo do StorSimple anfitriões tooyour ligado.

* Configurar StorSimple com [configurações de cluster de servidor de ficheiros de dois nós][1]. Ao remover pontos únicos de falha e a criação de redundância no lado do anfitrião de Olá, solução completa de Olá torna-se elevada.
* Utilize partilhas continuamente disponíveis (AC) disponíveis no Windows Server 2012 (SMB 3.0) para elevada disponibilidade durante a ativação pós-falha de controladores de armazenamento Olá. Para obter informações adicionais para configurar clusters de servidor de ficheiros e partilhas continuamente disponíveis com o Windows Server 2012, consulte toothis [demonstração vídeo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Passos seguintes
* [Saiba mais sobre os limites de sistema do StorSimple](storsimple-limits.md).
* [Saiba como toodeploy solução StorSimple](storsimple-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx
