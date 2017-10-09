---
title: "Servidor de cópia de segurança do Azure de aaaUse tooback segurança portal clássico do cargas de trabalho tooAzure | Microsoft Docs"
description: "Certifique-se de que o seu ambiente é devidamente preparado tooback utilizando o servidor de cópia de segurança do Azure de cargas de trabalho"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "servidor do backup do Azure; Cofre de cópia de segurança"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>A preparar tooback utilizando o servidor de cópia de segurança do Azure de cargas de trabalho
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Servidor do Backup do Azure (clássica)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clássica)](backup-azure-dpm-introduction-classic.md)
>
>

Este artigo é sobre a preparação do tooback ambiente utilizando o servidor de cópia de segurança do Azure de cargas de trabalho. Com o servidor de cópia de segurança do Azure, pode proteger cargas de trabalho de aplicações como VMs de Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange e clientes Windows de uma única consola.

> [!WARNING]
> Servidor do Backup do Azure herda a funcionalidade de Olá do Data Protection Manager (DPM) para cópia de segurança da carga de trabalho. Encontrará ponteiros tooDPM documentação para algumas dessas funcionalidades. No entanto servidor de cópia de segurança do Azure não fornecer proteção em banda ou integrar com o System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Computador Windows Server
![step1](./media/backup-azure-microsoft-azure-backup/step1.png)

primeiro passo de Olá para obter hello do servidor de cópia de segurança do Azure, cópias de segurança e em execução é toohave computador Windows Server.

