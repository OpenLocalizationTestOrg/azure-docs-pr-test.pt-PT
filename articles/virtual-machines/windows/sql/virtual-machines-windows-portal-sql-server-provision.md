---
title: "aaaProvision uma Máquina Virtual do SQL Server | Microsoft Docs"
description: "Criar e ligar a máquina de virtual tooa do SQL Server no Azure através do portal Olá. Este tutorial utiliza o modo do Olá Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Aprovisionar uma máquina virtual do SQL Server no Olá portal do Azure
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Este tutorial ponto-a-ponto mostra-lhe como toouse Olá tooprovision portal do Azure uma máquina virtual com o SQL Server.

Galeria da máquina virtual do Azure (VM) de Olá inclui várias imagens que contêm o Microsoft SQL Server. Com alguns cliques, pode selecionar uma das imagens de VM do SQL na Galeria de Olá de Olá e aprovisioná-lo no seu ambiente do Azure.

Neste tutorial, irá:

* [Selecionar uma imagem de VM do SQL da Galeria de Olá](#select-a-sql-vm-image-from-the-gallery)
* [Configurar e criar Olá VM](#configure-the-vm)
* [Abrir Olá VM com o ambiente de trabalho remoto](#open-the-vm-with-remote-desktop)
* [Ligar tooSQL servidor remotamente](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Selecionar uma imagem de VM do SQL da Galeria de Olá

1. Inicie sessão no toohello [portal do Azure](https://portal.azure.com) utilizando a sua conta.

   > [!NOTE]
   > Se não tiver uma conta do Azure, aceda a [Versão de avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

2. No portal do Azure Olá, clique em **novo**. portal de Olá abre Olá **novo** janela.

3. No Olá **novo** janela, clique em **computação** e, em seguida, clique em **ver todos os**.

   ![Janela Nova Computação](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. No campo de pesquisa de Olá, escreva **do SQL Server**, e prima ENTER.

5. Em seguida, clique em Olá **filtro** ícone e selecione **Microsoft** para o publicador de Olá. Clique em **feito** nos resultados de Olá Olá filtro janela toofilter tooMicrosoft publicados imagens do SQL Server.

   ![Janela Máquinas Virtuais do Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Reveja as imagens de SQL Server disponíveis Olá. Cada imagem identifica uma versão do SQL Server e um sistema operativo.

6. Com o nome de imagem de Olá selecione **licença livre: SQL Server 2016 SP1 Programador no Windows Server 2016**.

   > [!TIP]
   > edição de programador Olá é utilizada neste tutorial, porque é uma edição completa do SQL Server que está livre para fins de teste de desenvolvimento. Só paga pelos custo de Olá de execução Olá VM. No entanto, estiver livre toochoose qualquer uma das imagens de Olá toouse neste tutorial.

   > [!TIP]
   > Imagens da VM do SQL Server incluem custos de licenciamento Olá para o SQL Server para Olá preços por minuto de Olá VM criar (exceto para edições Olá programador e o Express). O SQL Server Developer é gratuito para programação/teste (não para produção) e o SQL Express é gratuito para cargas de trabalho leves (inferiores a 1GB de memória e inferiores a 10 GB de armazenamento). Há outra opção toobring-your-proprietário-licença (BYOL) e pagar apenas para Olá VM. Aos nomes dessas imagem é adicionado o prefixo {BYOL}. 
   >
   > Para obter mais informações sobre estas opções, consulte [Pricing guidance for SQL Server Azure VMs (Documentação de orientação sobre preços de VMs do Azure do SQL Server)](virtual-machines-windows-sql-server-pricing-guidance.md).

7. Em **Selecionar um modelo de implementação**, confirme se **Resource Manager** está selecionado. Gestor de recursos é Olá recomendado modelo de implementação de novas máquinas virtuais. 

8. Clique em **Criar**.

    ![Criar a VM do SQL com o Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Configurar Olá VM
Existem cinco janelas para configurar uma máquina virtual do SQL Server.

| Passo | Descrição |
| --- | --- |
| **Noções básicas** |[Configurar as definições básicas](#1-configure-basic-settings) |
| **Tamanho** |[Selecionar o tamanho da máquina virtual](#2-choose-virtual-machine-size) |
| **Definições** |[Configurar funcionalidades opcionais](#3-configure-optional-features) |
| **Definições do SQL Server** |[Configurar definições do SQL Server](#4-configure-sql-server-settings) |
| **Resumo** |[Resumo de Olá de revisão](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Configurar as definições básicas

No Olá **Noções básicas** janela, fornecer Olá seguintes informações:

* Introduza um **Nome** exclusivo para a máquina virtual.

* Selecione **SSD** no tipo de disco da VM, para um desempenho ideal.

* Especifique um **nome de utilizador** Olá conta de administrador local no Olá VM. Esta conta também é adicionada toohello do SQL Server **sysadmin** função de servidor fixa.

* Forneça uma **Palavra-passe** forte.

* Se tiver várias subscrições, certifique-se de que está correta para a subscrição de Olá Olá nova VM.

* No Olá **grupo de recursos** caixa, escreva um nome para um novo grupo de recursos. Em alternativa, toouse um grupo de recursos existente clique em **utilizar existente**. Um grupo de recursos é uma coleção de recursos relacionados no Azure (máquinas virtuais, contas do Storage, redes virtuais, etc.).

  > [!NOTE]
  > Utilizar um novo grupo de recursos é útil se estiver apenas a testar ou a saber mais sobre implementações do SQL Server no Azure. Depois de concluir o teste, elimine Olá de eliminação de tooautomatically de grupo de recursos do Olá VM e todos os recursos associados esse grupo de recursos. Para mais informações sobre grupos de recursos, consulte o artigo [Descrição Geral do Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).

* Selecione um **localização** para Olá região do Azure que irá alojar esta implementação.

* Clique em **OK** definições de Olá toosave.

    ![Janela Informações Básicas do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Selecionar o tamanho da máquina virtual

No Olá **tamanho** passo, escolha um tamanho de máquina virtual em Olá **escolher um tamanho** janela. janela de Olá inicialmente apresenta os tamanhos de máquina recomendadas com base na imagem de Olá que selecionou.

> [!IMPORTANT]
> Olá estimado custo mensal apresentado no Olá **escolher um tamanho** janela não inclui os custos de licenciamento do SQL Server. Este é o custo de Olá de Olá VM individualmente. Para Olá rápida e programador as edições do SQL Server, este é o custo estimado total de Olá. Para outras edições, consulte Olá [página de preços de máquinas virtuais do Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) e selecione a edição de destino do SQL Server. Consulte também Olá [preços orientação para as VMs do SQL do Azure](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opções de Tamanho da VM do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Para cargas de trabalho de produção, consulte Olá recomendado tamanhos de máquina e configuração no [práticas recomendadas do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-performance.md). Se precisar de um tamanho da máquina não estiver listado, clique em Olá **ver todos os** botão.

> [!NOTE]
> Para obter mais informações sobre os tamanhos da máquina virtual, consulte [Tamanhos das Virtual Machines](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Selecione o tamanho da máquina e, em seguida, clique em **Selecionar**.

## <a name="3-configure-optional-features"></a>3. Configurar funcionalidades opcionais

No Olá **definições** janela, configure o storage do Azure, redes e a monitorização para a máquina virtual de Olá.

* Em **Armazenamento**, selecione **Sim**, em **Managed Disks**.

   > [!NOTE]
   > A Microsoft recomenda o Managed Disks para o SQL Server. Armazenamento de identificadores de discos em segundo plano de Olá de gerido. Além disso, quando as máquinas virtuais com discos geridos estão em Olá redundância adequada de tooprovide recursos de armazenamento Olá distribui o mesmo conjunto de disponibilidade, o Azure. Para obter informações adicionais, veja [Azure Managed Disks Overview](../../../storage/storage-managed-disks-overview.md) (Descrição Geral do Managed Disks). Para obter informações específicas sobre os discos geridos em conjuntos de disponibilidade, veja [Use managed disks for VMs in availability set](../manage-availability.md) (Utilizar discos geridos em VMs num conjunto de disponibilidade).

* Em **rede**, pode aceitar valores de Olá preenchido automaticamente. Também pode clicar em cada funcionalidade toomanually configurar Olá **rede Virtual**, **sub-rede**, **endereço IP público**, e **dogrupodesegurançaderede**. Para efeitos de Olá deste tutorial, mantenha os valores predefinidos de Olá.

* Azure ativa **monitorização** por predefinição com Olá a mesma conta do storage designada para Olá VM. Pode alterar estas definições aqui.

* Em **do conjunto de disponibilidade**, pode deixar predefinição Olá **nenhum** para este tutorial. Se planear tooset dos grupos de disponibilidade do AlwaysOn de SQL Server, configure Olá disponibilidade tooavoid recriar Olá máquina.  Para obter mais informações, consulte [gerir Olá disponibilidade das Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Quando tiver terminado de configurar estas definições, clique em **OK**.

## <a name="4-configure-sql-server-settings"></a>4. Configurar definições do SQL Server
No Olá **definições do SQL Server** janela, configure as definições específicas e otimizações para SQL Server. definições de Olá que pode configurar para o SQL Server incluem o seguinte Olá.

| Definição |
| --- |
| [Conetividade](#connectivity) |
| [Autenticação](#authentication) |
| [Configuração do armazenamento](#storage-configuration) |
| [Aplicação de Patches Automatizada](#automated-patching) |
| [Cópia de Segurança Automatizada](#automated-backup) |
| [Integração do Cofre de Chaves do Azure](#azure-key-vault-integration) |
| [Serviços R](#r-services) |

### <a name="connectivity"></a>Conectividade

Em **conectividade do SQL**, especifique o tipo de Olá de acesso que pretende toohello instância do SQL Server nesta VM. Para efeitos de Olá deste tutorial, selecione **público (internet)** Olá, tooallow ligações tooSQL servidor de máquinas ou serviços na internet. Com esta opção selecionada, Azure configura automaticamente a firewall de Olá e tráfego de tooallow do grupo de segurança de rede da Olá na porta 1433.

![Opções de Conectividade do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> Por predefinição, o SQL Server escuta numa porta bem conhecida, a **1433**. Para maior segurança, altere a porta de Olá no Olá toolisten de caixa de diálogo anterior numa porta não predefinidos, tais como 1401. Se o fizer, tem de utilizar essa parte para se ligar a partir de qualquer ferramenta cliente, como o SSMS.

tooconnect tooSQL servidor através de Olá internet, também tem de ativar a autenticação do SQL Server, que está descrito na secção seguinte, Olá.

Se preferir toonot ativar ligações toohello motor de base de dados através de Olá internet, escolha uma das seguintes opções de Olá:

* **Local (no interior da VM)** tooallow ligações tooSQL Server apenas a partir de dentro de Olá VM.
* **Privada (na Virtual Network)** tooallow ligações tooSQL servidor de máquinas ou serviços na Olá mesma rede virtual.

Em geral, melhore a segurança, selecionando a conectividade mais restritiva Olá que permite o seu cenário. Mas todas as opções de Olá com capacidade de segurança através de regras do grupo de segurança de rede e a autenticação SQL/Windows. Pode editar o grupo de segurança de rede após Olá que é criada a VM. Para obter mais informações, veja [Security Considerations for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-security.md) (Considerações de segurança para o SQL Server em Máquinas Virtuais do Azure).

> [!NOTE]
> imagem de máquina virtual de Olá para o SQL Server Express edition não ativar automaticamente a protocolo Olá TCP/IP. Isto acontece mesmo para Olá conectividade pública e privada opções. Para a edição Express, tem de utilizar SQL Server Configuration Manager demasiado[ative manualmente o protocolo de TCP/IP de Olá](#configure-sql-server-to-listen-on-the-tcp-protocol) depois de criar Olá VM.

### <a name="authentication"></a>Autenticação

Se necessitar da Autenticação do SQL Server, clique em **Ativar** em **Autenticação do SQL**.

![Autenticação do SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Se planear tooaccess do SQL Server através de Olá internet (ou seja, a Olá opção de conectividade pública), tem de ativar a autenticação do SQL aqui. Acesso público toohello do SQL Server requer a utilização de Olá da autenticação do SQL.
> 
> 

Se ativar a Autenticação do SQL Server, especifique um **Nome de início de sessão** e uma **Palavra-passe**. Este nome de utilizador está configurado como um início de sessão da autenticação do SQL Server e é membro de Olá **sysadmin** função de servidor fixa. Consulte o artigo [Escolher um Modo de Autenticação](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) para obter mais informações sobre Modos de Autenticação.

Se não ativar a autenticação do SQL Server, pode utilizar conta de administrador local Olá na instância de SQL Server do Olá VM tooconnect toohello.

### <a name="storage-configuration"></a>Configuração do armazenamento

Clique em **configuração de armazenamento** os requisitos de armazenamento de Olá toospecify.

![Configuração do Armazenamento do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Se tiver configurado manualmente o armazenamento padrão do toouse VM, esta opção não está disponível. A otimização de armazenamento automática só está disponível para o Premium Storage.

> [!TIP]
> número de Olá de paragens e os limites superiores Olá de cada controlo de deslize estão dependentes de tamanho de Olá da VM que selecionou. Uma VM maior e mais poderosa é capaz de tooscale cópias de segurança mais.

Pode especificar os requisitos como operações de entrada/saída por segundo (IOPs), débito em MB/s e tamanho de armazenamento total. Configure estes valores, utilizando as escalas deslizantes de Olá. Pode alterar estas definições de armazenamento com base na carga de trabalho. portal de Olá calcula automaticamente Olá número de discos tooattach e configurar com base nestes requisitos.

Em **armazenamento otimizado para**, selecione uma das seguintes opções de Olá:

* **Geral** é Olá predefinição e suporta a maioria das cargas de trabalho.
* **Transacional** processamento otimiza o armazenamento de Olá para cargas de trabalho OLTP de bases de dados tradicionais.
* **Armazenamento de dados** otimiza o armazenamento de Olá para cargas de trabalho analíticas e de relatórios.

### <a name="automated-patching"></a>Aplicação de patches automatizada

A **Aplicação de patches automatizada** está ativada por predefinição. Aplicação de patches automatizada permite Azure tooautomatically patch do SQL Server e Olá sistema operativo. Especifique um dia da semana de Olá, a hora e a duração de uma janela de manutenção. O Azure executa a aplicação de patches nesta janela de manutenção. agenda da janela de manutenção Olá utiliza a região da VM Olá por período de tempo. Se não pretender que o Azure tooautomatically patch do SQL Server e Olá sistema operativo, clique em **desativar**.  

![Aplicação de Patches Automatizada do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Para obter mais informações, consulte o artigo [Aplicação de Patches Automatizada para o SQL Server nas Virtual Machines do Azure](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Cópia de segurança automatizada

Ative as cópias de segurança de bases de dados automáticas em **Cópia de segurança automatizada**. A cópia de segurança automatizada está desativada por predefinição.

Quando ativa a cópia de segurança automatizada do SQL Server, pode configurar as seguintes Olá:

* Período de retenção (dias) para cópias de segurança
* Toouse de conta de armazenamento para cópias de segurança
* Opção de encriptação e palavra-passe para as cópias de segurança
* Realizar cópia de segurança das bases de dados do sistema
* Configurar agenda da cópia de segurança

Clique em cópia de segurança, do tooencrypt Olá **ativar**. Em seguida, especifique Olá **palavra-passe**. O Azure cria um certificado tooencrypt Olá as cópias de segurança e utiliza Olá especificado tooprotect de palavra-passe esse certificado.

![Cópia de Segurança Automatizada do SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Para obter mais informações, consulte o artigo [Cópia de Segurança Automatizada para o SQL Server nas Virtual Machines do Azure](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Integração do Cofre de Chaves do Azure

toostore segredos de segurança no Azure para a encriptação, clique em **integração do Cofre de chaves do Azure** e clique em **ativar**.

![Integração do Cofre de Chaves do SQL Azure](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Olá tabela seguinte lista Olá parâmetros necessários tooconfigure integração do Cofre de chaves do Azure.

| PARÂMETRO | DESCRIÇÃO | EXEMPLO |
| --- | --- | --- |
| **URL do Cofre de Chaves** |localização de Olá do Cofre de chaves Olá. |https://contosokeyvault.vault.azure.net/ |
| **Nome principal** |Nome principal do serviço Azure Active Directory. Este nome também é referido tooas Olá ID de cliente. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Segredo principal** |Segredo principal do serviço Azure Active Directory. Este segredo também é referido tooas Olá segredo do cliente. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Nome da credencial** |**Nome da credencial**: a integração AKV cria uma credencial dentro do SQL Server, permitindo Olá VM toohave acesso toohello Cofre de chaves. Escolha um nome para esta credencial. |mycred1 |

Para obter mais informações, consulte o artigo [Configurar a Integração do Cofre de Chaves do Azure para o SQL Server em VMs do Azure](virtual-machines-windows-ps-sql-keyvault.md).

### <a name="r-services"></a>Serviços R

Tiver Olá opção tooenable [serviços do SQL Server R](https://msdn.microsoft.com/library/mt604845.aspx). Isto permite-lhe toouse avançada de análise com o SQL Server 2016. Clique em **ativar** no Olá **definições do SQL Server** janela.

> [!NOTE]
> Para o SQL Server 2016 programador Edition, esta opção está incorretamente desativada pelo portal Olá. Na Developer Edition, tem de ativar os Serviços R manualmente depois de criar a VM.

![Ativar os Serviços R do SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

Quando tiver terminado de configurar as definições do SQL Server, clique em **OK**.

## <a name="5-review-hello-summary"></a>5. Resumo de Olá de revisão

No Olá **resumo** janela, reveja Olá resumo e clique em **Compra** toocreate do SQL Server, grupo de recursos e recursos especificados para esta VM.

Pode monitorizar a implementação de Olá de Olá portal do Azure. Olá **notificações** botão, Olá parte superior do ecrã de Olá mostra o estado básico da implementação de Olá.

> [!NOTE]
> tooprovide, com uma ideia na implementação exceder o tempo, implementei uma região de EUA Leste toohello VM do SQL Server com as predefinições. Esta implementação de teste demorou um total de 26 minutos toocomplete. Mas poderá ter uma implementação mais lenta ou mais rápida com base na sua região e nas definições selecionadas.

## <a name="open-hello-vm-with-remote-desktop"></a>Abrir Olá VM com o ambiente de trabalho remoto

Utilize Olá os seguintes passos tooconnect toohello do SQL Server virtual máquina com o ambiente de trabalho remoto:

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Depois de ligar a máquina de virtual toohello do SQL Server, pode iniciar o SQL Server Management Studio e estabelecer ligação com a autenticação do Windows com as suas credenciais de administrador local. Se ativou a autenticação do SQL Server, também pode ligar com autenticação de SQL com o início de sessão do Olá SQL e a palavra-passe que configurou durante o aprovisionamento.

Máquina toohello de acesso permite-lhe toodirectly alteração máquina e definições do SQL Server com base nos seus requisitos. Por exemplo, pode configurar as definições da firewall Olá ou alterar as definições de configuração do SQL Server.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>Ativar o TCP/IP para edições Developer e Express

Quando aprovisionar uma nova VM do SQL Server, Azure não automaticamente ativa o protocolo de TCP/IP Olá para programadores do SQL Server e edições Express. passos de Olá abaixo explicam como toomanually ative TCP/IP para que possam ligar remotamente por endereço IP.

Olá, utilize os passos a seguir **Gestor de configuração do SQL Server** tooenable protocolo de Olá TCP/IP para programadores do SQL Server e edições Express.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>Ligar tooSQL servidor remotamente

Neste tutorial, selecionamos **pública** acesso para a máquina virtual de Olá e **autenticação do SQL Server**. Estas definições Olá configurada automaticamente máquinas virtuais tooallow do SQL Server ligações a partir da qualquer cliente através de Olá internet (partindo do princípio de que tem início de sessão Olá correto SQL).

> [!NOTE]
> Se não selecionou público durante o aprovisionamento, pode alterar as definições de conectividade do SQL Server através do portal Olá após o aprovisionamento. Para obter mais informações, veja o artigo [Alterar as definições de conectividade SQL](virtual-machines-windows-sql-connect.md#change).

Olá secções a seguir mostra como tooconnect tooyour instância de SQL Server na VM a partir de outro computador através de Olá internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Passos Seguintes

Para outras informações sobre como utilizar o SQL Server no Azure, consulte [do SQL Server em Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md) e Olá [perguntas mais frequentes](virtual-machines-windows-sql-server-iaas-faq.md).
