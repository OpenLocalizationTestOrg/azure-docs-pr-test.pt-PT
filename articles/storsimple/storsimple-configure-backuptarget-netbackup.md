---
title: "série de aaaStorSimple 8000 como destino de cópia de segurança com NetBackup | Microsoft Docs"
description: "Descreve a configuração de destino de cópia de segurança do StorSimple Olá com Veritas NetBackup."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>StorSimple como destino de cópia de segurança com NetBackup

## <a name="overview"></a>Descrição geral

Azure StorSimple é uma solução de armazenamento de nuvem híbrida da Microsoft. StorSimple endereços complexidades Olá de crescimento de dados exponencial utilizando uma conta de armazenamento do Azure como uma extensão de Olá na solução no local e dados automaticamente em camadas através de armazenamento no local e na nuvem.

Neste artigo, discutimos a integração do StorSimple com Veritas NetBackup e melhores práticas para integrar ambas as soluções. Podemos também o tornam recomendações sobre como tooset segurança Veritas NetBackup toobest integrar com StorSimple. Iremos diferir tooVeritas melhores práticas, arquitetos de cópia de segurança e administradores para melhor forma tooset Olá dos requisitos de cópia de segurança individuais Veritas NetBackup toomeet e contratos de nível de serviço (SLAs).

Embora é ilustrar os passos de configuração e conceitos chave, este artigo não é de um guia passo a passo de instalação ou a configuração. Iremos partem do princípio de que os componentes básico Olá e infraestruturas estão por ordem de trabalho e toosupport pronto conceitos Olá dita.

### <a name="who-should-read-this"></a>Quem deve ler este artigo?

informações de Olá neste artigo será mais úteis toobackup administradores, administradores de armazenamento e arquitetos de armazenamento que tem conhecimento do armazenamento, Windows Server 2012 R2, Ethernet, cloud services e Veritas NetBackup.

### <a name="supported-versions"></a>Versões suportadas

