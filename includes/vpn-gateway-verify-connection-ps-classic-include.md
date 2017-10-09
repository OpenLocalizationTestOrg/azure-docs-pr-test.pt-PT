Pode verificar se a ligação teve êxito com o cmdlet Olá 'Get-AzureVNetConnection'.

1. Olá utilize seguinte o exemplo de cmdlet, a configuração Olá valores toomatch os seus próprios. nome de Olá da rede virtual Olá tem de ser aspas se contiver espaços.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Após concluir Olá cmdlet, veja os valores de Olá. Exemplo de Olá abaixo, mostra o estado de conectividade Olá como 'Ligado' e pode ver bytes de entrada e de saída.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal