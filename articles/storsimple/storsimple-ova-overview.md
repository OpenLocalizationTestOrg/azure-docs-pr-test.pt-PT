---
title: "Descrição geral de matriz Virtual do Azure StorSimple aaaMicrosoft | Microsoft Docs"
description: "Descreve Olá StorSimple Virtual matriz, uma solução de armazenamento integrada que gere as tarefas de armazenamento entre uma matriz virtual no local e o armazenamento do Microsoft Azure na nuvem."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 169c639b-1124-46a5-ae69-ba9695525b77
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/09/2016
ms.author: alkohli
ms.openlocfilehash: 8978e074142940748857150cc93b37272349d53d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-storsimple-virtual-array"></a>Introdução toohello matriz Virtual StorSimple
## <a name="overview"></a>Descrição geral
Olá matriz Virtual do Microsoft Azure StorSimple é uma solução de armazenamento integrada que gere as tarefas de armazenamento entre uma matriz de virtual no local em execução num hipervisor e armazenamento de nuvem do Microsoft Azure. matriz virtual Olá é um servidor de ficheiros facilmente gerido, eficiente e económico ou uma solução de servidor de iSCSI que elimina muitos dos problemas de Olá e as despesas associadas a proteção de armazenamento e os dados da empresa. matriz virtual Olá é particularmente adequada para cenários de sucursais/office remoto.

Este tópico fornece uma descrição geral da matriz virtual Olá - aqui estão alguns outros recursos:

