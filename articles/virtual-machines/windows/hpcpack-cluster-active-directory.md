---
title: aaaHPC pacote do cluster com o Azure Active Directory | Microsoft Docs
description: Saiba como toointegrate um 2016 de pacote HPC cluster no Azure com o Azure Active Directory
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Gerir um cluster HPC Pack no Azure utilizando o Azure Active Directory
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) suporta a integração com [do Azure Active Directory](../../active-directory/index.md) (Azure AD) para os administradores que implementar um cluster HPC Pack no Azure.



Siga os passos de Olá neste artigo para Olá seguintes tarefas de nível elevadas: 
* Integrar manualmente o seu cluster HPC Pack com o seu inquilino do Azure AD
* Gerir e agendar tarefas no seu cluster HPC Pack no Azure 

Integrar uma solução de cluster HPC Pack com o Azure AD segue o padrão de passos toointegrate outras aplicações e serviços. Este artigo pressupõe que está familiarizado com a gestão de utilizador básico no Azure AD. Para obter mais informações e em segundo plano, consulte Olá [documentação do Azure Active Directory](../../active-directory/index.md) e Olá secção a seguir.

## <a name="benefits-of-integration"></a>Vantagens da integração


Azure Active Directory (Azure AD) é um multi-inquilino baseado na nuvem diretório e identidade do serviço de gestão que fornece acesso de início de sessão único (SSO) toocloud soluções.

Integração de um cluster HPC Pack com o Azure AD pode ajudar a alcançar Olá os seguintes objetivos:

