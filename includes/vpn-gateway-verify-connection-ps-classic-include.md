<span data-ttu-id="644cb-101">Pode verificar se a ligação teve êxito com o cmdlet Olá 'Get-AzureVNetConnection'.</span><span class="sxs-lookup"><span data-stu-id="644cb-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="644cb-102">Olá utilize seguinte o exemplo de cmdlet, a configuração Olá valores toomatch os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="644cb-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="644cb-103">nome de Olá da rede virtual Olá tem de ser aspas se contiver espaços.</span><span class="sxs-lookup"><span data-stu-id="644cb-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="644cb-104">Após concluir Olá cmdlet, veja os valores de Olá.</span><span class="sxs-lookup"><span data-stu-id="644cb-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="644cb-105">Exemplo de Olá abaixo, mostra o estado de conectividade Olá como 'Ligado' e pode ver bytes de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="644cb-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal