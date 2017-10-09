# <a name="securing-docker-containers-in-azure-container-service"></a>Proteger contentores do Docker no Azure Container Service

Este artigo apresenta considerações e recomendações para proteger contentores d Docker implementados no Azure Container Service. Muitas destas considerações aplicam-se, geralmente, os contentores de tooDocker implementados no Azure ou outros ambientes. 

## <a name="image-security"></a>Segurança das imagens

Os contentores são criados a partir de imagens que estão armazenadas num ou mais repositórios. Estes repositórios podem pertencer toopublic ou os registos do contentor privada. O[Docker Hub](https://hub.docker.com/) é um exemplo de um registo público. Um exemplo de um registo privado é Olá [Docker fidedigna registo](https://docs.docker.com/datacenter/dtr/2.0/), que pode ser instalado no local ou numa nuvem privada virtual. Também existem serviços de registo de contentores privados baseados na cloud, entre os quais o [Azure Container Registry](../articles/container-registry/container-registry-intro.md).

### <a name="public-and-private-images"></a>Imagens públicas e privadas
De um modo geral, tal como sucede com qualquer pacote de software publicado publicamente, as imagens de contentores disponíveis de forma pública não garantem a segurança. As imagens de contentores consistem em várias camadas de software, sendo que cada camada de software pode ter vulnerabilidades. É a origem de Olá toounderstand chave da imagem do contentor de Olá, incluindo Olá proprietário da imagem de Olá (toodetermine se se tratar de uma origem fiável ou não), hello é composto de camadas de software e Olá versões de software. 

Por exemplo, se ficarem toohello oficial [nginx repositório](https://hub.docker.com/_/nginx/) no Hub de Docker e navegue toohello **etiquetas** separador, consulte codificado por cores vulnerabilidades em cada imagem. Cada cor ilustra vulnerabilidade Olá de uma camada de software da imagem de Olá. Para obter mais informações sobre a análise de vulnerabilidades no Docker Hub, veja [Understanding official repos on Docker Hub](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/) (Compreender os repositórios oficiais no Docker Hub).

![Imagens de Nginx no Docker Hub](./media/container-service-security/docker-hub-nginx.png)

As empresas mais importantes para si profundamente sobre segurança e tooprotect próprios contra ataques de segurança devem armazenar e obter imagens a partir de um registo privado, tais como o registo de contentor do Azure ou Docker fidedigna registo. Em adição tooproviding um registo privado gerido, o registo de contentor do Azure suporta [autenticação baseada em principal do serviço](../articles/container-registry/container-registry-authentication.md) através do Azure Active Directory para fluxos de autenticação básica, incluindo o acesso baseado em funções para só de leitura, escrita e permissões de proprietário.

### <a name="image-security-scanning"></a>Análise de segurança das imagens

Mesmo quando utilizar um registo privado, é uma imagem de toouse boa ideia análise soluções para validação de segurança adicionais. Cada camada de software numa imagem de contentor é suscetível potencialmente toovulnerabilities independente de outras camadas numa imagem de contentor Olá. Como cada vez mais as empresas começar a implementar as respetivas cargas de trabalho de produção, com base nas tecnologias de contentor, análise de imagem torna-se importante tooensure prevenção de ameaças de segurança contra das suas organizações. 

Monitorização e análise, tais como soluções de segurança [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) e [Aqua segurança](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), entre outros, podem ser utilizado tooscan imagens do contentor no registo de privada e identificar potenciais vulnerabilidades. É importante fornecer profundidade de Olá toounderstand da análise que Olá diferentes soluções. Por exemplo, algumas podem fazer apenas verificações cruzadas de camadas das imagens relativamente a vulnerabilidades conhecidas. Estas soluções podem não estar tooverify capaz de software de camada de imagem incorporada através de determinado software do Gestor de pacote. Outras soluções têm uma integração de análises mais profunda e podem encontrar vulnerabilidades em qualquer software de pacotes.

### <a name="production-deployment-rules-and-audit"></a>Regras de implementação e auditoria de produção
Depois de uma aplicação é implementada na produção, é essencial tooset alguns tooensure de regras que as imagens utilizadas em ambientes de produção são seguras e não conter nenhuma vulnerabilidades.

* Como uma regra, as imagens com vulnerabilidades, mesmo menores, não devem ser permitidas toorun num ambiente de produção. Além disso, todas as imagens implementadas na produção deverá Idealmente ser guardadas numa select registo privada acessível tooa poucos. Também é importante tookeep Olá diversas tooensure de pequenas de imagens de produção que possam ser geridos com eficiência.

* Uma vez que esta origem de Olá toopinpoint disco rígido de software a partir de uma imagem de contentor publicamente disponíveis, é a imagens de toobuild boa prática do conhecimento de tooensure de origem da origem de Olá de camada de Olá. Quando um analisa vulnerabilidade numa imagem incorporada automática do contentor, os clientes podem encontrar uma resolução de tooa mais rápida do caminho. Com uma imagem pública, os clientes teria de raiz de Olá toofind de uma imagem pública toofix-lo ou obter outra imagem segura do publicador Olá.

* Uma imagem exaustivamente digitalizada implementada na produção não é assegurada toobe segurança toodate para duração Olá da aplicação Olá. Vulnerabilidades de segurança podem ser comunicadas para as camadas da imagem de Olá que não foram anteriormente conhecidas ou que foram introduzidas após a implementação de produção Olá. A auditoria periódica de imagens implementadas na produção é necessário tooidentify imagens que estão Desatualizadas ou que não foram atualizadas no tempo. Um poderá utilizar metodologias de implementação de blue verde e implementar imagens de contentor tooupdate mecanismos de atualização sem períodos de indisponibilidade. Análise de imagem pode ser feito com as ferramentas descritas no Olá anterior a secção. 

* Um pipeline de integração contínua (CI) toobuild imagens e a segurança integrada análise podem ajudar a manter segurados registos privados com imagens de contentores seguros. Olá análise de vulnerabilidade contempla a solução de CI de Olá assegura que as imagens que passaram todos os testes de Olá são enviadas registo privada toohello da qual produção cargas de trabalho são implementadas. Falha no pipeline CI garante que imagens vulneráveis não são enviadas para o registo de privada Olá utilizado para implementações de carga de trabalho de produção. Também automatiza a análise de segurança de imagens se houver um número significativamente grande de imagens. Caso contrário, auditar manualmente as imagens relativamente a vulnerabilidades pode ser extremamente moroso e suscetível a erros.

## <a name="host-level-container-isolation"></a>Isolamento de contentores ao nível do anfitrião
Quando um cliente implementa aplicações de contentor em recursos do Azure, estas são implementadas ao nível da subscrição nos grupos de recursos e não são multi-inquilino. Isto significa que se um cliente partilha uma subscrição com outras pessoas, não existem nenhum limites que podem ser criados entre duas implementações no Olá mesma subscrição. Por conseguinte, a segurança ao nível do contentor. não é garantida. 

Também é toounderstand crítico que contentores partilham kernel Olá e recursos de Olá do anfitrião de Olá (o que, no serviço de contentor do Azure é uma VM do Azure num cluster). Por este motivo, os contentores em execução em produção têm de ser executados no modo de utilizador não privilegiado. Um contentor a ser executado com privilégios de raiz pode comprometer a todo o ambiente Olá. Com acesso de nível de raiz no contentor, um hacker poderem obter acesso privilégios totais de raiz de toohello no anfitrião de Olá. Além disso, é importante toorun contentores com sistemas de ficheiros só de leitura. Isto impede que alguém que tenha acesso toohello comprometido contentor toowrite scripts maliciosos toohello sistema de ficheiros e obter acesso tooother ficheiros. Da mesma forma, é recursos de Olá toolimit importante (por exemplo, memória, CPU e largura de banda de rede) atribuídos tooa contentor. Isto ajuda a impedir que hackers sobrecarreguem a recursos e tentar obter atividades ilegais, como fraude de cartão de crédito ou de extração bitcoin, que pode impedir que outros contentores em execução no Olá anfitrião ou cluster.

## <a name="orchestrator-considerations"></a>Considerações de orquestração

Cada orquestrador disponível no Azure Container Service tem as suas próprias considerações de segurança. Por exemplo, deve limitar diretas SSH de nós de tooorchestrator de acesso no serviço de contentor. Em vez disso, deve utilizar a IU de cada orchestrator ou ferramentas de linha de comandos (tais como `kubectl` para Kubernetes) ambiente de contentor de Olá toomanage sem aceder aos anfitriões Olá. Para obter mais informações, consulte [tornar um Kubernetes, DC/OS ou Docker Swarm cluster tooa de ligação remota](../articles/container-service/kubernetes/container-service-connect.md).

Para informações adicionais de segurança específicas do orchestrator, consulte Olá os seguintes recursos:

* **Kubernetes**: [Security Best Practices for Kubernetes Deployment](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html) (Melhores Práticas de Segurança para Implementação de Kubernetes)

* **DC/OS**: [Securing Your Cluster](https://dcos.io/docs/1.8/administration/securing-your-cluster/) (Proteger o Seu Cluster)

* **Docker Swarm**: [Docker Security](https://www.docker.com/docker-security) (Segurança do Docker)

## <a name="next-steps"></a>Passos seguintes

* Para obter mais informações sobre a segurança de arquitetura e contentor de Docker, consulte [introdução tooContainer segurança](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Para informações sobre a segurança da plataforma do Azure, consulte Olá [Centro de segurança do Azure](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
