---
title: "Referência do Azure Active Directory B2C: - Confiar estruturas | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C e Olá Framework de experiência de identidade"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Definir as estruturas de confiança com o Framework de experiência de identidade do Azure AD B2C

O Azure Active Directory B2C políticas personalizadas (Azure AD B2C) que utilizam Olá Framework de experiência de identidade fornecem a sua organização com um serviço centralizado. Este serviço reduz o complexidade Olá de Federação de identidade numa grande Comunidade de interesse. complexidade Olá é a relação de confiança único tooa reduzido e uma troca de metadados único.

Azure AD B2C as políticas personalizadas que utilizam Olá identidade experiência Framework tooenable tooanswer Olá seguintes questões:

- Quais são Olá legal, segurança, privacidade e as políticas de proteção de dados tem de ser aderiu a?
- Quem são os contactos de Olá e quais são os processos de Olá para se tornar um participante autorizado?
- Quem são Olá accredited fornecedores de informações de identidade (também conhecido como "fornecedores de afirmações") e que estes oferecem?
- Quem são Olá accredited das entidades confiadoras (e, opcionalmente, o que é necessário)?
- Quais são Olá técnica "na transmissão de Olá" requisitos de interoperabilidade para participantes?
- Quais são regras de operacional "tempo de execução" Olá que devem ser impostas para trocar informações de identidade digital?

construir o tooanswer todas estas perguntas, as políticas personalizadas do Azure AD B2C que utilizam Olá de utilização de estrutura de experiência de identidade Olá confiar Framework (TF). Vejamos este construção e que fornece.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Compreender foundation de gestão de fidedignidade Framework e a Federação Olá

Olá confiar Framework é uma especificação de escrita de Olá identidade, segurança, privacidade e dados de políticas de proteção devem ter toowhich participantes numa Comunidade de interesse.

Identidade federada fornece uma base para alcançar a garantia de identidade do utilizador final na escala da Internet. Por delegar as partes de toothird de gestão de identidade, uma identidade digital única para um utilizador final pode ser reutilizada com várias entidades confiadoras.  

Garantia de identidade requer que Fornecedores de identidade (IdPs) e os fornecedores de atributo (AtPs) aderem toospecific segurança, privacidade e políticas operacionais e práticas.  Se não podem efetuar inspections diretas, confiadoras (RPs) tem de desenvolver as relações de confiança com Olá IdPs e AtPs escolherem toowork com.  

À medida que cresce o número de Olá de fornecedores de informações de identidade digital e os consumidores, é difícil toocontinue management pairwise estas relações de fidedignidade, ou mesmo Olá pairwise troca de metadados de técnica Olá necessária para conetividade de rede .  Hubs de federação tem atingido apenas limitado êxito a resolução desses problemas.

### <a name="what-a-trust-framework-specification-defines"></a>Define que uma especificação de confiança Framework
TFs são linchpins Olá do modelo de abrir identidade Exchange (OIX) de confiança Framework Olá, onde cada Comunidade de interesse é regida por uma especificação de TF específica. Define uma especificação de TF:

- **Olá métricas de segurança e privacidade para a Comunidade Olá de interesse com a definição de Olá de:**
    - níveis de Olá de garantia (LOA) que são oferecidos/exigido pela participantes; Por exemplo, um conjunto ordenado de confiança de que as classificações para autenticidade Olá das informações de identidade digital.
    - níveis de Olá de proteção (LOP) que são oferecidos/exigido pela participantes; Por exemplo, um conjunto ordenado de confiança de que as classificações para proteção de Olá de informações de identidade digital que são processadas pelo participantes na Comunidade Olá de interesse.

- **Descrição do Olá digital informações de identidade que tem oferecidas/necessário por participantes de Olá**.

- **Olá técnica políticas para produção e o consumo de informações de identidade digital e, consequentemente, para medir LOA e LOP. Escrito normalmente políticas incluem Olá seguintes categorias de políticas:**
    - Identidade de verificação do políticas, por exemplo: *são vivamente como informações de identidade de uma pessoa vetted?*
    - As políticas de segurança, por exemplo: *como vivamente são integridade informações e confidencialidade protegida?*
    - Políticas de privacidade, por exemplo: *que controlo a um utilizador tem sobre informações de identificação pessoais (PII)*?
    - Políticas de Survivability, por exemplo: *se um fornecedor ceases operações, como funciona continuidade e a proteção da função PII?*

