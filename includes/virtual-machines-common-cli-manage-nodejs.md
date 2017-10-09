Antes de poder utilizar Olá CLI do Azure com o Gestor de recursos comandos e modelos toodeploy Azure recursos e cargas de trabalho utilizar grupos de recursos, terá de uma conta com o Azure. Se não tiver uma conta, pode obter uma [avaliação gratuita do Azure, aqui](https://azure.microsoft.com/pricing/free-trial/).

Se ainda não instalou Olá CLI do Azure e subscrição tooyour ligado, consulte [instalação Olá CLI do Azure](../articles/cli-install-nodejs.md) definir o modo de Olá demasiado`arm` com `azure config mode arm`e ligar-se tooAzure Olá `azure login` comando.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá
Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

- CLI do Azure 10 – os nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Comandos básicos do Azure Resource Manager na CLI do Azure
Este artigo abrange comandos básicos será pretende toouse com toomanage CLI do Azure e interagir com os recursos (principalmente VMs) na sua subscrição do Azure.  Para obter mais ajuda com os parâmetros da linha de comandos específicos e as opções, pode utilizar opções de ajuda do comando online Olá e escrevendo `azure <command> <subcommand> --help` ou `azure help <command> <subcommand>`.

> [!NOTE]
> Estes exemplos não incluem operações baseadas em modelos que, geralmente, são recomendadas para implementações de VM no Resource Manager. Para informações, consulte [Olá de utilizar a CLI do Azure com o Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) e [implementar e gerir máquinas virtuais utilizando os modelos Azure Resource Manager e Olá CLI do Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Tarefa | Resource Manager |
| --- | --- | --- |
| Criar Olá VM mais básica |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Obter Olá `image-urn` de Olá `azure vm image list` comando. Veja [este artigo](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter exemplos). |
| Criar uma VM do Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Criar uma VM do Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Listar VMs |`azure  vm list [options]` |
| Obter informações sobre uma VM |`azure  vm show [options] <resource_group> <name>` |
| Iniciar uma VM |`azure vm start [options] <resource_group> <name>` |
| Parar uma VM |`azure vm stop [options] <resource_group> <name>` |
| Desalocar uma VM |`azure vm deallocate [options] <resource-group> <name>` |
| Reiniciar uma VM |`azure vm restart [options] <resource_group> <name>` |
| Eliminar uma VM |`azure vm delete [options] <resource_group> <name>` |
| Capturar uma VM |`azure vm capture [options] <resource_group> <name>` |
| Criar uma VM a partir de uma imagem de utilizador |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Criar uma VM a partir de um disco especializado |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Adicionar um tooa de disco de dados VM |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Remover um disco de dados de uma VM |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Adicionar um tooa genérico extensão VM |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Adicionar extensão de acesso de VM tooa VM |`azure vm reset-access [options] <resource-group> <name>` |
| Adicionar extensão de Docker tooa VM |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Remover uma extensão de VM |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Obter a utilização de recursos de VM |`azure vm list-usage [options] <location>` |
| Obter todos os tamanhos de VM disponíveis |`azure vm sizes [options]` |

## <a name="next-steps"></a>Passos seguintes
* Para obter exemplos adicionais de comandos da CLI Olá ultrapassar a gestão de VM básicas, consulte [Olá de utilizar a CLI do Azure com o Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).
