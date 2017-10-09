---
title: "Descrição geral da solução de série de aaaStorSimple 8000 | Microsoft Docs"
description: "Descreve a criação de camadas do StorSimple, dispositivo Olá, dispositivo virtual, serviços e gestão de armazenamento e apresenta chaves termos utilizados no StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>Série 8000 do StorSimple: uma solução de armazenamento de nuvem híbrida
## <a name="overview"></a>Descrição geral
Bem-vindo tooMicrosoft Azure StorSimple, uma solução de armazenamento integrada que gere as tarefas de armazenamento entre dispositivos no local e o armazenamento de nuvem do Microsoft Azure. StorSimple é uma solução de rede (SAN) de área de armazenamento eficiente, económica e facilmente gerível que elimina muitos dos problemas de Olá e as despesas associadas a proteção de armazenamento e os dados da empresa. Utiliza dispositivos de série de 8000 do StorSimple Olá proprietários, integrado com serviços em nuvem e fornece um conjunto de ferramentas de gestão para uma vista totalmente integrada de todo o armazenamento empresarial, incluindo o armazenamento na nuvem. (as informações de implementação do Olá StorSimple publicadas no Web site do Microsoft Azure de Olá aplica-se tooStorSimple 8000 série apenas dispositivos. Se estiver a utilizar um dispositivo de série do StorSimple 5000/7000, aceda demasiado[StorSimple ajuda](http://onlinehelp.storsimple.com/).)

Utiliza StorSimple [armazenamento em camadas](#automatic-storage-tiering) toomanage armazenados os dados em vários suportes de dados de armazenamento. conjunto de trabalho atual Olá é armazenada no local em unidades de estado sólido (SSDs), os dados que são utilizados com menos frequência são armazenados em unidades de disco rígido (HDDs) e os dados de arquivo é feito o Push toohello nuvem. Além disso, StorSimple utiliza a eliminação de duplicados e a quantidade de Olá tooreduce compressão de armazenamento que Olá dados consome. Para mais informações, visite demasiado[eliminação de duplicados e compressão](#deduplication-and-compression). Definições das outras chaves termos e conceitos utilizados na documentação da série 8000 do StorSimple de Olá, aceda demasiado[terminologia do StorSimple](#storsimple-terminology) no fim de Olá deste artigo.

Além disso toostorage management, funcionalidades de proteção de dados do StorSimple ativar toocreate a pedido e cópias de segurança agendadas e, em seguida, armazená-los localmente ou numa Olá na nuvem. São efetuadas cópias de segurança no formulário de Olá de instantâneos incrementais, o que significa que pode ser criados e restaurados rapidamente. Instantâneos de nuvem podem ser extremamente importantes em cenários de recuperação após desastre porque substituir sistemas de armazenamento secundário (por exemplo, a cópia de segurança de banda) e permitir toorestore dados tooyour datacenter ou tooalternate sites, se necessário.

![ícone de vídeo](./media/storsimple-overview/video_icon.png) Veja o vídeo de Olá para tooMicrosoft uma introdução rápida do Azure StorSimple.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>Porquê utilizar StorSimple?
Olá tabela seguinte descreve algumas das principais vantagens do Olá que fornece o Microsoft Azure StorSimple.

| Funcionalidade | Vantagem |
| --- | --- |
| Integração transparente |Utiliza Olá iSCSI protocolo tooinvisibly ligação armazenamento instalações do dados. Isto garante que os dados armazenados na nuvem de Olá, no Centro de dados de Olá, ou em servidores remotos aparece toobe armazenado numa única localização. |
| Custos de armazenamento reduzido |Atribui suficiente local ou na nuvem armazenamento toomeet atual dar resposta às exigências e expande o armazenamento na nuvem apenas quando é necessário. Reduz ainda mais os requisitos de armazenamento e despesas por versões redundantes de Olá, eliminando os mesmos dados (eliminação de duplicados) e através da utilização de compressão. |
| Gestão de armazenamento simplificada |Fornece tooconfigure de ferramentas de administração do sistema e gerir dados armazenados no local, num servidor remoto e na nuvem de Olá. Além disso, pode gerir a cópia de segurança e restaurar as funções a partir de um snap-in Consola de gestão da Microsoft (MMC).|
| Recuperação após desastre melhorada e conformidade |Não necessita de tempo de recuperação expandida. Em vez disso, restaura dados conforme for necessário. Isto significa que as operações normais podem continuar com a mínima interrupção. Além disso, pode configurar as agendas de cópia de segurança de toospecify de políticas e retenção de dados. |
| Mobilidade de dados |Dados carregados tooMicrosoft serviços podem ser acedidos a partir de outros sites para fins de recuperação e de migração de nuvem do Azure. Além disso, pode utilizar aplicações de nuvem do StorSimple tooconfigure StorSimple em máquinas virtuais (VMs) em execução no Microsoft Azure. Olá VMs, em seguida, pode utilizar dados de tooaccess armazenados dispositivos virtuais para fins de teste ou de recuperação. |
| Continuidade do negócio |Permite StorSimple 5000 7000 série utilizadores toomigrate dispositivo dados tooa 8000 do StorSimple série. |
| Disponibilidade em Olá Portal do Azure Government |StorSimple está disponível no Olá Portal do Azure Government. Para obter mais informações, consulte [implementar o dispositivo StorSimple no local Olá Government Portal](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Proteção de dados e a disponibilidade |Olá série 8000 do StorSimple suporta zona redundante armazenamento (ZRS), em adição tooLocally armazenamento redundante (LRS) e armazenamento georredundante (GRS). Consulte demasiado[neste artigo sobre as opções de redundância do armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-redundancy/) para detalhes ZRS. |
| Suporte para aplicações críticas |Permite StorSimple que identificar volumes adequados como afixado localmente que por sua vez assegura que dados requeridos por aplicações críticas não toohello em camadas na nuvem. Volumes localmente afixados não são as latências toocloud do requerente ou problemas de conectividade. Para obter mais informações sobre volumes localmente afixados, consulte [utilizar Olá Gestor de dispositivos do StorSimple serviço toomanage volumes](storsimple-8000-manage-volumes-u2.md). |
| Baixa latência e elevado desempenho |Pode criar aplicações de nuvem que tirar partido das Olá de elevado desempenho, baixa latência as funcionalidades do armazenamento do Azure premium. Para obter mais informações sobre aplicações de nuvem do StorSimple premium, consulte [implementar e gerir um dispositivo de nuvem do StorSimple no Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>Componentes do StorSimple
Olá solução do Microsoft Azure StorSimple inclui Olá os seguintes componentes:

* **Dispositivo do Microsoft Azure StorSimple** – uma matriz de armazenamento híbrida no local que contém SSDs e HDDs, juntamente com os controladores de redundantes e capacidades de ativação pós-falha automática. os controladores de Olá faça a gestão de armazenamento em camadas, colocando atualmente utilizados (ou quentes) dados no armazenamento local (em Olá no local ou de dispositivo servidores), ao mover toohello de dados com menos frequência utilizada na nuvem.
* **Aplicação de nuvem do StorSimple** – também conhecido como Olá dispositivo Virtual StorSimple, esta é uma versão de software do dispositivo StorSimple Olá que replica arquitetura Olá e a maioria das capacidades do dispositivo de armazenamento físico híbrida Olá. Olá dispositivo de nuvem do StorSimple é executado num único nó numa máquina virtual do Azure. Dispositivos virtuais Premium que tirar partido do armazenamento premium do Azure, estão disponíveis na atualização 2 e versões posteriores.
* **Serviço do Gestor de dispositivos do StorSimple** – uma extensão de Olá portal do Azure que permite-lhe gerir um dispositivo StorSimple ou um dispositivo de nuvem do StorSimple a partir de uma interface web único. Pode utilizar toocreate de serviço do Gestor de dispositivos do StorSimple Olá e gerir serviços, ver e gerir dispositivos, ver alertas, gira volumes e ver e gerir políticas de cópia de segurança e de catálogo Olá de cópia de segurança.
* **O Windows PowerShell para StorSimple** – uma interface de linha de comandos que pode utilizar toomanage Olá dispositivo StorSimple. O Windows PowerShell para StorSimple tem funcionalidades que lhe permitem tooregister o dispositivo StorSimple, configure a interface de rede de Olá no seu dispositivo, instalar determinados tipos de atualizações, resolver problemas relacionados com o seu dispositivo ao aceder a sessão de suporte de Olá e alterar Olá Estado do dispositivo. Pode aceder a do Windows PowerShell para StorSimple, ligação toohello consola de série ou utilizando a comunicação remota do Windows PowerShell.
* **Cmdlets do Azure PowerShell StorSimple** – uma coleção de cmdlets do Windows PowerShell que permitem as tarefas de migração de nível de serviço e tooautomate Olá linha de comandos. Para mais informações sobre Olá cmdlets Azure PowerShell para StorSimple, visite toohello [referência de cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **Snapshot Manager do StorSimple** – um snap-in da MMC, que utiliza grupos de volume e Olá serviço de cópia de sombra de volumes do Windows toogenerate consistentes com aplicações cópias de segurança. Além disso, pode utilizar as agendas de cópia de segurança toocreate Snapshot Manager do StorSimple e clone ou restauro de volumes.
* **Placa StorSimple para SharePoint** – uma ferramenta de forma transparente expande a proteção de dados e de armazenamento do Microsoft Azure StorSimple tooSharePoint farms de servidores, ao tornar o armazenamento StorSimple podem ser visualizados e gerível de Olá Central do SharePoint Portal de administração.

Diagrama de Olá abaixo fornece uma vista detalhada da arquitetura do Microsoft Azure StorSimple de Olá e componentes.

![Arquitetura do StorSimple](./media/storsimple-overview/overview-big-picture.png)

Olá secções seguintes descrevem cada um destes componentes em maior detalhe e explicam como solução de Olá dispõe de dados, atribui o armazenamento e facilita a gestão de armazenamento e da proteção de dados. última seção do Olá fornece definições para alguns dos termos importantes Olá e conceitos tooStorSimple relacionados componentes e respetiva gestão.

## <a name="storsimple-device"></a>Dispositivo StorSimple
dispositivo de Microsoft Azure StorSimple Olá é uma matriz de armazenamento híbrida no local que fornece armazenamento primário e o iSCSI acesso toodata armazenados no mesmo. Gere a comunicação com o armazenamento na nuvem e ajuda a segurança de Olá tooensure e confidencialidade de todos os dados armazenados em Olá solução do Microsoft Azure StorSimple.

o dispositivo StorSimple Olá inclui SSDs e HDDs de unidades de disco rígido, bem como suporte de ativação pós-falha de clustering e automático. Contém um processador partilhado, o armazenamento partilhado e dois controladores espelhados. Cada controlador fornece seguinte Olá:

* Computador de anfitrião de tooa de ligação
* Cópia de segurança toosix rede portas tooconnect toohello rede local (LAN)
* Monitorização de hardware
* Memória de acesso aleatório não volátil (NVRAM), que mantém informações mesmo energia é interrompida
* Suporte para cluster sem qualquer efeito na disponibilidade do serviço de atualização toomanage atualizações de software em servidores num cluster de ativação pós-falha para que as atualizações de Olá têm mínima ou
* Cluster do serviço, as funções, como um cluster de back-end, fornecer elevada disponibilidade e minimizar os efeitos adversos que podem ocorrer se um HDD ou o SSD falha ou for colocado offline

Apenas um controlador é Active Directory em qualquer ponto no tempo. Se o controlador de Active Directory Olá falhar, controlador segundo Olá fica ativa automaticamente.

Para mais informações, visite demasiado[StorSimple componentes de hardware e estado](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>StorSimple Cloud Appliance
Pode utilizar StorSimple toocreate uma aplicação de nuvem que replica arquitetura Olá e capacidades do dispositivo de armazenamento físico híbrida Olá. Olá dispositivo StorSimple de nuvem (também conhecido como Olá dispositivo Virtual StorSimple) é executado num único nó numa máquina virtual do Azure. (Uma aplicação de nuvem só é possível criar uma máquina virtual do Azure. Não é possível criar um dispositivo StorSimple ou um servidor no local.)

aplicação de nuvem Olá tem Olá seguintes funcionalidades:

* Este comporta-se como um dispositivo físico e pode oferecer um iSCSI máquinas de toovirtual interface na nuvem de Olá.
* Pode criar um número ilimitado de aplicações em nuvem na nuvem de Olá e ativá-los e desativar o conforme necessário.
* Pode ajudá-lo a simular ambientes no local na recuperação após desastre, desenvolvimento e teste cenários e pode ajudar a obtenção ao nível do item de cópias de segurança.

Olá dispositivo de nuvem do StorSimple está disponível em dois modelos: dispositivo Olá 8010 (anteriormente conhecido como modelo Olá 1100) e Olá 8020 dispositivo. dispositivos 8010 Olá tem uma capacidade máxima de 30 TB. dispositivo 8020 Olá, que tira partido do armazenamento premium do Azure, tem uma capacidade máxima de 64 TB. (No locais camadas, armazenamento premium do Azure armazena os dados em SSDs enquanto o armazenamento standard armazena dados em HDDs.) Tenha em atenção que tem de ter um armazenamento de premium toouse de conta de armazenamento de premium do Azure. Para mais informações sobre o armazenamento premium, visite demasiado[Premium Storage: armazenamento de elevado desempenho para cargas de trabalho de Máquina Virtual de Azure](../storage/common/storage-premium-storage.md).

Para obter mais informações sobre Olá dispositivo de nuvem do StorSimple, visite demasiado[implementar e gerir um dispositivo de nuvem do StorSimple no Azure](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>Serviço do Gestor de dispositivos do StorSimple
Microsoft Azure StorSimple fornece uma interface de utilizador baseadas na web (serviço do Gestor de dispositivos do StorSimple Olá) que permite-lhe toocentrally gerir centros de dados e armazenamento na nuvem. Pode utilizar Olá tooperform Olá Gestor de dispositivos do StorSimple serviço seguintes tarefas:

* Configure definições do sistema para dispositivos StorSimple.
* Configurar e gerir as definições de segurança para dispositivos StorSimple.
* Configure as credenciais de nuvem e de propriedades.
* Configurar e gerir volumes num servidor.
* Configure grupos de volume.
* Cópia de segurança e restaurar dados.
* Monitorizar o desempenho.
* Reveja as definições do sistema e identificar informações sobre problemas possíveis.

Pode utilizar tooperform de serviço do Gestor de dispositivos do StorSimple Olá todas as tarefas de administração, exceto aqueles que necessitam de sistema pendente tempo, tais como a configuração inicial e a instalação das atualizações.

Para mais informações, visite demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell para StorSimple
O Windows PowerShell para StorSimple fornece uma interface de linha de comandos que pode utilizar toocreate e gestão do serviço Microsoft Azure StorSimple Olá e configurar e monitorizar dispositivos StorSimple. É uma interface de linha de comandos baseado no Windows PowerShell, que inclui cmdlets dedicados para gerir o dispositivo StorSimple. O Windows PowerShell para StorSimple tem funcionalidades que lhe permitem:

* Registe um dispositivo.
* Configure a interface de rede de Olá num dispositivo.
* Instale determinados tipos de atualizações.
* Resolver problemas relacionados com o seu dispositivo ao aceder a sessão de suporte de Olá.
* Alterar Estado do dispositivo Olá.

Pode aceder ao Windows PowerShell para StorSimple a partir de uma consola de série (num anfitrião computador ligado diretamente dispositivos toohello) ou remotamente através da utilização de comunicação remota do Windows PowerShell. Tenha em atenção que alguns do Windows PowerShell para StorSimple tarefas, tais como o registo de dispositivos inicial, só pode ser efetuado na consola de série de Olá.

Para mais informações, visite demasiado[utilize o Windows PowerShell para StorSimple tooadminister dispositivo](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>Cmdlets do Azure PowerShell StorSimple
cmdlets do Azure PowerShell StorSimple Olá são um conjunto de cmdlets do Windows PowerShell que permitem que tooautomate nível de serviço e tarefas de migração a partir da linha de comandos Olá. Para mais informações sobre Olá cmdlets Azure PowerShell para StorSimple, visite toohello [referência de cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>Snapshot Manager do StorSimple
Snapshot Manager do StorSimple é um snap-in Consola de gestão da Microsoft (MMC) que pode utilizar toocreate consistente, ponto no tempo cópias de segurança do local e da nuvem. Olá snap-in em execução no anfitrião baseado no Windows Server. Pode utilizar o Snapshot Manager do StorSimple para:

* Configurar, fazer cópias de segurança e eliminar os volumes.
* Configurar o volume tooensure de grupos de segurança dos dados é consistente com aplicações.
* Gerir políticas de cópia de segurança para que os dados são uma cópia de segurança com base numa agenda predeterminada e armazenados numa localização designada (local ou na nuvem de Olá).
* Restaure volumes e ficheiros individuais.

As cópias de segurança são capturadas como instantâneos, que apenas as alterações de Olá de registo uma vez que Olá último instantâneo e necessitam de menos espaço de armazenamento de cópias de segurança completas. Pode criar agendas de cópia de segurança ou fazer cópias de segurança de imediato, conforme necessário. Além disso, pode utilizar as políticas de retenção do Snapshot Manager do StorSimple tooestablish esse controlo instantâneos quantos serão guardados. Se precisar de toorestore dados a partir de uma cópia de segurança, permite do Snapshot Manager do StorSimple, subsequentemente, selecione catálogo Olá da local ou instantâneos de nuvem. 

Se ocorrer um desastre ou se precisar de dados de toorestore por outro motivo, Snapshot Manager do StorSimple restaura-incrementalmente conforme for necessário. Restauro de dados não necessita que a encerrar Olá todo sistema ao restaurar um ficheiro, substitua o equipamento ou mover site tooanother de operações.

Para mais informações, visite demasiado[Novidades Snapshot Manager do StorSimple?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>Adaptador do StorSimple para o SharePoint
Microsoft Azure StorSimple inclui Olá StorSimple adaptador para o SharePoint, um componente opcional que transparente expande farms de servidores de tooSharePoint de funcionalidades de proteção de dados e armazenamento StorSimple. placa Olá funciona com um fornecedor de armazenamento de BLOBs remoto (RBS) e a funcionalidade do SQL Server RBS Olá, permitindo toomove BLOBs tooa servidor uma cópia de segurança pelo sistema de Microsoft Azure StorSimple Olá. Microsoft Azure StorSimple, em seguida, armazena dados de BLOBS de Olá localmente ou numa nuvem Olá, com base na utilização.

Olá StorSimple adaptador para o SharePoint é gerido a partir do portal de Administração Central do SharePoint Olá. Por conseguinte, gestão do SharePoint permanece centralizada e todo o armazenamento aparece toobe no farm do SharePoint Olá.

Para mais informações, visite demasiado[StorSimple adaptador para o SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Tecnologias de gestão de armazenamento
Além disso toohello dedicado dispositivo StorSimple, dispositivo virtual e outros componentes, utiliza o Microsoft Azure StorSimple Olá seguir software tecnologias tooprovide acesso rápido toodata e tooreduce consumo de armazenamento:

* [A criação de camadas de armazenamento automática](#automatic-storage-tiering) 
* [Aprovisionamento dinâmico](#thin-provisioning) 
* [A eliminação de duplicados e compressão](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>A criação de camadas de armazenamento automática
Microsoft Azure StorSimple dispõe automaticamente os dados na lógicas camadas com base na utilização atual, idade e os dados de tooother de relação. Dados que está a maioria dos Active Directory estiver armazenado localmente, enquanto menos ativa e inativos dados são automaticamente migradas toohello nuvem. Olá seguinte diagrama ilustra esta abordagem de armazenamento.

![Camadas de armazenamento do StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

acesso rápido tooenable, StorSimple armazena dados muito ativos (dados) em SSDs no dispositivo do StorSimple Olá. Armazena dados que são ocasionalmente utilizados (transfira dados) em HDDs no dispositivo Olá ou em servidores no Olá datacenter. Move os dados inativos, dados de cópia de segurança, e os dados retidos de arquivo ou conformidade fins toohello nuvem. 

> [!NOTE]
> Na atualização 2 ou posterior, pode especificar um volume afixado localmente como, caso em que os dados de Olá permanecem no dispositivo local Olá e não estão em camadas toohello nuvem. 


StorSimple ajusta e reorganiza dados e altere as atribuições de armazenamento como padrões de utilização. Por exemplo, algumas informações podem ficar menos ativas ao longo do tempo. À medida que for progressivamente menos ativa, é migrada SSDs tooHDDs e, em seguida, toohello nuvem. Se esse mesmos dados ficam ativos novamente, é migrada toohello back dispositivo de armazenamento.

processo de camadas de armazenamento de Olá ocorre da seguinte forma:

1. Um administrador de sistema configura uma conta de armazenamento de nuvem do Microsoft Azure.
2. administrador de Olá utiliza Olá série consola e Olá Gestor de dispositivos do StorSimple serviço (em execução no Olá portal do Azure) tooconfigure Olá dispositivos e servidores de ficheiros, criar políticas de proteção de volumes e dados. Máquinas no local (como servidores de ficheiros) utilizam Olá Internet Small Computer System Interface (iSCSI) tooaccess Olá o dispositivo do StorSimple.
3. Inicialmente, StorSimple armazena os dados na camada SSD rápida Olá do dispositivo Olá.
4. Como Olá abordagens capacidade da camada SSD, StorSimple deduplicates comprime blocos de dados mais antigos Olá e move-los camada HDD de toohello.
5. Como Olá capacidade de abordagens de camada HDD, StorSimple encripta os blocos de dados mais antigos Olá e envia-as em segurança conta de armazenamento do Microsoft Azure toohello através de HTTPS.
6. Microsoft Azure cria várias réplicas de dados de Olá no seu datacenter e num centro de dados remoto, garantindo que podem ser recuperados dados Olá, se ocorrer um desastre.
7. Quando o servidor de ficheiros de Olá solicita dados armazenados na nuvem de Olá, StorSimple devolve-lo de forma totalmente integrada e armazena uma cópia na camada SSD Olá de dispositivo do StorSimple Olá.

#### <a name="how-storsimple-manages-cloud-data"></a>Como StorSimple gere dados em nuvem

StorSimple deduplicates dados de cliente em todos os instantâneos de Olá e dados de principal de Olá (os dados escritos pelos anfitriões). Enquanto a eliminação de duplicados é excelente eficiência de armazenamento, faz pergunta Olá "que é na nuvem de Olá" complicou. Olá dados primários em camadas e dados de instantâneos de Olá sobrepor-se entre si. Um segmento de dados na nuvem de Olá único podia ser utilizado como dados primários em camadas e também ser referenciado por vários instantâneos. Todos os instantâneos de nuvem garante que uma cópia de todos os dados de ponto no tempo de Olá está bloqueada para a nuvem de Olá até esse instantâneo é eliminado.

Dados só são eliminados da nuvem Olá quando existem não existem dados de toothat de referências. Por exemplo, se iremos tirar um instantâneo de nuvem de todos os dados de Olá que o dispositivo StorSimple Olá e, em seguida, elimine alguns dados primários, seria vemos Olá _dados primários_ drop imediatamente. Olá _da nuvem_ que inclui Olá dados em camadas e Olá cópias de segurança, permanece Olá mesmo. Isto acontece porque há um instantâneo ainda com referência a dados de nuvem Olá. Após a nuvem de Olá instantâneo é eliminado (e quaisquer outros instantâneos referenciado Olá mesmos dados), cloud remoções de consumo. Antes de Iremos remover dados em nuvem, iremos Verifique se não existem instantâneos ainda fazem referência a dados. Este processo é denominado _recolha de lixo_ e é um serviço em segundo plano em execução no dispositivo Olá. Remoção de dados em nuvem não é imediata, como o serviço de recolha de lixo Olá verifica a existência de outras referências a dados toothat antes da eliminação de Olá. velocidade de Olá da recolha de lixo depende do número total de Olá de instantâneos e total de dados Olá. Normalmente, dados de nuvem Olá foram limpos em menos de uma semana.


### <a name="thin-provisioning"></a>Aprovisionamento dinâmico
Aprovisionamento dinâmico é uma tecnologia de virtualização em que o armazenamento disponível aparece recursos físicos tooexceed. Em vez de reservar antecipadamente armazenamento suficiente, StorSimple utiliza tooallocate de aprovisionamento dinâmico suficiente toomeet atual os requisitos de espaço. natureza elástico Olá armazenamento na nuvem facilita esta abordagem porque StorSimple pode aumentar ou diminuir cloud storage toomeet evolutivos.

> [!NOTE]
> Volumes localmente afixados não são com aprovisionamento dinâmico. Armazenamento atribuído tooa só local volume é aprovisionado na íntegra quando Olá volume é criado.


### <a name="deduplication-and-compression"></a>A eliminação de duplicados e compressão
A eliminação de duplicados do Microsoft Azure StorSimple utiliza e toofurther de compressão de dados a reduzir os requisitos de armazenamento.

A eliminação de duplicados reduz Olá quantidade global de dados armazenados através da eliminação de redundância no conjunto de dados de Olá armazenado. Como informação muda, StorSimple ignora os dados de Olá inalterado e capturas de Olá apenas as alterações. Além disso, o StorSimple reduz a quantidade de Olá dos dados armazenados ao identificar e remover informações desnecessárias. 

> [!NOTE]
> Dados em volumes localmente afixados não eliminação de duplicados ou não estão comprimidos. No entanto, as cópias de segurança de volumes localmente afixados são duplicadas e comprimidas.


## <a name="storsimple-workload-summary"></a>Resumo da carga de trabalho do StorSimple
Um resumo das cargas de trabalho do Olá suportado StorSimple é apresentado abaixo.

| Cenário | Carga de trabalho | Suportado | Restrições | Versão |
| --- | --- | --- | --- | --- |
| Colaboração |Partilha de ficheiros |Sim | |Todas as versões |
| Colaboração |Partilha de ficheiros distribuído |Sim | |Todas as versões |
| Colaboração |SharePoint |Sim* |Suportado apenas com volumes localmente afixados |Atualização 2 e posterior |
| Arquivo |Arquivo de ficheiro simples |Sim | |Todas as versões |
| Virtualização |Máquinas virtuais |Sim* |Suportado apenas com volumes localmente afixados |Atualização 2 e posterior |
| Base de Dados |SQL |Sim* |Suportado apenas com volumes localmente afixados |Atualização 2 e posterior |
| Vigilância de vídeo |Vigilância de vídeo |Sim* |Suportada quando o dispositivo StorSimple é dedicado única carga de trabalho do toothis |Atualização 2 e posterior |
| Cópia de segurança |Cópia de segurança do destino principal |Sim* |Suportada quando o dispositivo StorSimple é dedicado única carga de trabalho do toothis |Update 3 e posterior |
| Cópia de segurança |Cópia de segurança de destino secundária |Sim* |Suportada quando o dispositivo StorSimple é dedicado única carga de trabalho do toothis |Update 3 e posterior |

*Sim &#42; -Solução diretrizes e restrições devem ser aplicadas.*

Olá seguintes cargas de trabalho não é suportado pelos dispositivos de série 8000 do StorSimple. Se tiver implementado num StorSimple, estas cargas de trabalho irão resultar numa configuração não suportada.

* Processamento de imagens médicas
* Troca
* VDI
* Oracle
* SAP
* Macrodados
* Distribuição de conteúdo
* Arranque a partir de SCSI

Segue-se uma lista de componentes da infraestrutura Olá StorSimple suportado.

| Cenário | Carga de trabalho | Suportado | Restrições | Versão |
| --- | --- | --- | --- | --- |
| Geral |ExpressRoute |Sim | |Todas as versões |
| Geral |DataCore FC |Sim* |Suportado com DataCore SANsymphony |Todas as versões |
| Geral |DFSR |Sim* |Suportado apenas com volumes localmente afixados |Todas as versões |
| Geral |Indexação |Sim* |Volumes em camadas, a indexação de metadados só é suportada (sem dados).<br>Para volumes afixados localmente, a indexação completa é suportada. |Todas as versões |
| Geral |Software antivírus |Sim* |A volumes em camadas, é suportada apenas análise na abertura e fecho.<br> Para volumes afixados localmente, análise completa é suportada. |Todas as versões |

*Sim &#42; -Solução diretrizes e restrições devem ser aplicadas.*

Segue-se uma lista de outro software que são utilizadas com soluções de toobuild do StorSimple.

| Tipo de carga de trabalho | Software utilizados com StorSimple | Versões suportadas|Guia de toosolution de ligação| 
| --- | --- | --- | --- |
| Destino de cópia de segurança |Veeam |Veeam v 9 e posterior |[StorSimple como destino de cópia de segurança com Veaam](storsimple-configure-backup-target-veeam.md)|
| Destino de cópia de segurança |Exec VERITAS cópia de segurança |Cópia de segurança Exec 16 e posterior |[StorSimple como destino de cópia de segurança com Exec cópia de segurança](storsimple-configure-backup-target-using-backup-exec.md)|
| Destino de cópia de segurança |VERITAS NetBackup |NetBackup 7.7.x e posterior  |[StorSimple como destino de cópia de segurança com NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Partilha de ficheiros global <br></br> Colaboração |Talon  |[StorSimple com Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>Terminologia do StorSimple
Antes de implementar a sua solução do Microsoft Azure StorSimple, recomendamos que consulte o artigo seguinte Olá termos e definições.

### <a name="key-terms-and-definitions"></a>Termos de chaves e definições
| Duração (acrónimo ou abreviatura) | Descrição |
| --- | --- |
| registo de controlo de acesso (ACR) |Um registo associado um volume no dispositivo Microsoft Azure StorSimple que determina os anfitriões que podem ligar tooit. a determinação de Olá é baseada em iSCSI de Olá nome qualificado (IQN) de anfitriões de Olá (contidos Olá ACR) que estão a ligar tooyour o dispositivo StorSimple. |
| AES 256 |Um algoritmo de encriptação AES (Advanced Standard) 256 bits para encriptar os dados são transmitidos tooand da nuvem Olá. |
| tamanho da unidade de alocação (AUS) |Olá mais pequena quantidade de espaço em disco que pode ser atribuído toohold um ficheiro no seu sistemas de ficheiros do Windows. Se um tamanho de ficheiro não é um múltiplo par de tamanho de cluster Olá, espaço adicional tem de ser ficheiro de Olá toohold utilizados (cópia de segurança toohello seguinte múltiplo do tamanho do cluster Olá) resultando num espaço perdido e a fragmentação do disco de rígido Olá. <br>Olá recomendado que Aus para volumes de Azure StorSimple é 64 KB porque funciona bem com os algoritmos de eliminação de duplicados Olá. |
| a criação de camadas de armazenamento automático |Mover automaticamente dados menos ativos do SSDs tooHDDs e, em seguida, a camada tooa na nuvem Olá e, em seguida, ativar a gestão de todo o armazenamento de uma interface de utilizador central. |
| Catálogo de cópias de segurança |Uma coleção de cópias de segurança, normalmente, relacionados por tipo de aplicação Olá que foi utilizado. Esta coleção é apresentada no painel de catálogo de cópia de segurança de Olá da Olá serviço Gestor de dispositivos do StorSimple da IU. |
| ficheiro de cópia de segurança de catálogo |Um ficheiro que contém uma lista de instantâneos disponíveis atualmente armazenados em Olá cópia de segurança da base de dados do Snapshot Manager do StorSimple. |
| política de cópia de segurança |Uma seleção de volumes, tipo de cópia de segurança e um timetable que lhe permite toocreate cópias de segurança numa agenda predefinida. |
| objetos de grandes dimensões binários (BLOBs) |Uma coleção de dados binários armazenados como uma única entidade no sistema de gestão da base de dados. Os bLOBs são, normalmente, imagens, áudio ou outros objetos multimedia, embora código executável binário, por vezes, é armazenado como um BLOB. |
| Protocolo de autenticação de Handshake de desafio (CHAP) |Um protocolo utilizado tooauthenticate ponto a ponto Olá de uma ligação, com base no elemento de Olá partilha uma palavra-passe ou o segredo. CHAP pode ser unidirecional ou mútua. Com unidirecional CHAP, o destino de Olá autentica um iniciador. CHAP mútua requer que o destino Olá autenticar iniciador Olá e esse iniciador Olá autentica destino Olá. |
| Clone |Uma cópia duplicada de um volume. |
| Nuvem como uma camada (CaaT) |Nuvem de armazenamento integrado como uma camada dentro da arquitetura de armazenamento Olá, para que todo o armazenamento aparece toobe parte da rede de armazenamento de uma empresa. |
| fornecedor de serviço em nuvem (CSP) |Um fornecedor de serviços de computação na nuvem. |
| instantâneo na nuvem |Uma cópia de ponto no tempo dos dados do volume que são armazenadas na nuvem de Olá. Um instantâneo na nuvem é equivalente instantâneo tooa replicado num sistema de armazenamento diferentes, fora das instalações. Os instantâneos de nuvem são particularmente útil em cenários de recuperação após desastre. |
| Chave de encriptação de armazenamento na nuvem |Uma palavra-passe ou uma chave utilizado pelos seus dados de tooaccess dispositivo do StorSimple Olá encriptada enviados pelo seu dispositivo toohello nuvem. |
| atualização com suporte para cluster |Gerir atualizações de software em servidores num cluster de ativação pós-falha para que as atualizações de Olá têm mínima ou sem qualquer efeito na disponibilidade do serviço. |
| DataPath |Uma coleção de unidades funcionais que efetuar operações de processamento de dados entre ligado. |
| Desativar |Uma ação permanente que quebras Olá ligação entre o dispositivo StorSimple Olá e Olá associadas ao serviço em nuvem. Instantâneos de nuvem do dispositivo Olá permanecem após este processo e podem ser clonados ou utilizados para recuperação após desastre. |
| espelhamento do disco |Unidades de replicação de volumes de disco lógico no disco rígido separadas em tempo real tooensure a disponibilidade contínua. |
| espelhamento de disco dinâmico |Replicação de volumes de disco lógico em discos dinâmicos. |
| discos dinâmicos |Um formato de volume disco, que utiliza Olá toostore do Gestor de discos lógicos (LDM) e gerir os dados entre vários discos físicos. Os discos dinâmicos pode ser aumentada tooprovide mais espaço livre. |
| Inclusão de Bunch de discos (EBOD) expandida |Um bastidor secundário do dispositivo Microsoft Azure StorSimple que contém discos de disco rígido extra de armazenamento adicional. |
| Aprovisionamento FAT |Um convencional aprovisionamento de armazenamento no armazenamento de que o espaço é alocado com base no antecipado necessidades (e é, normalmente, para além da necessidade de atual Olá). Consulte também *aprovisionamento dinâmico*. |
| unidade de disco rígido (HDD) |Uma unidade que utiliza a rotação dos dados de toostore platters. |
| armazenamento de nuvem híbrida |Arquitetura de armazenamento que utiliza recursos locais e fora das instalações, incluindo o armazenamento na nuvem. |
| Internet Small Computer System Interface (iSCSI) |Um padrão de rede armazenamento baseado em IP do protocolo de Internet para ligar o equipamento de armazenamento de dados ou instalações. |
| iniciador iSCSI |Um componente de software que permite que um computador anfitrião com a rede de armazenamento baseado em iSCSI externo do Windows tooconnect tooan. |
| iSCSI nome qualificado (IQN) |Um nome exclusivo que identifica um destino de iSCSI ou de iniciador. |
| destino iSCSI |Um componente de software que fornece iSCSI centralizado subsistemas de disco em redes de armazenamento. |
| em direto arquivo |Uma abordagem de armazenamento na qual os dados de arquivo são acessíveis a todos os Olá tempo (não são armazenadas off-site em banda, por exemplo). Microsoft Azure StorSimple utiliza arquivar em direto. |
| volume afixado localmente |um volume que reside no dispositivo Olá e nunca se camadas toohello nuvem. |
| instantâneo local |Uma cópia de ponto no tempo dos dados do volume que são armazenados num dispositivo de Microsoft Azure StorSimple Olá. |
| Microsoft Azure StorSimple |Uma solução poderosa constituída por um dispositivo de armazenamento do Centro de dados e o software que permite IT organizações tooleverage armazenamento na nuvem como se fosse o armazenamento do Centro de dados. StorSimple simplifica a gestão de dados e proteção de dados ao reduzir os custos. solução Olá consolida primária armazenamento, arquivo, cópia de segurança e recuperação após desastre (DR) através da integração totalmente integrada com a nuvem de Olá. Ao combinar a gestão de dados de armazenamento e da nuvem SAN uma plataforma de classe empresarial, os dispositivos StorSimple ativar velocidade, simplicidade e fiabilidade para todas as necessidades relacionadas com o armazenamento. |
| Energia e arrefecimento módulo (PCM) |Componentes de hardware do dispositivo StorSimple constituída por fontes de alimentação Olá e Olá arrefecimento ventoinha, Olá, por conseguinte, o módulo de energia e Cooling do nome. inclusão de primário Olá do dispositivo Olá tem dois 764W PCMs Olá bastidor EBOD tem dois 580W PCMs. |
| Inclusão principal |Inclusão principal do dispositivo StorSimple que contém os controladores de plataforma de aplicação Olá. |
| Objetivo de tempo de recuperação (RTO) |Olá período de tempo máximo que deve ser expended antes de um processo empresarial ou o sistema está totalmente restaurado depois de um desastre. |
| série attached SCSI (SAS) |Um tipo de unidade de disco rígido (HDD). |
| chave de encriptação de dados do serviço |Uma chave efetuadas dispositivo StorSimple novo tooany disponíveis que regista com Olá serviço StorSimple Manager do dispositivo. dados de configuração de Olá transferidos entre o serviço de Gestor de dispositivos do StorSimple Olá e dispositivo Olá são encriptados utilizando uma chave pública e, em seguida, podem ser desencriptados apenas no dispositivo Olá utilizando uma chave privada. Chave de encriptação de dados do serviço permite Olá serviço tooobtain esta chave privada para desencriptação. |
| Chave de registo do serviço |Uma chave que o ajuda a registar o dispositivo StorSimple Olá Olá serviço StorSimple Manager de dispositivo para que seja apresentado no Olá portal do Azure para obter ações de gestão. |
| Small Computer System Interface (SCSI) |Um conjunto de normas de fisicamente ligação de computadores e passar dados entre eles. |
| unidade de estado sólido (SSD) |Um disco que não contém as peças; Por exemplo, uma unidade flash. |
| conta de armazenamento |Um conjunto de credenciais de acesso tooyour ligado conta de armazenamento para um fornecedor de serviços de nuvem especificada. |
| Adaptador do StorSimple para o SharePoint |Um componente do Microsoft Azure StorSimple que expande transparente proteção de dados e armazenamento StorSimple tooSharePoint farms de servidores. |
| Serviço do Gestor de dispositivos do StorSimple |Uma extensão de Olá portal do Azure que permite-lhe toomanage o Azure StorSimple no local e os dispositivos virtuais. |
| Snapshot Manager do StorSimple |Snap-in uma consola de gestão da Microsoft (MMC) para gerir as operações de cópia de segurança e restauro no Microsoft Azure StorSimple. |
| Efetuar cópia de segurança |Uma funcionalidade que permite Olá utilizador tootake uma cópia de segurança interativa de um volume. É uma maneira alternativa de colocar uma cópia de segurança manual de um volume como tootaking oposição a uma cópia de segurança automatizada através de uma política definida. |
| Aprovisionamento dinâmico |Método de otimizar a eficiência de Olá com que Olá espaço de armazenamento disponível é utilizado em sistemas de armazenamento. No aprovisionamento dinâmico, o armazenamento de Olá é atribuído entre vários utilizadores com base no espaço mínimo Olá necessário por cada utilizador em qualquer momento. Consulte também *aprovisionamento fat*. |
| Criação de camadas |Arranging dados em agrupamentos lógicos com base na utilização atual, idade e os dados de tooother de relação. StorSimple dispõe automaticamente os dados em camadas. |
| Volume |Áreas de lógica de armazenamento apresentadas no formulário de Olá de unidades. Volumes do StorSimple correspondem os volumes de toohello montados pelo anfitrião Olá, incluindo as que são detetados através da utilização de Olá de iSCSI e um dispositivo StorSimple. |
| contentor de volume |Um agrupamento de volumes e definições de Olá que se aplicam toothem. Todos os volumes no dispositivo StorSimple estão agrupados em contentores de volume. Definições de contentor de volume incluem as contas de armazenamento, as definições de encriptação de dados enviados toocloud com chaves de encriptação associado e largura de banda consumida para operações que envolvem nuvem Olá. |
| grupo de volume |No Snapshot Manager do StorSimple, um grupo de volume é uma coleção de processamento de cópia de segurança de toofacilitate volumes configurados. |
| Serviço de cópia sombra de volumes (VSS) |Um serviço de sistema operativo Windows Server que facilita a consistência da aplicação ao comunicar com o suporte para VSS aplicações toocoordinate Olá a criação de instantâneos incrementais. VSS assegura que aplicações Olá estão temporariamente Inativas, quando são tirados instantâneos. |
| Windows PowerShell para StorSimple |Uma interface de linha de comandos baseada no Windows PowerShell utilizados toooperate e gerir o dispositivo StorSimple. Enquanto mantém algumas das funcionalidades básicas do Olá do Windows PowerShell, esta interface tem cmdlets dedicados adicionais que são adaptados para gerir um dispositivo StorSimple. |

## <a name="next-steps"></a>Passos seguintes
Saiba mais sobre [segurança do StorSimple](storsimple-8000-security.md).

