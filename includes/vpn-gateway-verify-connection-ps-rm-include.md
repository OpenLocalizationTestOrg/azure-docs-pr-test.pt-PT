Pode verificar se a ligação teve êxito com o cmdlet Olá 'Get-AzureRmVirtualNetworkGatewayConnection', com ou sem '-Debug'. 

1. Olá utilize seguinte o exemplo de cmdlet, a configuração Olá valores toomatch os seus próprios. Se lhe for pedido, selecione "A" em ordem toorun 'Tudo'. Exemplo de Olá, '-Name' refere-se toohello nome da ligação de Olá que pretende que o tootest.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Após concluir Olá cmdlet, veja os valores de Olá. Exemplo de Olá abaixo, o estado da ligação Olá mostra como 'Ligado' e pode ver bytes de entrada e saída.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```