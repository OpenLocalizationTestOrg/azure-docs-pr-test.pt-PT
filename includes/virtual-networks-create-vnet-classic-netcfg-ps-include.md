## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Como toocreate uma rede virtual com uma configuração de rede de ficheiros a partir do PowerShell
Azure utiliza um toodefine do ficheiro xml de subscrição de tooa disponíveis todas as redes virtuais. Pode transferir este ficheiro, editá-lo toomodify ou elimine as redes virtuais existentes e criar novas redes virtuais. Neste tutorial, saiba como toodownload deste ficheiro, referido tooas ficheiro de configuração (ou netcfg) de rede e editá-lo toocreate uma nova rede virtual. toolearn mais informações sobre o ficheiro de configuração de rede Olá, consulte Olá [esquema de configuração de rede virtual do Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate uma rede virtual com um ficheiro netcfg através do PowerShell, Olá concluir os seguintes passos:

1. Se nunca tiver utilizado o Azure PowerShell, Olá concluir os passos em Olá [como tooInstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) artigo, em seguida, inicie sessão no tooAzure e selecione a sua subscrição.
2. A partir da consola do Azure PowerShell Olá, utilize Olá **Get-AzureVnetConfig** cmdlet toodownload Olá rede configuração tooa diretório do ficheiro no seu computador através da execução Olá os seguintes comandos: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Resultado esperado:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Abrir o ficheiro de Olá guardou no passo 2 através de qualquer aplicação de editor de XML ou de texto e procure Olá  **<VirtualNetworkSites>**  elemento. Se tiver quaisquer redes já criados, cada rede é apresentado como a sua própria  **<VirtualNetworkSite>**  elemento.
4. rede de virtual de toocreate Olá descrito neste cenário, adicionar Olá seguir XML apenas em Olá  **<VirtualNetworkSites>**  elemento:

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
   
5. Guarde o ficheiro de configuração de rede Olá.
6. A partir da consola do Azure PowerShell Olá, utilize Olá **conjunto AzureVnetConfig** ficheiro de configuração do cmdlet tooupload Olá rede executando Olá os seguintes comandos: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Devolveu saída:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Se **OperationStatus** não é *com êxito* Olá devolvido resultados, verifique novamente Olá xml ficheiro erros e concluído passo 6.

7. A partir da consola do Azure PowerShell Olá, utilize Olá **Get-AzureVnetSite** tooverify cmdlet que Olá nova rede foi adicionado ao executar Olá os seguintes comandos: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Olá devolveu saída (abreviada) inclui Olá seguinte texto:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
