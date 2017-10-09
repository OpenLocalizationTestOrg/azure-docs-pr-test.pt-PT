Uma máquina virtual do Azure suporta anexar um número de discos de dados. Para um desempenho ideal, deverá toolimit Olá diversas altamente sobreutilizados discos anexados toohello máquina virtual tooavoid possíveis de limitação. Se todos os discos não estão a ser altamente utilizados em Olá mesmo tempo, conta de armazenamento Olá pode suportar um maior número de discos.

* **Para discos gerida do Azure:** limite de contagem de discos geridos é regional e também depende do tipo de armazenamento Olá. Olá predefinido e também o limite máximo de Olá é 10.000 por subscrição, por região e por tipo de armazenamento. Por exemplo, pode criar cópias de segurança too10, 000 padrão geridos discos e também 10 000 premium geridos discos numa subscrição e numa região. 

    Instantâneos gerido e imagens são contadas contra Olá que limitar discos geridos.

* **Para contas de armazenamento standard:** uma conta de armazenamento standard tem uma taxa de pedidos total máxima de 20.000 IOPS. Olá ESP totais em todos os discos da máquina virtual numa conta do standard storage não deve exceder este limite.
  
    Pode calcular aproximadamente número Olá de discos altamente sobreutilizados suportados por uma conta de armazenamento única padrão com base no limite de taxa de pedidos de Olá. Por exemplo, para um VM, o escalão básico Olá número máximo de elevada disponibilidade utilizados discos está prestes a 66 (20.000/300 IOPS por disco) e para uma VM de escalão Standard, está prestes a 40 (20.000/500 IOPS por disco), conforme mostrado na tabela de Olá abaixo. 
* **Para contas de armazenamento premium:** uma conta de armazenamento premium tem uma taxa de débito total máximo de 50 Gbps. débito total do Olá em todos os discos VM não deve exceder este limite.

