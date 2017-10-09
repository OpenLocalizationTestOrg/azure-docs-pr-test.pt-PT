
* conversão de Olá requer um reinício de Olá VM, por isso, agendar a migração de Olá das suas VMs durante uma janela de manutenção já existente. 

* a conversão de Olá não é reversível. 

* Ser conversão de Olá tootest se. Migre uma máquina virtual de teste antes de executar a migração de Olá na produção.

* Durante a conversão de Olá, desalocar Olá VM. Olá VM recebe um novo endereço IP quando é iniciada após a conversão de Olá. Se necessário, pode [atribuir um endereço IP estático](../articles/virtual-network/virtual-network-ip-addresses-overview-arm.md) toohello VM.

* Olá VHDs originais e conta de armazenamento de Olá utilizada pelo Olá VM antes de conversão não são eliminados. Podem continuar tooincur encargos. tooavoid a ser cobrado destes artefactos, eliminar blobs de VHD originais Olá depois de verificar que a conversão de Olá está concluída.