* Remova o controlador de domínio do Active Directory tradicional Olá do cluster HPC Pack de Olá. Isto pode ajudar a reduzir os custos de Olá de manutenção cluster Olá se isto não é necessário para o seu negócio e o processo de implementação de Olá speed-up dos.
* Tirar partido das Olá seguintes vantagens que são colocadas pelo Azure AD:
    *   Início de sessão único 
    *   Utilizar uma identidade de AD local para o cluster HPC Pack de Olá no Azure 

    ![Ambiente do Active Directory do Azure](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Pré-requisitos
* **Cluster HPC Pack 2016 implementado em máquinas virtuais do Azure** – para obter os passos, consulte [implementar um cluster HPC Pack 2016 no Azure](hpcpack-2016-cluster.md). Precisará de nome DNS de Olá do nó principal Olá e Olá as credenciais de um administrador de cluster para concluir os passos de Olá neste artigo.

  > [!NOTE]
  > Integração do Active Directory do Azure não é suportada em versões do pacote HPC antes do HPC Pack 2016.



* **Computador cliente** -precisa de um Windows ou Windows Server cliente computador demasiado executa HPC Pack cliente utilitários. Se pretender que apenas portal web do toouse Olá HPC Pack ou as tarefas de toosubmit de REST API, pode utilizar qualquer computador cliente à sua escolha.

* **Utilitários de cliente de HPC Pack** -instalar utilitários de cliente de HPC Pack Olá no computador de cliente Olá, utilizando o pacote de instalação livre Olá disponível a partir do Olá Microsoft Download Center.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Passo 1: Registar o servidor de cluster HPC Olá inquilino do Azure AD
1. Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **do Active Directory** no Olá menu à esquerda e, em seguida, clique em Olá diretório pretendido na sua subscrição. Tem de ter recursos de tooaccess permissão no diretório de Olá.
3. Clique em **utilizadores**e certifique-se de que existem utilizador contas já criados ou configurado.
4. Clique em **aplicações** > **adicionar**e, em seguida, clique em **adicionar uma aplicação que a minha organização está a desenvolver**. Introduza Olá informações no Assistente de Olá os seguintes:
    * **Nome** -HPCPackClusterServer
    * **Tipo** - selecione **aplicação e/ou Web API Web**
    * **Início de sessão URL**- hello base de URL para o exemplo Olá, que está por predefinição`https://hpcserver`
    * **URI de ID de aplicação** - `https://<Directory_name>/<application_name>`. Substitua `<Directory_name`> com o nome completo do seu inquilino do Azure AD, por exemplo, Olá `hpclocal.onmicrosoft.com`e substitua `<application_name>` com o nome de Olá que selecionou anteriormente.

5. Depois de é adicionada a aplicação Olá, clique em **configurar**. Configure Olá seguintes propriedades:
    * Selecione **Sim** para **aplicação é a multi-inquilino**
    * Selecione **Sim** para **utilizador atribuição tooaccess necessário aplicação**.

6. Clique em **Guardar**. Quando terminar de guardar, clique em **gerir manifesto**. Esta ação transfere ficheiros de notation (JSON) de objeto da aplicação manifesto JavaScript. Edite o manifesto de Olá transferido através da localização Olá `appRoles` definição e adicionar Olá seguir a função de aplicação:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Guarde o ficheiro de Olá. Em seguida, no portal de Olá, clique em **gerir manifesto** > **carregar manifesto**. Em seguida, pode carregar o manifesto editado Olá.
8. Clique em **utilizadores**, selecione um utilizador e, em seguida, clique em **atribuir**. Atribua um Olá funções disponíveis (HpcUsers ou HpcAdminMirror) toohello utilizador. Repita este passo com outros utilizadores no diretório de Olá. Para obter informações gerais sobre os utilizadores de cluster, consulte [gerir utilizadores do Cluster](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx).

   > [!NOTE] 
   > utilizadores toomanage, é recomendável utilizar o painel de pré-visualização do Azure Active Directory Olá no Olá [portal do Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Passo 2: Registar o cliente de cluster HPC de Olá inquilino do Azure AD

1. Inicie sessão no toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. Clique em **do Active Directory** no Olá menu à esquerda e, em seguida, clique em Olá diretório pretendido na sua subscrição. Tem de ter recursos de tooaccess permissão no diretório de Olá.
3. Clique em **aplicações** > **adicionar**e, em seguida, clique em **adicionar uma aplicação que a minha organização está a desenvolver**. Introduza Olá informações no Assistente de Olá os seguintes:

    * **Nome** -HPCPackClusterClient
    * **Tipo** - selecione **aplicação cliente nativa**
    * **URI de redirecionamento** - `http://hpcclient`

4. Depois de é adicionada a aplicação Olá, clique em **configurar**. Olá cópia **ID de cliente** valor e guarde-o. Poderá precisa deste mais tarde quando configurar a sua aplicação.

5. No **aplicações de tooother permissões**, clique em **Adicionar aplicação**. Procurar e adicionar Olá HpcPackClusterServer aplicação (criada no passo 1).

6. No Olá **permissões delegadas** lista pendente, selecione **acesso HpcClusterServer**. Em seguida, clique em **Guardar**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Passo 3: Configurar o cluster HPC de Olá

1. Ligar toohello HPC Pack 2016 nó principal no Azure.

2. Inicie o HPC PowerShell.

3. Execute Olá os seguintes comandos:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    onde

    * `AADTenant`Especifica o nome de inquilino do Azure AD de Olá, tais como`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Especifica o ID de cliente de Olá da aplicação Olá criada no passo 2.

4. Reinicie o serviço de HpcSchedulerStateful Olá.

    Num cluster com vários nós principais, pode executar os seguintes comandos do PowerShell no Olá nó principal tooswitch Olá réplica primária para o serviço de HpcSchedulerStateful Olá de Olá:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Passo 4: Gerir e submeter as tarefas de cliente de Olá

utilitários de cliente do tooinstall Olá HPC Pack no seu computador, transferir os ficheiros de configuração de HPC Pack 2016 (instalação completa) da Olá Microsoft Download Center. Quando iniciar a instalação de Olá, escolha a opção de configuração de Olá para Olá **utilitários de cliente de HPC Pack**.

computador de cliente do tooprepare Olá, instale o certificado de Olá utilizado durante [a configuração de cluster HPC](hpcpack-2016-cluster.md) no computador de cliente Olá. Utilizar o Windows padrão de certificado gestão procedimentos tooinstall Olá certificado público toohello **certificados-utilizador atual** > **autoridades de certificação de raiz fidedigna** armazenar. 

Pode agora executar comandos de HPC Pack Olá ou utilizar toosubmit Olá GUI do Gestor de tarefa do pacote HPC e gerir tarefas de cluster utilizando a conta de Olá do Azure AD. Para opções de submissão da tarefa, consulte [cluster HPC submeter tarefas tooan pacote HPC no Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Quando tenta tooconnect toohello HPC Pack cluster do Azure para Olá pela primeira vez, é apresentada uma janela de pop-up. Introduza o seu toolog de credenciais do Azure AD no. token de Olá, em seguida, é colocado em cache. Cluster de toohello ligações posterior na utilização do Azure Olá colocadas em cache token, a menos que as alterações de autenticação ou Olá em cache está desmarcada.
>
  
Por exemplo, depois de concluir os passos anteriores Olá, pode consultar as tarefas a partir de um cliente no local da seguinte forma:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Cmdlets útil para submissão da tarefa com a integração do Azure AD 

### <a name="manage-hello-local-token-cache"></a>Gerir a cache de token local Olá

HPC Pack 2016 fornece dois novos cmdlets do HPC PowerShell cache de token toomanage Olá local. Estes cmdlets são úteis para submeter tarefas de forma não interativa. Consulte o seguinte exemplo de Olá:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Defina credenciais de Olá para submeter tarefas utilizando a conta de Olá do Azure AD 

Por vezes, poderá ser útil tarefa de Olá toorun em utilizador de cluster HPC de Olá (para um cluster HPC associados a um domínio, executar como utilizador de domínio; para um cluster HPC não associados ao domínio, executado como um utilizador local no nó principal Olá).

1. Utilize Olá seguintes credenciais de Olá tooset de comandos:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. Em seguida, submeta tarefa Olá da seguinte forma. Olá tarefa é executada em $localUser em nós de computação Olá.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Se `–Credential` não for especificado com `Submit-HpcJob`, Olá trabalho ou tarefa é executado sob um utilizador local mapeado como Olá conta do Azure AD. (cluster HPC de Olá cria um utilizador local com o mesmo nome como Olá tarefas do Azure AD conta toorun Olá de Olá.)
    
3. Definir os dados expandidos para Olá conta do Azure AD. Isto é útil quando em execução uma tarefa MPI em nós de Linux utilizando a conta de Olá do Azure AD.

   * Definir os dados expandidos para Olá conta do Azure AD próprio

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Definir os dados expandidos e executadas como utilizador de cluster HPC
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

