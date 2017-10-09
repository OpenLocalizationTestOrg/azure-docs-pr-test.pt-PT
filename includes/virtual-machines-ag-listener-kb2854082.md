Em seguida, se todos os servidores no cluster de Olá estiver a executar Windows Server 2008 R2 ou Windows Server 2012, tem de verificar que correção Olá [KB2854082](http://support.microsoft.com/kb/2854082) está instalado em cada um dos servidores no local de Olá ou VMs do Azure que fazem parte do cluster de Olá. Qualquer servidor ou a VM se encontra num cluster de Olá, mas não está num grupo de disponibilidade de Olá, também deverá ter esta correção está instalada.

Olá ambiente de trabalho sessão remota para cada um de nós de cluster Olá transferir [KB2854082](http://support.microsoft.com/kb/2854082) tooa de diretório local. Em seguida, instale sequencialmente Olá correção em cada nó de cluster. Se o serviço de cluster Olá está atualmente em execução no nó de cluster Olá, servidor Olá é reiniciado no fim de Olá da instalação da correção de Olá.

> [!WARNING]
> Parar o serviço de cluster Olá ou reiniciar o servidor de Olá afeta o estado de funcionamento do Olá quórum do cluster e Olá do grupo de disponibilidade e pode provocar a toogo de cluster offline. toomaintain Olá elevada disponibilidade do cluster durante a instalação, certifique-se de que:
> 
> * cluster de Olá está num Estado de funcionamento de quórum ideais. 
> * Antes de instalar a correção de Olá em qualquer nó, todos os nós de cluster estão online.
> * Antes de instalar a correção de Olá no outro nó no cluster de Olá, permitir Olá correção instalação toorun toocompletion num único nó, incluindo totalmente reiniciar o servidor de Olá.
> 
> 

