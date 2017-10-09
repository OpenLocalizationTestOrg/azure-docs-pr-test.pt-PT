---
title: funcionalidades do motor de regras de aaaAzure CDN | Microsoft Docs
description: "Documentação de referência para a CDN do Azure regras de funcionalidades e as condições de correspondência do motor."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Funcionalidades do motor de regras CDN do Azure
Este tópico lista as descrições detalhadas das funcionalidades disponíveis Olá para a rede de entrega de conteúdos (CDN) do Azure [motor de regras](cdn-rules-engine.md).

Olá terceiro parte uma regra é a funcionalidade de Olá. Uma funcionalidade define o tipo de Olá de ação que será aplicada toohello tipo de pedido identificado por um conjunto de condições de correspondência.

## <a name="access"></a>Access

Estas funcionalidades são toocontrol concebida toocontent de acesso.


Nome | Objetivo
-----|--------
Negar o acesso | Determina se a todos os pedidos são rejeitados com resposta 403 Proibido.
Autenticação de token | Determina se a autenticação baseada em tokens será aplicado tooa pedido.
Código de recusa de token de autenticação | Determina o tipo de Olá de resposta que vai ser devolvido tooa utilizador quando um pedido é negado devido a autenticação baseada em tooToken.
Autenticação de token ignorar URL maiúsculas / minúsculas | Determina se será sensível comparações de URL, efetuadas pela autenticação baseada em tokens.
Parâmetro de autenticação de token | Determina se o parâmetro de cadeia de consulta Olá autenticação baseada em tokens deve ser mudado.

### <a name="deny-access"></a>Negar o acesso
**Objetivo**: determina se a todos os pedidos são rejeitados com resposta 403 Proibido.

Valor | resultado
------|-------
Ativado| Faz com que todos os pedidos que satisfaçam Olá correspondente critérios toobe rejeitada com resposta 403 Proibido.
Desativado| Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá é tooallow Olá origem toodetermine Olá tipo de servidor de resposta que vai ser devolvido.

**Comportamento de predefinido**: desativado

> [!TIP]
   > Uma utilização possíveis para esta funcionalidade é tooassociate-o com um cabeçalho de pedido corresponde ao referrers tooHTTP de acesso de tooblock de condição que estão a utilizar conteúdo do inline ligações tooyour.

### <a name="token-auth"></a>Autenticação de token
**Objetivo:** determina se a autenticação baseada em tokens será aplicado tooa pedido.

Se a autenticação baseada em tokens está ativada, apenas pedidos que fornecem um token de encriptados e cumprem os requisitos de toohello especificados por esse token serão cumpridos.

chave de encriptação de Olá que serão utilizados valores de token tooencrypt e desencriptação é determinado pela chave primária e as opções de chave de cópia de segurança na página de autenticação de Token. Tenha em atenção que as chaves de encriptação são específicas da plataforma.

Valor | resultado
------|---------
Ativado | Protege Olá pedida conteúdo com a autenticação baseada em tokens. Apenas os pedidos de clientes que fornecem um token válido e cumpram os requisitos serão cumpridos. Transações de FTP são excluídas da autenticação baseada em tokens.
Desativado| Restaura o comportamento predefinido de Olá. Olá comportamento predefinido é tooallow toodetermine de configuração da autenticação baseada em tokens se um pedido irá ser protegido.

**Comportamento predefinido:** desativado.

###<a name="token-auth-denial-code"></a>Código de recusa de token de autenticação
**Objetivo:** determina o tipo de Olá da resposta que vai ser devolvido tooa utilizador quando um pedido é negado devido a autenticação baseada em tooToken.

códigos de resposta disponíveis Olá estão listados abaixo.

Código de Resposta|Nome de resposta|Descrição
----------------|-----------|--------
301|Movida permanentemente|Este código de estado redireciona os utilizadores não autorizados toohello URL especificado no cabeçalho de localização.
302|Foi encontrado|Este código de estado redireciona os utilizadores não autorizados toohello URL especificado no cabeçalho de localização. Este código de estado é o método de padrão da indústria Olá da execução de um redirecionamento.
307|Redirecionamento temporário|Este código de estado redireciona os utilizadores não autorizados toohello URL especificado no cabeçalho de localização.
401|Não autorizado|Combinar este código de estado com o cabeçalho de resposta WWW-Authenticate permite-lhe tooprompt um utilizador para autenticação.
403|Proibido|Este é Olá padrão 403 Proibido mensagem de estado que um utilizador não autorizado, será apresentado quando tenta tooaccess conteúdo protegido.
404|Ficheiro não encontrado|Este código de estado indica que o cliente HTTP Olá foi capaz de toocommunicate com o servidor de Olá, mas Olá pedida não foi encontrado o conteúdo.

#### <a name="url-redirection"></a>URL de redirecionamento

Esta funcionalidade suporta tooa definido pelo utilizador URL de redirecionamento URL quando é configurado tooreturn um código de estado 3xx. Este URL definido pelo utilizador pode ser especificado efetuando Olá os seguintes passos:

1. Selecione um código de resposta de 3xx para a funcionalidade de código de recusa do Token Auth Olá.
2. Selecione a opção de nome de cabeçalho opcionais "Localização".
3. Defina o URL do valor do cabeçalho opcionais opção toohello assim o desejar.

Se um URL não está definido para um código de estado 3xx, em seguida, hello página resposta padrão para um código de estado 3xx será devolvida toohello utilizador.

Redirecionamento de URL só é aplicável para 3xx códigos de resposta.

A opção de valor de cabeçalho opcional suporta carateres alfanuméricos, aspas e espaços.

#### <a name="authentication"></a>Autenticação

Esta funcionalidade suporta o cabeçalho do Olá capacidade tooinclude o WWW-Authenticate quando responder tooan pedido não autorizado para conteúdo protegido pela autenticação baseada em tokens. Se o cabeçalho WWW-Authenticate foi definido demasiado "básico" na configuração, o utilizador não autorizado Olá será solicitado para as credenciais da conta.

Olá acima configuração pode ser conseguido efetuando Olá os seguintes passos:

1. Selecione "401" como código de resposta de Olá para a funcionalidade de código de recusa do Token Auth Olá.
2. Selecione "WWW-Authenticate" a opção de nome de cabeçalho opcionais.
3. Defina a opção de valor de cabeçalho opcionais demasiado "básico."

O cabeçalho WWW-Authenticate só é aplicável para 401 códigos de resposta.

### <a name="token-auth-ignore-url-case"></a>Autenticação de token ignorar URL maiúsculas / minúsculas
**Objetivo:** determina se comparações de URL, efetuadas pela autenticação baseada em tokens vai estar em maiúsculas e minúsculas.

os parâmetros de Olá afetados por esta funcionalidade são:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

Os valores válidos são:

Valor|resultado
---|----
Ativado|Faz com que a nossa servidor edge tooignore caso ao comparar os URLs para os parâmetros de autenticação baseada em tokens.
Desativado|Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá destina-se a comparações de URL para a autenticação de Token toobe maiúsculas e minúsculas.

**Comportamento predefinido:** desativado.
 
### <a name="token-auth-parameter"></a>Parâmetro de autenticação de token
**Objetivo:** determina se o parâmetro de cadeia de consulta Olá autenticação baseada em tokens deve ser mudado.

Informações da chave:

- A opção de valor define Olá consulta cadeia nome do parâmetro através do qual pode ser especificado um token.
- A opção de valor não pode ser definida demasiado "ec_token."
- Certifique-se de que o nome do Olá definido no apenas a opção de valor 
- contém carateres de URL válidos.

Valor|resultado
----|----
Ativado|A opção de valor define Olá consulta cadeia parâmetro nome através do qual tokens devem ser definidos.
Desativado|Um token pode ser especificado como um parâmetro de cadeia de consulta não definido no URL do pedido de Olá.

**Comportamento predefinido:** desativado. Um token pode ser especificado como um parâmetro de cadeia de consulta não definido no URL do pedido de Olá.

## <a name="caching"></a>Colocação em cache

Estas funcionalidades são toocustomize concebida quando e como o conteúdo é colocado em cache.

