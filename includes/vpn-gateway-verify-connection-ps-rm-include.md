<span data-ttu-id="62106-101">Pode verificar se a ligação teve êxito com o cmdlet Olá 'Get-AzureRmVirtualNetworkGatewayConnection', com ou sem '-Debug'.</span><span class="sxs-lookup"><span data-stu-id="62106-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="62106-102">Olá utilize seguinte o exemplo de cmdlet, a configuração Olá valores toomatch os seus próprios.</span><span class="sxs-lookup"><span data-stu-id="62106-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="62106-103">Se lhe for pedido, selecione "A" em ordem toorun 'Tudo'.</span><span class="sxs-lookup"><span data-stu-id="62106-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="62106-104">Exemplo de Olá, '-Name' refere-se toohello nome da ligação de Olá que pretende que o tootest.</span><span class="sxs-lookup"><span data-stu-id="62106-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="62106-105">Após concluir Olá cmdlet, veja os valores de Olá.</span><span class="sxs-lookup"><span data-stu-id="62106-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="62106-106">Exemplo de Olá abaixo, o estado da ligação Olá mostra como 'Ligado' e pode ver bytes de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="62106-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```