- **Olá técnica perfis para produção e consumo de informações de identidade digital. Estes perfis incluem:**
    - Interfaces de âmbito para o qual as informações de identidade digital estão disponíveis num LOA especificado.
    - Requisitos técnicos para interoperabilidade de na transmissão.

- **Olá as descrições dos Olá várias funções que participantes na Comunidade Olá podem efetuar e Olá qualificações que são necessária toofulfill estas funções.**

Assim uma especificação de TF é regida pelas como informações de identidade são trocadas entre os participantes Olá da Comunidade Olá de interesse: das entidades confiadoras, identidade e fornecedores de atributo e verificadores de atributo.

Uma especificação de TF é um ou vários documentos que funcionam como uma referência para governação Olá da Comunidade Olá de interesse regulates asserção Olá e consumo de informações de identidade digitais dentro da Comunidade de Olá. É um conjunto de políticas documentado e procedimentos concebido tooestablish confiança em identidades digitais Olá que são utilizados para transações online entre membros de uma Comunidade de interesse.  

Por outras palavras, uma especificação de TF define Olá as regras para criar um ecossistema de identidade federada viável para uma Comunidade.

Atualmente não há ampla contrato no benefício Olá essas uma abordagem. Não há doubt que confiança especificações de estrutura facilitam o desenvolvimento de Olá de ecossistemas de identidade digital com verificável características de segurança, segurança e privacidade, que significa que podem ser reutilizadas em várias comunidades de interesse.

Por esse motivo, as políticas personalizadas do Azure AD B2C que utilizam Olá identidade experiência Framework utiliza especificação Olá como base Olá da respetiva representação de dados para uma interoperabilidade de toofacilitate TF.  

Azure AD B2C as políticas personalizadas que tiram partido Olá identidade experiência Framework representam uma especificação de TF como uma combinação de dados humanos e machine-readable. Alguns secções deste modelo (normalmente, as secções são mais dedicadas a governação) são representadas como faz referência a documentação de política de segurança e privacidade toopublished juntamente com Olá relacionadas com procedimentos (se aplicável). Noutras secções descrevem em detalhe Olá metadados e o tempo de execução as regras de configuração que facilitam a automatização operacional.

## <a name="understand-trust-framework-policies"></a>Compreender as políticas de fidedignidade Framework

Em termos de implementação, Olá especificação TF é composta por um conjunto de políticas que lhe permitem o controlo total sobre experiências e comportamentos de identidade.  Azure AD B2C as políticas personalizadas que tiram partido Olá Framework de experiência de identidade ativar tooauthor e criar a suas próprias TF através deste tipo declarativas políticas que pode definir e configurar:

- referência de documento Olá ou referências que definem o ecossistema de identidade federada Olá da Comunidade de Olá que está relacionada com toohello TF. São documentação de TF toohello de ligações. Olá (predefinida) operacional "tempo de execução" regras ou percursos de utilizador de Olá que automatizarem e/ou controlam exchange Olá e a utilização de Olá afirmações. Estes percursos de utilizador associados a um LOA (e um LOP). Uma política, por conseguinte, pode ter percursos de utilizador com diversos LOAs (e LOPs).

- fornecedores de afirmações de fornecedores de identidade e o atributo de Olá ou Olá, na Comunidade Olá de interesse e Olá perfis técnicos de suporte, juntamente com accreditation de LOA/LOP de (fora de banda) Olá relacionada com toothem.

- integração de Olá verificadores de atributo ou fornecedores de afirmações.

- Olá das entidades confiadoras na Comunidade Olá (por inferência).

- metadados de Olá para estabelecer comunicações de rede entre os participantes. Estes metadados, juntamente com perfis de técnica Olá, são utilizados durante uma transação tooplumb "na transmissão de Olá" interoperabilidade entre da entidade confiadora Olá e outros participantes da Comunidade.

- Olá conversão de protocolo se qualquer (por exemplo, SAML, OAuth2, WS-Federation e o OpenID Connect).

- requisitos de autenticação de Olá.

- Olá multifator orchestration se aplicável.

- Um esquema partilhado para todas as afirmações de Olá que estão disponíveis e tooparticipants mapeamentos de uma Comunidade de interesse.

- Olá todas as afirmações de transformações, juntamente com minimization de dados de Olá neste contexto, o exchange de Olá toosustain e a utilização de afirmações de Olá.

