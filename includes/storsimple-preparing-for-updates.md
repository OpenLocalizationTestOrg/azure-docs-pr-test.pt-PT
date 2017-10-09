<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>A preparar para as atualizações
Terá de Olá tooperform antes de procurar e aplicar a atualização de Olá os seguintes passos:

1. Tire um instantâneo de nuvem de dados de dispositivo Olá.
2. Certifique-se de que o controlador de IPs fixo são encaminhável e pode ligar toohello Internet. Estes IPs fixos serão dispositivo de tooyour tooservice utilizados atualizações. Pode testar esta executando Olá seguintes cmdlet em cada controlador de interface do Windows PowerShell Olá do dispositivo Olá:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Saída de exemplo para Test-Connection quando IPs fixos pode ligar toohello Internet**

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

Depois de concluir estas pré-verificações de manuais, pode continuar tooscan e instalar atualizações Olá.

