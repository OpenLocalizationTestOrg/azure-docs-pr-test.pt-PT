---
title: "aaaCreate uma VM do Azure clássico com MySQL | Microsoft Docs"
description: "Criar uma máquina virtual do Azure com o Windows Server 2012 R2 e Olá utilizando o modelo de implementação clássica Olá de dados MySQL."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Instalar o MySQL numa máquina virtual criada com o modelo de implementação clássica Olá a executar o Windows Server 2016
[MySQL](https://www.mysql.com) é um código aberto popular, a base de dados SQL. Este tutorial mostra como Olá tooinstall e execute **versão de Comunidade do MySQL 5.7.18** como um servidor de MySQL numa máquina virtual em execução **Windows Server 2016**. A experiência poderão ser ligeiramente diferente para outras versões de MySQL ou Windows Server.

Para obter instruções sobre como instalar o MySQL no Linux, consulte: [como tooinstall MySQL no Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [Resource Manager e clássico](../../../resource-manager-deployment-model.md). Este artigo abrange utilizando o modelo de implementação clássica Olá. A Microsoft recomenda que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Criar uma máquina virtual com o Windows Server 2016
Se ainda não tiver uma VM com o Windows Server 2016, pode utilizá-lo [tutorial](./tutorial.md) toocreate Olá máquina.

## <a name="attach-a-data-disk"></a>Anexar um disco de dados
Depois de criar a máquina virtual de Olá, opcionalmente, pode anexar um disco de dados. Adicionar que um disco de dados é recomendado para cargas de trabalho de produção e tooavoid a ficar sem espaço na unidade do SO (c) de Olá, que inclui o sistema de operativo Olá.

Consulte [como tooattach dados de disco de máquina virtual do tooa Windows](../attach-managed-disk-portal.md) e siga as instruções de Olá para anexar um disco vazio. Olá anfitrião cache definição configurada demasiado**nenhum** ou **só de leitura**.

## <a name="log-on-toohello-virtual-machine"></a>Inicie sessão na máquina virtual de toohello
Em seguida, irá [iniciar sessão na máquina virtual de toohello](./connect-logon.md) como tal, pode instalar o MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Instalar e executar o servidor de Comunidade MySQL na máquina virtual de Olá
Siga estes passos tooinstall, configurar e executar a versão de Comunidade hello do servidor de MySQL:

> [!NOTE]
> Quando a transferência de itens utilizando o Internet Explorer, pode definir Olá IE **configuração de segurança avançada** tooOff e simplificar Olá processo de transferência. No menu de início de Olá, administrativo ferramentas/Local/Gestor de servidor, clique em IE **configuração de segurança avançada** e defina Olá configuração tooOff).
>
>

1. Depois de se ligar máquinas toohello utilizando o ambiente de trabalho remoto, clique em **Internet Explorer** a partir do ecrã de início de Olá.
2. Selecione Olá **ferramentas** clique no botão no canto superior direito de Olá (ícone da roda cogged Olá) e, em seguida, clique em **opções da Internet**. Clique em Olá **segurança** separador, clique em Olá **Sites fidedignos** ícone e, em seguida, clique em Olá **Sites** botão. Adicione http://*.mysql.com toohello lista de sites fidedignos. Clique em **fechar**e, em seguida, clique em **OK**.
3. No Olá endereço barra do Internet Explorer, escreva https://dev.mysql.com/downloads/mysql/.
4. Utilize Olá MySQL site toolocate e transferir a versão mais recente do Olá do Olá MySQL instalador para Windows. Ao escolher Olá instalador MySQL, transfira a versão de Olá que tenha Olá concluir o conjunto de ficheiros (por exemplo, Olá mysql-instalador-Comunidade-5.7.18.0.msi com um tamanho de ficheiro de 352.8 MB) e guarde o instalador Olá.
5. Quando o instalador Olá terminou de transferir, clique em **executar** toolaunch programa de configuração.
6. No Olá **contrato de licença** página, aceite o contrato de licença de Olá e clique em **seguinte**.
7. No Olá **escolher um tipo de configuração** página, clique em tipo de configuração de Olá que pretende e, em seguida, clique em **seguinte**. Olá passos partem do princípio de seleção de Olá de Olá **apenas servidor** tipo de configuração.
8. Se hello **verificar requisitos** página apresenta, clique em **executar** instalador de Olá toolet instalar quaisquer componentes em falta. Siga as instruções que apresentem, tais como o tempo de execução C++ Redistributable Olá.
9. No Olá **instalação** página, clique em **executar**. Quando a instalação estiver concluída, clique em **seguinte**.

10. No Olá **configuração do produto** página, clique em **seguinte**.

11. No Olá **tipo e a rede** página, especifique opções de tipo e a conectividade da configuração pretendida, incluindo a porta TCP Olá, se necessário. Selecione **Mostrar opções avançadas**e, em seguida, clique em **seguinte**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. No Olá **contas e funções** página, especifique uma palavra-passe da raiz de MySQL segura. Adicionar mais contas de utilizador do MySQL, conforme necessário e, em seguida, clique em **seguinte**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. No Olá **Windows serviço** página, especifique as definições predefinidas da toohello alterações para a execução Olá MySQL servidor como um serviço do Windows conforme necessário e, em seguida, clique em **seguinte**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Olá escolhas no Olá **plug-ins e extensões** página são opcionais. Clique em **seguinte** toocontinue.
15. No Olá **opções avançadas** página, especifique as opções de toologging alterações conforme necessário e, em seguida, clique em **seguinte**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. No Olá **aplicar a configuração do servidor** página, clique em **executar**. Quando os passos de configuração de Olá estiverem concluídos, clique em **concluir**.
17. No Olá **configuração do produto** página, clique em **seguinte**.
18. No Olá **instalação concluída** página, clique em **tooClipboard de registo de cópia** se quiser tooexamine-lo mais tarde e, em seguida, clique em **concluir**.
19. A partir do ecrã de início de Olá, escreva **mysql**e, em seguida, clique em **MySQL 5.7 da linha de comandos cliente**.
20. Introduza Olá raiz palavra-passe que especificou no passo 12 e são apresentadas, com uma linha de comandos, onde pode emitir comandos tooconfigure MySQL. Para detalhes de Olá de comandos e sintaxe, consulte [MySQL referência como](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. Também pode configurar definições de predefinido de configuração do servidor, tais como Olá base e diretórios de dados e unidades. Para obter mais informações, consulte [6.1.2 predefinições do servidor de configuração](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Configurar pontos finais

Olá MySQL serviço toobe tooclient disponíveis computadores Olá Internet, tem de configurar um ponto final para Olá a porta TCP e criar uma regra de Firewall do Windows. valor de porta Olá predefinido em que Olá MySQL servidor serviço de escuta para clientes de MySQL é 3306. Pode especificar outra porta, desde que a porta de Olá é consistente com o valor de Olá fornecido no Olá **tipo e a rede** página (passo 11 Olá anterior procedimento).

> [!NOTE]
> Para utilização em produção, considere Olá implicações de segurança de efetuar Olá MySQL servidor computadores tooall disponíveis de serviço no Olá Internet. Pode definir o conjunto de Olá de endereços IP de origem que são permitidos ponto final de Olá toouse com uma lista de controlo de acesso (ACL). Para obter mais informações, consulte [como tooSet pontos finais de cópia de segurança tooa Máquina Virtual](setup-endpoints.md).
>
>

um ponto final para Olá serviço servidor MySQL tooconfigure:

1. No portal do Azure Olá, clique em **máquinas virtuais (clássicas)**, clique no nome de Olá da máquina virtual MySQL e, em seguida, clique em **pontos finais**.
2. Na barra de comando Olá, clique em **adicionar**.
3. No Olá **adicionar ponto final** , escreva um nome exclusivo para **nome**.
4. Selecione **TCP** como protocolo de Olá.
5. Escreva o número de porta de Olá, tais como **3306**, no **Porta pública** e **porta privada**e, em seguida, clique em **OK**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Adicionar um tooallow de regra de Firewall do Windows tráfego MySQL
tooadd uma regra de Firewall do Windows que permita o tráfego de MySQL de Olá Internet, execute Olá seguinte comando num _linha de comandos elevada do Windows PowerShell_ na máquina virtual do Olá MySQL servidor.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Testar a ligação remota
a ligação remota toohello VM do Azure em execução Olá MySQL servidor tootest do serviço, tem de fornecer o nome DNS Olá do serviço de nuvem de Olá contendo Olá VN.

1. No portal do Azure Olá, clique em **máquinas virtuais (clássicas)**, clique no nome de Olá da máquina virtual server MySQL e, em seguida, clique em **descrição geral**.
2. A partir do dashboard de máquina virtual de Olá, tenha em atenção Olá **nome DNS** valor. Segue-se um exemplo:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. Num computador local com o MySQL ou Olá cliente MySQL, execute Olá os seguintes comandos toolog na como um utilizador MySQL.

     MySQL -u <yourMysqlUsername> - p -h<yourDNSname>

   Por exemplo, utilizando Olá nome de utilizador MySQL _dbadmin3_ e Olá _testmysql.cloudapp.net_ nome de DNS para a máquina virtual de Olá, foi possível iniciar o MySQL utilizando Olá os seguintes comandos:

     MySQL -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Passos seguintes
toolearn mais sobre a execução MySQL, consulte Olá [MySQL documentação](http://dev.mysql.com/doc/).
