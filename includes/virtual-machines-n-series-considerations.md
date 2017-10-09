## <a name="deployment-considerations"></a>Considerações sobre implementação

* Para disponibilidade de série N VMs, consulte [produtos disponíveis por região](https://azure.microsoft.com/en-us/regions/services/).

* Série N VMs só podem ser implementadas no modelo de implementação do Resource Manager Olá.

* Quando criar uma VM de série N utilizando Olá portal do Azure, no Olá **Noções básicas** painel, selecione um **tipo de disco da VM** de **HDD**. tamanho do toochoose uma série de N disponível, Olá **tamanho** painel, clique em **ver todos os**.

* Série N VMs não suportam discos VM que sejam copiados pelo armazenamento do Azure Premium.

* Se pretender que toodeploy mais do que alguns série N VMs, considere uma subscrição pay as you go ou outras opções de compra. Se estiver a utilizar uma [conta gratuita do Azure](https://azure.microsoft.com/free/), pode utilizar apenas um número limitado de núcleos de computação do Azure.

* Poderá necessitar de quota de núcleos de Olá tooincrease (por região) na sua subscrição do Azure e aumentar a quota de separado Olá para NC ou NV núcleos. toorequest uma quota de aumentar, [abrir um pedido de suporte ao cliente online](../articles/azure-supportability/how-to-create-azure-support-request.md) , sem encargos. Limites de predefinição podem variar consoante a categoria de subscrição.

* Uma imagem de VM, pode implementar em VMs de série de N é Olá [máquina de Virtual de ciência de dados do Azure](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Olá máquinas de virtuais de ciência de dados preinstalls e configura muitos ciência de dados mais populares e avançada ferramentas de aprendizagem. É também preinstalls controladores NVIDIA Tesla GPU para instâncias de NC.