Nome | Objetivo
-----|--------
Parâmetros de largura de banda | Determina se os parâmetros (ou seja, ec_rate e ec_prebuf) de limitação de largura de banda estará ativa.
Limitação de largura de banda | Acelera a largura de banda de Olá para resposta Olá fornecida pelos nossos servidores edge.
Ignorar a Cache | Determina se o pedido de Olá pode tirar partido da tecnologia colocação em cache.
Tratamento de cabeçalho de Cache-Control | Controlos Olá geração dos cabeçalhos Cache-Control pelo servidor de limite de Olá quando a funcionalidade de idade de máxima externo está ativa.
Cadeia de consulta de chave da cache | Determina se Olá-chave da cache será incluir ou excluir os parâmetros de cadeia de consulta associados a um pedido.
Chave da cache reescrever | Reescreve Olá associada a um pedido a chave de cache.
Concluir o preenchimento da Cache | Determina o que acontece quando um resultados de pedido numa falha de acerto na cache parciais num servidor edge.
Comprima os tipos de ficheiro | Define os formatos de ficheiro Olá que irão ser comprimidos no servidor de Olá.
Idade de máx. de interno predefinida | Determina o intervalo de idade máxima de predefinido Olá para revalidação de cache de servidor de tooorigin servidor edge.
Tratamento de cabeçalho de expirar | Controlos Olá geração dos cabeçalhos de expira por um servidor edge, quando a funcionalidade de idade de máxima externo Olá está ativa.
Externa de atribuição de idade máxima | Determina o intervalo de idade máxima de Olá para revalidação de cache do browser tooedge servidor.
Forçar interna de atribuição de idade máxima | Determina o intervalo de idade máxima de Olá para revalidação de cache de servidor de tooorigin servidor edge.
Suporte de 264 (transferência progressiva HTTP) | Determina os tipos de Olá de 264 formatos de ficheiro que podem ser utilizado toostream conteúdo.
Pedido de Cache não honor | Determina se não-pedidos um cliente HTTP serão reencaminhados toohello servidor de origem.
Ignorar a Cache não de origem | Determina se o nosso CDN ignorará determinadas diretivas servidas a partir de um servidor de origem.
Ignorar intervalos Unsatisfiable | Determina a resposta de Olá que vai ser devolvida tooclients quando um pedido gera um código de estado 416 pedido intervalo não satisfatório.
Interna obsoleta máx. | Controla a quanto decorridos desde a hora de expiração normal de Olá um recurso em cache poderão ser servido de um servidor edge quando o servidor edge de Olá é toorevalidate não é possível Olá asset em cache com o servidor de origem Olá.
Partilha de Cache parciais | Determina se um pedido pode gerar o conteúdo parcialmente em cache.
Prevalidate conteúdos em cache | Determina se o conteúdo em cache vai ser elegível para revalidação antecipada antes do valor de TTL expire.
Atualizar os ficheiros de Cache de Zero bytes | Determina o modo como os pedidos de um cliente HTTP para um elemento de cache de 0 bytes é processado pelos nossos servidores edge.
Códigos de estado colocáveis de conjunto | Define o conjunto de Olá de códigos de estado que podem resultar num conteúdos em cache.
Entrega de conteúdos obsoleta com o erro | Determina se expirado os conteúdos em cache serão entregues quando ocorre um erro durante a revalidação de cache ou quando Olá ao obter conteúdo de pedido do servidor de origem do cliente Olá.
Obsoleta ao Revalidate | Melhora o desempenho ao permitir que a nossa servidores edge tooserve cliente estagnado toohello autor do pedido enquanto revalidação ocorre.
Comentário | funcionalidade de comentários de Olá permite toobe uma nota adicionado dentro de uma regra.

###<a name="bandwidth-parameters"></a>Parâmetros de largura de banda
**Objetivo:** determina se os parâmetros (ou seja, ec_rate e ec_prebuf) de limitação de largura de banda estará ativa.

Parâmetros de limitação de largura de banda determinam se Olá velocidade de transferência de dados para o pedido do cliente estará taxa personalizado tooa limitado.

Valor|resultado
--|--
Ativado|Permite que os nossos servidores de edge toohonor largura de banda de limitação de pedidos.
Desativado|Faz com que a nossa servidores edge tooignore largura de banda de parâmetros de limitação. Olá pedida conteúdo será servido normalmente (ou seja, sem limitação de largura de banda).

**Comportamento predefinido:** ativada.

###<a name="bandwidth-throttling"></a>Limitação de largura de banda
**Objetivo:** limitações Olá largura de banda para resposta Olá fornecida pelos nossos servidores edge.

Ambos Olá opções a seguir tem de ser definido tooproperly configurar limitação de largura de banda.

Opção|Descrição
--|--
KBytes por segundo|Defina esta opção toohello largura de banda máxima (Kb por segundo) que pode ser utilizados toodeliver Olá resposta.
Segundos de Prebuf|Defina esta opção toohello número de segundos que os nossos servidores edge aguarda até que a limitação de largura de banda. objetivo Olá neste período de tempo de largura de banda sem restrições é tooprevent um leitor de multimédia da situação ocorrer stuttering ou problemas devido toobandwidth limitação da memória intermédia.

**Comportamento predefinido:** desativado.

###<a name="bypass-cache"></a>Ignorar a Cache
**Objetivo:** determina se o pedido de Olá pode tirar partido da tecnologia colocação em cache.

Valor|resultado
--|--
Ativado|Faz com que todos os pedidos toofall através do servidor de origem toohello, mesmo que o conteúdo de Olá foi colocado em cache anteriormente no servidores edge.
Desativado|Faz com que servidores edge ativos toocache de acordo com a política de cache de toohello definida no respetivos cabeçalhos de resposta.

**Comportamento predefinido:**

- **HTTP grande:** desativado

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Tratamento de cabeçalho do controlo de cache
**Objetivo:** controla geração Olá dos cabeçalhos Cache-Control pelo servidor de limite de Olá quando externos de idade máxima de funcionalidade está ativa.

Olá tooachieve de forma mais fácil este tipo de configuração é tooplace Olá externos de atribuição de idade máxima e funcionalidades de tratamento do cabeçalho de Cache-Control de Olá no Olá mesma instrução.

Valor|resultado
--|--
Substituir|Garante que Olá seguintes ações irão ocorrer:<br/> -Substitui o cabeçalho de Cache-Control gerado pelo servidor de origem Olá. <br/>-Adiciona o cabeçalho de Cache-Control produzido pelo Olá resposta de toohello de funcionalidade de idade de máxima externo.
Pass-Through|Garante que o cabeçalho de Cache-Control produzido pela funcionalidade de idade de máxima externo Olá nunca é adicionado toohello resposta. <br/> Se o servidor de origem Olá produz um cabeçalho de Cache-Control, este irá percorrer pelo utilizador final do toohello. <br/> Se o servidor de origem Olá não produz um cabeçalho de Cache-Control, em seguida, esta opção a toonot de cabeçalho de resposta de Olá causa pode conter um cabeçalho de Cache-Control.
Adicionar se estiverem em falta|Se um cabeçalho de Cache-Control não foi recebido do servidor de origem Olá, esta opção adiciona o cabeçalho de Cache-Control produzido pela funcionalidade de idade de máxima externo Olá. Esta opção é útil para assegurar que todos os elementos serão atribuídos um cabeçalho de Cache-Control.
Remover| Esta opção garante que um cabeçalho de Cache-Control não está incluído com a resposta de cabeçalho de Olá. Se já tiver sido atribuído um cabeçalho de Cache-Control, em seguida,-irá ser eliminado da resposta de cabeçalho de Olá.

**Comportamento predefinido:** substituir.

###<a name="cache-key-query-string"></a>Cadeia de consulta de chave da cache
**Objetivo:** determina se a chave de cache irá incluir ou excluir os parâmetros de cadeia de consulta associados a um pedido.

Informações da chave:

- Especifique um ou mais nomes de parâmetro de cadeia de consulta. Cada nome de parâmetro deve ser delimitado com um único espaço.
- Esta funcionalidade determina se os parâmetros de cadeia de consulta irão ser incluídos ou excluídos da Olá-chave da cache. Para cada opção abaixo, são fornecidas informações adicionais.

Tipo|Descrição
--|--
 Incluir|  Indica se cada parâmetro especificado deve ser incluído nas Olá-chave da cache. Uma chave exclusiva de cache será gerada para cada pedido que contém um valor exclusivo para um parâmetro de cadeia de consulta definido nesta funcionalidade. 
 Incluir todos os  |Indica que será criada uma chave de cache exclusiva para cada recurso de tooan pedido que inclui uma cadeia de consulta exclusivo. Este tipo de configuração não é normalmente recomendado, uma vez que poderá provocar tooa pequena percentagem de acertos na cache. Isto irá aumentar a carga de Olá no servidor de origem Olá, uma vez que pode ter tooserve mais pedidos. Esta configuração duplica Olá comportamento conhecido como "exclusivo-cache" na página de colocação em cache de cadeia de consulta a colocação em cache. 
 Excluir | Indica que apenas Olá especificado parâmetro (s) será excluído de Olá-chave da cache. Todos os outros parâmetros de cadeia de consulta serão incluídos em Olá-chave da cache. 
 Excluir todos os  |Indica que todos os parâmetros de cadeia de consulta serão excluídos Olá-chave da cache. Esta configuração duplica predefinido Olá comportamento, que é conhecido como "standard-cache" na página de colocação em cache de cadeia de consulta a colocação em cache. 

energia Olá do motor de regras de HTTP permite-lhe forma de Olá toocustomize no qual está implementada o colocação em cache de cadeia de consulta. Por exemplo, pode especificar que a consulta colocação em cache apenas ser efetuada em determinadas localizações ou tipos de ficheiro.

Se gostaria de cadeia de consulta tooduplicate Olá comportamento conhecido como "não-cache" na página de colocação em cache de cadeia de consulta a colocação em cache, em seguida, terá de toocreate uma regra que contém uma condição de correspondência de carateres universais de consulta de URL e uma funcionalidade de ignorar a Cache. Olá condição de correspondência de consulta de URL com carateres universais deve ser definido tooan asterisco (*).

