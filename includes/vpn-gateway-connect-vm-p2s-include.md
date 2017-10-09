Pode ligar tooa VM que é implementado tooyour VNet através da criação de uma VM de tooyour de ligação de ambiente de trabalho remoto. Olá melhor forma tooinitially Certifique-se de que pode ligar tooyour VM é tooconnect por utilizar o IP privado de endereços, em vez do nome do computador. Dessa forma, que está a testar toosee se pode ligar, não se resolução de nomes está corretamente configurada.

1. Localize o endereço IP privado Olá. Pode encontrar o endereço IP privado Olá de uma VM observando qualquer uma das propriedades Olá Olá VM Olá portal do Azure, ou utilizando o PowerShell.

  - Portal do Azure – localizar a máquina virtual no Olá portal do Azure. Ver propriedades Olá Olá VM. endereço IP privado Olá está listado.

  - PowerShell – tooview de exemplo de Olá para utilizar uma lista de VMs e endereços IP privados da sua grupos de recursos. Não precisa de toomodify neste exemplo antes de o utilizar.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Certifique-se de que está ligado tooyour VNet com Olá ponto a Site VPN ligação.
3. Abra **ligação ao ambiente de trabalho remoto** introduzindo "RDP" ou "Ligação de ambiente de trabalho remoto" na caixa de pesquisa de Olá na barra de tarefas Olá, em seguida, selecione a ligação ao ambiente de trabalho remoto. Também pode abrir a ligação ao ambiente de trabalho remoto utilizando o comando de 'mstsc' Olá no PowerShell. 
4. Na ligação ao ambiente de trabalho remoto, introduza o endereço IP privado Olá de Olá VM. -Pode definições adicionais do tooadjust "Mostrar opções", clique em ligar.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot um tooa de ligação de RDP VM

Se estiver a ter problemas de ligação de máquina virtual de tooa através da ligação VPN, verifique o seguinte Olá:

- Certifique-se de que a ligação VPN é efetuada com êxito.
- Certifique-se de que está a ligar toohello endereço IP privado para Olá VM.
- Utilize 'ipconfig' toocheck Olá endereço de IPv4 atribuído a placa de Ethernet toohello no computador de Olá partir do qual está a ligar. Se o endereço IP Olá está dentro do intervalo de endereços de Olá de Olá VNet que está a ligar a ou dentro do intervalo de endereços de Olá do seu VPNClientAddressPool, isto é referido tooas uma sobreposição do espaço de endereços. Quando o espaço de endereços sobreposições desta forma, o tráfego de rede Olá não alcance do Azure, esta permanece na rede local Olá.
- Se pode ligar toohello VM através de IP privado Olá endereços, mas não Olá nome do computador, certifique-se de que configurou DNS corretamente. Para obter mais informações sobre como funciona a resolução de nomes para VMs, consulte o artigo [Name Resolution for VMs](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)(Resolução de Nomes para VMs).
- Certifique-se de que esse pacote de configuração do cliente VPN Olá foi gerado depois de endereços IP do servidor DNS Olá foram especificados para Olá VNet. Se atualizar endereços IP do servidor DNS Olá, gerar e instalar um novo pacote de configuração de cliente VPN.
- Para obter mais informações sobre ligações RDP, consulte [tooa de ligações de resolução de problemas de ambiente de trabalho remoto VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
