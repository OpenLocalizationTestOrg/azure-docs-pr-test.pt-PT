# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Perguntas mais frequentes sobre a migração do Gestor de recursos de tooAzure clássico

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Este plano de migração afeta algum dos meus serviços ou aplicações existentes que são executados em máquinas virtuais do Azure? 

Não. VMs de Olá (clássica) são totalmente suportados serviços na disponibilidade geral. Pode continuar toouse tooexpand estes recursos os requisitos de espaço no Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>O que acontece toomy VMs, se não a planear na migração em Olá quase futuro? 

Não podemos são descontinuar Olá existente APIs e recurso modelo clássico. Queremos toomake migração fácil, tendo em consideração Olá funcionalidades que estão disponíveis no modelo de implementação do Resource Manager Olá avançadas. Recomendamos vivamente que reveja [alguns avanços Olá](../articles/azure-resource-manager/resource-manager-deployment-model.md) que fazem parte do IaaS em Gestor de recursos.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>O que significa este plano de migração para as minhas ferramentas existentes? 

Atualizar o modelo de implementação do Gestor de recursos de toohello ferramentas é uma das alterações mais importantes de Olá que tenham tooaccount no seu plano de migração.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Quanto tempo será o período de indisponibilidade do Olá plane gestão? 

Depende do número de Olá de recursos que estão a ser migrados. Para implementações mais pequenas (alguns dezenas de VMs), migração completa Olá deve demorar menos de uma hora. Para implementações em grande escala (centenas de VMs), a migração de Olá pode demorar algumas horas.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Depois de os recursos migrados forem considerados no Resource Manager, posso reverter a migração? 

Pode abortar a migração, desde que os recursos de Olá estão numa Olá preparado estado. A reversão não é suportada depois recursos Olá terem sido migrados com êxito através de operação de consolidação de Olá.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>Pode posso reverter a minha migração se falhar de operação de consolidação de Olá? 

Não é possível abortar migração se a operação de consolidação Olá falhar. Todas as operações de migração, incluindo a operação de consolidação de Olá, são idempotent. Por isso, recomendamos a repetir a operação de Olá após um curto período de tempo. Se ainda enfrentam um erro, crie um pedido de suporte ou crie uma mensagem num fórum com Olá ClassicIaaSMigration Etiquetar no nosso [fórum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>É necessário toobuy outro circuito de expressroute se tiver toouse IaaS em Gestor de recursos? 

Não. Iremos recentemente ativada [mover circuitos ExpressRoute do modelo de implementação Resource Manager do Olá toohello clássico](../articles/expressroute/expressroute-move.md). Não tem toobuy um circuito de ExpressRoute nova se já tiver uma.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>O que acontece se tiver configurado políticas de Controlo de Aceso Baseado em Funções nos meus recursos de IaaS clássicos? 

Durante a migração, os recursos Olá transformar do Gestor de tooResource clássico. Por isso, recomendamos que planeie atualizações de políticas RBAC Olá que necessitam de toohappen após a migração.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Criei uma cópia de segurança das minhas VMs clássicas num cofre do Backup. Pode migrar as minhas VMs do modo de Gestor de tooResource modo clássico e protegê-los num cofre dos serviços de recuperação? 

Pontos de recuperação VM Clássicos no Cofre de cópia de segurança não migra automaticamente tooa Cofre de serviços de recuperação quando move Olá VM do clássico tooResource modo Manager. Siga estes passos tootransfer as cópias de segurança VM:

1. No Cofre de cópia de segurança de Olá, aceda toohello **itens protegidos** separador e selecione Olá VM. Clique em [Parar Proteção](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deixe a opção *Eliminar dados de cópia de segurança associados* **desmarcada**.
2. Elimine a extensão de cópia de segurança/instantâneo de Olá da Olá VM.
3. Migre máquina virtual de Olá do modo de Gestor de tooResource modo clássico. Certifique-se a informações de rede e de armazenamento de Olá máquina de virtual toohello correspondente também é migrada tooResource Manager modo.
4. Criar um cofre dos serviços de recuperação e configurar a cópia de segurança Olá migrar máquina virtual a utilizar **cópia de segurança** ação por cima do dashboard do cofre. Para informações detalhadas sobre a cópia de segurança dos serviços de recuperação do tooa VM do cofre, consulte o artigo Olá, [proteger as VMs do Azure com um cofre dos serviços de recuperação](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Pode posso validar a minha subscrição ou recursos toosee se não estiverem com capacidade de migração? 

Sim. Na opção de migração de plataforma suportada Olá, o primeiro passo de Olá na preparação da migração é toovalidate se recursos Olá são capazes de migração. No caso de Olá validar falha da operação, receber mensagens por motivos de Olá todos os não é possível concluir a migração de Olá.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>O que acontece se executar um erro de quota ao preparar os recursos de IaaS Olá para migração? 

Recomendamos que abortar a migração e, em seguida, inicie um quotas de Olá de tooincrease de pedido de suporte na região de olá onde estiver Olá migrar VMs. Depois de Olá quota pedido for aprovado, pode começar a executar os passos de migração de Olá novamente.

## <a name="how-do-i-report-an-issue"></a>Como posso comunicar problemas? 

Publique os problemas e questões sobre migração tooour [fórum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), com a palavra-chave de Olá ClassicIaaSMigration. Recomendamos que publique todas as suas perguntas neste fórum. Se tiver um contrato de suporte, está toolog boas-vindas, bem como um pedido de suporte.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>E se posso não gostar Olá os nomes de recursos de Olá Olá plataforma escolheu durante a migração? 

Todos os recursos de Olá que forneça explicitamente os nomes no modelo de implementação clássica Olá são mantidos durante a migração. Em alguns casos, são criados recursos novos. Por exemplo, é criada uma interface de rede para cada VM. Não é atualmente suportado Olá capacidade toocontrol Olá os nomes destes recursos novos criado durante a migração. Inicie os votos para esta funcionalidade em Olá [fórum de comentários do Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Posso migrar circuitos do ExpressRoute utilizados em várias subscrições com ligações de autorização? 

Os circuitos do ExpressRoute que utilizem ligações de autorização em várias subscrições não podem ser migrados automaticamente sem tempo de inatividade. Temos orientações que mostram como utilizar passos manuais para migrá-los. Consulte [migrar ExpressRoute circuitos e associadas redes virtuais do modelo de implementação Resource Manager do Olá toohello clássico](../articles/expressroute/expressroute-migration-classic-resource-manager.md) para passos e mais informações.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Posso recebeu uma mensagem *"VM está a comunicar Olá estado geral de agente como não está preparado. Por conseguinte, não pode ser migrada Olá VM. Certifique-se de que Olá agente da VM está a comunicar o estado geral de agente como pronto"* ou *"VM contém a extensão não está a ser reportado cujo estado de Olá VM. Por este motivo, esta VM não pode ser migrada”. *

Esta mensagem é recebida quando Olá VM não tem conectividade de saída toohello internet. agente da VM Olá utiliza a conta de armazenamento do Azure de Olá de tooreach de conectividade de saída para atualizar o estado do agente Olá a cada cinco minutos.