#### <a name="sample-scenarios"></a>Cenários de exemplo

Utilização de exemplo para esta funcionalidade é fornecida em baixo. Um exemplo de pedido e Olá predefinido cache-chave são fornecidas em baixo.

- **Exemplo de pedido:** http://wpc.0001.&lt; Domínio&gt;/800001/Origin/folder/asset.htm?sessionid=1234 e idioma = EN & userid = 01
- **Predefinido da chave de cache:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Incluir

Configuração de exemplo:

- **Tipo:** incluem
- **Parâmetro (s):** idioma

Este tipo de configuração irá gerar Olá seguir a cache de parâmetro de cadeia de consulta-chave:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Incluir todos os

Configuração de exemplo:

- **Tipo:** incluir todos os

Este tipo de configuração irá gerar Olá seguir a cache de parâmetro de cadeia de consulta-chave:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Excluir

Configuração de exemplo:

- **Tipo:** excluir
- **Parâmetro (s):** sessionid userid

Este tipo de configuração irá gerar Olá seguir a cache de parâmetro de cadeia de consulta-chave:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Excluir todos os

Configuração de exemplo:

- **Tipo:** excluir todos os

Este tipo de configuração irá gerar Olá seguir a cache de parâmetro de cadeia de consulta-chave:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Chave da cache reescrever
**Objetivo:** Reescritas Olá associada a um pedido de chave de cache.

Uma chave de cache é o caminho relativo Olá que identifique um recurso para fins de Olá da colocação em cache. Por outras palavras, os nossos servidores irão verificar para uma versão em cache de um recurso de acordo com o caminho de tooits tal como definido pela respetiva chave de cache.

Configure esta funcionalidade, definindo ambos Olá seguintes opções:

Opção|Descrição
--|--
Caminho original| Defina Olá caminho relativo toohello tipos de pedidos cuja chave de cache irá ser foi reescrita. Pode ser definido um caminho relativo ao selecionar um caminho de base de origem e, em seguida, definir um padrão de expressão regular.
Novo caminho|Defina o caminho relativo de Olá para Olá nova cache-chave. Pode ser definido um caminho relativo ao selecionar um caminho de base de origem e, em seguida, definir um padrão de expressão regular. Este caminho relativo que pode ser construído dinamicamente através da utilização de Olá de variáveis de HTTP
**Comportamento predefinido:** -chave um pedido da cache é determinado pelo URI do pedido de Olá.

###<a name="complete-cache-fill"></a>Concluir o preenchimento da Cache
**Objetivo:** determina o que acontece quando um pedido resulta numa falha de acerto na cache parciais num servidor edge.

Uma falha de acerto na cache parciais descreve o estado de cache de Olá para um recurso que não estava servidor edge de tooan completamente transferido. Se um recurso é colocado em cache apenas parcialmente num servidor edge, em seguida, hello pedido seguinte para esse recurso será reencaminhado novamente toohello servidor de origem.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
Uma falha de acerto na cache parcial ocorre normalmente depois de um utilizador cancela uma transferência ou para recursos de que apenas são pedidos através de pedidos de intervalo HTTP. Esta funcionalidade é mais útil para grandes ativos onde os utilizadores serão não normalmente transferi-los de início toofinish (por exemplo, vídeos). Como consequência, esta funcionalidade está ativada por predefinição na plataforma de HTTP grande Olá. Está desativada em todas as outras plataformas.

É recomendado tooleave Olá configuração para a plataforma de HTTP grande Olá, uma vez que irá reduzir a carga de Olá no seu servidor de origem do cliente e aumentar a velocidade de Olá em que os seus clientes transferem o conteúdo.

Devido a forma de toohello na cache de que as definições são registadas, esta funcionalidade não pode ser associada com Olá seguintes condições de correspondência: Edge Cname, Literal de cabeçalho de pedido, universal do cabeçalho de pedido, o Literal de consulta do URL e consulta de URL com carateres universais.

Valor|resultado
--|--
Ativado|Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá é tooforce Olá edge servidor tooinitiate uma obtenção de fundo do elemento de Olá do servidor de origem Olá. Após o qual, asset Olá estarão disponíveis na cache local do servidor edge Olá.
Desativado|Impede que um servidor edge efetuar uma obtenção de fundo para o recurso de Olá. Isto significa que esse pedido seguinte Olá para esse recurso a que região fará com que um toorequest de servidor edge-lo a partir do servidor de origem do cliente Olá.

**Comportamento predefinido:** ativada.

###<a name="compress-file-types"></a>Comprima os tipos de ficheiro
**Objetivo:** define os formatos de ficheiro Olá que irão ser comprimidos no servidor de Olá.

Um formato de ficheiro pode ser especificado utilizando o respetivo tipo de suporte de Internet (ou seja, Content-Type). Tipo de suporte de Internet é metadados independentes da plataforma que permite que o formato de ficheiro do Olá tooidentify nossos servidores de um recurso específico. É fornecida uma lista dos tipos de suportes de dados de Internet comuns abaixo.

Tipo de suporte de Internet|Descrição
--|--
texto/plain|Ficheiros de texto simples
texto/html| Ficheiros HTML
texto/css|Folhas de estilo em cascata (CSS)
Application/x-javascript|Javascript
aplicação/javascript|Javascript
Informações da chave:

- Especifique vários tipos de suportes de dados de Internet por delimiting cada um com um único espaço. 
- Esta funcionalidade só irá comprimir ativos cujo tamanho é inferior a 1 MB. Maior ativos não serão comprimidos pelos nossos servidores.
- Determinados tipos de conteúdos, tais como imagens, vídeos e os recursos de suporte de dados de áudio (por exemplo, JPG, MP3, MP4, etc.), já são comprimidos. Compressão adicional nestes tipos de recursos não irá reduzir significativamente o tamanho de ficheiro. Por conseguinte, é recomendado que não ativar a compressão nestes tipos de recursos.
- Carateres universais, tais como a série de asteriscos, não são suportadas.
- Antes de adicionar esta regra de tooa funcionalidade, certifique-se de que tooset a opção de compressão desativado na página de compressão de Olá plataforma toowhich que será aplicada esta regra.

###<a name="default-internal-max-age"></a>Idade de máx. de interno predefinida
**Objetivo:** intervalo de idade máxima do determina Olá predefinido para revalidação de cache de servidor de tooorigin servidor edge. Por outras palavras, Olá quantidade de tempo que irá passar antes de um servidor edge irá verificar se um recurso em cache corresponde ao recurso Olá armazenado no servidor de origem Olá.

Informações da chave:

- Esta ação só ocorrerá de respostas de um servidor de origem que não foi possível atribuir uma indicação de idade máxima no cabeçalho de Cache-Control ou Expires.
- Esta ação não irá demorar local para recursos que não são considerados colocáveis.
- Esta ação não afeta revalidations de cache do browser tooedge servidor. Estes tipos de revalidations são determinados pelo Cache-Control ou Expires cabeçalhos enviados toohello browser, que pode ser personalizada com a funcionalidade de idade de máxima externo.
- resultados de Olá desta ação não tem um efeito observable nos cabeçalhos de resposta de Olá e conteúdo Olá devolvido de servidores edge para o conteúdo, mas pode ter um efeito na quantidade de Olá de tráfego de revalidação enviado a partir do servidor de origem de tooyour de servidores edge.
- Configure esta funcionalidade por:
    - Selecionar o código de estado de Olá para os quais pode ser aplicada a idade interno-máxima uma predefinição.
    - Especificar um valor inteiro e, em seguida, selecionar Olá unidade de tempo pretendido (ou seja, segundos, minutos, horas, etc.). Este valor define o intervalo de idade máxima interno do Olá predefinido.

- Unidade de tempo de Olá definição demasiado "Off" atribuirá um intervalo de idade máxima interno do predefinido de 7 dias para pedidos que não tenham sido atribuídos uma indicação de idade máxima na respetiva Cache-Control ou Expires cabeçalho.
- Devido a forma de toohello na cache de que as definições são registadas, esta funcionalidade não pode ser associada com Olá seguintes condições de correspondência: 
    - Limite 
    - CNAME
    - Literal de cabeçalho de pedido
    - Caráter universal de cabeçalho de pedido
    - Método de pedido
    - Literal de consulta de URL
    - Consulta de URL com carateres universais

**Valor predefinido:** 7 dias

###<a name="expires-header-treatment"></a>Tratamento de cabeçalho de expirar
**Objetivo:** controla geração Olá dos cabeçalhos de expira por um servidor edge, quando a funcionalidade de idade de máxima externo está ativa.

Olá tooachieve de forma mais fácil este tipo de configuração é tooplace Olá externos de atribuição de idade máxima e funcionalidades de tratamento de cabeçalho expira Olá no Olá mesma instrução.

