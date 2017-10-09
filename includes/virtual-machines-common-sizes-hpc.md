<!-- A-series - compute-intensive instances, H-series -->

Olá tamanhos A8-A11 e H série são também conhecidos como *instâncias intensivas de computação*. hardware de Olá que executa estas tamanhos é concebido e otimizado para computação intensivas e aplicações, modelação e simulações de cluster de aplicações de rede intensiva, incluindo computacional de elevado desempenho (HPC). Olá A8-A11 série utiliza Intel Xeon E5-2670 @ 2.6 GHZ e Olá H série utiliza Intel Xeon E5-2667 v3 @ 3,2 GHz. 

Série H virtual machines do Azure são Olá próximo geração computação de alto desempenho que VMS diversificado necessidades computacional final elevada, como a modelação molecular e computacional fluída. Estes 8 e 16 vCPU VMs são criadas numa tecnologia de processador de Olá Intel Haswell E5-2667 V3 com DDR4 memória e armazenamento temporário baseadas em SSD. 

Além disso toohello substancial energia da CPU, Olá H série oferece opções de diversas para redes de RDMA de latência baixa FDR InfiniBand várias configurações toosupport memória exigente em termos computacionais requisitos de memória e a utilizar.



## <a name="h-series"></a>Série H

ACU: 290-300

| Tamanho | vCPU | Memória: GiB | Armazenamento (SSD) temporário GiB | Discos de dados máximos | Débito máximo do disco: IOPS | NICs máximos |
| --- | --- | --- | --- | --- | --- | --- |
| Standard_H8 |8 |56 |1000 |16 |16 x 500 |2  |
| Standard_H16 |16 |112 |2000 |32 |32 x 500 |4 |
| Standard_H8m |8 |112 |1000 |16 |16 x 500 |2  |
| Standard_H16m |16 |224 |2000 |32 |32 x 500 |4  |
| Standard_H16r* |16 |112 |2000 |32 |32 x 500 |4  |
| Standard_H16mr* |16 |224 |2000 |32 |32 x 500 |4 |

*Nas aplicações de MPI, a rede de back-end RDMA dedicada é ativada pela rede FDR InfiniBand, que oferece latência ultra baixa e elevada largura de banda.

<br>



## <a name="a-series---compute-intensive-instances"></a>Série A – Instâncias de computação intensiva

ACU: 225

| Tamanho | vCPU | Memória: GiB | Armazenamento (HDD) temporário: GiB | Discos de dados máximos | Débito máximo do disco de dados: IOPS | NICs máximos|
| --- | --- | --- | --- | --- | --- | --- |
| Standard_A8* |8 |56 |382 |16 |16x500 |2 |
| Standard_A9* |16 |112 |382 |16 |16x500 |4 |
| Standard_A10 |8 |56 |382 |16 |16x500 |2  |
| Standard_A11 |16 |112 |382 |16 |16x500 |4 |

*Nas aplicações de MPI, a rede de back-end RDMA dedicada é ativada pela rede FDR InfiniBand, que oferece latência ultra baixa e elevada largura de banda.

<br>



