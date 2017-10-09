---
title: aaaSet configurar um cluster do Service Fabric do Azure | Microsoft Docs
description: "Guia de introdução - criar um cluster do Service Fabric do Windows ou Linux no Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Crie o primeiro cluster Service Fabric no Azure
Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto ligado à rede de máquinas virtuais ou físicas, no qual os microsserviços são implementados e geridos. Este guia de introdução ajuda-o a toocreate um cluster de cinco nós, em execução no Windows ou Linux, através de Olá [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) ou [portal do Azure](http://portal.azure.com) em apenas alguns minutos.  

Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.


## <a name="use-hello-azure-portal"></a>Utilizar Olá portal do Azure

Início de sessão toohello do portal do Azure em [http://portal.azure.com](http://portal.azure.com).

### <a name="create-hello-cluster"></a>Criar cluster Olá

1. Clique em Olá **novo** botão encontrado no canto esquerda superior Olá de Olá portal do Azure.
2. Selecione **computação** de Olá **novo** painel e, em seguida, selecione **Cluster do Service Fabric** de Olá **computação** painel.
3. Preencha Olá Service Fabric **Noções básicas** formulário. Para **sistema operativo**, selecione versão Olá do Windows ou Linux que pretende Olá toorun de nós de cluster. nome de utilizador Olá e a palavra-passe introduzida aqui é toolog utilizado na máquina virtual de toohello. Para o **Grupo de recursos** crie um novo. Um grupo de recursos é um contentor lógico no qual os recursos do Azure são criados e geridos coletivamente. Quando terminar, clique em **OK**.

    ![Saída do programa de configuração do cluster][cluster-setup-basics]

4. Preencha Olá **configuração de Cluster** formulário.  Para a **contagem do tipo de Nó**, introduza "1".

5. Selecione **1 (principal) do tipo de nó** e preencher Olá **configuração de tipo de nó** formulário.  Introduza um nome de tipo de nó e defina Olá [o escalão de durabilidade](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) demasiado "Bronze."  Selecione um tamanho de VM.

    Tipos de nó definem o tamanho da VM Olá, número de VMs, os pontos finais personalizados e outras definições para Olá VMs desse tipo. Cada tipo de nó definido está configurado como um conjunto de dimensionamento de máquina virtual separada, o que é utilizado toodeploy e máquinas virtuais geridas como um conjunto. Cada tipo de nó pode ser aumentado ou reduzido verticalmente de forma independente, pode ter conjuntos diferentes de portas abertas e ter métricas de capacidade diferente.  Olá primeiro ou primária, tipo de nó é onde os serviços de sistema do Service Fabric alojados e tem de ter cinco ou mais VMs.

    Para qualquer implementação de produção, o [planeamento da capacidade](service-fabric-cluster-capacity.md) é um passo importante.  Para este guia de introdução, no entanto, não está a executar aplicações, pelo que deve selecionar um tamanho da VM *DS1_v2 Standard* .  Selecione "Silver" para Olá [escalão de fiabilidade](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) e um dimensionamento da máquina de virtual inicial defina a capacidade de 5.  

    Os pontos finais personalizados abrir portas no balanceador de carga do Azure de Olá para que possam ligar com as aplicações em execução no cluster de Olá.  Introduza "80, 8172" tooopen se as portas 80 e 8172.

    Não verificar Olá **configurar as definições avançada** caixa, que é utilizada para personalizar os pontos finais de gestão TCP/HTTP, intervalos de portas de aplicação, [restrições de posicionamento](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), e [capacidade propriedades](service-fabric-cluster-resource-manager-metrics.md).    

    Selecione **OK**.

6. No Olá **configuração de Cluster** formulário, defina **diagnóstico** demasiado**no**.  Para este início rápido, não é necessário tooenter qualquer [recursos de infraestrutura definição](service-fabric-cluster-fabric-settings.md) propriedades.  No **versão do Fabric**, selecione **automática** Atualize modo para que a Microsoft atualiza automaticamente a versão de Olá do código de recursos de infraestrutura de Olá em execução cluster Olá.  Definir o modo de Olá demasiado**Manual** se quiser demasiado[escolher uma versão suportada](service-fabric-cluster-upgrade.md) tooupgrade para. 

    ![Configuração do tipo de nó][node-type-config]

    Selecione **OK**.

7. Preencha Olá **segurança** formulário.  Para este guia de introdução, selecione **Inseguro**.  É altamente recomendado toocreate um cluster seguro para cargas de trabalho de produção, no entanto, uma vez que qualquer pessoa pode ligar a clusters não seguros tooan anonimamente e efetuar operações de gestão.  

    Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações. Para obter mais informações sobre como os certificados são utilizados no Service Fabric, consulte [Service Fabric cluster security scenarios (Cenários de segurança do cluster do Service Fabric)](service-fabric-cluster-security.md).  com o Azure Active Directory ou tooset configurar certificados para uma segurança de aplicação, a autenticação de utilizador tooenable [criar um cluster a partir de um modelo do Resource Manager](service-fabric-cluster-creation-via-arm.md).

    Selecione **OK**.

8. Resumo de Olá de revisão.  Se gostaria de toodownload um modelo do Resource Manager construído a partir das definições de Olá introduziu, selecione **transferir modelo e os parâmetros**.  Selecione **criar** cluster de Olá toocreate.

    Pode ver o progresso da criação Olá em notificações Olá. (Clique ícone de campainha"Olá" junto da barra de estado de Olá na Olá canto superior direito do ecrã). Se clicou em **Pin tooStartboard** ao criar o cluster de Olá, consulte **implementação de Cluster do Service Fabric** afixado toohello **iniciar** quadro.

### <a name="view-cluster-status"></a>Ver o estado do cluster
Depois do cluster foi criado, pode inspecionar o cluster Olá **descrição geral** painel no portal de Olá. Agora, pode ver os detalhes de Olá do cluster no dashboard de Olá, incluindo o ponto de final público do cluster Olá e tooService uma ligação Explorador de recursos de infraestrutura.

![Estado do cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizar o cluster de Olá através do Service Fabric explorer
O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o seu cluster e gerir aplicações.  Explorador de recursos de infraestrutura de serviço é um serviço que é executado no cluster de Olá.  Aceder ao mesmo utilizando um browser clicando Olá **Service Fabric Explorer** ligação de cluster Olá **descrição geral** página Olá portal.  Também pode introduzir o endereço de Olá diretamente no browser Olá: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

dashboard de cluster Olá fornece uma descrição geral do cluster, incluindo um resumo das aplicações e estado de funcionamento do nó. Vista de nó de Olá mostra o esquema físico do Olá do cluster de Olá. Para um determinado nó, pode inspecionar as aplicações que têm um código implementado nesse nó.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>Ligue o cluster de toohello através do PowerShell
Certifique-se de que esse cluster Olá está em execução, ligando-se com o PowerShell.  Olá ServiceFabric módulo do PowerShell é instalado com Olá [SDK de Service Fabric](service-fabric-get-started.md).  Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet estabelece um cluster de toohello de ligação.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
Consulte [Connect tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para outros exemplos de ligação de tooa de cluster. Depois de estabelecer ligação toohello cluster, utilize Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay uma lista de nós no Olá cluster e informações de estado para cada nó. O **HealthState** deve ser *OK* para cada nó.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Remover cluster Olá
Um cluster do Service Fabric é constituído por outros recursos do Azure Ademais toohello recurso de cluster em si. Pelo toocompletely eliminar um cluster do Service Fabric também precisa de toodelete que Olá todos os recursos que é composto. cluster de Olá para Olá mais simples forma toodelete e todos os recursos de Olá que consome é o grupo de recursos de Olá toodelete. Para outro toodelete formas um cluster ou toodelete algumas (mas não todos) recursos de Olá num grupo de recursos, consulte [eliminar um cluster](service-fabric-cluster-delete.md)

Elimine um grupo de recursos no Olá portal do Azure:
1. Navegue de cluster do Service Fabric toohello pretende toodelete.
2. Clique em Olá **grupo de recursos** nome na página do Olá cluster essentials.
3. No Olá **Essentials do grupo de recursos** página, clique em **eliminar grupo de recursos** e siga as instruções de Olá nessa página toocomplete Olá a eliminação do grupo de recursos de Olá.
    ![Eliminar grupo de recursos de Olá][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Utilizar o Azure Powershell toodeploy um cluster seguro
1. Transferir Olá [Azure Powershell versão 4.0 ou superior do módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) no seu computador.

2. Abra uma janela do Windows PowerShell, Olá de executar os seguintes comandos. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    Deverá ver um resultado semelhante toohello seguintes procedimentos.

    ![ps-list][ps-list]

3. Início de sessão tooAzure e selecione Olá subscrição toowhich pretende que o cluster de Olá toocreate

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. Olá execute os seguintes comandos toonow criar um cluster seguro. Não se esqueça de parâmetros de Olá toocustomize. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    comando Olá pode tomar entre toocomplete minutos, too30 10 minutos, no fim Olá, deve obter um resultado semelhante toohello seguintes procedimentos. saída de Olá tem informações sobre o certificado de Olá, Olá KeyVault em que foi carregado, e Olá pasta local onde o certificado de Olá é copiado. 

    ![ps-out][ps-out]

5. Copiar resultado completo Olá e guarde o ficheiro de texto tooa como precisamos toorefer tooit. Tome nota do Olá seguintes informações de saída de Olá. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>Instalar o certificado de Olá no seu computador local
  
tooconnect toohello cluster, precisa de tooinstall Olá certificado no arquivo de pessoais (os meus) Olá do utilizador atual Olá. 

Executar Olá seguir PowerShell

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

Agora, está pronto tooconnect tooyour segura cluster.

### <a name="connect-tooa-secure-cluster"></a>Ligue o cluster segura tooa 

Execute o seguinte de Olá de comando do PowerShell tooconnect tooa segura cluster. Detalhes do certificado Olá devem coincidir com um certificado que foi utilizado tooset segurança cluster Olá. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


Olá seguinte exemplo mostra Olá parâmetros completed: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

Execute Olá seguir toocheck comandos que estão ligadas e cluster Olá está em bom estado.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Publicar o seu cluster tooyour de aplicações a partir do Visual Studio

Agora que configurou um cluster do Azure, pode publicar o seu tooit de aplicações a partir do Visual Studio por Olá seguinte [publicar tooan cluster](service-fabric-publish-app-remote-cluster.md) documento. 

### <a name="remove-hello-cluster"></a>Remover cluster Olá
Um cluster é constituído por outros recursos do Azure Ademais toohello recurso de cluster em si. cluster de Olá para Olá mais simples forma toodelete e todos os recursos de Olá que consome é o grupo de recursos de Olá toodelete. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>Passos seguintes
Agora que configurou um cluster de desenvolvimento, experimente o seguinte Olá:
* [Criar um cluster seguro no portal de Olá](service-fabric-cluster-creation-via-portal.md)
* [Criar um cluster a partir de um modelo](service-fabric-cluster-creation-via-arm.md) 
* [Implementar aplicações com o Powershell](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