Valor|resultado
--|--
Substituir|Garante que Olá seguintes ações irão ocorrer:<br/>-Substitui o cabeçalho de expira gerado pelo servidor de origem Olá.<br/>-Adiciona o cabeçalho de expira produzido pela resposta do Olá idade de máxima externo funcionalidade toohello.
Pass-Through|Garante que o cabeçalho de expira produzido pela funcionalidade de idade de máxima externo Olá nunca é adicionado toohello resposta. <br/> Se o servidor de origem Olá produz um cabeçalho de expira, este irá percorrer pelo utilizador final do toohello. <br/>Se o servidor de origem Olá não produz um cabeçalho de expira, em seguida, esta opção a toonot de cabeçalho de resposta de Olá causa pode conter um cabeçalho de expira.
Adicionar se estiverem em falta| Se um cabeçalho de expira não foi recebido do servidor de origem Olá, esta opção adiciona o cabeçalho de expira produzido pela funcionalidade de idade de máxima externo Olá. Esta opção é útil para assegurar que todos os elementos serão atribuídos um cabeçalho de expira.
Remover| Garante que um cabeçalho de expira não está incluído com a resposta de cabeçalho de Olá. Se já tiver sido atribuído um cabeçalho de expira, em seguida, este irá ser eliminado da resposta de cabeçalho de Olá.

**Comportamento predefinido:** substituir

###<a name="external-max-age"></a>Externa de atribuição de idade máxima
**Objetivo:** intervalo de idade máxima de Olá determina para revalidação de cache do browser tooedge servidor. Por outras palavras, pode verificar Olá período de tempo que irá passar antes de um browser para uma nova versão de um ativo de um servidor edge.

A ativação desta funcionalidade irá gerar Cache-controlo: max-idade e expira cabeçalhos a partir de nossos servidores edge e enviá-los cliente toohello HTTP. Por predefinição, estes cabeçalhos substituirá as criadas pelo servidor de origem Olá. No entanto, o tratamento de cabeçalho de Cache-Control e as funcionalidades de tratamento de cabeçalho expira podem ser utilizado tooalter este comportamento.

Informações da chave:

- Esta ação não afeta revalidations de cache do servidor do contorno servidor tooorigin. Estes tipos de revalidations são determinados por cabeçalhos Cache-controlo/expira recebidos do servidor de origem Olá e podem ser personalizados com a predefinição interna-idade máxima e as funcionalidades de idade de máxima de interno Force.
- Configure esta funcionalidade, especificando um valor inteiro e selecionar a unidade de tempo pretendido hello (ou seja, segundos, minutos, horas, etc.).
- A definição deste valor negativo de tooa funcionalidade faz com que a nossa toosend de servidores edge uma Cache-controlo: não-cache e um período de tempo expira que está definido no Olá passado com cada browser toohello de resposta. Apesar de um cliente HTTP serão colocados em cache não resposta Olá, esta definição não irá afetar a resposta de Olá dos nossos servidores edge capacidade toocache do servidor de origem Olá.
- Unidade de tempo de Olá definição demasiado "Off" irá desativar esta funcionalidade. Os cabeçalhos Cache-controlo/expira em cache com a resposta de hello do servidor de origem Olá passará toohello browser.

**Comportamento predefinido:** desativado

###<a name="force-internal-max-age"></a>Forçar interna de atribuição de idade máxima
**Objetivo:** intervalo de idade máxima de Olá determina para revalidação de cache de servidor de tooorigin servidor edge. Por outras palavras, Olá período de tempo que irá passar antes de um servidor edge, pode verificar se um recurso em cache corresponde ao recurso Olá armazenado no servidor de origem Olá.

Informações da chave:

- Esta funcionalidade irá substituir o intervalo de idade máxima de Olá definido na Cache-Control ou Expires os cabeçalhos de gerado a partir de um servidor de origem.
- Esta funcionalidade não afeta revalidations de cache do browser tooedge servidor. Estes tipos de revalidations são determinados pelo Cache-Control ou Expires cabeçalhos enviados toohello browser.
- Esta funcionalidade não tem um efeito observable na resposta Olá fornecida por um autor de pedido de toohello de servidor edge. No entanto, pode ter um efeito na quantidade de Olá de tráfego de revalidação enviado do nosso servidor de origem do contorno servidores toohello.
- Configure esta funcionalidade por:
    - Selecionar o código de estado de Olá para os quais será aplicada uma idade máxima interna.
    - Especificar um valor inteiro e selecionar Olá unidade de tempo pretendido (ou seja, segundos, minutos, horas, etc.). Este valor define o intervalo de idade máxima do pedido de Olá.

- Unidade de tempo de Olá definição demasiado "Off" desativa a esta funcionalidade. Um intervalo de idade máxima interno não será atribuído toorequested ativos. Se o cabeçalho original Olá não contém instruções de colocação em cache, em seguida, asset Olá irá ser colocadas em cache toohello definição ativa a funcionalidade de predefinida interno-idade máxima de acordo com.
- Devido a forma de toohello na cache de que as definições são registadas, esta funcionalidade não pode ser associada com Olá seguintes condições de correspondência: 
    - Limite 
    - CNAME
    - Literal de cabeçalho de pedido
    - Caráter universal de cabeçalho de pedido
    - Método de pedido
    - Literal de consulta de URL
    - Consulta de URL com carateres universais

**Comportamento predefinido:** desativado

###<a name="h264-support-http-progressive-download"></a>Suporte de 264 (transferência progressiva HTTP)
**Objetivo:** tipos de Olá determina de 264 formatos de ficheiro que podem ser utilizado toostream conteúdo.

Informações da chave:

- Defina um conjunto delimitada por espaços de extensões de nome de ficheiro permitidas 264 na opção de extensões de ficheiro. A opção de extensões de ficheiro irá substituir o comportamento predefinido de Olá. Manter MP4 e F4V suporte, incluindo as extensões de nome de ficheiro quando definir esta opção. 
- Certifique-se de que tooinclude um período ao especificar cada extensão de nome de ficheiro (por exemplo, mp4 .f4v).

**Comportamento predefinido:** HTTP transferência progressiva transferir suporta MP4 e F4V suporte de dados por predefinição.

###<a name="honor-no-cache-request"></a>Pedido de cache não honor
**Objetivo:** determina se não-pedidos um cliente HTTP serão reencaminhados toohello servidor de origem.

Um pedido de cache não ocorre quando o cliente de Olá HTTP envia uma Cache-controlo: não-cache e/ou Pragma:no-cabeçalho de cache no pedido de Olá HTTP.

Valor|resultado
--|--
Ativado|Permite que o servidor de origem do toobe toohello reencaminhada os pedidos de cache não de um cliente HTTP e servidor de origem Olá devolverá cabeçalhos de resposta de Olá e um corpo de Olá através do servidor edge de Olá cliente back toohello HTTP.
Desativado|Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá é tooprevent de pedidos na cache de não de reencaminhados toohello servidor de origem.

Para todo o tráfego de produção, é altamente recomendado tooleave esta funcionalidade no respectivo estado predefinido desativado. Caso contrário, não serão possível proteger os servidores de origem dos utilizadores finais que inadvertidamente poderão acionar muitos pedidos não-cache ao atualizar as páginas web ou de Olá vários jogadores popular do suporte de dados que são codificadas toosend um cabeçalho de cache não com cada pedido de vídeo. Contudo, esta funcionalidade pode ser a transição de não produção tooapply útil toocertain ou testar diretórios, na ordem tooallow raiz toobe conteúdo solicitados a pedido do servidor de origem Olá.

Estado da cache de Olá que será reportado para um pedido permitido é de servidor de origem tooan toobe reencaminhado devido a funcionalidade de toothis TCP_Client_Refresh_Miss. O relatório de Estados de Cache, o que está disponível no módulo de relatórios de núcleos de Olá, fornece informações estatísticas por Estado da cache. Isto permite-lhe número de Olá tootrack e a percentagem de pedidos que são reencaminhados de servidor de origem tooan devido toothis funcionalidade.

**Comportamento predefinido:** desativado.

###<a name="ignore-origin-no-cache"></a>Ignorar a cache não de origem
**Objetivo:** determina se o nosso CDN ignorará Olá seguir diretivas servidas a partir de um servidor de origem:

- Cache-Control: privada
- Cache-Control: arquivo não
- Cache-Control: cache não
- Pragma: cache não

Informações da chave:

- Configure esta funcionalidade, definir uma lista delimitada por espaços de códigos de estado para o qual Olá acima diretivas será ignorada.
- Olá conjunto de códigos de estado válido para esta funcionalidade são: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 e 505.
- Desative esta funcionalidade ao defini-la tooa de valor em branco.
- Devido a forma de toohello na cache de que as definições são registadas, esta funcionalidade não pode ser associada com Olá seguintes condições de correspondência: 
    - Limite 
    - CNAME
    - Literal de cabeçalho de pedido
    - Caráter universal de cabeçalho de pedido
    - Método de pedido
    - Literal de consulta de URL
    - Consulta de URL com carateres universais

**Comportamento predefinido:** o comportamento predefinido é toohonor Olá acima diretivas.

