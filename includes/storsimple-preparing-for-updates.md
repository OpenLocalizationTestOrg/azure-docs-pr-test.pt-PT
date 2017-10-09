<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="51d7c-101">A preparar para as atualizações</span><span class="sxs-lookup"><span data-stu-id="51d7c-101">Preparing for updates</span></span>
<span data-ttu-id="51d7c-102">Terá de Olá tooperform antes de procurar e aplicar a atualização de Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="51d7c-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="51d7c-103">Tire um instantâneo de nuvem de dados de dispositivo Olá.</span><span class="sxs-lookup"><span data-stu-id="51d7c-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="51d7c-104">Certifique-se de que o controlador de IPs fixo são encaminhável e pode ligar toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="51d7c-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="51d7c-105">Estes IPs fixos serão dispositivo de tooyour tooservice utilizados atualizações.</span><span class="sxs-lookup"><span data-stu-id="51d7c-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="51d7c-106">Pode testar esta executando Olá seguintes cmdlet em cada controlador de interface do Windows PowerShell Olá do dispositivo Olá:</span><span class="sxs-lookup"><span data-stu-id="51d7c-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="51d7c-107">**Saída de exemplo para Test-Connection quando IPs fixos pode ligar toohello Internet**</span><span class="sxs-lookup"><span data-stu-id="51d7c-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

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

<span data-ttu-id="51d7c-108">Depois de concluir estas pré-verificações de manuais, pode continuar tooscan e instalar atualizações Olá.</span><span class="sxs-lookup"><span data-stu-id="51d7c-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