- enlace Olá e encriptação.

- Olá afirmações de armazenamento.

### <a name="understand-claims"></a>Compreender as afirmações

> [!NOTE]
> Iremos coletivamente Consulte tooall Olá possíveis os tipos de informações de identidade que podem ser trocadas como "afirmações": afirmações sobre a credencial de autenticação de um utilizador final vetting de identidade, dispositivo de comunicação, a localização física, identificar pessoalmente atributos e assim sucessivamente.  
>
> Utilizamos Olá termo "afirmações" – em vez de "atributos" – porque transações online, destes artefactos de dados não estão factos que podem ser verificados diretamente pelo Olá entidade confiadora. Em vez disso está asserções ou afirmações, sobre factos para o qual Olá da entidade confiadora tem de desenvolver transação solicitada suficientes confiança toogrant Olá do utilizador final.  
>
> Também utilizamos o termo Olá "afirmações" porque o Azure AD B2C são políticas personalizadas que utilizam Olá identidade experiência Framework concebido exchange de Olá toosimplify de todos os tipos de informações de identidade digital de uma forma consistente, independentemente de se Olá subjacente protocolo está definido para obtenção de atributo ou autenticação de utilizador.  Da mesma forma, utilizamos o termo Olá "fornecedores de afirmações" toocollectively Consulte tooidentity fornecedores, a fornecedores de atributo e verificadores de atributo, quando não queremos toodistinguish entre as respetivas funções específicas.   

Assim, governem como informações de identidade são trocadas entre uma entidade confiadora, identidade e fornecedores de atributo e verificadores de atributo. Controlarem que identity e fornecedores de atributo são necessárias para a autenticação da entidade confiadora. Estes devem ser considerados como linguagem específicas do domínio (DSL), ou seja, um idioma do computador que tenha especializada para um domínio de aplicação em particular com herança, *se* instruções, de que o polimorfismo.

Estas políticas constituem Olá machine-readable parte Olá TF construir nas políticas personalizadas do Azure AD B2C tirar partido Olá Framework de experiência de identidade. Estes incluem todos os detalhes de operacional da Olá, incluindo metadados e perfis técnicas, definições de esquema de afirmações, as funções de transformação de afirmações e percursos de utilizador que estão preenchidos fornecedores de afirmações no orchestration operacional toofacilitate e automatização.  

Estes são considerados toobe *documentos de maior duração* porque não há a possibilidade de boa irão alterar os respetivos conteúdos ao longo do tempo que dizem respeito à participantes de Active Directory Olá declarados nas políticas de Olá. Também é potencial Olá que possam alterar os termos de Olá e condições para a ser um participante.  

Configuração de Federação e de manutenção são muito simplificados das entidades confiadoras de Reconfigurações de confiança e a conectividade contínuas de proteção como fornecedores de afirmações diferentes/verificadores aderir ou sair (Olá da Comunidade representada pelo) Olá conjunto de políticas.

Interoperabilidade é outro significativo desafio. Fornecedores de afirmações adicionais/verificadores tem de ser integrados, porque das entidades confiadoras são pouco provável toosupport Olá todos os protocolos necessários. As políticas personalizadas do Azure AD B2C resolverem este problema, suporte de protocolos de norma da indústria e aplicando os percursos de utilizador específico tootranspose pedidos quando das entidades confiadoras e fornecedores de atributo não suportam Olá mesmo protocolo.  

Percursos de utilizador incluem perfis de protocolo e metadados que são utilizado tooplumb "na transmissão de Olá" interoperabilidade entre da entidade confiadora Olá e outros participantes. Também existem regras de tempo de execução operacional que são aplicados tooidentity exchange pedido/resposta as mensagens de informações para impor a compatibilidade com políticas publicadas como parte da especificação de TF Olá. ideia Olá de percursos de utilizador é toohello chave personalização da experiência do cliente Olá. É também sheds leve sobre o funcionamento do sistema de Olá ao nível do protocolo de Olá.

Dessa forma, portais e as aplicações de terceiros de entidade confiadora podem, consoante os respetivos contexto invocar políticas personalizadas do Azure AD B2C que tire partido Olá Framework de experiência de identidade transmitir o nome de Olá de uma política específica e obter precisamente comportamento Olá e informações Exchange que quiserem sem qualquer muss, fuss ou de risco.
