<!-- F-series, Fs-series* -->

Série F baseia-se no Olá 2.4 GHz Intel Xeon® E5-2673 v3 processador (Haswell), que pode alcançar a velocidades de relógio tão elevado como 3.1 GHz com Olá Intel Turbo intensificação tecnologia 2.0. Isto é Olá mesmo desempenho de CPU como Olá Dv2 série de VMs.  Um preço de lista por hora inferior, Olá série F é Olá valor melhor desempenho preços no Olá portefólio do Azure com base na unidade de computação do Azure (ACU) de Olá por vCPU. 

As VMs da série F são uma excelente opção para cargas de trabalho que exigem CPUs mais rápidas, mas não precisam de mais memória ou armazenamento temporário por vCPU.  Cargas de trabalho, tais como a análise, os servidores de jogos, servidores web e processamento em lote beneficiarão do valor Olá Olá série F.

Olá Fs-série fornece todas as vantagens Olá Olá série F, no armazenamento de tooPremium de adição.

## <a name="fs-series"></a>Série Fs*

ACU: 210 - 250

| Tamanho | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito máximo do armazenamento temporário e em cache: IOPS/MBps (tamanho da cache em GiB) | Débito máximo do disco não colocado em cache: IOPS/MBps | NICs. Máx. / Desempenho de rede esperado (Mbps) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_F1s |1 |2 |4 |2 |4,000 / 32 (12) |3,200 / 48 |2 / 750 |
| Standard_F2s |2 |4 |8 |4 |8,000 / 64 (24) |6,400 / 96 |2 / 1500 |
| Standard_F4s |4 |8 |16 |8 |16,000 / 128 (48) |12,800 / 192 |4 / 3000 |
| Standard_F8s |8 |16 |32 |16 |32,000 / 256 (96) |25,600 / 384 |8 / 6000 |
| Standard_F16s |16 |32 |64 |32 |64,000 / 512 (192) |51,200 / 768 |8 / 6000-12000 &#8224; |

MBps = 10^6 bytes por segundo e GiB = 1024^3 bytes.

* Olá máximo débito do disco (IOPS ou MBps) possível com uma série de Fs VM pode ser limitado pelo número de Olá, tamanho e striping de Olá anexado discos.  Para obter mais detalhes, veja [Armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquinas virtuais do Azure](../articles/storage/common/storage-premium-storage.md).


<br>

## <a name="f-series"></a>Série F

ACU: 210 - 250

| Tamanho         | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Débito do armazenamento temporário máximo: IOPS/MBps de Leitura/MBps de Escrita | Máximo do disco de dados/débito: IOPS | NICs. Máx. / Desempenho de rede esperado (Mbps) |
|--------------|-----------|-------------|----------------|----------------------------------------------------------|-----------------------------------|------------------------------|
| Standard_F1  | 1         | 2           | 16             | 3000 / 46 / 23                                           | 2 / 2x500                         | 2 / 750                 |
| Standard_F2  | 2         | 4           | 32             | 6000 / 93 / 46                                           | 4 / 4x500                         | 2 / 1500                     |
| Standard_F4  | 4         | 8           | 64             | 12000 / 187 / 93                                         | 8 / 8x500                         | 4 / 3000                     |
| Standard_F8  | 8         | 16          | 128            | 24000 / 375 / 187                                        | 16 / 16x500                       | 8 / 6000                     |
| Standard_F16 | 16        | 32          | 256            | 48000 / 750 / 375                                        | 32 / 32x500                       | 8 / 6000 - 12000 &#8224;           |


<br>


