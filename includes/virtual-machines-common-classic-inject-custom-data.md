


Este tópico descreve como:

* Inserir dados numa máquina virtual do Azure (VM) ao que está a ser aprovisionado.
* Obtê-lo para o Windows e Linux.
* Utilizar ferramentas especiais disponíveis em algumas toodetect de sistemas e processar dados personalizados automaticamente.

> [!NOTE]
> Este artigo descreve como personalizados dados podem ser injetadas através da utilização de uma VM criada com Olá API de gestão de serviços do Azure. toosee como toouse Olá API de gestão de recursos do Azure, consulte [modelo de exemplo de Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Dados personalizados inserirem-se para a máquina virtual do Azure
Esta funcionalidade atualmente só é suportada em Olá [Interface de linha de comandos do Azure](https://github.com/Azure/azure-xplat-cli). Aqui criamos uma `custom-data.txt` ficheiro que contém os nossos dados, em seguida, inserir que no toohello VM durante o aprovisionamento. Embora possa utilizar qualquer uma das opções de Olá para Olá `azure vm create` seguinte Olá demonstra uma abordagem muito básica, comando:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Dados personalizados a utilizar na máquina virtual de Olá
* Se a VM do Azure é uma VM com base no Windows, em seguida, é guardado no ficheiro de dados personalizados Olá a demasiado`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Embora foi com codificação base64 tootransfer de Olá computador local toohello nova VM, é automaticamente descodificar e pode ser aberta ou utilizadas imediatamente.
  
  > [!NOTE]
  > Se o ficheiro de Olá, será substituído. segurança de Olá no diretório de Olá estiver definida demasiado**controlo de sistema: completo** e **administradores: completo controlo**.
  > 
  > 
* Se a VM do Azure é uma VM baseado em Linux, em seguida, o ficheiro de dados personalizados Olá estarão localizado em um dos seguintes Olá coloca, dependendo do seu distro. Olá poderão ser codificado por base64, pelo que poderá ter dados de Olá toodecode primeiro:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Init de nuvem no Azure
Se a VM do Azure é a partir de uma imagem Ubuntu ou CoreOS, em seguida, pode utilizar CustomData toosend uma configuração de nuvem toocloud-init. Ou, se o ficheiro de dados personalizada é um script, em seguida, na nuvem init pode simplesmente executá-lo.

### <a name="ubuntu-cloud-images"></a>Ubuntu nuvem imagens
Na maioria das imagens de Linux do Azure, seria editar "/ etc/waagent.conf" tooconfigure Olá temporário disco e a comutação ficheiro de recursos. Consulte [guia de utilizador do agente Linux do Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações.

No entanto, nas imagens de nuvem de Ubuntu Olá, tem de utilizar o disco de recursos de Olá do cloud init tooconfigure (ou seja, Olá "efémeras" disco) e a comutação partição. Consulte Olá seguir a página Olá Ubuntu Wiki para obter mais detalhes: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Próximas etapas: nuvem init a utilizar
Para obter mais informações, consulte Olá [documentação de nuvem init para Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Adicionar referência de API de REST de gestão de serviço de função](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Interface de linha de comandos do Azure](https://github.com/Azure/azure-xplat-cli)

