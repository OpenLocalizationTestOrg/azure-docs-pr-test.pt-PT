Está agora disponível o suporte de duas funcionalidades de depuração no Azure: Saída da Consola e Captura de Ecrã para o modelo de implementação das Máquinas Virtuais do Azure (Resource Manager). 

Quando o seus próprios tooAzure de imagem ou mesmo arrancar uma das imagens da plataforma de Olá, pode ser muitos motivos por que motivo uma Máquina Virtual obtém num Estado não arranque. Ativar estas funcionalidades tooeasily diagnosticar e recuperar máquinas virtuais de falhas de arranque.

Para máquinas de virtuais do Linux, pode visualizar facilmente resultado Olá o início de sessão de consola do Olá Portal:

![Portal do Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
No entanto, para o Windows e máquinas virtuais do Linux, Azure também permite toosee uma captura de ecrã de Olá VM de hipervisor Olá:

![Erro](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Estas duas funcionalidades são suportadas para Máquinas Virtuais do Azure em todas as regiões. Tenha em atenção, capturas de ecrã e de saída podem demorar até too10 minutos tooappear na sua conta de armazenamento.

## <a name="common-boot-errors"></a>Erros de arranque comuns

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Não foi encontrado nenhum sistema operativo](https://support.microsoft.com/help/4010142)
- [Falha de arranque ou INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Ativar o diagnóstico numa máquina virtual nova
1. Quando criar uma nova máquina Virtual do Portal de pré-visualização de Olá, selecione Olá **do Azure Resource Manager** da lista pendente de modelo de implementação Olá:
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Configure Olá monitorização opção tooselect Olá conta do storage onde pretende que tooplace estes ficheiros de diagnóstico.
 
    ![Criar VM](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Se estiver a implementar a partir de um modelo Azure Resource Manager, navegue até tooyour recurso de Máquina Virtual e de acréscimo secção de perfil de diagnóstico de Olá. Lembre-se o cabeçalho de versão de API do toouse Olá "2015-06-15".

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. perfil de diagnóstico de Olá permite-lhe conta do storage tooselect olá onde pretende tooput estes registos.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy uma amostra de Máquina Virtual com o diagnóstico de arranque ativado, modificação do nosso repositório aqui.

## <a name="update-an-existing-virtual-machine"></a>Atualizar uma máquina virtual existente ##

diagnóstico de arranque tooenable através do Portal de Olá, também pode atualizar uma Máquina Virtual através de Olá Portal. Selecione Olá opção de diagnóstico de arranque e de guardar. Reinicie o efeito de tootake Olá VM.

![Atualizar VM Existente](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

