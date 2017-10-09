Se estiver a ter problemas de ligação de máquina virtual de tooa através da ligação VPN, verifique o seguinte Olá:

- Certifique-se de que a ligação VPN é efetuada com êxito.
- Certifique-se de que está a ligar toohello endereço IP privado para Olá VM.
- Se pode ligar toohello VM através de IP privado Olá endereços, mas não Olá nome do computador, certifique-se de que configurou DNS corretamente. Para obter mais informações sobre como funciona a resolução de nomes para VMs, consulte o artigo [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)(Resolução de Nomes para VMs).

Quando se liga através de ponto a Site, verifique Olá seguintes itens adicionais:

- Utilize 'ipconfig' toocheck Olá endereço de IPv4 atribuído a placa de Ethernet toohello no computador de Olá partir do qual está a ligar. Se o endereço IP Olá está dentro do intervalo de endereços de Olá de Olá VNet que está a ligar a ou dentro do intervalo de endereços de Olá do seu VPNClientAddressPool, isto é referido tooas uma sobreposição do espaço de endereços. Quando o espaço de endereços sobreposições desta forma, o tráfego de rede Olá não alcance do Azure, esta permanece na rede local Olá.
- Certifique-se de que esse pacote de configuração do cliente VPN Olá foi gerado depois de endereços IP do servidor DNS Olá foram especificados para Olá VNet. Se atualizar endereços IP do servidor DNS Olá, gerar e instalar um novo pacote de configuração de cliente VPN.

Para obter mais informações sobre resolução de problemas de uma ligação RDP, consulte [tooa de ligações de resolução de problemas de ambiente de trabalho remoto VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