###<a name="ignore-unsatisfiable-ranges"></a>Ignorar intervalos Unsatisfiable 
**Objetivo:** determina resposta Olá que vai ser devolvida tooclients quando um pedido gera um código de estado 416 pedido intervalo não satisfatório.

Por predefinição, este código de estado é devolvido quando Olá especificado não é possível satisfazer o pedido de intervalo de bytes por um servidor edge e um campo de cabeçalho de pedido de intervalo se não foi especificado.

Valor|resultado
-|-
Ativado|Impede que os nossos servidores de limite de pedido de intervalo de byte inválido tooan está a responder com um código de estado de pedido intervalo não satisfatório 416. Em vez disso nossos servidores irão fornecer o recurso solicitado Olá e devolver um 200 OK para cliente Olá.
Desativado|Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá é toohonor o código de estado 416 pedido intervalo não satisfatório.

**Comportamento predefinido:** desativado.

###<a name="internal-max-stale"></a>Interna obsoleta máx.
**Objetivo:** controla quanto passado Olá normal a hora de expiração um recurso em cache pode ser servido a partir de um servidor edge quando o servidor edge de Olá é toorevalidate não é possível Olá colocados em cache recurso com o servidor de origem Olá.

Normalmente, quando o período de idade máxima de um recurso expira, o servidor edge de Olá enviará um servidor de origem do revalidação pedido toohello. Olá servidor de origem serão, em seguida, responder com um um 304 não modificado para dar servidor edge de Olá uma concessão de raiz no elemento de cache Olá or else com 200 OK para fornecer o servidor edge de Olá com uma versão atualizada do recurso de Olá em cache.

Se o servidor edge de Olá tooestablish não é possível uma ligação com o servidor de origem Olá durante a tentativa de tal revalidação de uma, esta funcionalidade obsoleta máximo interno controla se e para Olá quanto, servidor edge pode continuar asset do tooserve Olá agora obsoleta.

Tenha em atenção que este intervalo de tempo é iniciado quando idade máxima do elemento de Olá expira, não ocorra hello revalidação de falha. Por conseguinte, o período máximo de Olá durante os quais um recurso pode ser servido sem êxito revalidação é Olá período de tempo especificado pela combinação de Olá de idade máxima plus máximo obsoleta. Por exemplo, se um recurso foi colocado em cache no 9:00, com uma duração do número máximo de 30 minutos e obsoleta uma máximo de 15 minutos, e tente uma revalidação de falhas em 9:44 resultaria num utilizador final recetor Olá obsoletos em cache recurso, enquanto uma tentativa de falha revalidação de 9:46 resultaria em utilizador final Olá receber um tempo limite do Gateway 504.

Qualquer valor configurado para esta funcionalidade é substituída pela Cache-controlo: tem-revalidate ou colocar em Cache-controlo: proxy-revalidate cabeçalhos recebidos do servidor de origem Olá. Se qualquer um desses cabeçalhos não for recebida do servidor de origem Olá quando um recurso inicialmente é colocado em cache, o servidor edge de Olá processará não um recurso em cache obsoleto. Nesse caso, se servidor edge de Olá toorevalidate não é possível com origem Olá quando o intervalo de idade máxima do elemento de Olá tiver expirado, em seguida, servidor edge de Olá irá devolver um tempo limite do Gateway 504.

Informações da chave:

- Configure esta funcionalidade por:
    - Selecionar o código de estado de Olá para o qual uma obsoleta máximo será aplicada.
    - Especificar um valor inteiro e, em seguida, selecionar Olá unidade de tempo pretendido (ou seja, segundos, minutos, horas, etc.). Este valor define Olá interno máximo obsoleta que será aplicada.

- Unidade de tempo de Olá definição demasiado "Off" irá desativar esta funcionalidade. Um recurso em cache não será servido que ultrapassem o tempo de expiração normal.
- Devido a forma de toohello na cache de que as definições são registadas, esta funcionalidade não pode ser associada com Olá seguintes condições de correspondência: 
    - Limite 
    - CNAME
    - Literal de cabeçalho de pedido
    - Caráter universal de cabeçalho de pedido
    - Método de pedido
    - Literal de consulta de URL
    - Consulta de URL com carateres universais

**Comportamento predefinido:** 2 minutos

###<a name="partial-cache-sharing"></a>Partilha de Cache parciais
**Objetivo:** determina se um pedido pode gerar o conteúdo parcialmente em cache.

Esta cache parcial, em seguida, pode ser utilizado toofulfill novos pedidos para esse conteúdo até Olá pedidos de conteúdo é totalmente colocados em cache.

Valor|resultado
-|-
Ativado|Pedidos podem gerar o conteúdo parcialmente em cache.
Desativado|Só podem gerar um totalmente em cache pedidos de versão do Olá pedida conteúdo.

**Comportamento predefinido:** desativado.

###<a name="prevalidate-cached-content"></a>Prevalidate conteúdos em cache
**Objetivo:** determina se o conteúdo em cache vai ser elegível para revalidação antecipada antes do valor de TTL expire.

Defina a quantidade de Olá de tempo de expiração de toohello anterior de Olá pediu o TTL do conteúdo durante os quais irá ser elegível para revalidação antecipada.

Informações da chave:

- Selecionar "Off" como unidade de tempo de Olá requer o local de tootake revalidação depois TTL do conteúdo na cache de Olá expirou. Não deve ser especificado o tempo e serão ignorada.

**Comportamento predefinido:** desativado. Revalidação pode apenas ocorrer após Olá TTL de conteúdo em cache expirou.

###<a name="refresh-zero-byte-cache-files"></a>Atualizar os ficheiros de Cache Zero bytes
**Objetivo:** determina o modo como os pedidos de um cliente HTTP para um elemento de cache de 0 bytes é processado pelos nossos servidores edge.

Os valores válidos são:

Valor|resultado
--|--
Ativado|Faz com que o recurso do Olá servidor toore obtenção nosso limite do servidor de origem Olá.
Desativado|Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá é tooserve dos recursos de cache válido após pedido.
Esta funcionalidade não é necessária para a colocação em cache correto e de entrega de conteúdos, mas poderá ser útil como uma solução. Por exemplo, generators conteúdos dinâmicos nos servidores de origem inadvertidamente podem resultar em respostas 0 bytes enviadas toohello servidores de limite. Estes tipos de respostas são normalmente colocadas em cache pelos nossos servidores edge. Se souber que uma resposta de 0 bytes nunca é uma resposta válida 

para esse conteúdo, em seguida, esta funcionalidade pode impedir que estes tipos de recursos de ser servido tooyour clientes.

**Comportamento predefinido:** desativado.

###<a name="set-cacheable-status-codes"></a>Códigos de estado colocáveis de conjunto
**Objetivo:** define Olá conjunto de códigos de estado que podem resultar num conteúdos em cache.

Por predefinição, a colocação em cache é apenas ativada para 200 respostas OK.

Defina um conjunto delimitada por espaços de códigos de estado de Olá assim o desejar.

Informações da chave:

- Também ative a funcionalidade de ignorar não-Cache de origem. Se essa funcionalidade não estiver ativada, em seguida, as respostas de não 200 OK poderão não ser colocadas em cache.
- Olá conjunto de códigos de estado válido para esta funcionalidade são: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 e 505.
- Esta funcionalidade não pode ser utilizado toodisable a colocação em cache para as respostas que geram um código de estado OK 200.

**Comportamento predefinido:** colocação em cache só é ativada para as respostas que geram um código de estado OK 200.
###<a name="stale-content-delivery-on-error"></a>Entrega de conteúdos obsoleta com o erro
**Objetivo:** 

Determina se expirado os conteúdos em cache serão entregues quando ocorre um erro durante a revalidação de cache ou quando Olá ao obter conteúdo de pedido do servidor de origem do cliente Olá.

Valor|resultado
-|-
Ativado|Conteúdo obsoleto será servido toohello autor do pedido quando ocorre um erro durante a um servidor de origem de tooan de ligação.
Desativado|Erro de servidor de origem a Olá será reencaminhado toohello autor do pedido.

**Comportamento predefinido:** desativado

###<a name="stale-while-revalidate"></a>Obsoleta ao Revalidate
**Objetivo:** melhora o desempenho, permitindo nossos servidores edge tooserve obsoletos toohello conteúdo solicitador enquanto revalidação ocorre.

Informações da chave:

- comportamento de Olá desta funcionalidade varia de acordo com unidade de tempo selecionado toohello.
    - **Unidade de tempo:** especificar um período de tempo e selecione uma hora unidade (por exemplo, segundos, minutos, horas, etc.) tooallow obsoletos entrega de conteúdos. Este tipo de configuração permite Olá CDN tooextend Olá período de tempo que pode fornecer conteúdo antes de exigir validação de acordo com toohello seguinte fórmula:**TTL** + **obsoletos enquanto Revalidate tempo** 
    - **Desativar:** selecione "Off" revalidação de toorequire antes de um pedido para conteúdo obsoleto pode ser servido.
        - Não especifique um período de tempo, uma vez que é forçando e serão ignorada.