-   NetBackup 7.7.x e versões posteriores
-   [StorSimple Update 3 e versões posteriores](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Por que motivo StorSimple como destino de cópia de segurança?

StorSimple é uma boa opção para um destino de cópia de segurança porque:

-   Fornece armazenamento standard, local de cópia de segurança de aplicações toouse como um destino de cópia de segurança rápida, sem quaisquer alterações. Também pode utilizar StorSimple para que um restauro rápido das cópias de segurança recentes.
-   A nuvem em camadas está totalmente integrado com um toouse de conta de armazenamento em nuvem do Azure económica Storage do Azure.
-   Automaticamente fornece armazenamento externo para recuperação após desastre.

## <a name="key-concepts"></a>Conceitos-chave

À semelhança de qualquer solução de armazenamento, uma avaliação tenha o cuidado de desempenho do armazenamento da solução de Olá, SLA, a taxa de alteração e as suas necessidades de crescimento de capacidade é toosuccess críticos. ideia principal Olá é que, introduzindo um escalão de nuvem, nuvem toohello tempos de acesso e throughputs desempenha uma função fundamental na capacidade de Olá do StorSimple toodo a tarefa.

StorSimple é concebida tooprovide armazenamento tooapplications que funciona num conjunto de trabalho bem definidos de dados (dados). Neste modelo, conjunto de trabalho de Olá dos dados armazenado em camadas locais Olá e hello restantes conjunto nonworking/frio/arquivados de dados em camadas toohello nuvem. Este modelo é representado na Olá figura a seguir. linha Olá quase flat verde representa dados de Olá armazenados em camadas locais do Olá de dispositivo do StorSimple Olá. Olá linha vermelha representa quantidade total de Olá dos dados armazenados em Olá solução StorSimple em todas as camadas. espaço de Olá entre linha Olá flat verde e em curva Olá exponencial vermelho representa a quantidade total de Olá dos dados armazenados na nuvem de Olá.

**Criação de camadas do StorSimple**
![diagrama camado do StorSimple](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

Com esta arquitetura em mente, encontrará que StorSimple é toooperate Idealmente adequada como destino de cópia de segurança. Pode utilizar StorSimple para:
-   Execute os restauros mais frequentes do conjunto de local trabalho Olá de dados.
-   Utilize nuvem Olá para recuperação de desastre num local externo e os dados mais antigos, onde são menos frequentes restauros.

## <a name="storsimple-benefits"></a>Vantagens do StorSimple

StorSimple fornece uma solução no local que está totalmente integrada com o Microsoft Azure, ao tirar partido da totalmente integrada aceder tooon local e armazenamento na nuvem.

StorSimple utiliza camadas automática entre dispositivos no local de Olá, que tem o dispositivo de estado sólido (SSD) e ligados à série armazenamento de SCSI (SAS) e armazenamento do Azure. Mantém camadas automática locais, em camadas SSD e SAS de Olá dados acedidos frequentemente. Move os dados acedidos com pouca frequência tooAzure armazenamento.

StorSimple oferece destas vantagens:

-   Algoritmos de eliminação de duplicados e compressão exclusivos que utilizam Olá nuvem tooachieve inédita níveis de eliminação de duplicados
-   Elevada disponibilidade
-   Georreplicação ao utilizar a georreplicação do Azure
-   Integração do Azure
-   Encriptação de dados na nuvem de Olá
-   Recuperação após desastre melhorada e conformidade

Embora StorSimple apresenta dois cenários de implementação principal (destino de cópia de segurança primário e secundário destino de cópia de segurança), fundamentalmente, é um dispositivo de armazenamento de blocos simples. StorSimple todas Olá compressão e a eliminação de duplicados. Perfeitamente envia e obtém dados entre Olá nuvem e de aplicação Olá e de sistema de ficheiros.

Para mais informações sobre StorSimple, consulte [série 8000 do StorSimple: solução de armazenamento de nuvem híbrida](storsimple-overview.md). Além disso, pode rever Olá [as especificações da série 8000 do StorSimple técnicas](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> Utilizar um StorSimple dispositivo como destino de cópia de segurança só é suportado para 3 de atualização de 8000 do StorSimple e versões posteriores.

## <a name="architecture-overview"></a>Descrição geral da arquitetura

Olá tabelas seguintes mostram Olá dispositivo modelo-arquitetura inicial documentação de orientação.

**As capacidades do StorSimple para locais e de armazenamento na nuvem**

| Capacidade de armazenamento       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| Capacidade de armazenamento local | &lt;10 TiB\*  | &lt;20 TiB\*  |
| Capacidade de armazenamento na nuvem | &gt;TiB de 200\* | &gt;500 TiB\* |
\*Tamanho de armazenamento parte do princípio de não eliminação de duplicados ou compressão.

**Capacidades do StorSimple para cópias de segurança primários e secundários**

| Cenário de cópia de segurança  | Capacidade de armazenamento local  | Capacidade de armazenamento na nuvem  |
|---|---|---|
| Cópia de segurança primária  | Cópias de segurança recentes armazenadas no armazenamento local para o objetivo de ponto de recuperação rápida toomeet recuperação (RPO) | Histórico de cópia de segurança (RPO) se adequa a capacidade de nuvem |
| Cópia de segurança secundária | Secundária cópia dos dados de cópia de segurança pode ser armazenada na capacidade de nuvem  | N/D  |

## <a name="storsimple-as-a-primary-backup-target"></a>StorSimple como um destino de cópia de segurança primário

Neste cenário, os volumes do StorSimple são apresentados toohello aplicação de cópia de segurança como repositório de único Olá para cópias de segurança. Olá figura a seguir mostra uma arquitetura de solução em que todas as cópias de segurança utilize StorSimple volumes em camadas para cópias de segurança e restauros.

![StorSimple como um diagrama lógico de destino de cópia de segurança primário](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Passos de lógica de cópia de segurança de destino principal

1.  contactos do servidor de cópia de segurança de Olá Olá agente de cópia de segurança de destino e o agente de cópia de segurança de Olá transmite o servidor de cópia de segurança de toohello de dados.
2.  servidor de cópia de segurança de Olá escreve dados toohello StorSimple volumes em camadas.
3.  servidor de cópia de segurança de Olá atualiza Olá catálogo da base de dados e, em seguida, concluir a tarefa de cópia de segurança de Olá.
4.  Um script de instantâneo aciona Olá snapshot manager do StorSimple (iniciar ou eliminar).
5.  servidor de cópia de segurança de Olá elimina expiradas cópias de segurança com base na política de retenção.

### <a name="primary-target-restore-logical-steps"></a>Passos de lógica de restauro de destino principal

1.  servidor de cópia de segurança de Olá inicia restaurar dados adequada Olá do repositório de armazenamento Olá.
2.  agente de cópia de segurança de Olá recebe dados de hello do servidor de cópia de segurança de Olá.
3.  servidor de cópia de segurança de Olá conclusão da tarefa de restauro Olá.

## <a name="storsimple-as-a-secondary-backup-target"></a>StorSimple como um destino de cópia de segurança secundário

Neste cenário, volumes do StorSimple principalmente são utilizados para a retenção de longa duração ou arquivar.

Olá figura seguinte mostra uma arquitetura em que cópias de segurança iniciais e restaura o volume de destino um elevado desempenho. Estas cópias de segurança são copiadas e arquivado tooa StorSimple camadas volume numa agenda definida.

É importante toosize o volume de elevado desempenho, para que as TI podem processar os requisitos de capacidade e o desempenho da política de retenção.

![StorSimple como um diagrama lógico de destino de cópia de segurança secundário](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Passos de lógica de cópia de segurança de destino secundária

1.  contactos do servidor de cópia de segurança de Olá Olá agente de cópia de segurança de destino e o agente de cópia de segurança de Olá transmite o servidor de cópia de segurança de toohello de dados.
2.  servidor de cópia de segurança de Olá escreve o armazenamento de desempenho toohigh de dados.
3.  servidor de cópia de segurança de Olá atualiza Olá catálogo da base de dados e, em seguida, concluir a tarefa de cópia de segurança de Olá.
4.  servidor de cópia de segurança de Olá copia tooStorSimple de cópias de segurança com base na política de retenção.
5.  Um script de instantâneo aciona Olá snapshot manager do StorSimple (iniciar ou eliminar).
6.  Olá cópia de segurança do servidor eliminações Olá expirou com base na política de retenção de cópias de segurança.

### <a name="secondary-target-restore-logical-steps"></a>Passos de lógica de restauro de destino secundária

1.  servidor de cópia de segurança de Olá inicia restaurar dados adequada Olá do repositório de armazenamento Olá.
2.  agente de cópia de segurança de Olá recebe dados de hello do servidor de cópia de segurança de Olá.
3.  servidor de cópia de segurança de Olá conclusão da tarefa de restauro Olá.

## <a name="deploy-hello-solution"></a>Implementar a solução de Olá

Implementar esta solução requer três passos:
1. Prepare a infraestrutura de rede Olá.
2. Implemente o dispositivo StorSimple como destino de cópia de segurança.
3. Implemente Veritas NetBackup.

Cada passo é abordado em detalhe no Olá secções a seguir.

### <a name="set-up-hello-network"></a>Configurar rede Olá

Uma vez StorSimple é uma solução que está integrada com Olá em nuvem do Azure, StorSimple requer um toohello de ligação do Active Directory e a funcionar em nuvem do Azure. Esta ligação é utilizada para operações como instantâneos de nuvem, gestão de dados e transferência de metadados e o armazenamento de nuvem de tooAzure de dados mais antigos, menos acedidos tootier.

Para Olá solução tooperform executadas de forma ideal, recomendamos que siga estas práticas recomendadas de rede:

-   ligação de Olá que estabelece ligação Olá StorSimple camada tooAzure têm de cumprir os requisitos de largura de banda. tooachieve, aplicar Olá adequada Quality of Service (QoS) tooyour nível infraestrutura comutadores toomatch o RPO e recuperação tempo SLAs de objetivo (RTO).

-   Latências de acesso de armazenamento de Blobs do Azure máximas devem ser cerca de 80 ms.

### <a name="deploy-storsimple"></a>Implementar StorSimple

Para orientações passo a passo de implementação StorSimple, consulte [implementar o dispositivo StorSimple no local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>Implementar NetBackup

Para orientações de implementação do 7.7.x de NetBackup passo a passo, consulte Olá [NetBackup 7.7.x documentação](http://www.veritas.com/docs/000094423).

## <a name="set-up-hello-solution"></a>Configurar a solução de Olá

Nesta secção, iremos demonstrar alguns exemplos de configuração. Olá recomendações e os exemplos seguintes mostram implementação mais básica e fundamentais de Olá. Esta implementação poderá não se aplica diretamente tooyour requisitos de cópia de segurança específicos.

### <a name="set-up-storsimple"></a>Configurar StorSimple

| Tarefas de implementação do StorSimple  | Comentários adicionais |
|---|---|
| Implemente o dispositivo StorSimple no local. | Versões suportadas: atualizar versões de 3 e posteriores. |
| Ative o destino de cópia de segurança de Olá. | Utilize estes comandos tooturn ou desativar o modo de destino de cópia de segurança e o estado de tooget. Para obter mais informações, consulte [ligar remotamente o dispositivo StorSimple tooa](storsimple-remote-connect.md).</br> tooturn no modo de cópia de segurança: `Set-HCSBackupApplianceMode -enable`. </br> tooturn desativar o modo de cópia de segurança: `Set-HCSBackupApplianceMode -disable`. </br> estado atual de Olá tooget das definições do modo de cópia de segurança: `Get-HCSBackupApplianceMode`. |
| Crie um contentor de volume comum para o volume que armazena dados de cópia de segurança de Olá. Todos os dados num contentor de volume tem eliminação de duplicados. | Contentores de volume do StorSimple definem domínios de eliminação de duplicados.  |
| Crie volumes do StorSimple. | Crie volumes com tamanhos como fechar toohello antecipado utilização quanto possível, porque o tamanho do volume afeta o tempo de duração de instantâneos de nuvem. Para obter informações sobre como toosize um volume, leia sobre [políticas de retenção](#retention-policies).</br> </br> Utilize StorSimple camadas volumes e selecione Olá **utilizar este volume para menos dados de arquivo acedidos com frequência** caixa de verificação. </br> Não é suportada apenas localmente afixado volumes a utilizar. |
| Crie uma política de cópia de segurança StorSimple exclusiva para todos os volumes de destino de cópia de segurança de Olá. | Uma política de cópia de segurança do StorSimple define o grupo de consistência de volume Olá. |
| Desactivar o agendamento de Olá como instantâneos de Olá expirarem. | Instantâneos são acionados como uma operação de pós-processamento. |

### <a name="set-up-hello-host-backup-server-storage"></a>Configurar o armazenamento de cópia de segurança do servidor de anfitrião Olá

Configure o armazenamento de cópia de segurança do servidor de anfitrião de Olá diretrizes toothese de acordo com:  

- Não utilize volumes expandidos (criados pela gestão de discos do Windows;) volumes expandidos não são suportados.
- Formate os volumes utilizando o NTFS com tamanho de alocação de 64 KB.
- Mapear os volumes do StorSimple Olá diretamente o toohello NetBackup servidor.
    - Utilize iSCSI para servidores físicos.
    - Utilize discos pass-through para servidores virtuais.


## <a name="best-practices-for-storsimple-and-netbackup"></a>Melhores práticas para StorSimple e NetBackup

Configure a sua solução de acordo com as diretrizes de toohello no Olá alguns secções a seguir.

### <a name="operating-system-best-practices"></a>Melhores práticas de sistema operativo

-   Desative a encriptação do Windows Server e eliminação de duplicados para o sistema de ficheiros NTFS Olá.
-   Desative uma desfragmentação do Windows Server em volumes do StorSimple Olá.
-   Desative o Windows Server indexação no Olá volumes do StorSimple.
-   Execute uma análise de antivírus no sistema anfitrião de origem Olá (não contra volumes do StorSimple Olá).
-   Desativar a predefinição de Olá [manutenção do Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) no Gestor de tarefas. Fazer isto dos Olá seguintes formas:
    - Desative configurador da manutenção Olá no programador de tarefas do Windows.
    - Transferir [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) do Windows Sysinternals. Depois de transferir PsExec, execute o Windows PowerShell como um administrador e escreva:
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Melhores práticas do StorSimple

-   Certifique-se de que o dispositivo StorSimple Olá é atualizado demasiado[atualização 3 ou posterior](storsimple-install-update-3.md).
-   Isolar tráfego iSCSI e na nuvem. Utilize ligações de iSCSI dedicado para o tráfego entre o servidor de cópia de segurança do StorSimple e Olá.
-   Lembre-se de que o dispositivo StorSimple é um destino de cópia de segurança dedicado. Cargas de trabalho mistas não são suportadas porque que afetam o RTO e RPO.

### <a name="netbackup-best-practices"></a>NetBackup melhores práticas

-   base de dados do Olá NetBackup deve ser a servidor local toohello e não reside num StorSimple volume.
-   Recuperação de desastres, fazer cópias de segurança base de dados do Olá NetBackup num StorSimple volume.
-   Suportamos NetBackup completas e incrementais cópias de segurança (também referida tooas diferencial cópias de segurança incrementais no NetBackup) para esta solução. Recomendamos que utilize sintéticas e cumulativas cópias de segurança incrementais.
-   Ficheiros de dados de cópia de segurança devem conter apenas Olá dados para uma tarefa específica. Por exemplo, sem suporte de dados acrescenta entre as diferentes tarefas são permitidas.

Para Olá mais recentes NetBackup definições e melhores práticas para implementar estes requisitos, consulte a documentação de NetBackup Olá em [www.veritas.com](https://www.veritas.com).


## <a name="retention-policies"></a>Políticas de retenção

Um dos tipos de política de retenção de cópias de segurança Olá mais comuns é uma política avô, Pai e filho (GFS). Uma política GFS, cópia de segurança incremental é executada diariamente em cópias de segurança completas terminadas semanais e mensais. Este resultados da política no StorSimple seis volumes em camadas: um volume contém Olá semanal, mensal e anual cópias de segurança completas; Olá outros cinco volumes armazenam cópias de segurança incrementais diárias.

No seguinte exemplo de Olá, utilizamos uma rotação GFS. exemplo de Olá assume seguinte Olá:

-   Dados comprimidos ou eliminação de não são utilizados.
-   Cópias de segurança completas são 1 TiB.
-   Cópias de segurança incrementais diárias são 500 GiB.
-   Cópias de segurança semanais quatro são mantidas durante um mês.
-   Cópias de segurança mensais doze são mantidas durante um ano.
-   Uma cópia de segurança anual é mantida para 10 anos.

Com base no Olá precedente pressupostos, cria um 26-TiB StorSimple camadas volume para Olá mensal e anual cópias de segurança completas. Criar um TiB 5 StorSimple volume em camadas para cada um dos Olá diária cópias de segurança incrementais.

| Retenção do tipo de cópia de segurança | Tamanho (TiB) | Multiplicador GFS\* | Capacidade total (TiB)  |
|---|---|---|---|
| Completa semanal | 1 | 4  | 4 |
| Diária incremental | 0.5 | 20 (ciclos igual número de semanas por mês) | 12 (2 para quota adicional) |
| Completa mensal | 1 | 12 | 12 |
| Completa anual | 1  | 10 | 10 |
| Requisito de GFS |   | 38 |   |
| Quota adicional  | 4  |   | 42 requisito GFS total  |
\*Olá multiplicador GFS é Olá número de cópias tem tooprotect e manter toomeet os requisitos de política de cópia de segurança.

## <a name="set-up-netbackup-storage"></a>Configurar o armazenamento de NetBackup

### <a name="tooset-up-netbackup-storage"></a>tooset NetBackup armazenamento

1.  Na consola de administração de NetBackup Olá, selecione **suportes de dados e gestão de dispositivos** > **dispositivos** > **agrupamentos de discos**. No Assistente de configuração do agrupamento de disco Olá, selecione o tipo de servidor de armazenamento de Olá **AdvancedDisk**e, em seguida, selecione **seguinte**.

    ![Consola de administração de NetBackup, o Assistente de configuração do agrupamento de disco](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Selecione o seu servidor e, em seguida, selecione **seguinte**.

    ![Consola de administração de NetBackup, servidor Olá selecione](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  Selecione o volume do StorSimple.

    ![Consola de administração de NetBackup, disco de volume do StorSimple Olá selecione](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Introduza um nome para o destino de cópia de segurança de Olá e, em seguida, selecione **seguinte** > **seguinte** Assistente de Olá toofinish.

5.  Reveja as definições de Olá e, em seguida, selecione **concluir**.

6.  No final de Olá de atribuição de cada volume, alterar Olá armazenamento dispositivo definições toomatch os recomendada na [melhores práticas para StorSimple e NetBackup](#best-practices-for-storsimple-and-netbackup).

7. Repita os passos 1-6 até tiver terminado de atribuir os volumes do StorSimple.

    ![Consola de administração de NetBackup, a configuração do disco](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurar StorSimple como um destino de cópia de segurança primário

> [!NOTE]
> Restauros de dados de uma cópia de segurança que foi toohello em camadas nuvem ocorrerem velocidades de nuvem.

Olá figura seguinte mostra mapeamento Olá de uma tarefa de cópia de segurança de tooa volume normal. Neste caso, cópias de segurança semanais Olá todos os mapeiam disco completo de Sábado toohello e cópias de segurança incrementais Olá mapeiam discos incremental tooMonday-sexta-feira. Olá todas as cópias de segurança e restauros são do StorSimple camadas volume.

![Diagrama lógico de configuração de destino de cópia de segurança primário ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemplo de agendar StorSimple como um destino de cópia de segurança primário GFS

Eis um exemplo de uma agenda de rotação GFS para quatro semanas, mensais e anuais:

| Tipo de frequência/cópia de segurança | Completo | Incremental (dias 1-5)  |   
|---|---|---|
| Semanal (1-4 de semanas) | Sábado | Segunda-sexta |
| Custo  | Sábado  |   |
| Anual | Sábado  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>Atribuir a tarefa cópia de segurança do StorSimple volumes tooa NetBackup

Olá seguir a sequência de parte do princípio de que anfitrião de destino NetBackup e Olá está configurado em conformidade com as diretrizes de agente do Olá NetBackup.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>tooassign StorSimple volumes tooa NetBackup tarefa de cópia

1.  Na consola de administração de NetBackup Olá, selecione **NetBackup gestão**, faça duplo clique **políticas**e, em seguida, selecione **nova política**.

    ![Consola de administração de NetBackup, crie uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  No Olá **adicionar uma nova política** caixa de diálogo, introduza um nome para a política de Olá e, em seguida, selecione Olá **Assistente de configuração de política de utilização** caixa de verificação. Selecione **OK**.

    ![Consola de administração de NetBackup, adicione uma caixa de diálogo nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  No Assistente de configuração de política de cópia de segurança Olá, elecionar Olá tipo de cópia de segurança que pretende e, em seguida, selecione **seguinte**.

    ![Consola de administração de NetBackup, selecione de tipo de cópia de segurança](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tooset Olá tipo de política, selecione **padrão**e, em seguida, selecione **seguinte**.

    ![Consola de administração de NetBackup, tipo de política selecione](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Selecione o anfitrião, selecione de Olá **detetar sistema operativo cliente** caixa de verificação e, em seguida, selecione **adicionar**. Selecione **seguinte**.

    ![Consola de administração de NetBackup, os clientes de lista numa política de novo](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Selecione unidades de Olá que pretende tooback cópias de segurança.

    ![Consola de administração de NetBackup, as seleções de cópia de segurança para uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Selecione a frequência de Olá e valores de retenção que satisfazem os requisitos de rotação de cópia de segurança.

    ![Consola de administração de NetBackup, a frequência de cópia de segurança e a rotação para uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Selecione **seguinte** > **seguinte** > **concluir**.  Pode modificar a agenda de Olá após criação da política Olá.

9.  Selecione a política de Olá de tooexpand que acabou de criar e, em seguida, selecione **agendas**.

    ![Consola de administração de NetBackup, agendas para uma nova política](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Clique com botão direito **valor diferencial Inc**, selecione **copiar toonew**e, em seguida, selecione **OK**.

    ![Consola de administração de NetBackup, nova política tooa da agenda de cópia](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Faça duplo clique agenda Olá recém-criado e, em seguida, selecione **alteração**.

12.  No Olá **atributos** separador, selecione de Olá **seleção de armazenamento de política de substituição** caixa de verificação e volume Olá, em seguida, selecione onde segunda-feira aceda cópias de segurança incrementais.

    ![Consola de administração de NetBackup, agenda de alteração](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  No Olá **iniciar janela** separador, a janela de tempo de Olá Selecione para as cópias de segurança.

    ![Consola de administração de NetBackup, janela de início de alteração](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  Selecione **OK**.

15.  Repita os passos 10-14 para cada cópia de segurança incremental. Selecione o volume adequado Olá e uma agenda para cada cópia de segurança que cria.

16.  Contexto Olá **valor diferencial Inc** agendar e elimine-o.

17.  Modificar o toomeet de agenda completa que tem da cópia de segurança.

    ![Consola de administração de NetBackup, agenda completa de alteração](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Janela de início de Olá de alteração.

    ![Consola de administração de NetBackup, janela de início de Olá de alteração](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  agenda final Olá tem o seguinte aspeto:

    ![Consola de administração de NetBackup, agenda final](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurar StorSimple como um destino de cópia de segurança secundário

> [!NOTE]
>Restauros de dados de uma cópia de segurança que foi toohello em camadas nuvem ocorrerem velocidades de nuvem.

Neste modelo, tem de ter um tooserve de suporte de dados (que não seja StorSimple) de armazenamento como uma cache temporária. Por exemplo, pode utilizar uma matriz redundante de espaço de tooaccommodate do volume de discos independentes (RAID), a entrada/saída (e/s) e a largura de banda. Recomendamos que utilize o RAID 5, 50 e 10.

Olá figura seguinte mostra típica curta duração retenção local (servidor toohello) volumes e retenção de longo prazo arquiva volumes. Neste cenário, todas cópias de segurança executam no Olá local (servidor toohello) o volume RAID. Estas cópias de segurança estão duplicadas periodicamente e tooan arquivado arquiva volume. Este é importante toosize local (servidor toohello) RAID de volume para que pode processar os requisitos de capacidade e o desempenho de retenção curta duração.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>StorSimple como um exemplo GFS secundário destino de cópia de segurança

![StorSimple como um diagrama lógico de destino de cópia de segurança secundário](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

tabela Olá seguinte mostra como tooset segurança toorun de cópias de segurança no local de Olá e os discos do StorSimple. Inclui os requisitos de capacidade individuais e total.

### <a name="backup-configuration-and-capacity-requirements"></a>Configuração de cópia de segurança e os requisitos de capacidade

| Tipo de cópia de segurança e retenção | Armazenamento configurados | Tamanho (TiB) | Multiplicador GFS | Total de capacidade\* (TiB) |
|---|---|---|---|---|
| Semana 1 (completas e incrementais) |Disco local (curto prazo)| 1 | 1 | 1 |
| StorSimple semanas 2 a 4 |Disco do StorSimple (longo prazo) | 1 | 4 | 4 |
| Completa mensal |Disco do StorSimple (longo prazo) | 1 | 12 | 12 |
| Completa anual |Disco do StorSimple (longo prazo) | 1 | 1 | 1 |
|Requisito de tamanho de volumes GFS |  |  |  | 18*|
\*Capacidade total inclui 17 TiB do StorSimple discos e 1 TiB de local RAID volume.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Agenda de exemplo GFS: rotação GFS agenda semanal, mensal e anual

| Semana | Completo | Dia incremental 1 | Dia incremental 2 | Dia incremental 3 | Dia incremental 4 | Dia incremental 5 |
|---|---|---|---|---|---|---|
| Semana 1 | Local RAID volume  | Local RAID volume | Local RAID volume | Local RAID volume | Local RAID volume | Local RAID volume |
| Semana 2 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Semana 3 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Semana 4 | StorSimple semanas 2 a 4 |   |   |   |   |   |
| Custo | Mensalmente StorSimple |   |   |   |   |   |
| Anual | Anualmente StorSimple  |   |   |   |   |   |   |


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Atribuir StorSimple volumes tooa NetBackup arquivo e duplicação tarefa

Porque NetBackup oferecem uma vasta gama de opções para gestão de armazenamento e suportes de dados, recomendamos que consulte com Veritas ou o tooproperly de arquiteto NetBackup avaliar os requisitos de política (SLP) do ciclo de vida de armazenamento.

Depois de definir os conjuntos de inicial do disco de Olá, toodefine três políticas de ciclo de vida de armazenamento adicional, é necessário para um total de quatro políticas:
* LocalRAIDVolume
* StorSimpleWeek2 4
* StorSimpleMonthlyFulls
* StorSimpleYearlyFulls

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>tooassign StorSimple volumes tooa NetBackup arquivo e duplicação tarefa

1.  Na consola de administração de NetBackup Olá, selecione **armazenamento** > **políticas de ciclo de vida de armazenamento** > **nova política de ciclo de vida de armazenamento**.

    ![Consola de administração de NetBackup, nova política de ciclo de vida de armazenamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Introduza um nome para o instantâneo de Olá e, em seguida, selecione **adicionar**.

3.  No Olá **nova operação** caixa de diálogo Olá **propriedades** separador, para **operação**, selecione **cópia de segurança**. Selecione os valores de Olá que pretende para **armazenamento de destino**, **tipo retenção**, e **período de retenção**. Selecione **OK**.

    ![Consola de administração de NetBackup, caixa de diálogo de operação de novo](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Isto define a operação de cópia de segurança primeiro Olá e repositório.

4.  Selecione toohighlight Olá anterior operação e, em seguida, selecione **adicionar**. No Olá **operação de armazenamento de alteração** caixa de diálogo, os valores de Olá selecione que pretende para **armazenamento de destino**, **tipo retenção**, e **período de retenção** .

    ![Consola de administração de NetBackup, caixa de diálogo de operação de armazenamento de alteração](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Selecione toohighlight Olá anterior operação e, em seguida, selecione **adicionar**. No Olá **nova política de ciclo de vida de armazenamento** diálogo caixa, adicione as cópias de segurança mensais durante um ano.

    ![Consola de administração de NetBackup, caixa de diálogo nova política de ciclo de vida de armazenamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Repita os passos 4 a 5 até criou Olá abrangente SLP política de retenção que precisa.

    ![Consola de administração de NetBackup, adicionar políticas na caixa de diálogo Olá nova política de ciclo de vida de armazenamento](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Quando tiver terminado de definir a política de retenção SLP em **política**, definir uma política de cópia de segurança, seguindo os passos de Olá detalhados [tarefa cópia de segurança do StorSimple atribuir volumes tooa NetBackup](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  Em **agendas**, no Olá **agendamento da alteração** caixa de diálogo, clique com botão direito **completa**e, em seguida, selecione **alteração**.

    ![Consola de administração de NetBackup, caixa de diálogo agenda de alteração](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Selecione Olá **seleção de armazenamento de política de substituição** caixa de verificação e a política de retenção SLP Olá, em seguida, selecione que criou nos passos 1-6.

    ![Consola de administração de NetBackup, seleção de armazenamento de política de substituição](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Selecione **OK**e, em seguida, repita para a agenda de cópia de segurança incrementais Olá.

    ![Consola de administração de NetBackup, caixa de diálogo de alteração de agenda para cópias de segurança incrementais](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Retenção do tipo de cópia de segurança | Tamanho (TiB) | Multiplicador GFS\* | Capacidade total (TiB)  |
|---|---|---|---|
| Completa semanal |  1  |  4 | 4  |
| Diária incremental  | 0.5  | 20 (ciclos são toohello igual número de semanas por mês) | 12 (2 para quota adicional) |
| Completa mensal  | 1 | 12 | 12 |
| Completa anual | 1  | 10 | 10 |
| Requisito de GFS  |     |     | 38 |
| Quota adicional  | 4  |    | 42 requisito GFS total |
\*Olá multiplicador GFS é Olá número de cópias tem tooprotect e manter toomeet os requisitos de política de cópia de segurança.

## <a name="storsimple-cloud-snapshots"></a>Instantâneos de nuvem do StorSimple

Instantâneos de nuvem do StorSimple protegem dados de Olá que residem no seu dispositivo StorSimple. Criar um instantâneo na nuvem é das instalações do tooshipping equivalente bandas de cópia de segurança local tooan noutro local. Se utilizar o armazenamento com redundância geográfica do Azure, criar um instantâneo na nuvem é sites de toomultiple tooshipping equivalente bandas de cópia de segurança. Se precisar de um dispositivo de toorestore depois de um desastre, poderá colocar o dispositivo StorSimple outro online e efetue uma ativação pós-falha. Após a ativação pós-falha de Olá, seria capaz de tooaccess dados Olá (velocidades de nuvem) do instantâneo na nuvem mais recente do Olá.

Olá seguinte secção descreve como toocreate toostart um script de curto e delete StorSimple cloud instantâneos durante o pós-processamento de cópia de segurança.

> [!NOTE]
> Instantâneos manualmente ou programaticamente criados não siga a política de expiração de instantâneo do Olá StorSimple. Estes instantâneos tem de ser manualmente ou programaticamente eliminados.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Iniciar e eliminar os instantâneos de nuvem utilizando um script

> [!NOTE]
> Avalie cuidadosamente repercussions de retenção de dados e de conformidade de Olá antes de eliminar um instantâneo do StorSimple. Para obter mais informações sobre como toorun um script pós-cópia de segurança, consulte Olá [NetBackup documentação](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>Ciclo de vida de cópia de segurança

![Diagrama de ciclo de vida de cópia de segurança](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

### <a name="requirements"></a>Requisitos

-   servidor de Olá que executa o script de Olá tem de ter acesso tooAzure recursos da nuvem.
-   conta de utilizador Olá tem de ter as permissões necessárias Olá.
-   Uma política de cópia de segurança do StorSimple com Olá associados StorSimple volumes devem ser configurar, mas não ativados.
-   Terá de Olá nome de recurso do StorSimple, chave de registo, nome do dispositivo e ID de política de cópia de segurança.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart ou eliminar um instantâneo na nuvem

1.  [Instalar o Azure PowerShell](/powershell/azure/overview).
2.  [Transferir e importar publicar definições e informações de subscrição](https://msdn.microsoft.com/library/dn385850.aspx).
3.  No portal clássico do Azure de Olá, obter o nome do recurso Olá e [chave de registo para o serviço StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  No servidor de Olá que executa o script de Olá, execute o PowerShell como administrador. Escreva este comando:

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    ID de política de cópia de segurança de Olá nota
5.  No bloco de notas, crie um novo script do PowerShell, utilizando Olá seguinte código.

    Copie e cole o fragmento de código:
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Guardar toohello de script do PowerShell Olá mesma localização onde guardou o Azure definições de publicação. Por exemplo, guarde como C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Adicione a tarefa de cópia de segurança Olá script tooyour no NetBackup. toodo este, edite o NetBackup de tarefa opções pré-processadas e processamento pós-cópia de comandos.

> [!NOTE]
> Recomendamos que execute a sua política de cópia de segurança de instantâneos de nuvem StorSimple como um script de pós-processamento no fim de Olá da tarefa de cópia de segurança diária. Para obter mais informações sobre como tooback cópias de segurança e restauro sua toohelp de ambiente de aplicação de cópia de segurança a corresponder aos seus RPO e RTO, consulte com o arquiteto de sistemas de cópia de segurança.

## <a name="storsimple-as-a-restore-source"></a>StorSimple como uma origem de restauro

Restaura a partir de um trabalho do dispositivo StorSimple como restaura a partir de qualquer dispositivo de armazenamento de blocos. Ocorre restauros dos dados que está em camadas toohello nuvem velocidades de nuvem. Para os dados locais, restauros ocorrerem à velocidade de disco local Olá do dispositivo Olá. Para obter informações sobre como tooperform um restauro, consulte Olá [NetBackup documentação](http://www.veritas.com/docs/000094423). Recomendamos que estar em conformidade tooNetBackup restauro melhores práticas.

## <a name="storsimple-failover-and-disaster-recovery"></a>StorSimple ativação pós-falha e recuperação após desastre

> [!NOTE]
> Para cenários de destino de cópia de segurança, o dispositivo de nuvem do StorSimple não é suportado como um destino de restauro.

Um desastre pode ser causado por vários fatores. Olá, a tabela seguinte apresenta uma lista de cenários de recuperação após desastre comuns.

| Cenário | Impacto | Como toorecover | Notas |
|---|---|---|---|
| Falha de dispositivo do StorSimple | Operações de cópia de segurança e restauro sejam interrompidas. | Substitua o dispositivo de falha de Olá e efetuar [StorSimple ativação pós-falha e recuperação após desastre](storsimple-device-failover-disaster-recovery.md). | Se precisar de tooperform um restauro após a recuperação de dispositivo, conjuntos de trabalho completo de dados são obtidos a partir Olá nuvem toohello nova o dispositivo. Todas as operações são velocidades de nuvem. catálogo reanálise da processo e o índice de Olá poderão fazer com que todos os conjuntos de cópia de segurança toobe, analisados e retirado da Olá camada toohello dispositivo local escalão de nuvem, que pode ser um processo moroso. |
| Falha do servidor NetBackup | Operações de cópia de segurança e restauro sejam interrompidas. | Reconstruir o servidor de cópia de segurança de Olá e efetuar o restauro de base de dados. | Tem de reconstruir ou restaurar Olá NetBackup servidor no site de recuperação de desastre Olá. Olá da base de dados toohello mais recente ponto de restauro. Se hello base de dados restaurada NetBackup não está sincronizada com as suas tarefas de cópia de segurança mais recentes, a indexação e cataloging são necessário. Este índice e o catálogo de reanálise da processo poderão fazer com que todos os conjuntos de cópia de segurança toobe, analisados e retirado da camada de dispositivo local Olá nuvem camada toohello. Isto torna mais tempo intensivas. |
| Falha do site que resulte em perda de hello do servidor de cópia de segurança de Olá e StorSimple | Operações de cópia de segurança e restauro sejam interrompidas. | Restaurar StorSimple primeiro e, em seguida, restaure NetBackup. | Restaurar StorSimple primeiro e, em seguida, restaure NetBackup. Se precisar de tooperform um restauro após a recuperação de dispositivo, conjuntos de trabalho de dados completa Olá são obtidos a partir Olá nuvem toohello nova o dispositivo. Todas as operações são velocidades de nuvem. |

## <a name="references"></a>Referências

Olá seguintes documentos foram referenciado para este artigo:

- [Configuração de e/s multipath do StorSimple](storsimple-configure-mpio-windows-server.md)
- [Cenários de armazenamento: aprovisionamento dinâmico](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Utilizar o GPT unidades](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Configurar cópias sombra para pastas partilhadas](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Passos seguintes

- Saiba mais sobre como demasiado[restauro a partir de um conjunto de cópia de segurança](storsimple-restore-from-backup-set-u2.md).
- Saiba mais sobre como tooperform [dispositivo ativação pós-falha e recuperação após desastre](storsimple-device-failover-disaster-recovery.md).
