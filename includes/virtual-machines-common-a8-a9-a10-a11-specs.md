

## <a name="deployment-considerations"></a>Considerações sobre implementação
* **Subscrição do Azure** – toodeploy mais do que alguns instâncias de computação intensiva, considere uma subscrição pay as you go ou outras opções de compra. Se estiver a utilizar uma [conta gratuita do Azure](https://azure.microsoft.com/free/), pode utilizar apenas um número limitado de núcleos de computação do Azure.

* **Preços e disponibilidade** -tamanhos de VM estas são fornecidos apenas no escalão de preço padrão Olá. Verifique [produtos disponíveis por região] (https://azure.microsoft.com/regions/services/) de disponibilidade em regiões do Azure. 
* **Quota de núcleos** – poderá ter de quota de núcleos de Olá tooincrease na sua subscrição do Azure a partir do valor predefinido de Olá. A subscrição também poderá limitar o número de Olá de núcleos que pode implementar em determinados famílias de tamanho VM, incluindo Olá série H. toorequest uma quota de aumentar, [abrir um pedido de suporte ao cliente online](../articles/azure-supportability/how-to-create-azure-support-request.md) , sem encargos. (Predefinição limites podem variar consoante a categoria de subscrição.)
  
  > [!NOTE]
  > Se tiver necessidades de capacidade em grande escala, contacte o suporte do Azure. Quotas do Azure são crédito limites, não as garantias de capacidade. Independentemente da sua quota, são-lhe apenas cobrados de núcleos que utiliza.
  > 
  > 
* **Rede virtual** – um Azure [rede virtual](https://azure.microsoft.com/documentation/services/virtual-network/) é toouse não é necessário instâncias intensivas de computação de Olá. No entanto, para muitas implementações precisa de, pelo menos, uma rede de virtual do Azure baseados na nuvem ou uma ligação site a site, se precisar de tooaccess recursos no local. Quando for necessário, crie uma nova rede virtual instâncias de Olá toodeploy. A adição de rede virtual do computação intensivas VMs tooa num grupo de afinidade não é suportada.
* **Redimensionamento** – devido ao seu hardware especializado, apenas pode redimensionar instâncias intensivas de computação dentro do Olá mesmo tamanho de família (série de H ou intensivas de computação série A). Por exemplo, apenas pode redimensionar uma VM de série de H a partir de um tooanother de tamanho de série de H. Além disso, a redimensionamento de um tamanho de não-intensivas de computação tooa intensivas de computação de tamanho não é suportado.  