**Comportamento predefinido:** desativado. Revalidação tem de efetuar antes de Olá pedido de conteúdo pode ser fornecido.

###<a name="comment"></a>Comentário
**Objetivo:** permite toobe uma nota adicionado dentro de uma regra.

Uma utilização para esta funcionalidade é tooprovide obter informações adicionais sobre fins gerais de Olá de uma regra ou por que razão um determinado corresponde a condição ou funcionalidade foi adicionada toohello regra.

Informações da chave:

- Pode ser especificado um máximo de 150 carateres.
- Certifique-se de que tooonly utilizar apenas carateres alfanuméricos.
- Esta funcionalidade não afeta o comportamento de Olá da regra de Olá. Apenas o principal objetivo é tooprovide uma área onde pode fornecer informações para referência futura ou que pode ajudar ao resolver problemas com a regra de Olá.
 
## <a name="headers"></a>Cabeçalhos

Estas funcionalidades são tooadd concebida, modificar ou eliminar os cabeçalhos de pedido de Olá ou resposta.

Nome | Objetivo
-----|--------
Cabeçalho de resposta de antiguidade | Determina se um cabeçalho de resposta de idade será incluído na resposta Olá enviada toohello autor do pedido.
Cabeçalhos de resposta de Cache de depuração | Determina se uma resposta pode incluir o cabeçalho de resposta de EC-X-Debug Olá que fornece informações sobre a política de cache de Olá para Olá de recurso pedido.
Modificar o cabeçalho de pedido de cliente | Substitui, acrescenta ou elimina um cabeçalho de um pedido.
Modificar o cabeçalho de resposta do cliente | Substitui, acrescenta ou elimina um cabeçalho de resposta.
Cabeçalho IP do conjunto de cliente personalizado | Permita Olá endereço IP do cliente pedir Olá toobe toohello adicionado pedido como um cabeçalho de pedido personalizado.

###<a name="age-response-header"></a>Cabeçalho de resposta de antiguidade
**Objetivo**: determina se um cabeçalho de resposta de idade será incluído em Olá resposta enviada toohello autor do pedido.
Valor|resultado
--|--
Ativado | cabeçalho de resposta de idade Olá será incluído na resposta Olá enviada toohello autor do pedido.
Desativado | cabeçalho de resposta de idade Olá será excluído da resposta de Olá enviada toohello autor do pedido.

**Comportamento de predefinido**: desativado.

###<a name="debug-cache-response-headers"></a>Cabeçalhos de resposta de Cache de depuração
**Objetivo:** determina se uma resposta pode incluir o cabeçalho de resposta de EC-X-Debug que fornece informações sobre a política de cache de Olá para Olá de recurso pedido.

Depurar a resposta de cache cabeçalhos serão incluídos na resposta Olá quando duas seguintes Olá forem verdadeiras:

- Olá depurar funcionalidade de cabeçalhos de resposta de Cache foi ativada no pedido pretendido Olá.
- Olá acima pedido define o conjunto de Olá de cabeçalhos de resposta de cache de depuração será incluído na resposta Olá.

Resposta de cache cabeçalhos podem ser solicitados, incluindo Olá seguir cabeçalho e Olá diretivas pretendidas do pedido de Olá de depuração:

X-EC-Debug: _Directive1_,_Directive2_,_DirectiveN_

**Exemplo:**

EC-X-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Valor|resultado
-|-
Ativado|Pedidos de cabeçalhos de resposta de cache de depuração irão devolver uma resposta que inclui o cabeçalho X-EC-Debug.
Desativado|O cabeçalho de resposta EC-X-Debug será excluído da resposta de Olá.

**Comportamento predefinido:** desativado.

###<a name="modify-client-response-header"></a>Modificar o cabeçalho de resposta do cliente
**Objetivo:** cada pedido contém um conjunto de [cabeçalhos de pedido]() que descrevem-lo. Esta funcionalidade pode optar por:

- Acrescentar ou substituir o valor de Olá atribuído tooa cabeçalho do pedido. Se o cabeçalho de pedido especificado Olá não existir, em seguida, esta funcionalidade irá adicioná-la toohello pedido.
- Elimine um cabeçalho de pedido do pedido de Olá.

Pedidos que são reencaminhados de servidor de origem tooan irão refletir alterações Olá graças esta funcionalidade.

Uma das seguintes ações de Olá pode ser efetuada num cabeçalho de pedido:

Opção|Descrição|Exemplo
-|-|-
Acrescentar|Olá especificado o valor será adicionado toend de valor de cabeçalho de pedido Olá existente.|**O valor do cabeçalho (cliente) do pedido:**Value1 <br/> **O valor do cabeçalho (motor de regras de HTTP) do pedido:** Value2 <br/>**Novo valor de cabeçalho de pedido:** Value1Value2
Substituir|pedido de Olá valor de cabeçalho será toohello conjunto especificado.|**O valor do cabeçalho (cliente) do pedido:**Value1 <br/>**O valor do cabeçalho (motor de regras de HTTP) do pedido:** Value2 <br/>**Novo valor de cabeçalho de pedido:** Value2 <br/>
Eliminar|Elimina o cabeçalho de pedido especificado Olá.|**O valor do cabeçalho (cliente) do pedido:**Value1 <br/> **Modificar configuração de cabeçalho de pedido de cliente:** eliminar Olá cabeçalho do pedido em questão. <br/>**Resultado:** Olá especificado cabeçalho do pedido não é reencaminhado de servidor de origem toohello.

Informações da chave:

- Certifique-se de que o valor de Olá especificado na opção de nome é uma correspondência exata para o cabeçalho de pedido pretendido Olá.
- Caso não é tida em conta para efeitos de Olá de identificar um cabeçalho. Por exemplo, qualquer um dos seguintes variações do nome de cabeçalho de Cache-Control de Olá podem ser utilizado tooidentify-lo:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Certifique-se de que tooonly utilizar apenas carateres alfanuméricos, traços ou carateres de sublinhado, ao especificar um nome de cabeçalho.
- Eliminar um cabeçalho irá impedir que sejam encaminhados o servidor de origem tooan pelos nossos servidores edge.
- Olá seguintes cabeçalhos estão reservados e não podem ser modificados por esta funcionalidade:
    - reencaminhado
    - anfitrião
    - através do
    - aviso
    - x-reencaminhados-para
    - Todos os nomes de cabeçalho que começam por "x-ec" estão reservados.

###<a name="modify-client-response-header"></a>Modificar o cabeçalho de resposta do cliente
Cada resposta contém um conjunto de [cabeçalhos de resposta]() que descrevem-lo. Esta funcionalidade pode optar por:

- Acrescentar ou substituir o valor de Olá atribuído tooa cabeçalho de resposta. Se o cabeçalho de pedido especificado Olá não existir, em seguida, esta funcionalidade irá adicioná-la toohello resposta.
- Elimine um cabeçalho de resposta da resposta Olá.

Por predefinição, os valores de cabeçalho de resposta são definidos por um servidor de origem e pelos nossos servidores edge.

Uma das seguintes ações de Olá pode ser efetuada num cabeçalho de resposta:

Opção|Descrição|Exemplo
-|-|-
Acrescentar|Olá especificado o valor será adicionado toend de valor de cabeçalho de pedido Olá existente.|**O valor de cabeçalho de resposta (cliente):**Value1 <br/> **O valor de cabeçalho de resposta (motor de regras de HTTP):** Value2 <br/>**Novo valor de cabeçalho de resposta:** Value1Value2
Substituir|pedido de Olá valor de cabeçalho será toohello conjunto especificado.|**O valor de cabeçalho de resposta (cliente):**Value1 <br/>**O valor de cabeçalho de resposta (motor de regras de HTTP):** Value2 <br/>**Novo valor de cabeçalho de resposta:** Value2 <br/>
Eliminar|Elimina o cabeçalho de pedido especificado Olá.|**O valor do cabeçalho (cliente) do pedido:** Value1 <br/> **Modificar configuração de cabeçalho de pedido de cliente:** cabeçalho de resposta de Olá Delete em questão. <br/>**Resultado:** Olá especificado de cabeçalho de resposta não será reencaminhado toohello autor do pedido.

Informações da chave:

- Certifique-se de que o valor de Olá especificado na opção de nome é uma correspondência exata para o cabeçalho de resposta pretendido Olá. 
- Caso não é tida em conta para efeitos de Olá de identificar um cabeçalho. Por exemplo, qualquer um dos seguintes variações do nome de cabeçalho de Cache-Control de Olá podem ser utilizado tooidentify-lo:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Eliminar um cabeçalho irá impedir que sejam encaminhados toohello autor do pedido.
- Olá seguintes cabeçalhos estão reservados e não podem ser modificados por esta funcionalidade:
    - codificação aceitar
    - idade
    - ligação
    - codificação de conteúdo
    - comprimento do conteúdo
    - intervalo de conteúdo
    - Data
    - servidor
    - trailer
    - codificação de transferência
    - atualização
    - variar
    - através do
    - aviso
    - Todos os nomes de cabeçalho que começam por "x-ec" estão reservados.

