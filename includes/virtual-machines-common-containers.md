As soluções em cloud do Azure são criadas com base em máquinas virtuais (emulação de hardware de computadores físicos), que permitem o ágil empacotamento de implementações e uma melhor consolidação de recursos do que o hardware físico. [Docker](https://www.docker.com) contentores e Olá ecossistema de docker tem formas Olá significativamente expandida pode desenvolver, são enviados e a gestão distribuída de software. Código da aplicação num contentor está isolado da VM do anfitrião de Olá e outros contentores no Olá mesma VM. Este isolamento proporciona-lhe mais agilidade em termos de desenvolvimento e implementação.

O Azure oferece Olá valores de Docker os seguintes:

* [Muitos](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [diferentes](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) formas toocreate Docker aloja para contentores toosuit sua situação
* Olá [serviço de contentor Azure](https://azure.microsoft.com/documentation/services/container-service/) cria clusters de anfitriões de contentor utilizando orchestrators como **marathon** e **swarm**.
* [O Azure Resource Manager](../articles/azure-resource-manager/resource-group-overview.md) e [os modelos de grupo de recursos](../articles/resource-group-authoring-templates.md) toosimplify implementar e atualizar aplicações distribuídas complexas
* Integração num vasto conjunto de ferramentas de gestão de configuração, proprietárias e de código aberto

E porque programaticamente pode criar VMs e Linux contentores no Azure, também pode utilizar VM e um contentor *orchestration* ferramentas toocreate grupos de máquinas virtuais (VMs) e aplicações de toodeploy dentro de ambos os Linux contentores e agora [Windows contentores](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

Este artigo aborda não apenas estes conceitos um nível elevado, também contém toneladas das informações de toomore ligações, tutoriais, e produtos relacionados com a utilização de toocontainer e cluster no Azure. Se souber tudo isto e deseje ligações Olá, apresentadas aqui se estiver em [ferramentas para trabalhar com contentores](#tools-for-working-with-azure-vms-and-containers).

## <a name="hello-difference-between-virtual-machines-and-containers"></a>diferença Olá entre máquinas virtuais e contentores
As máquinas virtuais são executadas dentro de um ambiente de virtualização de hardware isolado, fornecido por um [hipervisor](http://en.wikipedia.org/wiki/Hypervisor). No Azure, Olá [máquinas virtuais](https://azure.microsoft.com/services/virtual-machines/) service identificadores tudo o que por si: criar máquinas virtuais ao escolher o sistema de operativo Olá e configurar &mdash;ou através do carregamento de uma imagem VM personalizada. Máquinas virtuais são uma tecnologia de time-tested, "protegido luta", e existem muitas ferramentas disponíveis toomanage Olá SO e as aplicações contêm.  As aplicações numa VM estão ocultos de Olá sistema operativo do anfitrião. Olá ponto de vista de uma aplicação ou o utilizador numa VM Olá VM aparece toobe um computador físico autónomo.

[Os contentores de Linux](http://en.wikipedia.org/wiki/LXC) e os que são criadas e alojadas utilizando ferramentas do docker, não utilize uma isolamento de tooprovide hipervisor. Com contentores, o anfitrião de contentor Olá utiliza processo e funcionalidades de isolamento do sistema de ficheiros do contentor do Olá Linux kernel tooexpose toohello, respetivas aplicações, determinadas funcionalidades de kernel e seu próprio sistema de ficheiros isolado. Olá ponto de vista de uma aplicação em execução dentro de um contentor, de contentor de Olá aparece toobe uma única instância de SO. As aplicações contidas não conseguem ver processos nem outros recursos que estejam fora do contentor.

São utilizados muito menos recursos num contentor Docker do que são utilizados numa VM. Os contentores de docker recorrer a um isolamento e de execução do modelo de aplicação, que não partilha kernel Olá de anfitriões de Docker Olá. Olá contentor tem muito inferior disco requisitos de espaço que não inclui Olá SO completo. O tempo de arranque e o espaço em disco necessários são significativamente inferiores do que numa VM.
Os contentores de Windows fornecem Olá mesmas vantagens como contentores de Linux para aplicações que são executados no Windows. Contentores do Windows suportam o formato de imagem de Docker Olá e a API do Docker, mas também podem ser geridos através do PowerShell. Estão disponíveis dois runtimes de contentor nos Contentores do Windows, nos Contentores do Windows Server e nos Contentores de Hyper-V. Os contentores de Hyper-V alojam cada contentor numa VM superotimizada, proporcionando uma camada de isolamento adicional. toolearn mais informações sobre contentores do Windows, consulte [sobre contentores de Windows](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview). tooget iniciado com contentores do Windows no Azure, saiba como demasiado[implementar um cluster do serviço de contentor Azure](../articles/container-service/dcos-swarm/container-service-deployment.md).

## <a name="what-are-containers-good-for"></a>Para que servem os contentores?

Os contentores podem melhorar:

* código da aplicação Olá velocidade pode ser desenvolvido e partilhado em grande escala
* velocidade de Olá e confiança de que uma aplicação pode ser testada
* velocidade de Olá e confiança de que uma aplicação pode ser implementada

Os contentores são executados num anfitrião de contentor&mdash; um sistema operativo e, no Azure, isto significa uma Máquina Virtual do Azure. Mesmo se já a adoram ideia Olá de contentores, que ainda vai tooneed uma infraestrutura VM que aloja os contentores de Olá, mas as vantagens de Olá são que os contentores não se na qual VM estão a executar (embora se contentor Olá pretende um Linux ou do Windows ambiente de execução será importante, por exemplo).


## <a name="what-are-containers-good-for"></a>Para que servem os contentores?
Estiverem excelentes para inúmeros aspetos, mas estes encorajar&mdash;tal como [Cloud Services do Azure](https://azure.microsoft.com/services/cloud-services/) e [Azure Service Fabric](../articles/service-fabric/service-fabric-overview.md)&mdash;Olá criação de único serviços orientados para microsserviço aplicações distribuídas, na qual aplicação estrutura se baseia em partes mais de pequenas e compostas em vez de nos componentes maiores e mais fortemente conjugados.

Isto é especialmente verdade para os ambientes de cloud pública, como o Azure, nos quais as VMs são alugadas quando e onde as quer. Não só obtém o isolamento, a rápida implementação e as ferramentas de orquestração, como também pode tomar decisões relativas à infraestrutura das aplicações mais eficientes.

Por exemplo, pode ter, atualmente, uma implementação que consista em nove VMs do Azure de tamanho grande para uma aplicação distribuída de elevada disponibilidade. Se os componentes de Olá desta aplicação podem ser implementados em contentores, poderá ser capaz de toouse só 4 VMs e implementar os componentes da aplicação no interior de 20 contentores para redundância e balanceamento de carga.

Isto é apenas um exemplo, obviamente, mas se pode fazê-lo no seu cenário, pode ajustar os picos de toousage com mais contentores em vez de mais VMs do Azure e utilizar Olá restantes carga total da CPU de forma muito mais eficiente do que antes.

Além disso, existem vários cenários que não se devem tooa micro-serviços abordagem; saberá que melhor se micro-serviços e contentores irão ajudá-lo.

### <a name="container-benefits-for-developers"></a>Vantagens dos contentores para os programadores
Em geral, é fácil toosee que a tecnologia de contentor é um passo reencaminhar, mas existem benefícios mais específicos, bem como. Vamos exemplo de Olá de contentores de Docker. Este tópico irá não aprofundar profundamente Docker agora (ler [Novidades Docker?](https://www.docker.com/whatisdocker/) nesse bloco, ou [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), mas Docker e seu ecossistema oferecem vantagens imenso tooboth programadores e IT profissionais.

Os programadores tirar tooDocker contentores rapidamente, porque acima de todos os faz através de contentores de Linux e Windows:

* Que podem utilizar comandos simples, incrementais toocreate uma imagem fixa que seja fácil toodeploy e podem automatizar a criação essas imagens com um dockerfile
* Podem partilhar essas imagens facilmente com simples, [git](https://git-scm.com/)-estilo push e pull comandos demasiado[pública](https://registry.hub.docker.com/) ou [os registos do docker privada](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Podem pensar em componentes de aplicação isolados, em vez de computadores
* Podem utilizar um grande número de ferramentas que compreendem os contentores do Docker e as diferentes imagens de base

### <a name="container-benefits-for-operations-and-it-professionals"></a>Vantagens dos contentores para profissionais de operações e de TI
IT e profissionais de operações também beneficiam da combinação de Olá de contentores e máquinas virtuais.

* Os serviços contidos estão isolados do ambiente de execução do anfitrião de VM
* O código contido é verificavelmente idêntico
* Os serviços contidos podem ser iniciados, parados e movidos rapidamente entre ambientes de desenvolvimento, teste e produção.

Funcionalidades como estes&mdash;e não existirem mais&mdash;excite estabelecidas empresas, em que as organizações de tecnologia de informações profissionais que a tarefa de Olá dos recursos de ajuste&mdash;, incluindo a capacidade de processamento puro&mdash; toohello tarefas necessárias toonot apenas permaneça na empresa, mas aumenta a satisfação do cliente e alcançar. Pequenas empresas, ISVs e startups tem exatamente Olá mesmo requisito, mas poderá descrever-forma diferente.

## <a name="what-are-virtual-machines-good-for"></a>Para que servem as máquinas virtuais?
Máquinas virtuais fornecem o principal de Olá da informática em nuvem e que não irá alterar. Se as máquinas virtuais iniciar mais lentamente, ter um maior requisitos de espaço de disco e não mapeiam diretamente tooa micro-serviços arquitetura, têm muito importantes vantagens:

1. Por predefinição, têm proteções de segurança predefinidas muito mais robustas para o computador anfitrião
2. Suportam configurações dos principais SO e aplicações
3. Têm ecossistemas de ferramentas muito mais duradouros para comando e controlo
4. Fornecem execução Olá contentores de toohost de ambiente

último item de Olá é importante, porque uma aplicação contida ainda necessita de um sistema operativo específico e o tipo de CPU, consoante as chamadas de Olá aplicação Olá tornará. É importante tooremember instalar contentores em VMs porque contêm aplicações Olá pretende toodeploy; contentores não são substituições para as VMs ou sistemas operativos.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>Comparação pormenorizada de funcionalidades entre VMs e contentores
Olá tabela seguinte descreve um muito elevado em tipo de Olá nível de funcionalidade diferenças que&mdash;sem muito trabalho adicional&mdash;existir entre VMs e Linux contentores. Tenha em atenção que pode ser maior ou menor desejável, consoante as suas próprias aplicações necessita de algumas funcionalidades e que tal como acontece com todos os softwares, trabalho adicional fornece maior suporte de funcionalidades, especialmente na área de Olá de segurança.

| Funcionalidade | VMs | Contentores |
|:--- | --- | --- |
| Suporte para segurança “predefinido” |maior tooa |tooa grau ligeiramente inferior |
| Memória no disco necessária |SO completo e aplicações |Requisitos de aplicações apenas |
| Tempo decorrido toostart cópias de segurança |Substancialmente superior: arranque do SO e carregamento das aplicações |Substancialmente mais curto: apenas aplicações precisam de toostart porque kernel já está em execução |
| Portabilidade |Portátil com preparação adequada |Portátil dentro do formato da imagem; tipicamente mais pequena |
| Automatização de Imagem |Varia bastante, dependendo do SO e das aplicações |[Registo Docker](https://registry.hub.docker.com/); outras |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>Criar e gerir grupos de VMs e contentores
Nesta fase, os arquitetos, programadores ou especialistas em operações de TI devem estar a pensar: “Posso automatizar ISTO tudo; É mesmo Datacenter como Serviço!”.

Estiver correto, podem ser e existem qualquer número de sistemas, muitas das quais pode já utilizar, que podem ser gerir grupos de VMs do Azure e injetar código personalizado com scripts, muitas vezes, Olá [CustomScriptingExtension para Windows](https://msdn.microsoft.com/library/azure/dn781373.aspx) ou Olá [CustomScriptingExtension para Linux](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/). Pode automatizar&mdash; e se calhar até já o fez&mdash; as suas implementações do Azure com o PowerShell ou os scripts da CLI do Azure.

Estas capacidades são, muitas vezes, em seguida, como o tootools migrados [Puppet](https://puppetlabs.com/) e [Chef](https://www.chef.io/) tooautomate Olá criação de configuração e para as VMs ao dimensionamento. (Seguem-se algumas hiperligações demasiado[utilizar estas ferramentas com o Azure](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Modelos dos grupos de recursos do Azure
Mais recentemente, o Azure lançadas Olá [gestão de recursos do Azure](../articles/resource-manager-deployment-model.md) REST API e toouse de ferramentas do PowerShell e da CLI do Azure atualizada-lo facilmente. Pode implementar, modificar ou voltar a implementar topologias de aplicação completo utilizando [modelos Azure Resource Manager](../articles/resource-group-authoring-templates.md) com a utilização da API de gestão de recursos do Azure de Olá:

* Olá [portal do Azure utilizando modelos](https://github.com/Azure/azure-quickstart-templates)&mdash;sugestão, utilize o botão de "DeployToAzure" Olá
* Olá [CLI do Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>Implementação e gestão de grupos inteiros de VMs do Azure e contentores
Existem vários sistemas populares que podem implementar grupos inteiros de VMs e instalar o Docker (ou outros sistemas anfitriões de contentores de Linux) nas mesmas como um grupo automatizável. Para obter hiperligações diretas, consulte Olá [contentores e ferramentas](#containers-and-vm-technologies) secção abaixo. Existem vários sistemas que fazer esta extensão de maior ou menor tooa e esta lista não é exaustiva. Consoante as suas competências e os seus cenários, podem ser úteis ou não.

O Docker tem um conjunto de ferramentas de criação de VMs próprio ([docker-machine](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) e uma ferramenta de gestão de clusters de contentores do Docker de balanceamento de carga ([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Além disso, Olá [extensão da VM do Azure Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) vem com suporte de predefinido para [ `docker-compose` ](https://docs.docker.com/compose/), que pode implementar configurado contentores da aplicação através de vários contentores.

Além disso, pode experimentar o [Data Center Operating System (DCOS) da Mesosphere](http://docs.mesosphere.com). DCOS baseia-se no Olá open source [mesos](http://mesos.apache.org/) "kernel sistemas distribuídos" que permite tootreat seu centro de dados como um serviço endereçável. Tem pacotes incorporados para vários sistemas importantes, como o [Spark](http://spark.apache.org/) e o [Kafka](http://kafka.apache.org/) (entre outros), bem como serviços incorporados, como o [Marathon](https://mesosphere.github.io/marathon/) (um sistema de controlo de contentores) e o [Chronos](https://mesos.github.io/chronos/) (um agendador distribuído). O Mesos foi obtido com base em lições aprendidas na Twitter, na AirBnB e noutras empresas à escala da Web. Também pode utilizar **swarm** como motor de orquestração Olá.

Além disso, o [kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) é um sistema de código aberto para gestão de VMs e grupos de contentores, obtido a partir de lições aprendidas na Google. Pode utilizar o mesmo [kubernetes com weave suporte de redes tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave).

[Deis](http://deis.io/overview/) é uma abertura "Plataforma-como-um-serviço" (PaaS) que torna mais fácil toodeploy de origem e gerir aplicações nos seus próprios servidores. Deis compilações após Docker e CoreOS tooprovide uma PaaS simples com um fluxo de trabalho Heroku-inspired.

O [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html), uma distribuição de Linux com uma pegada otimizada, suporte para Docker e o seu próprio sistema de contentores chamado [rkt](https://github.com/coreos/rkt), também tem uma ferramenta de gestão de grupos de contentores, denominada [fleet](https://coreos.com/fleet/docs/latest/).

O Ubuntu, outra distribuição de Linux muito popular, suporta o Docker sem problemas, mas também suporta [clusters do Linux (estilo LXC)](https://help.ubuntu.com/lts/serverguide/lxc.html).

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Ferramentas para trabalhar com VMs do Azure e contentores
Trabalhar com contentores e VMs do Azure envolve ferramentas. Esta secção fornece uma lista de apenas alguns dos conceitos de Olá mais útil ou importantes de ferramentas e sobre contentores, grupos e a configuração de maior de Olá e ferramentas de orquestração utilizadas com os mesmos.

> [!NOTE]
> Esta área é alterar amazingly rapidamente e, enquanto ocorrerá nosso tookeep melhor neste tópico e respetivas ligações segurança toodate, também poderá ser uma tarefa impossível. Certifique-se de que efetua uma procura interessantes assuntos tookeep segurança toodate!
>
>

### <a name="containers-and-vm-technologies"></a>Tecnologias de contentores e VMs
Algumas tecnologias de contentores de Linux:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS e rkt](https://github.com/coreos/rkt)
* [Open Container Project](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Ligações para o Contentor do Windows:

* [Windows Containers](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Ligações para o Visual Studio Docker:

* [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Ferramentas do Docker:

* [Daemon do Docker](https://docs.docker.com/installation/#installation)
* Clientes de Docker
  * [Cliente de Docker do Windows no Chocolatey](https://chocolatey.org/packages/docker)
  * [Instruções de instalação do Docker](https://docs.docker.com/installation/#installation)

Docker no Microsoft Azure:

* [Docker VM Extension for Linux on Azure (Extensão Docker VM para Linux no Azure)](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Docker VM Extension User Guide (Guia do Utilizador da Extensão Azure Docker VM)](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Utilizar Olá Docker extensão da VM do Olá Interface de linha de comandos do Azure (CLI do Azure)](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Utilizar Olá Docker extensão da VM do Olá portal do Azure](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Como máquina docker toouse no Azure](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Como toouse docker swarm no Azure com o](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Get Started with Docker and Compose on Azure (Introdução ao Docker e ao Compose no Azure)](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Rapidamente a utilizar um toocreate de modelo do grupo de recursos do Azure num anfitrião de Docker no Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [Olá suporte incorporado para `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) às aplicações contidas
* [Implementar um registo privado do Docker no Azure](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Distribuições do Linux e exemplos do Azure:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

Configuração, gestão de clusters e orquestração de contentores:

* [Fleet on CoreOS (Fleet no CoreOS)](https://coreos.com/fleet/docs/latest/)
* Deis

  * [Concluir a implementação de cluster do guia tooautomated Kubernetes com CoreOS e Weave](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Data Center Operating System (DCOS) da Mesosphere](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) e [Hudson](http://hudson-ci.org/)

  * [Plug-in Jenkins VM Agent para o Azure](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [GitHub repo: Jenkins Storage Plug-in for Azure (Repositório do GitHub: Plug-in Jenkins Storage para o Azure)](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [Third Party: Hudson Slave Plug-in for Azure (Terceiros: Plug-in Hudson Slave para o Azure)](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [Third Party: Hudson Storage Plug-in for Azure (Terceiros: Plug-in Hudson Storage para o Azure)](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Automatização do Azure](https://azure.microsoft.com/services/automation/)

  * [Vídeo: Como tooUse da automatização do Azure com VMs com Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* PowerShell DSC para Linux

  * [Blogue: Como toodo DSC do Powershell para Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: Docker Client DSC (GitHub: DSC de Cliente do Docker)](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>Passos seguintes
Veja [Docker](https://www.docker.com) e [Windows Containers (Contentores do Windows)](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
