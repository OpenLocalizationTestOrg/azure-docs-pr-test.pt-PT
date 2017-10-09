---
title: aaaOptions para migrar no Azure RemoteApp | Microsoft Docs
description: "Saiba mais sobre as opções de Olá para migrar no Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Opções de migração no Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp vai ser descontinuado a 31 de agosto de 2017. Olá leitura [anúncio](https://go.microsoft.com/fwlink/?linkid=821148) para obter mais detalhes.


Se tiver parado a utilizar o Azure RemoteApp devido a Olá [anúncio de extinção](https://go.microsoft.com/fwlink/?linkid=821148) ou uma vez que terminar a avaliação, tem de toomigrate termina sessão do serviço de aplicações do Azure RemoteApp tooanother. Existem duas abordagens diferentes para a migração: um autogerida (frequentemente designado por infraestrutura como serviço [IaaS]) implementação ou uma plataforma completamente gerida (frequentemente denominada como um serviço) ou de Software como serviço [PaaS/SaaS] oferta. 

Self-service IaaS é uma implementação do-it-yourself que é gerida, operada e detida por si, diretamente implementados em máquinas virtuais (VMs) ou de sistemas físicos. Em Olá outro terminar uma PaaS/SaaS completamente gerido oferta é mais como o Azure RemoteApp – um parceiro fornece uma camada de serviço por cima de uma solução de gestão remota que processa operacional e de manutenção, enquanto, como cliente Olá, fazer alguma gestão de aplicações e de imagem.

[Ver Olá Azure RemoteApp webinars nas opções de migração](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou continue a ler para obter mais informações, (incluindo exemplos de Olá diferente opções de alojamento).

## <a name="self-managed-iaas-solutions"></a>Autogerida soluções de (IaaS)
### <a name="rds-on-iaas"></a>**RDS no IaaS**
Pode implementar uma nativa baseado em sessões dos serviços de ambiente de trabalho remoto (no Windows Server) implementação utilizando o RemoteApp ou ambientes de trabalho no local ou num ambiente alojado (por exemplo, em VMs do Azure). RDS em implementações IaaS são melhores para os clientes já familiarizados com e que tenham conhecimentos técnicos existente com as implementações de RDS. 

> [!NOTE]
> É necessário com o Software Assurance (SA) de licenciamento em Volume para toouse de licenças de acesso de cliente RDS esta opção de implementação.

Implementação de RDS em VMs do Azure é mais fácil do que nunca quando utiliza a implementação e modelos de aplicação de patches (ler um [descrição geral](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e, em seguida, [aceder-lhes obter](https://aka.ms/rdautomation)). Pode obter Olá mesmas capacidades de dimensionamento elásticas com recursos de modelo de implementação clássico do Azure (não a recursos de modelo de recursos do Azure) no Azure RemoteApp utilizando Olá [automática dimensionamento script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), apesar de existirem mais configurações e personalizações. Quando implementa o RDS em VMs do Azure, o suporte é fornecido através de [Azure suporta](https://azure.microsoft.com/support/plans/), Olá mesmo profissionais de suporte que suportados com o Azure RemoteApp. Pode obter custo estimativas com base na sua utilização existente contactando [suporte do Azure](https://azure.microsoft.com/support/plans/), ou pode efetuar cálculos por si através de um em breve toobe lançadas Calculadora de custo.  Além disso, com as VMs de série N (atualmente em pré-visualização privada) pode adicionar vGPU - saber mais sobre como adicionar vGPU e sobre como demasiado[escudo melhoramentos de RDS no Windows Server 2016](https://myignite.microsoft.com/videos/2794) na nossa sessão de Ignite.   

Temos de guias de implementação passo a passo para [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist com a sua implementação. Veja Olá [blogue de ambiente de trabalho remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) para Olá mais recentes notícias de última hora.

### <a name="citrix-on-iaas"></a>**Citrix no IaaS**
Um Citrix nativo implementação baseados em sessão XenApp ou XenDesktop pode ser implementado no local ou num ambiente alojado (tal como em VMs do Azure). 

Veja o guia de implementação passo a passo Olá, [Citrix XA 7.6 no Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), para obter mais informações. Leia mais sobre [Citrix no Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), incluindo uma calculadora de preços. Também pode encontrar um [Citrix contacte](http://citrix.com/English/contact/index.asp) toodiscuss as opções de com.

## <a name="fully-managed-paassaas-offerings"></a>Ofertas de (PaaS/SaaS) completamente geridas

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (lançadas Abril de 2017)
Agora disponível no Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials é Olá novo serviço de Virtualização de aplicações, energia Olá de combinar e flexibilidade de Olá plataforma de nuvem Citrix com Olá simples, prescritiva, e de consumir a visão do Microsoft Azure RemoteApp. 

Clientes existentes do Azure RemoteApp podem [registar-se numa avaliação gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Nota: Só encargos de serviço de utilizador Citrix é gratuito, aplicam-se de custos de armazenamento e computação do Azure

Saiba mais:
- [Migrar a partir do Azure RemoteApp tooCitrix XenApp Essentials](remoteapp-migrate-citrix.md)
- [Citrix e da Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Apresentação do Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix nuvem XenApp e XenDesktop serviço 

[Citrix nuvem XenApp e XenDesktop serviço](https://www.citrix.com/products/citrix-cloud/services.html) é Olá melhor solução para a entrega de Olá de aplicações e ambientes de trabalho, mais avançada de gestão e capacidades de monitorização. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (nome de plataforma: MyCloudIT)
[MyCloudIT](https://mycloudit.com) é uma plataforma de automatização para toosimplify de empresas IT, otimizar e dimensionar migração Olá e Olá, entrega de ambientes de trabalho remotos, aplicações remotas e infraestrutura de nuvem do Microsoft Azure. 

plataforma de MyCloudIT Olá reduz o tempo de implementação ao 95%, Azure custo por 30% e move-a infraestrutura de TI toda do seu cliente numa nuvem Olá num fim de alguns traços chaves. Parceiros agora podem gerir clientes a partir de um dashboard global, os utilizadores finais de serviço à volta de Olá mundo como nunca antes e aumentar as receitas sem adicionar overhead adicional ou um vasto conjunto formação do Azure.  

> Localização principal: Dallas, TX, EUA
> 
> Região da operação: em todo o mundo
> 
> Estado de parceiros: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Fornecedor de serviços de nuvem da Microsoft: Sim
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos
> 
> Soluções de migração do Azure RemoteApp: Sim, [Saiba mais](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, VP de desenvolvimento de negócio
> 
> Telefone: 972-218-0741
>   
> E-mail:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Moldura

As organizações de TI na empresa e government, fornecedores de serviço geridas e os principais fornecedores de software escolha moldura toocreate e gerir as respetivas áreas de trabalho seguras e definidas por software na nuvem de Olá. De toolarge pequenas organizações, moldura torna toolet incredibly fácil os utilizadores aceder às aplicações do Windows em qualquer browser a partir de qualquer dispositivo. Olá plataforma de moldura inclui tudo um administrador necessidades toodeploy aplicações da nuvem Olá, incluindo Olá infraestrutura do Azure e licenças RDS (colocar a sua própria conta do Azure e licenças é opcional). 

Saiba mais sobre [Frame no Azure](https://www.fra.me/ara). 

> Localização principal: San Mateo, AC, EUA
>
> Região da operação: em todo o mundo
>
> Parceiro da Microsoft: Sim
> 
> Telefone: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu oferece uma solução de área de trabalho online simples com aplicações legadas, SaaS e os documentos a partir de um browser html5. Como tal, disponibilizar quaisquer aplicações de forma segura em qualquer tipo de dispositivo. Para os serviços SaaS, está disponível uma vasta gama op Single-Sign-On opções. Também sistemas de ficheiros de diversos (nuvem) podem ser integrados profundamente na sua área de trabalho. Mobilidade de toofull seguinte, avançada online área de trabalho do Awingu de irá conceder-segurança ideal com controlos granulares (por exemplo, transferir/carregar), completo utilização auditoria, a multi-factor Authentication (por exemplo, o Azure MFA), a gravação da sessão e muito mais. Out-of-a-box, Awingu ativa e aplicação de partilha sessão para colaboração otimizada e segura de documentos.
Solução do Awingu é API multi-inquilino, AD multi e aberto. É utilizado pelo pequenas e grandes empresas, os fornecedores de serviços de nuvem e [ISVs](http://www.isv2saas.com). Estes clientes especialmente Agradecemos olá fáceis de utilizar, TCO facilidade para instalação e baixa.

Awingu tudo-em-é [disponíveis no Azure Marketplace de Olá](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) com 2 utilizadores em simultâneo incorporados. Licenças adicionais estão disponíveis através de um [vasta gama de distribuidores e revendedores](http://www.awingu.com/reseller).

Saiba mais sobre [Awingu no como tooAzure alternativo RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Localização principal: Belgium
> 
> Regiões a funcionar: EMEA, América do Norte e Brasil
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos 
> 
> **Global**:
> 
> Arnaud Marlière, CMO
> 
> E-mail:[arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Telefone: +1 646 583 3025
> 
> **Belgium HQ**:
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> E-mail:[info@awingu.com](mailto:info@awingu.com) 
> 
> Telefone: +32 9 296 40 11
> 
> **EUA**:
> 
> piso 7, 1177 Ave de Olá Americas,
> 
> Nova Iorque, NY 10036
> 
> E-mail:[info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Microsoft Hospedava o fornecedor de serviço
Parceiros de alojamento oferecem, normalmente, um completamente gerido de ambiente de trabalho do Windows alojados e Olá de serviço de aplicações, que pode incluir a gestão de recursos do Azure, sistemas operativos, aplicações e suporte técnico com o parceiro de Olá do contratos de licenciamento em com a Microsoft e outros fornecedores de software, juntamente com a ser um contrato de licença de fornecedor de serviços tooallow reselling de licença de acesso de subscritor (SAL). Olá informações seguintes fornecem detalhes e informações de contacto para algumas das Olá de que os fornecedores que especialização em clientes com a respetiva migração do Azure RemoteApp a prestar assistência. Veja [lista atual de Olá de fornecedores de serviços alojados](http://aka.ms/rdsonazurecertified) que concluiu Olá RDS no IaaS learning caminho e avaliação.  

### <a name="citrix-service-provider-program"></a>Programa de fornecedor de serviço do Citrix
Olá programa de fornecedor de serviço do Citrix torna mais fácil de simplicidade Olá de toodeliver de fornecedores do serviço de nuvem virtual informática tooSMBs, oferece os serviços de Olá pretendem um modelo de fácil, pay as you go. Fornecedores de serviços do Citrix aumentar as respetivas empresas da Microsoft SPLA e expandir os seus investimentos de plataforma RDS com qualquer dispositivo, acesso em qualquer local, hello mais amplas suporte da aplicação, uma experiência otimizada, maior segurança e maior escalabilidade. Por sua vez, os fornecedores de serviços de Citrix, attract subscritores mais aumentar satisfação do cliente e reduzir os custos operacionais. [Saiba mais](http://www.citrix.com/products/service-providers.html) ou [localizar um parceiro](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) specializes no fornecimento de soluções de ambiente de trabalho alojadas, entrega de ambiente de trabalho completo e aplicações de ISV experiências criadas no Microsoft tecnologia tooa global cliente base a partir do Azure e os respetivos centros de dados.

> Localização principal: Londres, RU; Singapura; Houston, TX
> 
> Região da operação: em todo o mundo
> 
> Estado de parceiros: Gold
> 
> Fornecedor de serviços de nuvem da Microsoft: Sim
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos
> 
> Soluções de migração do Azure RemoteApp: Sim, [Saiba mais](http://www.acuutech.com/ara-migration/)
> 
> **Reino Unido**:
>   
> 5/6 Iorque próxima, Langston viagem,
>   
> Loughton, Essex IG10 3TQ
>   
> Telefone: + 44 (0) 20 8502 2155
> 
> **Singapura**:
>   
> Rua 100 Cecil, #09-02 
>   
> Olá globo, Singapura 069532
> 
> Telefone: +65 6709 4933
>   
> **América do Norte**:
>   
> 3601 S. Sandman St.
>   
> 200 Suite, Houston, TX 77098
>   
> Telefone: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) specializes no ISVs transição toohello na nuvem e de ISV' procura toooptimize os respetivos atual setups de nuvem. ASPEX oferece um vasto leque de serviços geridos, devops e serviços de consultoria.  

> Localização principal: Antwerp, Belgium
> 
> Região da operação: na Europa Ocidental
> 
> Estado de parceiros: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Fornecedor de serviços de nuvem da Microsoft: Sim
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos
> 
> Soluções de migração do Azure RemoteApp: Sim, [Saiba mais](https://www.aspex.be/en/azure-remote-apps)
> 
> Telefone: +3232202198
> 
> Correio:[info@aspex.be](mailto:info@aspex.be)
> 
> Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) ajuda empresas, governments locais, não governamental corpos e instituições cuidados de saúde com os respetivos journey para uma forma mais inteligente do trabalho em Olá Microsoft Cloud. A ser produtivos e segura em qualquer local, com qualquer dispositivo e em custos com TI baixo. Caase.com é uma especialista em verdadeira para Microsoft Office365, o Azure, o Enterprise Mobility, segurança e Windows. Com o nosso consultancy, serviços de migração, os programas de adoção, formação, gestão e suporte Caase.com cria uma plataforma otimizada e segura para colaboração para clientes que os funcionários, parceiros e fornecedores.
Caase.com é mastermind Olá de Olá área de trabalho remoto do Azure (área de trabalho móvel) e Olá Digital à área de trabalho (sociais Intranet). Ambas as soluções – conseguidas com a adoção – são foundation Olá que assegura que os utilizadores de Olá destas soluções têm Olá mais pleasant, com êxito e eficaz a experiência no respetivo toohello rota Microsoft Cloud.
Neerlandês tradução ánd um filme suporte através de aqui: http://caase.com/over-ons/

> Região da operação: com base neerlandês, alcance global
> 
> Estado de parceiros: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Fornecedor de serviços de nuvem da Microsoft: Sim
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos
> 
> Soluções de migração do Azure RemoteApp: Sim, [mais](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Países Baixos:
> 
> Rigtersbleek-Zandvoort 10 (Alemanha Spinnerij)
> 
> 7521 BE, Enschede
> 
> Telefone: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio para o Azure](http://getnerdio.com/nfa/) é uma plataforma de automatização de IT que fornece seja extremamente simples de aprovisionamento, gestão e a otimização de ambientes de TI completas no Olá nuvem da Microsoft. Configurar ambientes de trabalho virtuais, aplicações remotas e os servidores a funcionar nas duas horas. Administrar o ambiente de Olá no três cliques ou menos com o Portal de administração de Nerdio. Utilize inteligente dimensionamento automático e guardar 40 too60% em recursos IaaS do Azure.

> Localização principal: região de operação de Chicago, IL: Estado de parceiro em todo o mundo: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) fornecedor de serviços do Microsoft Cloud: Sim
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos
> 
> Soluções de migração do Azure RemoteApp: Sim
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> EUA
> 
> Ext. 4NERDIO (844) 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) oferece completa Microsoft Dynamics portefólio (NAV AX, GP, SL, CRM) pública e privada de nuvem (Azure).

> Localização principal: Países Baixos
> 
> Operação região: em todo o mundo
> 
> Estado de parceiros: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Fornecedor de serviços de nuvem da Microsoft: Sim
> 
> Oferta de soluções de programas RemoteApp e o ambiente de trabalho baseados em sessões: Sim, ambos
> 
> **EMEA**:
> 
> Prins Mauritslaan 29 35
> 
> 71 LP Badhoevedorp
> 
> Olá Países Baixos
> 
> Telefone: +31 20 547 8060 
> 
>  **Americas**:
> 
> 171 Saxony viagem, Suite 105
> 
> Encinitas, AC 92024
> 
> San Diego
> 
> Estados Unidos
> 
> Telefone: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil Rua
>    
> \#11-08, Olá Octagon
> 
> Singapura 069534
> 
> Singapura
>   
> Phone - Singapura: +65 6222 6591
> 
> Phone - Austrália: +61 2 8310 5568 
>    
> Phone - Nova Zelândia: +64 4 488 0321
> 
## <a name="need-more-help"></a>Precisa de mais ajuda?
Ainda precisa de ajudar a escolher ou tem mais perguntas? Utilize um dos Olá métodos tooget ajuda a seguir. 

1. Enviar-nos por e-mail [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).
2. Contacte [suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Iniciar, abrindo um [caso de suporte do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Chamada-nos. [Localizar um número de venda local](https://azure.microsoft.com/overview/sales-number/).

