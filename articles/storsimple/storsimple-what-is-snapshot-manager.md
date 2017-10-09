---
title: "aaaWhat é Snapshot Manager do StorSimple? | Microsoft Docs"
description: "Descreve Olá Snapshot Manager do StorSimple, respetiva arquitetura e as respetivas funcionalidades."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Um tooStorSimple de introdução do Snapshot Manager

## <a name="overview"></a>Descrição geral
Snapshot Manager do StorSimple é um snap-in Consola de gestão da Microsoft (MMC) que simplifica a gestão de cópia de segurança num ambiente do Microsoft Azure StorSimple e proteção de dados. Com o Snapshot Manager do StorSimple, pode gerir dados do Microsoft Azure StorSimple no Centro de dados de Olá e na nuvem de Olá como uma solução de armazenamento integrada único, assim simplificar processos de cópia de segurança e reduzindo os custos.

Esta descrição geral apresenta Olá Snapshot Manager do StorSimple, descreve as suas funcionalidades e explica a respetiva função no Microsoft Azure StorSimple. 

Para obter uma descrição geral do Olá todo Microsoft Azure StorSimple sistema, incluindo o dispositivo StorSimple Olá, o serviço StorSimple Manager, o Snapshot Manager do StorSimple e o adaptador do StorSimple para o SharePoint, consulte [série 8000 do StorSimple: uma nuvem híbrida solução de armazenamento](storsimple-overview.md). 

> [!NOTE]
> * Não é possível utilizar o Snapshot Manager do StorSimple toomanage Microsoft Azure StorSimple Virtual matrizes (também conhecido como StorSimple no local dispositivos virtuais).
> * Se planear tooinstall atualização 2 do StorSimple no dispositivo StorSimple, se toodownload Olá versão mais recente do Snapshot Manager do StorSimple e instalá-lo **antes de instalar a atualização 2 do StorSimple**. versão mais recente do Olá do Snapshot Manager do StorSimple é retrocompatível e funciona com todas as versões de lançamento do Microsoft Azure StorSimple. Se estiver a utilizar versão anterior do Olá do Snapshot Manager do StorSimple, terá de tooupdate it (não precisa de versão anterior do toouninstall Olá antes de instalar a nova versão de Olá).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Arquitetura e o objetivo do Snapshot Manager do StorSimple
Snapshot Manager do StorSimple fornece uma consola de gestão central que pode utilizar toocreate consistente, cópias de segurança de ponto no tempo da local e nuvem dados. Por exemplo, pode utilizar a consola Olá para:

* Configurar, fazer cópias de segurança e eliminar os volumes.
* Configurar o volume tooensure de grupos de segurança dos dados é consistente com aplicações.
* Gerir políticas de cópia de segurança para que os dados de cópias de segurança com base numa agenda predeterminada.
* Criar local e na nuvem instantâneos, o que podem ser armazenados na nuvem de Olá e utilizados para recuperação após desastre.

Olá Snapshot Manager do StorSimple obtém a lista de Olá de aplicações registado com o fornecedor VSS Olá no anfitrião de Olá. Em seguida, toocreate consistentes com aplicações as cópias de segurança, verifica os volumes de Olá utilizado por uma aplicação e sugere tooconfigure de grupos de volume. Snapshot Manager do StorSimple utiliza estes volume grupos toogenerate cópias de segurança que sejam consistentes com aplicações. (Consistência da aplicação existe quando todos os ficheiros e relacionados são sincronizadas e representam Olá estado verdadeiro da aplicação Olá num ponto específico no tempo de bases de dados.) 

