>[!NOTE]
> Pode deixar comentários nesta página para comentários ou através de [comentários Azure](https://feedback.azure.com/forums/216843-virtual-machines) #azerrormessage ativado por etiqueta.

## <a name="error-response-format"></a>Formato de resposta de erro 
As VMs do Azure utilizam Olá seguir o formato JSON da resposta de erro:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Uma resposta de erro inclui sempre um código de estado e um objeto de erro. Cada objeto erro contém sempre um código de erro e uma mensagem. Se hello é criada a VM com um modelo, o objeto de erro Olá também contém uma secção de detalhes que contém um nível interno de códigos de erro e a mensagem. Normalmente, hello mais nível interno de mensagem de erro é Olá raiz falha.


## <a name="common-virtual-machine-management-errors"></a>Erros comuns de gestão de máquina virtual

Esta secção lista Olá mensagens de erro comuns que poderão surgir quando gerir VMs:

|  Código de erro  |  Mensagem de erro  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Falha na concessão de tooacquire ao criar o disco '{0}' com o blob URI {1}. BLOB já está em utilização.  |  
|  AllocationFailed  |  Falha na alocação. Tente reduzir o tamanho da VM Olá ou número de VMs, tente novamente mais tarde ou experimente implementar tooa conjunto de disponibilidade diferente ou localização do Azure diferente.  |  
|  AllocationFailed  |  Olá alocação da VM falhou devido a um erro interno tooan. Volte a tentar mais tarde ou experimente implementar tooa noutra localização.  |
|  ArtifactNotFound  |  Olá extensão da VM com o publicador '{0}' e o tipo '{1}' não foi possível encontrar na localização '{2}'.  |
|  ArtifactNotFound  |  Tipo de extensão com o publicador '{0}', '{1}' e não foi possível encontrar a versão de processador do tipo '{2}' no repositório de extensão de Olá.  |
|  ArtifactVersionNotFound  |  Nenhuma versão encontrada no repositório de artefactos Olá que satisfaça Olá pediu a versão '{0}'.  |
|  ArtifactVersionNotFound  |  Nenhuma versão encontrada no repositório de artefactos Olá que satisfaça Olá pedida versão com \\{1 \\}' publicador' e '{2}' de tipo '{0}' para a extensão VM.  |
|  AttachDiskWhileBeingDetached  |  Não é possível anexar o disco '{0}' de dados tooVM '{1}' porque o disco de Olá está a ser desanexado. Aguarde até a Olá disco ser totalmente desanexado e, em seguida, tente novamente.  |
|  BadRequest  |  Alinhada ' conjuntos de disponibilidade ainda não são suportados nesta região.  |
|  BadRequest  |  Adição de uma VM com discos geridos toonon gerido pelo conjunto de disponibilidade ou adição de uma VM com o blob com base em discos toomanaged do conjunto de disponibilidade não é suportada. Crie um conjunto de disponibilidade com a propriedade 'geridos' definida na ordem tooadd uma VM com discos geridos tooit.  |
|  BadRequest  |  Discos geridos não são suportados nesta região.  |
|  BadRequest  |  Múltiplas VMExtensions por processador que não é suportada para o SO do tipo '{0}'. VMExtension {1} Handler '{2}' já foi adicionada ou especificada na entrada.  |
|  BadRequest  |  Operação '{0}' não é suportada no recurso {1} com discos geridos.  |
|  CertificateImproperlyFormatted  |  Olá representação de JSON do segredo obtida {0} tem um campo de dados que não é um ficheiro PFX corretamente formatado ou palavra-passe de Olá fornecida não descodifica ficheiro PFX de Olá corretamente.  |
|  CertificateImproperlyFormatted  |  dados Olá obtidos {0} não são desserializáveis no JSON.  |
|  Conflito  |  Redimensionamento do disco é permitido apenas quando criar uma VM ou quando Olá VM é desalocada.  |
|  ConflictingUserInput  |  Não é possível anexar o disco '{0}' como disco de Olá já é propriedade de VM '{1}'.  |
|  ConflictingUserInput  |  Grupos de recursos de origem e de destino são Olá mesmo.  |
|  ConflictingUserInput  |  Contas de armazenamento de origem e de destino para o disco {0} são diferentes.  |
|  ContainerAlreadyOnLease  |  Já houver uma concessão no contentor de armazenamento de Olá que contém o blob de Olá com o URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  o pedido de movimentação de Olá recursos contém recursos KeyVault que são referenciados por uma ou mais {0} s no pedido de Olá. Isto não é suportado atualmente na subscrição mover cruzada. Verifique os detalhes do erro Olá para Olá Ids de recurso de KeyVault.  |
|  DiagnosticsOperationInternalError  |  Ocorreu um erro interno ao processar o perfil de diagnóstico da VM {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  Blob {0} já está a ser utilizado por outro disco pertencente tooVM '{1}'. Pode examinar os metadados do blob Olá para obter informações de referência do disco Olá.  |
|  DiskBlobNotFound  |  Não é possível toofind VHD blob com {0} URI para o disco '{1}'.  |
|  DiskBlobNotFound  |  Não é possível toofind VHD blob com o URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  segredo {0} não tem etiquetas de {1} Olá. Atualizar a versão secreta Olá, adicione etiquetas Olá necessário e repita.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  Abertura do valor de {0} secreta utilizando {1} chave falhou.  |
|  DiskImageNotReady  |  {0} de imagem de disco está num Estado de {1}. Tente novamente quando a imagem está pronta.  |
|  DiskPreparationError  |  Ocorreram um ou mais erros durante a preparação de discos VM. Consulte a vista de instância de disco para obter mais detalhes.  |
|  DiskProcessingError  |  Processamento de disco interrompida como Olá VM tem outros discos no discos com falhas.  |
|  ImageBlobNotFound  |  Não é possível toofind VHD blob com {0} URI para o disco '{1}'.  |
|  ImageBlobNotFound  |  Não é possível toofind VHD blob com o URI {0}.  |
|  IncorrectDiskBlobType  |  Os blobs de disco só podem ser de BLOBs de páginas de tipo. {0} blob para o disco '{1}' é do tipo blob de blocos.  |
|  IncorrectDiskBlobType  |  Os blobs de disco só podem ser de BLOBs de páginas de tipo. Blob {0} é do tipo '{1}'.  |
|  IncorrectImageBlobType  |  Os blobs de disco só podem ser de BLOBs de páginas de tipo. {0} blob para o disco '{1}' é do tipo blob de blocos.  |
|  IncorrectImageBlobType  |  Os blobs de disco só podem ser de BLOBs de páginas de tipo. Blob {0} é do tipo '{1}'.  |
|  InternalOperationError  |  Não foi possível resolver a conta de armazenamento {0}. Certifique-se de que foi criada através de Olá fornecedor de recursos de armazenamento no Olá mesma localização que Olá recursos de computação.  |
|  InternalOperationError  |  tarefas de atingir o objetivo de {0} falhou.  |
|  InternalOperationError  |  Ocorreu um erro na validação do perfil de rede Olá da VM '{0}'.  |
|  InvalidAccountType  |  Olá AccountType {0} é inválido.  |
|  InvalidParameter  |  Olá valor do parâmetro {0} é inválido.  |
|  InvalidParameter  |  palavra-passe a Olá do Admin especificada não é permitida.  |
|  InvalidParameter  |  "palavra-passe de Olá fornecido tem de estar entre 0}-\ {1 \} carateres de comprimento e deve satisfazer, pelo menos, {2} dos requisitos de complexidade de palavra-passe do seguinte Olá: <ol><li> Contém um caráter em maiúsculas</li><li>Contém um caráter em minúsculas</li><li>Contém um dígito numérico</li><li>Contém um caráter especial.</li></ol>  |
|  InvalidParameter  |  Olá nome de utilizador de Admin especificado não é permitida.  |
|  InvalidParameter  |  Não é possível anexar um disco de SO existente se hello VM é criada a partir de uma imagem de plataforma ou de utilizador.  |
|  InvalidParameter  |  {0} de nome do contentor é inválido. Os nomes de contentor tem de ter entre 3 e 63 carateres de comprimento e contenham apenas carateres alfanuméricos minúsculos e hífenes. Hífen tem de ser antecedido e seguido por um caráter alfanumérico.  |
|  InvalidParameter  |  Nome de contentor {0} no URL {1} é inválido. Os nomes de contentor tem de ter entre 3 e 63 carateres de comprimento e contenham apenas carateres alfanuméricos minúsculos e hífenes. Hífen tem de ser antecedido e seguido por um caráter alfanumérico.  |
|  InvalidParameter  |  nome do blob Olá no URL {0} contém uma barra. Isto atualmente não é suportado para discos.  |
|  InvalidParameter  |  Olá URI {0} procura toobe URI de blob correto.  |
|  InvalidParameter  |  Um disco com o nome "{0}" já utiliza Olá mesmo LUN: {1}.  |
|  InvalidParameter  |  Um disco chamado '{0}' já existe.  |
|  InvalidParameter  |  Não é possível especificar substituições da imagem de utilizador para um disco já definido no Olá especificado referência da imagem.  |
|  InvalidParameter  |  Um disco com o nome "{0}" já utiliza Olá {1} do mesmo URL de VHD.  |
|  InvalidParameter  |  Olá {0} de contagem de domínio de falhas especificado tem de estar no intervalo de Olá {1} too\ {2\}.  |
|  InvalidParameter  |  Olá licença tipo {0} é inválido. Tipos de licenças válidos são: Windows_Client ou Windows_Server, sensíveis a maiúsculas e minúsculas.  |
|  InvalidParameter  |  Nome do anfitrião Linux não pode exceder {0} carateres de comprimento ou conter Olá seguintes carateres: {1}.  |
|  InvalidParameter  |  Caminho de destino para chaves públicas Ssh está actualmente limitada tooits predefinido valor {0} tooa devida conhecido problema do agente de aprovisionamento do Linux.  |
|  InvalidParameter  |  Já existe um disco no LUN {0}.  |
|  InvalidParameter  |  {0} de subscrição de pedido de Olá tem de corresponder ao hello subscrição {1} contida no id de disco gerido Olá.  |
|  InvalidParameter  |  Dados personalizados de osprofile tem de ser codificação Base64 e com um comprimento máximo de carateres {0}.  |
|  InvalidParameter  |  Nome do blob no URL {0} tem de terminar com a extensão '{1}'.  |
|  InvalidParameter  |  {0}' não é um válido capturado VHD blob prefixo de nome. Um prefixo válido coincide com regex '{1}'.  |
|  InvalidParameter  |  Não não possível adicionar certificados tooyour VM se o agente da VM Olá não está aprovisionada.  |
|  InvalidParameter  |  Já existe um disco no LUN {0}.  |
|  InvalidParameter  |  Não é possível toocreate Olá VM porque Olá solicitada {0} de tamanho não está disponível no cluster de olá onde o conjunto de disponibilidade de Olá está atribuído. Olá disponíveis são: {1}. Leia mais VM na estratégia de https://aka.ms/azure-resizevm o redimensionamento.  |
|  InvalidParameter  |  Olá pedida {0} de tamanho VM não está disponível na região atual Olá. os tamanhos de Olá disponíveis na região atual Olá são: {1}. Saiba mais em tamanhos de VM Olá disponíveis em cada região na https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Olá pedida {0} de tamanho VM não está disponível na região atual Olá. Saiba mais em tamanhos de VM Olá disponíveis em cada região na https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Nome de utilizador de admin do Windows não pode ser mais do que {0} carateres longo, terminar com um ponto ou contenham Olá seguintes carateres: {1}.  |
|  InvalidParameter  |  Nome de computador do Windows não pode ser mais do que {0} carateres comprimento, ser inteiramente numérico ou contenham Olá seguintes carateres: {1}.  |
|  MissingMoveDependentResources  |  pedido de movimentação de recursos Olá não contém todos os recursos dependentes de Olá. Verifique os detalhes do erro de falta de ids de recurso.  |
|  MoveResourcesHaveInvalidState  |  pedido de mover recursos Olá contém as VMs que estão associadas a contas de armazenamento inválido. Verifique os detalhes para estes ids de recurso e os nomes das contas de armazenamento referenciado.  |
|  MoveResourcesHavePendingOperations  |  Olá pedido de movimentação de recursos contém recursos para o qual está pendente uma operação. Verifique os detalhes para estes ids de recurso. Repita a operação depois de concluir Olá operações pendentes.  |
|  MoveResourcesNotFound  |  Olá mover recursos pedido contém recursos que não não possível encontrar. Verifique os detalhes para estes ids de recurso.  |
|  NetworkingInternalOperationError  |  Erro de alocação de rede desconhecido.  |
|  NetworkingInternalOperationError  |  Erro de alocação de rede desconhecido  |
|  NetworkingInternalOperationError  |  Ocorreu um erro interno no processamento de perfil de rede Olá VM.  |
|  notFound  |  Não é possível localizar o Olá do conjunto de disponibilidade {0}.  |
|  notFound  |  Máquina Virtual de origem '{0}' especificado num pedido de Olá não existe nesta localização do Azure.  |
|  notFound  |  Inquilino com {0} id não foi encontrado.  |
|  notFound  |  Não é possível localizar o Olá {0} de imagem.  |
|  NotSupported  |  tipo de licença de Olá é {0}, mas {1} de blob de imagem de Olá não está no local.  |
|  OperationNotAllowed  |  Não é possível eliminar {0} de conjunto de disponibilidade. Antes de eliminar um conjunto de disponibilidade, certifique-se que não contém nenhuma VM.  |
|  OperationNotAllowed  |  Alterar disponibilidade SKU de conjunto a partir de 'Aligned' too'Classic' não é permitida.  |
|  OperationNotAllowed  |  Não é possível modificar as extensões na VM de Olá quando Olá VM não está em execução.  |
|  OperationNotAllowed  |  ação de captura de Olá só é suportada numa máquina Virtual com discos baseadas em BLOBs. Utilize Olá 'Imagem' recursos APIs toocreate uma imagem de uma Máquina Virtual gerida.  |
|  OperationNotAllowed  |  Não é possível criar Olá {0} de recurso de imagem {1} até que a imagem foi criada com êxito.  |
|  OperationNotAllowed  |  Atualizações tooencryptionSettings não é permitido quando a VM está alocada, repita a operação depois de VM é desalocada  |
|  OperationNotAllowed  |  Não é suportada a adição de um disco gerido de tooa VM com discos baseadas em BLOBs.  |
|  OperationNotAllowed  |  número máximo de Olá de discos de dados permitido toobe ligado tooa VM deste tamanho é {0}.  |
|  OperationNotAllowed  |  Não é suportada a adição de um tooVM de disco baseadas em BLOBs com discos geridos.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na imagem '{1}' desde Olá que imagem está marcada para eliminação. Só poderá repita a operação de eliminação de Olá (ou aguarde uma um toocomplete em curso).  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' desde Olá que VM está generalizada.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida porque a coleção de ponto de restauro '{1}' está marcada para eliminação.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na extensão de VM '{1}' porque está marcado para eliminação. Só poderá repita a operação de eliminação de Olá (ou aguarde uma um toocomplete em curso).  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida uma vez que as máquinas virtuais Olá '{1}' que está a ser aprovisionados com imagem Olá '{2}'.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida uma vez que Olá ScaleSet de Máquina Virtual '{1}' está atualmente a utilizar Olá imagem '{2}'.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' desde Olá que VM está marcada para eliminação. Só poderá repita a operação de eliminação de Olá (ou aguarde uma um toocomplete em curso).  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' uma vez que Olá VM é desalocada ou marcado toobe desalocada.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' desde Olá que VM está em execução. . Desligue explicitamente caso encerrar Olá VM a partir de dentro de Olá sistema operativo.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' desde Olá que VM é desalocada não.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' uma vez que a VM tem a extensão '{2}' num Estado com falhas.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '{1}' uma vez que está em curso outra operação.  |
|  OperationNotAllowed  |  operação de Olá '{0}' necessita de Olá Máquina Virtual '{1}' toobe generalizado.  |
|  OperationNotAllowed  |  operação de Olá requer Olá toobe VM em execução (ou defina toorun).  |
|  OperationNotAllowed  |  Disco com o tamanho de {0} GB, o que é menor que Olá tamanho {1}GB do disco correspondente na imagem, não é permitida.  |
|  OperationNotAllowed  |  Extensões de conjunto de dimensionamento de VM de mensagens em fila do processador '{0}' podem ser adicionadas apenas no momento de Olá da criação de conjunto de dimensionamento de VM.  |
|  OperationNotAllowed  |  Extensões de conjunto de dimensionamento de VM de mensagens em fila do processador '{0}' podem ser eliminadas apenas momento Olá da eliminação do conjunto de dimensionamento de VM.  |
|  OperationNotAllowed  |  VM '{0}' já está a utilizar discos geridos.  |
|  OperationNotAllowed  |  VM '{0}' pertence too'Classic' '{1}' do conjunto de disponibilidade. Atualização Olá disponibilidade defina toouse 'Aligned' SKU e, em seguida, repita Olá conversão.  |
|  OperationNotAllowed  |  VM criada a partir da imagem não pode ter discos baseadas em BLOBs. Todos os discos têm discos toobe gerido.  |
|  OperationNotAllowed  |  Capturar não é possível concluir a operação porque hello VM não está generalizada.  |
|  OperationNotAllowed  |  Operações de gestão na VM '{0}' não são permitidas porque os discos VM estão a ser convertida toomanaged discos.  |
|  OperationNotAllowed  |  Uma operação em curso está a mudar o estado de energia de Máquina Virtual {0} too\ {1 \}. Execute {2} da operação após algum tempo.  |
|  OperationNotAllowed  |  Não é possível tooadd ou atualização Olá VM. Olá pedida {0} de tamanho VM poderá não estar disponível na unidade de alocação Olá existente. Leia mais VM na estratégia de https://aka.ms/azure-resizevm o redimensionamento.  |
|  OperationNotAllowed  |  Não é possível tooresize Olá VM porque Olá solicitada {0} de tamanho não está disponível no cluster de olá onde o conjunto de disponibilidade de Olá está atribuído. Olá disponíveis são: {1}. Leia mais VM na estratégia de https://aka.ms/azure-resizevm o redimensionamento.  |
|  OperationNotAllowed  |  Não é possível tooresize Olá VM porque Olá solicitada {0} de tamanho não está disponível no cluster de olá onde hello VM está atribuída. tooresize too\ sua VM {1 \} desalocar. (esta é uma operação de interrupção no Olá portal do Azure) e tente a operação de redimensionamento Olá novamente. Leia mais VM na estratégia de https://aka.ms/azure-resizevm o redimensionamento.  |
|  OSProvisioningClientError  |  Aprovisionamento do SO falhou para a VM '{0}' porque o SO de convidado de Olá está atualmente a ser aprovisionado.  |
|  OSProvisioningClientError  |  Falha no aprovisionamento do SO para a VM '{0}'. Detalhes do erro: {1} disponibilizar imagem de Olá se foi preparada corretamente (generalizada). <ul><li>Instruções para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  Falha na geração de chaves de anfitrião SSH. Detalhes do erro: {0}. tooresolve este problema, verifique se o agente de Linux está corretamente configurada. <ul><li>Pode verificar instruções Olá em: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Nome de utilizador especificado para Olá que VM é inválida para esta distribuição de Linux. Detalhes do erro: {0}.  |
|  OSProvisioningInternalError  |  Aprovisionamento do SO falhou para a VM '{0}' devido a um erro interno tooan.  |
|  OSProvisioningTimedOut  |  Aprovisionamento de SO para a VM '{0}' não foi concluída no Olá atribuído tempo. Olá VM ainda poderá concluir o aprovisionamento com êxito. Verifique o estado de aprovisionamento mais tarde.  |
|  OSProvisioningTimedOut  |  Aprovisionamento de SO para a VM '{0}' não foi concluída no Olá atribuído tempo. Olá VM ainda poderá concluir o aprovisionamento com êxito. Verifique o estado de aprovisionamento mais tarde. Além disso, certifique-se a imagem de Olá foi preparada corretamente (generalizada).   <ul><li>Instruções para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instruções para Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Aprovisionamento de SO para a VM '{0}' não foi concluída no Olá atribuído tempo. No entanto, o agente convidado da VM Olá foi detetado em execução. Isto sugere convidado Olá SO não foi corretamente preparado toobe utilizado como uma imagem de VM (com CreateOption = FromImage). tooresolve este problema, o Olá utilize VHD como é com CreateOption = Attach ou prepará-la corretamente para utilização como uma imagem:   <ul><li>Instruções para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instruções para Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Olá necessário tamanho da VM não está atualmente disponível na localização de Olá selecionado.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Recurso não é possível atualizar neste momento devido a atualização de plataforma tooongoing. Tente novamente mais tarde.  |
|  StorageAccountLimitation  |  Conta de armazenamento '{0}' não suporta os blobs de páginas que são necessárias toocreate discos.  |
|  StorageAccountLimitation  |  Conta de armazenamento '{0}' excedeu a quota alocada.  |
|  StorageAccountLocationMismatch  |  Não foi possível resolver a conta de armazenamento {0}. Certifique-se de que foi criada através de Olá fornecedor de recursos de armazenamento no Olá mesma localização que Olá recursos de computação.  |
|  StorageAccountNotFound  |  {0} de conta de armazenamento não foi encontrado. Certifique-se a conta de armazenamento não é eliminada e pertence toohello Olá VM mesma localização do Azure.  |
|  StorageAccountNotRecognized  |  Utilize uma conta de armazenamento gerida pelo fornecedor de recursos de armazenamento. Não é suportada a utilização de {0}.  |
|  StorageAccountOperationInternalError  |  Ocorreu um erro interno ao aceder a conta de armazenamento {0}.  |
|  StorageAccountSubscriptionMismatch  |  {0} de conta de armazenamento não pertence toosubscription {1}.  |
|  StorageAccountTooBusy  |  Conta de armazenamento '{0}' está atualmente demasiado ocupada. Considere utilizar outra conta.  |
|  StorageAccountTypeNotSupported  |  Disco {0} utiliza {1} que é uma conta do Blob storage. Tente novamente com a conta de armazenamento de caráter geral.  |
|  StorageAccountTypeNotSupported  |  {0} de conta de armazenamento é do tipo de {1}. Diagnóstico de arranque suporta {2} tipos de conta de armazenamento.  |
|  SubscriptionNotAuthorizedForImage  |  subscrição de Olá não está autorizada.  |
|  TargetDiskBlobAlreadyExists  |  Blob {0} já existe. Forneça um toocreate URI de blob diferente um disco de dados vazio novo '{1}'.  |
|  TargetDiskBlobAlreadyExists  |  Capturar não é possível continuar a operação, porque já existe {0} de blob de imagem de destino e blobs de VHD Olá sinalizador toooverwrite não está definido. Eliminar o blob Olá ou defina o sinalizador de Olá toooverwrite blobs de VHD e repita.  |
|  TargetDiskBlobAlreadyExists  |  Captura de operação não pode continuar porque {0} de blob de imagem de destino tem uma concessão ativa.   |
|  TargetDiskBlobAlreadyExists  |  Blob {0} já existe. Forneça um URI de blob diferente como destino para o disco '{1}'.  |
|  TooManyVMRedeploymentRequests  |  Foram recebidos demasiados pedidos de reimplementação da VM '{0}' ou Olá de Olá VMs no mesmo conjunto de disponibilidades que com esta VM. Tente novamente mais tarde.  |
|  VHDSizeInvalid  |  Olá especificado o valor do tamanho de disco de {0} para disco {1} com {2} do blob é inválido. Tamanho do disco tem de estar entre {3} e {4}.  |
|  VMAgentStatusCommunicationError  |  VM '{0}' não comunicou o estado de agente da VM ou extensões. Verifique a Olá VM tem um agente VM em execução e pode estabelecer o armazenamento de tooAzure de ligações de saída.  |
|  VMArtifactRepositoryInternalError  |  Ocorreu um erro ao comunicar com detalhes de artefacto da VM repositório tooretrieve Olá artefactos.  |
|  VMArtifactRepositoryInternalError  |  Ocorreu um erro interno ao obter dados do artefacto VM Olá do repositório de artefactos Olá.  |
|  VMExtensionHandlerNonTransientError  |  O processador '{0}' relatou uma falha para a extensão de VM '{1}' com o código de erro terminal '{2}' e a mensagem de erro: '{3}'  |
|  VMExtensionManagementInternalError  |  Ocorreu um erro interno ao processar a extensão VM '{0}'.  |
|  VMExtensionManagementInternalError  |  Ocorreram vários erros durante a preparação de extensões VM Olá. Consulte a vista de instâncias de extensão VM para obter mais detalhes.  |
|  VMExtensionProvisioningError  |  VM reportou uma falha durante o processamento de extensão '{0}'. Mensagem de erro: "{1}".  |
|  VMExtensionProvisioningError  |  Várias extensões de VM não foi possível toobe aprovisionado Olá VM. Consulte a vista da instância de extensão de VM de Olá para obter mais detalhes.  |
|  VMExtensionProvisioningTimeout  |  O aprovisionamento da extensão de VM '{0}' foi excedido. Instalação da extensão poderá estar a demorar demasiado tempo ou não foi possível obter o estado da extensão.  |
|  VMMarketplaceInvalidInput  |  Criar uma máquina virtual a partir de uma imagem de tipo não mercado não precisa de informações do plano, remova Olá plano informações no pedido de Olá. Nome do disco de SO é {0}.  |
|  VMMarketplaceInvalidInput  |  as informações de compra Olá não correspondem. Não é possível toodeploy Olá imagem do Marketplace. Nome do disco de SO é {0}.  |
|  VMMarketplaceInvalidInput  |  Criar uma máquina virtual a partir da imagem do Marketplace requer as informações do pedido de Olá plano. Nome do disco de SO é {0}.  |
|  VMNotFound  |  Hello VM '{0}' não é possível encontrar.  |
|  VMRedeploymentFailed  |  Reimplementação da VM '{0}' falhou devido a um erro interno tooan. Tente novamente mais tarde.  |
|  VMRedeploymentTimedOut  |  A reimplementação da VM '{0}' não foi concluída no Olá atribuído tempo. Poderá ser concluída com êxito no algum tempo. Caso contrário, pode repetir o pedido de Olá.  |
|  VMStartTimedOut  |  VM '{0}' não foram iniciados no Olá atribuído tempo. Olá VM poderá ainda ser iniciada com êxito. Verifique o estado de energia hello mais tarde.  |


## <a name="next-steps"></a>Passos seguintes
Se precisar de mais ajuda, pode contactar Olá especialistas do Azure no [Olá fóruns do MSDN Azure e Stack Overflow](https://azure.microsoft.com/support/forums/). Em alternativa, pode ficheiro um incidente de suporte do Azure. Aceda toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporta**.