###<a name="set-client-ip-custom-header"></a>Cabeçalho IP do conjunto de cliente personalizado
**Objetivo:** adiciona um cabeçalho personalizado que identifica o cliente efetuou Olá por pedido de toohello de endereço IP.

A opção de nome de cabeçalho define o nome de Olá dos cabeçalhos de pedido personalizada de olá onde endereço IP do cliente Olá será armazenado.

Esta funcionalidade permite que um cliente toofind de servidor de origem endereços de IP de cliente através de um cabeçalho de pedido personalizado. Se o pedido de Olá é servido a partir da cache, o servidor de origem Olá não a ser informado de endereço IP do cliente Olá. Por conseguinte, é recomendado que esta funcionalidade ser utilizada com ADN ou recursos que não irão ser colocados em cache.

Certifique-se que o nome do cabeçalho especificado Olá não corresponde a nenhum dos seguintes Olá:

- Nomes de cabeçalho de pedido padrão. É possível encontrar uma lista de nomes de cabeçalho padrão no [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Nomes de cabeçalho reservado:
    - reencaminhado para
    - anfitrião
    - variar
    - através do
    - aviso
    - x-reencaminhados-para
    - Todos os nomes de cabeçalho que começam por "x-ec" estão reservados.
 
## <a name="logs"></a>Registos

Estas funcionalidades são os dados de Olá toocustomize concebida armazenados nos ficheiros de registo não processados.

Nome | Objetivo
-----|--------
Campo de registo personalizado 1 | Determina o formato de Olá e conteúdo Olá que será atribuído o campo de registo personalizado toohello num ficheiro de registo não processados.
Cadeia de consulta de registo | Determina se uma cadeia de consulta será armazenada, juntamente com o URL de Olá nos registos de acesso.

###<a name="custom-log-field-1"></a>Campo de registo personalizado 1
**Objetivo:** determina o formato de Olá e conteúdo Olá que será atribuído o campo de registo personalizado toohello num ficheiro de registo não processados.

objetivo principal de Olá atrás este campo personalizado é tooallow toodetermine os valores de cabeçalho de pedido e resposta serão armazenados nos seus ficheiros de registo.

Por predefinição, o campo de registo personalizado Olá é chamado "x-ec_custom-1." No entanto, o nome de Olá deste campo pode ser personalizado do [página de definições de registo em bruto]().

Olá formatação que deve utilizar cabeçalhos de pedido e resposta toospecify está definido abaixo.

Tipo de cabeçalho|formato|Exemplos
-|-|-
Cabeçalho de pedido|%{[RequestHeader]()}[i]() | % {Aceitar codificação} i <br/> {Referenciador} i <br/> % {Autorização} i
Cabeçalho de Resposta|%{[ResponseHeader]()}[Nã]()| O % {idade} <br/> O % {content-Type} <br/> O % {cookie}

Informações da chave:

- Um campo de registo personalizado pode conter qualquer combinação de campos de cabeçalho e texto simples.
- Os carateres válidos para este campo incluem o seguinte Olá: alfanuméricos (ou seja, 0-9, a-z e A-Z), travessões, vírgula, ponto e vírgula, apostrophes, vírgulas, períodos, carateres de sublinhado, sinais de igual, parênteses, parênteses Retos e espaços. Olá símbolo de percentagem e chavetas só são permitidas quando utilizado toospecify um campo de cabeçalho.
- ortografia Olá para cada campo de cabeçalho especificado tem de corresponder ao nome de cabeçalho de pedido/resposta pretendido Olá.
- Se gostaria toospecify vários cabeçalhos, e é recomendado que utilize um separador tooindicate cada cabeçalho. Por exemplo, pode utilizar uma abreviatura para cada cabeçalho. Sintaxe de exemplo é fornecida abaixo.
    - AE: % {aceitar codificação} i r: % {autorização} i Cionar: o % {Content-Type} 

**Valor predefinido:** -

###<a name="log-query-string"></a>Cadeia de consulta de registo
**Objetivo:** determina se uma cadeia de consulta será armazenada, juntamente com o URL de Olá nos registos de acesso.

Valor|resultado
-|-
Ativado|Permite o armazenamento de Olá de cadeias de consulta quando gravar URLs no registo de acesso. Se um URL contém uma cadeia de consulta, em seguida, esta opção só terá um efeito.
Desativado|Restaura o comportamento predefinido de Olá. comportamento predefinido de Olá é tooignore cadeias de consulta ao gravar os URLs no registo de acesso.

**Comportamento predefinido:** desativado.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Origem

Estas funcionalidades são toocontrol designado como Olá CDN comunica com um servidor de origem.

Nome | Objetivo
-----|--------
Máximo de pedidos de ligação Keep-Alive | Define o número máximo de Olá de pedidos para uma ligação Keep-Alive antes de que está fechado.
Cabeçalhos especiais de proxy | Define o conjunto de Olá dos cabeçalhos de pedido de CDN específicos que serão reencaminhados de um servidor de origem do contorno servidor tooan.


###<a name="maximum-keep-alive-requests"></a>Máximo de pedidos de ligação Keep-Alive
**Objetivo:** define o número máximo de Olá de pedidos para uma ligação Keep-Alive antes de que está fechado.

Definir o número máximo de Olá de valor baixo do pedidos tooa é vivamente desaconselhável e pode resultar numa degradação do desempenho.

Informações da chave:

- Especificar este valor como um número inteiro de todo.
- Não incluir vírgulas ou períodos Olá especificado valor.

**Valor predefinido:** 10 000 pedidos

###<a name="proxy-special-headers"></a>Cabeçalhos especiais de proxy
**Objetivo:** define conjunto Olá de [cabeçalhos de pedido específicos CDN]() que serão reencaminhados de um servidor de origem do contorno servidor tooan.

Informações da chave:

- Cada cabeçalho de pedido de CDN específica definido nesta funcionalidade será reencaminhado tooan servidor de origem.
- Impedi que um cabeçalho de pedido específicos CDN reencaminhados tooan servidor de origem, removendo-os desta lista.

**Comportamento predefinido:** todos os [cabeçalhos de pedido específicos CDN]() serão reencaminhados toohello servidor de origem.

## <a name="specialty"></a>Specialty

Estas funcionalidades oferecem funcionalidades avançadas que apenas devem ser utilizada por utilizadores avançados.

Nome | Objetivo
-----|--------
Métodos de HTTP colocáveis | Determina o conjunto de Olá de métodos HTTP adicionais que podem ser colocadas em cache na nossa rede.
Tamanho do corpo do pedido colocáveis | Define o limiar de Olá para determinar se uma resposta POST pode ser colocadas em cache.

###<a name="cacheable-http-methods"></a>Métodos de HTTP colocáveis
**Objetivo:** determina o conjunto de Olá de métodos HTTP adicionais que podem ser colocadas em cache na nossa rede.

Informações da chave:

- Esta funcionalidade parte do princípio de que GET respostas devem sempre ser colocado em cache. Como resultado, Olá método obter HTTP não deve estar incluído quando definir esta funcionalidade.
- Esta funcionalidade só suporta o método de POST HTTP Olá. Ativar o caching de resposta POST ao definir esta funcionalidade para: POST 
- Por predefinição, apenas os pedidos cujo corpo é menor do que 14 Kb irão ser colocadas em cache. Utilize a funcionalidade de tamanho de corpo do pedido colocáveis para definir o tamanho do corpo do pedido máximo Olá.

**Comportamento predefinido:** apenas respostas GET serão colocadas em cache.

###<a name="cacheable-request-body-size"></a>Tamanho do corpo do pedido colocáveis

**Objetivo:** define o limiar de Olá para determinar se uma resposta POST pode ser colocadas em cache.

Este limiar é determinado através da especificação de um tamanho do corpo do pedido máximo. Não serão possível em cache pedidos que contêm um grande corpo do pedido.

Informações da chave:

- Esta funcionalidade só é aplicável quando as respostas POST são elegíveis para colocar em cache. Utilize Olá colocáveis funcionalidade de métodos de HTTP para ativar a colocação em cache de pedido POST.
- corpo do pedido Olá é levado em consideração para:
    - valores x-www-form-urlencoded
    - Garantir uma chave exclusiva de cache
- Definir o tamanho do corpo um grande pedido máximo pode afetar o desempenho de entrega de dados.
    - **Valor recomendado:** 14 Kb
    - **Valor mínimo:** 1 Kb

**Comportamento predefinido:** 14 Kb
 
## <a name="url"></a>URL

Estas funcionalidades permitem uma toobe pedido redirecionado ou foi reescrita tooa outro URL.

Nome | Objetivo
-----|--------
Seguir redirecionamentos | Determina se os pedidos poderão ser hostname toohello redirecionada definida no cabeçalho de localização de Olá devolvido por um servidor de origem do cliente.
URL de redirecionamento | Redireciona pedidos através do cabeçalho de localização de Olá.
URL reescrever  | Reescreve Olá URL do pedido.

###<a name="follow-redirects"></a>Seguir redirecionamentos
**Objetivo:** determina se os pedidos poderão ser hostname toohello redirecionada definida no cabeçalho de localização devolvido por um servidor de origem do cliente.

Informações da chave:

- Pedidos só podem ser redirecionada tooedge CNAMEs que correspondem toohello mesma plataforma.

Valor|resultado
-|-
Ativado|Os pedidos podem ser redirecionados.
Desativado|Pedidos não serão redirecionados.

**Comportamento predefinido:** desativado.
###<a name="url-redirect"></a>URL de redirecionamento
**Objetivo:** redireciona pedidos através do cabeçalho de localização.

configuração de Olá desta funcionalidade requer a definição Olá seguintes opções:

Opção|Descrição
-|-
Código|Selecione o código de resposta de Olá que vai ser devolvido toohello autor do pedido.
Origem & padrão| Estas definições, defina um padrão URI do pedido que identifica o tipo de Olá de pedidos que podem ser redirecionados. Serão redirecionados apenas pedidos cujo URL satisfaça ambos Olá os seguintes critérios: <br/> <br/> **Origem:** (ou ponto de acesso ao conteúdo) selecione um caminho relativo que identifica um servidor de origem. Esta é a secção de "/XXXX/" Olá e o nome do ponto final. <br/> **Origem (padrão):** um padrão que identifica pedidos pelo caminho relativo tem de ser definido. Neste padrão de expressão regular tem de definir um caminho que inicia diretamente após Olá selecionado anteriormente o ponto de acesso ao conteúdo (consultar acima). <br/> -Certifique-se de que os critérios URI de pedido hello (ou seja, origem & padrão) definido acima não entra em conflito com quaisquer condições de correspondência definidas para esta funcionalidade. <br/> -Certifique-se de que toospecify um padrão. Utilizar um valor em branco como padrão Olá só irá corresponder à pasta raiz de toohello de pedidos do servidor de origem selecionado Olá (por exemplo, http://cdn.mydomain.com/).
Destino| Definir o URL de Olá toowhich Olá acima pedidos será redirecionado. <br/> Dinamicamente construir este URL a utilizar: <br/> -Um padrão de expressão regular <br/>-Variáveis HTTP <br/> Substitua os valores de Olá capturados num padrão de origem Olá para padrão de destino Olá utilizando $ _n_  onde  _n_  identifica um valor por ordem de Olá em que foi capturada. Por exemplo, $1 representa o primeiro valor de Olá capturado num padrão de origem Olá, enquanto $2 representa o segundo valor de Olá. <br/> 
É altamente recomendado toouse um URL absoluto. utilização de Olá de um URL relativo pode redirecionar caminho inválido do tooan URLs da CDN.

**Cenário de exemplo**

Neste exemplo, vamos demonstrar como tooredirect um limite de URL de CNAME que resolve toothis base CDN URL: http://marketing.azureedge.net/brochures

Elegíveis pedidos será redirecionado toothis edge base CNAME URL: http://cdn.mydomain.com/resources

Redirecionamento este URL pode ser conseguido através de Olá a seguinte configuração:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Pontos de chave:**

- a funcionalidade de URL de redirecionamento Olá define Olá pedido URLs que serão redirecionados. Como resultado, as condições de correspondência adicionais não são necessárias. Embora a condição de correspondência de Olá foi definida como "Sempre", apenas pedidos toohello esse ponto "brochures" pasta na origem de cliente "marketing" Olá será redirecionada. 
- Todos os pedidos correspondentes serão edge toohello redirecionada que URL de CNAME definido na opção de destino. 
    - Cenário de exemplo #1: 
        - Exemplo de pedido (CDN URL): http://marketing.azureedge.net/brochures/widgets.pdf 
        - O URL de pedido (após o redirecionamento): http://cdn.mydomain.com/resources/widgets.pdf  
    - Cenário de exemplo #2: 
        - Exemplo de pedido (Edge CNAME URL): http://marketing.mydomain.com/brochures/widgets.pdf 
        - O URL de pedido (após o redirecionamento): http://cdn.mydomain.com/resources/widgets.pdf cenário de exemplo
    - Cenário de exemplo #3: 
        - Exemplo de pedido (Edge CNAME URL): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - O URL de pedido (após o redirecionamento): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- variável de esquema pedido (% {esquema}) Olá foi utilizado na opção de destino. Isto garante que o esquema desse pedido Olá permanece inalterada após o redirecionamento.
- os segmentos de URL Olá que foram capturados pedido Olá são toohello anexado novo URL através de "$1."
 
###<a name="url-rewrite"></a>URL reescrever
**Objetivo:** reescreve Olá URL do pedido.

Informações da chave:

- configuração de Olá desta funcionalidade requer a definição Olá seguintes opções:

Opção|Descrição
-|-
 Origem & padrão | Estas definições, defina um padrão URI do pedido que identifica o tipo de Olá de pedidos que podem ser foi reescrita. Irão ser foi reescritos apenas pedidos cujo URL satisfaça ambos Olá os seguintes critérios: <br/>     - **Origem (ou ponto de acesso ao conteúdo):** selecione um caminho relativo que identifica um servidor de origem. Esta é a secção de "/XXXX/" Olá e o nome do ponto final. <br/> - **Origem (padrão):** um padrão que identifica pedidos pelo caminho relativo tem de ser definido. Neste padrão de expressão regular tem de definir um caminho que inicia diretamente após Olá selecionado anteriormente o ponto de acesso ao conteúdo (consultar acima). <br/> Certifique-se de que Olá pedido URI critérios (ou seja, origem & padrão) definidos acima não entra em conflito com qualquer uma das condições de correspondência de Olá definidas para esta funcionalidade. Certifique-se de que toospecify um padrão. Utilizar um valor em branco como padrão Olá só irá corresponder à pasta raiz de toohello de pedidos do servidor de origem selecionado Olá (por exemplo, http://cdn.mydomain.com/). 
 Destino  |Definir um URL relativo Olá irá ser foi reescrita toowhich Olá acima pedidos por: <br/>    1. Selecionar um ponto de acesso ao conteúdo que identifica um servidor de origem. <br/>    2. Definir a utilizar um caminho relativo: <br/>        -Um padrão de expressão regular <br/>        -Variáveis HTTP <br/> <br/> Substitua os valores de Olá capturados num padrão de origem Olá para padrão de destino Olá utilizando $ _n_  onde  _n_  identifica um valor por ordem de Olá em que foi capturada. Por exemplo, $1 representa o primeiro valor de Olá capturado num padrão de origem Olá, enquanto $2 representa o segundo valor de Olá. 
 Esta funcionalidade permite nossos servidores edge toorewrite Olá URL sem efetuar um redirecionamento tradicional. Isto significa que solicitador Olá receberá Olá resposta mesma código como se tivesse sido pedido a Olá foi reescrita URL.

**Cenário de exemplo 1**

Neste exemplo, vamos demonstrar como tooredirect um limite de URL de CNAME que resolve toothis base CDN URL: http://marketing.azureedge.net/brochures/

Elegíveis pedidos será redirecionado toothis edge base CNAME URL: http://MyOrigin.azureedge.net/resources/

Redirecionamento este URL pode ser conseguido através de Olá a seguinte configuração:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Cenário de exemplo 2**

Neste exemplo, vamos demonstrar como tooredirect contorno CNAME URL de maiúsculas toolowercase utilizando expressões regulares.

Redirecionamento este URL pode ser conseguido através de Olá a seguinte configuração:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Pontos de chave:**

- a funcionalidade de URL Rewrite Olá define Olá URLs que irão ser foi reescritos do pedido. Como resultado, as condições de correspondência adicionais não são necessárias. Embora a condição de correspondência de Olá foi definida como "Sempre", apenas pedidos toohello esse ponto "brochures" pasta na origem de cliente "marketing" Olá, irá ser foi de reescrita.

- os segmentos de URL Olá que foram capturados pedido Olá são toohello anexado novo URL através de "$1."



###<a name="compatibility"></a>Compatibilidade

Esta funcionalidade inclui correspondentes aos critérios que devem ser satisfeitos antes de ser aplicados tooa pedido. Em ordem tooprevent configurar critérios de correspondência em conflito, esta funcionalidade é incompatível com Olá seguintes condições de correspondência:

- COMO número
- Origem da CDN
- Endereço IP do cliente
- Origem de cliente
- Esquema de pedido
- Diretório de caminho de URL
- Extensão de caminho de URL
- Nome de ficheiro de caminho de URL
- Literal de caminho de URL
- Regex de caminho de URL
- Caminho de URL com carateres universais
- Literal de consulta de URL
- Parâmetro de consulta de URL
- Regex de consulta de URL
- Consulta de URL com carateres universais


## <a name="next-steps"></a>Passos Seguintes
* [Referência do motor de regras](cdn-rules-engine-reference.md)
* [Expressões condicionais de motor de regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Condições de correspondência do motor de regras](cdn-rules-engine-reference-match-conditions.md)
* [Substituir o comportamento HTTP predefinido utilizando o motor de regras de Olá](cdn-rules-engine.md)
* [Descrição geral da CDN do Azure](cdn-overview.md)