| Localização | Requisitos mínimos | Instruções adicionais |
| --- | --- | --- |
| Azure |Máquina de virtual IaaS do Azure<br><br>A2 Padrão: 2 núcleos, 3.5GB de RAM |Pode começar com uma imagem de galeria simples do Windows Server 2012 R2 Datacenter. [Proteger cargas de trabalho de IaaS com o servidor de cópia de segurança do Azure (DPM)](https://technet.microsoft.com/library/jj852163.aspx) tem muitas nuances. Certifique-se de que lê o artigo de Olá completamente antes de implementar a máquina Olá. |
| Local |VM de Hyper-V,<br> VM de VMWare<br> ou um anfitrião físico.<br><br>2 núcleos e 4GB de RAM |Pode eliminar o duplicados armazenamento do DPM Olá através de eliminação de duplicados do Windows Server. Saiba mais sobre como [DPM e eliminação de duplicados](https://technet.microsoft.com/library/dn891438.aspx) funcionam em conjunto, quando implementados em VMs de Hyper-V. |

> [!NOTE]
> Recomenda-se que o servidor de cópia de segurança do Azure seja instalado num computador com o Windows Server 2012 R2 Datacenter. Muitos dos pré-requisitos de Olá são abrangidos automaticamente com a versão mais recente do Olá do sistema de operativo do Windows hello.
>
>

Se pretender que o domínio de tooa toojoin servidor de cópia de segurança do Azure, é recomendado que associe o servidor físico Olá ou domínio de toohello de máquina virtual antes de instalar o software de servidor de cópia de segurança do Azure Olá. Mover um servidor de cópia de segurança do Azure tooa novo domínio, após a implementação, é *não suportado*.

## <a name="2-backup-vault"></a>2. Cofre de cópia de segurança
![step2](./media/backup-azure-microsoft-azure-backup/step2.png)

Quer enviar dados de cópia de segurança tooAzure ou mantenha-o localmente, hello do servidor de cópia de segurança do Azure tem de ser registado tooa cofre. Se for um novo utilizador de cópia de segurança do Azure e pretender toouse servidor de cópia de segurança do Azure, consulte Olá Azure portal versão deste artigo - [preparar tooback utilizando o servidor de cópia de segurança do Azure de cargas de trabalho](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> A partir de Março de 2017, já não pode utilizar cofres de cópia de segurança Olá toocreate portal clássico.
> Agora pode atualizar os cópia de segurança cofres tooRecovery os cofres dos serviços. Para obter mais informações, consulte o artigo de Olá [atualizar um tooa do Cofre de cópia de segurança do cofre dos serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft encoraja tooupgrade a cópia de segurança cofres dos cofres dos serviços de tooRecovery.<br/> Após 15 de Outubro de 2017, não é possível utilizar cofres de cópia de segurança de toocreate do PowerShell. **Até 1 de novembro de 2017**:
>- Todos os cofres de cópia de segurança restantes serão os cofres dos serviços de tooRecovery automaticamente atualizado.
>- Não será capaz de tooaccess os dados de cópia de segurança no portal clássico Olá. Em vez disso, utilize Olá tooaccess portal do Azure os dados de cópia de segurança cofres dos serviços de recuperação.
>



## <a name="3-software-package"></a>3. Pacote de software
![passo 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Transferir o pacote de software Olá
Credenciais de toovault semelhantes, pode transferir a cópia de segurança do Microsoft Azure para cargas de trabalho de aplicação de Olá **página início rápido** do Cofre de cópias de segurança de Olá.

1. Clique em **para aplicação cargas de trabalho (disco tooDisk tooCloud)**. Esta ação irá demorar toohello página de centro de transferências a partir de onde o pacote de software Olá pode ser transferido.

    ![Ecrã de boas-vindas cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Clique em **Transferir**.

    ![1 do Centro de transferências](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Selecione todos os ficheiros de Olá e clique em **seguinte**. Olá, transferência que Olá todos os ficheiros feitos página de transferência do Microsoft Azure Backup Olá e coloque Olá todos os ficheiros na mesma pasta.
   ![1 do Centro de transferências](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Uma vez que hello tamanho de transferência de todos os ficheiros de Olá em conjunto > 3G, uma ligação de transferência de 10 Mbps que esta operação pode demorar too60 minutos para Olá transferem toocomplete.

### <a name="extracting-hello-software-package"></a>Extrair o pacote de software Olá
Depois de transferir todos os ficheiros de Olá, clique em **MicrosoftAzureBackupInstaller.exe**. Esta ação iniciará Olá **Assistente de configuração de cópia de segurança do Microsoft Azure** ficheiros de configuração de Olá tooextract localização tooa especificada por si. Continuar com o Assistente de Olá e clique em Olá **extrair** botão o processo de extração de Olá toobegin.

> [!WARNING]
> Pelo menos 4GB de espaço livre é ficheiros de configuração de Olá tooextract necessária.
>
>

![Assistente de configuração de cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Uma vez processo de extração Olá concluído, verifique Olá caixa toolaunch Olá raiz extraídos *setup.exe* toobegin instalar o servidor de cópia de segurança do Microsoft Azure e clique em Olá **concluir** botão.

### <a name="installing-hello-software-package"></a>Instalar o pacote de software Olá
1. Clique em **cópia de segurança do Microsoft Azure** Assistente de configuração de Olá toolaunch.

    ![Assistente de configuração de cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. No ecrã de boas-vindas Olá clique Olá **seguinte** botão. Isto leva-o toohello *verificações de pré-requisitos* secção. Neste ecrã, clique em Olá **verifique** botão toodetermine se tiverem sido cumpridos os pré-requisitos de hardware e software Olá cópia de segurança do servidor do Azure. Se todos os Olá pré-requisitos estão tiverem sido cumpridos com êxito, verá uma mensagem a indicar que a máquina Olá cumpre os requisitos de Olá. Clique em Olá **seguinte** botão.

    ![Verificação do servidor de cópia de segurança do Azure - boas-vindas e pré-requisitos](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Servidor de cópia de segurança do Microsoft Azure requer o SQL Server Standard e pacote de instalação do servidor de cópia de segurança do Azure Olá inclui integrados em binários Olá adequados do SQL Server necessários. Ao iniciar com uma nova instalação do servidor de cópia de segurança do Azure, deve escolher a opção de Olá **instalar um novo instância do SQL Server com esta configuração** e clique em Olá **verificar e instalar** botão. Depois de pré-requisitos de Olá são instalados com êxito, clique em **seguinte**.

    ![Servidor de cópia de segurança do Azure - verificação do SQL Server](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Se ocorrer uma falha com uma máquina de Olá toorestart recomendação, o que pretende e clique em **verifique novamente**.

   > [!NOTE]
   > Servidor de cópia de segurança do Azure não irá funcionar com uma instância remota do SQL Server. instância de Olá que está a ser utilizada pelo servidor de cópia de segurança do Azure tem toobe local.
   >
   >

4. Forneça uma localização para instalação de Olá dos ficheiros do servidor de cópia de segurança do Microsoft Azure e clique em **seguinte**.

    ![PreReq2 de cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    localização de scratch Olá é um requisito para cópia de segurança tooAzure. Certifique-se localização scratch Olá, pelo menos, 5% de dados de Olá planeada toobe uma cópia de segurança toohello nuvem. Para a proteção de disco, discos separados necessário toobe configurado depois de concluída a instalação de Olá. Para obter mais informações sobre agrupamentos de armazenamento, consulte [configurar agrupamentos de armazenamento e armazenamento em disco](https://technet.microsoft.com/library/hh758075.aspx).
5. Forneça uma palavra-passe segura para contas de utilizador locais restritas e clique em **seguinte**.

    ![PreReq2 de cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Selecione se pretende toouse *Microsoft Update* toocheck para as atualizações e clique em **seguinte**.

   > [!NOTE]
   > Recomenda-se ter o Windows Update redirecionar tooMicrosoft atualização, o que oferece segurança e atualizações importantes para o Windows e outros produtos, como o servidor de cópia de segurança do Microsoft Azure.
   >
   >

    ![PreReq2 de cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Olá revisão *resumo de definições* e clique em **instalar**.

    ![PreReq2 de cópia de segurança do Microsoft Azure](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. instalação de Olá ocorre fases. No Olá de fase primeiro Olá Microsoft Azure Recovery Services Agent está instalado no servidor de Olá. Assistente de Olá também verifica a conectividade à Internet. Se a conectividade à Internet está disponível para poder continuar com a instalação, caso contrário, terá de tooprovide proxy detalhes tooconnect toohello Internet.

    Olá passo seguinte consiste em tooconfigure Olá Microsoft Azure Recovery Services Agent. Como parte da configuração de Olá, terá de tooprovide sua Olá cofre credenciais tooregister Olá máquina toohello cofre cópias de segurança. Também irá fornecer uma frase de acesso de dados de Olá da tooencrypt/desencriptação enviados entre o Azure e o local. Automaticamente pode gerar uma frase de acesso ou fornecer a suas próprias mínimo frase de acesso de 16 caracteres. Continue com o Assistente de Olá até Olá agente foi configurada.

    ![PreReq2 Serer de cópia de segurança do Azure](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Após a conclusão com êxito do registo do servidor de cópia de segurança do Microsoft Azure Olá, hello Assistente de configuração geral prossegue toohello instalação e configuração do SQL Server e componentes de servidor de cópia de segurança do Azure Olá. Uma vez concluída a instalação de componentes do SQL Server de Olá, os componentes de servidor de cópia de segurança do Azure de Olá estão instalados.

    ![Servidor do Backup do Azure](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Quando concluir o passo de instalação de Olá, hello ícones de ambiente de trabalho do produto irão ter sido criados, bem como. Apenas, faça duplo clique produto de Olá Olá ícone toolaunch.

### <a name="add-backup-storage"></a>Adicionar armazenamento de cópia de segurança
Olá primeira cópia de segurança é mantida no armazenamento ligado toohello máquina do servidor de cópia de segurança do Azure. Para obter mais informações sobre a adição de discos, consulte [configurar agrupamentos de armazenamento e armazenamento em disco](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Necessita de armazenamento de cópia de segurança tooadd, mesmo se planear toosend tooAzure de dados. A arquitetura atual hello do servidor de cópia de segurança do Azure, o Cofre de cópias de segurança do Azure Olá contém Olá *segundo* cópia dos dados de Olá enquanto o armazenamento local Olá contém Olá primeiro (e obrigatório) cópia de segurança.  
>
>

## <a name="4-network-connectivity"></a>4. Conectividade de rede
![step4](./media/backup-azure-microsoft-azure-backup/step4.png)

Servidor de cópia de segurança do Azure requer o serviço de cópia de segurança do Azure de toohello de conectividade para Olá produto toowork com êxito. toovalidate se máquina Olá tem Olá conectividade tooAzure, utilize Olá ```Get-DPMCloudConnection``` commandlet na consola do PowerShell de servidor de cópia de segurança do Azure de Olá. Se hello resultado Olá commandlet for TRUE, em seguida, existe conectividade, caso contrário existe sem conectividade.

Em Olá mesmo tempo, Olá subscrição do Azure tem toobe em bom estado. toofind saída Estado Olá da sua subscrição e toomanage-lo, inicie sessão toohello [portal subscrição](https://account.windowsazure.com/Subscriptions).

Quando souber Estado Olá dos Olá conectividade do Azure e dos Olá subscrição do Azure, pode utilizar tabela Olá abaixo toofind saída impacto Olá a funcionalidade de cópia de segurança/restauro Olá oferecidos.

| Estado de conectividade | Subscrição do Azure | Cópia de segurança tooAzure | Cópia de segurança toodisk | Restaurar a partir do Azure | Restaurar a partir do disco |
| --- | --- | --- | --- | --- | --- |
| Ligado |Ativa |Permitido |Permitido |Permitido |Permitido |
| Ligado |Expirou |Parada |Parada |Permitido |Permitido |
| Ligado |Desaprovisionada |Parada |Parada |Pontos de recuperação de paragem e o Azure eliminados |Parada |
| Conectividade perdida > 15 dias |Ativa |Parada |Parada |Permitido |Permitido |
| Conectividade perdida > 15 dias |Expirou |Parada |Parada |Permitido |Permitido |
| Conectividade perdida > 15 dias |Desaprovisionada |Parada |Parada |Pontos de recuperação de paragem e o Azure eliminados |Parada |

### <a name="recovering-from-loss-of-connectivity"></a>Recuperar a partir de perda de conectividade
Se tiver uma firewall ou um proxy que está a impedir o acesso tooAzure, terá de Olá toowhitelist endereços de domínio no perfil de firewall/proxy Olá os seguintes:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Depois de conectividade tooAzure foi restaurada toohello máquina de servidor de cópia de segurança do Azure, as operações de Olá que podem ser efetuadas são determinadas pelo Olá estado da subscrição do Azure. tabela de Olá acima tem detalhes sobre as operações de Olá permitidos depois Olá máquina é "ligada".

### <a name="handling-subscription-states"></a>Processamento de Estados de subscrição
É possível tootake uma subscrição do Azure a partir de um *expirado* ou *Deprovisioned* Estado toohello *Active Directory* estado. No entanto isto tem algumas implicações no comportamento do produto Olá enquanto Olá Estado não é *Active Directory*:

* A *Deprovisioned* subscrição perde a funcionalidade para o período de Olá é desaprovisionada. No ativar *Active Directory*, funcionalidade do produto Olá de cópia de segurança/restauro é revived. dados de cópia de segurança de Olá no disco local Olá também podem ser obtidos se de que foi guardado com um período de retenção suficientemente grande. No entanto, os dados de cópia de segurança de Olá no Azure são irretrievably perdidos depois de subscrição de Olá entra Olá *Deprovisioned* estado.
* Um *expirado* subscrição apenas perde a funcionalidade para até que foi efetuada *Active Directory* novamente. As cópias de segurança agendadas para o período de Olá Olá subscrição foi *expirado* não será executado.

## <a name="troubleshooting"></a>Resolução de problemas
Se o servidor de cópia de segurança do Microsoft Azure falhar com erros durante a fase de configuração de Olá (ou cópia de segurança ou restauro), consulte toothis [documento de códigos de erro](https://support.microsoft.com/kb/3041338) para obter mais informações.
Também pode consultar demasiado[perguntas mais frequentes relacionadas com a cópia de segurança do Azure](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Passos seguintes
Pode obter informações detalhadas [preparar o ambiente para o DPM](https://technet.microsoft.com/library/hh758176.aspx) no site da Microsoft TechNet de Olá. Também contém informações sobre configurações suportadas em que servidor de cópia de segurança do Azure podem ser implementado e utilizado.

Pode utilizar estes toogain artigos uma compreensão mais aprofundada da proteção de carga de trabalho utilizando o servidor de cópia de segurança do Microsoft Azure.

* [Cópia de segurança do SQL Server](backup-azure-backup-sql.md)
* [Cópia de segurança do SharePoint server](backup-azure-backup-sharepoint.md)
* [Cópia de segurança do servidor alternativo](backup-azure-alternate-dpm-server.md)