Cópias de segurança do Snapshot Manager do StorSimple ter a forma de Olá de instantâneos incrementais, o que capturar apenas alterações de Olá desde a última cópia de segurança Olá. Como resultado, as cópias de segurança necessitam de menos armazenamento e podem ser criadas e restauradas rapidamente. Snapshot Manager do StorSimple utiliza tooensure do serviço de cópia (VSS) do Windows Volume sombra Olá que instantâneos capturar os dados consistentes com aplicações. (Para obter mais informações, visite toohello integração com a secção do serviço de cópia de sombra de volumes do Windows.) Com o Snapshot Manager do StorSimple, pode criar agendas de cópia de segurança ou fazer cópias de segurança de imediato, conforme necessário. Se precisar de toorestore dados a partir de uma cópia de segurança, permite do Snapshot Manager do StorSimple selecione catálogo de local ou instantâneos de nuvem. Azure StorSimple restaura apenas Olá os dados que é necessário, uma vez que é necessária, que impede que os atrasos na disponibilidade de dados durante as operações de restauro.)

![Arquitetura do Snapshot Manager do StorSimple](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Arquitetura do Snapshot Manager do StorSimple** 

## <a name="support-for-multiple-volume-types"></a>Suporte para vários tipos de volume
Pode utilizar Olá tooconfigure Snapshot Manager do StorSimple e cópia de segurança Olá tipos de volumes seguintes: 

* **Volumes básicos** – um volume básico é uma partição única num disco básico. 
* **Volumes simples** – um volume simple é um volume dinâmico que contém o espaço em disco a partir de um único disco dinâmico. Um volume simple é composta por uma única região num disco ou Olá de várias regiões que estejam ligadas em conjunto no mesmo disco. (Pode criar volumes simples apenas em discos dinâmicos.) Volumes simples não são tolerante a falhas.
* **Volumes dinâmicos** – um volume dinâmico é um volume criado num disco dinâmico. Discos dinâmicos utilizam uma base de dados tootrack sobre volumes que estão contidos nos discos dinâmicos no computador. 
* **Volumes dinâmicos com o espelhamento** – volumes dinâmicos com o espelhamento são criados numa arquitetura de Olá RAID 1. Com RAID 1, dados idênticos são escritos no disco dois ou mais, que produz um conjunto espelhado. Um pedido de leitura, em seguida, pode ser processado por qualquer disco que contém Olá pedida dados.
* **Volumes partilhados de cluster** – com volumes partilhados de cluster (CSVs), vários nós num cluster de ativação pós-falha podem em simultâneo de leitura ou escrita toohello mesmo disco. A ativação pós-falha do nó de tooanother de um nó pode ocorrer rapidamente, sem necessidade de uma alteração de propriedade da unidade ou montar, desmontar e remoção de um volume. 

> [!IMPORTANT]
> Não misture os CSVs e não CSVs no Olá instantâneo mesmo. Não é suportada a mistura de csv e não CSVs num instantâneo. 
> 
> 

Pode utilizar grupos de volume completo toorestore Snapshot Manager do StorSimple ou clonar volumes individuais e recuperar ficheiros individuais.

* [Volumes e grupos de volume](#volumes-and-volume-groups) 
* [Tipos de cópia de segurança e políticas de cópia de segurança](#backup-types-and-backup-policies) 

Para obter mais informações sobre as funcionalidades do Snapshot Manager do StorSimple e como toouse-las, consulte o artigo [interface de utilizador do Snapshot Manager do StorSimple](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Volumes e grupos de volume
Com o Snapshot Manager do StorSimple, pode criar volumes e, em seguida, configurá-los em grupos de volume. 

Snapshot Manager do StorSimple utiliza volume grupos toocreate cópias de segurança que sejam consistentes com aplicações. Consistência de aplicações existe quando todos os ficheiros e relacionados bases de dados estão sincronizados e representam Olá estado verdadeiro de uma aplicação num ponto específico no tempo. Grupos de volume (que são também conhecidos como *grupos de consistência*) Olá base de uma cópia de segurança ou restaurar a tarefa.

Grupos de volume não são Olá mesmo como contentores de volume. Um contentor de volume contém um ou mais volumes que partilham uma conta de armazenamento de nuvem e de outros atributos, por exemplo, o consumo de largura de banda e encriptação. Um contentor de volume único pode conter a segurança de volumes do StorSimple too256 com aprovisionamento dinâmico. Para obter mais informações sobre contentores de volume, visite demasiado[gerir os contentores de volume](storsimple-manage-volume-containers.md). Os grupos de volume são coleções de que configura toofacilitate operações de cópia de segurança de volumes. Se selecionar dois volumes que pertencem os contentores de volume toodifferent, colocá-los num grupo de único volume e, em seguida, criar uma política de cópia de segurança para esse grupo de volume, cada volume serão efetuadas cópias de no contentor de volume adequado Olá, utilizando o armazenamento adequado Olá conta.

> [!NOTE]
> Todos os volumes de um grupo de volume tem de ser de um fornecedor de serviços de nuvem única.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Integração com o serviço de cópia de sombra de volumes do Windows
Snapshot Manager do StorSimple utiliza Olá dados consistentes com aplicações do serviço de cópia (VSS) do Windows Volume sombra toocapture. VSS facilita a consistência de aplicações, ao comunicar com suporte para VSS aplicações toocoordinate Olá a criação de instantâneos incrementais. VSS assegura que aplicações Olá estão temporariamente inativa ou quiescent, quando são tirados instantâneos. 

implementação de Snapshot Manager do StorSimple Olá do VSS funciona com o SQL Server e os volumes NTFS genéricos. processo de Olá é o seguinte: 

1. Um requerente, o que é normalmente um gestão de dados e a solução de proteção (tais como Snapshot Manager do StorSimple) ou uma aplicação de cópia de segurança, invoca o VSS e pede-lhe-toogather informações do software de escritor Olá na aplicação de destino Olá.
2. Contactos VSS Olá escritor componente tooretrieve uma descrição dos dados de Olá. Escritor de Olá devolve descrição Olá Olá dados toobe uma cópia de segurança. 
3. VSS sinalizar Olá tooprepare Olá aplicação de escrita de cópia de segurança. Escritor de Olá prepara dados Olá para cópia de segurança, concluindo transações abertas, ao atualizar os registos de transações e assim sucessivamente e, em seguida, notifica VSS.
4. VSS dá instruções ao escritor Olá dados da aplicação do tootemporarily paragem Olá armazenam e certifique-se de que não são escritos dados no toohello volume enquanto a cópia de sombra Olá é criada. Este passo garante a consistência de dados e demora mais do que 60 segundos.
5. VSS instrui a cópia de sombra Olá fornecedor toocreate Olá. Fornecedores, que podem ser software - ou baseada em hardware, faça a gestão de volumes de Olá que estão atualmente em execução e criar cópias sombra das-los a pedido. fornecedor de Olá cria a cópia de sombra Olá e notifica o VSS quando for concluído.
6. Contactos Olá escritor toonotify Olá aplicação VSS que pode retomar a e/s e também tooconfirm que e/s foi colocada em pausa com êxito durante a sombra copiar criação. 
7. Se copiar Olá foi bem sucedida, o VSS devolve Olá requerente de toohello de localização da cópia. 
8. Se os dados foram escritos na enquanto foi criada a cópia de sombra Olá, cópia de segurança de Olá será inconsistente. VSS elimina a cópia de sombra Olá e notifica o requerente Olá. Olá requerente pode repetir o processo de cópia de segurança de Olá automaticamente ou notificar Olá administrador tooretry-la numa altura posterior.

Consulte Olá seguinte ilustração.

![Processo VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Processo de serviço de cópia de sombra de volumes do Windows** 

## <a name="backup-types-and-backup-policies"></a>Tipos de cópia de segurança e políticas de cópia de segurança
Com o Snapshot Manager do StorSimple, pode fazer uma cópia de segurança de dados e guarde-o localmente e na nuvem de Olá. Pode utilizar imediatamente Snapshot Manager do StorSimple tooback dos dados, ou pode utilizar uma política de cópia de segurança de toocreate uma agenda para fazer cópias de segurança automaticamente. Políticas de cópia de segurança também permitem-lhe toospecify instantâneos quantos serão mantidos. 

### <a name="backup-types"></a>Tipos de cópia de segurança
Pode utilizar Olá Snapshot Manager do StorSimple toocreate tipos de cópias de segurança seguintes:

* **Instantâneos locais** – instantâneos locais são cópias de ponto no tempo dos dados de volumes que estão armazenados no dispositivo do StorSimple Olá. Normalmente, este tipo de cópia de segurança pode ser criado e restaurado rapidamente. Pode utilizar um instantâneo local como faria com uma cópia de segurança local.
* **Instantâneos de nuvem** – os instantâneos de nuvem são cópias de ponto no tempo dos dados de volume que estão armazenados na nuvem de Olá. Um instantâneo na nuvem é equivalente instantâneo tooa replicado num sistema de armazenamento diferentes, fora das instalações. Os instantâneos de nuvem são particularmente útil em cenários de recuperação após desastre.

### <a name="on-demand-and-scheduled-backups"></a>Cópias de segurança a pedido e agendadas
Com o Snapshot Manager do StorSimple, pode iniciar uma única toobe de cópia de segurança criado imediatamente, ou pode utilizar um tooschedule de política de cópia de segurança recorrente operações de cópia de segurança.

Uma política de cópia de segurança é um conjunto de regras automatizadas que pode utilizar cópias de segurança regulares tooschedule. Uma política de cópia de segurança permite-lhe toodefine Olá frequência e parâmetros para tirar instantâneos de um grupo específico de volume. Pode utilizar políticas toospecify início e de expiração as datas, horas, frequências e os requisitos de retenção, para ambos os locais e instantâneos de nuvem. Uma política é aplicada imediatamente depois de defini-lo. 

Pode utilizar o Snapshot Manager do StorSimple tooconfigure ou reconfigurar as políticas de cópia de segurança sempre que necessário. 

Configurar Olá seguintes informações para cada política de cópia de segurança que criar:

* **Nome** – Olá número exclusivo de Olá selecionar política de cópia de segurança.
* **Tipo** – Olá o tipo de política de cópia de segurança; local instantâneo ou instantâneo na nuvem.
* **Grupo de volume** – Olá volume toowhich Olá selecionado cópia de segurança política de grupo está atribuída.
* **Retenção** – Olá número de cópias de segurança tooretain. Se selecionar Olá **todos os** caixa, todas as cópias de segurança são mantidas até for atingido o número máximo de Olá de cópias de segurança por volume, em que Olá de ponto de política irá falhar e gerar uma mensagem de erro. Em alternativa, pode especificar um número de cópias de segurança tooretain (entre 1 e 64).
* **Data** – data Olá quando a política de cópia de segurança de Olá foi criada.

Para informações sobre como configurar políticas de cópia de segurança, aceda demasiado[toocreate Snapshot Manager do StorSimple utilizar e gerir políticas de cópia de segurança](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Tarefa de cópia de segurança a monitorização e gestão
Pode utilizar Olá toomonitor Snapshot Manager do StorSimple e gerir tarefas de cópia de segurança futuras, agendadas e concluídas. Além disso, o Snapshot Manager do StorSimple fornece um catálogo de cópias de segurança too64 concluída cópias de segurança. Pode utilizar Olá catálogo toofind e restaurar volumes ou ficheiros individuais. 

Para informações sobre a monitorização de tarefas de cópia de segurança, aceda demasiado[tooview Snapshot Manager do StorSimple utilizar e gerir tarefas de cópia de segurança](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre [utilizando Snapshot Manager do StorSimple tooadminister solução StorSimple](storsimple-snapshot-manager-admin.md).
* Transferir [Snapshot Manager do StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