* Para melhores práticas, consulte [melhores práticas de matriz Virtual StorSimple](storsimple-ova-best-practices.md).
* Para obter uma descrição geral dos dispositivos de série de Olá 8000 do StorSimple, visite demasiado[série 8000 do StorSimple: uma solução de nuvem híbrida](storsimple-overview.md). 
* Para informações sobre dispositivos das séries Olá StorSimple 5000/7000, aceda demasiado[Ajuda Online do StorSimple](http://onlinehelp.storsimple.com/).

matriz virtual Olá suporta Olá iSCSI ou de um protocolo Server Message Block (SMB). Este é executado na sua infraestrutura existente do hipervisor e fornece camadas toohello na nuvem, cópia de segurança de nuvem, restauro rápido, recuperação ao nível do item e funcionalidades de recuperação após desastre.

Olá tabela seguinte resume as funcionalidades importantes do Olá de Olá matriz Virtual StorSimple.

| Funcionalidade | Matriz Virtual do StorSimple |
| --- | --- |
| Requisitos de instalação |Utiliza a infraestrutura de Virtualização (Hyper-V ou VMware) |
| Disponibilidade |Nó único |
| Capacidade total (incluindo a nuvem) |Se a capacidade de utilizável TB too64 por matriz virtual |
| Capacidade de local |Capacidade de utilizável too6.4 TB 390 GB por matriz virtual (necessidade tooprovision 500 GB too8 TB de espaço em disco) |
| Protocolos nativos |iSCSI ou SMB |
| Objetivo de tempo de recuperação (RTO) |iSCSI: inferior a 2 minutos, independentemente do tamanho do |
| Objetivo de ponto de recuperação (RPO) |Cópias de segurança diárias e cópias de segurança a pedido |
| A criação de camadas de armazenamento |Utiliza térmico toodetermine mapeamento os dados que devem ser colocado em camadas ou reduzir |
| Suporte |Infraestrutura de Virtualização suportada pelo fornecedor de Olá |
| Desempenho |Varia consoante a infraestrutura subjacente |
| Mobilidade de dados |Pode restaurar toohello mesmo dispositivo ou ao nível do item recovery (servidor de ficheiros) |
| Camadas de armazenamento |Armazenamento de hipervisor local e na nuvem |
| Tamanho da partilha |Em camadas: cópia de segurança too20 TB; afixado localmente: até too2 TB |
| Tamanho do volume |Em camadas: TB de too5 500 GB; afixado localmente: 50 GB de too500 GB |
| Tamanho do volume |Em camadas: cópia de segurança too5 TB; afixado localmente: até too500 GB |
| Instantâneos |Com falhas |
| Recuperação ao nível do item |Sim; os utilizadores podem restaurar a partir de partilhas |

## <a name="why-use-storsimple"></a>Porquê utilizar StorSimple?
StorSimple liga-se os utilizadores e os servidores de armazenamento de tooAzure em minutos, sem modificações de aplicação.

Olá tabela seguinte descreve algumas das principais vantagens do Olá esse Olá matriz Virtual StorSimple solução fornece.

| Funcionalidade | Vantagem |
| --- | --- |
| Integração transparente |matriz virtual Olá suporta Olá iSCSI ou de um protocolo SMB Olá. movimento de dados de Olá entre escalão local Olá e escalão de nuvem Olá é utilizador toohello totalmente integrada e transparente. |
| Custos de armazenamento reduzido |Com StorSimple, aprovisionar suficientes armazenamento local toomeet atual exigências para os dados Olá mais utilizado. Como aumentar necessidades de armazenamento, StorSimple camadas de dados amovíveis económica para armazenamento na nuvem. Olá é eliminação de duplicados e dados comprimidos antes de enviar toohello nuvem toofurther reduzir os requisitos de armazenamento e despesas. |
| Gestão de armazenamento simplificada |StorSimple fornece uma gestão centralizada na nuvem de Olá utilizando o Gestor de dispositivos do StorSimple toomanage vários dispositivos. |
| Recuperação após desastre melhorada e conformidade |StorSimple facilita a recuperação de desastres mais rápida, restaurar Olá metadados imediatamente e restaurar dados de Olá conforme necessário. Isto significa que as operações normais podem continuar com a mínima interrupção. |
| Mobilidade de dados |Nuvem toohello em camadas pode ser acedida de outros sites para fins de recuperação e de migração de dados. Tenha em atenção que pode restaurar os dados única toohello original virtual matriz. No entanto, utilizar desastre recuperação funcionalidades toorestore Olá matriz virtual completo tooanother virtual matriz. |

## <a name="storsimple-workload-summary"></a>Resumo da carga de trabalho do StorSimple

Um resumo das cargas de trabalho suportadas do StorSimple é apresentado abaixo.

|Cenário     |Carga de trabalho     |Suportado      |Restrições               |
|-------------|-------------|---------------|---------------------------|
|Colaboração de ROBO |Partilha de ficheiros     |Sim      |Consulte [os limites máximos para servidor de ficheiros](storsimple-ova-limits.md).<br></br>Consulte [requisitos de sistema para as versões suportadas do SMB](storsimple-ova-system-requirements.md).| Todas as versões     |

## <a name="workflows"></a>Fluxos de trabalho
Olá matriz Virtual StorSimple é particularmente adequado para Olá seguir fluxos de trabalho:

* [Gestão de armazenamento baseado na nuvem](#cloud-based-storage-management)
* [Independente de localização de cópia de segurança](#location-independent-backup)
* [Recuperação após desastre e proteção de dados](#data-protection-and-disaster-recovery)

### <a name="cloud-based-storage-management"></a>gestão de armazenamento baseado na nuvem
Pode utilizar o serviço do Gestor de dispositivos do StorSimple Olá em execução no Olá dados toomanage portal do Azure, armazenados em vários dispositivos e em vários locais. Isto é particularmente útil em cenários de sucursais distribuída. Tenha em atenção que tem de criar instâncias separadas de matrizes de toomanage de serviço StorSimple Manager de dispositivo do Olá virtual e físicos dispositivos StorSimple. Note também que matriz de virtual Olá utiliza agora o novo portal do Azure Olá em vez de Olá portal clássico do Azure.

![gestão de armazenamento baseado na nuvem](./media/storsimple-ova-overview/cloud-based-storage-management.png)

### <a name="location-independent-backup"></a>Independente de localização de cópia de segurança
Com a matriz de virtual Olá, instantâneos de nuvem fornecem uma cópia independente de localização, o ponto no tempo de um volume ou partilha. Instantâneos de nuvem estão ativados por predefinição e não podem ser desativados. Todos os volumes e partilhas são cópia de segurança cópias de segurança em Olá hora mesmo através de uma única política de cópia de segurança diária e pode efetuar cópias de segurança ad-hoc adicionais sempre que necessário.

### <a name="data-protection-and-disaster-recovery"></a>Recuperação após desastre e proteção de dados
matriz virtual Olá suporta Olá os seguintes cenários de recuperação após desastre e proteção de dados:

* **Restauro de volume ou partilha** – utilize restore Olá novo fluxo de trabalho toorecover um volume ou partilha. Utilize esta abordagem toorecover Olá todo volume ou a partilha.
* **Ao nível do item recuperação** – partilhas permitirem o acesso simplificado toorecent cópias de segurança. Pode recuperar facilmente um ficheiro individual de uma oferta especial de *.backup* pasta disponível na nuvem de Olá. Esta capacidade de restauro é suscitada pelo departamento de utilizador e é necessária nenhuma intervenção administrativa.
* **Recuperação após desastre** – utilize Olá toorecover de capacidade de ativação pós-falha de todos os volumes ou partilhas tooa novo virtual matriz. Criar a matriz de virtual novo Olá e registá-lo com Olá serviço StorSimple Manager de dispositivo e efetuar a ativação pós-falha de matriz de virtual original Olá. matriz de virtual novo Olá, em seguida, irão assumir recursos Olá aprovisionado. 

## <a name="storsimple-virtual-array-components"></a>Componentes de matriz Virtual StorSimple
matriz virtual Olá inclui Olá os seguintes componentes:

* [Matriz virtual](#virtual-array) – um dispositivo de armazenamento de nuvem híbrida com base numa máquina virtual aprovisionada no seu ambiente virtualizado ou hipervisor.  
* [Serviço do Gestor de dispositivos do StorSimple](#storsimple-device-manager-service) – uma extensão de Olá portal do Azure que lhe permite gerir um ou mais dispositivos StorSimple a partir de uma interface web único que pode aceder a partir de localizações geográficas diferentes. Pode utilizar toocreate de serviço do Gestor de dispositivos do StorSimple Olá e gerir serviços, ver e gerir dispositivos e alertas e gerir volumes, partilhas e instantâneos existentes.
* [Interface de utilizador local web](#local-web-user-interface) – uma IU baseada na web que é o dispositivo de Olá tooconfigure utilizado para que possam estabelecer a ligação de rede local toohello e, em seguida, registe dispositivos Olá com o serviço de Gestor de dispositivos do StorSimple Olá. 
* [Interface de linha de comandos](#command-line-interface) – uma interface do Windows PowerShell que pode utilizar toostart uma sessão de suporte na matriz virtual Olá.
  Olá secções seguintes descrevem cada um destes componentes em maior detalhe e explicam como solução de Olá dispõe de dados, atribui o armazenamento e facilita a gestão de armazenamento e da proteção de dados.

### <a name="virtual-array"></a>Matriz virtual
matriz virtual Olá é uma solução de armazenamento de nó único, que fornece armazenamento primário, gere a comunicação com o armazenamento na nuvem e ajuda a segurança de Olá tooensure e confidencialidade de todos os dados armazenados no dispositivo Olá.

matriz virtual Olá está disponível um modelo que está disponível para transferência. matriz virtual Olá tem uma capacidade máxima de 6.4 TB no dispositivo de Olá (com um requisito de armazenamento subjacente de 8 TB) e 64 TB, incluindo armazenamento na nuvem. 

matriz virtual Olá tem Olá seguintes funcionalidades:

* É económica. -Utilizam da sua infraestrutura de Virtualização existente e pode ser implementado na sua hipervisor existente de Hyper-V ou VMware.
* Este reside no datacenter de Olá e pode ser configurado como um servidor de iSCSI ou de um servidor de ficheiros. 
* Está integrado com a nuvem de Olá.
* As cópias de segurança são armazenadas na nuvem de Olá, o que pode facilitar a recuperação após desastre e simplificar a recuperação ao nível do item (ILR). 
* Pode aplicar atualizações toohello virtual matriz, o que pretende aplicá-las tooa de dispositivo físico.

> [!NOTE]
> Uma matriz de virtual não pode ser expandida. Por conseguinte, é importante tooprovision de armazenamento adequados ao criar matriz virtual Olá. 
> 
> 

### <a name="storsimple-device-manager-service"></a>Serviço do Gestor de dispositivos do StorSimple
Microsoft Azure StorSimple fornece uma interface de utilizador baseadas na web, Olá serviço Gestor de dispositivos do StorSimple, que permite toocentrally gerir armazenamento StorSimple. Pode utilizar Olá tooperform Olá Gestor de dispositivos do StorSimple serviço seguintes tarefas:

* Gerir várias matrizes de Virtual StorSimple a partir de um único serviço. 
* Configurar e gerir as definições de segurança para as matrizes de Virtual StorSimple. (Encriptação na nuvem de Olá está dependente de APIs do Microsoft Azure.)
* Configure as credenciais da conta de armazenamento e as propriedades.
* Configurar e gerir volumes ou partilhas.
* Criar cópias de segurança e restaurar dados em volumes ou partilhas.
* Monitorizar o desempenho.
* Reveja as definições do sistema e identificar informações sobre problemas possíveis.

Utilize Olá Gestor de dispositivos do StorSimple serviço tooperform diária administração da sua matriz virtual.

Para mais informações, visite demasiado[utilize Olá tooadminister de serviço do Gestor de dispositivos do StorSimple o dispositivo StorSimple](storsimple-virtual-array-manager-service-administration.md).

### <a name="local-web-user-interface"></a>Interface de utilizador local web
matriz virtual Olá inclui uma IU baseada na web que é utilizada para uma única configuração e o registo do dispositivo de Olá com Olá serviço StorSimple Manager do dispositivo. Pode utilizá-lo tooshut para baixo e reiniciar matriz virtual Olá, executar testes de diagnóstico, atualização de software, alterar a palavra-passe de administrador de dispositivo Olá, ver os registos do sistema e contacte a Microsoft Support toofile um pedido de serviço. 

Para obter informações sobre como utilizar Olá IU baseada na web, visite demasiado[utilize Olá tooadminister de IU baseada na web a matriz de Virtual StorSimple](storsimple-ova-web-ui-admin.md).

### <a name="command-line-interface"></a>Interface de linha de comandos
interface do Windows PowerShell Olá incluído permite-lhe tooinitiate uma sessão de suporte com Support da Microsoft para que o podem ajudar a resolver problemas que poderá encontrar na sua matriz virtual.

## <a name="storage-management-technologies"></a>Tecnologias de gestão de armazenamento
Além disso matriz virtual toohello e outros componentes, Olá StorSimple solução utiliza Olá os seguintes dados do software tecnologias tooprovide acesso rápido tooimportant, reduzir o consumo de armazenamento e proteger os dados armazenados na sua matriz virtual:

* [A criação de camadas de armazenamento automática](#automatic-storage-tiering) 
* [Volumes e partilhas afixadas localmente](#locally-pinned-shares-and-volumes)
* [A eliminação de duplicados e compressão de dados em camadas ou uma cópia de segurança toohello nuvem](#deduplication-and-compression-for-data-tiered/backed-up-to-the-cloud) 
* [Cópias de segurança agendadas e a pedido](#scheduled-and-on-demand-backups)

### <a name="automatic-storage-tiering"></a>A criação de camadas de armazenamento automática
matriz virtual Olá utiliza um novos dados de toomanage armazenado mecanismo camadas em Olá virtual matriz e Olá na nuvem. Existem apenas duas camadas: matriz de virtual local Olá e o Azure armazenamento na nuvem. Olá matriz Virtual StorSimple dispõe automaticamente dados em camadas Olá com base num mapa térmico, que controla a utilização, a idade e relações tooother dados. Dados que está a maioria dos Active Directory (hottest) estiver armazenado localmente, enquanto menos dados ativos e inativos são automaticamente migradas toohello nuvem. (Todas as cópias de segurança são armazenadas na nuvem de Olá.) StorSimple ajusta e reorganiza dados e altere as atribuições de armazenamento como padrões de utilização. Por exemplo, algumas informações podem ficar menos ativas ao longo do tempo. À medida que for progressivamente menos ativa, é camada saída toohello nuvem. Se esse mesmos dados ficam ativos novamente, está em camadas na matriz de armazenamento toohello.

Dados para um volume ou partilha em camadas específica são garantidos o seu próprio espaço de escalão local. (aproximadamente 10% do espaço aprovisionado total Olá para esse volume ou partilha). Enquanto esta reduz o armazenamento disponível de Olá numa matriz de virtual Olá para esse volume ou partilha, assegura que camadas para um volume ou partilha não serão afetadas pela necessidades de camadas de Olá das outras partilhas ou volumes. Assim uma carga de trabalho muito ocupada, uma partilha ou volume não é possível forçar todas as outra cargas de trabalho toohello na nuvem. 

![A criação de camadas de armazenamento automática](./media/storsimple-ova-overview/automatic-storage-tiering.png)

> [!NOTE]
> Pode especificar um volume afixado localmente como, caso em que os dados de Olá permanecem na matriz virtual Olá e nunca se camadas toohello nuvem. Para mais informações, visite demasiado[afixado localmente partilhas e os volumes](#locally-pinned-shares-and-volumes).
> 
> 

### <a name="locally-pinned-shares-and-volumes"></a>Volumes e partilhas afixadas localmente
Pode criar partilhas adequadas e como localmente afixados de volumes. Esta capacidade, assegura que dados requeridos por aplicações críticas permanecem na matriz virtual Olá nunca se camadas toohello nuvem. Partilhas afixadas localmente e volumes têm Olá seguintes funcionalidades: 

* Não são as latências toocloud do requerente ou problemas de conectividade.
* Ainda beneficiar do StorSimple cópia de segurança e desastre recuperação funcionalidades da nuvem.

Pode restaurar uma partilha afixada localmente ou volume como camadas ou uma partilha em camadas ou volume como localmente afixado. 

Para obter mais informações sobre volumes localmente afixados, visite demasiado[utilizar Olá Gestor de dispositivos do StorSimple serviço toomanage volumes](storsimple-virtual-array-manage-volumes.md).

### <a name="deduplication-and-compression-for-data-tiered-or-backed-up-toohello-cloud"></a>A eliminação de duplicados e compressão de dados em camadas ou uma cópia de segurança toohello nuvem
StorSimple utiliza a eliminação de duplicados e os dados compressão toofurther reduzir os requisitos de armazenamento na nuvem de Olá. A eliminação de duplicados reduz Olá quantidade global de dados armazenados através da eliminação de redundância no conjunto de dados de Olá armazenado. Como informação muda, StorSimple ignora os dados de Olá inalterado e capturas de Olá apenas as alterações. Além disso, o StorSimple reduz a quantidade de Olá dos dados armazenados ao identificar e remover informações duplicadas. 

> [!NOTE]
> Os dados armazenados nessa matriz virtual Olá não eliminação de duplicados ou não estão comprimidos. Todos os eliminação de duplicados e compressão ocorre antes de envio de dados de Olá toohello nuvem.
> 
> 

### <a name="scheduled-and-on-demand-backups"></a>Cópias de segurança agendadas e a pedido
Funcionalidades de proteção de dados do StorSimple permitem-lhe toocreate a pedido as cópias de segurança. Além disso, uma agenda de cópia de segurança predefinida assegura que dados é uma cópia de segurança diária. No formulário de Olá de instantâneos incrementais, que são armazenados na nuvem de Olá, são efetuadas cópias de segurança. Instantâneos, o qual gravar apenas alterações de Olá desde a última cópia de segurança Olá, podem ser criados e restaurados rapidamente. Estes instantâneos podem ser extremamente importantes em cenários de recuperação após desastre porque substituir sistemas de armazenamento secundário (por exemplo, a cópia de segurança de banda) e permitir toorestore dados tooyour datacenter ou tooalternate sites, se necessário.

## <a name="next-steps"></a>Passos seguintes
Saiba como demasiado[preparar o portal de matriz virtual Olá](storsimple-virtual-array-deploy1-portal-prep.md).

