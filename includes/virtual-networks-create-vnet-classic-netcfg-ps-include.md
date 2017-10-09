## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="0a46d-101">Como toocreate uma rede virtual com uma configuração de rede de ficheiros a partir do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a46d-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="0a46d-102">Azure utiliza um toodefine do ficheiro xml de subscrição de tooa disponíveis todas as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="0a46d-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="0a46d-103">Pode transferir este ficheiro, editá-lo toomodify ou elimine as redes virtuais existentes e criar novas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="0a46d-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="0a46d-104">Neste tutorial, saiba como toodownload deste ficheiro, referido tooas ficheiro de configuração (ou netcfg) de rede e editá-lo toocreate uma nova rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0a46d-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="0a46d-105">toolearn mais informações sobre o ficheiro de configuração de rede Olá, consulte Olá [esquema de configuração de rede virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a46d-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="0a46d-106">toocreate uma rede virtual com um ficheiro netcfg através do PowerShell, Olá concluir os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="0a46d-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="0a46d-107">Se nunca tiver utilizado o Azure PowerShell, Olá concluir os passos em Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) artigo, em seguida, inicie sessão no tooAzure e selecione a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="0a46d-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="0a46d-108">A partir da consola do Azure PowerShell Olá, utilize Olá **Get-AzureVnetConfig** cmdlet toodownload Olá rede configuração tooa diretório do ficheiro no seu computador através da execução Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0a46d-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="0a46d-109">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="0a46d-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="0a46d-110">Abrir o ficheiro de Olá guardou no passo 2 através de qualquer aplicação de editor de XML ou de texto e procure Olá  **<VirtualNetworkSites>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="0a46d-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="0a46d-111">Se tiver quaisquer redes já criados, cada rede é apresentado como a sua própria  **<VirtualNetworkSite>**  elemento.</span><span class="sxs-lookup"><span data-stu-id="0a46d-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="0a46d-112">rede de virtual de toocreate Olá descrito neste cenário, adicionar Olá seguir XML apenas em Olá  **<VirtualNetworkSites>**  elemento:</span><span class="sxs-lookup"><span data-stu-id="0a46d-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. <span data-ttu-id="0a46d-113">Guarde o ficheiro de configuração de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="0a46d-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="0a46d-114">A partir da consola do Azure PowerShell Olá, utilize Olá **conjunto AzureVnetConfig** ficheiro de configuração do cmdlet tooupload Olá rede executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0a46d-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="0a46d-115">Devolveu saída:</span><span class="sxs-lookup"><span data-stu-id="0a46d-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="0a46d-116">Se **OperationStatus** não é *com êxito* Olá devolvido resultados, verifique novamente Olá xml ficheiro erros e concluído passo 6.</span><span class="sxs-lookup"><span data-stu-id="0a46d-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="0a46d-117">A partir da consola do Azure PowerShell Olá, utilize Olá **Get-AzureVnetSite** tooverify cmdlet que Olá nova rede foi adicionado ao executar Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="0a46d-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="0a46d-118">Olá devolveu saída (abreviada) inclui Olá seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="0a46d-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
