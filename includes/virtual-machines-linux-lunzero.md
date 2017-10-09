Ao adicionar dados discos tooa VM com Linux, pode deparar-se com erros se não existir um disco no LUN 0. Se estiver a adicionar um disco manualmente utilizando Olá `azure vm disk attach-new` comandos e especificar um LUN (`--lun`) em vez de permitir Olá toodetermine da plataforma Azure Olá LUN adequado, asseguramos que um disco já existe de colunas / existirá em LUN 0. 

Considere Olá seguinte o exemplo que mostra um fragmento de saída de Olá de `lsscsi`:

```bash
[5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc 
[5:0:0:1]    disk    Msft     Virtual Disk     1.0   /dev/sdd 
```

os discos de dados de Olá dois existem no LUN 0 e LUN 1 (primeira coluna de Olá no Olá `lsscsi` detalhes de saída `[host:channel:target:lun]`). Os dois discos devem ser accessbile de dentro de Olá VM. Se tivesse manualmente especificado Olá primeiro disco toobe adicionada em 1 de LUN e segundo disco de Olá em LUN 2, poderá não ver discos Olá corretamente a partir da sua VM.

> [!NOTE]
> Olá, Azure `host` valor é 5 nestes exemplos, mas isto pode variar, dependendo do tipo de Olá de armazenamento que selecionar.
> 
> 

Este comportamento de disco não é um problema do Azure, mas a forma de Olá no qual Olá Linux kernel segue as especificações de SCSI Olá. Quando kernel de Linux Olá analisa barramento SCSI de Olá para dispositivos ligados, um dispositivo tem de ser encontrado em LUN 0 por ordem para Olá sistema toocontinue análise de dispositivos adicionais. Como tal:

* Reveja o resultado Olá `lsscsi` depois de adicionar um tooverify de disco de dados que tem um disco no LUN 0.
* Se o disco não aparecer corretamente na VM, certifique-se de que existe um disco no LUN 0.

